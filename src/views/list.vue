<template>
<div>
    <span class='span1'> 인기상품 </span>
    <div class="products">
        <a href="#">
            <img src="@/components/mainPage/productTableImage/1.jpg">
            <p>선글라스</p>
            <p class="price">49,000</p>
        </a>
        <a href="#">
             <img src="@/components/mainPage/productTableImage/1.jpg">
            <p>구두</p>
            <p class="price">89,000</p>
        </a>
        <a href="#">
      <img src="@/components/mainPage/productTableImage/1.jpg">
            <p>가방</p>
            <p class="price">69,000</p>
        </a>
    </div>
    <span class="span1"> 관련상품</span>
    <div class="products1">
        <ul>
            <li class="item">
                <a href="#">
            <img src="@/components/mainPage/productTableImage/1.jpg">
                </a>
                <span class="name"> 상품명:<br>운동화</span>
                <span class="price"> 가격: <br>79,000</span>
                <span class="vendor">판매처:<br>홈쇼핑</span>
            </li>
            <li class="item">
                <a href="#">
                    <img src="@/components/mainPage/productTableImage/1.jpg">
                </a>
                <span class="name"> 상품명:<br>로퍼</span>
                <span class="price"> 가격: <br>99,000</span>
                <span class="vendor">판매처:<br>백화점</span>
            </li>
            <li class="item">
                <a href="#">
                       <img src="@/components/mainPage/productTableImage/1.jpg">
                </a>
                <span class="name"> 상품명:<br>손목시계</span>
                <span class="price"> 가격: <br>109,000</span>
                <span class="vendor">판매처:<br>아울렛</span>
            </li>
        </ul>
    </div>

    <div class="container">
        <div class="aside_info">
            <span>가격비교</span>
            <ul class="buy">
                <li>숙박대전</li>
                <li>배송선물</li>
                <li>희망쇼핑</li>
                <li>할인금액</li>
            </ul>
            <span>사이즈</span>
            <ul class="size">
                <li>130~140이상</li>
                <li>145~155이상</li>
                <li>160~170이상</li>
                <li>175이상</li>
            </ul>
            <span>색상</span>
            <ul class="color">
                <li>흰색</li>
                <li>검은색</li>
                <li>빨간색</li>
                <li>파란색</li>
            </ul>
            <span>판매처</span>
            <ul class="aside_vender">
                <li>백화점</li>
                <li>인터넷쇼핑몰</li>
                <li>홈쇼핑</li>
                <li>아울렛</li>
            </ul>
            <span>배송혜택</span>
            <ul class="aside_delivery">
                <li>무료배송</li>
                <li>오늘발송</li>
                <li>반품배송비 지원</li>
                <li>무료선물포장</li>
            </ul>
        </div>
    </div>

    <div class="clearfix"></div>
</div>
</template>

<script>
export default {

}
</script>

<style scoped>

</style>
