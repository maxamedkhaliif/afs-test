<template>
  <div class="home">
    <h1>This is a table with some important data</h1>
    <b-table :data="tableData" :columns="columns"></b-table>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import { TableData } from "@/types/types";

@Component
export default class Home extends Vue {
  tableData: TableData[] = [];
  columns = [
    {
      label: "Security class",
      field: "name",
    },
    {
      label: "Authorized amount",
      field: "authorizedAmount",
    },
    {
      label: "Issued amount",
      field: "issuedAmount",
    },
    {
      label: "Authorized Capital",
      field: "authorizedCapital",
    },
    {
      label: "Issued capital",
      field: "issuedCapital",
    },
  ];

  /**
   * Extract the data array from the getData function
   * to be accessible from the file scoop
   */
  data = [
    {
      id: "42f2462d-49d0-4e91-8fe1-de2e656b0f06",
      name: "Series A",
      nominalValue: 5,
      authorizedAmount: 1500,
      issuedAmount: 500,
      authorizedCapital: 7550,
      issuedCapital: 2500,
    },
    {
      id: "42f2462d-49d0-4e91-8fe1-de2e656b0f06",
      name: "Series B",
      nominalValue: 10,
      authorizedAmount: 15000,
      issuedAmount: 5000,
      authorizedCapital: 150000,
      issuedCapital: 50000,
    },
    {
      id: "fd78c11b-e3d2-455a-99b0-49907a75c463",
      name: "Series C",
      nominalValue: 1,
      authorizedAmount: 96876,
      issuedAmount: 61760,
      authorizedCapital: 96876,
      issuedCapital: 61760,
    },
    {
      id: "d8654cb0-8986-4fbc-b969-025e514cb934",
      name: "Series D",
      nominalValue: 1,
      authorizedAmount: 10110,
      issuedAmount: 1100,
      authorizedCapital: 10110,
      issuedCapital: 1100,
    },
  ];

  loading = false;

  /**
  * totalRow() retrieves the data array and adds
  * the total of the other rows
  */
  totalRow(data: TableData[]): void {
    // Create total object
    var total = {
      id: `${(Math.random()*100000).toString()}`,
      name: "Total",
      nominalValue: 0,
      authorizedAmount: 0,
      issuedAmount: 0,
      authorizedCapital: 0,
      issuedCapital: 0,
    };

    //Sum each row to the total object
    data.forEach(dataItem => {
      total.authorizedAmount += dataItem.authorizedAmount;
      total.issuedAmount += dataItem.issuedAmount;
      total.authorizedCapital += dataItem.authorizedCapital;
      total.issuedCapital += dataItem.issuedCapital;
    });

    //update data array
    data.push(total);
  }

  mounted(): void {
    //Invoke totalRow() and pass the updated data array
    this.totalRow(this.data);

    this.getData(this.data)
      .then((data: TableData[]) => {
        this.loading = true;
        return data.map((dataItem: TableData) => {
          return {
            ...dataItem,
            randomNumber: Math.random(),
          };
        });
      })
      .then((data: TableData[]) => {
        this.tableData = data;
        this.loading = false;
      })
      .catch((error) => {
        console.log(error, "This is not good");
      });
  }

  //Update getData() to return the passed data array
  async getData(data: TableData[]): Promise<TableData[]> {
    return data;
  }
}
</script>
