<template>
	<div>
		<app-user-image></app-user-image>
		<h1 @click="myResume" class="my-resume usi-h1">My Resume</h1>
		<h1 class="usi-h1">Industry</h1>
    	<div class="checkbox-container-industry">
			<app-user-sidebar-industry
				v-for="industry in displayIndustries"
				:key="industry.id"
				:industry="industry"
				@industryAdded="addToIndustrySearch"
				@industryDeleted="removeFromIndustrySearch"
			>
			</app-user-sidebar-industry>
		</div>
		<h1 class="usjt-h1">Type</h1>
    	<div class="checkbox-container-job-type">
			<app-user-sidebar-job-type 
				v-for="jobtype in displayJobTypes"
				:jobtype="jobtype"
				:key="jobtype.id"
				@typeAdded="addToTypeSearch"
				@typeDeleted="removeFromTypeSearch">
					
			</app-user-sidebar-job-type>
		</div>
		<!-- <button class="job-search-btn">Search</button> -->
	</div>
</template>

<script>
import UserImage from './UserImage.vue';
import {EventBus} from '../../../../main.js';
import UserSidebarIndustry from './UserSidebarIndustry.vue';
import UserSidebarJobType from './UserSidebarJobType.vue';
import {mapGetters} from 'vuex';

export default {
	data() {
		return {
			searchIndustry: [],
			searchType: []
		}
	},
	computed: {
		...mapGetters(['displayIndustries', 'displayJobTypes']),
	},
	watch: {
		searchIndustry() {
			this.$router.push({ path: `/app/user/${this.$route.params.user_id}`})
			EventBus.$emit('searchIndustryChanged', this.searchIndustry)
		},
		searchType() {
			this.$router.push({ path: `/app/user/${this.$route.params.user_id}`})
			EventBus.$emit('searchTypeChanged', this.searchType)
		}
	},
	methods: {
		addToIndustrySearch(val) {
			this.searchIndustry.push(val)
		},
		removeFromIndustrySearch(val) {
			this.searchIndustry.splice(this.searchIndustry.indexOf(val), 1)
		},
		addToTypeSearch(val) {
			this.searchType.push(val)
		},
		removeFromTypeSearch(val) {
			this.searchType.splice(this.searchType.indexOf(val), 1)
		},
		myResume() {
			this.$router.push({path: `/app/user/${this.$route.params.user_id}/resume`})
		}
	},
	components: {
	  appUserImage: UserImage,
		appUserSidebarIndustry: UserSidebarIndustry,
		appUserSidebarJobType: UserSidebarJobType
	}
}
</script>

<style>
	.usjt-h1 {
	  font-size: 19px;
	  font-weight: bold;
	  color: #fff;
	  margin: 20px 0 5px 20px;
	}

	.usi-h1 {
        font-size: 19px;
        font-weight: bold;
        color: #fff;
        margin: 20px 0 5px 20px;
	}
	
	.my-resume {
		cursor: pointer;
	}

    .checkbox-container-industry {
        width: 90%;
        height: 30vh;
        display: flex;
        flex-direction: column;
		overflow-y: scroll;
        overflow-x: hidden;
	}

	.checkbox-container-job-type {
	  width: 90%;
	  height: 20vh;
	  display: flex;
	  flex-direction: column;
	}	

	.sidebar_option {
		display: flex;
  		align-items: center;
  		text-overflow: ellipsis;
  		white-space: nowrap;
  		width: 85%;
	}

	.sidebar_option .md-checkbox-label {
		overflow: hidden;
		white-space: nowrap;
		text-overflow: ellipsis;
		color: #fff;
	}

	.md-checkbox .md-checkbox-container {
		border: 1px solid rgba(255, 255, 255, 0.54);
	}

	/* .job-search-btn {
		height: 30px;
		width: 70px;
		font-size: 14px;
		outline: none;
		border: none;
		color: #fff;
		background: #3f51b5;
		margin-left: 20px;
		margin-top: 20px;
		cursor: pointer;
	}

	.job-search-btn:hover {
		color: #3f51b5;
		background: #fff;
	} */
</style>
