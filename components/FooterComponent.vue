<template>
  <footer v-if="dataLoaded" v-cloak>
    <section id="footer">
      <div class="newsletter_signup">
        <div class="main_container">
          <div class="center-block">
            <span>Sign up to receive the latest deals and news!</span>
            <label for="userName" class="visuallyhidden">Enter First Name</label>
            <input
              id="userName"
              v-model="newsletter_name"
              type="text"
              placeholder="First Name*"
              class="newsletter_control"
              required
            />
            <label for="emailAddress" class="visuallyhidden">Enter Email Address</label>
            <input
              id="emailAddress"
              v-model="newsletter_email"
              type="text"
              placeholder="Email*"
              class="newsletter_control"
              required
            />
            <button @click="newsletterRoute" class="animated_btn">Sign Up</button>
          </div>
        </div>
      </div>
      <div class="footer_content">
        <div class="row main_container">
          <p class="margin_20">{{ property.name }}</p>
          <social-links class="margin_20"></social-links>
          <p>{{ getPropertyAddress }}</p>
          <p v-if="property.contact_phone" class="margin_40">
            <a :href="'tel:' + property.contact_phone">{{ property.contact_phone }}</a>
          </p>
          <div class="footer_links">
            <p>
              <a href="/pages/creekside-privacy-policy">Privacy Policy</a>
            </p>
          </div>
        </div>
      </div>
      <div class="copyright">
        <div class="row main_container">
          <div class="col-md-12">
            <p class="footer_text">
              &#169; {{copyright_year}}
              <a
                :href="siteInfo.propertyManagementURL"
                target="_blank"
              >{{ siteInfo.propertyManagementName }}</a>. All rights reserved. | Powered by
              <a
                href="https://www.mallmaverick.com/"
                target="_blank"
              >Mall Maverick</a>
            </p>
          </div>
        </div>
      </div>
    </section>
  </footer>
</template>

<script>
import { mapGetters } from 'vuex'
import moment from 'moment'

export default {
  // computed: {
  //   ...mapGetters(['property']),
  //   copyright_year() {
  //     return moment().year()
  //   }
  // }
  data: function data() {
    return {
      dataLoaded: false,
      instaFeed: null,
      newsletter_name: '',
      newsletter_email: '',
    }
  },
  components: {
    SocialLinks: () => import('~/components/PropertySocialLinks.vue')
  },
  created() {
    this.dataLoaded = true
  },
  computed: {
    ...mapGetters(['property', 'timezone']),
    copyright_year() {
      return moment().year()
    }
  },
  methods: {
    newsletterRoute() {
      this.show_menu = false
      this.$router.push({
        path: 'newsletter',
        query: { name: this.newsletter_name, email: this.newsletter_email }
      })
      this.newsletter_name = ''
      this.newsletter_email = ''
    }
  }
}
</script>
