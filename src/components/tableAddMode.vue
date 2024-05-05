<template>
  <table class="border-collapse border border-slate-400">
    <thead>
      <tr>
        <th class="border border-slate-400">Nama</th>
        <th class="border border-slate-400">Email</th>
        <th class="border border-slate-400">TTL</th>
        <th class="border border-slate-400">Alamat</th>
        <th class="border border-slate-400">Kelamin</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(i, index) in datas.datas" :key="index">
        <td class="border border-slate-400">{{ i.name }}</td>
        <td class="border border-slate-400">{{ i.email }}</td>
        <td class="border border-slate-400">{{ i.ttl }}</td>
        <td class="border border-slate-400">{{ i.alamat }}</td>
        <td class="border border-slate-400">{{ i.jk }}</td>
        <td class="border border-slate-400 cursor-pointer px-5" @click="destroy(index)">Hapus</td>
        <td class="border border-slate-400 cursor-pointer px-5" @click="edit(index)">Edit</td>
      </tr>
    </tbody>
  </table>
  <pre>{{ datas.datas }}</pre>
</template>
<script setup>
const datas = defineProps({
  datas: 'Object'
})
</script>
