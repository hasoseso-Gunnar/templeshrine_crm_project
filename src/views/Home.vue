<template>
  <div class="q-pa-md items-start q-gutter-md">
    <q-item-label class="text-h4 q-pa-md" style="font-weight: bold;">今日やること</q-item-label>

    <!-- タスクタブ設定 -->
    <div class="top-tab mt-3 mx-3">
      <q-tabs
        v-model="todaysTabs"
        dense
        class="text-grey-10"
        align="justify"
        active-color="white"
        active-bg-color="brown"
        indicator-color="transparent"
      >
        <div style="width: 98%; display: flex; margin-left: auto; margin-right: auto">
          <q-tab name="undone" label="未完了">
            <q-badge 
              color="red" 
              floating
              :label="todaysLableBadge.undonetasks"
              >
            </q-badge>
          </q-tab>
          
          <q-tab name="done" label="完了">
            <q-badge 
              color="red" 
              floating
              :label="todaysLableBadge.donetasks"
              >
            </q-badge>
          </q-tab>
        </div>
      </q-tabs>
    </div>
    <div class="top-separator" style="margin-top: 0px;">
      <q-separator></q-separator>
    </div>

    <q-tab-panels v-model="todaysTabs" style="height: 250px; overflow-y: scroll;">
        <!-- 未完了タスク -->
        <q-tab-panel name="undone">
          <div v-if="todaysLableBadge.undonetasks === 0" style="font-size: 18px; margin-top: 50px; text-align: center;">なし</div>
          <div v-for="task in todaysTasks" class="comment_section">

            <q-item 
              tag="label"
              v-ripple
              v-if="!task.done"
              >

              <q-item-section side top>
                <q-checkbox v-model="task.done"/>
              </q-item-section>

              <q-item-section>
                <q-item-label>{{ task.title }}</q-item-label>
                <q-item-label caption>
                  {{task.description}}
                </q-item-label>
              </q-item-section>
            
            </q-item>
          </div>
        </q-tab-panel>

        <!-- 完了タスク -->
        <q-tab-panel name="done">
          <div v-if="todaysLableBadge.donetasks === 0" style="font-size: 18px; margin-top: 50px; text-align: center;">なし</div>
          <div v-for="task in todaysTasks"  class="comment_section">

            <q-item 
              tag="label"
              v-ripple
              v-if="task.done"
              >

              <q-item-section side top>
                <q-checkbox v-model="task.done"/>
              </q-item-section>

              <q-item-section>
                <q-item-label>{{ task.title }}</q-item-label>
                <q-item-label caption>
                  {{task.description}}
                </q-item-label>
              </q-item-section>
            
            </q-item>
          </div>
        </q-tab-panel>
    </q-tab-panels>

    <q-item-label class="text-h4 q-pa-md" style="font-weight: bold;">近日やること</q-item-label>

    <!-- タスクタブ設定 -->
    <div class="top-tab mt-3 mx-3">
      <q-tabs
        v-model="recentTabs"
        dense
        class="text-grey-10"
        align="justify"
        active-color="white"
        active-bg-color="brown"
        indicator-color="transparent"
      >
        <div style="width: 98%; display: flex; margin-left: auto; margin-right: auto">
          <q-tab name="undone" label="未完了">
            <q-badge 
              color="red" 
              floating
              :label="recentLableBadge.undonetasks"
              >
            </q-badge>
          </q-tab>
          
          <q-tab name="done" label="完了">
            <q-badge 
              color="red" 
              floating
              :label="recentLableBadge.donetasks"
              >
            </q-badge>
          </q-tab>
        </div>
      </q-tabs>
    </div>
    <div class="top-separator" style="margin-top: 0px;">
      <q-separator></q-separator>
    </div>

    <q-tab-panels v-model="recentTabs" style="height: 250px; overflow-y: scroll;">
        <!-- 未完了タスク -->
        <q-tab-panel name="undone">
          <div v-if="recentLableBadge.undonetasks === 0" style="font-size: 18px; margin-top: 50px; text-align: center;">なし</div>
          <div v-for="task in recentTasks" class="comment_section">

            <q-item 
              tag="label"
              v-ripple
              v-if="!task.done"
              >

              <q-item-section side top>
                <q-checkbox v-model="task.done"/>
              </q-item-section>

              <q-item-section>
                <q-item-label>{{ task.title }}</q-item-label>
                <q-item-label caption>
                  {{task.description}}
                </q-item-label>
              </q-item-section>
            
            </q-item>
          </div>
        </q-tab-panel>

        <!-- 完了タスク -->
        <q-tab-panel name="done">
          <div v-if="recentLableBadge.donetasks === 0" style="font-size: 18px; margin-top: 50px; text-align: center;">なし</div>
          <div v-for="task in recentTasks"  class="comment_section">

            <q-item 
              tag="label"
              v-ripple
              v-if="task.done"
              >

              <q-item-section side top>
                <q-checkbox v-model="task.done"/>
              </q-item-section>

              <q-item-section>
                <q-item-label>{{ task.title }}</q-item-label>
                <q-item-label caption>
                  {{task.description}}
                </q-item-label>
              </q-item-section>
            
            </q-item>
          </div>
        </q-tab-panel>
    </q-tab-panels>
  </div>
