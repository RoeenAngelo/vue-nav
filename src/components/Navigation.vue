<script setup>
import { RouterLink, RouterView } from 'vue-router'

</script>
<script>
export default {
  name: "navigation",
  data() {
    return {
      scrolledNav: null,
      mobile: null,
      mobileNav: null,
      windowWidth: null,
    }
  },
  created() {
    window.addEventListener('resize', this.checkScreen)
  },
  mounted() {
    window.addEventListener('scroll', this.updateScroll)
  },
  methods: {
    toggleMobileNav() {
      this.mobileNav =!this.mobileNav
    },
    checkScreen() {
      this.windowWidth = window.innerWidth
      if (this.windowWidth <= 750) {
        this.mobile = true
        return
      }
      this.mobile = false;
      this.mobileNav = false;
      return
    },
    updateScroll() {
      const scrollPosition = window.scrollY;
      if (scrollPosition > 50) {
        this.scrolledNav = true;
        return
      }
      this.scrolledNav = false
    }
  }
}
</script>


<template>
   <header :class="{ 'scrolled-nav' : scrolledNav }">
        <nav>
            <div class="branding">
                <img src="@/assets/logo.svg" alt="">
            </div>
            <ul 
            v-show="!mobile"
            class="navigation"
            >
                <li><RouterLink class="link" :to="{name:'home'}">Home</RouterLink></li>
                <li><RouterLink class="link" :to="{name:''}">About</RouterLink></li>
                <li><RouterLink class="link" :to="{name:''}">Portfolio</RouterLink></li>
                <li><RouterLink class="link" :to="{name:''}">Contact</RouterLink></li>
            </ul>
            <div class="icon">
                <i 
                @click="toggleMobileNav" 
                v-show="mobile"
                class="fa fa-bars"
                :class="{'icon-active' : mobileNav}"
                >
                </i>
            </div>
            <Transition name="mobile-nav">
                <ul 
                    v-show="mobileNav"
                    class="dropdown-nav"
                    >
                    <li><RouterLink class="link" :to="{name:'home'}">Home</RouterLink></li>
                    <li><RouterLink class="link" :to="{name:''}">About</RouterLink></li>
                    <li><RouterLink class="link" :to="{name:''}">Portfolio</RouterLink></li>
                    <li><RouterLink class="link" :to="{name:''}">Contact</RouterLink></li>
                </ul>
            </Transition>
        </nav>
   </header>

  
</template>



<style lang="scss" scoped>

header {
  background-color: rgba(0, 0, 0, 0.8);
  z-index: 99;
  width: 100%;
  position: fixed;   
  transition: .5s ease all;
  color: #fff;

  nav {
    position: relative;
    display: flex;
    flex-direction: row;
    padding: 12px 0;
    transition: .5s ease all;
    width: 90%;
    margin: 0 auto;
    @media (min-width: 1140px) {
      max-width: 1140px;
    }

    ul,
    .link {
      font-weight: 500;
      list-style: none;
      text-decoration: none;
      color: #fff;
    }

    li {
      padding: 16px;
      margin-left: 16px;
    }
    
    .link {
      font-size: 14px;
      transition: .5s ease all;
      border-bottom: 1px solid transparent;
      padding-bottom: 4px;

      &:hover {
        color: #00afea;
        border-color: #00afea ;
      }
    }
    .branding {
        display: flex;
        align-items: center;

        img {
            width: 50px;
            transition: .5s ease all
        };
    }
    .navigation {
      display: flex;
      align-items: center;
      flex: 1;
      justify-content: flex-end;
    }
    .icon {
      display: flex;
      position: absolute;
      top: 0;
      align-items: center;
      right: 24px;
      height: 100%;
      padding: 10px ;

      i {
        cursor: pointer;
        font-size: 24px;
        transition: 0.8s ease all;

      }
    }
    
    .icon-active {
      transform: rotate(180deg);
    }

    .dropdown-nav {
      display: flex;
      flex-direction: column;
      position: fixed;
      width: 100%;
      max-width: 250px;
      height: 100%;
      background-color: #fff;
      top: 0;
      left: 0;

      li {
        margin-left: 0;
        .link {
          color: #000 ;
        }
      }
    }
    .mobile-nav-enter-active, 
    .mobile-nav-leave-active {
      transition: 1s ease all;
    }
    .mobile-nav-enter-from,
    .mobile-nav-leave-to {
      transform: translateX(-250px);
    }

    .mobile-nav-enter-to {
      transform: translateX(0);
    }
  }
}

.scrolled-nav {
  background-color: #000;
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);

  nav {
    padding: 8px;
    .branding {
        img {
            width: 40px;
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
        };
    }
  }
}
</style>