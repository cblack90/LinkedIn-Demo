<template>
    <form>
        <a @click="addCategory" class="add"> + Add Category</a>
        <div v-for="(category, index) in categories" :key="category.id">
            <input type="text" v-model="category.name" :ref="category.name">
            <input type="number" v-model="category.display_order">
            <a @click="removeCategory(index)" class="remove">delete</a>
            <div>
                <img v-if="category.image" :src="`/images/${category.image}`" width="100">
                <label v-else>Image: </label>
                <input type="text" v-model.lazy="category.image">
            </div>
            <hr>
        </div>
    </form>
</template>

<script>
    export default {
        props: ['initialCategories'],
        data() {
            return {
                categories: _.cloneDeep(this.initialCategories)
            };
        },
        methods: {
            removeCategory(index) {
                if (confirm('Are you sure?')) {
                    this.categories.splice(index, 1);
                }
            },
            addCategory(){
                this.categories.push({
                    id:0,
                    name: '',
                    image: '',
                    display_order: this.categories.length + 1
                });
                this.$nextTick(() => {
                    window.scrollTo(0, document.body.scrollheight);
                    this.$refs[''][0].focus();
                });
            }
        }
    }
</script>

<style scoped>
    hr {
        margin-bottom: 30px;
    }
    img {
        vertical-align: middle;
    }
</style>