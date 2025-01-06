<template>
    <h1>Get Data</h1>
    <button class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#exampleModal">Add New User</button>
    <div class="get-data-sec">
        <table class="table table-bordered" v-if="userVisible">
            <thead>
                <tr>
                    <th>Sr. No.</th>
                    <th>Title</th> 
                    <th>Body</th>
                    <th>Action</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(item,index)  in list" :key="index">
                    <td>{{ index + 1 }}</td> 
                    <td>{{ item.title }}</td>
                    <td>{{ item.body }}</td>
                    <td>
                        <button class="btn btn-primary" v-on:click="NextPage(item.id)" v-if="isVisible & item.id !== isVisit">Next</button>
                        <button class="btn btn-primary" v-if="!isVisible" @click="userDetail" >Detail</button>
                        <button class="btn btn-primary" v-if="item.id === isVisit" @click="deleteItem(index)">Delete  </button>
                    </td>
                </tr>
            </tbody>
        </table>
        <table class="table table-bordered" v-if="!userVisible">
            <thead>
                <tr>
                    <th>Sr. No.</th>
                    <th>Name</th> 
                    <th>Email</th>
                    <th>Body</th>
                    <th>Action</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(item,index) in list2" :key="index">
                    <td>{{ index + 1 }}</td>
                    <td>{{ item.name }}</td>
                    <td>{{ item.email }}</td>
                    <td>{{ item.body }}</td>
                    <td>
                        <button class="btn btn-primary" v-if="!isVisible" @click="deleter(item)">Delete</button>
                    </td>
                </tr>
            </tbody>
        </table>
        

        <!-- Modal -->
        <div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
            <div class="modal-dialog">
                <div class="modal-content">
                    <div class="modal-header">
                        <h5 class="modal-title" id="exampleModalLabel">Add User</h5>
                        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                    </div>
                    <div class="modal-body">
                        <form @submit.prevent="getFormValues">
                            <input type="text" class="form-control" placeholder="ID" v-model="createList.id" required>
                            <input type="text" class="form-control" placeholder="Title" v-model="createList.title" required>
                            <input type="text" class="form-control" placeholder="Body" v-model="createList.body" required>
                            <button type="submit" class="btn btn-success">Save changes</button>
                        </form>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
import axios from 'axios'
    export default{
        name: 'getData',
        data(){
            return{
                list:[],
                isVisible:true,
                userVisible:true,
                isVisit:'',
                list2:[], 
                createList:[{
                    id: "",
                    title: "",
                    body: "",
                }],
            }
        },
        created(){
            this.dataResult();
        },
        methods:{
            async dataResult(){
                let result = await axios.get("https://jsonplaceholder.typicode.com/posts");
                this.list = result.data;
            },
            async NextPage(id){
                let result = await axios.get(`https://jsonplaceholder.typicode.com/posts/${id}`);
                let second =  result.data;
                this.list = [second];
                this.isVisible = !this.isVisible;
                
            },
            async userDetail(){
                let result = await axios.get(`https://jsonplaceholder.typicode.com/posts/1/comments/`);
                this.list2 = result.data;
                this.userVisible = !this.userVisible;
            },
            deleter(item){
                this.list2.splice(item, 1)
            },
            getFormValues() {
                const newData = this.createList; 
                this.list.push(newData);
                this.isVisit = newData.id  
            },
            deleteItem(index) {
                this.list.splice(index, 1); // For arrays
                }
 
        }
        
        
    }
</script>
<style>
    .get-data-sec{
        padding: 30px;
    }
    table th{
        background-color: #efefef;
    }
    .form-control{
        margin-bottom: 20px;
    }
</style>