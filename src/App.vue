<script setup lang="ts">
import MyAsyncComponent from './components/MyAsyncComponent.vue';

// import { GraphQLClient, request, gql } from 'graphql-request'
// import { ref } from 'vue';

// const result = ref<any>(null)

// const document = gql`
//   {
//     visitors {
//           id
//       }
//   }
// `

// const endpoint = 'https://graphql.bubble.chat:8081/'

// //  const result = await request('https://graphql.bubble.chat:8081/', document)

// const client = new GraphQLClient(endpoint)
// const result = await client.request(document)

</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      Graphql Request
    </div>
  </header>
  <div>
    <Suspense>
   <template #default>
    <!-- {{ result }} -->
    <MyAsyncComponent />
   </template>
   <template #fallback>
     <span>Loading...</span>
   </template>
 </Suspense>
  </div>

  <main>
    <TheWelcome />
  </main>
  
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
