<template>
  <div main class="ion-page">
  <ion-tabs ref="tabs" @ionChange="updateRoute">
    <ion-tab tab="schedule">
      <SessionList />
      <!-- <SessionDetail :sessionId="1"/> -->
    </ion-tab>
    <ion-tab tab="speakers">
      <SpeakerList />
      <!-- <SpeakerDetail :speakerId="1"/> -->
    </ion-tab>
    <ion-tab tab="map">
      <Map />
    </ion-tab>
    <ion-tab tab="about">
      <About />
    </ion-tab>

    <ion-tab-bar slot="bottom">
      <ion-tab-button tab="schedule">
        <ion-label>Schedule</ion-label>
        <ion-icon name="calendar" />
      </ion-tab-button>
      <ion-tab-button tab="speakers">
        <ion-icon name="contacts" />
        <ion-label>Speakers</ion-label>
      </ion-tab-button>
      <ion-tab-button tab="map">
        <ion-icon name="map" />
        <ion-label>Map</ion-label>
      </ion-tab-button>
      <ion-tab-button tab="about">
        <ion-icon name="information-circle" />
        <ion-label>About</ion-label>
      </ion-tab-button>
    </ion-tab-bar>
  </ion-tabs>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import SessionList from '@/views/SessionList.vue';
import SessionDetail from '@/views/SessionDetail.vue';
import SpeakerList from '@/views/SpeakerList.vue';
import SpeakerDetail from '@/views/SpeakerDetail.vue';
import Map from '@/views/Map.vue';
import About from '@/views/About.vue';

@Component({
  components: {
    SessionList,
    SessionDetail,
    SpeakerList,
    SpeakerDetail,
    Map,
    About
  }
})
export default class Home extends Vue {
  $refs!: {
    tabs: HTMLIonTabsElement
  }
  mounted() {
    this.$store.dispatch('loadSessionData');
    this.$store.dispatch('loadSpeakerData');
  }
  get tabname() {
    return this.$route.params.tabs;
  }
  updateRoute(event: CustomEvent) {
    if (event.detail.tab) {
      const activeTab = event.detail.tab.tab;
      this.$router.push('/' + activeTab);
    }
  }
}
</script>
