<template>
  <div>
    <!--Div que va a tener el v-for para armar cada cajita-->
    <div class="score-container">

      <div v-for="index in completeBoxes" :key="index" class="box-container">
        <div class="box-line line-left"></div>
        <div class="box-line line-top"></div>
        <div class="box-line line-right"></div>
        <div class="box-line line-bottom"></div>
        <div class="box-line line-middle"></div>
      </div>

      <div v-if="partialBox > 0" class="box-container">
        <div class="box-line line-left" v-if="partialBox > 0"></div>
        <div class="box-line line-top" v-if="partialBox > 1"></div>
        <div class="box-line line-right" v-if="partialBox > 2"></div>
        <div class="box-line line-bottom" v-if="partialBox > 3"></div>
        <div class="box-line line-middle" v-if="partialBox > 4"></div>
      </div>

    </div>
  </div>
</template>

<script>
export default {
  props: {
    score: {
      type: Number,
      default: 0
    },
    size: {
      type: Number,
      default: 50
    },
    lineWeight: {
      type: Number,
      default: 3
    },
    lineColor: {
      type: String,
      default: "black"
    },
    direction: {
      type: String,
      default: "row"
    }
  },
  data() {
    return {
      boxSize: {
        width: this.size,
        height: this.size
      },
      completeBoxes: 0,
      partialBox: 0
    }
  },
  computed: {
    boxAmount: function() {
      return Math.ceil(this.score / 5)
    }
  },
  methods: {
    renderBoxes(score) {
      this.completeBoxes = Math.floor(score/5)
      this.partialBox = score % 5
      console.log(this.completeBoxes, this.partialBox)
    }
  },
  mounted() {
    this.renderBoxes(this.score)
  }
}
</script>

<style>
.score-container {
  display: flex;
  gap: 20px;
  flex-direction: v-bind(direction);
}
.box-container {
  position: relative;
  width: v-bind(size + 'px');
  height: v-bind(size + 'px');
}
.box-line {
  position: absolute;
}
.line-left, 
.line-top, 
.line-right, 
.line-bottom, 
.line-middle {
  background-color: v-bind(lineColor);
}
.line-left {
  top: 0;
  left: 0;
  width: v-bind(lineWeight + 'px');
  height: 100%;
}
.line-top {
  top: 0;
  left: 0;
  width: 100%;
  height: v-bind(lineWeight + 'px');
}
.line-right {
  top: 0;
  right: 0;
  width: v-bind(lineWeight + 'px');
  height: 100%;
}
.line-bottom {
  bottom: 0;
  left: 0;
  width: 100%;
  height: v-bind(lineWeight + 'px');
}
.line-middle {
  bottom: 0;
  left: 0;
  width: calc(141.5% - 7px);
  height: v-bind(lineWeight + 'px');
  transform: rotate(-45deg);
  transform-origin: 2% 0%;
}
</style>