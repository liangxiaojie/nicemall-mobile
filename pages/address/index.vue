<template>
  <div class="container">
    <appHeader title="收货地址" />
    <div class="address-item" v-for="(item, key) in deliveryAddresses" :key="key">
      <div>
        <span>{{ item.consignee }}</span>
        <span class="phone-number">{{ item.phone_number }}</span>
      </div>
      <p><span v-if="item.is_default" class="address-default">[默认地址]</span> {{ item.address }}</p>
      <div class="actions">
        <x-button mini @click.native="handleEdit(item)">编辑</x-button>
      </div>
    </div>
    <div class="footer">
      <x-button type="primary" link="/address/edit">添加收货地址</x-button>
    </div>
  </div>
</template>

<script>
import { mapGetters, mapActions } from 'vuex'
import appHeader from '~/components/appHeader'
import { getDeliveryAddresses } from '~/apollo/deliveryAddress'

export default {
  components: {
    appHeader,
  },
  data () {
    return {
      deliveryAddresses: null
    }
  },
  computed: {
    ...mapGetters(['user'])
  },
  async mounted() {
    const { deliveryAddresses } = await getDeliveryAddresses(this.$apollo)
    this.deliveryAddresses = deliveryAddresses
  },
  methods: {
    handleEdit(item) {
      this.$router.push({
        path: '/address/edit',
        query: {
          deliveryAddress: item,
        }
      })
    }
  }
}
</script>

<style lang="scss" scoped>
.container {
  margin-top: .45rem;
  margin-bottom: .5rem;
  overflow: auto;
}
.footer {
  position: fixed;
  bottom: 0;
  left: auto;
  right: auto;
  width: 3.75rem;
  box-sizing: border-box;
  padding: .1rem;
  background-color: rgb(245, 245, 245);
}
.address-default {
  color: #ff8800;
}
.address-item {
  margin: .05rem;
  padding: .1rem;
  border: .01rem solid #dbdbdb;
  font-size: .14rem;
}
.phone-number {
  margin-left: .1rem;
}
.actions {
  position: relative;
  top: -0.35rem;
  float: right;
}
</style>
