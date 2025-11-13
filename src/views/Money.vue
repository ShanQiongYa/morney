<template>
  <div class="money-wrapper">
    <TopNav name="left">
      <Tabs slot="title"
            class-prefix="types"
            :data-source="recordTypeList"
            :value.sync="selected.type"
      />
    </TopNav>
    <section class="main">
      <Tags @update:value="selected.tags = $event" />
    </section>
    <KeyboardSection :amount.sync="selected.amount"
                     :notes.sync="selected.notes"
                     :createdAt.sync="selected.createdAt"
                     @onSubmit="saveRecord"/>
  </div>
</template>

<script lang="ts">
  import TopNav from '@/components/TopNav.vue';
  import CategorySection from "@/components/money/CategorySection.vue"
  import KeyboardSection from "@/components/money/KeyboardSection.vue"
  import Tags from "@/components/money/Tags.vue";
  import Tabs from "@/components/Tabs.vue";
  
  import Vue from 'vue';
  import {Component} from 'vue-property-decorator';
  import recordTypeList from "@/constants/recordTypeList";

  @Component({
    components: {TopNav,CategorySection,KeyboardSection,Tags,Tabs},
    computed: {
      recordList() {
        return this.$store.state.recordList;
      },
    },

  })
  export default class Money extends Vue {
    recordTypeList = recordTypeList;
    // 初始值
    selected: RecordItem = {
      tags: [],
      notes: "",
      type: "-",
      amount: 0,
      createAt: new Date().toISOString(),
    };
    created() {
      console.log("0-------");
      
      console.log(recordTypeList);
      
      this.$store.commit('fetchRecords');
      this.$store.commit('fetchTags');
    }
    saveRecord() {
      console.log(this.selected);
      
      this.$store.commit('createRecord', this.selected);
    }
  }
</script>

<style lang="scss" scoped>
  .money-wrapper {
    max-width: 520px;
    margin: 0 auto;
    background-color: #fff;
    height: 100vh;
    position: absolute;
    top: 0;
    left: 0;
    bottom: 0;
    right: 0;
    overflow-y: auto;
    overflow-x: hidden;
    z-index: 1;
    display: flex;
    flex-direction: column;

    .main {
      background-color: #fafbf6;
      flex: 1;
      overflow: auto;

      &::-webkit-scrollbar {
        display: none;
      }
    }
  }
</style>