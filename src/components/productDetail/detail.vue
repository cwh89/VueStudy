<template>
<div>
    <div class="tabs">
        <TabItem v-for="item in list" v-bind="item" :key="item.id" v-model="currentId" class="tabTop" />
    </div>
    <div class="contents">
        <transition>
            <section class="item" :key="currentId">
                <div v-if="currentId === 1">
                    <img :src="
                                require(`@/components/productDetail/image/${current.content}`)
                            "
                            style="margin: 0 auto"
                        />
                    </div>
                    <div v-else-if="currentId === 2">
                        <review></review>
                    </div>
                    <div v-else-if="currentId === 3">
                        <qna></qna>
                    </div>
                </section>
            </transition>
        </div>
        <div class="tabs">
            <TabItem
                v-for="item in list"
                v-bind="item"
                :key="item.id"
                v-model="currentId"
                class="tabBottom"
            />
        </div>
    </div>
</template>

<script>
import TabItem from "./TabItem.vue";
import review from "./review.vue";
import qna from "./qna.vue";
export default {
    components: {
        TabItem,
        review,
        qna,
    },
    data() {
        return {
            currentId: 1,
            list: [
                {
                    id: 1,
                    label: "상품 상세 정보",
                    content: "productDetail01.jpg",
                },
                {
                    id: 2,
                    label: "상품 리뷰",
                    content: review,
                },
                {
                    id: 3,
                    label: "상품 문의",
                    content: qna,
                },
            ],
        };
    },
    computed: {
        current() {
            return this.list.find((el) => el.id === this.currentId) || {};
        },
    },
};
</script>

<style scoped>
.tabs {
    width: 200%;
}

.tabTop {
    border-top-left-radius: 4px;
    border-top-right-radius: 4px;
}

.tabBottom {
    border-top-left-radius: 0;
    border-top-right-radius: 0;
    border-bottom-left-radius: 4px;
    border-bottom-right-radius: 4px;
}

.contents {
    position: relative;
    width: 100%;
    border: 1px solid rgb(0, 153, 255);
    margin-left: 1px;
    overflow-y: auto;
    overflow-x: hidden;
    max-height: 1600px;
}

.item {
    box-sizing: border-box;
    padding: 10px;
    width: 100%;
    /* transition: all 0.8s ease; */
}

/* 트랜지션 전용 스타일 */
.v-leave-active {
    position: absolute;
}

.v-enter {
    transform: translateX(-100%);
}

.v-leave-to {
    transform: translateX(100%);
}

img {
    width: 80%;
    display: block;
    margin: 0px auto;
}
</style>
