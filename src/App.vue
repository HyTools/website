<template>
  <div id="coming-soon">
    <h1>{{ title }}</h1>
    <p>{{ message }}</p>
    <a :href="discordLink.url" target="_blank">{{ discordLink.text }}</a>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'App',
  data() {
    return {
      title: '',
      message: '',
      discordLink: {
        url: 'https://discord.gg/ryjcK2trHd',
        text: '',
      },
    };
  },
  methods: {
    detectLanguage(): string {
      const userLang = navigator.language || navigator.userLanguage;
      return userLang.substring(0, 2);
    },
    updateContent(language: string) {
      const titles = {
        fr: 'HyTools',
        en: 'HyTools',
      };

      const messages = {
        fr: 'Notre site est en cours de développement. Rejoignez notre communauté sur Discord pour rester informé.',
        en: 'Our website is under development. Join our Discord community to stay informed.',
      };

      const links = {
        fr: 'Rejoignez-nous sur Discord',
        en: 'Join us on Discord',
      };

      this.title = titles[language] || titles['en'];
      this.message = messages[language] || messages['en'];
      this.discordLink.text = links[language] || links['en'];
    },
  },
  mounted() {
    const language = this.detectLanguage();
    this.updateContent(language);
  },
});
</script>

