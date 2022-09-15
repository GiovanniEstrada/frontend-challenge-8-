<script setup lang="ts">
    import { ref } from 'vue'
    const data = ref(["7", "8", "9", "DEL", "4", "5", "6", "+", "1", "2", "3", "-", ".", "0", "/", "*"]).value
    var operation = ref()


    function print(info: any) {

        if(info == "DEL"){
            operation.value = operation.value.slice(0, -1)
        } else if(operation.value == undefined) {
            operation.value = info
        } else {
            operation.value += info
            console.log();
        }
    }

    const clear = () => operation.value = ""
    const operate = () => operation.value = eval(operation.value).toString()

    defineProps<{
        scheme:string
    }>()

    const classCalc = (data:string) =>{
        if(data == "dark"){
            return "calc dark"
        } else if(data == "light") {
            return "calc light"
        } else {
            return "calc purple"
        }
        }
</script>

<template>
    <div :class="classCalc(scheme)">
        <div class="screen" >
            <h1 class="print">{{operation}}</h1>
        </div>
        <div class="numpad">
            <div v-for="icon in data">
                <div class="btn" @click="print(icon)" :id="icon">{{icon}}</div>
            </div>
            <div class="reset" @click="clear">RESET</div>
            <div class="result" @click="operate">=</div>
        </div>
    </div>
</template>

