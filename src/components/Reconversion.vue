<template>
  <section class="text-gray-600 body-font relative">
    <div class="container px-5 py-16 mx-auto">
      <div class="lg:w-1/3 md:w-3/3 sm:w-2/3 mx-auto">
        <div class="flex flex-wrap -m-2 bg-gray-50 p-6 rounded">
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
                  placeholder="0,00"
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
                >Bolivar Soberano</label
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
                  >BsS:</span
                >
                <input
                  type="text"
                  id="bss"
                  name="bss"
                  readonly
                  v-model="bsS"
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
					<button @click="convertCono(item)" class="text-black font-semibold bg-gray-300 border-0 py-1 px-1 focus:outline-none rounded hover:bg-gray-600 text-lg">{{item.bss}}</button>
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
      bsS: "0,00",
    };
  },
  methods: {
	convertCono(item){
		this.bsF = item.bsf;
		this.bsS = item.bss;
	},
    convert() {
      var bsf1 = this.bsF.replace(/\./g, "");
      var bsf2 = bsf1.replace(/,/g, ".");
      var bss = this.roundDecimal(bsf2 / 100000);
      var bss1 = bss.toString();
      var bss2 = bss1.replace(/\./g, ",");
      this.bsS = this.numberFormat(bss2);
    },
    roundDecimal(numero) {
      var original = parseFloat(numero);
      var prueba = original.toString().split(".");
      var bol_s = 0;
      var len = prueba.length;
      var dec_final = "";

      if (len == 2) {
        var prueba1 = prueba[1];
        var decimales = "";
        var len1 = prueba[1].length;
      }

      if (len1 >= 3) {
        for (var i = 0; i < 2; i++) {
          if (i != 2) decimales += prueba1.charAt(i);
          if (i == 2)
            if ((prueba1[2] != 0) & (prueba1[2] != "")) {
              dec_final = this.obtenerdecimales(decimales);
            }
          bol_s = prueba[0] + "." + dec_final;
        }
      } else {
        bol_s = original;
      }

      var result = Math.round(parseFloat(bol_s) * 100) / 100;
      result = result.toFixed(2);
      return result;
    },
    obtenerdecimales(decimales) {
      if (decimales == "98") {
        decimales = "99";
      }
      if (decimales == "97") {
        decimales = "98";
      }
      if (decimales == "96") {
        decimales = "97";
      }
      if (decimales == "95") {
        decimales = "96";
      }
      if (decimales == "94") {
        decimales = "95";
      }
      if (decimales == "93") {
        decimales = "94";
      }
      if (decimales == "92") {
        decimales = "93";
      }
      if (decimales == "91") {
        decimales = "92";
      }
      if (decimales == "90") {
        decimales = "91";
      }
      if (decimales == "89") {
        decimales = "90";
      }
      if (decimales == "88") {
        decimales = "89";
      }
      if (decimales == "87") {
        decimales = "88";
      }
      if (decimales == "86") {
        decimales = "87";
      }
      if (decimales == "85") {
        decimales = "86";
      }
      if (decimales == "84") {
        decimales = "85";
      }
      if (decimales == "83") {
        decimales = "84";
      }
      if (decimales == "82") {
        decimales = "83";
      }
      if (decimales == "81") {
        decimales = "82";
      }
      if (decimales == "80") {
        decimales = "81";
      }
      if (decimales == "79") {
        decimales = "80";
      }
      if (decimales == "78") {
        decimales = "79";
      }
      if (decimales == "77") {
        decimales = "78";
      }
      if (decimales == "76") {
        decimales = "77";
      }
      if (decimales == "75") {
        decimales = "76";
      }
      if (decimales == "74") {
        decimales = "75";
      }
      if (decimales == "73") {
        decimales = "74";
      }
      if (decimales == "72") {
        decimales = "73";
      }
      if (decimales == "71") {
        decimales = "72";
      }
      if (decimales == "70") {
        decimales = "71";
      }
      if (decimales == "69") {
        decimales = "70";
      }
      if (decimales == "68") {
        decimales = "69";
      }
      if (decimales == "67") {
        decimales = "68";
      }
      if (decimales == "66") {
        decimales = "67";
      }
      if (decimales == "65") {
        decimales = "66";
      }
      if (decimales == "64") {
        decimales = "65";
      }
      if (decimales == "63") {
        decimales = "64";
      }
      if (decimales == "62") {
        decimales = "63";
      }
      if (decimales == "61") {
        decimales = "62";
      }
      if (decimales == "60") {
        decimales = "61";
      }
      if (decimales == "59") {
        decimales = "60";
      }
      if (decimales == "58") {
        decimales = "59";
      }
      if (decimales == "57") {
        decimales = "58";
      }
      if (decimales == "56") {
        decimales = "57";
      }
      if (decimales == "55") {
        decimales = "56";
      }
      if (decimales == "54") {
        decimales = "55";
      }
      if (decimales == "53") {
        decimales = "54";
      }
      if (decimales == "52") {
        decimales = "53";
      }
      if (decimales == "51") {
        decimales = "52";
      }
      if (decimales == "50") {
        decimales = "51";
      }
      if (decimales == "49") {
        decimales = "50";
      }
      if (decimales == "48") {
        decimales = "49";
      }
      if (decimales == "47") {
        decimales = "48";
      }
      if (decimales == "46") {
        decimales = "47";
      }
      if (decimales == "45") {
        decimales = "46";
      }
      if (decimales == "44") {
        decimales = "45";
      }
      if (decimales == "43") {
        decimales = "44";
      }
      if (decimales == "42") {
        decimales = "43";
      }
      if (decimales == "41") {
        decimales = "42";
      }
      if (decimales == "40") {
        decimales = "41";
      }
      if (decimales == "39") {
        decimales = "40";
      }
      if (decimales == "38") {
        decimales = "39";
      }
      if (decimales == "37") {
        decimales = "38";
      }
      if (decimales == "36") {
        decimales = "37";
      }
      if (decimales == "35") {
        decimales = "36";
      }
      if (decimales == "34") {
        decimales = "35";
      }
      if (decimales == "33") {
        decimales = "34";
      }
      if (decimales == "32") {
        decimales = "33";
      }
      if (decimales == "31") {
        decimales = "32";
      }
      if (decimales == "30") {
        decimales = "31";
      }
      if (decimales == "29") {
        decimales = "30";
      }
      if (decimales == "28") {
        decimales = "29";
      }
      if (decimales == "27") {
        decimales = "28";
      }
      if (decimales == "26") {
        decimales = "27";
      }
      if (decimales == "25") {
        decimales = "26";
      }
      if (decimales == "24") {
        decimales = "25";
      }
      if (decimales == "23") {
        decimales = "24";
      }
      if (decimales == "22") {
        decimales = "23";
      }
      if (decimales == "21") {
        decimales = "22";
      }
      if (decimales == "20") {
        decimales = "21";
      }
      if (decimales == "19") {
        decimales = "20";
      }
      if (decimales == "18") {
        decimales = "19";
      }
      if (decimales == "17") {
        decimales = "18";
      }
      if (decimales == "16") {
        decimales = "17";
      }
      if (decimales == "15") {
        decimales = "16";
      }
      if (decimales == "14") {
        decimales = "15";
      }
      if (decimales == "13") {
        decimales = "14";
      }
      if (decimales == "12") {
        decimales = "13";
      }
      if (decimales == "11") {
        decimales = "12";
      }
      if (decimales == "10") {
        decimales = "11";
      }
      if (decimales == "09") {
        decimales = "10";
      }
      if (decimales == "08") {
        decimales = "09";
      }
      if (decimales == "07") {
        decimales = "08";
      }
      if (decimales == "06") {
        decimales = "07";
      }
      if (decimales == "05") {
        decimales = "06";
      }
      if (decimales == "04") {
        decimales = "05";
      }
      if (decimales == "03") {
        decimales = "04";
      }
      if (decimales == "02") {
        decimales = "03";
      }
      if (decimales == "01") {
        decimales = "02";
      }
      if (decimales == "00") {
        decimales = "01";
      }
      return decimales;
    },
    Numeros(string) {
      var out = "";
      var filtro = "1234567890,";
      for (var i = 0; i < string.length; i++)
        if (filtro.indexOf(string.charAt(i)) != -1) out += string.charAt(i);
      return out;
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