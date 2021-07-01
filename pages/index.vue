<template>
  <div>
    <h2>着回しコーディネート</h2>
    <div id="xzbiz_suggestion"></div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import Component from 'vue-class-component'

@Component({
})
export default class extends Vue {
  created() {
    this.loadXZBiz("stg") // 検証環境への接続時は stg を指定してください
  }

  // XZbizのタグ読み込み
  loadXZBiz(env: "prod" | "stg") {
    const loaderScript = document.createElement("script")
    loaderScript.async = true
    loaderScript.onload = this.initXZBiz
    loaderScript.src = `https://biz.xz-closet.jp/assets/xzbiz-script-loader.js?type=suggest&site=andmall&env=${env}`
    document.body.appendChild(loaderScript)
  }

  // XZbizのタグ初期化
  initXZBiz() {
    const apiKey = "" // 指定されたAPIキーを設定
    const site = ""; // 指定されたサイト名を設定

    (window as any).xzbiz({
        apiKey       : apiKey,  
        site         : site, 
        mountTargetId: "#xzbiz_suggestion",
        modelCd: '1650000056300',
        testMode: true, /* テスト環境かどうか */
        debugMode: true /* 開発時はtrue */
    })
  }
}
</script>
