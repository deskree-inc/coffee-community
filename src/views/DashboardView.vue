<template>
  <div class="dashboard-wrapper">
    <div class="my-products-nav">
      <div class="tabs">
        <button class="tab" v-for="tab in tabs" :class="{active: tab === currentTab}" @click="setActiveTab(tab)"
                :key="tab">
          {{ tab.replace(/-/g, " ") }}
        </button>
      </div>
      <button-primary text="New Product" @click="newProduct"></button-primary>
    </div>
    <div class="my-products" v-if="currentTab === 'my-beans'">
      <div class="product" v-for="bean in myBeans" :key="bean._id">
        <div class="product-image" :style="{'background-image': `url(${bean.picture.url})`}"
             v-if="bean.hasOwnProperty('picture')">
        </div>
        <div class="product-info">
          <h2>{{ bean.name }}</h2>
          <span>{{ user.name }}</span>
        </div>
      </div>
    </div>
    <div class="my-products" v-if="currentTab === 'all-beans'">
      <div class="product" v-for="bean in beans" :key="bean._id">
        <div class="product-image" :style="{'background-image': `url(${bean.picture.url})`}"
             v-if="bean.hasOwnProperty('picture')">
        </div>
        <div class="product-info">
          <h2>{{ bean.name }}</h2>
          <span>{{ user.name }}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import {defineComponent} from 'vue';
import ButtonPrimary from "@/components/Button.vue";
import {client} from "@/server";
import {WebflowBeansCollectionResponseInterface} from "@/interfaces/webflowCollection.interface";

export default defineComponent({
  name: 'DashboardView',
  components: {ButtonPrimary},
  data() {
    return {
      beans: [] as Array<Record<string, any>>,
      tabs: ["my-beans", "all-beans"] as Array<string>,
      currentTab: "my-beans" as string,
    };
  },
  computed: {
    user() {
      return this.$store.getters["user"];
    },
    myBeans() {
      const beans = JSON.parse(JSON.stringify(this.beans));
      return beans.filter(bean => bean.author === this.user.webflow_author_id);
    },
  },
  mounted() {
    this.getBeans();
  },
  methods: {
    newProduct() {
      console.log("newProduct");
    },
    setActiveTab(tab: string) {
      this.currentTab = tab;
    },
    async getBeans() {
      try {
        const res: { data: WebflowBeansCollectionResponseInterface } = await client.get(`/integrations/webflow/collections/${process.env.VUE_APP_WEBFLOW_BEANS_COLLECTION_ID}/items`);
        this.beans = res.data.items;
      } catch (e) {
        console.error(e)
      }
    }
  }
});
</script>

<style lang="scss" scoped>
.dashboard-wrapper {
  padding: 100px 10%;
}

.product {
  display: flex;
  width: 31%;
  margin-bottom: 50px;
  padding-right: 10px;
  padding-left: 10px;
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
  -webkit-flex-direction: column;
  -ms-flex-direction: column;
  flex-direction: column;
  -webkit-box-align: center;
  -webkit-align-items: center;
  -ms-flex-align: center;
  align-items: center;
  -webkit-box-flex: 0;
  -webkit-flex: 0 auto;
  -ms-flex: 0 auto;
  flex: 0 auto;
  text-align: center;

  .product-image {
    width: 300px;
    height: 380px;
    background-position: center;
    background-size: cover;
  }

  .product-info {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;

    h2 {
      display: inline-block;
      margin-bottom: 5px;
      color: #1d1f2e;
      font-size: 20px;
      line-height: 30px;
      font-weight: 400;
      text-align: center;
    }

    span {
      display: inline-block;
      color: rgba(29, 31, 46, 0.7);
      font-family: Karla, sans-serif;
      font-size: 16px;
      line-height: 28px;
      font-weight: 400;
      text-transform: capitalize;
    }
  }
}

.my-products-nav {
  width: 100%;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  margin-bottom: 50px;
}

.my-products {
  display: flex;
  margin: 0 -10px;
  -webkit-box-orient: horizontal;
  -webkit-box-direction: normal;
  flex-direction: row;
  -webkit-box-pack: center;
  justify-content: center;
  -webkit-flex-wrap: wrap;
  -ms-flex-wrap: wrap;
  flex-wrap: wrap;
  -webkit-box-align: start;
  align-items: flex-start;
  align-content: flex-start;
}

.tabs {
  display: flex;
  flex-direction: row;
  justify-content: space-between;

  .tab {
    text-transform: capitalize;
    margin-right: 20px;
    cursor: pointer;
    border: none;
    background: none;
    transition: color 0.2s ease-in-out;

    &.active {
      color: #a25f4b;
      text-decoration: underline;
    }
  }
}

</style>