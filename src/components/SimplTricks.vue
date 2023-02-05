<template>
  <div class="surface-200 -mt-5">
    <div
      class="flex gap-4 my-4 pt-4 pr-4 justify-content-end align-items-center"
    >
      <i class="pi pi-print"></i>
      <i class="pi pi-bell"></i>
      <i class="pi pi-user"></i>
    </div>
    <div
      class="flex md:flex-row gap-3 my-3 ml-4 md:justify-content-start justify-content-center flex-column align-items-center"
    >
      <CaleNdar inputId="icon" :showIcon="true" />

      <i class="pi pi-question-circle"></i>

      <DropDown placeholder="Sales units" />

      <span class="p-buttonset">
        <ButTon label="Accending" />
        <ButTon
          label="Decending"
          class="p-button-raised p-button-secondary surface-0 p-button-text"
        />
      </span>
    </div>
    <div
      class="m-4 bg-white p-3 border-round flex md:justify-content-start justify-content-center"
    >
      <DropDown placeholder="Sales units" />
    </div>
    <div class="grid gap-2 mx-4 flex md:flex-row flex-column">
      <CaRd
        style="margin-bottom: 2em; border: 1px solid red"
        class="bg-red-100 col"
      >
        <template #title>
          <div class="flex justify-content-center">RETURN ON INVESTMENT</div>
        </template>
        <template #content>
          <p class="flex justify-content-center text-red-500">
            <i class="pi pi-arRow-up font-bold" style="font-size: 4rem"
              ><span class="ml-2 font-bold font-bold">0%</span></i
            >
          </p>
        </template>
      </CaRd>
      <CaRd
        style="margin-bottom: 2em; border: 1px solid red"
        class="bg-red-100 col"
      >
        <template #title>
          <div class="flex justify-content-center">PROFIT MARGIN</div>
        </template>
        <template #content>
          <p class="flex justify-content-center text-red-500">
            <i class="pi pi-arRow-up mr-2 font-bold" style="font-size: 4rem"
              ><span class="ml-2 font-bold">0%</span></i
            >
          </p>
        </template>
      </CaRd>

      <CaRd
        style="margin-bottom: 2em; border: 1px solid gray"
        class="surface-400 col"
      >
        <template #title> </template>
        <template #content>
          <p class="flex justify-content-center">
            <i
              class="pi pi-arrow-down mr-2 font-bold text-red-500"
              style="font-size: 2rem"
            ></i
            ><span class="ml-2 font-bold" style="font-size: 1rem">87%</span>
          </p>
          <div class="flex gap-5 justify-content-center my-2">
            <p>1-7 Days</p>
            <p>$3,942.80</p>
            <p>1-33</p>
          </div>
          <div class="flex gap-5 justify-content-center">
            <p>8-14 Days</p>
            <p>$4,509.24</p>
            <p>30-1</p>
          </div>
        </template>
      </CaRd>
      <CaRd
        style="margin-bottom: 2em; border: 1px solid gray"
        class="surface-400 col"
      >
        <template #title> </template>
        <template #content>
          <p class="flex justify-content-center">
            <i
              class="pi pi-arrow-up mr-2 font-bold text-green-500"
              style="font-size: 2rem"
            ></i
            ><span class="ml-2 font-bold" style="font-size: 1rem">113%</span>
          </p>
          <div class="flex gap-5 justify-content-center my-2">
            <p>1-7 Days</p>
            <p>$3,942.80</p>
            <p>1-33</p>
          </div>
          <div class="flex gap-5 justify-content-center">
            <p>8-14 Days</p>
            <p>$4,509.24</p>
            <p>30-1</p>
          </div>
        </template>
      </CaRd>
    </div>
    <div class="flex md:flex-column flex-row">
      <DataTable :value="sales" responsiveLayout="scroll" class="mx-4">
        <ColumnGroup type="header">
          <TableRow>
            <ColUmn header="Product" :rowspan="3" />
            <ColUmn header="Sale Rate" :colspan="4" />
          </TableRow>
          <TableRow>
            <ColUmn header="Sales" :colspan="2" />
            <ColUmn header="Profits" :colspan="2" />
          </TableRow>
          <TableRow>
            <ColUmn header="Last Year" :sortable="true" field="lastYearSale" />
            <ColUmn header="This Year" :sortable="true" field="thisYearSale" />
            <ColUmn
              header="Last Year"
              :sortable="true"
              field="lastYearProfit"
            />
            <ColUmn
              header="This Year"
              :sortable="true"
              field="thisYearProfit"
            />
          </TableRow>
        </ColumnGroup>
        <ColUmn field="product" />
        <ColUmn field="lastYearSale">
          <template #body="slotProps">
            {{ slotProps.data.lastYearSale }}%
          </template>
        </ColUmn>
        <ColUmn field="thisYearSale">
          <template #body="slotProps">
            {{ slotProps.data.thisYearSale }}%
          </template>
        </ColUmn>
        <ColUmn field="lastYearProfit">
          <template #body="slotProps">
            {{ formatCurrency(slotProps.data.lastYearProfit) }}
          </template>
        </ColUmn>
        <ColUmn field="thisYearProfit">
          <template #body="slotProps">
            {{ formatCurrency(slotProps.data.thisYearProfit) }}
          </template>
        </ColUmn>
        <ColumnGroup type="footer">
          <TableRow>
            <ColUmn
              footer="Totals:"
              :colspan="3"
              footerStyle="text-align:right"
            />
            <ColUmn :footer="lastYearTotal" />
            <ColUmn :footer="thisYearTotal" />
          </TableRow>
        </ColumnGroup>
      </DataTable>
    </div>
  </div>
