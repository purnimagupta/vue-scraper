<template>
  <table class="table">
    <tbody >   
      <tr>
        <th :key="value" v-for="(value,key) in companyData">{{key}}</th> 
      </tr>    
      
      <tr >
        <td :key="value" v-for="(value) in companyData">
          <table>
            <tbody>
              <tr v-for="(val) in value" :key="val" >
                <template v-if="typeof(val) === 'object'">
                  <td v-for="(v, k) in val" :key="v" ><b>{{k}}</b> - {{ v}}</td>
                </template>
                <template v-else>
                  <td><h5><b>{{val}}</b></h5></td>
                </template>
              </tr>
            
            </tbody>
          </table>
        </td>
      </tr>
    </tbody>
  </table>
</template>   
<script>

export default {
  name: 'CompanyTable',
  props: {
    companyData: Object
  }   
}
</script>

<style scoped>
  table {
  font-family: 'Open Sans', sans-serif;
  /* width: 750px; */
  border-collapse: collapse;
  /* border: 3px solid #44475C; */
  margin: 10px 10px 0 10px;
}

table th {
  text-transform: uppercase;
  background: #44475C;
  color: #FFF;
  cursor: pointer;
  padding: 8px;
  min-width: 30px;
}
table th:hover {
  background: #717699;
}
table td {
  text-align: left;
  padding: 8px;
  border-right: 2px solid #7D82A8;
}
table td:last-child {
  border-right: none;
}
table tbody tr:nth-child(2n) td {
  background: #eaeef2;
} 
</style>

