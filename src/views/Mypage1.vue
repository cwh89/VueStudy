<template>
<div>
    <!--top-->
    <div class="top" style="text-align:center">

        <h1>마이페이지</h1>
    </div>
    <div class="container">
        <!--left-->
        <div class="left">
            <div class="List1">
                <router-link v-bind:to="'/mypage1'">나의쇼핑내역</router-link>
                <hr>
            </div>
            <div class="Check">
                <a href="">주문/배송 조회</a><br>
                <a href="">취소/반품/교환 신청</a><br>
                <a href="">취소/반품/교환 현황</a><br>
                <a href="">환불/입금내역</a><br>
                <a href="">영수증/소득공제</a><br>
            </div>
            <div class="List2">
                <router-link v-bind:to="'/mypage2'">회원정보 열람</router-link>
                <hr>
            </div>
            <div class="Check">
                <a href="">닉네임 수정</a><br>
                <a href="">비밀번호 수정</a><br>
                <a href="">전화번호 수정</a><br>
                <a href="">주소 수정</a><br>
                <a href="">회원정보 변경/ 탈퇴</a><br>
                <a href="">로그인 관리</a><br>
                <a href="">개인정보 이용내역</a>
            </div>
            <!-- <router-link v-bind:to="'/'"> <button class="logoutbtn" @click="logout"> 로그아웃 </button></router-link> -->
            <!-- <router-link v-bind:to="'/'"> <button class="logoutbtn"> 로그아웃 </button></router-link> -->
        </div>
        <!--right-->
        <div class="right">
            <div class="pList1">
                <h2>나의쇼핑내역</h2><br>주문/ 배송 / 취소 / 환불 조회
            </div>
            <div class="date1">
                <div class="table1st">
                    <div class="tables_header">조회기간</div>
                    <div>
                        <div class="row1">
                            <button class="dateBtn">오늘</button>
                            <button class="dateBtn">1주일</button>
                            <button class="dateBtn">1개월</button>
                            <button class="dateBtn">6개월</button>
                            <button class="dateBtn">12월</button>
                            <button class="dateBtn">11월</button>
                            <button class="dateBtn">10월</button>
                        </div>
                        <div class="row2">
                            <select name="" id="" @change="setStartYear">
                                <option v-for="n in years" :key="n" :value="n" :selected="n == getYear()">{{n}}</option>
                            </select>
                            <label for="">년</label>
                            <select name="" id="" @change="setStartMonth">
                                <option v-for="n in 12" :key="n" :value="n" :selected="n == getMonth()">{{n}}</option>
                            </select>
                            <label for="">월</label>
                            <select name="" id="" @change="setStartDate">
                                <option v-for="n in 31" :key="n" :value="n" :selected="n == getDate()">{{n}}</option>
                            </select>
                            <label for="">일</label>
                            -
                            <select name="" id="" @change="setEndYear">
                                <option v-for="n in years" :key="n" :value="n" :selected="n == getYear()">{{n}}</option>
                            </select>
                            <label for="">년</label>
                            <select name="" id="" @change="setEndMonth">
                                <option v-for="n in 12" :key="n" :value="n" :selected="n == getMonth()">{{n}}</option>
                            </select>
                            <label for="">월</label>
                            <select name="" id="" @change="setEndDate">
                                <option v-for="n in 31" :key="n" :value="n" :selected="n == getDate()">{{n}}</option>
                            </select>
                            <label for="">일</label>
                        </div>
                        <div class="row3">
                            <input type="text" class="searchBar" id="searchInput" placeholder="주문 상품명을 검색하세요!">
                            <button class="searchBtn" @click="search">조회하기</button>
                        </div>
                    </div>
                </div>
            </div>

            <div class="pList2">
                <h2>주문내역 조회</h2>
            </div>

            <div class="date2">
                <table class="table2" style="width:1000px">
                    <tr class="tr1" style="height:50px;">
                        <td id="edge1" style="width:100px">주문일자</td>
                        <td style="width:80px">이미지</td>
                        <td style="width:80px">판매자명</td>
                        <td style="width:370px">상품명</td>
                        <td style="width:90px">옵션</td>
                        <td style="width:100px">수량</td>
                        <td style="width:100px">가격</td>
                        <td id="edge2" style="width:80px">배송비</td>
                    </tr>
                    <!-- v-show="compareDate(item) && compareInform(item)" -->
                    <tr v-for="(item, idx) in users" :key="idx" v-show="compareDate(item) && compareInform(item) ">
                        <td style="height:30px;">{{item.orderDate}}</td>
                        <td style="height:30px;">
                            <img :src="require(`@/components/mainPage/productTableImage/${item.img}`)" alt="banner" style="width:50px; height:50px;">
                        </td>
                        <td>{{item.name}}</td>
                        <td>{{item.product}}</td>
                        <td>{{item.option}}</td>
                        <td>{{item.amount}}</td>
                        <td>{{AddComma(item.price)}}원</td>
                        <td>{{item.charge}}</td>
                    </tr>
                </table>
            </div>

            <div class="pList3">
                <h2>취소/환불 조회</h2>
            </div>
            <div class="date3">
                <table class="table3" style="width:1000px">
                      <tr class="tr1" style="height:50px;">
                        <td id="edge1" style="width:100px">주문일자</td>
                        <td style="width:80px">이미지</td>
                        <td style="width:80px">판매자명</td>
                        <td style="width:370px">상품명</td>
                        <td style="width:90px">옵션</td>
                        <td style="width:100px">가격</td>
                        <td style="width:100px">처리상태</td>
                        <td id="edge2" style="width:80px">결과</td>
                    </tr>
                    <!-- v-show="compareDate(item) && compareInform(item)" -->
                    <tr v-for="(item, asd) in users2" :key="asd" v-show="compareDate(item) && compareInform(item) ">
                        <td style="height:30px;">{{item.orderDate}}</td>
                        <td style="height:30px;">
                            <img :src="require(`@/components/mainPage/productTableImage/${item.img}`)" alt="banner" style="width:50px; height:50px;">
                        </td>
                        <td>{{item.name}}</td>
                        <td>{{item.product}}</td>
                        <td>{{item.option}}</td>
                        <td>{{AddComma(item.price)}}원</td>
                        <td>{{item.process}}</td>
                        <td>{{item.result}}</td>
                    </tr>
                </table>
            </div>
        </div>
    </div>
