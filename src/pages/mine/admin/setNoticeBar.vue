<template>
    <view class="content">
        <textarea class="notice-bar-content" v-model="notice" maxlength="36"></textarea>
        <span class="left">还可以输入{{ 36 - notice.length }}个字</span>
        <button class="save" @click="saveMyNotice">保存设置</button>
    </view>
</template>

<script> 
import { saveNotice, getNotice } from '../../../api/notice'

export default {
    data() {
        return {
            notice: ''
        }
    },
    onLoad() {
        this.getOriginNotice();
    },
    methods: {
        saveMyNotice() {
            let that = this;
            saveNotice({
                content: that.notice
            }).then(res => {
                uni.showToast({
                    title: res.msg,
                    icon: 'none'
                })
            }).catch(err => {
                uni.showToast({
                    title: err.errMsg,
                    icon: 'none'
                })
            }
            )
        },
        getOriginNotice() {
            let that = this;
            getNotice().then(res => {
                if(res.code == 0) {
                    that.notice = res.data.content;
                }
                uni.showToast({
                    title: res.msg,
                    icon: 'none'
                });
            }).catch(err => {
                uni.showToast({
                    title: err.errMsg,
                    icon: 'none'
                });
            })
        }
    }
}
</script>

<style lang="scss">
    .notice-bar-content {
        width: 80%;
        height: 220rpx;
        padding: 20rpx;
        background: #EAE0E0;
        margin: 20px auto;
        border-radius: 16rpx;
    }
    .left {
        display: block;
        width: 300rpx;
        height: 60rpx;
        position: absolute;
        top: 340rpx;
        left: calc(10% - 20rpx);
        line-height: 60rpx;
        color: #928d8d;
    }
    .save {
        color: white;
        background: #CE8B8B;
        text-align: center;
        width: 180rpx;
        height: 60rpx;
        line-height: 60rpx;
        padding: 0;
        font-size: 30rpx;
        border: none;
        border-radius: 0;
        position: absolute;
        top: 340rpx;
        right: calc(10% - 20rpx);
    }
</style>