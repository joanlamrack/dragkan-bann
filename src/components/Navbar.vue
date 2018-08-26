<template>
	<nav class="navbar navbar-expand-lg navbar-light bg-light">
  <a class="navbar-brand" href="#">DragKan-bann</a>
  <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
    <span class="navbar-toggler-icon"></span>
  </button>

  <div class="collapse navbar-collapse" id="navbarSupportedContent">
    <ul class="navbar-nav mr-auto">
     
    </ul>
      <button class="btn btn-outline-primary my-2 my-sm-0" data-toggle="modal" data-target="#exampleModalCenter" type="submit">Add Task</button>
  </div>
  <div class="modal fade" id="exampleModalCenter" tabindex="-1" role="dialog" aria-labelledby="exampleModalCenterTitle" aria-hidden="true">
  <div class="modal-dialog modal-dialog-centered" role="document">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title" id="exampleModalCenterTitle">Add new Task</h5>
        <button type="button" class="close" data-dismiss="modal" aria-label="Close">
          <span aria-hidden="true">&times;</span>
        </button>
      </div>
      <div class="modal-body">
        <form>
			<div class="form-group">
				<label for="exampleInputEmail1">Title</label>
				<input type="text" class="form-control" id="exampleInputEmail1" v-model="title" aria-describedby="emailHelp" >
			</div>
			<div class="form-group">
				<label for="exampleInputEmail1">Content</label>
				<input type="text" class="form-control" id="exampleInputEmail1" v-model="content" aria-describedby="emailHelp" >
			</div>
			<div class="form-group">
				<label for="exampleInputEmail1">Priority</label>
				<input type="number" class="form-control" id="exampleInputEmail1" v-model.number="priority" aria-describedby="emailHelp" >
			</div>
		</form>
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
        <button type="button" @click="addTask" data-dismiss="modal" class="btn btn-primary">Add</button>
      </div>
    </div>
  </div>
</div>
</nav>
</template>

<script>
export default {
	data(){
		return {
			title:"",
			content:"",
			priority:0
		}

	},
	methods:{
		addTask(){
			this.$emit("new-task", {
				title:this.title,
				content:this.content,
				priority:this.priority
			})
		}
	}
	
}
</script>

<style>
</style>
