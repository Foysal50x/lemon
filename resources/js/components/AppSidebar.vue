<script setup lang="ts">
import NavFooter from '@/components/NavFooter.vue';
import NavMain from '@/components/NavMain.vue';
import NavUser from '@/components/NavUser.vue';
import BranchSwitcher from '@/components/BranchSwitcher.vue';
import { Sidebar, SidebarContent, SidebarFooter, SidebarHeader } from '@/components/ui/sidebar';
import { Branch, type NavItem } from '@/types';
import { Settings, LayoutDashboard, LayoutList, ChartArea, Handshake, Store } from 'lucide-vue-next';

const inventoryMenuItems: NavItem[] = [
    {
        title: 'Dashboard',
        href: '#',
        icon: LayoutDashboard,
        items: [
            {
                title: 'Regular',
                href: '/dashboard',
                icon: LayoutList,
            },
            {
                title: 'Analytics',
                href: '/dashboard-analytics',
                icon: ChartArea,
            },
        ]
    },
    {
        title: 'Suppliers',
        href: '/suppliers',
        icon: Handshake
    }
];

const posMenuItems: NavItem[] = [
    {
        title: 'POS',
        href: '#',
        icon: Store,
        items: [
            {
                title: 'POS Sell',
                href: '/pos-sell'
            },
            {
                title: 'Register (Open/Close)',
                href: '/registers'
            }
        ]
    },
    {
        title: 'Register',
        href: '/registers',
        icon: Handshake,
    }

];

const footerNavItems: NavItem[] = [
    {
        title: 'Settings',
        href: '/settings',
        icon: Settings,
    },
];

const branches: Branch[] = [{ name: "Rajshahi", id: 1 }, { name: "Dhaka", id: 2 }, { name: "Chittagong", id: 3 }]

</script>

<template>
    <Sidebar collapsible="icon" variant="inset">
        <SidebarHeader>
            <BranchSwitcher :branches="branches" :default-branch="branches[0]" />
        </SidebarHeader>

        <SidebarContent>
            <NavMain label="Inventory management" :items="inventoryMenuItems" />
            <NavMain label="Point of sell" :items="posMenuItems" />
        </SidebarContent>

        <SidebarFooter>
            <NavFooter :items="footerNavItems" />
            <NavUser />
        </SidebarFooter>
    </Sidebar>
    <slot />
</template>