</div>
</template>

<script>
import userList from "../assets/data/orderList.json";
import userList2 from "../assets/data/refundList.json";
export default {
    data() {
        return {
            startPoint: {
                year: "1900",
                month: "01",
                date: "01",
            },
            endPoint: {
                year: this.getYear(),
                month: this.getMonth(),
                date: this.getDate(),
            },
            years: [],
            months: [],
            dates: [],
            target: "",

        }
    },
    name: "userList",
    name2: "userList2",
    computed: {
        users() {
            return userList.users.map((items) => {
                return items;
            })
        },
        users2() {
            return userList2.users2.map((items) => {
                return items;
            })
        }
    },
    methods: {
        getDate() {
            let today = new Date();
            let date = today.getDate();
            return date;
        },
        getMonth() {
            let today = new Date();
            let month = today.getMonth() + 1;
            return month;
        },
        getYear() {
            let today = new Date();
            let year = today.getFullYear();
            return year;
        },
        // 2000-01-01
        replaceAt(input, index, character) {
            return input.substr(0, index) + character + input.substr(index + character.length);
        },
        setStartDate(event) {
            if (event.target.value < 10)
                this.startPoint.date = 0 + event.target.value;
            else
                this.startPoint.date = event.target.value;
        },
        setStartMonth(event) {
            if (event.target.value < 10)
                this.startPoint.month = 0 + event.target.value;
            else
                this.startPoint.month = event.target.value;
        },
        setStartYear(event) {
            this.startPoint.year = event.target.value;
        },
        setEndDate(event) {
            if (event.target.value < 10)
                this.endPoint.date = 0 + event.target.value;
            else
                this.endPoint.date = event.target.value;
        },
        setEndMonth(event) {
            if (event.target.value < 10)
                this.endPoint.month = 0 + event.target.value;
            else
                this.endPoint.month = event.target.value;
        },
        setEndYear(event) {
            this.endPoint.year = event.target.value;
        },
        compareDate(target) {
            // alert(`${this.selectTerm.year}-${this.selectTerm.month}-${this.selectTerm.date}`)
            // alert(target.date)
            if (`${this.startPoint.year}-${this.startPoint.month}-${this.startPoint.orderDate}` <= target.orderDate)
                if (target.orderDate <= `${this.endPoint.year}-${this.endPoint.month}-${this.endPoint.date}`)
                    return true;
        },
        search() {
            this.target = document.getElementById("searchInput").value
        },
        compareInform(event) {
            if (this.target == "")
                return true;
            else {
                // if (this.target == event.inform)
                if (event.product.indexOf(this.target) !== -1)
                    return true;
                else
                    return false;
            }
        },
        AddComma(num) {
            var regexp = /\B(?=(\d{3})+(?!\d))/g;
            return num.toString().replace(regexp, ",");
        },
    },
    mounted() {
        {
            for (let i = this.getYear() - 10; i <= this.getYear(); i++) {
                this.years.push(i);
            }
            this.year = this.getYear();
            this.month = this.getMonth();
            this.date = this.getDate();
        }
    }
}
</script>

