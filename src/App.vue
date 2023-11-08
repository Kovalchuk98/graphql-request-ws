<script setup lang="ts">
import { createClient } from 'graphql-ws';
import MyAsyncComponent from './components/MyAsyncComponent.vue';

import { gql } from 'graphql-request'
import { ref } from 'vue';

const responseData = ref<any>(null)

const document = gql`
      subscription onMessageAdded {
        messageNew {
        id
        text
        dialog {
          id
          visitor {
            id
          }
          }
        }
      }
    `
 
const client = createClient({
  url: 'wss://graphql.bubble.chat:8081/',
});
 
(async () => {
  const query = client.iterate({
    query: document,
  });
 
  try {
    const { value } = await query.next();
    responseData.value = value.data
    console.log(value);
    // next = value = { data: { hello: 'Hello World!' } }
    // complete
  } catch (err) {
    // error
  }
})();
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
     <MyAsyncComponent />
    </template>
    <template #fallback>
      <span>Loading...</span>
    </template>
  </Suspense>
</div>
<div>
  {{ responseData }}
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
