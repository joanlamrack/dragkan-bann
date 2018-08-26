<template>
	<div class="col-4">
		<div class="card" v-if="!(Object.keys(kanbandata) > 0)">
		
		<div class="card-body">
			{{kanbantitle}}<br>
				<div class="card kanban" @ v-for="(kanbanitem,key) of kanbandata.list" :key="key">
					<button type="button" v-if="!!kanbandata.previous" @click="moveToPrevious(key)" class="btn btn-primary float-left"><</button>
					<div class="card-body">
						<h5 class="card-title">{{kanbanitem.title}}</h5>
						<h6 class="card-subtitle mb-2 text-muted">Priority :{{kanbanitem.priority}}</h6>
						<p class="card-text">{{kanbanitem.content}}</p>
						
					</div>
					<button type="button float-right" v-if="!!kanbandata.next" @click="moveToAfter(key)" class="btn btn-primary float-right">></button>
				</div>
					
		</div>
		
		</div>
	</div>
  
</template>

<script>
export default {
  name: 'List',
  props: ["kanbantitle","kanbandata"],
  methods:{
	  moveToAfter(index){
		  this.$emit("move-after",{
			  index:index,
			  from:this.kanbantitle,
			  destination:this.kanbandata.next
		})
	  },
	  moveToPrevious(index){
		  this.$emit("move-previous",{
			  index:index,
			  from:this.kanbantitle,
			  destination:this.kanbandata.previous
		})
	  }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
	.kanban{
		height: 200px;
	}
	.float-left, .float-right{
		width: 40px;
		height: 40px;
		position: relative;
	}

	.float-left{
		top:90px;
		left:-20px;
	}

	.float-right{
		margin-left:95%;
		top:-70px;
	}
</style>
