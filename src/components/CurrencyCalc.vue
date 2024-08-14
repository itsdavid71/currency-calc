<template>
  <div class="currency-calculator">
    <h1>Калькулятор курса валют</h1>

    <form @submit.prevent="calcCurrency">
      <div>
        <input type="number" v-model="amount" id="amout" required>
      </div>
      <p class="info-p">Exchangeratesapi ограничивает выбор валюты, которую конвертируем :(</p>
      <div class="from-to">
        <select v-model="fromCurrency" id="from" required disabled>
          <option v-for="currency in currencies" :key="currency" :value="currency">{{ currency }}</option>
        </select>
        <div class="from-to-icon">
          <img src="../assets/right-arrow.png" alt="">
        </div>
        <select v-model="toCurrency" id="to" required>
            <option v-for="currency in currencies" :key="currency" :value="currency">{{ currency }}</option>
        </select>
      </div>
      <div>
        <button type="submit">Конвертировать</button>
      </div>
    </form>
    <div id="result" v-if="result">
      <h2>{{ result }}</h2>
    </div>
  </div>
</template>
<script>
  export default {
    data() {
      return {
        amount: 0,
        fromCurrency: 'EUR',
        toCurrency: 'RUB',
        result: null,
        currencies: [
          "AED", "AFN", "ALL", "AMD", "ANG", "AOA", "ARS", "AUD", "AWG", "AZN",
          "BAM", "BBD", "BDT", "BGN", "BHD", "BIF", "BMD", "BND", "BOB", "BRL",
          "BSD", "BTC", "BTN", "BWP", "BYN", "BYR", "BZD", "CAD", "CDF", "CHF",
          "CLF", "CLP", "CNY", "COP", "CRC", "CUC", "CUP", "CVE", "CZK", "DJF",
          "DKK", "DOP", "DZD", "EGP", "ERN", "ETB", "EUR", "FJD", "FKP", "FOK",
          "GBP", "GEL", "GGP", "GHS", "GIP", "GMD", "GNF", "GTQ", "GYD", "HKD",
          "HNL", "HRK", "HTG", "HUF", "IDR", "ILS", "IMP", "INR", "IQD", "IRR",
          "ISK", "JEP", "JMD", "JOD", "JPY", "KES", "KGS", "KHR", "KMF", "KPW",
          "KRW", "KWD", "KYD", "KZT", "LAK", "LBP", "LKR", "LRD", "LSL", "LYD",
          "MAD", "MDL", "MGA", "MKD", "MMK", "MNT", "MOP", "MRU", "MUR", "MVR",
          "MWK", "MXN", "MYR", "MZN", "NAD", "NGN", "NIO", "NOK", "NPR", "NZD",
          "OMR", "PAB", "PEN", "PGK", "PHP", "PKR", "PLN", "PYG", "QAR", "RON",
          "RSD", "RUB", "RWF", "SAR", "SBD", "SCR", "SDG", "SEK", "SGD", "SHP",
          "SLE", "SLL", "SOS", "SRD", "SSP", "STD", "STN", "SVC", "SYP", "SZL",
          "THB", "TJS", "TMT", "TND", "TOP", "TRY", "TTD", "TWD", "TZS", "UAH",
          "UGX", "USD", "UYU", "UZS", "VES", "VND", "VUV", "WST", "XAF", "XCD",
          "XDR", "XOF", "XPF", "YER", "ZAR", "ZMW", "ZWL"
        ],
      }
    },
    methods: {
      async calcCurrency() {
        const apiKey = 'aea1320d186d6a219a1179dd5c91818e';
        const apiUrl = `https://api.exchangeratesapi.io/v1/latest?access_key=${apiKey}`;
        try {
          const response = await fetch(apiUrl);
          const data = await response.json();
          const rate = data.rates[this.toCurrency];
          this.result = (this.amount * rate) + ' ' + this.toCurrency;
        } catch (error) {
          console.log(error);
          this.result = 'Произошла ошибка';
        }
      }
    }
  }
</script>

<style>

.info-p {
  font-size: 11px;
  opacity: 0.5;
}

.from-to {
  display: flex;
  margin: 10px 0;
}
.from-to-icon {
  padding: 20px;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 0;
}
.from-to-icon img {
  width: 20px;
}
.currency-calculator {
  max-width: 400px;
  margin: 0 auto;
  margin-top: 20px;
  font-family: Arial, "Helvetica Neue", Helvetica, sans-serif;
  padding: 20px;
  text-align: center;
  border: 1px solid #99999928;
  border-radius: 10px;
}
h1 {
  margin-top: 0;
  font-size: 18px;
  font-weight: 400;
}


.currency-calculator label {
  display: block;
  margin-bottom: 5px;
}

.currency-calculator input,
.currency-calculator select,
.currency-calculator button {
  width: 100%;
  box-sizing: border-box;
  padding: 8px;
  margin-top: 5px;
}
.currency-calculator input,
.currency-calculator select {
  border: 1px solid #9999994d;
  border-radius: 5px;
  padding: 20px;
}
.currency-calculator button {
  background: #4584ff;
  border: none;
  border-radius: 5px;
  color: #fff;
  font-weight: 600;
  padding: 15px 0;
  cursor: pointer;
}
.currency-calculator button:hover {
  background: #396bd1;

}

.currency-calculator h2 {
  margin-top: 20px;
  margin-bottom: 0;
  color: #222;
}
</style>