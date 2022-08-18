<template>
<div id="app">
  <div class="container my-5">
    <h1>Photo Listing</h1>
        <table class="table table-bordered" >
             <thead>
                <tr>
                    <!-- <th class="text-center" colspan="4">Photo Listing</th> -->
                </tr>
            </thead>
            <tbody>
                <tr>
                    <th class="id fw-bold" style="width:10%">ID</th>
                    <th class="url fw-bold" style="width:20%">Image</th>
                    <th class="url fw-bold" style="width:20%">URL</th>
                    <th class="Title fw-bold" style="width:20%">Title</th>
                    <th></th>
                </tr>
                <tr v-for="(photodetails, index) in photodetail" :key="photodetails.id">
                    <td>{{photodetails.id}}</td>
                    <td v-bind:style="{ 'background-image': 'url(' + photodetails.thumbnailUrl + ')' }"></td>
                    <td ><a href="">{{photodetails.url}}</a></td>
                    <td>{{photodetails.title}}</td>
                    <td>
                      <button type="button" class="btn btn-primary" @click="() => onSelect(photodetails)" >Compare</button>
                      <button style="margin-left:10px" type="button" class="btn btn-danger" @click="removeRow(index)">Remove</button>
                  </td>
                </tr>
            </tbody>
        </table>
    </div>
        <div class="container my-5">
          <h1>Comparison Table</h1>
        <table class="table table-bordered"  @v-model="clickedItem">
             <thead>
                <tr>
                    <!-- <th class="text-center" colspan="4"></th> -->
                </tr>
            </thead>
            <tbody>
                <tr >
                    <td class="id fw-bold" style="width:10%">image</td>
                    <td class="id fw-bold" style="width:10%">ID</td>
                    <td class="url fw-bold" style="width:20%">URL</td>
                    <td class="Title fw-bold" style="width:20%">Title</td>
                </tr>
                <tr v-for="(row) in clickedItem" :key="row.id">
                    <td v-bind:style="{ 'background-image': 'url(' + row.thumbnailUrl + ')' }"></td>
                    <td>{{row.id}}</td>
                    <td ><a href="">{{row.url}}</a></td>
                    <td>{{row.title}}</td>
                </tr>
            </tbody>
        </table>
    </div>
</div>
</template>

<script>
import axios from 'axios'

const baseURL = "https://jsonplaceholder.typicode.com/photos"

export default {
    name: 'App',
    data() {
        return {
            photodetail: [],
            clickedItem: [],
            isFavorite: false,
        }
    },
    async created() {
      try {
            const res = await axios.get(baseURL);
            this.photodetail = res.data;
        }catch (e) {
        console.error(e);
    }
    },
    methods: {
      async onSelect(photodetails) {
        this.isFavorite = true;
        this.clickedItem.push(photodetails);
        console.log(this.clickedItem);
        console.log(this.clickedItem[0].title);

        // const res = await axios.post(baseURL, {name: this.photodetail});
        // this.photodetail = [...this.photodetail, res.data];
        // this.compare = [];
        // this.$router.push('/Compare');
        // console.log(this.compare);
      },
      removeRow(clickedItem, index) {
      this.isFavorite = false;
      this.clickedItem.splice(index, 1);
      // console.log(this.clickedItem.splice(index, 1));
    }
    },
    
};
</script>

<style>
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
}
.tbl-fixed{
  -webkit-overflow-x:scroll;
  -moz-overflow-x: scroll ;
  overflow-x: scroll;
 }

</style>
