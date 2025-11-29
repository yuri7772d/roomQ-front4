<template>
    <div>
        <div>
            <input type="text" placeholder="ชื่อผู้ใช้" v-model="input.username"
                class=" p-3 border mb-4 rounded-md focus:ring-2 focus:ring-blue-500">
            <input type="text" placeholder="รหัสผ่าน" v-model="input.password"
                class=" p-3 border mb-6 rounded-md focus:ring-2 focus:ring-blue-500">
                     <input type="number" placeholder="role" v-model="input.role"
                class=" p-3 border mb-6 rounded-md focus:ring-2 focus:ring-blue-500">
            <button @click="onAdd()"
                class=" bg-blue-500 text-white py-3 rounded-md hover:bg-blue-600 focus:ring-2 focus:ring-blue-500">
                ตกลง
            </button>
            {{ input }}
        </div>
   <div> 
     <ul>
        <li><P></P></li>
     </ul>

   </div>
    </div>
</template>
<script setup>
definePageMeta({middleware:'role'})

const input = ref({username:'',password:'',role:null});
const config = useRuntimeConfig();
const fetch = useRequestFetch();
async function onAdd(){

    try {
      await fetch(`${config.public.api}/auth`, {
        method: "POST",
        body: {
          username: input.value.username,
          password: input.value.password,
          role: input.value.role
        },
        credentials: "include",
      });

    } catch (err) {
        console.log(err?.data)
      alert("add failed: ",err?.data?.msg);
    }
   
}



</script>