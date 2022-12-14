<template>
  <div class="header">
    <div class="header-container">
      <svg
        v-if="toggleMenuButtonVisible"
        class="toggleMenu"
        @click="toggleMenu"
      >
        <use xlink:href="#icon-menu"></use>
      </svg>
      <router-link to="/" class="logo">
        <span class="can-hide"> Run UI</span>
      </router-link>
      <nav class="nav-links can-hide">
        <div class="nav-item">
          <router-link to="/doc/intro">指南</router-link>
        </div>
        <div class="nav-item">
          <router-link to="/doc/switch">组件</router-link>
        </div>
        <div class="nav-item">
          <a href="https://github.com">
            <svg class="icon">
              <use xlink:href="#icon-github"></use>
            </svg>
            GitHub
          </a>
        </div>
      </nav>
    </div>
  </div>
</template>

<script lang="ts">
import { inject, Ref } from "vue";

export default {
  props: {
    toggleMenuButtonVisible: {
      type: Boolean,
      default: false,
    },
  },
  setup() {
    const menuVisible = inject<Ref<boolean>>("menuVisible");
    const toggleMenu = () => {
      menuVisible.value = !menuVisible.value;
    };
    return { toggleMenu };
  },
};
</script>

<style lang="scss" scoped>
$bg-primary: rgba(255, 255, 255, 0.7);
$border-primary: #e7e9e8;

.header {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 60px;
  z-index: 20;
  background: $bg-primary;
  backdrop-filter: saturate(50%) blur(8px);
  border-bottom: 1px solid $border-primary;

  > .header-container {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100%;
    padding: 0 24px;

    > .logo {
      display: inline-block;
      font-weight: 500;
      text-decoration: none;
      margin-right: auto;

      > svg {
        height: 2.2rem;
        min-width: 2.2rem;
        margin-right: 0.8rem;
        vertical-align: top;
      }

      > span {
        font-size: 1.3rem;
        font-weight: 600;
        color: #502c4e;
        position: relative;
      }
    }

    > .nav-links {
      display: flex;
      white-space: nowrap;

      > .nav-item {
        position: relative;
        display: inline-block;
        margin: 0 1rem;
        line-height: 2rem;

        > a {
          line-height: 1.4rem;
          color: inherit;
          font-weight: 500;
          text-decoration: none;
        }

        > a:hover {
          color: #819ce4;
        }

        > .router-link-active {
          color: #819ce4;
          font-weight: bolder;
          margin-bottom: -2px;
          border-bottom: 2px solid #819ce4;
        }
      }
    }

    > .toggleMenu {
      width: 24px;
      height: 24px;
      position: absolute;
      left: 16px;
      top: 50%;
      transform: translateY(-50%);
      display: none;
    }

    @media (max-width: 500px) {
      .can-hide {
        display: none;
      }
      > .nav-links .can-hide {
        display: none;
      }
      > .menu {
        display: none;
      }
      > .logo {
        margin: 0 auto;
      }
      > .toggleMenu {
        display: inline-block;
      }
    }
  }
}
</style>
