<template>
	<form>
		<div class="form-group">
			<textarea class="form-control" placeholder="Type or paste text here" v-model="textContent" rows="5"></textarea>
		</div>
	</form>
</template>
<script>
	export default {
		name: 'Editor'
	}
</script>