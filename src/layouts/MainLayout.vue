<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          @click="leftDrawerOpen = !leftDrawerOpen"
          icon="menu"
          aria-label="Menu"
        />

        <q-toolbar-title>
          Breaking Bad Quotes
        </q-toolbar-title>

      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      bordered
      content-class="bg-grey-1"
    >
      <q-list>
        <q-item-label header class="text-grey-8">Essential Links</q-item-label>
        <EssentialLink
          v-for="link in essentialLinks"
          :key="link.title"
          v-bind="link"
        />
      </q-list>
    </q-drawer>

    <q-page-container class="row justify-center items-center">
      <div>
       <div class="q-pa-md row items-start q-gutter-md">
    <q-card
 dark bordered class="bg-grey-9 my-card " inline style="width: 800px"
    >
        <q-img
        src="https://miro.medium.com/max/3840/1*-U9ShJEjPqTkhkweZdT2oA.jpeg"
        basic
      ></q-img>
      <q-card-section>
        <div class="text-h6">Breaking Bad Quotes</div>
        <div class="text-subtitle2">by {{ info[0].author }}</div>
      </q-card-section>

      <q-card-section class="q-pt-none">
        {{ info[0].quote }}
      </q-card-section>
    </q-card>
  </div>
      </div>
    </q-page-container>
  </q-layout>
</template>

<script>
import EssentialLink from 'components/EssentialLink'
import axios from 'axios'

export default {
  name: 'MainLayout',

  components: {
    EssentialLink
  },

  data () {
    return {
      info: [],
      leftDrawerOpen: false,
      lorem: 'hahaha',
      essentialLinks: [
        {
          title: 'Github',
          caption: 'github.com/olivmarcos',
          icon: 'code',
          link: 'https://github.com/olivmarcos'
        },
        {
          title: 'Twitter',
          caption: '@_olivmarcos',
          icon: 'rss_feed',
          link: 'https://twitter.com/_olivmarcos'
        },
        {
          title: 'Instagram',
          caption: '@_olivmarcos',
          icon: 'public',
          link: 'https://www.instagram.com/_olivmarcos/'
        }
      ]
    }
  },
  mounted () {
    axios.get('https://breaking-bad-quotes.herokuapp.com/v1/quotes').then(response => (this.info = response.data))
  }
}
</script>
