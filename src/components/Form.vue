<template>
  <div>
    <b-card>
      <b-form @submit="onSubmit" v-if="show">
        <div class="ui vertical segment">
          <div class="flexbox">
            <div class="flex-content">
              <b-form-group
                id="input-group-1"
                label="Company Symbol"
                label-for="input-1"
              />
              <div>
                <basic-select
                  :options="companies"
                  :selected-option="selectedCompany"
                  placeholder="Enter Company symbol"
                  @select="onCompanySelect"
                  required
                />
              </div>
              <b-form-group
                id="input-group-2"
                label="Period"
                label-for="input-2"
              />
              <basic-select
                :options="periods"
                :selected-option="selectedPeriod"
                placeholder="Select period"
                @select="onPeriodSelect"
                required
              />
            </div>
          </div>
        </div>  
        <b-button type="submit" >Submit</b-button>
      </b-form>
       <CompanyInfoTable :companyData="companyData"/>
    </b-card>
  </div>
</template>

<script>

import { BasicSelect } from 'vue-search-select';
import CompanyInfoTable from './CompanyInfoTable';

export default {
  name: 'Form',
  components: {
    BasicSelect,
    CompanyInfoTable
  },
  data() {
    return {
      companies: [
        { value: '1', text: 'INFY' },
        { value: '2', text: 'TCS' },
        { value: '2', text: 'CHAMBLFERT' },
      ],
      periods: [
        { value: '1', text: 'Last 1 Year'},
        { value: '2', text: 'Last 2 Years'},
        { value: '3', text: 'Last 5 Years'},
        { value: '4', text: 'More than 5 Years'}
      ],
      searchText: '', // If value is falsy, reset searchText & searchItem
      selectedCompany: {
        value: '',
        text: ''
      },
      selectedPeriod: {
        value: '',
        text: ''
      },
      form: {
        symbol: '',
        Period: '',
      },
      companyData: {},
      show: true
    }
  },
  methods: {
    onSubmit(evt) {
      evt.preventDefault()
        const { symbol, Period } = this.form;
        // var that = this;
        const baseURI = 'http://localhost:3000/api/search'
        console.log(`${baseURI}?symbol=${symbol}&&Period=${Period}`)

        this.$http.get(`${baseURI}?symbol=${symbol}&&Period=${Period}`)
          .then((result) => {
            console.log(result.data.data)
            const data = JSON.parse(result.data.data)
            this.companyData = data;
        })
    },
    onCompanySelect (item) {
      this.selectedCompany = item
      this.form.symbol = item.text;
    },   
    onPeriodSelect (item) {
      this.selectedPeriod = item
      this.form.Period = item.text;
    },
  }  
}
</script>
