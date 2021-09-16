<template>
  <sd-container full>
    <div class="home">
      <sd-grid>
        <sd-cell :sm="6">
          <sd-select
            v-model="repository"
            label="Repository"
          >
            <option value="rsthecom-v2">
              rsthecom-v2
            </option>
            <option value="rewardstyle-v2">
              rewardstyle-v2
            </option>
          </sd-select>
        </sd-cell>
        <sd-cell :sm="6">
          <sd-field
            v-model.trim="branch"
            label="Branch"
            required
          />
        </sd-cell>

        <sd-cell :sm="6">
          <sd-field
            v-model.trim="target"
            label="Target"
            required
          />
        </sd-cell>
      </sd-grid>
      <sd-sheet
        class="home__result"
        theme="dark"
        padded
      >
        <code>@ltk-leeloo deploy {{ repository || 'repository' }}:{{ branch || 'branch' }} to {{ target || 'target' }}</code>
      </sd-sheet>

      <div class="home__actions">
        <sd-button
          theme="dark"
          @click="clear"
        >
          Clear
        </sd-button>
        <sd-button
          :disabled="!isValid"
          @click="copy"
        >
          Copy
        </sd-button>
      </div>
    </div>
    <sd-toast
      v-model:active="toast.active"
      theme="success"
      dismissable
      placement="bottom-left"
    >
      Copied to clipboard.
    </sd-toast>
  </sd-container>
</template>

<script lang="ts">
import {computed, defineComponent, reactive, ref, toRefs} from 'vue';

export default defineComponent({
  name: 'HelloWorld',
  setup() {
    const count = ref(0);
    const state = reactive({
      botName: '@ltk-leeloo',
      repository: 'rsthecom-v2',
      branch: '',
      target: '',
    });
    const toast = reactive({
      active: false,
    });

    const isValid = computed(() => {
      return state.repository && state.branch && state.target ? true : false;
    });

    const botScript = computed(() => {
      if (state.repository && state.branch && state.target) {
        return `${state.botName} deploy ${state.repository}:${state.branch} to ${state.target}`;
      }
      return '';
    });

    const clear = () => {
      state.repository = '';
      state.branch = '';
      state.target = '';
    };

    const copy = () => {
      if(botScript.value) {
        navigator.clipboard.writeText(botScript.value).then(
          () => {
            toast.active = true;
          });
      }
    };
    return {count, ...toRefs(state), botScript, clear, copy, toast, isValid};
  },
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">
.home {
  padding: 40px 0;
  &__actions {
    display:flex;
    justify-content: space-between;
    position: absolute;
    bottom:0;
    left: 0;
    right: 0;
    padding: 16px;
  }
  &__result {
    margin-bottom: 16px;
  }
}
</style>
