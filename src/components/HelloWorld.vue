<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
  </div>
  <draggable
    :list="myArray"
    @start="drag = true"
    @end="drag = false"
    item-key="id"
    v-bind="dragOptions"
    handle=".handle"
  >
    <template #item="{ element, index }">
      <div class="list-group-item">
        <span class="handle"> mdi-drag-horizontal-variant </span>
        <span class="text">{{ element.name + index }} </span>
      </div>
    </template>
  </draggable>
</template>

<script lang="ts">
import { defineComponent, ref, reactive } from "vue";
import draggable from "vuedraggable";

export default defineComponent({
  name: "HelloWorld",
  props: {
    msg: String,
  },
  components: {
    draggable,
  },
  setup() {
    const myArray = reactive([
      { name: "1だよ", id: 0 },
      { name: "2だよ", id: 1 },
      { name: "3だよ", id: 2 },
      { name: "4だよ", id: 3 },
      { name: "5だよ", id: 4 },
      { name: "6だよ", id: 5 },
    ]);

    const drag = ref(false);
    return { myArray, drag };
  },
  computed: {
    dragOptions() {
      return {
        animation: 200,
        group: "description",
        disabled: false,
        ghostClass: "ghost",
      };
    },
  },
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.ghost {
  opacity: 0.75;
  background: #c8ebfb;
}
.list-group-item {
  padding: 5px;
  border-bottom: solid #000000 1px;
}
.handle {
  cursor: move;
}
</style>
