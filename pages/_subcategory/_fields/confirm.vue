<template>
  <div>
    <header class="info-process">
      <headerNav
        :nav-sub-group="navSubGroup"
        :step-active="stepActive" />
    </header>

    <main class="info-process thank-you">

      <h2>Thanks for the report!</h2>
      
      <h3>
        <strong>Service Request ID:
        <span>{{ serviceID }}</span>
        </strong>
      </h3>

      <nuxt-link
        :to="{
          name: 'index',
          query: {
            ticket: serviceID
          }
        }"
        class="button ok-button">
        View Ticket
      </nuxt-link>
    </main>
  </div>
</template>

<style lang="scss" scoped>
  main {
    &.thank-you {
      text-align: center;
      justify-content: center;

      h2, h3 {
        color: white;
        border-bottom: none;
        margin: 0;
      }

      h2 {
        font-size: 24px;
        line-height: 28px;
        margin: 0 0 10px 0;

        span {
          background: darken($color-blue, 5%);
          padding: 0 10px 2px 10px;
        }
      }

      h3 {
        font-size: 22px;
        line-height: 26px;
      }

      p {
        color: white;
        margin: 0 0 20px 0;

        a {
          color: white;
          border-bottom: 1px solid white;
        }

        &:last-of-type {
          margin: 0;
        }
      }

      .ok-button {
        display: flex;
        background: $fern;
        font-size: 30px;
        color: white;
        width: 125px;
        height: 125px;
        font-size: 18px;
        line-height: 18px;
        border-radius: 50%;
        margin: 20px auto 0 auto;
      }
    }
  }
</style>

<script>
import headerNav              from '~/components/nav.vue'
import { mapFields,
         mapMultiRowFields }  from 'vuex-map-fields'

export default {
  beforeRouteEnter (to, from, next) {
    if(from.path == '/')
      next('/');
    next();
  },
  head () {
    return {
      titleTemplate: `%s - Thanks!`
    }
  },
  components: {
    headerNav
  },
  data() {
    return {
      stepActive:     6,
      crmLink:        `${process.env.CRM_BASE_URL}${process.env.CRM_TICKETS}`,
      serviceReqID:   '',
      navSubGroup:    true,
    }
  },
  methods: {
    goHome() {
      alert('go home')
      this.$router.go('index');
    },
  },
  computed: {
    ...mapFields([
      'serviceInfos.service_response',
    ]),
    serviceReponse() {
      return JSON.parse(this.service_response.data.body.body)
    },
    serviceID() {
      return this.serviceReponse[0].service_request_id
    },
  }
}
</script>