<template>
  <modal name="modal-newsletter" :width="450">
    <p slot="header">Newsletter</p>
    <div slot="content">
      <form @submit.prevent="subscribe" novalidate>
        <div class="mb35">
          <p class="h4">Sign up to our newsletter and receive a coupon for 10% off!</p>
          <input class="brdr-none py10 h4 weight-200" autofocus type="email" name="email" v-model="email" autocomplete="email" placeholder="E-mail address *">
          <p class="m0 c-red h6" v-if="$v.email.$error && !$v.email.required">Field is required.</p>
          <p class="m0 c-red h6" v-if="!$v.email.email">Please provide valid e-mail address.</p>
        </div>
        <div class="mb35 center-xs">
          <button-full class="btn-full p0 ripple" text="Subscribe" @click.native="$v.email.$touch(); subscribe()"/>
        </div>
      </form>
    </div>
  </modal>
</template>
<script>
import ButtonFull from 'theme/components/theme/ButtonFull.vue'
import Modal from 'theme/components/core/Modal'
import { required, email } from 'vuelidate/lib/validators'
import EventBus from 'src/event-bus'
import i18n from 'lib/i18n'

export default {
  data () {
    return {
      email: ''
    }
  },
  validations: {
    email: {
      required,
      email
    }
  },
  methods: {
    subscribe () {
      if (this.$v.$invalid) {
        this.$bus.$emit('notification', {
          type: 'error',
          message: i18n.t('Please fix the validation errors'),
          action1: { label: 'OK', action: 'close' }
        })
        return
      }

      // todo: add user email to newsletter list
      EventBus.$emit('newsletter-after-subscribe', { email: this.email })

      this.$bus.$emit('notification', {
        type: 'success',
        message: i18n.t('You have been successfully subscribed to our newsletter!'),
        action1: { label: 'OK', action: 'close' }
      })

      this.$bus.$emit('modal.hide', 'modal-newsletter')
    }
  },
  components: {
    ButtonFull,
    Modal
  }
}
</script>
<style lang="scss" scoped>

  input[type=email] {
    box-sizing: border-box;
    border-bottom: 1px solid #BDBDBD;
    width: 100%;
    font-family: 'Roboto', sans-serif;
  }

  input::-webkit-input-placeholder,
  input::-moz-placeholder {
    color: #BDBDBD;
  }

  input:focus {
    outline: none;
    border-color: #000000;
    transition: 0.3s all;
  }

  .btn-full {
    display: block;
  }

</style>
