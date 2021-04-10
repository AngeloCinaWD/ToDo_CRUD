<template>
    <div class="w-25">
        <form @submit.prevent="saveData()">
            <div class="input-group mb-3 w-100">
                <input
                    v-model="title"
                    type="text"
                    class="form-control form-control-lg"
                    aria-label="Recipient's username"
                    aria-describedby="button-addon2"
                    required
                />
                <button
                    class="btn btn-success"
                    type="submit"
                    id="button-addon2"
                >
                    Add this to your list
                </button>
            </div>
        </form>
        <div class="w-25">
            <div class="w-100" v-for="todo in todos" :key="todo.id">
                {{ todo.title }}
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            todos: "",
            title: ""
        };
    },
    methods: {
        getTodos() {
            axios.get("/api/todo").then(res => {
                this.todos = res.data;
            });
        },
        saveData() {
            let data = new FormData();
            data.append("title", this.title);
            axios.post("/api/todo", data).then(res => {
                this.title = "";
                this.getTodos();
            });
        }
    },
    mounted() {
        this.getTodos();
    }
};
</script>
