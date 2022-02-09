<template>
    <div class="project">
        <div class="flexing">
            <div>
                <h3 @click="ShowData=!ShowData">{{vic.title}}</h3>
            </div>
            <div>
                <span class="material-icons" @click="deleteProject">
                    delete
                </span>
                <span class="material-icons">
                    edit
                </span>
                <span class="material-icons">
                    done
                </span>
            </div>
        </div>
        <p v-if="ShowData">{{vic.detail}}</p>
        
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

</style>