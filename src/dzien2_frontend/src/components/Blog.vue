<template>
    <div>
        <h1>Witaj na blogu! :D</h1>
        <h2 class="text-blue-600">Aktualne wpisy: </h2>
        <div class="w-100 flex flex-row-reverse">
            <button @click="pobierzWpisy" class="float-right bg-blue-600 rounded text-white p-4">Odswiez bloga</button>
        </div>
        <div class="grid mx-6 gap-4 my-4" >
            <div v-for="(wpis, index) in wpisy" class="drop-shadow-xl bg-stone-300 p-4">
            <p> {{ index }} - {{ wpis }}</p>
            <button @click="deleteWpis(index)" class="float-right bg-blue-600 rounded text-white p-4">usuń wpis</button>
        </div>
        </div>
        <br>
        <div class="flex flex-cal justify-center">
            <input v-model="nowyBlog" class="border border-blue-600 p-3" type="text" placeholder="Wpisz nowy wpis do bloga!">
            <button @click="dodajWpisy" class="float-right bg-blue-600 rounded text-white p-4">Dodaj nowy wpis</button>
        </div>
        <br>
        
    </div>
</template>

<script>

import { dzien2_backend } from 'declarations/dzien2_backend/index';
    export default {
        data() {
            return {
                wpisy: [],
                nowyBlog: ""
            }
        },
        methods: {
            async dodajWpisy(){
                await dzien2_backend.dodaj_wpis(this.nowyBlog);
                await this.pobierzWpisy()
            },
            async deleteWpis(index){
                await dzien2_backend.usun_wpis(index)
                await this.pobierzWpisy()
            },
            async pobierzWpisy() {
                this.wpisy = await dzien2_backend.odczytaj_wpisy()
            }
        },
        async mounted(){
            this.pobierzWpisy()
        }
    }
</script>