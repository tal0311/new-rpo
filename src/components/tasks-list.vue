<template>
  <Container  orientation="vertical" @drop="onDrop">
    <Draggable  v-for="eltask in eltasks" :key="eltask.id">
      <task-preview :task="eltask" :groupColor="groupColor" :group="group"></task-preview>
    </Draggable>
  </Container>
</template>

<script>
import taskPreview from "./task-preview.vue";
import { Container, Draggable } from "vue3-smooth-dnd";
export default {
  props: {
    tasks: Array,
    group: Object,
    groupColor: String
  },
  data() {
    return {
      eltasks: this.tasks,
    }
  },
  methods: {
    onDrop(dropResult) {
      this.eltasks = this.applyDrag(this.eltasks, dropResult);
    },
    applyDrag(arr, dragResult) {
      const { removedIndex, addedIndex, payload } = dragResult;

      if (removedIndex === null && addedIndex === null) return arr;
      const result = [...arr];
      let taskToAdd = payload;

      if (removedIndex !== null) {
        taskToAdd = result.splice(removedIndex, 1)[0];
      }
      if (addedIndex !== null) {
        result.splice(addedIndex, 0, taskToAdd);
      }
      this.updateGroup(result)

      return result;
    },
    updateGroup(result) {
      const newGroup = JSON.parse(JSON.stringify(this.group))
      newGroup.tasks = JSON.parse(JSON.stringify(result))
      this.$store.dispatch({
          type: 'updateGroup',
          groupToUpdate: newGroup,
      })
    },
  },
  computed: {
    board() {
      
    }
  },
  components: {
    taskPreview,
    Container,
    Draggable,
  },
  created() {
    // this.eltasks = JSON.parse(JSON.stringify(this.tasks))
    // this.eltasks = this.tasks
  },
};
</script>

<style>

</style>
