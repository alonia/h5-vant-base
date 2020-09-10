<template>
  <div class="home">
    <div class="list">
      ddd
    </div>
    <div
      class="home" 
      attr="1"
      attrs="1"
    >
      fff
    </div>
  </div>
</template>

<script>
// 使用vant 组件
import { List, NoticeBar, Cell, Notify, NavBar } from "vant";

// 使用装饰器
import { confirm } from "@/decorator";

// 使用日期工具类
import { format, DATE_FMT } from "@/utils/date";

// 接口
import { getDemoData } from "@/api/home";

export default {
    name: "Home",
    components: {
        [List.name]: List,
        [Cell.name]: Cell,
        [NavBar.name]: NavBar,
        [NoticeBar.name]: NoticeBar
    },
    data() {
        return {
            currentDate: format(new Date(), DATE_FMT)
        };
    },
    created() {},

    methods: {
    @confirm("这是通过装饰器添加的确认信息", "提示")
        $_handleUseDecorator() {
            console.log(`
        你还可以使用
        @alert 提示框
        @throttle 函数节流
        @debounce 函数防抖
        更多装饰器正在完善中
      `);
        },
        // 加载数据
        async $_loadData() {
            const loading = this.$loading();
            try {
                console.log(await getDemoData());
                Notify({
                    message: "数据加载成功",
                    type: "success"
                });
            } catch (error) {
                console.error(error);
            } finally {
                loading.close();
            }
        }
    }
};
</script>
<style lang="less" scoped>
.list {
  width: 375px;
  height: 44px;
  background: #ffffff;
}
</style>
