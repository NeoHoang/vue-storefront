<template>
  <modal name="modal-onboard" class="modal-onboard">
    <div class="content flex middle-xs">
      <i slot="close" class="modal-close material-icons p15 c-gray" @click="close">close</i>
      <img src="/assets/logo.svg" alt="Vuestore" class="logo">

      <div class="copy align-center c-gray-secondary weight-200">
        <p class="h1">Welcome to Vue Storefront!</p>
        <div class="h4">
          <p>Vue Storefront is a PWA storefront  for eCommerce.
          It is and always will be in the open source. Anyone can use and support the project, we want it to be a tool for the improvement of the shopping experience.</p>
          <p>This demo is synchronized with Magento 2.2.0.</p>
          <p><strong>If you want to use the solution or join our passionate PWA community - feel free to contact us via <a href="mailto:contributors@vuestorefront.io" class="c-ocean-green">e-mail</a> or <a href="https://vuestorefront.slack.com/" class="c-ocean-green">Slack</a>.</strong></p>
          <p>
            <button type="button" class="show-demo ripple brdr-none bg-ocean-green c-white h4" @click="close">Show me the demo</button>
          </p>
        </div>
      </div>
    </div>
  </modal>
</template>
<script>
import Modal from 'theme/components/core/Modal.vue'
export default {
  components: {
    Modal
  },
  methods: {
    close () {
      this.$bus.$emit('modal.hide', 'modal-onboard')
    }
  }
}
</script>
<style lang="scss" scoped>
@import '~theme/css/global_vars';
$z-index-notification: map-get($z-index, notification);

.modal-onboard {
  z-index: $z-index-notification + 1;
}

.content {
  min-height: 600px;
  position: relative;
  overflow: hidden;

  @media (max-width: 600px) {
    display: block;
    padding: 40px 20px;
  }
}

.copy {
  @media (min-width: 601px) {
    max-width: 62%;
    margin-left: 30%;
  }
}

.logo {
  display: block;
  margin: auto;

  @media (min-width: 601px) {
    position: absolute;
    width: 48%;
    top: 0;
    bottom: 0;
    transform: translateX(-48%)
  }
}

.show-demo {
  height: 60px;
  width: 270px;
  margin-top: 35px;
  border-radius: 60px;
  cursor: pointer;
}
</style>
