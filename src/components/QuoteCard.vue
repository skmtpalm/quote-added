<template>
  <div class="card" @click="handleDeleteQuote">
    <div class="card-content">
      <p class="title" :class="randomFontStyle">
        {{ quote.content }}
      </p>
      <p class="subtitle">
        <span>#{{quote.id}}</span>
        {{ quote.source }}
      </p>
    </div>
  </div>
</template>

<script>
import _ from 'lodash'
import { quoteBus } from '../main';
export default {
  props: ['quote'],
  methods: {
    handleDeleteQuote() {
      console.log('click card')
      quoteBus.$emit('deleteQuote', this.quote.id)
    }
  },
  computed: {
    randomFontStyle() {
      const fontClasses = ['pacifico', 'alfa', 'monoton', 'cabin']
      return _.sample(fontClasses)
    }
  }
}
</script>

<style lang="scss" scoped>
  @import url('https://fonts.googleapis.com/css?family=Alfa+Slab+One|Cabin+Sketch|Monoton|Pacifico');
//   font-family: 'Pacifico', cursive;
// font-family: 'Alfa Slab One', cursive;
// font-family: 'Monoton', cursive;
// font-family: 'Cabin Sketch', cursive;
  .pacifico {
    font-family: 'Pacifico', cursive;
  }
  .alfa {
    font-family: 'Alfa Slab One', cursive;
  }
  .monoton {
    font-family: 'Monoton', cursive;
  }
  .cabin {
    font-family: 'Cabin Sketch', cursive;
  }

</style>
