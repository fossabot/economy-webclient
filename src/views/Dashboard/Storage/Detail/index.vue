<template>
  <div style="padding: 3rem;">
    <h1 style="margin-top: 0;">Storage</h1>

    <!-- Storage Items -->
    <div v-if="storage && storage.items">
      <h2>Items</h2>

      <div v-if="storage.items.lenght === 0">
        Sorry, no items found in the storage
      </div>

      <table class="gc-table" v-if="storage.items.length > 0">
        <thead>
          <tr>
            <th>Unique ID</th>
            <th>Item</th>
            <th></th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="storageItem in storage.items" :key="storageItem.id">
            <td>{{ storageItem.id }}</td>
            <td>
              <div>{{ storageItem.item.name }}</div>
              <div class="gc-table__description">({{ storageItem.item.id }})</div>
            </td>
            <td>
              <a href="">Remove</a>
            </td>
          </tr>
        </tbody>
      </table>
    </div>

    <!-- Give item -->
    <div v-if="storage">
      <h2>Give item</h2>
      <give-item
        :storageId="this.$route.params.id"
      ></give-item>
    </div>

    <!-- Raw storage -->
    <div v-if="storage">
      <h2>Raw storage</h2>
      <pre class="gc-pre">{{ JSON.stringify(storage, null, 2) }}</pre>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import GiveItem from '@/components/GiveItem/index.vue';

@Component({
  components: {
    GiveItem,
  },
})
export default class Storage extends Vue {
  public storage = null;

  public mounted() {
    this.$economyService.getStorage(this.$route.params.id)
      .then(({ storage }) => {
        this.storage = storage;
      });
  }
}
</script>
