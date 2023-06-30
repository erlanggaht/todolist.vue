<script setup>
import { computed, onMounted, onUpdated, reactive, ref, watch } from 'vue';


// Props
defineProps(['title'])


// Ref
let namas = ref([])
let input = ref('')
let modalShow = ref(false)
let categories = ref('Anythink')

console.log(namas)

// Method
function TambahData() {
    namas.value.push(input.value)
    input.value = ''
}

function HapusData(index) {
    namas.value.splice(index, 1)
}

function ModalShow() {
    modalShow.value = !modalShow.value || false
}

function SaveData(categories) {
    const toJsonData = JSON.stringify(namas._rawValue)
    localStorage.setItem(categories, toJsonData)
}




// Computed
const lenghtList = computed(() => {
    return namas.value.length
})
const categorie_select = computed(() => {
    return function (param) {
        const getSaveData = JSON.parse(localStorage.getItem(param))
        categories.value = param
        namas.value = getSaveData
        ModalShow()
    }
})

// LifeSycle

onMounted(() => {
    const getSaveData = JSON.parse(localStorage.getItem('Anythink'))
    const setIfLocal = !localStorage.getItem('Anythink') || !localStorage.getItem('Favorite Animal') || !localStorage.getItem('Favorite Food') || !localStorage.getItem('Favorite Movie')
    
    if(setIfLocal)
    {
        localStorage.setItem('Anythink', JSON.stringify([]))
        localStorage.setItem('Favorite Animal', JSON.stringify([]))
        localStorage.setItem('Favorite Food', JSON.stringify([]))
        localStorage.setItem('Favorite Movie', JSON.stringify([]))

    }   else{
        namas.value = getSaveData
    }
  
})






</script>


<template>
    <h1 class="title">{{ title }}</h1>

    <form class="form" @submit.prevent="TambahData()">
       
        <div style="display: flex;justify-content:space-between;padding:2rem">
            <p class="not_data" v-if="namas.length === 0">no assignment yet</p> 
            <div class="btn_abs" v-if="namas.length <= 0">
                <button type="button" class="buttonSave_abs" @click="SaveData(categories)">Save</button>
            </div>
        </div>

        <p style="text-align: left;padding:0rem 1rem;font-size:1.2rem;font-weight:400" v-if="namas.length > 0"> <span style="font-weight:700">{{categories}}</span> - Sum
            List: {{ lenghtList }}</p>
        <ul class="ul" :style="!namas.length > 0 && 'display:inline'">
            <li class="list" v-for="(nama, index) in namas">
                <div style="display: flex;align-items:center;gap:10px;text-transform:capitalize"> <span class="square_list"></span> {{ nama }}</div>
                <button type="button" class="deletebutton" @click="HapusData(index)"><img src="../assets/delete.svg"
                        alt="deletebutton" style="width: 28px;height:28px;" /></button>
            </li>
        </ul>
        <div v-if="namas.length > 0" style="display:flex;justify-content:flex-end;margin:2rem 1rem 3rem 0">
            <button type="button" class="buttonSave" @click="SaveData(categories)">Save</button>
        </div>

        <section class="area-input-submit">
            <input class="input" maxlength='30' placeholder="Write a new task" v-model="input" />
            <button type="button" class="btn_anythink" @click="ModalShow">{{ categories }}  </button>
            <button type="button" class="buttonSubmit" @click="ModalShow"><img src="../assets/menu.svg" alt='menu'
                    style="width:35px;height35px;" /></button>
        </section>
        <section :class="modalShow ? 'modalshow' : 'modalshow_hidden'">
            <div :class="modalShow ? 'modalshow_ul' : 'modalshow_hidden'">
                <li style="list" @click="categorie_select('Favorite Animal')">Favorite Animal</li>
                <li style="list" @click="categorie_select('Favorite Food')">Favorite Food</li>
                <li style="list" @click="categorie_select('Favorite Movie')">Favorite Movie</li>
                <li style="list" @click="categorie_select('Anythink')">Anything</li>
            </div>
        </section>
    </form>
</template>


<style scoped>
.title {
    font-size: 3rem;
    font-weight: 700;
    text-transform: uppercase;
    text-align: center;
    margin: 0px;
    padding: 2rem 0 0 0;
}

.btn_abs {
    display: flex;
    justify-content: center;
    margin: 0;
}

