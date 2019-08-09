<template>
    <div>
        <div class="learningAcademyHeader">
            <div class="headerText">Learn</div>
        </div>
        <div>
            <div id="learningAcademyTabs" :class="activeIndex === 0 ? 'bottom-bar-index-0' : 'bottom-bar-index-1'">
                <div class="learningAcademyTabItem " @click="changeActive(0)" :class="activeIndex === 0 ? 'ActiveTabItem' : ''">Must-See</div>
                <div class="learningAcademyTabItem " @click="changeActive(1)" :class="activeIndex === 0 ? '' : 'ActiveTabItem'">How-To</div>

            </div>
        </div>
        <div class="howToContentList" >
            <a class="howToContentItem" @click="jumpToSecond('getStart')">
                <div class="howToContentImg">
                    <img src="../../assets/images/h5/faq/get-your-first-order.png">
                </div>
                <div class="howToContentBox">
                    <div class="howToContentText textEllipsis">
                        Getting started
                    </div>
                    <div class="howToContentSubtext textEllipsis">Get Your First Order</div>
                </div>
            </a>
            <a class="howToContentItem" @click="jumpToSecond('findMoreCustomer')">
                <div class="howToContentImg">
                    <img src="../../assets/images/h5/faq/find-more-customers.png">
                </div>
                <div class="howToContentBox">
                    <div class="howToContentText textEllipsis">
                        Find More Customers
                    </div>
                    <div class="howToContentSubtext textEllipsis">Learn to sell over social media</div>
                </div>
            </a>
            <a class="howToContentItem" @click="jumpToSecond('findProductsToShare')">
                <div class="howToContentImg">
                    <img src="../../assets/images/h5/faq/find-products-to-share.png">
                </div>
                <div class="howToContentBox">
                    <div class="howToContentText textEllipsis">
                        Find Products To Share
                    </div>
                    <div class="howToContentSubtext textEllipsis">Understand what products would sell easily</div>
                </div>
            </a>
            <a class="howToContentItem" @click="jumpToSecond('manageOrdersDelivery')">
                <div class="howToContentImg">
                    <img src="../../assets/images/h5/faq/manage-orders-and-delivery.png">
                </div>
                <div class="howToContentBox">
                    <div class="howToContentText textEllipsis">
                        Manage Orders & Delivery
                    </div>
                    <div class="howToContentSubtext textEllipsis">Everything you need to fulfill orders</div>
                </div>
            </a>
            <a class="howToContentItem" @click="jumpToSecond('makePayments')">
                <div class="howToContentImg">
                    <img src="../../assets/images/h5/faq/make-payments.png">
                </div>
                <div class="howToContentBox">
                    <div class="howToContentText textEllipsis">
                        Make Payments
                    </div>
                    <div class="howToContentSubtext textEllipsis">All about making payments</div>
                </div>
            </a>
            <a class="howToContentItem" @click="jumpToSecond('returnOrExchange')">
                <div class="howToContentImg">
                    <img src="../../assets/images/h5/faq/return-or-exchange.png">
                </div>
                <div class="howToContentBox">
                    <div class="howToContentText textEllipsis">
                        Return or Exchange
                    </div>
                    <div class="howToContentSubtext textEllipsis">Return or Exchange</div>
                </div>
            </a>
            <a class="howToContentItem" @click="jumpToSecond('trackMarginBonus')">
                <div class="howToContentImg">
                    <img src="../../assets/images/h5/faq/track-margin-and-bonus.png">
                </div>
                <div class="howToContentBox">
                    <div class="howToContentText textEllipsis">
                        Track Margin & Bonus
                    </div>
                    <div class="howToContentSubtext textEllipsis">Track Margin & Bonus</div>
                </div>
            </a>
            <a class="howToContentItem" @click="jumpToSecond('manageAccountsSettings')">
                <div class="howToContentImg">
                    <img src="../../assets/images/h5/faq/manage-accounts-and-settings.png">
                </div>
                <div class="howToContentBox">
                    <div class="howToContentText textEllipsis">
                        Manage Accounts & Settings
                    </div>
                    <div class="howToContentSubtext textEllipsis">Manage Accounts & Settings</div>
                </div>
            </a>

        </div>
    </div>
