<template>
  <div class="home">
    <h1>This is a table with some important data</h1>
    <button type="button" class="btn" @click="showModal">Add Security Class</button>
    <b-table :data="tableData" :columns="columns"></b-table>
    <Form v-show="isModalVisible" style="display: block" @close="closeModal" @add-security-class="addSecurityClass" @update-total="updateTotal" />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import { TableData } from "@/types/types";
import Button from '../components/Button.vue';
import Form from '../components/Form.vue';

@Component({
  components: {
    Form
  }
})
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
  dataArray = [
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

  //Booleans
  loading = false;
  isModalVisible = false;

  /**
  * totalRow() retrieves the dataArray array and adds
  * the total of the other rows
  */
  totalRow(table: TableData[]): void {
    // Create total object
    var Total = {
      id: `${(Math.random()*100000).toString()}`,
      name: "Total",
      nominalValue: 0,
      authorizedAmount: 0,
      issuedAmount: 0,
      authorizedCapital: 0,
      issuedCapital: 0,
    };

    //Sum each row to the Total object
    table.forEach(tableItem => {
      Total.authorizedAmount += tableItem.authorizedAmount;
      Total.issuedAmount += tableItem.issuedAmount;
      Total.authorizedCapital += tableItem.authorizedCapital;
      Total.issuedCapital += tableItem.issuedCapital;
    });

    //update dataArray table
    table.push(Total);
  }

  async mounted(): Promise<void> {
    //Invoke totalRow() and pass the updated dataArray array
    this.totalRow(this.dataArray);

    return await this.parseDataArray();
  }

  //Parse the updated dataArray to tableData
  async parseDataArray(): Promise<void> {
    this.tableData = await this.getDataArray(this.dataArray);
    this.loading = false
  }

  //Update getDataArray() to map and manipulate the dataArray array
  async getDataArray(dataArray: TableData[]): Promise<TableData[]> {
      this.loading = true;
      return dataArray.map((dataArrayItem: TableData) => {
        return {...dataArrayItem,
        randomNumber: Math.random(),
        }
      })
  }
  
  //Push newly added security class to the data array and update it
  addSecurityClass(newClass: TableData): TableData[] {
    this.tableData.pop();
    return this.tableData = [...this.tableData, newClass]
  }

  //Update total after each table input
  updateTotal() {
    this.totalRow(this.tableData);
  }

  //Open modal
  showModal(): boolean {
    return this.isModalVisible = true;
  }

  //Close modal
  closeModal(): boolean {
    return this.isModalVisible = false;
  }
}
</script>
