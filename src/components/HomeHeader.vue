<template>
  <header class="header is-desktop" v-if="hasNav || currentIcons.length > 0 || hasComponentsAroundIcons">
    <div class="header-container">
      <header-nav
        :current-nav="currentNav"
        :has-nav="hasNav"
        :show-nav="showNav">
      </header-nav>
      <div
        class="header-right"
        v-if="currentIcons.length > 0 || hasComponentsAroundIcons">
        <custom-components place="icons:start" />
        <header-icons
          :current-icons="currentIcons"
          :show-nav="showNav">
        </header-icons>
        <custom-components place="icons:end" />
      </div>
    </div>
  </header>
</template>

<script>
  import { mapGetters } from 'vuex'
  import HeaderNav from 'components/HeaderNav.vue'
  import HeaderIcons from 'components/HeaderIcons.vue'
  import CustomComponents from 'components/CustomComponents'
  import componentManager from 'utils/component-manager'

  export default {
    props: {
      currentIcons: {
        type: Array
      },
      hasNav: {
        type: Boolean
      },
      showNav: {
        type: Boolean
      }
    },
    computed: {
      ...mapGetters(['currentNav']),
      hasComponentsAroundIcons() {
        return componentManager.count('icons:start') > 0 ||
          componentManager.count('icons:end') > 0
      }
    },
    components: {
      HeaderNav,
      HeaderIcons,
      CustomComponents
    }
  }
</script>

<style>
  .header {
    height: 40px;
    border-bottom: 1px solid rgba(0,0,0,.07);
    background-color: white;
    &:empty {
      display: none;
    }
    .header-container {
      display: flex;
      justify-content: space-between;
      align-items: center;
      max-width: 1000px;
      height: 100%;
      margin: 0 auto;
      padding: 0 30px;
    }
  }

  .no-sidebar .header {
    margin: 0 auto;
    max-width: 1000px;
  }

  .header-right {
    display: flex;
    align-items: center;
  }
</style>

<style>
  @media screen and (max-width: 768px) {
    .header {
      padding: 0 10px;
    }
  }
</style>
