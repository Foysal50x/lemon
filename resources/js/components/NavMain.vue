<script setup lang="ts">
import { SidebarGroup, SidebarGroupLabel, SidebarMenu } from '@/components/ui/sidebar';
import { type NavItem, type SharedData } from '@/types';
import { usePage } from '@inertiajs/vue3';
import NavItemCollapsible from '@/components/ui/sidebar/NavItemCollapsible.vue';
import NavItemSingle from '@/components/ui/sidebar/NavItem.vue';


defineProps<{
    items: NavItem[];
    label: string;
}>();

const page = usePage<SharedData>();
</script>

<template>
    <SidebarGroup class="px-2 py-0">
        <SidebarGroupLabel> {{ label }} </SidebarGroupLabel>
        <SidebarMenu>
            <template v-for="item in items">
                <NavItemCollapsible v-if="item?.items && item.items.length > 0" :item="item" />
                <NavItemSingle v-else :item="item" />
            </template>
        </SidebarMenu>
    </SidebarGroup>
</template>
