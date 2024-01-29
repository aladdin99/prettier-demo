<script setup>
class Foo {
  bar() {
    return 1;
  }
  bar() {
    return 2;
  }
}
</script>
<template>
  <zoehis-dialog
    :visible.sync="visibleDlg"
    :width="500"
    :height="300"
    :title="$t('operationManage.selectYieldType', '请选择要产生的类型')"
    ><div class="dialog-substance">
      <!--发货方不能为空提示-->
      <div v-show="isEmpty" class="empty">
        {{ $t("operationManage.shipperIsNull", "发货方不能为空！") }}
      </div>
      <div class="switch-type">
        <zoehis-radio-group v-model="applyType" @change="applyTypeChange">
          <zoehis-radio
            class="switch-icon type-one"
            name="size"
            label="1"
            :disabled="!procureDisable"
            >{{
              $tc("operationManage.switchPlan", 1, "转成采购计划单")
            }}</zoehis-radio
          >
          <zoehis-radio class="switch-icon type-two" name="size" label="2">{{
            $tc("operationManage.switchPlan", 2, "转成请领单")
          }}</zoehis-radio>
        </zoehis-radio-group>
      </div>
      <div v-show="consignorVisable" class="consignor">
        <span class="level-text"
          >{{ $t("operationManage.consignorCode", "选择发货方") }}：</span
        >
        <zoehis-select
          ref="keyfocus"
          v-model="consignorCode"
          :class="[{ 'empty-border': isEmpty }]"
          :selectdata="consignorList"
          :width="130"
          :placeholder="$t('operationManage.substituteName', '科室代用名')"
          itemcode="deptCode"
          itemtext="deptName"
          filterable
          @change="consignorChange"
        ></zoehis-select>
      </div>
    </div>
    <div slot="footer" class="dialog-footer">
      <zoehis-button
        icon="z_cancellationOA_normal02"
        @clickenter="closeDialog"
        >{{ $t("common.cancel", "取消") }}</zoehis-button
      >
      <zoehis-button
        type="primary"
        :disabled="!saveDisable"
        icon="z_examine_normal"
        @clickenter="saveApplyType"
        >{{ $t("common.sure", "确定") }}</zoehis-button
      >
    </div>
  </zoehis-dialog>
</template>
