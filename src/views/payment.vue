<template>
    <div class="payment">
        <div class="orderProduct">
            <h2>주문 상품 정보</h2>
            <table class="orderProductTable">
                <tr v-for="(op, idx) in getOrderList" :key="idx">
                    <td class="orderProductTd" style="width: 10%">
                        <h3 v-html="op.seller"></h3>
                    </td>
                    <td class="orderProductTd" style="width: 10%">
                        <img
                            class="orderProductImg"
                            :src="
                                require(`@/components/productDetail/image/${op.img}`)
                            "
                            alt="productImage"
                        />
                    </td>
                    <td
                        class="orderProductTd"
                        style="width: 50%; text-align: left"
                    >
                        <p v-html="op.title"></p>
                        <p v-html="op.name"></p>
                        <p>
                            <span>옵션 : </span><span v-html="op.size"></span>
                        </p>
                    </td>
                    <td class="orderProductTd" style="width: 10%">
                        <span v-html="AddComma(op.amount)"></span
                        ><span>개</span>
                    </td>
                    <td class="orderProductTd" style="width: 10%">
                        <span v-html="AddComma(op.price)"></span><span>원</span>
                    </td>
                    <td class="orderProductTd" style="width: 10%">
                        <span v-html="AddComma(op.delivery_fee)"></span
                        ><span v-if="op.delivery_fee > 0">원</span>
                    </td>
                </tr>
            </table>
        </div>
        <div class="coupon">
            <h2>할인/포인트</h2>
            <table class="couponTable">
                <tr>
                    <td><span>쿠폰 할인</span></td>
                    <td class="couponNum">{{ AddComma(coupon) }}원</td>
                    <td>
                        <button class="couponBtn" @click="applyCoupon()">
                            쿠폰 변경
                        </button>
                    </td>
                </tr>
                <tr>
                    <td class="tableMiddle">1</td>
                </tr>
                <tr>
                    <td><span>포인트</span></td>
                    <td class="couponNum">{{ AddComma(point) }}원</td>
                    <td>
                        <input
                            id="pointInput"
                            type="text"
                            style="width: 100%"
                        />
                    </td>
                    <td>
                        <button class="couponBtn" @click="applyPoint()">
                            사용
                        </button>
                    </td>
                    <td style="width: 200px">
                        사용 가능 포인트 : {{ AddComma(usable) }}원
                    </td>
                </tr>
            </table>
        </div>
        <div class="delivery">
            <h2 style="margin: 20px 0 0 -10px">배송지 입력</h2>
            <p>
                <span style="margin-right: 28px">이름</span>
                <span>
                    <input
                        type="text"
                        id="username"
                        class="shortInput inputValues"
                        name="이름"
                    />
                </span>
            </p>
            <p>
                <span>전화번호</span>
                <span>
                    <input
                        type="text"
                        class="shortInput inputValues"
                        placeholder="-없이 숫자만"
                        id="mobile"
                        name="전화번호"
                        @keyup="phoneCheck()"
                    />
                </span>
                <span>
                    <span class="validate" v-if="!phoneValidate"
                        >- 없이 숫자만 입력해주세요</span
                    >
                </span>
            </p>
            <p>
                <span>우편번호</span>
                <span>
                    <input
                        class="shortInput inputValues"
                        type="text"
                        v-model="postcode"
                        placeholder="우편번호"
                        name="우편번호"
                    />
                    <span>
                        <button class="addrBtn" @click="execDaumPostcode()">
                            검색
                        </button>
                    </span>
                </span>
            </p>
            <p>
                <span>기본주소</span>
                <span colspan="2">
                    <input
                        type="text"
                        class="longInput inputValues"
                        id="address"
                        v-model="address"
                        placeholder="주소"
                        name="주소"
                    />
                </span>
            </p>
            <p>
                <span>상세주소</span>
                <span colspan="2">
                    <input
                        type="text"
                        class="longInput inputValues"
                        id="detailAddress"
                        placeholder="상세주소"
                        name="상세주소"
                    />
                </span>
            </p>
        </div>

        <div class="payMethod">
            <h2 style="margin: 20px 0 0 -10px">결제수단 선택</h2>
            <p>
                <input
                    type="radio"
                    value="credit"
                    v-model="radioPay"
                    name="payMethodRadio"
                    id="payMethodRadio"
                    style="width: auto"
                />신용카드
                <input
                    type="radio"
                    value="cash"
                    v-model="radioPay"
                    name="payMethodRadio"
                    id="payMethodRadio"
                    style="width: auto; margin-left: 30px"
                />무통장 입금
                <input
                    type="radio"
                    value="phone"
                    v-model="radioPay"
                    name="payMethodRadio"
                    id="payMethodRadio"
                    style="width: auto; margin-left: 30px"
                />휴대폰 결제
            </p>
            <div v-if="radioPay === 'credit'">
                <select class="creditPay">
                    <option value="선택">선택</option>
                    <option value="">신한카드</option>
                    <option value="">국민카드</option>
                    <option value="">삼성카드</option>
                    <option value="">현대카드</option>
                    <option value="">롯데카드</option>
                    <option value="">농협카드</option>
                    <option value="">우리카드</option>
                    <option value="">하나카드</option>
                </select>
            </div>
            <div v-if="radioPay === 'cash'">
                <select class="cashPay">
                    <option value="선택">선택</option>
                    <option value="">신한은행</option>
                    <option value="">국민은행</option>
                    <option value="">우리은행</option>
                    <option value="">카카오뱅크</option>
                </select>
            </div>
            <div v-if="radioPay === 'phone'"></div>
        </div>
        <div class="payInfo">
            <h2>최종 결제 정보</h2>
            <table class="payInfoTable">
                <tr>
                    <td
                        class="payIf"
                        style="border-top: 1px solid rgb(197, 195, 195)"
                    >
                        상품금액
                    </td>
                    <td
                        class="payNum"
                        style="border-top: 1px solid rgb(197, 195, 195)"
                    >
                        {{ AddComma(totalPrice) }}원
                    </td>
                    <td rowspan="4" class="buyBtnTd">
                        <button class="buyBtn" @click="payCheck()">
                            결제하기
                        </button>
                    </td>
                </tr>
                <tr>
                    <td class="payIf">할인금액</td>
                    <td class="payNum">{{ AddComma(sale) }}원</td>
                </tr>
                <tr>
                    <td class="payIf">배송비</td>
                    <td class="payNum">{{ AddComma(delivery) }}원</td>
                </tr>
                <tr style="border-top: 2px rgb(197, 195, 195) solid">
                    <td
                        class="payIf"
                        style="border-bottom: 1px solid rgb(197, 195, 195)"
                    >
                        결제 금액
                    </td>
                    <td
                        class="payNum"
                        style="border-bottom: 1px solid rgb(197, 195, 195)"
                    >
                        {{ AddComma(finalPrice) }}원
                    </td>
                </tr>
            </table>
        </div>
    </div>
