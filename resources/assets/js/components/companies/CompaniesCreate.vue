<template lang="pug">
  div
    .form-group
      router-link.btn.btn-default(to="/") Back

    .panel.panel-heading Create new Company
    .panel-body
      form('v-on:submit'="saveForm()")
        .row
          .col-xs-12.form-group
            label.contro-label Company name
            input.form-control(v-model="company.name")
        .row
          .col-xs-12.form-group
            label.contro-label Company address
            input.form-control(v-model="company.address")
        .row
          .col-xs-12.form-group
            label.contro-label Company website
            input.form-control(v-model="company.website")
        .row
          .col-xs-12.form-group
            label.contro-label Company email
            input.form-control(v-model="company.email")
        .row
          .col-xs-12.form-group
            button.btn.btn-success Create

</template>
 
<script>
export default {
  data: function () {
    return {
      company: {
        name: '',
        address: '',
        website: '',
        email: ''
      }
    }
  },
  methods: { 
    saveForm() { 
      event.preventDefault();
      var app = this;
      var newCompany = app.company;
      axios.post('/api/v1/companies', newCompany)
        .then(function (resp) {
          app.$router.push({path: '/'});
        })
        .catch(function (resp) {
          console.log(resp);
          alert("Could not create your company");
      });
    }
  }
}
</script>