<template>
  <div id="footer-container">
    <div id="solar-tweaks-container">
      <img
        src="@/assets/logo-gray.svg"
        id="footer-image"
        alt="Solar Tweaks Logo"
      />
      <h4 id="solartweaks-text" class="footer-text">
        Solar Tweaks • {{ version }} • {{ os }}
      </h4>
    </div>
    <div id="links-container">
      <ul id="links">
        <li
          v-for="link in links"
          v-bind:key="link.url"
          class="link"
          @click="openLink(link.url)"
        >
          <i :class="link.icon" style="color: #3b3b3b"></i>
        </li>
      </ul>
    </div>
    <div id="mojang-disclaimer-container">
      <h4 class="footer-text">Not affiliated with Mojang, AB.</h4>
    </div>
  </div>
</template>

<script>
import { remote } from 'electron';
import { platform } from 'process';
import constants from '../constants';

export default {
  name: 'Footer',

  data: () => ({
    version: remote.app.getVersion(),
    os:
      platform === 'win32'
        ? 'Windows'
        : platform === 'darwin'
        ? 'MacOS'
        : platform === 'linux'
        ? 'Linux'
        : `Unknown (${platform})`,
    links: [
      {
        icon: 'fa-brands fa-github',
        url: constants.links.GITHUB,
      },
      {
        icon: 'fa-solid fa-comments',
        url: constants.links.GH_DISCUSSIONS,
      },
      {
        icon: 'fa-brands fa-youtube',
        url: constants.links.YOUTUBE,
      },
      {
        icon: 'fa-solid fa-globe',
        url: constants.links.WEBSITE,
      },
    ],
  }),

  methods: {
    /**
     * Opens a link in the default browser
     * @param {string} url The url to open
     */
    openLink(url) {
      remote.shell.openExternal(url);
    },
  },
};
</script>

<style scoped>
#footer-container {
  position: fixed;
  background-color: #141414;
  bottom: 0;
  height: 50px;
  width: 100%;
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-between;
  z-index: 10;
}

#solar-tweaks-container {
  display: flex;
}

#footer-image {
  opacity: 0.3;
  margin-left: 15px;
  height: 30px;
  -webkit-user-drag: none;
}

.footer-text {
  color: #3b3b3b;
  font-weight: 600;
  letter-spacing: 0.25px;
  text-shadow: 0 1px 0 rgba(0, 0, 0, 0.25);
  font-size: 17px;
}

#solartweaks-text {
  margin-left: 10px;
  margin-top: auto;
  margin-bottom: auto;
}

#links {
  list-style-type: none;
}

.link {
  display: inline;
  margin: 0 10px;
  color: #3b3b3b;
  font-size: 20px;
  cursor: pointer;
  text-shadow: 0 2px 0 #00000050;
  transition: 0.2s ease;
}

.link:hover {
  filter: brightness(1.5);
}

#mojang-disclaimer-container {
  font-weight: 200;
  letter-spacing: 0.2px;
  justify-self: right;
  margin-right: 15px;
  margin-left: 25px;
}
</style>
