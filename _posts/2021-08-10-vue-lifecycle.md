---
layout: post
title: Vue Lifecycle 관련
subheading: mounted 훅에 대해
author: kyong
categories: 
tags: Vue, 회사
sidebar: []
---


vue에 구글맵이 rendering 안되는 버그 발생<br/>
현재 프로젝트는 vue2 + typescript로 구성되어 있는데, 뭔가 안에서 꼬여서 아이폰에서만 구글맵이 보이지 않는 버그가 발생했다.<br/>

#### 해결 방법
GoogleMap.vue (App.vue에 임포트하는 컴포넌트) <br/>
`/src/components/GoogleMap.vue`
```javascript
 <template>	
	<div class="container">
		<gmap-map
      v-bind="options"
      id="map"
    ></gmap-map>
	</div>	
</template>
<script>
import { gmapApi } from 'vue2-google-maps';

export default {
  name: "GoogleMap",
  data() {
    return {
      options: {
        zoom: 10,
        center: {
          lat: 39.9995601,
          lng: -75.1395161
        },
        mapTypeId: 'roadmap'
      }
    };
  },
  computed: {
    google: gmapApi
  },

};
</script>

<style scoped>
#map {
  height: 500px;
  width: 100%;
  margin: 0 auto;
}
</style>
```

vue.config.js <br/>
`/vue.config.js`
```javascript
module.exports = {
    runtimeCompiler: true
}
```

main.ts<br/>
`/src/main.ts`
```typescript
import Vue from 'vue'
import App from './App.vue'
import './registerServiceWorker'
import router from './router'
import store from './store'
import * as VueGoogleMaps from "vue2-google-maps";

Vue.config.productionTip = false

new Vue({ //프로젝트 기본 설정
  router,
  store,
  render: h => h(App)
}).$mount('#app')

Vue.use(VueGoogleMaps, {
  load: {
    key: "",
    libraries: "places", // necessary for places input
    region: "uk,en"
  }
});

```

vue2-google-maps.d.ts<br/>
`/src/@types/vue2-google-maps.d.ts`
```typescript
declare module 'vue2-google-maps' {
    import { PluginFunction } from "vue";
    export const install: PluginFunction<{}>;
    /// <reference types="@types/googlemaps" />
    class gmapApi extends Vue {}

    export { gmapApi };
  }
  
```