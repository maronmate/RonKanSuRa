<template>
    <div>
         <div class="container">
        <div class="row">
            <div class="col">
                <h6>{{TotelAnswer}}</h6>
            </div>
        </div>
        <div class="row">
            <div class="col">
                beverage : <input class="mr10"  v-model="beverageName">
    
                price : <input class="mr10"  v-model="price" type="number">
    
                <b-button class="btn-add" v-on:click="addBeverage"><i class="material-icons icon-btn">add_circle</i> Add beverage</b-button>
            </div>
        </div>
        <br>
        <div>

                    <template>
                        <b-table striped hover :items="beverageItemDataList" :fields="beveragHeader">
                            <template slot="action" slot-scope="row">
                                <b-button class="btn-delete mr-1" size="sm" @click.stop="deleteBeverage(row.index)"><i class="material-icons icon-btn">delete_forever</i>Remove</b-button>
                                <b-button size="sm" @click.stop="getAnswer(row.index)" class="mr-1"><i class="material-icons icon-btn">record_voice_over</i>Ask!</b-button>
                            </template>
                        </b-table>
                    </template>
        </div>
    </div>
    </div>
</template>
<script>
import axios from 'axios';
export default {
        props: ['beveragetypename'],
         data: function () {
        return {
            beverageName: null,
            price: null,
            answer: null,
            beverageItemDataList: [],

            beveragHeader: [ 'beverageName', 'price','answer' ,'action' ],
        };
    },
      methods:
    {
        addBeverage() {
            if (this.beverageName != null && this.beverageName !== '' && this.price != null && this.price !== '') {
                this.beverageItemDataList.push({ beverageName: this.beverageName, price: this.price, answer: '',answerList:[] });
                this.beverageName = '';
                this.price = '';
            }
        },
        deleteBeverage(index) {
            this.beverageItemDataList.splice(index, 1);
        },

        getAnswer(index) {
            var vm = this;
            axios.get('https://yesno.wtf/api')
                .then(function (response) {
                    vm.answer = response.data.answer;
                    vm.beverageItemDataList[index].answer = vm.answer;
                    vm.beverageItemDataList[index].answerList.push(vm.answer);
                    vm.answer = '';
                });
        }
    },
    computed:
    {
        TotelAnswer() {
            var result='';
            var countYes =0;
            var countNo = 0;
            for(let indexItem = 0; indexItem < this.beverageItemDataList.length; indexItem++)
            {
                for (let index = 0; index < this.beverageItemDataList[indexItem].answerList.length; index++) {
                    const answer = this.beverageItemDataList[indexItem].answerList[index];
                    if(answer==='yes')
                    {
                        countYes = countYes +1;
                    }
                    else if(answer==='no')
                    {
                        countNo=countNo+1;
                    }                
                }
            }
            
            result = '[yes = '+ countYes +', no = ' + countNo+']';
            return result;
        }
    }
}
</script>

