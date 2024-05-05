<template>
  <div class="min-h-screen flex justify-center items-center p-20">
    <div class="flex flex-col gap-10">
      <div class="flex justify-center">
        <div class="flex flex-col">
          <input type="" name="" class="border border-black" v-model="input" />
          <small>Example: rizky,rizky@cipoho.com,30 juli,cipoho,laki laki</small>
        </div>
        <!-- <button class="bg-blue-500 text-white mx-3 px-3" @click="add">set</button> -->
        <button
          class="bg-blue-500 text-white mx-3 px-3"
          @click="mode == 'add' ? (mode = 'search') : (mode = 'add')"
        >
          {{ mode == 'add' ? 'change search' : 'change add' }}
        </button>
        <!-- <button class="bg-blue-500 text-white mx-3 px-3" @click="destroyy">delete</button> -->
      </div>
      <TableAddMode :datas="datas" v-if="mode == 'add'" />
      <TableSearchMode :datas="search" v-if="mode == 'search'" />
    </div>
    <!-- {{ search }} -->
  </div>
</template>
<script type="text/javascript" setup>
import { ref, computed, watch } from 'vue'
import TableAddMode from '../components/tableAddMode.vue'
import TableSearchMode from '../components/tableSearchMode.vue'
let mode = ref('add')
let datas = ref($cookies.isKey('datas') ? [...$cookies.get('datas')] : [])
let input = ref('')

if (!$cookies.isKey('datas')) {
  $cookies.set('datas', [
    {
      name: 'Rizky',
      email: 'Rizky@gmail.com',
      ttl: '30 juli',
      alamat: 'cipoho',
      jk: 'laki-laki'
    },
    {
      name: 'rizal',
      email: 'rizal@gmail.com',
      ttl: '30 agustus',
      alamat: 'balandongan',
      jk: 'laki-laki'
    },
    {
      name: 'akbar',
      email: 'akbar@gmail.com',
      ttl: '30 juni',
      alamat: 'jakarta',
      jk: 'laki-laki'
    }
  ])
}

function add() {
  datas.value.push(input.value)
  $cookies.set('datas', [...datas.value])
}
function edit(index) {
  datas.value[index] = input.value
  $cookies.set('datas', [...datas.value])
}
function destroy(index) {
  datas.value.splice(index, 1)
  $cookies.set('datas', [...datas.value])
}
function destroyy(index) {
  datas.value.splice(index, 1)
  $cookies.remove('datas')
}
const search = computed(() => {
  const dataResult = []
  if (input.value != '' && mode.value == 'search') {
    datas.value.forEach((val) => {
      Object.keys(val).forEach((objectName) => {
        console.log(val[objectName] == input.value)
        if (val[objectName] == input.value) {
          dataResult.includes(val) == false ? dataResult.push(val) : ''
        }
      })
    })
  } else {
    return datas.value
  }
  return dataResult
})

// if (val[valName] == input.value) {
//         dataResult.forEach((valDuplicate) => {
//           valDuplicate.id.includes(val.id) == false
//           dataResult.push(val)
//         })
//       }
</script>
