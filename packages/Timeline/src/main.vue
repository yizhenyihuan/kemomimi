<template>
    <div style="text-align: left">
        <el-timeline
                v-if="activities.length>0"
                :reverse="reverse"
        >
            <el-timeline-item
                    v-for="(activity, index) in activities"
                    :key="index"
                    v-bind="activity"
                    :timestamp="activity.timestamp"
            >
                <render-content
                        :key="index"
                        :render="activity.render"
                        :activity="activity"
                ></render-content>
            </el-timeline-item>
        </el-timeline>
        <div v-else>
            暂无记录
        </div>
    </div>
</template>

<script lang="jsx">
// 表格字段格式化
const RenderContent = {
    props: {
        render: Function,
        activity: Object,

    },
    render (h) {
        const { content } = this.activity
        const params = {
            activity:this.activity,
        }

        if (this.render) {
            return this.render(h, params)
        }

        return <span>{content}</span>
    }
}
export default {
    name: 'KemTimeline',
    components:{
        RenderContent
    },
    props: {
        activities: {
            type: Array,
            required:true
        },
        reverse: {
            type: Boolean,
            default:true
        }
    },
 }
</script>

<style scoped>

</style>
