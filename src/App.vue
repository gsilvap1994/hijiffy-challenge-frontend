<template>
  <app-header
    :isAuthenticated="true"
    :hasNotifications="true"
    :imgSrc="require(`@/assets/images/icons/profile.jpg`)"
  />
  <main class="main-page">
    <div class="table-actions">
      <app-shared-button
        :type="'button'"
        :label="'Add Contact'" 
      />
    </div>
    <app-contact-list :contacts="contacts" />
  </main>
  <app-footer />
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import axios from 'axios';

import Header from './components/header/Header.vue';
import Footer from './components/footer/Footer.vue';
import ContactList from './components/contact-list/ContactList.vue';
import Button from './components/shared/button/Button.vue';

export default defineComponent({
  name: 'App',
  components: {
    'app-header': Header,
    'app-footer': Footer,
    'app-contact-list': ContactList,
    'app-shared-button': Button
  },
  data() {
    return {
      contacts: [],
    }
  },
  async created() {
    try {
      const res = await axios.get(`http://localhost:3000/contacts`)
      this.contacts = res.data;
    } catch(e) {
      console.log(e);
    }
  }
});
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

body {
  margin: 0;
  color: $light-color-text; 
}

.main-page {
  background-color: $light-primary-light-grey;
  padding-top: calc(100px + 2rem);


  .contact-list, .table-actions {
    width: 90%;
    margin: 0 auto;
    padding-bottom: 2rem;
    
  }

  .table-actions {
    text-align: end;
  }
}

</style>
