<template>
	<div>
		<div>
			<div class="jd-header">
				<h1 class="jd-h1">Job Description</h1>
			</div>
			<div class="jd-content-container">
				<div class="jd-flex">
					<div>
						<h2 class="jd-h2">Position Title</h2>
						<h2 class="jd-h2">Location</h2>
						<h2 class="jd-h2">Job Type</h2>
						<h2 class="jd-h2">Industry</h2>
						 <h2 class="jd-h2">Description</h2>
						 
						 
					</div>
					<div class="jd-inputs-container">

						<md-input-container class="jd-input-job-title" md-inline>
							<label>Enter job title here</label>
							<md-input v-model="postTitle"></md-input>
						</md-input-container>

						<md-input-container class="jd-input-job-title" md-inline>
							<label>Enter location here</label>
							<md-input v-model="postLocation"></md-input>
						</md-input-container>

						<md-input-container class="jd-select-job-type">
							<md-select v-model="postJobType" name="job-type" id="job-type">
								<md-option v-for="jobType in displayJobTypes"  :key="jobType.id" :value="jobType.id">{{jobType.name}}</md-option>
							</md-select>
						</md-input-container>

						<md-input-container class="jd-select-industry">
							<md-select v-model="postIndustry" name="industry" id="industry">
								<md-option v-for="industry in displayIndustries" :key="industry.id" :value="industry.id">{{industry.name}}</md-option>
							</md-select>
						</md-input-container>

						 <textarea v-model="postDescription" class="jd-textarea-desciption"></textarea>
					</div>
				</div>
			</div>
		</div>

	</div>
</template>

<script>
import {mapGetters} from 'vuex';
export default {
	data() {
		return {
			postTitle: '',
			postJobType: '',
			postLocation: '',
			postIndustry: '',
			postDescription: ''				
		}
	},
	computed: {
		...mapGetters(['displayIndustries', 'displayJobTypes'])
	},
	watch: {
		postTitle() {
			this.$emit('updateTitle', this.postTitle)
		},
		postLocation() {
			this.$emit('updateLocation', this.postLocation)
		},
		postJobType() {
			this.$emit('updateType', this.postJobType)
		},
		postIndustry() {
			this.$emit('updateIndustry', this.postIndustry)
		},
		postDescription() {
			this.$emit('updateDescription', this.postDescription)
		}
	}
}
</script>

<style>
.jd-header {
	height: 50px;
	background: linear-gradient(45deg, #1CB48B, #2ED590);
	border-top-left-radius: 5px;
	border-top-right-radius: 5px;
	display: flex;
	justify-content: space-between;
}

.jd-pencil {
	margin-right: 15px;
}

.jd-h1 {
	font-size: 22px;
	color: #fff;
	margin-left: 30px;
	display: flex;
	justify-content: center;
	flex-direction: column;
	height: 100%;
}

.jd-content-container {
	border-right: 1px solid #cccccc;
	border-bottom: 1px solid #cccccc;
	border-left: 1px solid #cccccc;
}

.jd-flex {
	display: flex;
	margin-left: 30px;
}


.test-flex {
	display: flex;
}

.jd-inputs-container {
	width: 50%;
	display: flex;
	flex-direction: column;
	margin-left: 30px;
	margin-top: 5px;
}

.jd-title-input {
	width: 100px;
	margin-top: 30px;
	margin-left: 30px;
}

.jd-textarea-desciption {
	width: 100%;
	margin: 35px 0;
	height: 150px;
	outline: #2ED590;
	font-size: 14px;
}

.jd-textarea-desciption:focus {
	outline: none;
	border: 2px solid #2ED590;
}

.jd-h2 {
	font-size: 17px;
	margin-top: 30px;
}

.jd-input-job-title {
	margin-left: 30px;
}

.jd-select-job-type {
	width: 100px;
}

.jd-select-industry {
	width: 300px;
}

.md-select .md-select-value {
	font-size: 14px;
}

.md-menu-item {
	font-size: 13px;
}

.md-list-item .md-list-item-container {
	font-size: 14px;
}

.md-input-container {
	margin: 0;
}

</style>
