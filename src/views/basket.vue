<template>
<div class="basket">
    <div class="main">
        <div class="title">
            <h1>장바구니</h1>
        </div>
        <div class="selectDiv">
            <div class="allSelectDiv">
                <!-- <div><input type="checkbox" @click="allCheck()" id="allCheckedList"></div> -->
                <button class="selectBtn" @click="allCheck">전체선택</button>
                <button class="selectBtn" @click="allDisCheck">전체해제</button>
                <button class="selectBtn" @click="removeList">선택삭제</button>
            </div>
        </div>
        <div>
            <div class="listDiv" v-for="(item, idx) in getBasketList" :key="idx">
                <ul class="list">
                    <li class="list1">
                        <!-- <div><input class="checkedList" type="checkbox" @click="[productPrice(),sumPrice(),sumDelivery(),discount()]"></div> -->
                        <div><input class="checkedList" type="checkbox" @click="calcPrice"></div>
                    </li>
                    <li class="list2">
                        <div class="listImage">
                            <!-- <img style="width: 500px; height: 500px; border-radius: 10px" src="@/components/productDetail/image/product01.jpg" /> -->
                            <img class="productImage" :src="require(`@/components/productDetail/image/${item.img}`)" alt="">
                        </div>
                    </li>
                    <li class="list3">
                        <div>
                            <!-- {{ item.seller}} -->
                            <p>{{item.title}}</p>
                            <p>옵션1 : {{item.name}}</p>
                            <p>옵션2 : {{item.size}}</p>
                            <p>수량 : {{item.amount}}</p>
                        </div>
                    </li>
                    <li class="list4">
                        <div>
                            <p class="price">{{AddComma(item.price)}}원</p>
                            <p class="rate">{{AddComma(item.price*0.9)}}원</p>
                        </div>
                    </li>
                    <li class="list5">
                        <div>
                            <p>{{AddComma(item.delivery_fee)}}원</p>
                            <!-- <p class="info">{{item.info}}</p>
                            <p class="fee">{{item.fee}}</p> -->
                        </div>
                    </li>
                </ul>
            </div>
        </div>
    </div>
    <div class="right">
        <div class="inform">
            <div class="line">
                <h2>결제예정금액</h2>
            </div>
            <div>
                <h3>상품금액</h3>
                <label class="price" id="totalPro">0원</label>
            </div>
            <div>
                <h3>배송비(선결제)</h3>
                <label class="price" id="totalDel">0원</label>
            </div>
            <div>
                <h3>할인금액</h3>
                <label class="price" style="color:red;" id="totalSale">0원</label>
            </div>
            <div style="color:red; ">
                <h2>합계</h2>

                <label class="price" style="font-size:25px;" id="totalSum">0원</label>

            </div>
        </div>
        <div class="orderBtn">
            <router-link class="signUpLink" v-bind:to="'/payment'"> <button @click="selectList">주문</button></router-link>
        </div>

    </div>
</div>
</template>

