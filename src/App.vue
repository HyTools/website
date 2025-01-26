<template>
  <div id="coming-soon">
    <h1>{{ title }}</h1>
    <p>{{ message }}</p>
    <a :href="discordLink.url" target="_blank">{{ discordLink.text }}</a>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

type Language = 'fr' | 'en';

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
    detectLanguage(): Language {
      const userLang = navigator.language || navigator.language;
      return userLang.startsWith('fr') ? 'fr' : 'en';
    },
    updateContent(language: Language) {
      const titles: Record<Language, string> = {
        fr: 'HyTools',
        en: 'HyTools',
      };

      const messages: Record<Language, string> = {
        fr: 'Notre site est en cours de développement. Rejoignez notre communauté sur Discord pour rester informé.',
        en: 'Our website is under development. Join our Discord community to stay informed.',
      };

      const links: Record<Language, string> = {
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

