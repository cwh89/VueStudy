<template>
<div class="main">
    <div class="banner">
        <!-- <img src="http://placehold.it/1920x500" alt="banner" style="cursor:
            pointer"/> -->
        <!-- <img src="https://picsum.photos/1900/00" alt="banner" style="cursor:
            pointer"/> -->
        <bannerImage />
    </div>
    <div></div>
    <div>
        <h1>추천상품</h1>
        <div class="imageArea" v-for="n in length" v-bind:key="n">
            <ul>
                <li class="card_image" v-for='j in 4' :key="j">
                    <div class="imageDiv">
                        <!-- <a v-bind:href="images[0].link"><img :src="getImage(images[0].image)"
                            alt="productImage"></a> -->
                        <a v-bind:href="images[(j-1)+(n-1)*4].link">
                            <img :src="require(`@/components/mainPage/productTableImage/${images[(j-1)+(n-1)*4].image}`)" alt="productImage"></a>
                    </div>
                    <div class="imageTitle">
                        <a v-bind:href="images[(j-1)+(n-1)*4].link">
                            <temp class="temp"><label for="">{{images[(j-1)+(n-1)*4].name}}</label></temp>
                            <h3 for="">{{AddComma(images[(j-1)+(n-1)*4].price) }}원</h3>
                        </a>
                    </div>
                </li>
            </ul>
        </div>
        <div class="moreImageDiv">
            <button v-on:click="moreImage" class="moreImageBtn">더 보기</button>
        </div>
    </div>
</div>
</template>

<script>
import imageJson from './image.json'
import bannerImage from '@/components/mainPage/mainPageBanner.vue'
export default {
    data() {
        return {
            length: 3,
            imageLength: imageJson.length / 4,
            images: imageJson
        }
    },
    components: {
        bannerImage
    },
    methods: {
        moreImage() {
            // console.log(this.length, this.imageLength);
            if (this.length < this.imageLength) {
                if (this.imageLength - this.length == 1)
                    return this.length++;
                return this.length += 2;
            } else
                return this.length;

        },
        AddComma(num) {
            let regexp = /\B(?=(\d{3})+(?!\d))/g;
            return num.toString().replace(regexp, ",");
        },
    },

}
</script>

<style scoped>
.main {
    /* border: 1px solid black; */
}

.banner img {
    max-width: 100%;
    height: auto;
}

h2 {
    text-align: left;
    margin: 0 0 0 10px;
    padding: 0;
    margin-bottom: 20px;
}

ul {
    list-style: none;
    display: flex;
    margin: 10;
    padding: 0;
}

.card_image {
    margin-left: auto;
    margin-right: auto;
    border: 1px solid rgb(197, 195, 195);
    border-radius: 4px;
}

.card_image>.imageDiv {
    width: 300px;
    height: 300px;
    /* border: black 1px solid; */
    overflow: hidden;
    /* margin: 0 auto; */
    margin-top: 0px;
    margin-bottom: 0px;
    border-radius: 4px 4px 0 0;
}

.imageDiv img {
    width: 100%;
    height: 100%;

    object-fit: cover;
}

.card_image>.imageTitle {
    display: block;
    text-align: left;
    width: 290px;
    /* border: black 1px solid; */
    overflow: hidden;
    /* margin: 0 auto; */
    margin-top: 0px;
    margin-bottom: 0px;
    background-color: #fafafa;
    border-radius: 0 0 4px 4px;
    padding-top: 5px;
    padding-left: 10px;
}

.imageTitle a:link {
    color: rgb(78, 76, 76);
    text-decoration: none;
}

.imageTitle a:hover {
    color: rgb(78, 76, 76);
    text-decoration: none;
}

.imageTitle a:visited {
    color: rgb(78, 76, 76);
    text-decoration: none;
}

.imageTitle a {
    font-weight: none;
    color: rgb(78, 76, 76);
}

.moreImageDiv {
    text-align: center;
}

label {
    font-weight: 600;
}

.temp {
    height: 48px;
    display: block;
}

h1 {
    text-align: left;
    background-color: #fafafa;
    padding: 10px;
    border: 1px solid rgb(197, 195, 195);
    border-radius: 4px;
    color: rgb(78, 76, 76);
}

/*  */
</style>
