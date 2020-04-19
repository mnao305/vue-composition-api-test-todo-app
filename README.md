# vue-composition-api-test-todo-app

## 学習メモ

### 導入
Vue本体は2系を導入した。ここは通常通り下記コマンドでやる。
```shell
$ vue create project-name
```

`Please pick a preset:`と聞かれるので、`Manually select features`を選択する。  
`Check the features needed for your project:`と導入するものを選択できるので`TypeScript`を選択する。他は適当に。  
その後、`Use class-style component syntax?`とclassスタイル使うか？と聞かれるので`n`を押す。後は適当に。

その後プロジェクトルートに行き、`@vue/composition-api`を入れる。
```shell
$ cd project-name
$ npm install @vue/composition-api
```

`src/main.ts`に下記のように追加する。
```typescript
import Vue from 'vue';
import VueCompositionApi from '@vue/composition-api';

Vue.use(VueCompositionApi);
```

### 基本
```html
<script lang="ts">
import { defineComponent } from '@vue/composition-api'

export default defineComponent({
  setup (props, context) {
    console.log('hello world')
    const state = reactive({ text: 'hogefuga', coutn: 0 })
    const countUp = () => {
      state.count++
    }
    console.log(state.text)
    return {
      state,
      countUp
    }
  }
})
</script>
```
これが基本形。  
`defineComponent`を使うことで型推論が正しく行われる。

composition-apiv0.4.0で`createComponent`から`defineComponent`に名前が変わった

#### setup
そのコンポーネントインスタンスが作られたときに発火する。
第一引数には`props`、第二引数には`context`が渡される。
`props`は親から渡されるデータ、`context`はVue2系での`this`に入っているようなもの（ex: emit）が入っている。

Vue2系での`data`のように、リアクティブな値を定義する場合は`reactive`を使う。  
上の例の場合、`state.text`のようにアクセスすれば`hogefuga`が返ってくる。

`setup`関数内で定義した変数や関数をtemplate内で使う場合はreturnでオブジェクトを返すようにする

### props - 親から子にデータを渡す
```typescript
import { defineComponent, PropType } from '@vue/composition-api'

export default defineComponent({
  props: {
    item: {
      type: Object as PropType<TodoItemType>,
      required: true
    }
  },
  setup (props) {
    console.log(props.todoList)
  略
```
`props`というオブジェクトのキーに受け取る名前、その中のオブジェクトの`type`で型指定、`required`で必須かどうか指定ができる。  
`default`を設定すれば、親から値が渡されなかった場合のデフォルト値を指定できる。

オブジェクトを使う時に型定義をしたい場合があると思うが、そのまま`type: TodoItemType`のようには指定できない。  
`PropType`を使うことで型を指定することができる。

`setup`関数内で`props`を使う場合、1つ目の引数にpropsが入ってくるのでそれを使う。

```typescript
  setup (props, { emit }) {
    const inputText = computed({
      get: () => props.text,
      set: (value) => emit('input', value)
    })
    return {
      inputText
    }
  }
```
`template`内で使いたい場合はsetup関数でreturnしてあげないといけない。  
`props`で受け取った値を変更するような場合は↑のように、`computed`を使うとシンプルになる。

`props`はリアクティブなオブジェクトだが、下記のように分割代入するとそうじゃなくなり、変更検知等できなくなるので注意。
```typescript
setup({ text }) {
}
```


## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Run your unit tests
```
npm run test:unit
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
