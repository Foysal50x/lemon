<script setup lang="ts">
import {
    Collapsible,
    CollapsibleContent,
    CollapsibleTrigger,
} from '@/components/ui/collapsible'
import { SidebarMenuSub, SidebarMenuSubItem, SidebarMenuSubButton, SidebarMenuButton, SidebarMenuItem } from '@/components/ui/sidebar';
import { type NavItem, type SharedData } from '@/types';
import { ChevronRight } from 'lucide-vue-next'
import { Link, usePage } from '@inertiajs/vue3';
import { computed } from 'vue';


const props = defineProps<{
    item: NavItem;
}>();

const page = usePage<SharedData>();
const isActive = computed(() => {
    return props.item?.items?.some((navItem) => {
        if (navItem.href === page.url) {
            return true;
        }
        return false;
    });
});
</script>
<template>
    <Collapsible :key="item.title" as-child :default-open="isActive"
        class="group/collapsible">
        <SidebarMenuItem>
            <CollapsibleTrigger as-child>
                <SidebarMenuButton :tooltip="item.title">
                    <component :is="item.icon" v-if="item.icon" />
                    <span>{{ item.title }}</span>
                    <ChevronRight
                        class="ml-auto transition-transform duration-200 group-data-[state=open]/collapsible:rotate-90" />
                </SidebarMenuButton>
            </CollapsibleTrigger>
            <CollapsibleContent>
                <SidebarMenuSub>
                    <SidebarMenuSubItem v-for="subItem in item.items" :key="subItem.title">
                        <SidebarMenuSubButton as-child :is-active="subItem.href === page.url">
                            <Link :href="subItem.href">
                                <!-- <component :is="item.icon" v-if="item.icon" /> -->
                                <span>{{ subItem.title }}</span>
                            </Link>
                        </SidebarMenuSubButton>
                    </SidebarMenuSubItem>
                </SidebarMenuSub>
            </CollapsibleContent>
        </SidebarMenuItem>
    </Collapsible>
</template>