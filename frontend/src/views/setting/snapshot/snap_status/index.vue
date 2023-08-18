<template>
    <el-dialog v-model="dialogVisiable" :destroy-on-close="true" :close-on-click-modal="false" width="50%">
        <template #header>
            <div class="card-header">
                <span>快照状态</span>
            </div>
        </template>
        <div style="height: 300px">
            <el-alert show-icon title="备份 1Panel 服务" type="success" :closable="false" />
            <el-alert show-icon title="备份 1Panel 脚本" type="error" close-text="重试" />
            <el-alert show-icon title="备份 1Panel 二进制" type="success" :closable="false" />
            <el-alert show-icon title="备份 Docker 配置" type="success" :closable="false" />
            <el-alert show-icon title="备份 1Panel 应用" type="success" :closable="false" />
            <el-alert show-icon title="备份 1Panel 数据目录" type="info" :closable="false" />
            <el-alert show-icon icon="Search" title="备份 1Panel 本地备份目录" type="info" :closable="false" />
        </div>
        <template #footer>
            <span class="dialog-footer">
                <el-button @click="onCancel">
                    {{ $t('commons.button.cancel') }}
                </el-button>
            </span>
        </template>
    </el-dialog>
</template>

<script lang="ts" setup>
// import { loadSnapStatus } from '@/api/modules/setting';
import { onBeforeUnmount, ref } from 'vue';

// const status = ref();
const dialogVisiable = ref(false);

let timer: NodeJS.Timer | null = null;

interface DialogProps {
    id: number;
}

const acceptParams = (props: DialogProps): void => {
    dialogVisiable.value = true;
    console.log(props.id);
    // timer = setInterval(async () => {
    //     const res = await loadSnapStatus(props.id);
    //     status.value = res.data;
    // }, 1000 * 3);
};
const emit = defineEmits(['cancel']);

const onCancel = async () => {
    emit('cancel');
    dialogVisiable.value = false;
};

onBeforeUnmount(() => {
    clearInterval(Number(timer));
    timer = null;
});

defineExpose({
    acceptParams,
});
</script>
<style scoped lang="scss">
.el-alert {
    margin: 10px 0 0;
}
.el-alert:first-child {
    margin: 0;
}
</style>
