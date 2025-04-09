<script setup lang="ts">
import {
  DropdownMenu,
  DropdownMenuContent,
  DropdownMenuItem,
  DropdownMenuTrigger,
  DropdownMenuLabel,
  DropdownMenuSeparator,
} from '@/components/ui/dropdown-menu'
import {
  SidebarMenu,
  SidebarMenuButton,
  SidebarMenuItem,
} from '@/components/ui/sidebar'
import { Branch } from '@/types';
import AppLogoIcon from '@/components/AppLogoIcon.vue';
import { Check, ChevronsUpDown, Plus } from 'lucide-vue-next'
import { ref } from 'vue'

const props = defineProps<{
  branches: Branch[]
  defaultBranch: Branch
}>()
const selectedBranch = ref<Branch>(props.defaultBranch)
</script>
<template>
  <SidebarMenu>
    <SidebarMenuItem>
      <DropdownMenu>
        <DropdownMenuTrigger as-child>
          <SidebarMenuButton
            size="lg"
            class="data-[state=open]:bg-sidebar-accent data-[state=open]:text-sidebar-accent-foreground"
          >
            <div class="flex aspect-square size-8 items-center justify-center rounded bg-sidebar-primary dark:bg-white text-white dark:text-sidebar-primary">
              <AppLogoIcon class="size-5 fill-current" />
            </div>
            <div class="flex flex-col gap-0.5 leading-none">
              <span class="font-semibold">Branch</span>
              <span class="">{{ selectedBranch.name }}</span>
            </div>
            <ChevronsUpDown class="ml-auto" />
          </SidebarMenuButton>
        </DropdownMenuTrigger>
        <DropdownMenuContent
          class="w-[--reka-dropdown-menu-trigger-width]"
          align="start"
        >
          <DropdownMenuLabel class="text-xs text-muted-foreground">
              Branches
          </DropdownMenuLabel>
          <DropdownMenuItem
            class="gap-2 p-2"
            v-for="branch in branches"
            :key="branch.id"
            @select="selectedBranch = branch"
          >
            {{ branch.name }}
            <Check v-if="branch.id === selectedBranch.id" class="ml-auto" />
          </DropdownMenuItem>
          <DropdownMenuSeparator />
          <DropdownMenuItem class="gap-2 p-2">
            <div class="flex size-6 items-center justify-center rounded-md border bg-background">
              <Plus class="size-4" />
            </div>
            <div class="font-medium text-muted-foreground">
              Add branch
            </div>
          </DropdownMenuItem>
        </DropdownMenuContent>
      </DropdownMenu>
    </SidebarMenuItem>
  </SidebarMenu>
</template>