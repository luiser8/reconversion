<template>
  <section class="text-gray-600 body-font relative">
    <div class="container px-5 py-16 mx-auto">
      <div class="lg:w-1/3 md:w-3/3 sm:w-2/3 mx-auto">
        <div class="flex flex-wrap -m-2 bg-gray-50 p-0 sm:p2 xs:p-2 rounded">
          <div class="flex flex-col text-center w-full mb-6">
            <h1
              class="sm:text-3xl text-2xl font-medium title-font text-gray-900"
            >
              Calculadora reconversión monetaria {{ year }}
            </h1>
          </div>
          <div class="p-2 w-full">
            <div class="relative">
              <label
                for="bsf"
                class="leading-7 text-lg text-gray-800 font-medium"
                >Bolivar Fuerte</label
              >
              <div class="mt-1 flex rounded-md shadow-sm">
                <span
                  class="
                    text-2xl
                    font-medium
                    inline-flex
                    items-center
                    text-bold
                    px-3
                    rounded-l-md
                    border border-r-0 border-gray-300
                    bg-gray-200
                  "
                  >BsF:</span
                >
                <input
                  @keyup="convert()"
                  type="text"
                  id="bsf"
                  autofocus
                  name="bsf"
                  v-model="bsF"
                  placeholder="0"
                  class="
                    text-3xl
                    w-full
                    bg-white-200 bg-opacity-50
                    rounded
                    border border-gray-300
                    focus:border-indigo-500
                    focus:bg-white
                    focus:ring-2 focus:ring-indigo-200
                    text-base
                    outline-none
                    text-gray-700
                    py-1
                    px-3
                    leading-8
                    transition-colors
                    duration-200
                    ease-in-out
                  "
                />
              </div>
            </div>
          </div>
          <div class="p-2 w-full">
            <div class="relative">
              <label
                for="bss"
                class="leading-7 text-lg text-gray-800 font-medium"
                >Bolivar Digital</label
              >
              <div class="mt-1 flex rounded-md shadow-sm">
                <span
                  class="
                    text-2xl
                    font-medium
                    inline-flex
                    items-center
                    text-bold
                    px-3
                    rounded-l-md
                    border border-r-0 border-gray-300
                    bg-gray-200
                  "
                  >BsD:</span
                >
                <input
                  type="text"
                  id="bsd"
                  name="bsd"
                  readonly
                  v-model="bsD"
                  class="
                    text-3xl
                    w-full
                    font-bold
                    bg-gray-200 bg-opacity-50
                    rounded
                    border border-gray-300
                    focus:border-indigo-500
                    focus:bg-white
                    focus:ring-2 focus:ring-indigo-200
                    text-base
                    outline-none
                    text-gray-700
                    py-1
                    px-3
                    leading-8
                    transition-colors
                    duration-200
                    ease-in-out
                  "
                />
              </div>
            </div>
          </div>
				<div class="p-2 flex flex-wrap content-evenly space-x-2" v-for="(item, index) in cono" :key="index">
					<button @click="convertCono(item)" class="text-black hover:text-white font-semibold bg-gray-300 border-0 py-1 px-1 focus:outline-none rounded hover:bg-gray-600 text-lg">{{item.bsd}}</button>
				</div>

          <div class="p-2 w-full">
            <button
              @click="convert()"
              class="
                flex
                mx-auto
                text-white
                bg-gray-500
                border-0
                pt-1
				        pb-2
                px-8
                focus:outline-none
                hover:bg-gray-600
                rounded
                text-lg
                w-full
              "
            >
              <span class="text-center-custom font-semibold text-2xl"
                >Convertir</span
              >
            </button>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import json from "../assets/cono.json";
export default {
  name: "Reconversion",
  props: {
    msg: String,
  },
  data() {
    return {
      cono: json,
      year: new Date().getFullYear(),
      bsF: "",
      bsD: "0",
    };
  },
  methods: {
	convertCono(item){
		this.bsF = item.bsf;
		this.bsD = item.bsd;
	},
    convert() {
      var bsf1 = this.bsF.replace(/\./g, "");
      var bsf2 = bsf1.replace(/,/g, ".");
      var bsd = bsf2 / 1000000;
      var bsd1 = bsd.toString();
      var bsd2 = bsd1.replace(/\./g, ",");
      this.bsD = this.numberFormat(bsd2);
      this.bsD = Number.parseFloat(bsd);
    },
    numberFormat(numero) {
      var resultado = "";
      var nuevoNumero = numero.replace(/\./g, "");
      if (numero.indexOf(",") >= 0)
        nuevoNumero = nuevoNumero.substring(0, nuevoNumero.indexOf(","));
      for (var j, i = nuevoNumero.length - 1; i >= 0; i--, j++) {
        resultado =
          nuevoNumero.charAt(i) + (j > 0 && j % 3 == 0 ? "." : "") + resultado;
      }
      if (numero.indexOf(",") >= 0) {
        resultado += numero.substring(numero.indexOf(","));
      }
      return resultado; 
    },
  },
};
</script>
<style scoped>
.text-center-custom {
  margin: 0 auto !important;
}
</style>