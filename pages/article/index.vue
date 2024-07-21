<template>
  
  <CompNavbar />

  <section class="px-4 py-16 mx-auto sm:max-w-xl md:max-w-full lg:max-w-screen-xl md:px-24 lg:px-8 lg:py-20">
    <div class="grid gap-5 lg:grid-cols-3 sm:max-w-sm sm:mx-auto lg:max-w-full">
      <div v-for="article in allArticle">        
        <div class="overflow-hidden transition-shadow duration-300 bg-white rounded">
          <a href="#" aria-label="Article"><img src="https://random.imagecdn.app/500/150" class="object-cover w-full h-64 rounded" alt="" /></a>
          <div class="py-5">
            <p class="mb-2 text-xs font-semibold text-gray-600 uppercase">
              13 Jul 2020
            </p>
            <a href="/" aria-label="Article" class="inline-block mb-3 text-black transition-colors duration-200 hover:text-deep-purple-accent-700"><p class="text-2xl font-bold h-16">{{ article.title }}</p></a>
            <p class="mb-4 text-gray-700 line-clamp-3">
              {{ article.body }}
            </p>
            <div class="flex space-x-4">
              <a href="#" aria-label="Likes" class="flex items-start text-gray-800 transition-colors duration-200 hover:text-deep-purple-accent-700 group">
                <div class="mr-2">
                  <svg
                    xmlns="http://www.w3.org/2000/svg"
                    width="24"
                    height="24"
                    viewBox="0 0 24 24"
                    stroke="currentColor"
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                    class="w-5 h-5 text-gray-600 transition-colors duration-200 group-hover:text-deep-purple-accent-700"
                  >
                    <polyline points="6 23 1 23 1 12 6 12" fill="none" stroke-miterlimit="10"></polyline>
                    <path d="M6,12,9,1H9a3,3,0,0,1,3,3v6h7.5a3,3,0,0,1,2.965,3.456l-1.077,7A3,3,0,0,1,18.426,23H6Z" fill="none" stroke="currentColor" stroke-miterlimit="10"></path>
                  </svg>
                </div>
                <p class="font-semibold">{{ article.reactions.likes }}</p>
              </a>
              <a href="#" aria-label="Comments" class="flex items-start text-gray-800 transition-colors duration-200 hover:text-deep-purple-accent-700 group">
                <div class="mr-2">
                  <svg
                    xmlns="http://www.w3.org/2000/svg"
                    width="24"
                    height="24"
                    viewBox="0 0 24 24"
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                    stroke="currentColor"
                    class="w-5 h-5 text-gray-600 transition-colors duration-200 group-hover:text-deep-purple-accent-700"
                  >
                    <polyline points="23 5 23 18 19 18 19 22 13 18 12 18" fill="none" stroke-miterlimit="10"></polyline>
                    <polygon points="19 2 1 2 1 14 5 14 5 19 12 14 19 14 19 2" fill="none" stroke="currentColor" stroke-miterlimit="10"></polygon>
                  </svg>
                </div>
                <p class="font-semibold">{{ article.views }}</p>
              </a>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>

</template>

<script setup>

  const getAllArticle = await $fetch('https://dummyjson.com/posts');
  const allArticle = getAllArticle ? getAllArticle.posts : []

</script>