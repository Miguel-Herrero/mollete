<template>
  <section>
    <div class="tags">
      <span 
        class="tag is-light is-medium"
        :class="{'is-success': Object.keys(selectedItems).indexOf(key) >= 0}"
        v-for="(value, key) in foods" 
        :key="key" 
        @click="$emit('selected', key)">{{ value }}</span>
    </div>

    <div class="tags">
      <span 
        class="tag is-medium"
        :class="{'is-success': Object.keys(selectedItems).indexOf(key) >= 0}"
        v-for="(value, key) in drinks" 
        :key="key" 
        @click="$emit('selected', key)">{{ value }}</span>
    </div>
  </section>
</template>

<script>
export default {
  props: {
    selectedItems: {
      type: Object
    }
  },
  data () {
    return {
      foods: {
        'Barrita': 'Barrita',
        'Mollete': 'Mollete',
        'Tortilla': 'Tortilla',
        'Churros': 'Churros'
      },
      drinks: {
        'Cafe-Solo': 'Café solo',
        'Cafe-Cortado': 'Café cortado',
        'Cafe-con-Leche': 'Café con leche',
        'Zumo': 'Zumo',
        'Cola-Cao': 'Cola-Cao'
      }
    }
  }
}
</script>