</template>
<script>
import { ref, computed } from "vue";

export default {
  setup() {
    const sales = ref([
      {
        product: "Bamboo Watch",
        lastYearSale: 51,
        thisYearSale: 40,
        lastYearProfit: 54406,
        thisYearProfit: 43342,
      },
      {
        product: "Black Watch",
        lastYearSale: 83,
        thisYearSale: 9,
        lastYearProfit: 423132,
        thisYearProfit: 312122,
      },
      {
        product: "Blue Band",
        lastYearSale: 38,
        thisYearSale: 5,
        lastYearProfit: 12321,
        thisYearProfit: 8500,
      },
      {
        product: "Blue T-Shirt",
        lastYearSale: 49,
        thisYearSale: 22,
        lastYearProfit: 745232,
        thisYearProfit: 65323,
      },
      {
        product: "BRown Purse",
        lastYearSale: 17,
        thisYearSale: 79,
        lastYearProfit: 643242,
        thisYearProfit: 500332,
      },
      {
        product: "Chakra Bracelet",
        lastYearSale: 52,
        thisYearSale: 65,
        lastYearProfit: 421132,
        thisYearProfit: 150005,
      },
      {
        product: "Galaxy Earrings",
        lastYearSale: 82,
        thisYearSale: 12,
        lastYearProfit: 131211,
        thisYearProfit: 100214,
      },
      {
        product: "Game Controller",
        lastYearSale: 44,
        thisYearSale: 45,
        lastYearProfit: 66442,
        thisYearProfit: 53322,
      },
      {
        product: "Gaming Set",
        lastYearSale: 90,
        thisYearSale: 56,
        lastYearProfit: 765442,
        thisYearProfit: 296232,
      },
      {
        product: "Gold Phone Case",
        lastYearSale: 75,
        thisYearSale: 54,
        lastYearProfit: 21212,
        thisYearProfit: 12533,
      },
    ]);

    const formatCurrency = (value) => {
      return value.toLocaleString("en-US", {
        style: "currency",
        currency: "USD",
      });
    };

    const lastYearTotal = computed(() => {
      let total = 0;
      for (let sale of sales.value) {
        total += sale.lastYearProfit;
      }

      return formatCurrency(total);
    });

    const thisYearTotal = computed(() => {
      let total = 0;
      for (let sale of sales.value) {
        total += sale.thisYearProfit;
      }

      return formatCurrency(total);
    });

    return { sales, formatCurrency, lastYearTotal, thisYearTotal };
  },
};
</script>
<style>
* {
  margin: 0;
  padding: 0;
}
</style>
