<template>
  <nav class="navigation normalize-width">
    <div class="logo" @click="$router.push('/')">
      <img src="@/assets/logo.svg" alt="Karmakurier Logo" />
      <!-- <video class="video" autoplay muted playsinline>
              <source src="@/assets/logo_animated_cropped.mp4" type="video/mp4" />
      </video>-->
    </div>

    <div class="hamburger-menu" @click="expandMenu = true">
      <i class="fas fa-bars"></i>
    </div>

    <div class="menu-items">
      <ul>
        <li @click="$router.push('/faq')">
          <a>Wie es funktioniert & FAQ</a>
        </li>
        <li @click="$router.push('/login')">
          <a>Helfer Login</a>
        </li>
        <li @click="$router.push('/signup')">
          <a>Als Helfer registrieren</a>
        </li>
      </ul>
    </div>

    <div class="open-menu" :class="{expand: expandMenu}">
      <div class="top normalize-width">
        <div class="logo" @click="$router.push('/')">
          <img src="@/assets/logo_inverted.svg" alt="Karmakurier Logo" />
        </div>

        <div class="hamburger-menu" @click="expandMenu = false">
          <i class="fas fa-times"></i>
        </div>
      </div>
      <div class="items normalize-width">
        <ul>
          <li @click="$router.push('/faq'); expandMenu = false">Wie es funktioniert & FAQ</li>
          <li @click="$router.push('/einloggen'); expandMenu = false">Helfer Login</li>
          <li @click="$router.push('/registrieren'); expandMenu = false">Als Helfer registrieren</li>
        </ul>
      </div>
    </div>
  </nav>
</template>

<script>
export default {
  data() {
    return {
      expandMenu: false
    };
  },
  props: {},
  mounted() {
    // Start video.
    const isSafari = /^((?!chrome|android).)*safari/i.test(navigator.userAgent);
    const video = document.querySelector(".video");
    if (isSafari && video) {
      setTimeout(function() {
        // werid fix for safari
        document.querySelector(".video-wrapper").innerHTML = video.outerHTML;
      }, 100);
    }
  }
};
</script>

<style lang="scss" scoped>
@import "@/Branding.scss";

.navigation {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.logo {
  cursor: pointer;
}

.logo img {
  width: 7rem;
}

.logo video {
  width: 7rem;
}

.hamburger-menu {
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
  border-radius: 100%;
  height: 40px;
  width: 40px;
  &:hover {
    background-color: rgba($primary, 0.16);
  }
  @media only screen and (min-width: 560px) {
    display: none;
  }
}

.fas {
  display: inline-block;
  font-size: 22px;
}

.menu-items {
  display: none;
  @media only screen and (min-width: 560px) {
    display: block;
  }
  ul {
    display: flex;
    justify-content: flex-end;
    align-items: center;
    list-style: none;
    margin: 0;
    padding: 0;
    li {
      font-weight: 700;
      a {
        color: $black;
        padding-left: 40px;
      }
      img {
        margin-left: 16px;
        width: 48px;
        height: 48px;
        border-radius: 100%;
      }
      &.helper-login {
        a {
          color: $secondary;
        }
      }
      &:hover {
        cursor: pointer;
        a {
          color: $primary;
        }
      }
    }
  }
}

.open-menu {
  z-index: 99;
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 0%;
  background-color: $primary;
  overflow: hidden;
  transition: all 0.16s ease;

  &.expand {
    height: 100%;
  }

  .top {
    margin-top: 8px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    i {
      color: $secondary;
    }
  }

  .items {
    ul {
      margin: 0;
      width: 100%;
      li {
        padding: 16px 0;
        text-align: center;
        font-weight: 700;
        font-size: 1.6rem;
        color: $black;
        cursor: pointer;
        &:hover {
          background-color: #ff9065;
        }
      }
    }
  }
}
</style>
