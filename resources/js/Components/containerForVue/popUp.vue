<template>
    <div v-if="OpenPopUp" class="container">
        <div class="block p-6 rounded-lg shadow-lg bg-white">
            <form @submit.prevent="submit" class="max-w-md mx-auto mt-7">
                <div class="block p-6 rounded-lg shadow-lg bg-white m-6">
                    <label class="p-2"  for="front">Front</label>
                    <input type="radio" value="Front"  v-model="form.title" name="title" id="front">
                    <label class="p-2" for="back">Back</label>
                    <input type="radio" value="Back" v-model="form.title" name="title" id="back">
                      <label class="p-2" for="fullstack">Full Stack</label>
                    <input type="radio"  value="fs" v-model="form.title" name="title" id="fullstack">
                     <label class="p-2" for="mobile">Mobile</label>
                    <input type="radio"  value="mobile" v-model="form.title" name="title" id="mobile">
                </div>

                <div class="form-group mb-6">
                    <input
                        v-model="form.salary"
                        type="number"
                        class="form-control block w-full px-3 py-1.5 text-base font-normal text-gray-700 bg-white bg-clip-padding border border-solid border-gray-300 rounded transition ease-in-out m-0 focus:text-gray-700 focus:bg-white focus:border-blue-600 focus:outline-none"
                        placeholder="Expected Salary"
                        required
                    />
                </div>
                <div class="form-group mb-6">
                    <input
                        v-model="form.duration"
                        type="number"
                        class="form-control block w-full px-3 py-1.5 text-base font-normal text-gray-700 bg-white bg-clip-padding border border-solid border-gray-300 rounded transition ease-in-out m-0 focus:text-gray-700 focus:bg-white focus:border-blue-600 focus:outline-none"
                        placeholder="Duration(Days)"
                        required
                    />
                </div>
                <div class="form-group mb-6">
                    <textarea
                        v-model="form.description"
                        type="textarea"
                        class="form-control block w-full px-3 py-1.5 text-base font-normal text-gray-700 bg-white bg-clip-padding border border-solid border-gray-300 rounded transition ease-in-out m-0 focus:text-gray-700 focus:bg-white focus:border-blue-600 focus:outline-none"
                        aria-describedby="emailHelp123"
                        placeholder="Description"
                        required
                    />
                </div>

                <button
                    :disabled="form.processing"
                    type="submit"
                    class="w-full px-6 py-2.5 bg-blue-600 text-white font-medium text-xs leading-tight uppercase rounded shadow-md hover:bg-blue-700 hover:shadow-lg focus:bg-blue-700 focus:shadow-lg focus:outline-none focus:ring-0 active:bg-blue-800 active:shadow-lg transition duration-150 ease-in-out"
                >
                    Post Job
                </button>
            </form>
        </div>
    </div>
</template>

<script setup>
import { reactive } from "vue";
import { Inertia } from "@inertiajs/inertia";
import { useForm, usePage } from "@inertiajs/inertia-vue3";

const form = useForm({
    user_id: usePage().props.value.auth.company.id,
    title: "",
    salary: "",
    duration: "",
    description: "",
});

defineProps({
    OpenPopUp: Boolean,
});
let submit = () => {
    Inertia.post(route("companies.store"), form);
};
</script>
<script>
export default {};
</script>
<style></style>
