<template>
    <div class="container-fluid">
        <div class="row">
            <div class="col-lg-12">
                <h2 class="text-center my-4">RIWAYAT KUNJUNGAN</h2>
                <div class="my-3">
                    <form @submit.prevent="getPengunjung">
                        <input v-model="keyword" type="search" class="form-control rounded-5 btn-dark btn-lg " placeholder="Fiter">
                    </form>
                </div>
                <div class="my-3 text-muted">menampilkan daftar riwayat kunjungan </div>
                <table class="table table-bordered">
                    <thead>
                        <tr>
                            <td>#</td>
                            <td>NAMA</td>
                            <td>KEANGGOTAAN</td>
                            <td>WAKTU</td>
                            <td>KEPERLUAN</td>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="(visitor,i) in visitors" :key="i">
                            <td>{{ i+1 }}.</td>
                            <td>{{ visitor.nama }}</td>
                            <td>{{ visitor.keanggotaan.nama }}</td>
                            <td>{{ visitor.tanggal }}, {{ visitor.waktu }}</td>
                            <td>{{ visitor.keperluan.nama }}</td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>
        <NuxtLink to="/pengunjung/tambah">
            <button type="submit" class="btn btn-dark btn-lg rounded-5 px-5">kembali</button>
        </NuxtLink>
    </div>
</template>
<script setup>
import { compileTemplate } from 'vue/compiler-sfc';

const supabase = useSupabaseClient()
const keyword = ref('')
const visitors = ref([])

const getPengunjung = async () => {
    const { data, error } = await supabase.from('Pengunjung').select(`*, keanggotaan(*), keperluan(*)`)
    .ilike('nama', `%${keyword.value}%`)
    if(error) throw error
    if(data) visitors.value = data
}
onMounted(() => {
    getPengunjung()
})
</script>
<style scoped>
.btn{
    background-color: #DFF2F6;
    color: black;
}
.form-control{
    background-color: #DFF2F6;
}
</style>                                                                                        