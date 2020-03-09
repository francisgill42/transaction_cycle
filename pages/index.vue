<template>
<v-app>
<v-container class="white px-10">

<v-row v-for="(input,index) in inputs" :key="index">

<v-col
cols="12"
md="6"
>
<v-text-field
v-model="input.item"
label="Fund"
required
></v-text-field>
</v-col>

<v-col
cols="12"
md="4"
>
<v-text-field
type="number"
v-model="input.amount"
label="Balance"
required
></v-text-field>
</v-col>

<v-col
cols="12"
md="2"
>
<v-icon class="py-4 red--text"   @click="deleteRow(index)">mdi-delete</v-icon>
</v-col>


<v-col
cols="12"
md="2"
>

</v-col>
</v-row>
<v-row>
<v-col
cols="12"
md="2"
>
Total {{total}}
</v-col>
</v-row>

<v-row>
<v-col
cols="12"
md="2"
>
IBFT Limit {{ibft_limit}}
</v-col>
</v-row>


<v-row>
<v-col
cols="12"
md="2"
>
<v-btn @click="add_item">Add Fund +</v-btn>
</v-col>

<v-col
cols="12"
md="4"
>
<!-- <v-btn class="info" >Submit Transaction</v-btn> -->
</v-col>

</v-row>

</v-container>
</v-app>      
</template>
<script>
export default {
data: () => ({
res:'',    
inputs: [{
item: '',
amount: 0,
}],
}),
computed:{
    total(){
        return this.inputs.reduce((sum,p) => {
            return parseInt(sum) + parseInt(p.amount)
        },0)
    },
      ibft_limit () {
            return this.total  >= 666666.65 ? 500000 : (this.total/100) * 75
    }
},
methods:{

deleteRow(index) {
this.inputs.splice(index,1)
},
add_item(){
this.inputs.push({
item: '',
amount: 0
});
},
}

}
</script>