<script>
import {
    createNamespacedHelpers
} from "vuex";
const basketList = createNamespacedHelpers("basketList");
const orderList = createNamespacedHelpers("orderList");
export default {
    data() {
        return {
            sum: 0,
            delivery: 0,
            product: 0,
            sale: 0,
            // items: [{
            //     image: "f1.jpg",
            //     name: "[뉴발란스] 운동화 MW880GR4 NBPQAS102G",
            //     option: "옵션변경",
            //     price: "125000",
            //     rate: "0",
            //     totalRate: "",
            //     info: "무료배송",
            // }, {
            //     image: "s1.jpg",
            //     name: "나이키 에어맥스97 트리플블랙",
            //     option: "옵션변경",
            //     price: "173000",
            //     rate: "10",
            //     totalRate: "",
            //     info: "무료배송",
            // }, {
            //     image: "b1.jpg",
            //     name: "[네파]21년 신상 남성용 벨키자 미드 구스 다운자켓(7H7026)",
            //     option: "옵션변경",
            //     price: "129000",
            //     rate: "24",
            //     totalRate: "",
            //     info: "무료배송",
            // }, {
            //     image: "b2.jpg",
            //     name: "LG Gram 17Z90N 노트북 17인치 IPS 초경량, (2560 x 1600), 10세대 인텔 코어 i7, 8GB RAM, 512GB SSD, 윈도우 10 홈, 17시간 배터리",
            //     option: "옵션변경",
            //     price: "1382490",
            //     rate: "14",
            //     totalRate: "",
            //     info: "예상 통관대행료",
            //     fee: "155360",
            // }, {
            //     image: "b3.jpg",
            //     name: "벌레퇴치 영국방역회사인정 초파리 페로몬 삼각트랩(1개입)",
            //     option: "옵션변경",
            //     price: "1980",
            //     rate: "0",
            //     totalRate: "",
            //     info: "배송비",
            //     fee: "2500",
            // }, ]
        }
    },
    methods: {
        calcPrice() {
            let checkedList = document.getElementsByClassName("checkedList");
            let totalPro = document.getElementById("totalPro");
            let totalDel = document.getElementById("totalDel")
            let totalSale = document.getElementById("totalSale");
            let totalSum = document.getElementById("totalSum");
            this.product = 0;
            this.delivery = 0;
            this.sale = 0;
            this.sum = 0;
            for (let i = 0; i < checkedList.length; i++) {
                if (checkedList[i].checked == true) {
                    this.product += Number(this.getBasketList[i].price);
                    this.delivery += Number(this.getBasketList[i].delivery_fee);
                    this.sale += this.getBasketList[i].price * 0.1;
                    this.sum += Number(this.getBasketList[i].price);
                }
            }
            totalPro.textContent = this.AddComma( this.product) + "원";
            totalDel.textContent = this.AddComma(this.delivery) + "원";
            totalSale.textContent = "-" + this.AddComma(this.sale) + "원";
            totalSum.textContent = this.AddComma(this.sum + this.delivery - this.sale) + "원";
        },
        allCheck() {
            // let allCheck = document.getElementById("allCheckedList");
            let checkedList = document.getElementsByClassName("checkedList");
            // if (allCheck.checked == true)
            for (let i = 0; i < checkedList.length; i++) {
                checkedList[i].checked = true;
                // }
                // else {
                //     for (let i = 0; i < checkedList.length; i++) {
                //         checkedList[i].checked = false;
                //     }
            }
            this.calcPrice();
        },
        allDisCheck() {
            // let allCheck = document.getElementById("allCheckedList");
            let checkedList = document.getElementsByClassName("checkedList");
            // if (allCheck.checked == true)
            //     for (let i = 0; i < checkedList.length; i++) {
            //         checkedList[i].checked = true;
            //     }
            // else {
            for (let i = 0; i < checkedList.length; i++) {
                checkedList[i].checked = false;
            }
            // }
            this.calcPrice();
        },
        AddComma(num) {
            var regexp = /\B(?=(\d{3})+(?!\d))/g;
            return num.toString().replace(regexp, ',');
        },
        removeList() {
            let checkedList = document.getElementsByClassName("checkedList");
            for (let i = checkedList.length - 1; i >= 0; i--) {
                if (checkedList[i].checked == true) {
                    this.delList(i);
                    checkedList[i].checked = false;
                }
            }
            let totalPro = document.getElementById("totalPro");
            let totalDel = document.getElementById("totalDel")
            let totalSale = document.getElementById("totalSale");
            let totalSum = document.getElementById("totalSum");

            totalPro.textContent = "0원";
            totalDel.textContent = "0원";
            totalSale.textContent = "0원";
            totalSum.textContent = "0원";
        },
        selectList() {
            let checkedList = document.getElementsByClassName("checkedList");
            this.clearOrderList();
            for (let i = 0; i < checkedList.length; i++) {
                if (checkedList[i].checked == true) {
                    this.addOrderList(this.getBasketList[i])
                }
            }
        },
        ...basketList.mapMutations(["delList"]),
        ...orderList.mapMutations(["addOrderList"]),
        ...orderList.mapMutations(["clearOrderList"]),
    },
    computed: {
        ...basketList.mapGetters(["getBasketList"]),
    },
}
</script>

 <style scoped>
        .basket {
            display: flex;
        }
        
        .main {
            display: inline-block;
            width: 85%;
            /* border: 1px solid black; */
        }
        
        .selectDiv {
            display: flex;
            width: 100%;
        }
        
        .selectDiv>div {
            width: 50%;
            /* border: 1px solid black; */
        
        }
        
        .allSelectDiv {
            display: flex;
        }
        
        .list {
            list-style: none;
            display: flex;
            width: 100%;
            margin: 0;
            padding: 0;
            margin-top: 10px;
            margin-bottom: 10px;
            background-color: #fafafa;
            border: 1px solid rgb(197, 195, 195);
            border-radius: 4px;
        }
        .list p {
            margin: 10px 0;
        }
        
        .list3 p {
            margin: 10px 0;
            padding: 0px;
        }
        
        .list3 .option {
            margin-right: 10px;
        }
        
        .list4 .price {
            font-size: 16px;
            margin: 10px 0;
            text-decoration: line-through;
            opacity: 0.5;
        }
        
        .list5 .info {
            margin: 10px 0;
            padding: 0px;
        }
        
        .list4 .rate {
            font-weight: bold;
            margin: 20px 0;
        }
        
        .list :nth-child(3) {
            width: 50%;
        }
        
        .list :nth-child(4) {
            width: 20%;
        
        }
        
        .list :nth-child(5) {
            width: 20%;
        }
        
        .list li {
            /* border: 1px solid black; */
            border-left: 1px solid rgb(197, 195, 195);
            position: relative;
        
            padding: 5px;
        }
        
        /* .listImage{
             width: 200px;
            height: 200px;
            overflow: hidden;
            margin: 0 auto;
        } */
        .list1 {
            width: 30px;
            margin: 0;
            padding: 0;
        }
        
        .list1 input {
            position: absolute;
            left: 50%;
            top: 50%;
            transform: translate(-50%, -50%);
            margin: 0;
            padding: 0;
        }
        
        /* .list3 {
            width: 15%;
        }
        
        .list4 {
            width: 15%;
        }
        
        .list5 {
            width: 70%;
        } */
        
        .right {
            position: relative;
            display: inline-block;
            width: 30%;
            /* border: 1px solid black; */
            padding: 10px;
            margin-left: 20px;
            min-height: 600px;
            border: 1px solid rgb(197, 195, 195);
            border-radius: 4px;
        }
        
        .inform {
            /* border: 1px solid black; */
            width: 100%;
            background-color: #fafafa;
            border-radius: 4px;
            border: 1px solid rgb(197, 195, 195);
            margin: 0;
        }
        
        .inform .line {
            margin: 0;
            border-bottom: 1px solid rgb(197, 195, 195);
           
        }
        
        .inform>div {
            display: flex;
            padding: 20px 5px;
        
        }
        
        .price {
          margin-left: auto;
          margin-top: 20px;
            
        }
        
        .orderBtn {
            margin-top: 20px;
            width: 100%;
            text-align: center;
            background-color: #0099ff;
            border-radius: 4px;
        }
        
        .productImage {
            width: 150px;
            height: 150px;
            object-fit: cover;
        }
        
        .productImage {
            width: 150px;
            height: 150px;
            object-fit: cover;
        }
        
        h1{
            background-color: #fafafa;
            border: 1px solid rgb(197, 195, 195);
            border-radius: 4px;
            padding: 10px;
            
        }
        
        .selectBtn {
            font-size: 15px;
            height: 22px;
            padding-top: 1px;
            padding-bottom: 1px;
        }
        .signUpLink > button {
            font-size: 22px;
            width: 100%;
            
        }
       

        </style>
