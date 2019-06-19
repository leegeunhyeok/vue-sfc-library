# vue-sfc-library

[Packaging Vue.js components for npm](https://vuejs.org/v2/cookbook/packaging-sfc-for-npm.html)

## Project structure
```
package.json
build/
   rollup.config.js
src/
   wrapper.js
   my-component.vue
dist/
```

## package.json

```json
{
  "name": "my-component",
  "version": "1.2.3",
  "main": "dist/my-component.umd.js",
  "module": "dist/my-component.esm.js",
  "unpkg": "dist/my-component.min.js",
  "browser": {
    "./sfc": "src/my-component.vue"
  },
  "scripts": {
    // !! Build path와 위의 main, module, unpkg의 경로가 같아야함 !!
    "build": "npm run build:umd & npm run build:es & npm run build:unpkg",
    "build:umd": "rollup --config build/rollup.config.js --format umd --file dist/my-component.umd.js",
    "build:es": "rollup --config build/rollup.config.js --format es --file dist/my-component.esm.js",
    "build:unpkg": "rollup --config build/rollup.config.js --format iife --file dist/my-component.min.js"
  },
  "devDependencies": {
    "node-sass": "^4.12.0",
    "rollup": "^1.15.6",
    "rollup-plugin-buble": "^0.19.6",
    "rollup-plugin-commonjs": "^10.0.0",
    "rollup-plugin-vue": "^5.0.0",
    "sass-loader": "^7.1.0",
    "vue": "^2.6.10",
    "vue-template-compiler": "^2.6.10",
    ...
  },
  ...
}
```


## wrapper.js
필요한 컴포넌트를 빌드하기 위해 wrapper.js를 통해 묶어줌 (혹은 필요 로직 구현)
```javascript
// Vue 컴포넌트 import
import Component1 from './a.vue'
import Component2 from './b.vue'
import Component2 from './c.vue'

const components = {
  Component1,
  Component2,
  Component3
}

// Vue.use()에서 실행될 함수 선언
export function install(Vue) {
	if (install.installed) return
  install.installed = true

  Object.keys(components).forEach(name => {
    Vue.component(name, components[name])
  })
}

// Vue.use()를 위해 모듈 정의 생성
const plugin = {
	install
}

// 브라우저 환경에서 Vue가 있다면 Auto-install 진행
let GlobalVue = null
if (typeof window !== 'undefined') {
	GlobalVue = window.Vue
} else if (typeof global !== 'undefined') {
	GlobalVue = global.Vue
}
if (GlobalVue) {
	GlobalVue.use(plugin)
}

// 모듈로 사용하는것을 허용
export components
```

## rollup.config.js
```javascript
import commonjs from 'rollup-plugin-commonjs' // commonjs
import vue from 'rollup-plugin-vue' // SFC 제어
import buble from 'rollup-plugin-buble' // 브라우저를 위해 트랜스파일, 폴리필 적용

export default {
  input: 'src/wrapper.js', // entry
  output: {
    name: 'Vest', // 라이브러리명
    exports: 'named'
  },
  plugins: [
    commonjs(),
    vue({
      css: true, // style 태그의 스타일을 js 파일에 주입 (inline)
      compileTemplate: true // 템플릿을 render 함수로 변환
    }),
    buble() // ES5로 트랜스파일
  ]
}
```

## Build

```
npm run build
```
