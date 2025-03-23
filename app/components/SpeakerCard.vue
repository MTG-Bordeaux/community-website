<script setup lang="ts">
import type { SpeakersCollectionItem } from '@nuxt/content';

defineProps<{ speaker: SpeakersCollectionItem }>();
const emit = defineEmits(['click']);
</script>

<template>
  <UPageCard spotlight spotlight-color="primary">
    <div @click="emit('click', speaker)" class="flex">
        <div class="w-1/3 flex items-center justify-center">
          <UAvatar
            :src="speaker.photo"
            :alt="`${speaker.firstname} ${speaker.lastname}`"
            size="3xl"
            class="size-24 text-4xl"
          />
        </div>
        <div class="w-2/3 p-4 flex flex-col justify-center">
          <h3 class="text-lg font-semibold">{{ speaker.firstname }} {{ speaker.lastname }}</h3>
          <p class="text-sm text-gray-600">{{ speaker.role }}</p>
          <p v-if="speaker.company" class="text-sm text-gray-500">
            {{ speaker.company.name }}
          </p>
          <div v-if="speaker.socials" class="mt-2">
            <SocialLinks :socials="speaker.socials" />
          </div>
        </div>
    </div>
  </UPageCard>
</template>