<template>
    <div class="container-fluid">
        <div class="row">
            <div class="col-lg-12">
                <h2 class="text-center my-4">BUKU</h2>
                <div class="my-3">
                    <form @submit.prevent="getBooks">
                        <input v-model="keyword" type="search" class="form-control rounded-5" placeholder="Mau baca apa hari ini?"> 
                    </form>
                </div>
                <div class="my-3 text-muted">menampilkan {{ books.length}}dari {{ book }}</div>
                <div class="row">
                    <div v-for="(book,i) in books" :key="i" class="col-lg-2">
                        <div class="card mb-4">
                            <NuxtLink :to="`/buku/${book.id}`">
                                <img :src="book.cover" class="cover" alt="cover">
                            </NuxtLink>
                        </div>
                    </div>
                </div>
            </div>
         </div>
     </div>
     <div class="d-flex justify-content-between">
        <nuxt-link to="/" class="btn btn-primary btn-lg rounded-5 px-5">
                        back
        </nuxt-link>
    </div>
</template>
<script setup>
const supabase = useSupabaseClient()
const keyword = ref('')
const books =ref([])
const book = ref(0)

const getBooks = async () => {
    const { data, error } = await supabase.from('buku').select(`*, kategori(*)`)
    .ilike('judul', `%${keyword.value}%`)
    if(data) books.value = data
}
const hitungData = async() => {
  const { data, count } = await supabase.from("buku").select("*", { count : 'exact'})
  if (data) book.value = count

}
onMounted(() => {
    getBooks()
})
</script>

<style scoped>
.card {
    width: 100%;
    padding: 0;
    border: none;
}

.card img {
    width: 90%;
    height: 30%;
}
.buku {
    width: 100%;
    height: 100%;
    object-fit: buku;
    object-position: 0 30;
}
</style>