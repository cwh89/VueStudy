<template>
<div>
    <!--top-->
    <div class="top" style="text-align:center">
        <h1>마이페이지</h1>
    </div>
    <div class="container" name="login_member" preva>
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
            <!-- <router-link v-bind:to="'/'"> <button class="logoutbtn">로그아웃</button></router-link> -->
        </div>
        <!--right-->
        <div class="right">
            <div class="pList1">
                <h2>회원 정보 열람</h2>
            </div>
            <div class="tempDiv">
               <label class="labelClass" for="">닉네임</label>
                    <input type="text" class="mdText"  v-model="putnick">
                    <button class="classBtn" @click="nickMod"> 수정하기 </button>  
            </div>
            <div class="tempDiv">
                <label class="labelClass" for="">비밀번호</label>
                    <input v-model="signup.password" type="password" class="mdText"  @keyup="passwordValid">
                    <div v-if="!passwordValidFlag" class="pwFlag"> 유효하지 않은 비밀번호 입니다. </div>
                <br>
            </div>
            <div class="tempDiv">
                <label class="labelClass" for="">비밀번호확인</label>
                <input v-model="passwordCheck" type="password" name="비밀번호 확인" class="mdText"  @keyup="passwordCheckValid">
                <button class="classBtn" @click="pwMod"> 수정하기 </button>
                <div v-if="!passwordCheckFlag" class="re_pwFlag"> 비밀번호가 동일하지 않습니다. </div>
     
            </div>
            <div class="tempDiv">
                <label class="labelClass" for="">전화번호</label>
                    <input v-model="putNum" type="text" class="mdText"  @keyup="numValid" placeholder="- 없이 숫자만" maxlength="11">
                    <button class="classBtn" @click="numMod"> 수정하기 </button>
                    <div v-if="!numValidFlag" class="numFlag"> 유효하지 않은 전화번호 입니다. </div>
            </div>
            <div class="tempDiv">
                <label class="labelClass" for="">*우편번호</label>

                <input type="text" class="mdText" v-model="postcode" placeholder="우편번호">
                <span>
                    <button type="button" class="classBtn" @click="execDaumPostcode()">주소검색</button>
                </span>
         
                <!-- <input type="text" name="total_add" class="total_add"> -->

            </div>
            <div class="tempDiv">
                <label class="labelClass" for="">*주소</label>
                       <input type="text" class="mdText" id="address" v-model="address" placeholder="주소">

            </div>
            <div class="tempDiv">
                <label class="labelClass" for="">*상세주소</label>
                <input type="text" class="mdText" id="detailAddress" placeholder="상세주소">
            </div>
            <div class="content1">
                <router-link v-bind:to="'/'"> <button class="quit" @click="quitBtn">회원탈퇴</button></router-link>
            </div>
        </div>
    </div>
</div>
</template>

<script>
export default {
    data() {
        return {
            postcode: "",
            address: "",
            extraAddress: "",
            signup: {
                password: null,
                pwhint: '',
                pwhintans: null,
                putNum: null,
            },
            passwordValidFlag: true,
            passwordCheck: '',
            passwordCheckFlag: true,
            numValidFlag: true,
            putNum: '',
            putnick: '',
            msg: '',
        }
    },
    methods: {
        nickMod() {
            try {
                if ("" === this.putnick) {
                    alert("공백 입니다.");
                } else if ("asd" === this.putnick) {
                    alert("이미 가입된 닉네임 입니다.");
                } else {
                    alert("수정 되었습니다.");
                }
            } catch (err) {
                this.msg = "error";
            }
        },
        passwordValid() {
            if (/^(?=.*[a-z])(?=.*[A-Z])(?=.*[0-9]).{8,16}$/.test(this.signup.password)) {
                this.passwordValidFlag = true
            } else {
                this.passwordValidFlag = false
            }

        },
        passwordCheckValid() {
            if (this.signup.password === this.passwordCheck) {
                this.passwordCheckFlag = true;
                this.checkRePwdFlag = true;
            } else {
                this.passwordCheckFlag = false;
                this.checkRePwdFlag = false;
            }
        },
        pwMod() {
            try {
                if ("" === this.signup.password) {
                    alert("공백 입니다.");
                } else if (/^(?=.*[a-z])(?=.*[A-Z])(?=.*[0-9]).{8,16}$/.test(this.signup.password)) {
                    if (this.passwordValidFlag == true)
                    if (this.signup.password === this.passwordCheck)
                        alert("수정되었습니다.");
                } else {
                    if (!this.passwordValidFlag == true)
                        alert("비밀번호 형식은 대문자,소문자,숫자 포함 8~16글자 입니다.");
                }
            } catch (err) {
                this.msg = "error";
            }
        },
        numValid() {
            if (/^(01[016789]{1}|02|0[3-9]{1}[0-9]{1})-?[0-9]{3,4}-?[0-9]{4}$/.test(this.putNum)) {
                this.numValidFlag = true
            } else {
                this.numValidFlag = false
            }

        },
        numMod() {
            try {
                if ("" === this.putNum) {
                    alert("공백 입니다.");
                } else if (/^(01[016789]{1}|02|0[3-9]{1}[0-9]{1})-?[0-9]{3,4}-?[0-9]{4}$/.test(this.putNum)) {
                    alert("수정 되었습니다.");
                } else {
                    alert("제대로 입력해주세요.")
                }
            } catch (err) {
                this.msg = "error";
            }
        },
        quitBtn() {
            alert("정말 탈퇴하시겠습니까?")
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
                        if (data.bname !== "" && /[동|로|가]$/g.test(data.bname)) {
                            this.extraAddress += data.bname;
                        }
                        // 건물명이 있고, 공동주택일 경우 추가한다.
                        if (data.buildingName !== "" && data.apartment === "Y") {
                            this.extraAddress +=
                                this.extraAddress !== "" ?
                                `, ${data.buildingName}` :
                                data.buildingName;
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

.top {
    margin-left: 70px;
}

.container {
    display: flex;
}

.left {
    display: inline-block;
    height: 887px;
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
    width: 1100px;
    border: 1px solid rgb(197, 195, 195);
    margin-left: 50px;
    background-color: #fafafa;
    border-radius: 4px;
}

.right>div:not(.content1){
    border-bottom: 1px solid rgb(197, 195, 195);
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

.check li {
    width: 150px;
    padding: 0;
    margin: 10px 0px;
}

.pList1 {
    text-align: center;
    border-bottom: 1px solid black;
}

.content {
    padding: 10px;
}

.content>h3 {
    margin-left: 150px;
}

.mdText {
    width: 350px;
    height: 30px;
    margin-right: 30px;
    border-radius: 4px;
    border: 1px solid;
    text-align: center;
    font-size: 16px;
}

.mdBtn {
    margin-left: 20px;
}

.logoutbtn {
    margin-top: 100px;
    margin-left: 45px;
}

.quit {
    width: 130px;
    height: 65px;
    margin-left: 450px;
    margin-bottom: 30px;
    background-color: #00ba54;
}

.pwFlag,
.re_pwFlag,
.numFlag {
    color: red;
    margin-left: 20px;
}

.tempDiv {
    display: flex;
    margin: 40px 0 40px 0;
}
.labelClass {
    margin-left: 150px;
    padding-bottom: 40px;
    min-width: 120px;
    font-weight: bold;
}

.classBtn {
    width: 100px;
    height: 30px;
    margin-left: 10px;
    padding: 0;
}
</style>
