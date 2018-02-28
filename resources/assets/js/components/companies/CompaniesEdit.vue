<template lang="pug">
    div
        .form-group
            router-link.btn.btn-default(to="/") Back

        .panel.panel-default
            .panel-heading Edit Company
            .panel-body
                form(v-on:submit="saveForm()")
                    .row
                        .col-xs-12.form-group
                            label.control-label Company name
                            input.form-control(v-model="company.name")
                    .row
                        .col-xs-12.form-group
                            label.control-label Company address
                            input.form-control(v-model="company.address")
                    .row
                        .col-xs-12.form-group
                            label.control-label Company website
                            input.form-control(v-model="company.website")
                    .row
                        .col-xs-12.form-group
                            label.control-label Company email
                            input.form-control(v-model="company.email")
                    .row
                        .col-xs-12.form-group
                            button.btn.btn-success Update

</template>

<script>
    export default {
        mounted() {
            let app = this;
            let id = app.$route.params.id;
            app.companyId = id;
            axios.get('/api/v1/companies/' + id)
                .then(function (resp) {
                    app.company = resp.data;
                })
                .catch(function () {
                    alert("Could not load your company")
                });
        },
        data: function () {
            return {
                companyId: null,
                company: {
                    name: '',
                    address: '',
                    website: '',
                    email: '',
                }
            }
        },
        methods: {
            saveForm() {
                var app = this;
                var newCompany = app.company;
                axios.patch('/api/v1/companies/' + app.companyId, newCompany)
                    .then(function (resp) {
                        app.$router.replace('/');
                    })
                    .catch(function (resp) {
                        console.log(resp);
                        alert("Could not create your company");
                    });
            }
        }
    }
</script>

<style lang="scss" scoped>
    form {
        
    }
</style>
