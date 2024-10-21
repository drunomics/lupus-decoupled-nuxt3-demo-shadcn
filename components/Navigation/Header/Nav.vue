<template>
  <UiNavigationMenu>
    <UiNavigationMenuList>
      <UiNavigationMenuItem v-for="menuItem in mainMenu" :key="menuItem.key" class="relative">
        <NuxtLink
          v-slot="{ isActive }"
          :to="menuItem.external ? menuItem.absolute : `/${menuItem.alias}`"
          :external="menuItem.external"
        >
          <Icon
            v-if="menuItem.external"
            name="lucide:arrow-up-right"
            class="absolute right-2 top-2 text-muted-foreground"
            size="13"
          />
          <UiNavigationMenuLink
            :active="isActive"
            class="bg-transparent pr-6 font-semibold"
            :class="navigationMenuTriggerStyle()"
          >
            {{ menuItem.title }}
          </UiNavigationMenuLink>
        </NuxtLink>
      </UiNavigationMenuItem>
    </UiNavigationMenuList>
  </UiNavigationMenu>
</template>

<script setup lang="ts">
import { navigationMenuTriggerStyle } from '@/components/Ui/navigation-menu'
const { fetchMenu } = useDrupalCe()
const mainMenu = await fetchMenu('main')
</script>
