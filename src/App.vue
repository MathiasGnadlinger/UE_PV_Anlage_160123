<template>
  <div>
    <HelloWorld
      :items="items"
      @update-application="updateApplication"
      :maxFunding="10000000"
    />
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue';
import items from './components/data.js';

export default {
  name: 'App',
  components: {
    HelloWorld,
  },
  data() {
    return {
      items,
    };
  },
  methods: {
    updateApplication(index) {
      this.items[index].bewilligt = !this.items[index].bewilligt;
    },
  },
};
</script>
