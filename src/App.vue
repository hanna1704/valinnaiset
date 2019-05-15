<template>

<div>
 
    <v-data-table
      v-model="valitutpakoliset"

      :items="pakolliset"
      item-key="nimi"
      class="elevation-1"
    >
      <template v-slot:headers="props">
        <tr>
          <th>
            
          </th>
          <th>
            Pakolliset valinnaiset
          </th>
          <th>
            Tunnus
          </th>
        </tr>
      </template>
      <template v-slot:items="rivi">
        <tr :active="rivi.selected" @click="vaihdavalintap(rivi)">
          <td>
            <v-checkbox
              :input-value="rivi.selected"
              :disabled="!saakovaihtaap(rivi)"
              primary
              hide-details
            ></v-checkbox>
          </td>
          <td>{{ rivi.item.nimi }}</td>
          <td class="text-xs-right">{{ rivi.item.tunnus }}</td>
          
        </tr>
      </template>
    </v-data-table>
    
  
  
    <v-data-table
      v-model="valitutvalinnaiset"

      :items="valinnaiset"
      item-key="nimi"
      class="elevation-1"
    >
      <template v-slot:headers="props">
        <tr>
          <th>
            
          </th>
          <th>
            Vapaasti valittavat valinnaisaineet
          </th>
          <th>
            Tunnus
          </th>
        </tr>
      </template>
      <template v-slot:items="props">
        <tr :active="props.selected" @click="vaihdavalintav(props)">
          <td>
            <v-checkbox
              :input-value="props.selected"
              :disabled="!saakovaihtaav(props)"
              primary
              hide-details
            ></v-checkbox>
          </td>
          <td>{{ props.item.nimi }}</td>
          <td class="text-xs-right">{{ props.item.tunnus }}</td>
          
        </tr>
      </template>
    </v-data-table>
    <ul>Pakolliset valinnaiset
      <li v-for="item in valitutpakoliset"> {{item.nimi}} </li>
      
    </ul>
    <ul>Vapaasti valittavat valinnaisaineet
      <li v-for="item in valitutvalinnaiset"> {{item.nimi}} </li>
      
    </ul>
    <v-flex md4>
          Nimi:<v-text-field v-model="name"  clearable />
    </v-flex>
    <v-flex   md4>
          Luokka:<v-text-field v-model="luokka"  clearable />
    </v-flex>

    <v-btn v-bind:disabled="name == ''" @click="save()">Save</v-btn>
    

</div>
</template>

<script>
import HelloWorld from './components/HelloWorld'
import * as easings from 'vuetify/es5/util/easing-patterns'

export default {
  
  data: () => ({
      
      valitutpakoliset: [],
      valitutvalinnaiset: [],
      name: '',
      luokka: '',
     
      pakolliset: [],
     
      valinnaiset: []
    }),
    created: function () {
      this.haetiedot()
    },
    methods: {
      haetiedot() {
        var vm = this
        var db = new restdb(process.env.VUE_APP_RESTDB_API_KEY);
        db.pakolliset.find({}, function(err, res){
          if (!err){
            console.log(res)
            vm.pakolliset = res
          }
        });
        db.valinnaiset.find({}, function(err, res){
          if (!err){
            console.log(res)
            vm.valinnaiset = res
          }
        });
      },
      save() {
       var db = new restdb(process.env.VUE_APP_RESTDB_API_KEY);

       var vastaus = {
         nimi: this.name, 
         luokka: this.luokka, 
         pvm: new Date(), 
         valinnat: this.valitutpakoliset.join("\n")  + "\n" + this.valitutvalinnaiset.join("\n")
      }

       var obj = new db.vastaukset(vastaus);

       obj.save(function(err, res){
        if (!err){
         console.log("onnistui")
        }
        else {
          console.log("ei onnistunut")
        }

      });
        
        
      },
      vaihdavalintap(rivi) {
        
        if  (this.saakovaihtaap(rivi)) {
         rivi.selected = !rivi.selected
        }


      },
      saakovaihtaap(rivi) {

        if (rivi.selected) {
          return true
        }
        for (var i=0 ; i < this.valitutvalinnaiset.length ; i++) {
          if (this.valitutvalinnaiset[i].tunnus == rivi.item.tunnus) {
            return false
          }
        }
        if (this.valitutpakoliset.length <= 1) {
          return true
        }
        return false
  
      },
      vaihdavalintav(rivi) {
        
        if  (this.saakovaihtaav(rivi)) {
         rivi.selected = !rivi.selected
        }


      },
      saakovaihtaav(rivi) {

        if (rivi.selected) {
          return true
        } 
        for (var i=0 ; i < this.valitutpakoliset.length ; i++) {
          if (this.valitutpakoliset[i].tunnus == rivi.item.tunnus) {
            return false
          }
        }
        if (this.valitutvalinnaiset.length <= 1) {
          return true
        }
        return false
  
      }

      
    }
  }

</script>
<style>
  
 #app {
   color: #00FFFF;
 }
 
 
</style>
