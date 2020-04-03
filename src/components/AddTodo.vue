<template>
    <div>
        <form @submit="addTodo" >
            <input type="text" v-model="title" name="title" placeholder="add Todo item...">
            <input type="submit" value="Submit" class="btn">
        </form>
    </div>
</template>

<script>
export default {
		name: "AddTodo",
		data() {
			return {
				title: ''
			}
		},
		methods: {
			addTodo(e) {
				e.preventDefault(); //To avoid default behavior on submit
				const newTodo = {
					title: this.title,
					completed: false
				}
				this.$emit('add-todo', newTodo)
				this.title = '' //clear the input after create
			}
		}
}
</script>

<style scoped>
	form {
		display: flex;
		height: 5rem;
		padding: 0.8rem;
	}

	input[type="text"] {
		flex: 10;
		padding: 5px;
	}

	input[type="submit"] {
		flex: 2;
	}
</style>