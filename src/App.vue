<template>
<div>
  
    <v-data-table
      v-model="selected"

      :items="desserts"
      :pagination.sync="pagination"
      item-key="nimi"
      class="elevation-1"
    >
      <template v-slot:headers="props">
        <tr>
          <th>
            
          </th>
          <th>
            Valinnaiset aineet
          </th>
          <th>
            Tunnus
          </th>
        </tr>
      </template>
      <template v-slot:items="props">
        <tr :active="props.selected" @click="props.selected = !props.selected">
          <td>
            <v-checkbox
              :input-value="props.selected"
              :disabled="selected.length >=  4"
              primary
              hide-details
            ></v-checkbox>
          </td>
          <td>{{ props.item.nimi }}</td>
          <td class="text-xs-right">{{ props.item.tunnus }}</td>
          
        </tr>
      </template>
    </v-data-table>
    
  
  
    <v-data-table
      v-model="selected"

      :items="valinnaiset"
      :pagination.sync="paginatio"
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
        <tr :active="props.selected" @click="props.selected = !props.selected">
          <td>
            <v-checkbox
              :input-value="props.selectedt"
              :disabled="selected.length >= 4"
              primary
              hide-details
            ></v-checkbox>
          </td>
          <td>{{ props.item.nimi }}</td>
          <td class="text-xs-right">{{ props.item.tunnus }}</td>
          
        </tr>
      </template>
    </v-data-table>
    <ul>
      <li v-for="item in selected"> {{item.nimi}} </li>
      
    </ul>
    <v-flex xs12 sm6 md3>
          Nimi:<v-text-field v-model="name"  clearable />
    </v-flex>
    <v-flex xs12 sm6 md3>
          Luokka:<v-text-field v-model="luokka"  clearable />
    </v-flex>

    <v-btn v-bind:disabled="name == ''" :v-bind:disabled="luokka == ''" @click="save()">Save</v-btn>
    <v-list two-line>
      <template  v-for="option in selected2.entries()">{{ option[1] }} 
      
      
            
      </template>
    </v-list>

</div>
</template>

<script>
import HelloWorld from './components/HelloWorld'
import * as easings from 'vuetify/es5/util/easing-patterns'

export default {
  
  data: () => ({
      pagination: {
        sortBy: 'nimi'
      },
      selected: [],
      selected2: [],
      
     
      desserts: [
        {
          nimi: 'Verkkojen hallinta',
          tunnus: 123123
        },
        {
          nimi: 'Ice cream sandwich',
          tunnus: 237,
          
        },
        {
          nimi: 'Eclair',
          tunnus: 262,
          
        },
        {
          nimi: 'Cupcake',
          tunnus: 305,
          
        },
        {
          nimi: 'Olio-ohjelmointi',
          tunnus: 234234,
          
        },
        
      ],
      paginatio: {
        sortBy: 'name'
      },
      
     
      valinnaiset: [
        {
          nimi: 'Verkkojen hallinta',
          tunnus: 123123
        },
        
        {
          nimi: 'Olio-ohjelmointi',
          tunnus: 234234,
          
        },
        {
          nimi: 'Jelly bean',
          tunnus: 375,
         
        },
        {
          nimi: 'Lollipop',
          tunnus: 392,
         
        },
        {
          nimi: 'Honeycomb',
          tunnus: 408,
          
        },
       
      ]
    }),

    methods: {
      save() {

        this.selected2.push(this.name);
            this.name = "";
            var nimet = "";
            for (var i=0 ; i < this.selected2.length ; i=i+1) {
              nimet = this.selected2[i];
              
            };
        this.selected2.push(this.luokka);
            this.luokka = "";
            var luokat = "";
            for (var i=0 ; i < this.selected2.length ; i=i+1) {
              luokat = this.selected2[i];
              
            };
      }
      
    }
  }

</script>
<style scoped>
  
 #app {
   color: #00FFFF;
 }
 
</style>
