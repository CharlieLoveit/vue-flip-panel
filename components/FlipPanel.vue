<template>
<div :class="['panel-container', {'panel-border': border}, 
                {'panel-rounded': rounded}, 
                {'panel-shadow': shadow}]" 
      :style="{width: width}">
  <div :class="[ 'content', {flipped: isFlipped}]" :style="{height: height}">
    <div class="content-face content-face-front" :style="{'background-color': frontColor}">
      <slot name="front"></slot>
    </div>
    <div class="content-face content-face-back" :style="{'background-color': backColor}">
      <slot name="back"></slot>
    </div>
  </div>
  <div class="flip-navigation">
      <span @click="flipPanel">
        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"><path d="M12 0c-3.31 0-6.291 1.353-8.459 3.522l-2.48-2.48-1.061 7.341 7.437-.966-2.489-2.488c1.808-1.808 4.299-2.929 7.052-2.929 5.514 0 10 4.486 10 10s-4.486 10-10 10c-3.872 0-7.229-2.216-8.89-5.443l-1.717 1.046c2.012 3.803 6.005 6.397 10.607 6.397 6.627 0 12-5.373 12-12s-5.373-12-12-12z"/></svg>
      </span>
  </div>
</div>
</template>

<script>
export default {
  data() {
    return {
      isFlipped: false
    }
  },
  props: {
    shadow: {
      type: Boolean,
      default: false
    },
    rounded: {
      type: Boolean,
      default: false
    },
   border: {
      type: Boolean,
      default: true
    },
    width: {
      type: String,
      default: '250px'
    },
    height: {
      type: String,
      default: '400px'
    },
    frontColor: {
      type: String,
      default: '#ffffff'
    },
    backColor: {
      type: String,
      default: '#ffffff'
    }
  },
  methods: {
    flipPanel() {
      this.isFlipped = !this.isFlipped;
    }
  }
};
</script>

<style scoped>
.panel-container {
  perspective: 600px;
}

.content {
  width: 100%;
  position: relative;
  transition: transform 1s;
  transform-origin: center right;
  transform-style: preserve-3d;
}

.content-face {
  position: absolute;
  height: 100%;
  width: 100%;
  backface-visibility: hidden;
}

.content-face-back {
  transform: rotateY(180deg);
}

.content.flipped {
  transform: translateX(-100%) rotateY(-180deg);
}

.flip-navigation {
  text-align: center;
  padding: 5px;
}
.flip-navigation > span {
    cursor: pointer;
}

.flip-navigation > span >svg:hover {
	-webkit-animation: rotate-center 0.6s ease-in-out reverse both;
	        animation: rotate-center 0.6s ease-in-out reverse both;
}

/* ----------------------------------------------
 * Generated by Animista on 2019-2-4 15:40:44
 * w: http://animista.net, t: @cssanimista
 * ---------------------------------------------- */

/**
 * ----------------------------------------
 * animation rotate-center
 * ----------------------------------------
 */
@-webkit-keyframes rotate-center {
  0% {
    -webkit-transform: rotate(0);
            transform: rotate(0);
  }
  100% {
    -webkit-transform: rotate(360deg);
            transform: rotate(360deg);
  }
}
@keyframes rotate-center {
  0% {
    -webkit-transform: rotate(0);
            transform: rotate(0);
  }
  100% {
    -webkit-transform: rotate(360deg);
            transform: rotate(360deg);
  }
}

.panel-border {
  border: 1px solid #CAD3C8;
}
.panel-rounded {
  border-radius: 11px;
}
.panel-shadow {
  -webkit-box-shadow: 4px 4px 15px -3px rgba(99,110,114,1);
  -moz-box-shadow: 4px 4px 15px -3px rgba(99,110,114,1);
  box-shadow: 4px 4px 15px -3px rgba(99,110,114,1);
}
</style>
