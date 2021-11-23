<template>
    <div class="home">
        <div v-if="showHideInputSection" class="inputSection">
            <input v-model="name" type="text" placeholder="Name" />
            <input v-model="amount" type="text" placeholder="Amount" />
            <input v-model="date" type="date" />
            <input v-model="months" type="text" placeholder="Which Months Paid" />
            <button @click="addData()">Submit</button>
        </div>
        <div v-else @click="showInputSection()" class="addSection">
            <i class="fas fa-plus"></i>
            <span>Add</span>
        </div>
        <div class="listSection">
            <div class="list" v-for="data in lists" :key="data.id">
                <span id="name">{{ data.name }}</span>
                <div class="amount">
                    <i id="rupees" class="fas fa-rupee-sign"></i>
                    <span>{{ data.amount }}</span>
                </div>
                <span>{{ data.date }}</span>
                <span> {{ data.months }}</span>
                <i @click="showDeletePage()" id="deleteButton" class="fas fa-trash"></i>
                <DeleteAlert class="alert" :alertStatus="deleteAlert" @close="deleteAlert = false">
                    <h3>Delete?</h3>
                    <span>Are you sure want to delete this file?</span>
                    <div class="cancelDeleteSection">
                        <div @click="cutDeletePage()" class="cancelSection">
                            <i class="far fa-window-close"></i>
                            <button>Cancel</button>
                        </div>
                        <div @click="deleteList(data.id)" class="deleteSection">
                            <i class="fas fa-trash"></i>
                            <button>Delete</button>
                        </div>
                    </div>
                </DeleteAlert>
            </div>
        </div>
    </div>
