<script lang="ts" setup>
import { ref, computed, onMounted } from "vue";

const show = ref(false);

interface compoundData {
  date: number;
  profit: string;
  amount: string;
  rate: string;
}

const principal = ref("10000000");
const period_input = ref(20);
const period = ref(0);
const _rate = ref(5);
const result = ref<compoundData[]>([]);
const currency = ref("원");
const totalProfit = ref(0);
const totalRate = ref(0);
const totalAmount = ref(0);

const cal = function () {
  show.value = false;
  totalProfit.value = 0;
  period.value = period_input.value;

  result.value = [];
  const start = Number(principal.value.replace(/,/g, ""));
  totalAmount.value = start;
  for (let i = 0; i < period.value; i++) {
    const date = i + 1;
    const profit = (totalAmount.value * _rate.value) / 100;
    totalProfit.value += profit;

    totalAmount.value = totalAmount.value + profit;
    const rate = ((totalAmount.value - start) / start) * 100;
    totalRate.value = rate;
    const temp: compoundData = {
      date: date,
      profit: Math.round(profit).toLocaleString("en-US") + currency.value,
      amount:
        Math.round(totalAmount.value).toLocaleString("en-US") + currency.value,
      rate: rate.toFixed(2) + "%",
    };
    result.value.push(temp);
  }

  show.value = true;
};

const comma = function () {
  principal.value = principal.value.replace(/,/g, "");
  principal.value = principal.value.replace(
    /\B(?<!\.\d*)(?=(\d{3})+(?!\d))/g,
    ","
  );
};

const numberStyle = function (num: number) {
  return Math.round(num).toLocaleString("en-US") + currency.value;
};

onMounted(() => {
  comma();
});
</script>

<template>
  <div class="table-container">
    <div class="table-wrapper">
      <div class="inputBox">
        <div class="input-wrapper">
          <label for="principal">투자원금</label>
          <input
            type="text"
            id="principal"
            v-model="principal"
            @change="comma"
          />
        </div>
        <div class="input-wrapper">
          <label for="period">복리기간</label>
          <input type="number" id="period" v-model="period_input" />
        </div>
        <div class="input-wrapper">
          <label for="rate">수익률</label>
          <input type="number" id="rate" v-model="_rate" />
        </div>
        <button @click="cal()">계산</button>
      </div>
    </div>
    <div v-if="show" class="result-container">
      <div class="box">
        <div class="stat">
          <span class="title">누적수익</span
          ><span class="content">{{ numberStyle(totalProfit) }}</span>
        </div>
        <div class="stat">
          <span class="title">최종 금액</span
          ><span class="content">{{ numberStyle(totalAmount) }}</span>
        </div>
        <div class="stat">
          <span class="title">최종 수익률</span
          ><span class="content">{{ totalRate.toFixed(2) + "%" }}</span>
        </div>
        <div class="stat">
          <span class="title">총 복리기간</span
          ><span class="content">{{ period }}</span>
        </div>
      </div>
      <table>
        <thead>
          <th scope="col">기간</th>
          <th scope="col">수익</th>
          <th scope="col">총 금액</th>
          <th scope="col">수익률</th>
        </thead>
        <tbody>
          <tr v-for="line in result" :key="line.date">
            <td v-for="(item, index) in line" :key="index">
              {{ item }}
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.table-container {
  width: 100%;
  display: flex;
  flex-direction: column;
  padding-top: 60px;
  .table-wrapper {
    display: flex;
    margin: 0 auto;
    .inputBox {
      display: flex;
      flex-direction: column;
      align-items: center;
      padding-top: 25px;
      animation: riseUp 1s;
      .input-wrapper {
        display: flex;
        justify-content: center;
        align-items: center;
        margin: 25px;
        label {
          font-size: 20px;
          font-weight: var(--font-weight-b);
          padding-bottom: 1px;
          width: 120px;
          text-align: center;
        }
        input {
          height: 36px;
          padding: 0 16px;
          transition: 0.2s;

          &:focus-visible {
            border-color: var(--input-focus);
          }
        }
      }

      button {
        height: 36px;
        width: 160px;
        margin: 25px;
        cursor: pointer;
        font-size: 16px;
        // background: var(--btn-bg);
        background: var(--bg-color);
        color: var(--font-color);
        border: var(--btn-border);
        // border: var(--border);

        // box-shadow: var(--box-shadow);
        &:hover {
          // box-shadow: var(--box-shadow-hover);
          background: var(--btn-bg);
          transition: all 0.4s;
          color: var(--c-white);
        }
      }
    }
  }
  .result-container {
    display: flex;
    flex-direction: column;
    justify-content: center;
    margin: 25px auto;
    background: var(--bg-color-2);
    border: var(--border);
    box-shadow: var(--box-shadow);
    border-radius: var(--border-radius);
    animation: riseUp 1s;

    .box {
      margin: 25px 25px 0;
      display: flex;
      flex-direction: column;
      .stat {
        flex-grow: 1;
        display: flex;
        justify-content: space-between;
        width: 50%;
        margin: 7px auto 0;
        .title {
          font-weight: 300;
          margin-right: 10px;
        }
      }
    }
    table {
      margin: 25px;
      border: var(--border);
      border-collapse: collapse;
      text-align: center;
      font-size: 14px;
      thead th {
        font-weight: 400;
        width: 200px;
        &:nth-child(1) {
          width: 80px;
        }
      }
      th,
      td {
        border: var(--border);

        font-weight: 300;
      }
      th {
        padding: 3px 0;
      }
      td {
        color: var(--font-color-2);
        padding: 2px 0;
      }
    }
  }
}
</style>
