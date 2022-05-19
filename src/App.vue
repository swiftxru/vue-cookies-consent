<template>
  <div class="page">
    <div class="container pt-3">
      <h1>Vue Cookies Consent</h1>
      <p>🔥 Nice and clean Vue component to display message about cookies</p>
      <h4>Colors</h4>
      <hr style="opacity: 0.1" />
      <div class="row mb-5">
        <div class="col-md-4">
          <div class="settings__item">
            <input
              type="color"
              class="form-control form-control-color"
              id="colorTitle"
              v-model="colorTitle"
            />
            <label for="colorTitle"> Color of window title </label>
          </div>
          <div class="settings__item">
            <input
              type="color"
              class="form-control form-control-color"
              id="colorDescription"
              v-model="colorDescription"
            />
            <label for="colorDescription"> Color of window description </label>
          </div>
        </div>
        <div class="col-md-4">
          <div class="settings__item">
            <input
              type="color"
              class="form-control form-control-color"
              id="colorButton"
              v-model="colorButton"
            />
            <label for="colorButton"> Color of button text </label>
          </div>
          <div class="settings__item">
            <input
              type="color"
              class="form-control form-control-color"
              id="backgroundWindow"
              v-model="backgroundWindow"
            />
            <label for="backgroundWindow"> Background of window </label>
          </div>
        </div>
        <div class="col-md-4">
          <div class="settings__item">
            <input
              type="color"
              class="form-control form-control-color"
              id="backgroundButton"
              v-model="backgroundButton"
            />
            <label for="backgroundButton"> Background of button </label>
          </div>
          <div class="settings__item">
            <input
              type="color"
              class="form-control form-control-color"
              id="backgroundButtonHover"
              v-model="backgroundButtonHover"
            />
            <label for="backgroundButtonHover">
              Background of button on hover state
            </label>
          </div>
        </div>
      </div>
      <div class="row align-items-center">
        <div class="col-md-10">
          <h4 class="mb-0">Other settings</h4>
        </div>
        <div class="col-md-2 d-flex justify-content-end">
          <button @click="resetState" class="btn btn-primary btn-block">
            Reset state
          </button>
        </div>
      </div>
      <hr style="opacity: 0.1" />
      <div class="row">
        <div class="col-md-4">
          <div class="mb-3">
            <label for="position" class="form-label">Position of window</label>
            <select id="position" class="form-select" v-model="position">
              <option value="top">Top</option>
              <option value="bottom">Bottom</option>
            </select>
          </div>
          <div>
            <label for="saveMethod" class="form-label"
              >Method to save window state after accept</label
            >
            <select id="saveMethod" class="form-select" v-model="saveMethod">
              <option value="ls">localStorage</option>
              <option value="cookies">Cookies</option>
            </select>
          </div>
        </div>
        <div class="col-md-4">
          <div class="mb-3">
            <label for="offsetY" class="form-label"
              >Offset of window by Y in px</label
            >
            <input
              v-model="offsetY"
              type="email"
              class="form-control"
              id="offsetY"
            />
          </div>
          <div>
            <label for="offsetX" class="form-label"
              >Offset of window by X in px</label
            >
            <input
              v-model="offsetX"
              type="email"
              class="form-control"
              id="offsetX"
            />
          </div>
        </div>
        <div class="col-md-4">
          <div>
            <label for="borderRadius" class="form-label"
              >Border radius of window in px</label
            >
            <input
              v-model="borderRadius"
              type="email"
              class="form-control"
              id="borderRadius"
            />
          </div>
          <div class="settings__item mt-5">
            <div class="form-check form-switch">
              <input
                v-model="hasShadow"
                class="form-check-input"
                type="checkbox"
                id="hasShadow"
              />
              <label class="form-check-label" for="hasShadow"
                >Window has shadow</label
              >
            </div>
          </div>
        </div>
      </div>
      <h4 class="mt-4">Text</h4>
      <hr style="opacity: 0.1" />
      <div class="row">
        <div class="col-md-4">
          <label for="textTitle" class="form-label">Title text</label>
          <textarea
            v-model="textTitle"
            class="form-control"
            id="textTitle"
            rows="3"
          ></textarea>
        </div>
        <div class="col-md-4">
          <label for="textDescription" class="form-label"
            >Description text</label
          >
          <textarea
            v-model="textDescription"
            class="form-control"
            id="textDescription"
            rows="3"
          ></textarea>
        </div>
        <div class="col-md-4">
          <label for="textButton" class="form-label">Button text</label>
          <textarea
            v-model="textButton"
            class="form-control"
            id="textButton"
            rows="3"
          ></textarea>
        </div>
      </div>
    </div>
    <vue-cookies-consent
      :color-title="colorTitle"
      :color-description="colorDescription"
      :color-button="colorButton"
      :background-window="backgroundWindow"
      :background-button="backgroundButton"
      :background-button-hover="backgroundButtonHover"
      :has-shadow="hasShadow"
      :border-radius="borderRadius"
      :position="position"
      :offset-y="offsetY"
      :offset-x="offsetX"
      :save-method="saveMethod"
    >
      <template #title>{{ textTitle }}</template>
      <template #description>
        <p v-html="textDescription"></p>
      </template>
      <template #button>{{ textButton }}</template>
    </vue-cookies-consent>
  </div>
</template>

<script>
import VueCookiesConsent from "@/components/VueCookiesConsent";
import Cookies from "js-cookie";
export default {
  name: "App",
  components: { VueCookiesConsent },
  data() {
    return {
      colorTitle: "#1F2030",
      colorDescription: "#4D4D4D",
      colorButton: "#FFFFFF",
      backgroundWindow: "#FFFFFF",
      backgroundButton: "#C11E31",
      backgroundButtonHover: "#de2b40",
      hasShadow: true,
      borderRadius: 16,
      position: "bottom",
      offsetY: 32,
      offsetX: 32,
      saveMethod: "ls",
      textTitle: "Some default title for window",
      textDescription: "Some description in window",
      textButton: "Accept cookies",
    };
  },
  mounted() {
    document.title = "Vue Cookies Consent";
  },
  methods: {
    resetState() {
      localStorage.removeItem("vcc-window");
      Cookies.remove("vcc-window");
      location.reload();
    },
  },
};
</script>

<style lang="scss">
.page {
  margin-bottom: 150px;
}
.settings {
  &__item {
    display: flex;
    align-items: center;
    .form-control {
      margin-right: 16px;
    }
    & + & {
      margin-top: 16px;
    }
  }
}
@media (max-width: 840px) {
  .page {
    margin-bottom: 300px;
  }
}
</style>
