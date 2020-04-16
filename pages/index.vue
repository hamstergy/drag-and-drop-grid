<template>
  <div class="container-fluid">
    <h1>Grid Nuxt Component</h1>

    <div class="row p-3">
      <button class="btn btn-success m-1" @click="state.boxCount++">Add Box</button>
      <button class="btn btn-danger m-1" @click="state.boxCount = Math.max(0, state.boxCount-1)">Remove Box</button>
    </div>

    <grid-container
            :layout.sync="state.layout"
            :cellSize="cellSize"
            :maxColumnCount="maxColumnCount"
            :maxRowCount="maxRowCount"
            :margin="margin"
            :bubbleUp="bubbleUp"
    >
      <grid-box
              v-for="number in state.boxCount"
              :boxId="number"
              :key="number"
              dragSelector="div.card-header"
      >
        <div class="card demo-box">
          <div class="card-header">
            <button type="button" class="close" aria-label="Close" @click="removeBox(number)">
              <span aria-hidden="true">&times;</span>
            </button>
          </div>
          <div class="card-body">
            <textarea>Some text</textarea>
          </div>
        </div>
      </grid-box>
    </grid-container>
  </div>
</template>

<style>
  .demo-box {
    width: 100%;
    height: 100%;
  }
  .card-header {
    background-color: white;
    border-bottom: 0px solid white;
  }
  .card-header:hover {
    cursor: -webkit-grab;
    background-color: rgba(0, 0, 0, 0.01);
    border-bottom: 1px solid rgba(0, 0, 0, 0.1);
}
  .dragging .card .card-header:hover {
    cursor: -webkit-grabbing;
    background-color: rgba(0, 0, 0, 0.01);
    border-bottom: 1px solid rgba(0, 0, 0, 0.1);
  }
  .card-body {
    padding: 3px;
  }
  textarea {
    border: none;
    overflow: auto;
    outline: none;

    -webkit-box-shadow: none;
    -moz-box-shadow: none;
    box-shadow: none;

    resize: none;
    width: 100%;
    height:100%;

  }
</style>

<script lang="ts">
  import { Box, Container } from '../components'
  import { reactive } from "@vue/composition-api";

  export default {
    name: 'App',
    components: {
      GridContainer: Container,
      GridBox: Box
    },
    setup() {
      const state = reactive({
        boxCount: 2,
        layout: []
      });
      const cellSize = {w:100, h:100};
      const maxColumnCount = 14;
      const maxRowCount = Infinity;
      const bubbleUp = true;
      const margin = 5;

      function removeBox(index) {
        console.log(index);
        state.layout.splice(state.layout.findIndex((i) => {
          return i.id === 1;
        }), 1);
      }
      return {
        cellSize,
        maxColumnCount,
        maxRowCount,
        bubbleUp,
        margin,
        state,
        removeBox
      }
    },
  }
</script>
