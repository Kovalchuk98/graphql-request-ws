<template>
    {{ data }}
</template>

<script lang="ts">

import { request, gql } from 'graphql-request'
import { ref } from 'vue'

export default {

    name: 'MyAsyncComponent',
    async setup() {
        const document = gql`
        {
            visitors {
                id
            }
        }
    `
        // const endpoint = 'https://graphql.bubble.chat:8081/'

        // const result = await request('https://graphql.bubble.chat:8081/', document)

        // const client = new GraphQLClient(endpoint)
        // const result = await client.request(document)

        const data = ref<any>(null)

        // await new Promise((r) => setTimeout(r, 2000))

        try {
            const res = await request('https://graphql.bubble.chat:8081/', document)
            data.value = await res
        } catch (e) {
            console.error(e)
        }
        return { data }
    }
}

</script>