</template>

<script>
import { createNamespacedHelpers } from "vuex";
const orderList = createNamespacedHelpers("orderList");
export default {
    data() {
        return {
            point: 0,
            totalPrice: 0,
            coupon: 0,
            sale: 0,
            finalPrice: 110500,
            radioPay: "",
            delivery: 2500,
            phoneValidate: true,
            usable: 3548,
            open: false,
            postcode: "",
            address: "",
            extraAddress: "",
        };
    },
    methods: {
        applyPoint() {
            let pt = document.getElementById("pointInput").value;
            if (pt === "") {
                alert("숫자를 입력해주세요");
            } else if (pt > parseInt(this.usable) + parseInt(this.point)) {
                alert("포인트가 부족합니다.");
            } else {
                this.sale -= parseInt(this.point);
                this.usable = this.usable - pt + parseInt(this.point);
                this.point = pt;
                this.sale += parseInt(this.point);
                this.finalPrice = this.totalPrice - this.sale + this.delivery;
            }
        },
        applyCoupon() {
            this.sale -= parseInt(this.coupon);
            this.coupon = this.totalPrice * 0.1;
            this.sale += parseInt(this.coupon);
            this.finalPrice = this.totalPrice - this.sale + this.delivery;
        },
        phoneCheck() {
            let mobile = document.getElementById("mobile").value;
            if (
                /^(01[016789]{1}|02|0[3-9]{1}[0-9]{1})[0-9]{3,4}[0-9]{4}$/.test(
                    mobile
                )
            ) {
                this.phoneValidate = true;
            } else {
                this.phoneValidate = false;
            }
        },
        execDaumPostcode() {
            new window.daum.Postcode({
                oncomplete: (data) => {
                    if (this.extraAddress !== "") {
                        this.extraAddress = "";
                    }
                    if (data.userSelectedType === "R") {
                        // 사용자가 도로명 주소를 선택했을 경우
                        this.address = data.roadAddress;
                    } else {
                        // 사용자가 지번 주소를 선택했을 경우(J)
                        this.address = data.jibunAddress;
                    }

                    // 사용자가 선택한 주소가 도로명 타입일때 참고항목을 조합한다.
                    if (data.userSelectedType === "R") {
                        // 법정동명이 있을 경우 추가한다. (법정리는 제외)
                        // 법정동의 경우 마지막 문자가 "동/로/가"로 끝난다.
                        if (
                            data.bname !== "" &&
                            /[동|로|가]$/g.test(data.bname)
                        ) {
                            this.extraAddress += data.bname;
                        }
                        // 건물명이 있고, 공동주택일 경우 추가한다.
                        if (
                            data.buildingName !== "" &&
                            data.apartment === "Y"
                        ) {
                            this.extraAddress +=
                                this.extraAddress !== ""
                                    ? `, ${data.buildingName}`
                                    : data.buildingName;
                        }
                        // 표시할 참고항목이 있을 경우, 괄호까지 추가한 최종 문자열을 만든다.
                        if (this.extraAddress !== "") {
                            this.extraAddress = `(${this.extraAddress})`;
                        }
                    } else {
                        this.extraAddress = "";
                    }
                    // 우편번호를 입력한다.
                    this.postcode = data.zonecode;
                },
            }).open();
        },
        AddComma(num) {
            var regexp = /\B(?=(\d{3})+(?!\d))/g;
            return num.toString().replace(regexp, ",");
        },
        payCheck() {
            const checked = document.getElementsByClassName("inputValues");
            for (var i = 0; i < checked.length; i++) {
                if (checked[i].value.length == 0) {
                    alert(`${checked[i].name}을/를 입력하세요`);
                    checked[i].focus();
                    return;
                }
            }

            const radioCheck = document.querySelector(
                'input[name = "payMethodRadio"]:checked'
            );
            if (radioCheck == null) {
                alert("결제수단을 선택해주세요");
                radioCheck.focus();
                return;
            }

            if (!this.phoneValidate) {
                alert("전화번호를 확인하세요");
                return;
            } else {
                alert("결제를 완료했습니다");
            }
        },
    },
    computed: {
        ...orderList.mapGetters(["getOrderList"]),
    },
    mounted() {
        {
            for (let i = 0; i < this.getOrderList.length; i++) {
                this.totalPrice += this.getOrderList[i].price;
                this.sale += this.getOrderList[i].price * 0.1;
            }
        }
    },
};
</script>

