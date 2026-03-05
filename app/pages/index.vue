<template>
  <div>
    <UPageHero
      description="A collection of community bundles for Sulu CMS."
      orientation="horizontal"
      :links="[
        {
          label: `Browse ${bundles.length} bundles`,
          to: '#bundles',
          trailingIcon: 'i-lucide-arrow-down',
          size: 'xl',
        },
      ]"
    >
      <template #title> Sulu<span class="text-green-500">Hub</span> </template>
      <div class="hero-logo"></div>
    </UPageHero>

    <BundleList :bundles="bundles" />

    <UPageSection class="pt-0">
      <UPageCTA
        title="About Sulu Hub"
        description="This page is a collection of community bundles for Sulu CMS. It is a platform for developers to share and discover bundles for Sulu CMS."
        variant="subtle"
        :links="[
          {
            label: 'Start building',
            to: 'https://ui.nuxt.com/docs/getting-started/installation/nuxt',
            target: '_blank',
            trailingIcon: 'i-lucide-arrow-right',
            color: 'neutral',
          },
          {
            label: 'View on GitHub',
            to: 'https://github.com/nuxt-ui-templates/starter',
            target: '_blank',
            icon: 'i-simple-icons-github',
            color: 'neutral',
            variant: 'outline',
          },
        ]"
      />
    </UPageSection>
  </div>
</template>

<script setup lang="ts">
const { data: bundles } = await useAsyncData(() =>
  queryCollection("bundle").all(),
);
</script>

<style lang="css">
.hero-logo {
  mask: url("sulu.svg") 0 0/100% 100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(
    -45deg,
    var(--color-green-700),
    var(--color-green-600),
    var(--color-green-500)
  );
  background-size: 300% 300%;
  animation: gradient 10s ease infinite;
}

@keyframes gradient {
  0% {
    background-position: 0% 50%;
  }
  50% {
    background-position: 100% 50%;
  }
  100% {
    background-position: 0% 50%;
  }
}
</style>
