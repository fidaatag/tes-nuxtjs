<template>

  <CompNavbar />

  <section class="mb-4 px-2 w-full max-w-md mx-auto mt-10">
    <div class="relative">
      <div class="absolute left-0 inset-y-0 pl-3 flex items-center">
        <svg class="fill-current h-6 w-6 text-gray-400" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20"><path d="M12.9 14.32a8 8 0 1 1 1.41-1.41l5.35 5.33-1.42 1.42-5.33-5.34zM8 14A6 6 0 1 0 8 2a6 6 0 0 0 0 12z" /></svg>
      </div>

      <input v-model="search" @input="handleSearch" class="w-full border pl-12 pr-4 py-2 rounded-full focus:border-gray-500 focus:shadow-outline outline-none" type="text" placeholder="Search..." />
    </div>
  </section>


  <section class="mt-10 grid max-w-md gap-10 row-gap-8 lg:max-w-screen-lg sm:row-gap-10 lg:grid-cols-3 xl:max-w-screen-lg sm:mx-auto">
    <div v-for="product in filteredProducts" :key="product.id">
      <div class="flex flex-col transition duration-300 bg-white rounded shadow-sm hover:shadow">
        <div class="w-full h-48 flex justify-center border">
          <img :src="product.thumbnail" class="h-48"/>
        </div>
        <div class="flex flex-col justify-between flex-grow p-8 border border-t-0 rounded-b">
          <div>
            <div class="text-lg font-semibold h-16">{{ product.title }}</div>
            <p class="text-sm text-gray-900 line-clamp-3">
              {{ product.description }}
            </p>
            <div class="mt-1 mb-4 mr-1 text-4xl font-bold sm:text-5xl">${{ product.price }}</div>
          </div>
          <a
            href="#"
            class="inline-flex items-center justify-center w-full h-12 px-6 font-medium tracking-wide text-white transition duration-200 rounded shadow-md bg-purple-400 hover:bg-purple-700 focus:shadow-outline focus:outline-none"
          >
            Buy Basic
          </a>
        </div>
      </div>
    </div>
  </section>

</template>

<script setup>

  const search = ref('')
  const allProduct = ref([])
  const filteredProducts = ref([]);

  const getAllProducts = async () => {
    try {
      const response = await fetch('https://dummyjson.com/products');
      if (!response.ok) {
        throw new Error('Failed to fetch products');
      }
      const data = await response.json();
      return data.products;
    } catch (error) {
      console.error('Error fetching products:', error);
      return [];
    }
  };

  const searchContent = () => {
    return allProduct.value.filter(product =>
      product.title.toLowerCase().includes(search.value.toLowerCase())
    );
  };

  const handleSearch = () => {
    filteredProducts.value = searchContent();
  };

  getAllProducts().then(product => {
    allProduct.value = product;
    filteredProducts.value = searchContent()
  })


</script>