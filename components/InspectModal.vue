<template>
  <div class="container" v-on:click.self="$emit('close')">
    <div class="modal">
      <div class="html-block">
        <p class="bar">
          <span class="label">HTML</span>
          <span class="copy" v-clipboard="() => src.html" v-clipboard:success="onHtmlCopy">
            COPY
            <transition name="copied">
              <svg v-show="htmlCopied" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24">
                <polyline points="20 6 9 17 4 12"></polyline>
              </svg>
            </transition>
          </span>
        </p>
        <pre v-highlightjs><code class="html">{{ src.html }}</code></pre>
      </div>

      <div class="css-block">
        <p class="bar">
          <span class="label">CSS</span>
          <span class="copy" v-clipboard="() => src.css" v-clipboard:success="onCssCopy">
            COPY
            <transition name="copied">
              <svg v-show="cssCopied" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24">
                <polyline points="20 6 9 17 4 12"></polyline>
              </svg>
            </transition>
          </span>
        </p>
        <pre v-highlightjs><code class="css">{{ src.css }}</code></pre>
      </div>
    </div>

    <svg
      v-on:click="$emit('close')"
      class="modal__close"
      xmlns="http://www.w3.org/2000/svg"
      viewBox="0 0 24 24"
    >
      <line x1="18" y1="6" x2="6" y2="18"></line>
      <line x1="6" y1="6" x2="18" y2="18"></line>
    </svg>
  </div>
</template>

<script>
export default {
  props: ["src"],
  data() {
    return {
      htmlCopied: false,
      cssCopied: false
    };
  },
  methods: {
    onHtmlCopy() {
      this.htmlCopied = true;
      this.cssCopied = false;
    },
    onCssCopy() {
      this.cssCopied = true;
      this.htmlCopied = false;
    }
  }
};
</script>


<style lang="scss" scoped>
.container {
  z-index: 100;
  overflow: auto;
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: hsla(0, 0%, 0%, 0.3);
  padding: 4em 0;
  display: flex;
}

.modal__close {
  position: fixed;
  top: 2em;
  right: 2em;
  width: 1.75em;
  fill: none;
  stroke: white;
  opacity: 0.75;
  stroke-width: 2;
  stroke-linecap: round;
  stroke-linejoin: round;

  transition: opacity 0.1s linear;
  &:hover {
    cursor: pointer;
    opacity: 1;
  }
}

.modal {
  margin: auto;
  padding: 2em 3em;
  background-color: hsl(243, 60%, 8%);
  max-width: 90%;
  display: flex;
  flex-flow: column nowrap;
}

pre {
  background-color: hsla(246, 45%, 15%, 0.2);
  padding: 2em;
  overflow: auto;
}

code {
  font-size: 0.9em;
  line-height: 1.4;
  color: hsla(0, 0%, 100%, 0.9);
  font-family: "Roboto Mono", monospace;
}

.html-block {
  margin-bottom: 2em;
}

.bar {
  display: flex;
  flex-flow: row nowrap;
  justify-content: space-between;
  align-items: flex-end;
  margin-bottom: 0.75em;
}

.copy {
  font-size: 0.8em;
  color: white;
  display: flex;
  flex-flow: row nowrap;
  align-items: center;

  &:hover {
    cursor: pointer;
  }

  svg {
    width: 1.5em;
    margin-left: 0.5em;
    fill: none;
    stroke: #3cefff;
    stroke-width: 2;
    stroke-linecap: round;
    stroke-linejoin: round;
    transform-origin: center;
  }
}

.copied-enter-active {
  animation: copied 0.5s linear forwards;
}

@keyframes copied {
  0% {
    opacity: 0;
    transform: scale(1);
  }
  50% {
    transform: scale(1.5);
  }
  100% {
    opacity: 1;
    transform: scale(1);
  }
}
</style>