</template>
<script>
import DeleteAlert from "./DeleteAlert.vue";
export default {
    name: "Home",
    components: {
        DeleteAlert,
    },
    data() {
        return {
            showHideInputSection: false,
            lists: [],
            name: "",
            amount: "",
            date: "",
            months: "",
            records: null,
            deleteAlert: false,
        };
    },
    methods: {
        addData() {
            const id = Date.now();
            const dataToPush = {
                id,
                name: this.name,
                amount: this.amount,
                date: this.date,
                months: this.months,
            };
            this.lists.push(dataToPush);
            localStorage.setItem("record", JSON.stringify(this.lists));
            this.getList();
            this.name = "";
            this.amount = "";
            this.date = "";
            this.months = "";
            this.showHideInputSection = false;
        },
        getList() {
            this.records = JSON.parse(localStorage.getItem("record"));
            this.lists = this.records;
        },
        showInputSection() {
            this.showHideInputSection = true;
        },
        showDeletePage() {
            this.deleteAlert = true;
        },
        cutDeletePage() {
            this.deleteAlert = false;
        },
        deleteList(listtodelete) {
            this.lists = this.lists.filter((data) => {
                return data.id != listtodelete;
            });
            localStorage.setItem("record", JSON.stringify(this.lists));
            this.getList();
            this.deleteAlert = false;
        },
    //     practice() {
    //         let data;
    //         if (this.deleteAlert) {
    //             data = 1;
    //         } else {
    //             data = 2;
    //         }
    //     },
    //     practice1(){
    //     let data = this.deleteAlert ? 1 : 2;
    //    if(data==1){
    //        return true
    //    }
    //    else{
    //        return false
    //    }
    //     return data==1 ? true : false;
    //     return data==1
    //     },
    },
    created() {
        this.getList();
        console.log(this.records);
    },
};
</script>
<style scoped>
.home {
    height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;
}
.inputSection input {
    height: 20px;
    padding: 10px;
    outline: none;
    border: none;
    background-color: rgb(243, 239, 239);
    margin-top: 20px;
    font-size: 14px;
    font-weight: 550;
}
.inputSection button {
    background-color: orange;
    height: 36px;
    color: #ffff;
    font-weight: 700;
    font-size: 15px;
    margin-left: 10px;
    border: none;
    border-radius: 3px;
    cursor: pointer;
    width: 80px;
}
.addSection {
    background-color: green;
    width: 5%;
    height: 25px;
    border-radius: 5px;
    padding: 5px;
    display: flex;
    align-items: center;
    justify-content: space-evenly;
    cursor: pointer;
    margin-top: 20px;
}
.addSection i {
    font-size: 15px;
    color: #ffff;
}
.addSection span {
    font-size: 15px;
    color: #ffff;
    font-weight: 600;
}
.listSection {
    width: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
}
.list {
    display: flex;
    justify-content: space-between;
    background-color: rgb(226, 222, 222);
    border: 1px solid rgb(80, 79, 79);
    color: black;
    margin-top: 20px;
    padding: 10px;
    font-size: 16px;
    font-weight: 600;
    width: 50%;
}
.list i {
    color: red;
    font-size: 25px;
    cursor: pointer;
}
.list span {
    margin-left: 15px;
    margin-right: 20px;
}
.amount {
    display: flex;
    align-items: center;
}
#rupees {
    color: black;
    font-size: 20px;
    margin-right: -12%;
    cursor: auto;
}
.alert h3 {
    margin: 0px 0px 15px 0px;
    font-size: 22px;
}
.alert span {
    font-size: 16px;
    font-weight: 700;
}
.cancelDeleteSection {
    display: flex;
    justify-content: space-between;
    align-items: center;
}
.deleteSection {
    display: flex;
    justify-content: space-around;
    background-color: red;
    padding: 8px;
    border-radius: 4px;
    margin: 20px;
    cursor: pointer;
}
.deleteSection button {
    border: none;
    background-color: red;
    color: #fff;
    font-size: 18px;
    font-weight: 900;
    cursor: pointer;
}
.deleteSection i {
    color: #ffff;
    font-size: 18px;
}
.cancelSection {
    display: flex;
    justify-content: space-around;
    align-items: center;
    border: 1px solid rgb(240, 234, 234);
    padding: 8px;
    margin: 20px;
    border-radius: 4px;
    background-color: #ffff;
    cursor: pointer;
}
.cancelSection button {
    border: none;
    background-color: #fff;
    color: red;
    font-size: 17 px;
    font-weight: 550;
    cursor: pointer;
}
.cancelSection i {
    font-size: 20px;
    color: red;
}
@media only screen and (max-width: 350px) {
    .inputSection {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
    }
    .inputSection input {
        width: 100%;
        margin-top: 10px;
    }
    .inputSection button {
        margin-top: 5%;
    }
    .addSection {
        width: 20%;
    }
    .amount {
        margin-left: 10px;
    }
    .list {
        flex-direction: column;
        width: 90%;
        font-size: 13px;
        font-weight: 00;
        padding: 3px 0px;
        text-align: left;
        position: relative;
    }
    #deleteButton {
        font-size: 22px;
        position: absolute;
        top: 20%;
        right: 2%;
    }
    #name {
        font-size: 18px;
        font-weight: 800;
        text-transform: uppercase;
    }
    #rupees {
        font-size: 17px;
        margin-right: -4%;
    }
}
@media only screen and (min-width: 350px) and (max-width: 550px) {
    .inputSection {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
    }
    .inputSection input {
        width: 100%;
        margin-top: 10px;
    }
    .inputSection button {
        margin-top: 5%;
    }
    .addSection {
        width: 20%;
    }
    .amount {
        margin-left: 15px;
    }
    .list {
        flex-direction: column;
        width: 90%;
        font-size: 12px;
        font-weight: 00;
        padding: 5px 0px;
        text-align: left;
        position: relative;
    }
    #deleteButton {
        font-size: 24px;
        position: absolute;
        top: 23%;
        right: 2%;
    }
    #name {
        font-size: 14px;
        font-weight: 600;
        text-transform: uppercase;
    }
    #rupees {
        font-size: 12px;
        margin-right: -4%;
    }
}
</style>
