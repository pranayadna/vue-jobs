<script>
import axios from "axios";
import JobListing from "./JobListing.vue";

export default {
    data() {
        return {
            state: {
                jobs: [],
                isLoading: true
            }
        }
    },
    components: {
        JobListing
    },
    props: {
        limit: Number,
        showButton: {
            type: Boolean,
            default: false
        }
    },
    mounted:
        async function () {
            try {
                const resp = await axios.get("http://localhost:8000/jobs");
                this.state.jobs = resp.data;
            } catch (error) {
                console.log("Error fetching jobs data", error);
            } finally {
                this.state.isLoading = false;
            }

        }
}
</script>

<template>
    <section class="bg-green-50 px-4 py-10">
        <div class="container-xl lg:container m-auto">
            <h2 class="text-3xl font-bold text-green-500 mb-6 text-center">
                Browse Jobs
            </h2>
            <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
                <JobListing v-for="job in state.jobs.slice(0, limit || state.jobs.length)" :key="job.id" :job="job" />
            </div>
        </div>
    </section>

    <section v-if="showButton" class="m-auto max-w-lg my-10 px-6">
        <RouterLink to="/jobs" class="block bg-black text-white text-center py-4 px-6 rounded-xl hover:bg-gray-700">View
            All Jobs</RouterLink>
    </section>
</template>
