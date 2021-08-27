<template>
  <div 
    class="dropdown mx-3 category-main is-hoverable"
    :class="{'mb-toggle': mbToggle}"
  >
    <div class="dropdown-trigger">
      <button  class="button" aria-haspopup="true" aria-controls="dropdown-menu4">
        <span>Category</span>
        <span class="icon is-small">
          <i class="fas fa-angle-down" aria-hidden="true"></i>
        </span>
      </button>
    </div>
    <div class="dropdown-menu" id="dropdown-menu4" role="menu">
      <div class="dropdown-content">
        <template v-for="item in category" :key="item.id">
          <router-link 
            :to="item.slug" 
            class="dropdown-item"
            :class="{'is-active': item.id === menuActive}"
            @click="setActiveMenu(item.id)"
          >
            {{ item.name }}
          </router-link>
        </template>
        <router-link 
          to="/" 
          class="dropdown-item"
          @click="setActiveMenu(null)"
        >
          Show All
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CategoryMenu',
  props: {
    category: Array
  },
  mounted() {
    this.screenSizeCheck()
  },
  data() {
    return {
      menuActive: '',
      isActive: 'is-active',
      toggle: false,
      mbToggle: false
    }
  },
  methods: {
    setActiveMenu(id) {
      this.menuActive = id
    },
    toggleCategory() {
      this.toggle = !this.toggle
    },
    handleMouseLeave() {
      console.log('handleMouseLeave')
    },
    screenSizeCheck() {
      let windowSize = window.screen.width
      if (windowSize <= 1023) {
        this.mbToggle = true
      }
    }
  }
}
</script>

<style scope>
a:link .is-active {
  background-color: #3ec46d;
}

.mb-toggle {
  margin-bottom: 15px;
}

.category-main {
  cursor: pointer;
}
</style>
