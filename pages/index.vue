<template>
<div>
    <!-- product section -->
    <section v-if="pending">
        <img src="~/assets/images/loading.gif" alt="">
    </section>

    <section v-else>
        <div class="mb-3">
            <label for="" class="form-label">Food</label>
            <select class="form-select form-select-lg" name="" id="" v-model="name" @change="getUrl(name)">
            <option selected>Select one</option>
            <option :value="category.strCategory" v-for="(category, index) in categoryData.categories" :key="index">{{category.strCategory }}</option>
            </select>
        </div>
        <div class="cointainer ms-auto grid lg:grid-cols-4 gap-4 m-3">
            <div v-for="(p, index) in data.meals" :key="index">
                <nuxt-link :to="`products/${p.idMeal}`">
                    <product-component :product="p" />
                </nuxt-link>
            </div>
        </div>
    </section>
</div>
</template>

<script setup>
let name = "";
const url = ref(`https://www.themealdb.com/api/json/v1/1/filter.php?c=Seafood`);

const {data: categoryData} = await useFetch("https://www.themealdb.com/api/json/v1/1/categories.php")
const {data} = useFetch(url, {refetch:true});
function getUrl(category){
    url.value =(`https://www.themealdb.com/api/json/v1/1/filter.php?c=${category}`)
    }
</script>

<style  scoped>

</style>
