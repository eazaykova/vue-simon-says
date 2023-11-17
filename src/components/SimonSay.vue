<template>
  <div class="simon-say">
    <h1 class="simon-say__title">Simon Says</h1>
    <div
      :class="{
        'simon-say__buttons': true,
        disabled: isDisabled,
      }"
    >
      <ButtonQuarterCircle
        isPositionTopLeft
        :say="says[0]"
        :current="current"
        @idPressed="getIdPressed"
      />
      <ButtonQuarterCircle
        isPositionTopRight
        :say="says[1]"
        :current="current"
        @idPressed="getIdPressed"
      />
      <ButtonQuarterCircle
        isPositionBottomLeft
        :say="says[2]"
        :current="current"
        @idPressed="getIdPressed"
      />
      <ButtonQuarterCircle
        isPositionBottomRight
        :say="says[3]"
        :current="current"
        @idPressed="getIdPressed"
      />
    </div>
    <div class="simon-say__general">
      <div class="simon-say__container">
        <h2 class="simon-say__subtitle">Round: {{ round }}</h2>
        <Button @game="game"> {{ isStart ? "Stop" : "Start" }}</Button>
      </div>
      <div class="simon-say__container simon-say__container_left">
        <h2 class="simon-say__subtitle">Game Options:</h2>
        <RadioField
          v-for="time in times"
          :key="time.title"
          :value="time.value"
          name="timeID"
          :title="time.title"
          :isChecked="time.isChecked"
          @getTime="getTime"
        />
      </div>
    </div>
  </div>
</template>

<script>
import ButtonQuarterCircle from "@/components/ui/ButtonQuarterCircle.vue";
import Button from "@/components/ui/Button.vue";
import RadioField from "@/components/ui/RadioField.vue";

export default {
  name: "SimonSay",
  data() {
    return {
      says: [
        { id: 1, sound: "1.mp3" },
        { id: 2, sound: "2.mp3" },
        { id: 3, sound: "3.mp3" },
        { id: 4, sound: "4.mp3" },
      ],
      times: [
        { title: "Easy", value: "1500", isChecked: true },
        { title: "Middle", value: "1000", isChecked: false },
        { title: "Hard", value: "400", isChecked: false },
      ],
      sequence: [],
      round: 0,
      current: 0,
      userClick: [],
      isDisabled: true,
      timer: 1500,
      isStart: false,
      timeouts: [],
    };
  },
  components: { ButtonQuarterCircle, Button, RadioField },
  methods: {
    game() {
      if (this.isStart) {
        this.stop();
      } else {
        this.start();
      }
    },

    start() {
      this.isStart = true;
      this.round++;
      this.current = this.getRandomValue();
      this.sequence.push(this.current);
      this.isDisabled = false;
    },

    stop() {
      this.sequence = [];
      this.userClick = [];
      this.round = 0;
      this.current = 0;
      this.isStart = false;
      this.isDisabled = true;
      this.clearTimeouts();
    },

    getIdPressed(id) {
      this.userClick.push(id);
      let index = this.userClick.length - 1;
      if (this.sequence[index] !== id) {
        alert(`GAME OVER! Your result in round ${this.round - 1}.`);
        this.stop();
        return;
      }

      if (this.sequence.length !== index + 1) {
        return;
      }

      this.userClick = [];
      this.current = 0;
      this.isDisabled = true;
      this.nextRound();
    },

    nextRound() {
      this.round++;
      let newCurrent = this.getRandomValue();
      this.sequence.push(newCurrent);
      this.sequence.forEach((item, index) => {
        this.timeouts.push(
          setTimeout(() => {
            if (item === this.current) {
              this.current = -1 * item;
            } else {
              this.current = item;
            }
            if (index === this.sequence.length - 1) {
              this.isDisabled = false;
            }
          }, this.timer * (index + 1))
        );
      });
    },

    getRandomValue() {
      return Math.floor(Math.random() * 4) + 1;
    },

    getTime(time) {
      this.timer = Number(time);
    },

    clearTimeouts() {
      for (var i = 0; i < this.timeouts.length; i++) {
        clearTimeout(this.timeouts[i]);
      }
      this.timeouts = [];
    },
  },
};
</script>

<style scoped>
.simon-say,
.simon-say__container {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
  -ms-flex-direction: column;
  flex-direction: column;
  -webkit-box-align: center;
  -ms-flex-align: center;
  align-items: center;
}
.simon-say {
  gap: 25px;
}

.simon-say__container_left {
  -webkit-box-align: start;
  -ms-flex-align: start;
  align-items: flex-start;
}

.simon-say__buttons {
  display: -ms-inline-grid;
  display: inline-grid;
  grid-template-columns: repeat(2, 148px);
  grid-template-rows: repeat(2, 145px);
}

.simon-say__buttons > *:nth-child(1) {
  -ms-grid-row: 1;
  -ms-grid-column: 1;
}

.simon-say__buttons > *:nth-child(2) {
  -ms-grid-row: 1;
  -ms-grid-column: 2;
}

.simon-say__buttons > *:nth-child(3) {
  -ms-grid-row: 2;
  -ms-grid-column: 1;
}

.simon-say__buttons > *:nth-child(4) {
  -ms-grid-row: 2;
  -ms-grid-column: 2;
}

.simon-say__title {
  font-size: 2.5em;
}

.simon-say__general {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  gap: 45px;
}

.simon-say__subtitle {
  font-size: 1.5em;
  margin-bottom: 25px;
}

.disabled {
  pointer-events: none;
}
</style>
