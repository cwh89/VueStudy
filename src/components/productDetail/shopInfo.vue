<template>
    <div class="shop-info">
        <div class="shop-infoBox">
            <div class="shop-title"><h2>신세계몰</h2></div>
        </div>
        <div class="shop-bestItem">
            <div class="bestItemMore">
                <span style="margin-right: 10px"
                    >이 판매자의 인기상품이에요</span
                >
                <button class="showMore">더 보기</button>
            </div>
            <div class="bestPicDiv" >
                <div class="bestPic" v-for="(best, idx) in bests" :key="idx">
                    <img
                        :src="
                            require(`@/components/productDetail/image/${best.image}`)
                        "
                        style="width: 140px; height: 140px"
                    />
                </div>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    data() {
        return {
            bests: [
                {
                    image: "best01.jpg",
                },
                {
                    image: "best02.jpg",
                },
                {
                    image: "best03.jpg",
                },
                {
                    image: "best04.jpg",
                },
                {
                    image: "best05.jpg",
                },
                {
                    image: "best06.jpg",
                },
            ],
        };
    },
};
</script>
       
<style scoped>
.shop-info {
    width: 100%;
    height: 210px;
    border: 1px rgb(197, 195, 195) solid;
    overflow: hidden;
    margin: 0 0 5px 0;
    background-color: #fafafa;
}

.shop-infoBox {
    float: left;
    position: relative;
    width: 16%;
    height: 100%;
    padding: auto;
}

.shop-title {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    font-size: 150%;
}

.shop-bestItem {
    float: right;
    width: 83%;
    height: 100%;
    padding: 0px 0px;
    border-left: 1px rgb(197, 195, 195) solid;
}

.bestItemMore {
    padding: 10px 10px 5px 10px;
    border-bottom: 1px rgb(197, 195, 195) solid;
}
.bestPicDiv {
    height: 162px;
    text-align: center;
    display: flex;
    padding: 10px 10px;
}

.bestPic {
    height: 140px;
    width: 140px;
    margin: 0px 20px 0 20px;
    border-radius: 4px;
    overflow: hidden;
}
.bestImg {
    height: 140px;
    width: 140px;
}
.showMore {
    height: 30px;
    padding: 5px 10px;
}
</style>
