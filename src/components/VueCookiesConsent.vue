<template>
  <div v-if="showWindow" :style="cssVars" :class="windowClasses">
    <div class="vcc-window__grid">
      <div class="vcc-window__content">
        <p class="vcc-window__title" v-if="hasTitleSlot">
          <slot name="title">Default title</slot>
        </p>
        <div v-if="hasDescriptionSlot" class="vcc-window__description">
          <slot name="description">
            Default description on cookies window
          </slot>
        </div>
      </div>
      <div class="vcc-window__action">
        <button
          @click="buttonClickHandler"
          type="button"
          class="vcc-window__btn"
        >
          <slot name="button">Accept cookies</slot>
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import Cookies from "js-cookie";
export default {
  name: "VueCookiesConsent",
  props: {
    /**
     * Color of window title
     */
    colorTitle: {
      type: String,
      default: "#1F2030",
    },
    /**
     * Color of window description
     */
    colorDescription: {
      type: String,
      default: "#4D4D4D",
    },
    /**
     * Color of button text
     */
    colorButton: {
      type: String,
      default: "#FFF",
    },
    /**
     * Background of window
     */
    backgroundWindow: {
      type: String,
      default: "#FFF",
    },
    /**
     * Background of button
     */
    backgroundButton: {
      type: String,
      default: "#C11E31",
    },
    /**
     * Background of button on hover state
     */
    backgroundButtonHover: {
      type: String,
      default: "#de2b40",
    },
    /**
     * Window has shadow
     */
    hasShadow: {
      type: Boolean,
      default: true,
    },
    /**
     * Border radius of window in px
     */
    borderRadius: {
      type: Number,
      default: 16,
    },
    /**
     * Position of window
     * @values top, bottom
     */
    position: {
      type: String,
      default: "bottom",
    },
    /**
     * Offset of window by Y in px
     */
    offsetY: {
      type: Number,
      default: 32,
    },
    /**
     * Offset of window by X in px
     */
    offsetX: {
      type: Number,
      default: 32,
    },
    /**
     * Method to save window state after accept
     * @values ls, cookies
     */
    saveMethod: {
      type: String,
      default: "ls",
    },
  },
  computed: {
    cssVars() {
      return {
        "--color-title": this.colorTitle,
        "--color-description": this.colorDescription,
        "--color-button": this.colorButton,
        "--background-window": this.backgroundWindow,
        "--background-button": this.backgroundButton,
        "--background-button-hover": this.backgroundButtonHover,
        "--border-radius": `${this.borderRadius}px`,
        "--offset-y": `${this.offsetY}px`,
        "--offset-x": `${this.offsetX}px`,
      };
    },
    windowClasses() {
      return [
        "vcc-window",
        {
          "vcc-window--shadow": this.hasShadow,
          "vcc-window--top": this.position === "top",
        },
      ];
    },
    hasTitleSlot() {
      return this.$slots.title;
    },
    hasDescriptionSlot() {
      return this.$slots.description;
    },
  },
  methods: {
    buttonClickHandler() {
      this.$emit("accept");
      if (this.saveMethod === "ls") {
        this.$emit("ls-saved");
        localStorage.setItem("vcc-window", "hide");
      }
      if (this.saveMethod === "cookies") {
        this.$emit("cookies-saved");
        Cookies.set("vcc-window", "hide", { expires: 7, path: "*" });
      }
      this.showWindow = false;
      this.$emit("hidden");
    },
  },
  data() {
    return {
      showWindow: true,
    };
  },
  created() {
    if (this.saveMethod === "cookies") {
      const cookiesHideWindow = Cookies.get("vcc-window");
      if (cookiesHideWindow && cookiesHideWindow === "hide") {
        this.showWindow = false;
      } else {
        this.$emit("shown");
      }
    } else if (this.saveMethod === "ls") {
      const lsHideWindow = localStorage.getItem("vcc-window");
      if (lsHideWindow && lsHideWindow === "hide") {
        this.showWindow = false;
      } else {
        this.$emit("shown");
      }
    } else {
      this.$emit("shown");
    }
  },
};
</script>

<style>
.vcc-window {
  margin: 0;
  border: 0;
  font-size: 100%;
  font-family: Calibri, sans-serif;
  vertical-align: baseline;
  position: fixed;
  background: var(--background-window);
  border-radius: var(--border-radius);
  padding: 16px;
  bottom: var(--offset-y);
  left: var(--offset-x);
  right: var(--offset-x);
  box-sizing: border-box;
}

.vcc-window * {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  font-size: 100%;
}

.vcc-window__grid {
  display: grid;
  grid-template-columns: 1fr auto;
  column-gap: 16px;
  align-items: center;
}
.vcc-window__title {
  font-weight: bold;
  font-size: 20px;
  color: var(--color-title);
}
.vcc-window__description {
  font-size: 16px;
  margin-top: 8px;
  color: var(--color-description);
}
.vcc-window__btn {
  display: inline-flex;
  font-weight: 500;
  font-size: 16px;
  color: var(--color-button);
  text-align: center;
  text-decoration: none;
  vertical-align: middle;
  cursor: pointer;
  -webkit-user-select: none;
  -moz-user-select: none;
  user-select: none;
  background-color: var(--background-button);
  border: 1px solid transparent;
  height: 50px;
  align-items: center;
  justify-content: center;
  border-radius: 4px;
  transition: 0.4s ease;
  padding-right: 32px;
  padding-left: 32px;
}
.vcc-window__btn:hover {
  background-color: var(--background-button-hover);
}
.vcc-window--shadow {
  box-shadow: 0 0 20px 3px rgba(31, 32, 48, 0.15);
}
.vcc-window--top {
  top: var(--offset-y);
  bottom: auto;
}
@media (max-width: 840px) {
  .vcc-window__grid {
    flex-direction: column;
    grid-template-columns: auto;
    gap: 16px;
  }
}
</style>
