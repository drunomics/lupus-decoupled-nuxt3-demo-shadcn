<template>
  <div class="drupal-tabs my-2">
    <ul v-if="tabs.primary" class="flex">
      <li v-for="tab in tabs.primary" :key="tab.url">
        <UiButton variant="link" size="sm" as-child>
          <nuxt-link
            :href="tab.url"
            tabindex="-1"
            :class="{ 'is-active': tab.active }"
          >
            {{ tab.label }}
            <span v-if="tab.active" class="sr-only"> (active tab) </span>
          </nuxt-link>
        </UiButton>
      </li>
    </ul>
  </div>
</template>

<script setup lang="ts">
defineProps<{
  tabs: object;
}>()
</script>
