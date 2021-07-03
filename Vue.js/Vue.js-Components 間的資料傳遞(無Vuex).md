---
title: '[Vue.js] Components 間的資料傳遞（無Vuex）'
tags: [JavaScript, Vue.js, Components]
category: Vue.js
date: 2021-03-03 01:06:42
permalink: posts/210303

---

示例 Component 之間的各種傳值方式－父子互傳(`props`/`emit`)、祖孫互傳(`listeners`/`attr`)、同輩互傳(`eventBus`) 

<!--more--> 

> 適用:
> - Vue 2.x
> - 知道基本的 Vue.js 結構
> - 知道 Component 概念
  
---

## Demo
[> CodeSandbox]([https://codesandbox.io/s/componentjiandeziliaochuandilianxiwuvuex-uu0fb?from-embed])

<iframe src="https://codesandbox.io/embed/componentjiandeziliaochuandilianxiwuvuex-uu0fb?autoresize=1&fontsize=14&hidenavigation=1&theme=dark&view=preview"
     style="width:100%; height:860px; border:0; border-radius: 4px; overflow:hidden;"
     title="*Component間的資料傳遞練習（無VueX)"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

<iframe src="https://codesandbox.io/embed/componentjiandeziliaochuandilianxiwuvuex-uu0fb?autoresize=1&codemirror=1&fontsize=14&module=%2Fsrc%2Fcomponents%2Fa1.vue&theme=dark&view=editor"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="*Component間的資料傳遞練習（無VueX)"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

> (點左上角選單按鈕可以展開目錄欄，瀏覽檔案)

---

- 本例 Components 組件引用關係：

    - a1 引入 b1 & b2
    ```html{2,3}
    <template>
        <b1/></b1>
        <b2/></c2>
    </template>
    ```

    - b1 引入 c1
    ```html{2}
    <template>
        <c1/></c1>
    </template>
    ```

---

# 往下傳：

## 1.父傳子 (props in)

- a1 ：引子組件時直接透過 v-bind 傳資料

    ```html{2,8}
    <template>
    	<b1 :textA1="textA1" />
    </template>

    <script>
    	data: () => {
            return {
                textA1: "A1",
            };
        },
    </script>
    ```

- b1：定義 props 接收父層資料

    ```html{2,6-10}
    <template>
    	<p>{{ textA1 }}</p>
    </template>

    <script>
        props: {
            textA1: {
                type: String
            }
        }
    </script>
    ```

---

## 2.爺傳孫


### 2-1.透過父（props in x2）

- a1 傳給子

    ```html{2,8}
    <template>
    	<b1 :textA1="textA1" />
    </template>

    <script>
    	data: () => {
            return {
                textA1: "A1"
            };
      },
    </script>
    ```

- b1 再傳給子

    ```html{2,6-10}
    <template>
    	<c1 :textA1="textA1" />
    </template>

    <script>
    	props: {
            textA1: {
                type: String
            }
        }
    </script>
    ```

- c1

    ```html{2,6-10}
    <template>
    	<p>{{ textA1 }}</p>
    </template>

    <script>
    	props: {
            textA1: {
                type: String
            }
      }
    </script>
    ```

---

### 2-2.不透過父（`attr`）

- a1 傳給子

    ```html{2,8}
    <template>
    	<b1 :textA2="textA2" />
    </template>

    <script>
    	data: () => {
            return {
                extA2: "A2",
            };
        }
    </script>
    ```

- b1 引用子時使用 `$v-bind="$attrs"`

    ```html{2}
    <template>
    	<c1 v-bind="$attrs" />
    </template>
    ```

- c1 透過 `$attrs.XXX` 取資料

    ```html{2}
    <template>
    	<p>{{ $attrs.textA2 }}</p>
    </template>
    ```

---

# 往上傳

## 3.子傳父 ( `emit`)

- a1

    ```html{2-3,9,13-15}
    <template>
    	<b1 @emit-data="getChildData"/>
    	<p>{{ dataFromChild }}</p>
    </template>

    <script>
    	data: () => {
            return {
                dataFromChild: "",
            };
        },
    	methods: {
            getChildData(param) {
                this.dataFromChild = param;
            }
        }
    </script>
    ```

- b1

    ```html{2,8,12-14}
    <template>
    	<button @click="dataToParent">傳資料給父層</button>
    </template>

    <script>
        data: () => {
            return {
                textB1: "B1",
            };
        },
        methods: {
            dataToParent() {
                this.$emit("emit-data", this.textB1);
            }
        }
    </script>
    ```

---

## 4.孫傳爺（`emit` / `listeners`）

- a1

    ```html{2,3,9,13-15}
    <template>
    	<b1 @getGrandSonData="getGrandSonData"/>
    	<p>{{ dataFromGrandSon }}</p>
    </template>

    <script>
    	data: () => {
            return {
                dataFromChild: ""
            };
        },
        methods: {
            getChildData(param) {
                this.dataFromChild = param;
            }
        }
    </script>
    ```

- b1

    ```html{2}
    <template>
    	<c1 v-on="$listeners" />
    </template>
    ```

- c1

    ```html{2,8,12-15}
    <template>
        <button @click="sendGrandSonData">傳資料給祖父層</button>
    </template>

    <script>
      data: () => {
            return {
                textC1: "C1",
            };
        },
        methods: {
            dataToParent() {
                this.$listeners.getGrandSonData(this.textC1);
                // 等同於 this.$emit("getGrandSonData", this.textC1);
            },
        }
    </script>
    ```

---

# 左右傳

## 5.傳兄弟 (eventBus)

- 父層a1含b1、b2。b1要傳給b2

    ```html{2,3}
    <template>
    	<b1/></b1>
    	<b2/></c2>
    </template>
    ```

1. eventBus：建立共用同一個事件機制-新增一個獨立的js檔 (例:eventBus.js)

    ```js
    import Vue from 'vue';

    export default new Vue();
    ```

2. 子組件 b1、b2 都引入 eventBus.js 檔

    ```html{2}
    <script>
    	import eventBus from "./../js/eventBus.js";
    </script>
    ```

3. 子組件 b1 (要傳遞資料的）

    ```html{2,8,12-14}
    <template>
    	<button @click="dataToBrother">傳資料給兄弟</button>
    </template>

    <script>
        data: () => {
            return {
                textB1: "B1",
            };
        },
        methods: {
            dataToBrother() {
                eventBus.$emit("emit-data", this.textB1);
            }
        }
    </script>
    ```

4. 子組件 b2（要接收資料的）

    ```html{2,8,12,15-19}
    <template>
    	<p>{{ dataFromBrother}}</p>
    </template>

    <script>
        data: () => {
            return {
                dataFromBrother: "",
            };
        },
        created: function () {
            this.getFromBrother();
        },
        methods: {
            getFromBrother() {
                eventBus.$on("emit-data", (param) => {
                    this.dataFromBrother= param;
                });
            }
        }
    </script>
    ```

---

## (參考資料)

   - [props|Vue.js](https://vuejs.org/v2/guide/components-props.html)
   - [vue.js 兄弟元件之間的值傳遞方法](https://www.itread01.com/content/1542000913.html)
   - [Vue祖孙组件怎么传值](https://blog.csdn.net/qq_40738077/article/details/106765455)
   - [Vue父子组件传值其实不难](https://blog.csdn.net/qq_40738077/article/details/106737301)