<script>
import NavbarDetailPage from "../components/NavbarDetailPage.vue";
import { useAppStore } from "../stores/app";
import { mapState, mapActions } from "pinia";

export default {
  components: { NavbarDetailPage },
  computed: {
    ...mapState(useAppStore, ['eventMoreDetail'])
  },
  methods: {
    ...mapActions(useAppStore, ['fetchEventMoreDetail'])
  },
  created() {
    this.fetchEventMoreDetail(this.$route.params.id)
  }
};
</script>

<template>
  <!-- ! Navbar -->
  <NavbarDetailPage />
  <!-- ! End of Navbar -->

  <div class="event-more-detail-section">
    <div class="event-detail">
        <div class="event-title-container">
            <div class="event-detail-name">{{ eventMoreDetail.title }}</div>
            <div class="event-detail-type">{{ eventMoreDetail.type }}</div>
        </div>
        <div class="event-detail-container">
            <table class="event-table">
                <tr>
                    <td class="event-detail-tag">Price</td>
                    <td>:</td>
                    <td class="event-detail-value">{{ (eventMoreDetail.price === null) ? "Not Available" : `From $ ${eventMoreDetail.price}` }}</td>
                </tr>
                <tr>
                    <td class="event-detail-tag">Venue</td>
                    <td>:</td>
                    <td class="event-detail-value">{{ eventMoreDetail.venue.address + ' ' + eventMoreDetail.venue.state + ', ' + eventMoreDetail.venue.country }}</td>
                </tr>
                <tr>
                    <td class="event-detail-tag">Date</td>
                    <td>:</td>
                    <td class="event-detail-value">{{ eventMoreDetail.date }}</td>
                </tr>
                <tr>
                    <td class="event-detail-tag">Performer</td>
                    <td>:</td>
                    <td class="event-detail-value">{{eventMoreDetail.performer.name}}</td>
                </tr>
            </table>
        </div>
    </div>
    <div class="event-image-container">
        <img class="event-image" :src="eventMoreDetail.performer.image" alt="">
    </div>
  </div>

</template>

<style scoped>
    .event-table {
        display: flex;
        flex-direction: column;
        align-items: flex-start;
        justify-content: flex-start;
        row-gap: 30px;
    } 

    .event-table tr {
        width: 100%;
        
    }

    .event-table tr td:nth-child(even) {
        width: 10px;
    }

    .event-detail-tag {
        width: 25%;
    }

    .event-detail-value {
        width: 3000px;
        padding-left: 20px;
    }

    .event-more-detail-section {
        height: auto;
        width: 100%;
        display: flex;
        flex-direction: row;
        align-items: center;
        justify-content: center;
    }

    .event-detail {
        height: auto;
        width: 60%;
        display: flex;
        flex-direction: column;
        justify-content: flex-start;
        align-items: flex-start;
        padding-left: 100px;
        padding-top: 20px;
    }

    .event-image-container {
        width: 40%;
        height: 85vh;
        display: flex;
        flex-direction: row;
        align-items: center;
        justify-content: center;
    }

    .event-image {
        width: 80%;
        height: 80%;
        object-fit: cover;
        object-position: center;
        border: none;
        border-radius: 10px;
    }

    .event-title-container {
        width: 100%;
        display: flex;
        flex-direction: column;
        align-items: flex-start;
        justify-content: flex-start;
        padding-bottom: 10px;
        border-bottom: 2px solid rgba(53, 53, 53);
    }

    .event-detail-name {
        font-size: 30px;
        font-weight: bold;
    }

    .event-detail-type {
        padding-left: 10px;
        font-size: 24px;
        padding-bottom: 20px;
        color: gray;
    }

    .event-detail-container {
        width: 80%;
        height: 100%;
    }
</style>
