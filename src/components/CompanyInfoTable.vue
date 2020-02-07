<template>
  <table class="table">
    <tbody>   
      <tr>
        <th :key="value" v-for="(value, key) in companyData">{{key}}</th> 
      </tr>    
      
      <tr >
        <td :key="val" v-for="(val) in companyData">
          <table>
            <tbody>
              <tr>
                <td>{{val}}</td>
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
  name: 'CompanyInfoTable',
  props: {
    companyData: Object
  }   
}
</script>

<style scoped>
  table {
  font-family: 'Open Sans', sans-serif;
  border-collapse: collapse;
  margin: 10px 10px 0 10px;
}

table th {
  text-transform: uppercase;
  text-align: left;
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