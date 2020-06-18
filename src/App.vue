<template>
  <div id="app">
    <header>ヘッダー</header>
    <div class="container">
      <main>
        <h2>収支</h2>
        <p>{{query}}月収支</p>
        <hr />
        <p>
          収入 {{sum}}
          円
        </p>
        <p>支出 ????円</p>
        <h1>ここにグラフが入ります</h1>
      </main>
      <div class="column">
        <div class="right">
          <h2>収入</h2>
          <p>
            日付：
            <input type="Date" v-model="incomeDate" />
          </p>
          <p>
            金額：
            <input type="Number" v-model="incomeMoney" />
          </p>
          <p>
            名目：
            <input type="text" v-model="incomeNominal" />
          </p>
          <button @click="addIncome">登録</button>
          <hr />
          <div v-for="income in incomes" :key="income.no">
            日付：{{income.id}} 金額：{{income.im}} 名目：{{income.in}}
            <button
              @click="deleteIncome(income)"
            >削除</button>
          </div>
        </div>
        <div class="right">
          <h2>支出</h2>
          <p>
            日付：
            <input type="Date" />
          </p>
          <p>
            金額：
            <input type="Number" />
          </p>
          <p>
            名目：
            <input type="text" />
          </p>
          <button>登録</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import moment from "moment";
// YYYY/MM/DDだと、input type="date"で認識してくれないので、YYYY-MM-DD形式に直す
let now = moment(new Date()).format("YYYY-MM-DD");

export default {
  data() {
    return {
      incomes: [],
      incomeDate: now,
      incomeMoney: "",
      incomeNominal: "",
      query: now,
      payments: [],
      paymentDate: now,
      paymentMoney: "",
      paymentNominal: ""
    };
  },

  mounted() {
    if (localStorage.getItem("incomes")) {
      try {
        this.incomes = JSON.parse(localStorage.getItem("incomes"));
      } catch (e) {
        localStorage.removeItem("incomes");
      }
    }
  },
  methods: {
    addIncome() {
      if (this.incomeMoney === "" && this.incomeDate === "") {
        return;
      }
      this.incomes.push({
        id: this.incomeDate,
        im: this.incomeMoney,
        in: this.incomeNominal
      });
      this.incomeDate = "";
      this.incomeMoney = "";
      this.incomeNominal = "";
      this.save();
    },
    deleteIncome(income) {
      this.incomes.splice(this.incomes.indexOf(income), 1);
      this.save();
    },

    save() {
      const a = JSON.stringify(this.incomes);
      localStorage.setItem("incomes", a);
    }
  },
  computed: {
    sum() {
      const total = this.incomes.reduce((sum, i) => sum + Number(i.im), 0);
      return total;
    }
  }
};
</script>

<style>
#app {
  width: 1000px;
  margin: 0 auto;
}
.container {
  display: flex;
}
.column {
  flex-direction: column;
}
main {
  flex: 1;
  height: 1000px;
}
.right {
  width: 450px;
  height: 500px;
}
</style>