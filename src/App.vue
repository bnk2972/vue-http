<template>
    <div class="container">
        <div class="row">
            <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
                <h1>Http</h1>
                <div class="form-group">
                    <label for="">Username</label>
                    <input type="text" class="form-control" v-model="user.username">
                </div>
                <div class="form-group">
                    <label for="">Email</label>
                    <input type="text" class="form-control" v-model="user.email">
                </div>
                <button @click="submit" class="btn btn-primary">Submit</button>
                <hr>
                <input type="text" class="form-control" v-model="node">
                <br>
                <button class="btn btn-primary" @click="fetchData">Get Data</button>
                <br><br>
                <ul class="list-group">
                    <li class="list-group-item" v-for="u in users">{{u.username}}</li>
                </ul>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data () {
            return {
                user: {
                    username: '',
                    email: ''
                },
                users: [],
                resource: [],
                node: 'data'
            }
        },
        methods: {
            submit () {
                // this.$http.post('data.json', this.user)
                //     .then(resource => {
                //         console.log(resource)
                //     }, error => {
                //         console.log(error)
                //     })
                // this.resource.save({}, this.user)
                this.resource.saveAlt(this.user)
            },
            fetchData () {
                // this.$http.get('data.json')
                //     .then(resource => {
                //         return resource.json()
                //     })
                //     .then(data => {
                //         const resultArray = [];
                //         for (let key in data) {
                //             resultArray.push(data[key])
                //         }
                //         this.users = resultArray;
                //     })
                this.resource.getData({
                    node: this.node
                }).then(resource => {
                    return resource.json()
                })
                .then(data => {
                    const resultArray = [];
                    for (let key in data) {
                        resultArray.push(data[key])
                    }
                    this.users = resultArray;
                })
            }
        },
        created () {
            const customActions = {
                saveAlt: {
                    method: 'POST',
                    url: 'alternative.json'
                },
                getData: {
                    method: 'GET'
                }
            }
            this.resource = this.$resource('{node}.json', {}, customActions)
        }
    }
</script>

<style>
</style>
