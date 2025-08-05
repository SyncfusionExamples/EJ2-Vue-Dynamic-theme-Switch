<template>
  <div id="app">
    <div id='container'>
        <br>
        <ejs-dropdownlist id='dropdownlist' :dataSource='themes' :change='onChange' placeholder='Select a theme'></ejs-dropdownlist>
        <br/>
        <br/>
        <ejs-grid :dataSource="data">
        <e-columns>
          <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=90></e-column>
          <e-column field='CustomerID' headerText='Customer ID' width=120></e-column>
          <e-column field='Freight' headerText='Freight' textAlign='Right' format='C2' width=90></e-column>
        </e-columns>
       </ejs-grid>
    </div>
  </div>
</template>
<script>
import { DropDownListComponent } from "@syncfusion/ej2-vue-dropdowns";
import { GridComponent, ColumnsDirective, ColumnDirective, Page } from "@syncfusion/ej2-vue-grids";
import { Ajax } from '@syncfusion/ej2-base';

export default {
  components: {
    'ejs-dropdownlist': DropDownListComponent,
    'ejs-grid': GridComponent,
    'e-columns': ColumnsDirective,
    'e-column': ColumnDirective
  },
  data (){
    return {
      themes: ['material', 'fabric', 'bootstrap'],
      data: [
          { OrderID: 10248, CustomerID: 'VINET', Freight: 32.38 },
          { OrderID: 10249, CustomerID: 'TOMSP', Freight: 11.61 },
          { OrderID: 10250, CustomerID: 'HANAR', Freight: 65.83 },
          { OrderID: 10251, CustomerID: 'VICTE', Freight: 41.34 },
          { OrderID: 10252, CustomerID: 'SUPRD', Freight: 51.3 },
          { OrderID: 10253, CustomerID: 'HANAR', Freight: 58.17 },
          { OrderID: 10254, CustomerID: 'CHOPS', Freight: 22.98 },
          { OrderID: 10255, CustomerID: 'RICSU', Freight: 148.33 },
          { OrderID: 10256, CustomerID: 'WELLI', Freight: 13.97 }
      ],
      pageSettings: { pageSize: 5 }
    }
  },
  provide: {
    grid: [Page]
  },
  methods: {
    onChange: function(e) {
        console.log(e);
        if (e && e.itemData.value) {
            let ajax = new Ajax('src/assets/styles/' + e.itemData.value + '.css', 'GET', true);
            ajax.send().then((result) => {
              let styleTag = document.getElementById('theme');
              if (styleTag) {
                styleTag.innerHTML=`/*${e.itemData.value}*/` + result;
              }
            });
        }
    }
  }
}

</script>
