<template>
<div>
  {{sphere.position.x}},{{sphere.position.y}},{{sphere.position.z}}
  <a-scene>
    <a-sphere
      v-bind:position="spherePositionAttr"
      radius="0.5"
      color="#EF2D5E"
    ></a-sphere>
    <a-plane
      rotation="-90 0 0"
      width="4"
      height="4"
      color="#7BC8A4"
    ></a-plane>
  </a-scene>
</div>
</template>

<script>
require('aframe')
import Leap from 'leapjs'

export default {
  name: 'HelloWorld',
  data () {
    return {
      sphere: {
        position: {
          x: 1,
          y: 1,
          z: -2
        }
      },
      plane: {
        dimensions: {
          width: 4,
          height: 4
        }
      }
    }
  },
  computed: {
    spherePositionAttr () {
      const pos = this.sphere.position
      return `${pos.x} ${pos.y} ${pos.z}`
    }
  },
  mounted () {
    Leap.loop((f) => {
      if (f.hands.length > 0) {
        const sPos = this.sphere.position
        const hPos = f.hands[0].palmPosition
        sPos.x = hPos[0] / 150
        sPos.y = hPos[1] / 150
        sPos.z = hPos[2] / 150
      }
    })
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1,
h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
