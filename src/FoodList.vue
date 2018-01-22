<template>
  <section>
    <div class="tags">
      <span 
        class="tag is-light is-medium"
        :class="{'is-success': Object.keys(selectedItems).indexOf(key) >= 0}"
        v-for="(value, key) in foods" 
        :key="key" 
        @click="$emit('selected', key)">{{ value }}</span>

      <span 
        class="tag is-medium"
        :class="{'is-success': Object.keys(selectedItems).indexOf(key) >= 0}"
        v-for="(value, key) in drinks" 
        :key="key" 
        @click="$emit('selected', key)">{{ value }}</span>
      
      <span 
        class="tag is-medium is-success"
        v-for="item in customItems"
        :key="item"
        @click="$emit('selected', item)">{{ item }}</span>

      <span 
        class="tag is-medium"
        :class="{'is-success': isCustomItemVisible}"
        @click="isCustomItemVisible = !isCustomItemVisible">+</span>
    </div>

    <div v-if="isCustomItemVisible" class="field">
      <div class="control">
        <input 
          class="input"
          type="text"
          v-model="customItem"
          placeholder="Pulsa intro para añadirlo"
          @keyup.enter="emitCustomItem(customItem)">
      </div>
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
      },
      isCustomItemVisible: false,
      customItem: ''
    }
  },

  methods: {
    emitCustomItem (customItem) {
      this.$emit('selected', customItem)

      // Close input
      this.isCustomItemVisible = false

      // Empty input for next input opening
      this.customItem = ''
    }
  },

  computed: {
    /**
     * @returns {Array} Items not in foods/drinks list, entered by user
     */
    customItems () {
      let customItems = []

      const foodItems = Object.keys(this.foods)
      const drinkItems = Object.keys(this.drinks)

      Object.keys(this.selectedItems).forEach(item => {
        if (foodItems.indexOf(item) < 0 && drinkItems.indexOf(item) < 0) {
          // If item is not among standards, return as custom
          customItems.push(item)
        }
      })

      return customItems
    }
  }
}
</script>
