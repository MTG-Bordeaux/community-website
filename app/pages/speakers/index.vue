<script setup lang="ts">
import { useAsyncData } from '#app'

const { data: speakers } = await useAsyncData('speakers', () => queryCollection('speakers').all())
</script>

<template>
  <UContainer>
    <UPageHeader
      title="Speakers"
      description="Meet our amazing speakers."
      class="py-[50px]"
    />

    <UPageBody>
      <UPageGrid>
        <SpeakerCard
          v-for="speaker in speakers"
          :key="speaker.firstname + speaker.lastname"
          :speaker="speaker"
        />
      </UPageGrid>
    </UPageBody>
  </UContainer>
</template>