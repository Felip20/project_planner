<template>
    <div class="project" :class="{checking:vic.complete}">
        <div class="flexing">
            <div>
                <h3 @click="ShowData=!ShowData">{{vic.title}}</h3>
            </div>
            <div>
                <span class="material-icons" @click="deleteProject">
                    delete
                </span>
                <router-link :to="{name:'EditProject',params:{id:vic.id}}">
                    <span class="material-icons">
                        edit
                    </span>
                </router-link>
                <span class="material-icons" @click="doneProject">
                    done
                </span>
            </div>
        </div>
        <p v-if="ShowData">{{vic.detail}}</p>
            {{vic.complete}}
    </div>
</template>

<script>
export default {
    props:['vic'],
    data(){
        return{
            ShowData: false,
            api: "http://localhost:3000/projects/"
        }
    },
    methods:{
        deleteProject(){
            let deleteRoute = this.api+this.vic.id;
            fetch(deleteRoute,{method:"DELETE"})
            .then(()=>{
                this.$emit("dele",this.vic.id)
            })
            .catch(()=>{

            })
            
        },
        doneProject(){
            let updateRoute = this.api+this.vic.id;
            fetch(updateRoute,{method:"PATCH",
                headers:{
                    "Content-Type":"application/json"
                },
                body:JSON.stringify(
                    {
                        complete:!this.vic.complete
                    }
                )
            })
            .then(()=>{
                this.$emit("complete",this.vic.id)
            })
            .catch(()=>{

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
    border-left: 6px solid red;
    border-radius: 8px;
}

h3{
    cursor: pointer;
    color: cyan;
    font-style: italic;
}
p{
    color: black;
}
.flexing{
    display: flex;
    justify-content: space-between;
    align-items: center;
}
span{
    margin-left: 10px;
}
span:hover{
    cursor: pointer;
    color: #777;
}
.checking{
    border-left-color: green;
}

</style>