<style>
    @import url('https://fonts.googleapis.com/css2?family=League+Spartan:wght@700&display=swap');
    
    *{
        font-family: 'League Spartan', sans-serif;
        font-weight: 700;
        transition: all 400ms;
        color: #fff;
    }

    .calc {
        max-width: 540px;
        max-height: 650px;
        width: 100%;
        height: 100%;
        display: flex;
        flex-direction: column;
        justify-content: space-between;
    }

    .screen {
        width: 100%;
        height: 130px;
        border-radius: 15px;
        padding: 15px;
        display: flex;
        justify-content: flex-end;
        align-items: center;
    }

    .print {
        font-size: 47px;
    }

    .numpad {
        width: 100%;
        height: 485px;
        border-radius: 15px;
        display: flex;
        flex-wrap: wrap;
        justify-content: space-around;
        align-items: center;
        gap: 10px;
        padding: 10px;

    }
    
    .btn {
        width: 100px;
        height: 60px;
        border-radius: 8px;
        display: flex;
        justify-content: center;
        align-items: center;
        font-size: 32px;
        cursor: pointer;
    }

    .reset, .result {
        width: 230px;
        height: 60px;
        background-color: rgb(234, 227, 219);
        border-radius: 8px;
        display: flex;
        justify-content: center;
        align-items: center;
        font-size: 32px;
        cursor: pointer;
        box-shadow: 0px 4px 0px 0px rgb(182, 164, 154);
        -webkit-box-shadow: 0px 4px 0px 0px rgb(182, 164, 154);
        -moz-box-shadow: 0px 4px 0px 0px rgb(182, 164, 154);
    }

    /* ----------------- Dark Mode ---------------------- */

    .calc.dark .screen {
        background-color: rgb(24,31,50);
    }

    .calc.dark .print {
        color: #fff;
    }

    .calc.dark .numpad {
        background-color: rgb(37, 45, 68);
    }

    .calc.dark .btn,
    .calc.dark .reset,
    .calc.dark .result {
        background-color: rgb(234, 227, 219);
        color: rgb(69, 78, 95);
        box-shadow: 0px 4px 0px 0px rgb(182, 164, 154);
        -webkit-box-shadow: 0px 4px 0px 0px rgb(182, 164, 154);
        -moz-box-shadow: 0px 4px 0px 0px rgb(182, 164, 154);
    }

    .calc.dark .btn:hover {
        background-color: #fff;
    }


    .calc.dark .reset:hover,
    .calc.dark #DEL:hover {
        background-color: rgb(162, 179, 225);
        color: #fff;
        box-shadow: 0px 4px 0px 0px rgb(65, 78, 113);
        -webkit-box-shadow: 0px 4px 0px 0px rgb(65, 78, 113);
        -moz-box-shadow: 0px 4px 0px 0px rgb(65, 78, 113);
    }

    .calc.dark .result:hover{
        background-color: rgb(249, 108, 91) ;
        color: #fff;
        box-shadow: 0px 4px 0px 0px rgb(150, 39, 28);
        -webkit-box-shadow: 0px 4px 0px 0px rgb(150, 39, 28);
        -moz-box-shadow: 0px 4px 0px 0px rgb(150, 39, 28);
    }

    /* ----------------- Light Mode ---------------------- */

    .calc.light .screen {
        background-color: rgb(238, 238, 238);
    }

    .calc.light .print {
        color: #000;
    }

    .calc.light .numpad {
        background-color: rgb(211, 205, 205);
    }

    .calc.light .btn,
    .calc.light .reset,
    .calc.light .result {
        background-color: rgb(229, 228, 224);
        color: rgb(0,0,0);
        box-shadow: 0px 4px 0px 0px rgb(168, 159, 150);
        -webkit-box-shadow: 0px 4px 0px 0px rgb(168, 159, 150);
        -moz-box-shadow: 0px 4px 0px 0px rgb(168, 159, 150);
    }

    .calc.light .btn:hover {
        background-color: #fff;
    }


    .calc.light .reset:hover,
    .calc.light #DEL:hover {
        background-color: rgb(97, 182, 187);
        color: #fff;
        box-shadow: 0px 4px 0px 0px rgb(39, 88, 95);
        -webkit-box-shadow: 0px 4px 0px 0px rgb(39, 88, 95);
        -moz-box-shadow: 0px 4px 0px 0px rgb(39, 88, 95);
    }

    .calc.light .result:hover{
        background-color: rgb(255, 139, 56) ;
        color: #fff;
        box-shadow: 0px 4px 0px 0px rgb(121, 60, 16);
        -webkit-box-shadow: 0px 4px 0px 0px rgb(121, 60, 16);
        -moz-box-shadow: 0px 4px 0px 0px rgb(121, 60, 16);
    }

    /* ----------------- Purple Mode ---------------------- */

    .calc.purple .screen {
        background-color: rgb(30, 8, 54);
    }

    .calc.purple .print {
        color: rgb(255, 226, 58);
    }

    .calc.purple .numpad {
        background-color: rgb(30, 8, 54);
    }

    .calc.purple .btn,
    .calc.purple .reset,
    .calc.purple .result {
        background-color: rgb(51, 27, 77);
        color: rgb(255, 226, 58);
        box-shadow: 0px 4px 0px 0px rgb(121, 35, 144);
        -webkit-box-shadow: 0px 4px 0px 0px rgb(121, 35, 144);
        -moz-box-shadow: 0px 4px 0px 0px rgb(121, 35, 144);
    }

    .calc.purple .btn:hover {
        background-color: rgb(107, 52, 172);
    }


    .calc.purple .reset:hover,
    .calc.purple #DEL:hover {
        background-color: rgb(134, 49, 176);
        color: #fff;
        box-shadow: 0px 4px 0px 0px rgb(169, 36, 215);
        -webkit-box-shadow: 0px 4px 0px 0px rgb(169, 36, 215);
        -moz-box-shadow: 0px 4px 0px 0px rgb(169, 36, 215);
    }

    .calc.purple .result:hover{
        background-color: rgb(148, 255, 249) ;
        color: #000;
        box-shadow: 0px 4px 0px 0px rgb(136, 235, 240);
        -webkit-box-shadow: 0px 4px 0px 0px rgb(136, 235, 240);
        -moz-box-shadow: 0px 4px 0px 0px rgb(136, 235, 240);
    }

    @media screen and (max-width: 550px) {

        .calc {
            width: 90%;
        }

        .btn {
            width: 60px;
        }

        .result, .reset {
            width: 140px;
        }

        .screen {
            height: 90px;
        }
    }

</style>
