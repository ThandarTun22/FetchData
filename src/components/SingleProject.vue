<template>
  <div class="project"  :class="{complete:project.complete}">
    <div class="flexing" >
        <div >
            <h3 @click="showDetail = !showDetail">{{project.title}}</h3>
        </div>
        <div>
            <span class="material-symbols-outlined" @click="deleteProject">
            delete
            </span>
            <router-link :to="{name:'editProject', params:{id:project.id}}">
                <span class="material-symbols-outlined">
                edit
                </span>
            </router-link>
            <span class="material-symbols-outlined" @click="completeProject">
            done
            </span>
        </div>
    </div>
    <p v-if="showDetail">{{project.detail}}</p>
    {{project.complete}}

  </div>
</template>

<script>
export default {
    props:['project'],
    data(){
        return{
            showDetail : false,
            api: 'http://localhost:3000/projects'
        }
    },
    methods:{
        deleteProject(){
            let deleteRoute = this.api+"/"+this.project.id;
            console.log(deleteRoute);
            fetch(deleteRoute, {method:"DELETE"})
            .then(()=>{
                this.$emit('delete', this.project.id)
            })
            .catch((err)=>{
                console.log(err);
            })
        },
        completeProject(){
            let updateCompleteRoute = this.api+"/"+this.project.id;
            console.log(updateCompleteRoute);
            fetch(updateCompleteRoute, {
                method: "PATCH",
                headers: {
                    "Content-Type": "application/json"
                },
                body: JSON.stringify(
                    {
                        complete: !this.project.complete
                    }
                )
                })
                .then(()=>{
                    this.$emit("complete",this.project.id)
                })
                .catch((err)=>{
                    console.log(err);
                })
        }
    }
}
</script>

<style>
    .project{
        padding: 20px;
        background-color: #f2f2f2;      
        margin: 10px;
        border-left: 6px solid crimson;
        border-radius: 8px;
    }
    h3{
        cursor: pointer;
        color: indigo;
    }
    .flexing{
        display: flex;
        justify-content: space-between;
        align-items: center;
    }
    span{
        margin-left: 3px;
    }
    span:hover{
        color: #777;
        cursor: pointer;
    }
    .complete{
        border-left-color: green;
    }
</style>