</template>

<script setup lang="ts">
  import { ref, computed} from 'vue';

  interface tasksRules {
    title: string;
    deadline: string;
    description: string;
    done: boolean;
  }

  const todaysTabs = ref<string>("undone");
  const recentTabs = ref<string>("undone");

  //今日やること
  const todaysTasks = ref<Array<tasksRules>>([
    {
      title:'田中様 お電話',
      deadline:'2023/04/01',
      description:'先日のことで確認したいことがあるため、電話。',
      done: false,
    },
    {
      title:'佐藤様 打ち合わせ',
      deadline:'2023/04/01',
      description:'来週のことで打ち合わせ。',
      done: false,
    },
    {
      title:'給与振込確認',
      deadline:'2023/04/01',
      description:'バイトの太郎君の給与振り込みを行う。',
      done: false,
    },
  ]);

  interface todaysLableBadgeObj {
    donetasks: number;
    undonetasks: number;
  }
  const todaysLableBadge = computed(() => {
    let temp: todaysLableBadgeObj = {
      donetasks: 0,
      undonetasks: 0
    };
    temp.donetasks = todaysTasks.value.reduce(
      (sum, item: any) => (item.done === true ? sum + 1 : sum),
      0
    );
    temp.undonetasks = todaysTasks.value.reduce(
      (sum, item: any) => (item.done === false ? sum + 1 : sum),
      0
    );
    return temp;
  });

  //近日やること
  const recentTasks = ref<Array<tasksRules>>([
    {
      title:'社団法人○○訪問',
      deadline:'2023/04/31',
      description:'来月のイベントの件で顔合わせ。',
      done: false,
    },
    {
      title:'○○様 5周忌',
      deadline:'2023/04/21',
      description:'○○様のご家族に事前連絡。',
      done: false,
    },
  ]);

  interface recentLableBadgeObj {
    donetasks: number;
    undonetasks: number;
  }
  const recentLableBadge = computed(() => {
    let temp: recentLableBadgeObj = {
      donetasks: 0,
      undonetasks: 0
    };
    temp.donetasks = recentTasks.value.reduce(
      (sum, item: any) => (item.done === true ? sum + 1 : sum),
      0
    );
    temp.undonetasks = recentTasks.value.reduce(
      (sum, item: any) => (item.done === false ? sum + 1 : sum),
      0
    );
    return temp;
  });

</script>
<style lang="scss" scoped>

.top-separator {
  .q-separator {
    height: 3px;
    background-color: $brown;
  }
}
</style>