<template>
    <div class="row justify-content-center">
        <div class="col-md-8">
            <form-component
                @new="addThought">
            </form-component>

            <thought-component
                v-for="(thought, index) in thoughts"
                :key="thought.id"
                :thought="thought"
                @update="updateThought(index, ...arguments)"
                @delete="deleteThought(index)">
            </thought-component>
        </div>
    </div>
</template>

<script>
    export default {
        data(){
            return{
                thoughts:[]
            }
        },
        mounted() {
            axios.get('/controldoc/public/thoughts').then(Response=>{
                this.thoughts = Response.data;
            });
        },
        methods: {
            addThought(thought){
                console.log(thought);
                this.thoughts.push(thought);
            },
            updateThought(index, thought){
                console.log(thought);
                this.thoughts[index] = thought;
            },
            deleteThought(index){
                this.thoughts.splice(index, 1);
            }
        }
    }
</script>
