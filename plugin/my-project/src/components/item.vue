/
<template>
  <main>
    <div class="top-card">
      <p>{{itemData.title}}</p>
    </div>
  </main>
</template>

<script>
  export default {
    name: 'item',
    data() {
      return {
        defaultText: 'Im a Random Article',
        topStoriesLink:'https://hacker-news.firebaseio.com/v0/topstories.json',
        topStories:[],
        itemId:0,
        itemData:{}
      }
    },
    mounted(){
      this.getItemList();
    },
    methods: {
      getItemList() {
        this.$http.get(this.topStoriesLink).then(
          function(response){
          // get body data
          console.log(response);
          this.topStories = response.body;

        }, function (error) {
          // error callback
          console.log(error.statusText);
        });
      },

      getItem(itemID){

        let itemLink = `https://hacker-news.firebaseio.com/v0/item/${itemID}.json`
        this.$http.get(itemLink).then(
          function(response){
            // get body data
            console.log(response);
            this.itemData = response.body;

          }, function (error) {
            // error callback
            console.log(error.statusText);
          });
      }
    },
    watch:{
      topStories(stories){
        console.log(stories);
        var randomNumber = Math.floor(Math.random() * stories.length)+0;
        this.itemId = stories[randomNumber]
        this.getItem(this.itemId);
      }
    }
  }
</script>

<style>

</style>
