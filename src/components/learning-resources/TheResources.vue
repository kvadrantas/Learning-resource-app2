<template>
  <div>
    <base-card>
      <base-button @click="setSelectedTab('stored-resources')"
      :mode="storedButtonMode"
        >Stored Resources</base-button
      >
      <base-button @click="setSelectedTab('add-resource')"
      :mode="addButtonMode"
        >Add Resource</base-button
      >
    </base-card>
    <keep-alive>
        <component :is="selectedTab"></component>
    </keep-alive>
  </div>
</template>

<script>
import StoredResources from "./StoredResources.vue";
import AddResource from "./AddResource.vue";

export default {
  components: {
    StoredResources,
    AddResource,
  },
  data() {
    return {
      selectedTab: "stored-resources",
      storedResources: [
        {
          id: "official-quide",
          title: "Official Guide",
          description: "The official Vue.js documentation.",
          link: "https://vuejs.org",
        },
        {
          id: "google",
          title: "Google",
          description: "The official Vue.js documentation.",
          link: "https://vuejs.org",
        },
      ],
    };
  },
  provide() {
    return {
      resources: this.storedResources,
      addResource: this.addResource,
      deleteResource: this.deleteResource
    };
  },
  computed: {      
      storedButtonMode() {
          return this.selectedTab === 'stored-resources' ? null : 'flat'
      },
      addButtonMode() {
          return this.selectedTab === 'add-resource' ? null : 'flat'
      }
  },
  methods: {
    setSelectedTab(tab) {
      console.log("AAAAA", tab);
      this.selectedTab = tab;
    },
    addResource(title, description, url) {
        this.storedResources.unshift(
            {
                id: new Date().toISOString(),
                title, 
                description, 
                link: url
                });
                this.setSelectedTab('stored-resources');
    },
    deleteResource(resourceId) {
        const index = this.storedResources.findIndex(res => res.id === resourceId);
        console.log('TRINAM ', resourceId, index);
        this.storedResources.splice(index, 1);
    }
  },
};
</script>
