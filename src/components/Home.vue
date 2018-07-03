<template>
	<div class="container-fluid">
		<div class="row">
			<div class="col-sm-8">
				<form>
					<div class="form-group">
						<textarea class="form-control" placeholder="Type or paste text here" v-model="textContent" rows="5" :change="getWordOccurrences()"></textarea>
					</div>
				</form>
				<!-- <editor></editor> -->
			</div>
			<div class="col-sm-4">
				<div class="card">
					<div class="card-header"><h5>Results</h5></div>
					<div class="card-body">
						
						<div class="card-text">
							<p><span class="badge badge-secondary">{{ textContent.length }}</span> characters</p>
							<p><span class="badge badge-secondary">{{ wordsCount }}</span> words</p>
						</div>
						<div class="card-header">Keyword density</div>
						<ul class="list-group list-group-flush" v-for="obj in getWordOccurrences()">
							<li class="list-group-item">{{ Object.values(obj)[0] }} <span class="badge badge-primary pull-right">{{Object.values(obj)[1] }}</span></li>
						  </ul>
					</div>
				</div>
			</div>
		</div>
	</div>
</template>
<script>
import Editor from '@/components/Editor'
	export default{
		name: 'Home',
		data() {
			return {
				textContent: ''
			}
		},
		components: { Editor },
		methods: {
			getWordOccurrences(){
				let content = this.textContent.split(" ");

				let newArray = [];
				let that = this;
				content.forEach(function(word, index, parentArray){
					let key = "";
					if(key = that.findObjectByKey(newArray, word, word)){
						key.count += 1;
					}
					else{
						let obj = {};
						obj[word] = word;
						obj['count'] = 1;
						newArray.push(obj);
					}
					
				});
				return newArray;
				
			},
			findObjectByKey(array, key, value) {

			    for (var i = 0; i < array.length; i++) {
			        if (array[i][key] === value) {
			            return array[i];
			        }
			    }
			    return null;
			}
		},
		computed: {
			wordsCount() {
				return this.textContent.length > 0 ? this.textContent.split(" ").length : 0;
			},
			keyDensity() {
				 
			}
		}
	}
</script>