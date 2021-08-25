<template>
  <div 
    @click="toggleCategory"
    class="dropdown mx-3 category-main"
    :class="{'is-active': toggle}"
  >
    <div class="dropdown-trigger">
      <p aria-haspopup="true" aria-controls="dropdown-menu4">
        <span>Category</span>
        <span class="icon is-small">
          <i class="fas fa-angle-down" aria-hidden="true"></i>
        </span>
      </p>
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
  data() {
    return {
      menuActive: '',
      isActive: 'is-active',
      toggle: false
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
    }
  }
}
</script>

<style scope>
a:link .is-active {
  background-color: #3ec46d;
}

.category-main {
  cursor: pointer;
}
</style>