<style scoped>
a {
    text-decoration: none;
    color: inherit;
    margin-left: 15px;
}

hr {
    width: 200px;
}

tr {
    border: inherit;
}

.top {
    margin-left: 70px;
}

.container {
    display: flex;
    border: none;
}

.left {
    display: inline-block;
    height: 1090px;
    border: 1px solid rgb(197, 195, 195);
    background-color: #fafafa;
    border-radius: 4px;
    width: 210px;
    padding: 15px;
    padding-top: 40px;
    font-size: 18px;
}

.right {
    display: inline-block;
    height: 1150px;
    width: 85%;
    border: 1px solid rgb(197, 195, 195);
    margin-left: 50px;
    background-color: #fafafa;
    border-radius: 4px;
}

.pList1,
.pList2,
.pList3 {
    text-align: center;
    border-bottom: 1px solid rgb(197, 195, 195);

}

.date1,
.date2 {

    border-bottom: 1px solid rgb(197, 195, 195);
    padding-top: 20px;
    padding-bottom: 20px;
}

.date1 {
    display: flex;
}

.date2 {
    height: 300px;
    overflow-y: scroll;
}

.date3 {
    margin-top: 20px;
    padding-top: 15px;
    height: 300px;
    overflow-y: scroll;
}

.table1st {
    margin-left: auto;
    margin-right: auto;
    display: flex;

}

.tables_header {
    width: 150px;
    padding-top: 20px;
    text-align: center;
    line-height: 90px;
    font-weight: bold;
    border: 1px solid;
    border-radius: 4px;
    background-color: #00ba54;
    color: white;
    margin-right: 20px;
}

.searchBtn {
    margin-left: 20px;
}

.row1,
.row2 {
    padding: 1px;
    border-radius: 4px;
}

.row2 {
    margin-left: 6px;
}

.row3 {
    display: flex;
    padding: 5px 0px;
}

.searchBar {
    width: 400px;
    margin-left: auto;
    margin-right: 1px;
    border-radius: 4px;
    border: 1px solid;
    padding: 20px;
}

.table2,
.table3 {
    margin-left: auto;
    margin-right: auto;
    border-collapse: collapse;
    text-align: center;
    background-color: white;
}

.table2 td,
.table3 td {
    border-bottom: 2px solid rgb(184, 181, 181);
    padding: 7px 4px;
    font-size: 16px;
}

.List1 {
    text-align: center;
    padding-top: 15px;
    padding-bottom: 10px;
    margin-right: 20px;
    font-size: 22px;
}

.List2 {
    text-align: center;
    padding-top: 70px;
    padding-bottom: 10px;
    margin-right: 20px;
    font-size: 22px
}

.Check {
    margin-left: 20px;
    color: rgb(129, 124, 124);
    border-color: inherit;
    line-height: 35px;
    font-size: 18px
}

.Check li {
    width: 150px;
    padding: 0;
    margin: 10px 0px;
}

.dateBtn {
    border-radius: 4px;
    border: none;
    color: white;
    padding: 5px 10px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 13px;
    cursor: pointer;
    margin: 0px 1px;
    margin: 0px 5px;

}

.logoutbtn {
    margin-top: 170px;
    margin-left: 40px;
}

.tr1 {
    background-color: rgb(0, 153, 255);
    color: white;
}

#edge1 {
    border-top-left-radius: 8px;
}

#edge2 {
    border-top-right-radius: 8px;
}
</style>
