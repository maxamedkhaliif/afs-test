## Assignment 1 : table row
The data array of TableData object has been extracted from the getData(), so to be in the global scoop and accessible for any fucntion. 
The totalRow() is set to create a total object that their properties will be updated with the sum of the other row, and finally to be pushed to the data array and displayed in the table of home component. 

## Assignment 2 : Async/Await
Decouple the inside the mounthed() into multiple functions using Async/await approach instead of Promise chaining.
Refactore the getData() to change the state of loading property, then the map() is used to clone every item in the data array and generate a random number with Math.random() for the data.randomNumber property.
The async parseData() returns a promise object,
the function calls the getData() and parse the updated data to the tableData property to be passed then to the template and lastly it updates the loading property to false.

## Assignment 3 : Add a security class
Implement a Modal component that allows the user to add a security class to the table. To pass input data from the Form to Home component, the Vuex approache was on the table since an empty store was already implemented, but I used the $emit way since the data was already in top app component. The $emit lifts the data and triggers the addSecurityClass() component to push the input into the tableData and pass then to be rendred, then comes the updateTotal() to update the total row.

## Assignment 4 : Transfer search
Add an recordDate constrainte to the getter searchedTransfers() so it could include the recordDate the search.

## Assignment 5 : Style the transferRow.vue component
