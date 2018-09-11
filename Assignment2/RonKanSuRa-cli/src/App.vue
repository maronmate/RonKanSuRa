<template>
  <div id="app">
    <div class="container">
        <div class="row justify-content-md-center">
            <div class="col-md-auto">
                <h1>Ron Kan Su Ra</h1>
            </div>

        </div>
        <div class="row justify-content-md-center">
            <div class="col-md-auto">
                <h2>Beveragel Menu</h2>
            </div>
        </div>
    </div>

     <div class="container">
            <div class="row">

                <div class="col">
                    <h5>Input Beveragel Type </h5>
                </div>

            </div>
            <div class="row">
                <div class="col">
                    <span>Beveragel Type : </span>

                    <input class="mr10" v-model="beverageTypeName" style="width: 300px;">

                    <b-button class="btn-add" v-on:click="addBeverageType"><i class="material-icons icon-btn">add_circle</i>
                        Add beverage Type</b-button>
                </div>
            </div>
            <br>

            <div v-for="(item, index) in beverageTypeList" :key="index">
                <b-card>
                    <b-card-header>
                        <div class="row tab-header">
                            <div class="col-8">
                                <h3><U>{{item}}</U></h3>
                            </div>
                            <div class="col-1"></div>
                            <b-button class="btn-delete" v-on:click="deleteBeverageType(index)"><i class="material-icons icon-btn">delete_forever</i>Remove
                                Type
                            </b-button>
                        </div>
                    </b-card-header>
                    <div class="row">
                            <div class="col">
                                <BeverageItem v-bind:beveragetypename="item"></BeverageItem>
                            </div>
                        </div>
                </b-card>
                <br>
            </div>
        </div>    
  </div>
</template>

<script>
import BeverageItem from './components/BeverageItem.vue'

export default {
  name: 'app',
  components: {
    BeverageItem
  },
  data: function () {
    return {
        beverageTypeList: [],
        beverageTypeName: null,
        yesCount: null,
        noCount: null,
    }
    },
    methods:
    {
        addBeverageType() {

            if (this.beverageTypeName != null && this.beverageTypeName !== '')
                this.beverageTypeList.push(this.beverageTypeName);
            this.beverageTypeName = '';
        },
        deleteBeverageType(index) {
            this.beverageTypeList.splice(index, 1);
        }
    }
}
</script>

<style>
.mr10
{
  margin-right: 10px;
}
.headerType{
    margin:2px;
    float: left;
}
.ColorRed{
    color:red;
}
.btn-delete
{
    background-color: #ea6565 !important;
}
.btn-add
{
    background-color: #50865c !important;
}
.icon-btn
{
    vertical-align: top;
}
header
{
    color:gray;
    height: 200px;
    background-color: gainsboro;
    border-color: gray;
   
}
#app{
    background-color: gainsboro;
}
body{
    background-color: gainsboro !important;
    color:gray !important;
}
</style>
