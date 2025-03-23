<script lang="ts" setup>
import type { SpeakersCollectionItem } from '@nuxt/content';
type SocialLinkType = SpeakersCollectionItem['socials'][number]['type'];

const props = defineProps<{
  socials: SpeakersCollectionItem['socials'];
}>()

function getIconFromSocial(social: SocialLinkType){
  switch (social) {
    case 'GITHUB':
      return 'i-mdi-github'
    case 'TWITTER':
      return 'i-mdi-twitter'
    case 'BLOG':
      return 'i-mdi-notebook-edit'
    case 'LINKEDIN':
      return 'i-mdi-linkedin'
    case 'BLUESKY':
      return 'i-mingcute-bluesky-social-fill'
    default:
      return 'default'
  }
}
</script>

<template>
  <div>
    <div class="flex space-x-4">
      <div v-for="social in props.socials" :key="social.type">
        <NuxtLink :to="social.link" target="_blank">
          <UIcon :name="getIconFromSocial(social.type)" size="20"/>
        </NuxtLink>
      </div>
    </div>
  </div>
</template>