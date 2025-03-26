<script setup lang="ts">
import type { SpeakersCollectionItem } from '@nuxt/content';

const { data: speakers } = await useAsyncData('speakers', () => queryCollection('speakers').order('firstname', 'ASC').all());

const selectedSpeaker = ref<SpeakersCollectionItem | null>(null);
const openSpeakerDetails = (speaker: SpeakersCollectionItem) => {
  selectedSpeaker.value = speaker;
};
</script>

<template>
  <UContainer>
    <UPageHeader title="Speakers" description="Meet our amazing speakers." class="py-[50px]" />

    <UPageBody>
      <USlideover title="Speaker details">

        <UPageGrid>
          <SpeakerCard v-for="speaker in speakers" :key="speaker.firstname + speaker.lastname" :speaker="speaker"
            @click="openSpeakerDetails(speaker)" />
        </UPageGrid>

        <template #body v-if="selectedSpeaker">
          <div class="flex flex-col">
            <UUser 
              :name="`${selectedSpeaker.firstname} ${selectedSpeaker.lastname}`"
              :description="selectedSpeaker.role"
              :avatar="{
                src: selectedSpeaker.photo
              }"
              size="xl" 
              class="justify-center mb-10"
              :ui="{avatar: 'size-24'}" />
            <div v-if="selectedSpeaker.company" class="flex items-center space-x-2">
              <UIcon name="lucide:building-2" class="text-gray-500" />
              <p>{{ selectedSpeaker.company.name }}</p>
            </div>
            <USeparator class="mt-10"/>
            <div v-if="selectedSpeaker.socials" class="mt-5 flex justify-center">
              <SocialLinks :socials="selectedSpeaker.socials"/>
            </div>
          </div>
        </template>
      </USlideover>
    </UPageBody>
  </UContainer>
</template>