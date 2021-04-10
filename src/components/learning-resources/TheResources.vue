<template>
    <base-card>
    <base-button @click="setSelectedTab('stored-resources')" :mode="seletedStoredButton">Stored Resources</base-button>
    <base-button @click="setSelectedTab('add-resources')" :mode="seletedAddButton">Add Resources</base-button>
    </base-card>
    <keep-alive>
    <component :is="seletedTab"></component>
    </keep-alive>
</template>

<script>
import BaseButton from '../UI/BaseButton.vue'
import AddResources from './AddResources.vue'
import StoredResources from './StoredResources'
export default {
      components: {
           BaseButton,
           StoredResources,
           AddResources
            },
  data () {
    return {
        seletedTab : 'add-resources',
        storedResources : [
            {
                id : 1,
                title : 'Official Guide',
                description : "The official Vue Resource Guide",
                link : 'https://vuejs.org'
            },
            {
                id : 2,
                title : 'Google',
                description : "Where you can find anything we may want to know",
                link : 'https://google.com'
            },
        ]
    };

  },
  methods : {
      setSelectedTab(tab){
          this.seletedTab = tab;
      },
      addResource(fromData){
          this.storedResources.unshift(fromData);
          this.seletedTab = 'stored-resources';
      },
      deleteResource(resId){
          const index = this.storedResources.findIndex(res => res.id == resId);
         this.storedResources.splice(index, 1);
        // console.log(deleteResource.length);
      }
  },
  computed : {
      seletedStoredButton(){
          return this.seletedTab === 'stored-resources' ? null : 'flat'
      },
      seletedAddButton(){
          return this.seletedTab === 'add-resources' ? null : 'flat'
      }
  },
  provide(){
      return {
          StoredResources : this.storedResources,
          addResource : this.addResource,
          deleteResource : this.deleteResource
      }
  }
    
}
</script>