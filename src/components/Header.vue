<script setup>
import { reactive, onMounted } from 'vue'

const state = reactive({
  repositories: []
})

onMounted(() => {
  fetch('https://api.github.com/users/Abdulquadri-Akos', {
    method: 'GET',
    headers: {
      'X-Github-Api-Version': '2022-11-28',
      Accept: ' application/vnd.github+json'
    }
  }).then((res) =>
    res.json().then((data) => {
      state.repositories = data
      //   console.log(data)
    })
  )
})
</script>
<template>
  <section class="mt-80 mb-64">
    <div class="grid grid-cols-5 gap-4 w-fit">
      <div class="flex flex-col justify-center items-center row-span-2">
        <img
          class="rounded-full border-solid border-2 border-black w-4/5"
          :src="state.repositories?.avatar_url"
          alt="github_avatar"
        />
        <h2 class="text-2xl font-bold text-center pt-2">{{ state.repositories.name }}</h2>
        <p class="text-center">{{ state.repositories.bio }}</p>
      </div>
      <div class="bg-black text-white col-span-4 p-4 rounded-md">
        <h3 class="text-lg font-bold">About Me</h3>
        <p class="pt-4 text-justify">
          I'm Abdulquadri Akosile, a passionate and dedicated individual pursuing my education at
          AltSchool Africa. I am immersed in a dynamic learning environment that fosters innovation
          and creativity in the technology field. I am currently a student at AltSchool Africa,
          where I am honing my skills and knowledge in various aspects of computer science and
          software development. In addition to my academic pursuits, I have practical experience in
          Desktop Publishing. This has allowed me to blend my technical skills with a creative
          touch, producing visually appealing and user-friendly designs.
        </p>
      </div>
      <div class="bg-primary text-black col-span-2 p-4 h-85">
        <h3 class="text-lg font-bold">Repositories</h3>
        <p class="text-xl pt-2">{{ state.repositories.public_repos }}</p>
      </div>
      <div class="bg-primary text-black col-span-1 p-4 h-85">
        <h3 class="text-lg font-bold">Following</h3>
        <p class="text-xl pt-2">{{ state.repositories.following }}</p>
      </div>
      <div class="bg-primary text-black col-span-1 p-4 h-85">
        <h3 class="text-lg font-bold">Followers</h3>
        <p class="text-xl pt-2">{{ state.repositories.followers }}</p>
      </div>
    </div>
  </section>
</template>
<style scoped></style>