.buttonSave_abs {
    border: none;
    border-radius: 29px 29px 29px 29px;
    padding: 1rem 1.3rem;
    font-weight: 700;
    outline: none;
    background-color: #fff;
    margin: .6rem .6rem 0 0;
    color: #58595a;
    font-size: 1.1rem;
    display: flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;
    font-family: 'Roboto Condensed', sans-serif;

}


.not_data {
    padding: 1rem 0 0 0;
    text-align: center;
    font-size: 1rem;
    font-style: italic;
    font-family: 'Roboto Condensed', sans-serif;


}

.form {
    margin: 0 0 0 0;
    padding: 0;
    position: relative;
}

.square_list {
    width: 1.3rem;
    height: 1.3rem;
    border-radius: .4rem;
    display: block;
    background-color: #e9ecee;

}
.ul {
    margin:0px;padding: .5rem 1rem .2rem 1rem;
    max-height:360px ;
    overflow: auto;
    scroll-padding-top: 20px;
}
.list {
    text-transform: capitalize;
    background-color: #fffeff;
    padding: 1.1rem 1.1rem;
    display: flex;
    justify-content: space-between;
    border-radius: 1.2rem;
    font-weight: 400;
    font-size: 22px;
    color: #58595a;
    margin: .6rem 0;
    font-family: 'Roboto Condensed', sans-serif;

}

.buttonSave {
    border: none;
    border-radius: 16px;
    padding: 1rem 1.3rem;
    font-weight: 700;
    outline: none;
    background-color: #fff;
    margin: .6rem .6rem 0 0;
    color: #58595a;
    font-size: 1.1rem;
    display: flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;
    font-family: 'Roboto Condensed', sans-serif;

}


.deletebutton {
    background-color: transparent;
    border: none;
    outline: none;
}




.input {
    border: none;
    border-radius: 2rem;
    padding: 1.5rem 1.5rem;
    width: 60%;
    font-size: 1rem;
    position: relative;
}



.input:active {
    background-color: #eee;
}

.buttonSubmit {
    border: none;
    border-radius: 100%;
    padding: 0rem 1rem;
    outline: none;
    margin: 0 12px;
    background-color: #fff;
    color: #757575;
    font-size: 1rem;
    display: flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;
}

.area-input-submit {
    text-align: center;
    margin: 1rem;
    display: flex;
    justify-content: center;
    position: relative;

}

.buttonSubmit:active,
.buttonSave_abs:active {
    background-color: #ddd;
}


.buttonSubmit:disabled {
    background-color: #e7e7e7;
    cursor: not-allowed;
    color: #999
}

.btn_anythink {
    position: absolute;
    right: 170px;
    bottom: 10px;
    border: none;
    outline: none;
    background-color: #eee;
    padding: 1rem;
    border-radius: 1rem;
    color: #757575;
}

.btn_anythink:active {
    background-color: #ddd;
}



.modalshow {
    background-color: #fff;
    border-radius: 0 0 3rem 3rem;
    margin: 3rem 0 0 0;
    box-shadow: -7px -18px 19px -11px rgba(129, 129, 129, 0.1);
    transition: all .6s;

}

.modalshow_hidden {
    margin: 0px 100px;
    transition: all .5s;
    font-size: 0;
}

.modalshow_ul {
    margin: 0px;
    list-style: none;
}



.modalshow_ul li {
    padding: 2rem 3rem;
    margin: 0rem 0rem;
    font-size: 1.2rem;
    font-weight: 700;
    display: flex;
    align-items: center;
    gap: 1.3rem;
    color: #666;
    font-family: 'Roboto Condensed', sans-serif;
}



.modalshow_ul li:before {
    content: '';
    display: inline-block;
    width: 10px;
    height: 10px;
    border-radius: 7px;
    background-color: transparent;
    border: 3px solid #4caf50;
}

.modalshow_ul li:nth-child(2):before {
    background-color: transparent;
    border: 3px solid #6a4fed;
}

.modalshow_ul li:nth-child(3):before {
    background-color: transparent;
    border: 3px solid #cb2c31;
}

.modalshow_ul li:last-child:before {
    background-color: transparent;
    border: 3px solid gray;
}

.modalshow_ul li:hover {
    background-color: #eee;
 
}

.modalshow_ul li:last-child:hover {
    border-radius: 0 0 3rem 3rem;
}

.modalshow_ul li:active {
    background-color: #ddd;
}</style>