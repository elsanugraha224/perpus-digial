<template>
    <div class="container-fluid">
        <div class="row my-5">
            <div class="col-lg-6 box">
                <nuxt-link to="../pengunjung/tambah">
                    <div class="card bg-pengunjung rounded-5">
                        <div class="card-body">
                            <h2>PENGUNJUNG</h2>
                        </div>
                    </div>
                </nuxt-link>
            </div>
            <div class="col-lg-6 box">
                <nuxt-link to="../buku">
                    <div class="card bg-buku rounded-5">
                        <div class="card-body">
                            <h2>CARI BUKU</h2>
                        </div>
                    </div>
                </nuxt-link>
            </div>
        </div>
    </div>
    <h2 style="margin: 30px"><strong>STATISTIK</strong></h2>
  <div class="Container-fluid">
    <div class="row justify-content-evenly rounded-3">
      <div class="col-5">
        <nuxt-link to="/pengunjung">
        <div class="card-body text">
          <div class="raccing">
            <h2><span class="no">{{ jml_pengunjung }}</span> pengunjung</h2>
          </div>
        </div>
        </nuxt-link>
      </div>
      <div class="col-5">
        <nuxt-link to="https://perpus-digial.vercel.app/buku">
        <div class="raccing1">
          <h2><span class="no">{{ jml_buku }}</span> Buku</h2>
        </div>
        </nuxt-link>
      </div>
      <div class="line">
        <statistik/>
      </div>
    </div>
  </div>
</template>

<script setup>
const supabase = useSupabaseClient()
const jml_pengunjung = ref(0)
const jml_buku = ref(0)

async function getjml_pengunjung() {
  const{ error , data, count } = await supabase
  .from("Pengunjung")
  .select('*', { count: 'exact' })
  if (count) jml_pengunjung.value = count
  
}
async function getjml_buku() {
  const{ error , data, count } = await supabase
  .from("Buku")
  .select('*', { count: 'exact' })
  if (count) jml_buku.value = count
  
}


onMounted(() => {
  getjml_pengunjung()
  getjml_buku()
})
</script>

<style scoped>
.card {
    height: 250px;
    box-shadow: 1px 1px 10px #424242;
}
.card.bg-pengunjung {
    background-image: url('../assets/img/Picture1.png');
    background-repeat: no-repeat;
    background-position: center center;
    background-size: cover;
}
.card.bg-buku {
    background: url('../assets/img/Picture2.png') no-repeat center center;
    background-repeat: no-repeat;
    background-position: center center;
    background-size: cover;
}
.raccing {
  height: 200px;
  box-shadow: 1px 1px 10px;
  border-radius: 20px;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color:#F5C9E4;
}
.raccing1 {
  height: 200px;
  box-shadow: 1px 1px 10px;
  border-radius: 20px;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #C0F2EC;
}
.card-body h2{
    color: black;
}
.box {
  width: 50%;
}
.box a{
  text-decoration: none;
}
h5{
  padding-top: 10px;
}
.card-body h2{
    color: black;
}

</style>