<script>
import JobListing from "@/components/JobListing.vue";
import axios from "axios";

export default {
    data() {
        return {
            jobs: []
        }
    },
    components: {
        JobListing
    },
    mounted: async function () {
        try {
            const resp = await axios.get("http://localhost:8000/jobs");
            this.jobs = resp.data;
        } catch (error) {
            console.log("Error fetching jobs data", error);

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
                <!-- Job Listing 1 -->
                <JobListing v-for="job in jobs" :key="job.id" :job="job" />
            </div>
        </div>
    </section>
</template>