<style scoped>
.payment {
    padding: 20px 10px;
    background-color: #fafafa;
}

.orderProduct,
.coupon,
.delivery,
.payMethod {
    border-bottom: 1px solid rgb(197, 195, 195);
}

.orderProductTable {
    width: 100%;
    border-collapse: collapse;
    padding: 10px 10px;
    text-align: center;
    margin: 10px 0;
}

.orderProductTd {
    border: 1px rgb(197, 195, 195) solid;
    padding: 5px 5px;
}

.orderProductImg {
    height: 140px;
}

.payInfoTable {
    width: 100%;
    border-collapse: collapse;
    padding: 10px 10px;
    text-align: center;
}

.payIf {
    width: 25%;
    text-align: left;
    padding: 5px 20px;
    border-left: 1px solid rgb(197, 195, 195);
}

.payNum {
    width: 25%;
    text-align: right;
    padding: 5px 20px;
    border-right: 1px solid rgb(197, 195, 195);
}

.couponTable {
    width: 850px;
    border-collapse: collapse;
    padding: 10px 30px;
}

td {
    padding: 3px 10px;
}

.buyBtnTd {
    width: 50%;
    border: 0px;
}

.buyBtn {
    width: 200px;
    font-size: 150%;
}

.addrBtn {
    font-size: 15px;
    padding: 0 5px;
    width: 50px;
    margin: 0 10px;
}

.delivery,
.payMethod {
    padding: 0 10px;
}

.payMethod {
    height: 140px;
}

.shortInput {
    width: 250px;
    margin-left: 10px;
}

.longInput {
    width: 500px;
    margin-left: 10px;
}

.cardSelect {
    margin: 0 10px;
    width: 10%;
}

.couponSpan {
    margin: 0 20px;
}

.couponBtn {
    width: 100px;
    font-size: 17px;
    padding: 2px 5px;
}

.tableMiddle {
    font-size: 4px;
    padding: 0 0;
    color: white;
}

.couponNum {
    width: 20%;
    text-align: right;
    padding: 5px 20px;
}

.creditPay,
.cashPay {
    min-width: 125px;
    font-size: 16px;
    border: 2px solid rgb(0, 153, 255);
    border-radius: 4px;
}

#pointInput,
.shortInput,
.longInput {
    font-size: 16px;
}

.validate {
    margin-left: 10px;
    color: red;
}
</style>
