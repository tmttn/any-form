<template>
    <div id="home">
        <div v-if="content || isPreviewing()">
            <RenderContent model="page" :content="content" :api-key="BUILDER_PUBLIC_API_KEY" />
        </div>
        <div v-else>Content not Found</div>
    </div>
</template>
  
<script setup>
import { RenderContent, getContent, isPreviewing } from '@builder.io/sdk-vue/vue3';

const BUILDER_PUBLIC_API_KEY = '586cc052940e4f7faccde4112771ec56';

const route = useRoute();

// fetch builder content data
const { data: content } = await useAsyncData('builderData', () =>
    getContent({
        model: 'page',
        apiKey: BUILDER_PUBLIC_API_KEY,
        userAttributes: {
            urlPath: route.path,
        },
    })
);
</script>