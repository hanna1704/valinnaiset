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
            :disabled="selected.length >= 2"
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
    <li v-for="item in selected"> {{item.nimi}}</li>
  </ul>
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
        {
          nimi: 'Donut',
          tunnus: 452,
          
        },
        {
          nimi: 'KitKat',
          tunnus: 518,
         
        }
      ]
    }),

    methods: {
      
    }
  }

</script>
<style scoped>
  
 #app {
   color: #00FFFF;
 }
 
</style>
