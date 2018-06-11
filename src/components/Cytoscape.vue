<template>
  <div class="cytoscape"></div>
</template>
<style>
</style>
<script>
import cytoscape from "cytoscape";
export default {
  name: "Cytoscape",
  props: ["cyStyle", "cyLayout"],
  data() {
    return {
      cy: {
        elements: [
          {
            // node a
            data: { id: "a" }
          },
          {
            // node b
            data: { id: "b" }
          },
          {
            // edge ab
            data: { id: "ab", source: "a", target: "b" }
          }
        ],
        style: [
          {
            selector: "node",
            style: {
              "background-color": "#666",
              label: "data(id)"
            }
          },
          {
            selector: "edge",
            style: {
              width: 3,
              "line-color": "#ccc",
              "target-arrow-color": "#ccc",
              "target-arrow-shape": "triangle"
            }
          }
        ],
        layout: {
          name: "grid",
          rows: 1
        }
      }
    };
  },
  methods: {
    renderView: function(newElements) {
      // the only reliable way to do this is to recreate the view
      this.cy = cytoscape({
        container: document.getElementById(this.$el.id),
        elements: newElements,
        style: this.cyStyle,
        layout: this.cyLayout
      });
    }
  },
  mounted: function() {
    this.$emit("created", this);
  }
};
</script>