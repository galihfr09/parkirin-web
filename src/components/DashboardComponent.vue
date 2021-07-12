<template>
  <div>
    <q-card bordered class="q-pa-md">
      <q-card-section>
        <q-img src="~assets/parkirin-logo.png"/>
        <p class="text-caption text-center">Park smarter and easier</p>
        <q-input class='q-pa-md' outlined label="Username" />
        <q-input class='q-pa-md' outlined label="Password" />
      </q-card-section>

      <q-card-actions vertical>
        <q-btn flat>Login</q-btn>
        <q-btn flat>Sign Up</q-btn>
      </q-card-actions>
    </q-card>
  </div>
</template>

<script lang="ts">
import {
  defineComponent,
  PropType,
  computed,
  ref,
  toRef,
  Ref,
} from 'vue';
import { Todo, Meta } from './models';

function useClickCount() {
  const clickCount = ref(0);
  function increment() {
    clickCount.value += 1
    return clickCount.value;
  }

  return { clickCount, increment };
}

function useDisplayTodo(todos: Ref<Todo[]>) {
  const todoCount = computed(() => todos.value.length);
  return { todoCount };
}

export default defineComponent({
  name: 'CompositionComponent',
  props: {
    title: {
      type: String,
      required: true
    },
    todos: {
      type: Array as PropType<Todo[]>,
      default: () => []
    },
    meta: {
      type: Object as PropType<Meta>,
      required: true
    },
    active: {
      type: Boolean
    }
  },
  setup(props) {
    return { ...useClickCount(), ...useDisplayTodo(toRef(props, 'todos')) };
  },
});
</script>
