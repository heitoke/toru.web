<template>
    <ClientOnly>
        <Wait/>
        <Notifications/>
    </ClientOnly>

    <NuxtLayout class="layout">
        <Header v-if="!$route.meta?.flags?.includes('hide:header')"/>

        <NuxtPage class="page" v-if="$index.ready"/>
    </NuxtLayout>
</template>

<script lang="ts" setup>

import Header from '~/components/models/header/Index.vue';
import Notifications from '~/components/models/notifications/Index.vue';
import Wait from '~/components/models/wait/Index.vue';


const { $lang } = useNuxtApp();

const
    $route = useRoute(),
    $request = useRequestURL();


const $index = useStore();
const $user = useUserStore();


onMounted(() => {
    if (process.server) return;

    console.log('start app');
    
    $lang.init();

    if ($cookies.get('THEME') !== 'light') {
        document.querySelector('html')?.classList.add('dark');
    }
});


// * Meta
useHead({
    titleTemplate: title => {
        return (title ? `${title} - ` : '') + 'Toru'
    },
    meta: [
        { name: 'og:type', content: 'website' },
        { name: 'og:url', content: $request.origin + $route.fullPath },
        { name: 'refresh', content: '5' },
        { name: 'theme-color', content: '#fe4d7c' },
        { name: 'apple-mobile-web-app-status-bar-style', content: '#fe4d7c' },
    ],
    link: [
        {
            rel: 'icon',
            type: 'image/png',
            href: '/favicon.ico'
        },
        {
            rel: 'stylesheet',
            href: 'https://ti.heito.xyz/style.css'
        }
    ],
    htmlAttrs: {
        class: 'light',
        lang: 'en'
    }
});

</script>