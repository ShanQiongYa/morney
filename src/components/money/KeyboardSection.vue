<template>
  <div>
      <div class="notes">
        <FromItem
          type="date"
          field-name="日期"
          :value.sync="record.createAt"
          placeholder="在这里输入日期"
        />
        <FromItem
          field-name="备注"
          :value.sync="record.notes"
          placeholder="在这里输入备注"
        />
      </div>
        <number-pad :value.sync="record.amount" @submit="saveRecord" />
  </div>
</template>

<script lang="ts">
  import Vue from 'vue';
  import {Component, Prop} from 'vue-property-decorator';
  import NumberPad from "@/components/money/NumberPad.vue";
  import FromItem from "@/components/money/FromItem.vue";

  @Component({
      components: {NumberPad, FromItem}
  })
  export default class KeyboardSection extends Vue {
      record: RecordItem = {
          tags: [],
          notes: "",
          type: "-",
          amount: 0,
          createAt: new Date().toISOString(),
      };
      created() {
          this.$store.commit("fetchRecords");
      }
      onUpdateNotes(notes: string) {
          this.record.notes = notes;
      }
      saveRecord() {   
          if (!this.record.tags || this.record.tags.length === 0) {
              return window.alert("请至少选择一个标签");
          }
          if (this.record.amount === 0) {
              return;
          }
          this.$store.commit("createRecord", this.record);
          if (this.$store.state.createRecordError === null) {
              window.alert("已保存");
              this.record.notes = "";
          }
      }
  }
</script>

<style lang="scss" scoped>
   .show-money {
    margin-top: 68px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;

    span {
      padding: 5px;
      font-weight: 700;
    }

    .title {
      color: #81B7AA;
    }

    .titleWrapper {
      display: flex;
      flex-direction: row;
      align-items: center;
      border-bottom: 5px solid #9ccac0;
      font-size: 26px;
      padding: 8px;
      color: rgba(185, 186, 184, 0.9);

      & .icon {
        margin-right: 12px;
        width: 38px;
        height: 38px;
        fill: #9ccac0;
      }
    }

    .pay {
      font-size: 28px;
      color: #81B7AA;
    }

    .count {
      margin-top: 10px;
      font-size: 18px;
      color: rgba(185, 186, 184, 0.9);
      padding: 10px 16px;
      background-color: #f9faf5;
      border-radius: 8px;
    }

    .income {
      margin-top: 15px;
      color: #B7B7B7;
      font-size: 16px;
    }
  }
</style>