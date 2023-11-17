<template>
  <button
    :class="{
      button: true,
      button_topLeft: isPositionTopLeft,
      button_topRight: isPositionTopRight,
      button_bottomLeft: isPositionBottomLeft,
      button_bottomRight: isPositionBottomRight,
      active: isActive,
    }"
    @click="sendSound()"
  ></button>
</template>

<script>
export default {
  name: "ButtonQuarterCircle",
  data() {
    return {
      sound: new Audio(`./sounds/${this.say.sound}`),
      extraSound: new Audio(`./sounds/${this.say.sound}`),
      isSendSound: false,
      isActive: false,
    };
  },
  props: {
    say: Object,
    current: Number,
    isPositionTopLeft: {
      type: Boolean,
      default: function () {
        return false;
      },
    },
    isPositionTopRight: {
      type: Boolean,
      default: function () {
        return false;
      },
    },
    isPositionBottomLeft: {
      type: Boolean,
      default: function () {
        return false;
      },
    },
    isPositionBottomRight: {
      type: Boolean,
      default: function () {
        return false;
      },
    },
  },
  watch: {
    current(value) {
      if (Math.abs(value) === this.say.id) {
        this.play();
        this.isActive = true;

        setTimeout(() => {
          this.isActive = false;
        }, 300);
      }
    },
  },
  methods: {
    sendSound() {
      this.play();
      this.$emit("idPressed", this.say.id);
    },

    play() {
      if (!this.isSendSound) {
        this.sound.play();
        this.isSendSound = true;
      } else {
        this.extraSound.play();
        this.isSendSound = false;
      }
    },
  },
};
</script>

<style scoped>
.button {
  width: 148px;
  height: 145px;
  opacity: 0.6;
}

.button_topLeft {
  background-color: dodgerblue;
  border-top-left-radius: 148px;
}

.button_topRight {
  background-color: #ff5643;
  border-top-right-radius: 148px;
}

.button_bottomLeft {
  background-color: #feef33;
  border-bottom-left-radius: 148px;
}

.button_bottomRight {
  background-color: #bede15;
  border-bottom-right-radius: 148px;
}

.button_topLeft:hover,
.button_topRight:hover,
.button_bottomLeft:hover,
.button_bottomRight:hover {
  border: 2px solid black;
}

.button_topLeft:hover {
  border-right: 0;
  border-bottom: 0;
}

.button_topRight:hover {
  border-left: 0;
  border-bottom: 0;
}

.button_bottomLeft:hover {
  border-top: 0;
  border-right: 0;
}

.button_bottomRight:hover {
  border-top: 0;
  border-left: 0;
}

.active,
.button_topLeft:active,
.button_topRight:active,
.button_bottomLeft:active,
.button_bottomRight:active {
  opacity: 1;
}
</style>
