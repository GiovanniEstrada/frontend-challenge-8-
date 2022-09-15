<script setup lang="ts">
    import Calculator from "../components/Calculator.vue"
    import {ref} from 'vue'
import { computed } from "@vue/reactivity";

        
    let scheme = ref("")
    let defaultTheme = window.matchMedia("(prefers-color-scheme: dark)").matches
    
    if(defaultTheme) {
        scheme.value = "dark"
    } else {
        scheme.value = "light"
    }
    
    const darkMode =  () => {
        let btn = document.querySelectorAll(".select")
        btn[0].classList.add("active")
        btn[1].classList.remove("active")
        btn[2].classList.remove("active")
        scheme.value = "dark"
    }

    const lightMode = () => {
        const btn = document.querySelectorAll(".select")
        btn[0].classList.remove("active")
        btn[1].classList.add("active")
        btn[2].classList.remove("active")
        scheme.value = "light"
    }

    const purpleMode = () => {
        const btn = document.querySelectorAll(".select")
        btn[0].classList.remove("active")
        btn[1].classList.remove("active")
        btn[2].classList.add("active")
        scheme.value = "purple"
    }


    const classMode = computed(()=>{
        if(scheme.value == "dark"){
            scheme.value="dark"
            return "container dark"
        } else if(scheme.value == "light") {
            scheme.value = "light"
            return "container light"
        } else {
            scheme.value = "purple"
            return "container purple"
        }
    })

</script>

<template>
    <div :class="classMode">
        <header>
            <h1 class="title">calc</h1>
            <div class="change">
                <p class="subtitle">THEME</p>
                <div class="switch">
                    <div class="numbers">
                        <p class="number">1</p>
                        <p class="number">2</p>
                        <p class="number">3</p>
                    </div>
                    <div class="selection">
                        <div @click="darkMode" class="select"></div>
                        <div @click="lightMode" class="select"></div>
                        <div @click="purpleMode" class="select"></div>
                    </div>
                </div>
            </div>
        </header>
        <Calculator :scheme = "scheme"/>
    </div>
</template>



<style>
    * {
  padding: 0;
  margin: 0;
}

    .container {
        height: 100vh;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
      }

      header {
        display: flex;
        justify-content: space-between;
        width: 540px;
        margin-bottom: 10px;
      }

      .change {
        display: flex;
        width: 150px;
        height: 50px;
        justify-content: space-between;
        align-items: center;
      }

      .numbers {
        display: flex;
        justify-content: space-around;
      }

      .switch {
        display: flex;
        flex-direction: column;
        width: 70px;
        height: 50px;
      }

      .selection {
        display: grid;
        grid-template-columns: repeat(3, 1fr);
        justify-items: center;
        align-items: center;
        width: 70px;
        height: 30px;
        border-radius: 20px;
      }

      .select {
        width: 20px;
        height: 20px;
        border-radius: 50%;
        cursor: pointer;
      }

      .container .select:first-child.active{
          background-color: rgb(248, 108, 93);
      }

      .container .select:nth-child(2).active{
          background-color: rgb(255, 137, 50);
      }

      .container .select:nth-child(3).active{
          background-color: rgb(143, 254, 245);
      }

      /* ----------------- Dark Mode ---------------------- */

        .container.dark {
            background-color: rgb(59, 70, 100);
        }

        .container.dark .selection {
            background-color: rgb(37, 45, 68);
        }

        .container.dark .title,
        .container.dark .subtitle,
        .container.dark .number {
            color: #fff;
        }


        /* ----------------- Light Mode ---------------------- */

        .container.light {
            background-color: rgb(230, 230, 230);
        }

        .container.light .selection {
            background-color: rgb(213, 204, 205);
        }

        .container.light .title,
        .container.light .subtitle,
        .container.light .number {
            color: #000;
        }

        /* ----------------- Purple Mode ---------------------- */

        .container.purple {
            background-color: rgb(23, 6, 42);
        }

        .container.container.purple .selection {
            background-color: rgb(30, 8, 54);
        }

        .container.purple .title,
        .container.purple .subtitle,
        .container.purple .number {
            color: rgb(255, 228, 63);
        }

        @media screen and (max-width: 550px) {
            header {
                width: 90%;
                margin: 15px 0;
            }
        }

</style>