<template>
  <div id="app">
    <header>ヘッダー</header>
    <div class="container">
      <main>
        <h2>収支</h2>
        <p>????年??月収支</p>
        <p>????円</p>
        <hr />
        <p>収入 ????円</p>
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
          <div
            v-for="income in incomes"
            :key="income.no"
          >日付：{{income.id}} 金額：{{income.im}} 名目：{{income.in}}</div>
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
export default {
  data() {
    return {
      incomes: [],
      incomeDate: "",
      incomeMoney: 0,
      incomeNominal: ""
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
      this.incomes.push({
        id: this.incomeDate,
        im: this.incomeMoney,
        in: this.incomeNominal
      });
      this.save();
    },
    save() {
      const a = JSON.stringify(this.incomes);
      localStorage.setItem("incomes", a);
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