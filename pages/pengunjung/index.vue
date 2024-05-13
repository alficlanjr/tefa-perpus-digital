<template>
    <div class="container-fluid">
        <div class="row">
           <div class="col-lg-12">
             <h2 class="text-center my-4">RIWAYAT KUNJUNGAN</h2>
             <div class="my-3">
                <form  @submit.prevent="getPengunjung">
                <input v-model="keyword" type="search" class="form-control rounded-5" placeholder="Filter...">
                </form>
             </div>
             <div class="my-3 text-muted">menampilkan {{ visitors.length }} dari {{ visitor }}</div>
             <table class="table">
                <thead>
                     <tr >
                        <td>no</td>
                        <td>nama</td>
                        <td>keanggotaan</td>
                        <td>waktu</td>
                        <td>keperluan</td>
                        
                        </tr>
                </thead>
                <tbody>
                    <tr v-for="(visitor,i) in visitors" :key="i">
                        <td>{{ i+1 }}.</td>
                        <td>{{ visitor.nama }}</td>
                        <td>{{ visitor.keanggotaan.nama }}</td>
                        <td>{{ visitor.tgl }}, {{ visitor.waktu }}</td>
                        <td>{{ visitor.keperluan.nama }}</td>
                    </tr>
                </tbody>
             </table>
           </div> 
    </div>
    <div class="d-flex justify-content-between">
        <nuxt-link to="/" class="btn btn-primary btn-lg rounded-5 px-5">
                        back
        </nuxt-link>
    </div>
    </div>
</template>
<script setup>
const supabase = useSupabaseClient()
const visitor =ref(0)
const visitors = ref([])
const keyword = ref([])

const getPengunjung = async () => {
    const { data, error } = await supabase.from('pengunjung').select(`*, keanggotaan(*), keperluan(*)`).ilike('nama',`%${keyword.value}`) .order("id", { ascending: false });
    if(data) visitors.value = data
}
const hitungData = async() => {
  const { data, count } = await supabase.from("pengunjung").select("*", { count : 'exact'})
  if (data) visitor.value = count

}
onMounted(() => {
    getPengunjung()
    hitungData()
})
</script>