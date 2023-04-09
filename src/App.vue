<template>
  <div class="space_for_header">
    <div class="q-pa-md">

      <!-- left menubar -->
      <q-dialog v-model="dialog" :position="position">
        <q-card style="width: 250px; height: 100%;">
          <q-card-section class="items-start no-wrap">
            <q-btn class="text-weight-bold text-h6 q-mb-sm" flat to="./"><q-icon name="house"></q-icon>　トップ画面</q-btn>
            <q-btn class="text-weight-bold text-h6 q-mb-sm" flat to="./thoughts"><q-icon name="menu_book"></q-icon>　顧客管理</q-btn>
            
            <q-separator spaced />

            <q-btn class="text-weight-bold text-h6 q-mb-sm" flat to="./"><q-icon name="settings"></q-icon>　設定</q-btn>
            <q-btn class="text-weight-bold text-h6 q-mb-sm" flat to="./"><q-icon name="help"></q-icon>　問い合わせ</q-btn>

          </q-card-section>
        </q-card>
      </q-dialog>

        <!-- header -->
        <q-layout view="lHh lpr lFf"  class="shadow-2 rounded-borders">
            <q-header elevated class="bg-brown">
            <q-toolbar>
                <q-btn flat round dense icon="menu" class="q-mr-sm" @click="open('left')"/>
    
                <q-toolbar-title class="title_for_phone">神社仏閣向け CRMサンプル</q-toolbar-title>
            </q-toolbar>
            </q-header>

              <!-- router -->
              <RouterView />

        </q-layout>
    </div>
  </div>
</template>

<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
import { ref } from 'vue'

const dialog = ref<boolean>(false)
const position = ref<any>('left')

function open(pos:any) {
  position.value = pos
  dialog.value = true
}

</script>

<style scoped>
.space_for_header{
  margin-top: 60px;
  margin-bottom: 50px;
}

header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}

@media screen and (max-width: 1024px){
  div.title_for_phone{
    font-size: 16px;
    font-weight: bold;
  }
}
</style>
