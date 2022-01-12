<template>
    <div class="modal-backdrop">
        <div class="modal"
        style="display: block" 
        role="dialog" 
        aria-labelledby="table-input"
        aria-describedby="security-class-input">

            <header class="modal-header" id="inputForm">
                <h2>Add Security Class</h2>
                <button class="btn-green" 
                @click="closeModal" 
                aria-label="Close modal">
                    X
                </button>
            </header>
            
            <section class="modal-body" id="addSecurityClass">
                <form @submit="onSubmit" method="post">
                    <h3>Enter you security class data</h3>

                    <label for="id">ID</label>
                    <input type="text" name="id" id="id" v-model="id" placeholder="Ex: 42f2462d-49d0-4e91-8fe1-de2e656b0f06"/>
            
                    <label for="name">Name</label>
                    <input type="text" name="name" id="name" v-model="name" placeholder="Ex: Series X" />
            
                    <label for="nominalValue">Nominal Value</label>
                    <input name="nominalValue" id="nominalValue" v-model.number="nominalValue" type="number" placehoder="Ex: 5" />
            
                    <label for="authorizedAmount">Authorized Amount</label>
                    <input name="authorizedAmount" id="authorizedAmount" v-model.number="authorizedAmount" type="number" placeholder="Ex: 1500" />
            
                    <label for="issuedAmount">Issued Amount</label>
                    <input name="issuedAmount" id="issuedAmount" v-model.number="issuedAmount" type="number" placeholder="Ex: 500" />
            
                    <label for="authorizedCapital"> Authorized Capital</label>
                    <input name="authorizedCapital" id="authorizedCapital" v-model.number="authorizedCapital" type="number" placeholder="Ex: 7550" />
            
                    <label for="issuedCapital">Issued Capital</label>
                    <input name="issuedCapital" id="issuedCapital" v-model.number="issuedCapital" type="number" placeholder="Ex: 2500" />

                    <input type="submit" value="Add" id="submit">
                </form>
            </section>
        </div>
    </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import { TableData } from "@/types/types";

@Component
export default class Form extends Vue {
    //Bind form data
    data(): TableData {
    return {
        id: "",
        name: "",
        nominalValue: 0,
        authorizedAmount: 0,
        issuedAmount: 0,
        authorizedCapital: 0,
        issuedCapital: 0
        } 
    }

    onSubmit(e: any): void {
        e.preventDefault();
        //Create new security class object
        const newClass = {
            id: this.id,
            name: this.name,
            nominalValue: this.nominalValue,
            authorizedAmount: this.authorizedAmount,
            issuedAmount: this.issuedAmount,
            authorizedCapital: this.authorizedCapital,
            issuedCapital: this.issuedCapital
        }

        //Emit the security class to parent component
        this.$emit("add-security-class", newClass);
        this.$emit("update-total");

        //Reset Form
        this.id = ""
        this.name = ""
        this.nominalValue = 0
        this.authorizedAmount = 0
        this.issuedAmount = 0
        this.authorizedCapital = 0
        this.issuedCapital = 0

    }

    //Close modal
    closeModal(): void {
        this.$emit("close");
    }
}
</script>

<style lang="scss">
.modal-backdrop {
    position: fixed;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    background-color: rgba(0, 0, 0, 0.5);
    display: flex;
    
    .modal {
        margin: auto;
        background: #FFFFFF;
        box-shadow: 2px 2px 20px 1px;
        max-width: 40%;
        max-height: 80%;

        .modal-header {
            padding: 15px;
            display: flex;
            position: relative;
            border-bottom: 1px solid #eeeeee;
            color: #4AAE9B;
            justify-content: space-between;
        }

        .btn-green, #submit {
            color: white;
            background: #4AAE9B;
            border: 1px solid #4AAE9B;
            border-radius: 2px;
        }

        .modal-body {
            position: relative;
            padding: 20px 10px;
            overflow: visible;

            form {
                display: flex;
                flex-direction: column;
                label {
                    text-align: left;
                    font-size: 1.1rem;
                    margin-top: 15px;
                }

                input {
                    font-size: 1.2rem;
                }

                #submit {
                    margin-top: 10px;
                    width: 50px;
                }
            }                
        }
    }
}
</style>