<template>
  <NuxtLink :to="bundle.path">
    <UPageCard
      :title="title"
      :description="bundle.shortDescription"
      spotlight-color="primary"
      class="h-full flex flex-col cursor-pointer hover:bg-elevated transition-colors"
    >
      <template
        v-if="bundle.targetSuluVersion"
        #header
      >
        <div class="flex flex-wrap gap-2">
          <UBadge
            v-for="version in suluVersionBadges"
            :key="version"
            size="sm"
            variant="soft"
          >
            {{ version }}
          </UBadge>
        </div>
      </template>

      <template #footer>
        <div class="flex gap-4">
          <span
            v-if="bundle.githubMaintainer"
            class="flex items-center gap-2 text-muted transition-colors truncate"
          >
            <UAvatar
              v-if="bundle.githubAvatar"
              :src="bundle.githubAvatar"
              size="xs"
            />
            <span class="truncate">@{{ bundle.githubMaintainer }}</span>
          </span>
          <span class="flex items-center gap-1 text-muted ml-auto">
            <UIcon
              name="i-lucide-download"
              class="size-4"
            />
            {{ parseInt(bundle.totalDownloads.toString()).toLocaleString() }}
          </span>
          <span class="flex items-center gap-1 text-muted">
            <UIcon
              name="i-lucide-star"
              class="size-4"
            />
            {{ bundle.githubStars }}
          </span>
        </div>
      </template>
    </UPageCard>
  </NuxtLink>
</template>

<script setup lang="ts">
import type { BundleCollectionItem } from '@nuxt/content'

const props = defineProps<{
  bundle: BundleCollectionItem
}>()

const to = computed(() => `/${props.bundle.path.split('/').pop() || ''}`)

const title = computed(() =>
  props.bundle.title.startsWith('Sulu')
    ? props.bundle.title.replace('Sulu', '')
    : props.bundle.title
)

const suluVersionBadges = computed(() => {
  const target = props.bundle.targetSuluVersion

  if (!target) return []

  const versions: string[] = []

  if (target.includes('2.')) {
    versions.push('2.x')
  }

  if (target.includes('3.')) {
    versions.push('3.x')
  }

  return versions
})
</script>
