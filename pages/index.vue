<template>
    <div class="container-fluid">
        <div class="row my-5">
            <div class="col-lg-6">
                <nuxt-link to="/pengunjung/tambah">
                    <div class="card bg-pengunjung rounded-5 mb-3">
                        <div class="card-body">
                            <h2>pengunjung</h2>
                        </div>
                    </div>
                </nuxt-link>
            </div>

            <div class="col-lg-6">
                <nuxt-link to="/buku">
                    <div class="card bg-buku rounded-5">
                        <div class="card-body">
                            <h2>Cari Buku</h2>
                        </div>
                    </div>
                </nuxt-link>
            </div>
        </div>
    </div>

    <h2 class="mt-5" style="font-family: inter; margin-left: 150px;">STATISTIK</h2>
    <div class="container-fluid">
        <div class="row my-5">
            <div class="col-lg-6"> 
                <div class="card bg-warning rounded-5 mb-3">
                    <div class="pengunjung1">
                        <div class="card-body">
                            <h1 style="font-size: 110px;">{{ visitor }}</h1>
                            <h2>pengunjung</h2>
                        </div>
                    </div>
                </div>    
            </div>
            <div class="col-lg-6">
                <div class="card bg-primary rounded-5">
                    <div class="buku1">
                        <div class="card-body">
                            <h1 style="font-size: 110px;">{{ book }}</h1>
                            <h2>Buku</h2>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <div>
            <Chart />
        </div>
    </div>

    <!-- <div class="container">
        <div class="d1"></div>
        <div class="d2"></div>
        <div class="d3"></div>
        <div class="d4"></div>
        <div class="d5"></div>
        <div class="d6"></div>
    <ul class="content">
        <li><div>100%</div></li>
        <li><div>80%</div></li>
        <li><div>50%</div></li>
        <li><div>30%</div></li>
        <li><div>10%</div></li>
        <li><div>0%</div></li>
    </ul>
    </div> -->
</template>

<style scoped>
.card {
    height:258px;
    box-shadow: 1px 1px 10px #424242;
}
.card.bg-pengunjung {
    background-image: url('../assets/img/kunjungan.jpeg');
    background-repeat: no-repeat;
    background-position: center center;
    background-size: cover;
    color: rgb(252, 251, 251);
}
.card.bg-buku {
    background: url('../assets/img/buku.jpg') no-repeat center center;
    background-size: cover;
    color: rgb(245, 244, 244);
}
</style>
<script setup>
const supabase = useSupabaseClient()
const book = ref(0)
const visitor = ref(0)

const hitungDatabuku = async() => {
  const { data, count } = await supabase.from("buku").select("*", { count : 'exact'})
  if (data) book.value = count

}
const hitungData = async() => {
  const { data, count } = await supabase.from("pengunjung").select("*", { count : 'exact'})
  if (data) visitor.value = count

}
onMounted(() => {
  hitungDatabuku()
  hitungData()
})
</script>
