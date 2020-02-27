<template>
    <div>
        <mdb-container>
            <mdb-datatable
                    :data="data"
                    striped
                    bordered
                    arrows
                    :display="3"
                    responsive
                    :tfoot="false"
                    :pagination="pagination"
                    scrollY
                    maxHeight=2hv
                    maxWidth=auto
            />
        </mdb-container>
    </div>
</template>
<script>
    import axios from "axios";
    import { mdbDatatable, mdbContainer } from 'mdbvue';

    export default {
        name: "UserRepos",
        components: {
            mdbDatatable,
            mdbContainer
        },
        data() {
            return {
                columns: [],
                rows: [],
                pagination: false
            }
        },
        computed: {
            data() {
                return {
                    columns: this.columns,
                    rows: this.rows
                };
            },
        },
        created: function () {
            if (this.$isMobile()) {
                this.candidato = JSON.parse(localStorage.getItem('candidatoLocal'));
            } else {
                this.candidato = JSON.parse(this.$cookie.get("candidatoLocalPC"))
            }
        },
        mounted() {
            axios.get("https://api.github.com/users/"+this.candidato["usuario"]+ "/repos")
                .then(response =>  response.data)
                .then(response => {
                    //lenguaje, branch por defecto, url git, nombre y descripción.
                    let keys = ["lenguaje", "branch","url","nombre","descripción"];
                    let repo = [];
                    response.map( function(value, key) {
                        repo.push( { lenguaje : value.language , branch : value.default_branch, url : value.url, nombre: value.name, descripción: value.description });
                    });

                    let entries = this.filterData(repo, keys);

                    if (repo.length>=5) this.pagination = true; //app web
                    if (this.$isMobile()) { //mobile
                        this.pagination = false;
                    }
                                        //columns
                    this.columns = keys.map(key => {
                        return {
                            label: key.toUpperCase(),
                            field: key,
                            sort: 'asc'
                        };
                    });
                    //rows
                    entries.map(entry => this.rows.push(entry));

                })
                .catch(err => {
                    console.log("Fallo" + err)
                    // Manage the state of the application if the request
                    // has failed
                })
        },
        methods: {
            filterData(dataArr, keys) {
                let data = dataArr.map(entry => {
                    let filteredEntry = {};
                    keys.forEach(key => {
                        if (key in entry) {
                            filteredEntry[key] = entry[key];
                        }
                    });
                    return filteredEntry;
                });
                return data;
            }
        },
    }
</script>
