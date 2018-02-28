<template lang="pug">
div
  .form-group
    router-link.btn.btn-success(:to="{name: 'createCompany'}") Create new company

  .panel.panel-default
    .panel-heading Companies
    .panel-body
      table.table.table-bordered.table-striped
        thead
          tr
            th Name
            th Address
            th Website
            th Email
            th(width="100") &nbsp;
        tbody
          tr(v-for="(company,index) in companies" :key="index")
            td {{company.name}}
            td {{company.address}}
            td {{company.website}}
            td {{company.email}}
            td.flex
              router-link.rout.btn.btn-xs.btn-default(:to="{name: 'editCompany', params: {id: company.id}}") Edit
              a.btn.btn-xs.btn-danger(href="#" 'v-on:click'='deleteEntry(company.id,index)') Delete

</template>
 
<script>
export default {
  data: function () {
    return {
      companies: []
    }
  },
  mounted() {
    var app = this;
    axios.get('/api/v1/companies')
      .then(function (resp) {
        app.companies = resp.data;
      })
      .catch(function (resp) {
        console.log(resp);
        alert("Could not load companies");
      });
  },
  methods: {
    deleteEntry(id, index) {
      console.log(id);
      console.log(index);
      if (confirm("Do you really want to delete it?")) {
        var app = this;
        axios.delete('/api/v1/companies/' + id)
          .then(function (resp) {
            app.companies.splice(index, 1);
          })
          .catch(function (resp) {
            alert("Could not delete company");
          });
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.flex{
  display: flex;
}
.rout{
  margin-right: .3em;
}
</style>
