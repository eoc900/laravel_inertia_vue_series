<template>
    <app-layout>
        <!-- header -->
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                Books List
            </h2>
        </template>
        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="bg-white overflow-hidden shadow-xl sm:rounded-lg px-4 py-4">
                    <div class="bg-teal-100 border-t-4 border-teal-500 rounded-b text-teal-900 px-4 py-3 shadow-md my-3" role="alert" v-if="$page.props.flash.message">
                        <div class="flex">
                            <div>
                                <p class="text-sm">{{ $page.props.flash.message }}</p>
                            </div>
                        </div>
                    </div>

                    <button
                        @click="openForm()"
                        class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded my-3">Create New Book</button>

                    <!-- table -->
                    <table class="table-fixed w-full posts-table">
                        <thead>
                        <tr class="bg-gray-100">
                            <th class="px-4 py-2 w-20">No.</th>
                            <th class="px-4 py-2">Title</th>
                            <th class="px-4 py-2">Author</th>
                            <th class="px-4 py-2">Image</th>
                            <th class="px-4 py-2">Action</th>
                        </tr>
                        </thead>
                        <tbody>
                            <tr v-for="item in data.data">
                                <td class="px-4 py-2 border">{{ item.id }}</td>
                                <td class="px-4 py-2 border">{{ item.title }}</td>
                                <td class="px-4 py-2 border">{{ item.author }}</td>
                                <td class="px-4 py-2 border"><!-- image --></td>
                                <td class="border px-4 py-2">
                                    <button
                                        @click="openForm(item)"
                                        class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">Edit</button>
                                    <button
                                        @click="deleteItem(item)"
                                        class="bg-red-500 hover:bg-red-700 text-white font-bold py-2 px-4 rounded">Delete</button>
                                </td>
                            </tr>
                        </tbody>
                    </table>
                    <pagination :links="data.links"></pagination>
                    <book-form :isOpen="isFormOpen" :isEdit="isFormEdit" :form="formObject" @formsave="saveItem" @formclose="closeModal"></book-form>
                </div>
            </div>
        </div>
    </app-layout>
</template>

<script>

    const defaultFormObject = {
        title: null, author: null, image: null
    };

    import AppLayout from './../Layouts/AppLayout.vue';
    import Pagination from './../Components/pagination.vue'
    export default{
        props: ['data'],
        components: {
            AppLayout,
            Pagination
        }
    }

</script>