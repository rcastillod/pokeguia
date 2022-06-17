<template>
  <div id="app" class="grid">
    <div class="container">
      <pokedata></pokedata>
    </div>
  </div>
</template>

<script>
import PokeData from '@/components/PokeData.vue'

export default {
  name: 'App',
  data: function() {
    return {
      
    }
  },
  components: {
    'pokedata': PokeData
  },
  //methods: {}
  // watch: {},
  // components: {},
  // mixins: [],
  // filters: {},
  // -- Lifecycle Methods
  // -- End Lifecycle Methods
}
</script>

<style>
/* -------------------------------------------------------------------------- */
/*                              CUSTOM PROPERTIES                             */
/* -------------------------------------------------------------------------- */
:root {

    /* Colors */
    --clr-body: hsl(350, 90%, 45%);
    --clr-body-shadow: hsl(351, 89%, 28%);
    --clr-body-shine: hsl(350, 76%, 66%);

    --clr-button-lightblue: hsl(205, 99%, 59%);
    --clr-button-lightblue-shadow: hsl(204, 71%, 36%);
    --clr-button-lightblue-shine: hsl(202, 96%, 81%);

    --clr-button-yellow: hsl(52, 88%, 58%);
    --clr-button-yellow-shadow: hsl(51, 84%, 34%);
    --clr-button-yellow-shine: hsl(51, 97%, 87%);

    --clr-button-green: hsl(131, 32%, 48%);
    --clr-button-green-shadow: hsl(131, 33%, 32%);
    --clr-button-green-shine: hsl(135, 64%, 85%);

    --clr-button-darkgreen: hsl(173, 69%, 11%);
    --clr-button-darkgreen-tint: hsl(174, 67%, 15%);

    --clr-border-grey: hsl(0, 0%, 87%);
    --clr-panel-darkgrey: hsl(0, 0%, 14%);

    --clr-text: ;
    --clr-white: hsl(0, 0%, 100%);
    --clr-black: hsl(0, 0%, 0%);

    /* Font Familiy */
    --body-font: 'VT323', monospace;

    /* Font Weights */
    --fw-regular: 400;


}

/* -------------------------------------------------------------------------- */
/*                                    RESET                                   */
/* -------------------------------------------------------------------------- */

/* https://piccalil.li/blog/a-modern-css-reset/ */

/* Box sizing rules */
*,
*::before,
*::after {
    box-sizing: border-box;
}

/* Remove default margin */
body,
h1,
h2,
h3,
h4,
p,
figure,
blockquote,
dl,
dd {
    margin: 0;
}

/* Remove list styles on ul, ol elements with a list role, which suggests default styling will be removed */
ul[role='list'],
ol[role='list'] {
    list-style: none;
}

ul,
ol {
    margin: 0;
    padding: 0;
    list-style-type: none;
}

/* Set core root defaults */
html,
html:focus-within,
body {
    scroll-behavior: smooth;
}

/* Set core body defaults */
body {
    color: var(--clr-white);
    font-family: var(--body-font);
    min-height: 100%;
    height: 100vh;
    text-rendering: optimizeSpeed;
    line-height: 1.5;
}

/* A elements that don't have a class get default styles */
a:not([class]) {
    text-decoration-skip-ink: auto;
}

/* Make images easier to work with */
img,
picture {
    max-width: 100%;
    display: block;
}

/* Inherit fonts for inputs and buttons */
input,
button,
textarea,
select {
    font: inherit;
}

/* Remove all animations, transitions and smooth scroll for people that prefer not to see them */
@media (prefers-reduced-motion: reduce) {
    html:focus-within {
        scroll-behavior: auto;
    }

    *,
    *::before,
    *::after {
        animation-duration: 0.01ms !important;
        animation-iteration-count: 1 !important;
        transition-duration: 0.01ms !important;
        scroll-behavior: auto !important;
    }
}

/* Custom Scrollbar */
::-webkit-scrollbar {
    width: .3125em;
    height: .3125em;
}
::-webkit-scrollbar-track {
    background-color: var(--clr-black);
    margin-block: .5em;
    margin-inline: .5em;
}
::-webkit-scrollbar-thumb {
    background-color: var(--clr-button-darkgreen);
    border-radius: 5px;
}

/* -------------------------------------------------------------------------- */
/*                               UTILITY CLASSESS                             */
/* -------------------------------------------------------------------------- */

/* General */

.flex {
    display: flex;
    gap: var(--gap, 1rem);
}

.direction-column {
    flex-direction: column;
}

.space-between {
  justify-content: space-between;
}

.align-center {
  align-items: center;
}

.grid {
    display: grid;
    gap: var(--gap, 1rem);
}

.flow > *:where(:not(:first-child)) {
    margin-top: var(--flow-gap, 1rem);
}

.container {
    padding-inline: 2em;
    margin-inline: auto;
    max-width: min(100% - 2rem, 83.75rem);
}

.section-title {
    color: hsl( var(--white-color) );
    font-family: var(--heading-font);
    font-size: 4rem;
    font-weight: var(--fw-bold);
    letter-spacing: .325rem;
    line-height: 1.2;
    max-width: 18ch;
}
.section-title span {
    display: inline-flex;
    align-items: center;
    gap: 0.25em;
    position: relative;
}
.section-title span::after {
    content: '';
    background-color: hsl( var(--white-color) );
    height: 0.4375rem;
    width: 1.175em;
}

.btn {
    font-size: 1rem;
    padding-block: .625em;
    width: 5em;
    text-align: center;
    text-decoration: none;
}

.sr-only {
    position: absolute;
    width: 1px;
    height: 1px;
    padding: 0;
    margin: -1px;
    overflow: hidden;
    clip: rect(0, 0, 0, 0);
    white-space: nowrap;
    border: 0;
}

/* -------------------------------------------------------------------------- */
/*                                  COMPONENT                                 */
/* -------------------------------------------------------------------------- */
#app {
  height: 100%;
  place-items: center;
}
</style>
