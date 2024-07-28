<template>
  <q-page class="q-page q-pa-lg">
    <div class="row justify-center">
      <div class="col-9 q-px-xl q-pb-xl bg-brand">
        <h4>你好！</h4>
        <p>這是一個音樂劇的wiki目前的功能有：</p>
        <ul>
          <li>演員列表</li>
          <li>演員的出演作品</li>
          <li>演員的大頭貼和圖片集</li>
        </ul>
        <h5 class="q-my-lg">架構</h5>
        <img src="~assets/架構圖.jpg" />
        <h6 class="q-my-lg">後端</h6>
        <p>
          <a href="https://github.com/FallPrediction/musical_wiki_backend"
            >Repo</a
          >
        </p>
        <p>
          這是我剛開始學習GO的專案，使用<a
            href="https://github.com/gin-gonic/gin"
            >Gin</a
          >框架。因為習慣PHP的Laravel，所以這個專案的某些檔案目錄會參照Laravel，如：
        </p>
        <ul>
          <li>handler(controller)</li>
          <li>service</li>
          <li>repository</li>
          <li>helper</li>
          <li>request</li>
          <li>等等</li>
        </ul>
        <p>
          目前只有給helper寫unittest。以及大部分initialize都用singleton，如Redis,
          DB Connection等，之後會用GO wire改寫
        </p>
        <h6 class="q-my-lg">前端</h6>
        <p>
          <a href="https://github.com/FallPrediction/musical_wiki_frontend"
            >Repo</a
          >
        </p>
        <p>
          非前端工程師所以選了<a
            href="https://github.com/quasarframework/quasar"
            >Quasar</a
          >，是使用Vue（專案使用Vue3）的UI框架
        </p>
        <h6 class="q-my-lg">Infra</h6>
        <p>
          <a href="https://github.com/FallPrediction/musical_wiki_terraform"
            >Terraform Repo</a
          >
        </p>
        <p>
          <a href="https://github.com/FallPrediction/musical_wiki_ansible"
            >Ansible Repo</a
          >
        </p>
        <p>此專案使用Terraform + Ansible架在AWS上</p>

        <p>
          為了<del>省錢</del>簡單，使用託管的資料庫<a
            href="https://supabase.com/"
            >Supabase</a
          >，也因為這樣所以服務全放在一台在public subnet的server
        </p>
        <p>
          使用Gihub action觸發CodeDeploy部署。如何使用CodeDeploy部署GO
          APP，可以參考<a
            href="https://fallprediction.github.io/blog/posts/code-deploy/"
            >我的部落格文章</a
          >
        </p>
        <h5 class="q-my-lg">作者</h5>
        <p>Elizabeth Huang</p>
        <p>
          現職PHP後端工程師，喜歡在業餘時間研究一些哩哩摳摳。最近致力成為一名Gopher
        </p>
        <p><a href="https://fallprediction.github.io/blog/">我的部落格</a></p>
        <p><a href="https://github.com/FallPrediction">我的Github</a></p>
      </div>
    </div>
  </q-page>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "IndexPage",
});
</script>