</template>

<script>
    export default {
        name: 'faq',
        data () {
          return {
              activeIndex: 0
          }
        },
        mounted() {
            console.log(111)
            let oMeta = document.createElement('meta');
            oMeta.content = 'width=device-width, initial-scale=1.0, maximum-scale=1.0,minimum-scale=1.0, user-scalable=0';
            oMeta.name = 'viewport';
            document.getElementsByTagName('head')[0].appendChild(oMeta);
            document.title = 'FAQ'
        },
        methods: {
            jumpToSecond (name) {
                this.$router.push({name: 'How-to',params: {name: name}})
            },
            changeActive (value) {
                this.activeIndex = value
            }
        }
    }
</script>

<style lang="scss" scoped>
    .learningAcademyHeader{
        padding: 16px;
        position: fixed;
        background-color: #fff;
        top: 0;
        left: 50%;
        z-index: 2;
        transform: translateX(-50%);
        -webkit-transform: translateX(-50%);
        -moz-transform: translateX(-50%);
        -ms-transform: translateX(-50%);
        -o-transform: translateX(-50%);
        max-width: 600px;
        width: 100%;
        .headerText{
            font-size: 16px;
            line-height: 1.5;
            display: inline-block;
            color: #333;
        }
    }
    #learningAcademyTabs{
        position: fixed;
        top: 56px;
        left: 50%;
        display: flex;
        box-shadow: 0 2px 4px 0 rgba(0,0,0,.1);
        z-index: 1;
        cursor: pointer;
        background-color: #fff;
        transform: translateX(-50%);
        -webkit-transform: translateX(-50%);
        -moz-transform: translateX(-50%);
        -ms-transform: translateX(-50%);
        -o-transform: translateX(-50%);
        max-width: 600px;
        width: 100%;
        .learningAcademyTabItem{
            font-size: 14px;
            line-height: 16px;
            color: #999;
            display: inline-block;
            padding: 16px;
            width: 50%;
            text-align: center;
        }

        .ActiveTabItem{
            color: #333;
        }
    }
    #learningAcademyTabs:after{
        width: 50%;
        content: "";
        clear: both;
        bottom: 0;
        display: block;
        background-color: #fe4d9b;
        height: 2px;
        position: absolute;
        transition: left .4s cubic-bezier(.23,1,.32,1);
        /*margin: 0 15px;*/
    }
    .bottom-bar-index-0:after{
        left: 0%;
    }
    .bottom-bar-index-1:after{
        left: 50%;
    }

    .howToContentList{
    margin-top: 60px;
    /*padding-bottom: 10px;*/
    .howToContentItem{
        background-color: #fff;
        margin-bottom: 16px;
        padding: 16px;
        display: block;
        position: relative;
        box-shadow: 0 0 4px 0 rgba(0,0,0,.05);
        text-decoration: none!important;
        color: #337ab7;
        cursor: pointer;
        .howToContentImg{
            position: absolute;
            top: 16px;
            left: 16px;
            img{
                width: 48px;
                margin-right: 24px;
                max-width: 100%;
                vertical-align: middle;
                display: inline-block;
            }
        }
        .howToContentBox{
            display: block;
            padding-left: 72px;
            .textEllipsis{
                white-space: nowrap;
                overflow: hidden;
                text-overflow: ellipsis;
            }
            .howToContentText{
                font-size: 14px;
                line-height: 24px;
                color: #333;
            }
            .howToContentSubtext{
                font-size: 12px;
                line-height: 1.33;
                color: #999;
                margin-top: 4px;
            }
        }
    }
}

</style>