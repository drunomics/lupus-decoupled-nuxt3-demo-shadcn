<template>
  <UiSheet v-model:open="open">
    <UiSheetTrigger as-child>
      <UiButton variant="ghost" size="icon" class="md:hidden">
        <Icon name="lucide:menu" size="18" />
      </UiButton>
    </UiSheetTrigger>
    <UiSheetContent side="left" class="pr-0">
      <UiSheetTitle class="sr-only">Menu</UiSheetTitle>
      <UiSheetDescription class="sr-only">Mobile menu</UiSheetDescription>
      <UiScrollArea
        orientation="vertical"
        class="relative h-full py-6 pr-6 text-sm md:pr-4 !overflow-visible"
        type="hover"
      >
        <ul class="flex flex-col gap-1 pb-4">
          <li v-for="menuItem in mainMenu" :key="menuItem.key">
            <NuxtLink
              v-slot="{ isActive }"
              :to="menuItem.external ? menuItem.absolute : `/${menuItem.alias}`"
              :external="menuItem.external"
            >
              <div
                class="flex h-8 items-center gap-2 rounded-md p-2 m-[2px] text-sm text-foreground/80 hover:bg-muted hover:text-primary"
                :class="[isActive && 'bg-muted !text-primary']"
              >
                {{ menuItem.title }}
              </div>
            </NuxtLink>
          </li>
        </ul>
      </UiScrollArea>
    </UiSheetContent>
  </UiSheet>
</template>

<script setup lang="ts">
const { fetchMenu } = useDrupalCe()
const mainMenu = await fetchMenu('main')

const open = ref(false)
// Close sheet on navigation
watch(
  () => useRoute().path,
  () => {
    open.value = false
  }
)
</script>
