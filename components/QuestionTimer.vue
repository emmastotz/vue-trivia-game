<template>
  <div class="relative h-24 w-24 text-white">
    <svg
      class="relative h-24 w-24 transform scale-100"
      viewBox="0 0 100 100"
      xmlns="http://www.w3.org/2000/svg"
    >
      <g class="relative h-24 w-24 circle stroke-0">
        <circle
          class="relative h-24 w-24 path-elapsed stroke-current text-gray-600"
          cx="50"
          cy="50"
          r="45"
        />
        <path
          :stroke-dasharray="circleDasharray"
          class="relative h-24 w-24 path-remaining stroke-current"
          :class="remainingPathColor"
          d="
            M 50, 50
            m -45, 0
            a 45,45 0 1,0 90,0
            a 45,45 0 1,0 -90,0
          "
        />
      </g>
    </svg>
    <span class="relative h-24 w-24 label">{{ formattedTimeLeft }}</span>
  </div>
</template>

<script>
const FULL_DASH_ARRAY = 283;

export default {
  props: {
    alertThreshold: {
      type: Number,
      default: 5
    },

    timeLimit: {
      type: Number,
      required: true
    },

    timeLeft: {
      type: Number,
      required: true
    },

    warningThreshold: {
      type: Number,
      default: 10
    }
  },

  computed: {
    circleDasharray() {
      return `${(this.timeFraction * FULL_DASH_ARRAY).toFixed(0)} 283`;
    },

    colorCodes() {
      return {
        info: {
          color: "green"
        },
        warning: {
          color: "orange",
          threshold: this.warningThreshold
        },
        alert: {
          color: "red",
          threshold: this.alertThreshold
        }
      };
    },

    formattedTimeLeft() {
      const timeLeft = this.timeLeft;
      const minutes = Math.floor(timeLeft / 60);
      let seconds = timeLeft % 60;

      if (seconds < 10) {
        seconds = `0${seconds}`;
      }

      return `${minutes}:${seconds}`;
    },

    timeFraction() {
      const rawTimeFraction = this.timeLeft / this.timeLimit;
      return rawTimeFraction - (1 / this.timeLimit) * (1 - rawTimeFraction);
    },

    remainingPathColor() {
      const { alert, warning, info } = this.colorCodes;

      if (this.timeLeft <= alert.threshold) {
        return alert.color;
      } else if (this.timeLeft <= warning.threshold) {
        return warning.color;
      } else {
        return info.color;
      }
    }
  }
};
</script>

<style scoped lang="postcss">
.circle {
  fill: none;
}

.path-elapsed {
  stroke-width: 7px;
}

.path-remaining {
  stroke-width: 7px;
  stroke-linecap: round;
  transform: rotate(90deg);
  transform-origin: center;
  transition: 1s linear all;
  fill-rule: nonzero;
}

.green {
  color: #0b527a;
}

.orange {
  color: orange;
}

.red {
  color: red;
}

.label {
  position: absolute;
  width: 100px;
  height: 100px;
  top: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 24px;
}
</style>
