<template>
  <NuxtPage />
</template>
<script setup lang="ts">
  const route = useRoute();
  const description = "This is a web application built in Nuxt, Vue, and TypeScript. It shows a live countdown to Exotical's birthday.";
  const title = String(route.meta.title || "Unknown Page");
  const siteName = "Exotical Birthday Countdown";
  const author = "ItzExotical";
  useServerSeoMeta({
    title: title,
    author: author,
    ogLocale: "en_GB",
    ogTitle: title,
    description: description,
    ogDescription: description,
    ogSiteName: siteName
  });
</script>