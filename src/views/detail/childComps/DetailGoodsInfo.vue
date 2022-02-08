<template>
<div v-if="Object.keys(detailInfo).length !== 0" class="goods-info">
    <div class="info-desc clear-fix">
        <div class="start">
        </div>
        <div class="desc">{{detailInfo.desc}}</div>
        <div class="end"></div>
    </div>
    <div class="info-key">{{detailInfo.detailImage[0].key}}</div>
    <div class="info-list">
        <img v-for="(item, index) in detailInfo.detailImage[0].list" :key="index"
        :src="item" @load="imgLoad" alt="">
    </div>
</div>
  
</template>

<script>
export default {
    name: "DetailGoodsInfo",
    props: {
        detailInfo: {
            type: Object,
            default() {
                return {}
            }
        }
    },
    data() {
        return {
            counter: 0,
            imagesLength: 0
        }
    },
    methods: {
        imgLoad() {
            if (++this.counter === this.imagesLength) {
                this.$emit('imagetLoad')
            }
        }
    },
    watch: {
        detailInfo() {
            this.imagesLength = this.detailInfo.detailImage[0].list.imagesLength

        }
    }

}
</script>

<style scoped>
.good-info {
    padding: 30px 8px 0;
    border-bottom: solid 4px rgba(100, 100, 100, .1);
}

.info-desc {
    padding: 0 8px 0;
    font-size: 14px;
}

.info-desc .desc {
    text-indent: 2em;
}

.info-desc .desc {
    text-indent: 2em;
}
.info-key {
    padding: 8px;
}
.info-list img {
    width: 100%;
}

</style>