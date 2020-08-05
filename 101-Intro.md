# Vue instance
Vue instance это центр управления приложением. Он может контроллировать целое приложение или его часть.
Vue instance работает по принципу реактивности. Это значит, что вся информация связана с местами ее использования (ее обновление происходит сразу везде).
для начала работы нужно вставить в HTML скрипт
```html
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
```
### Instance structure
```js
new Vue({
    el: '#vueRoot',
    data: {
        sample: 'pew-pew'
    },
    methods: {
        makeItPew: function () {
            return this.sample;
        }
    }
})
```

# Using data properties & methods
```js
new Vue({
    el: '#vueRoot',
    data: {
        sample: 'It is header',
        methodOutput: "Advanced header"
    },
    methods: {
        makeItPew: function () {
            return this.methodOutput;
        }
    }
})
```
```html
<div id="vueRoot" >
    <!--h1 content = It is header-->
    <h1>{{ sample }}</h1>
    <!--h1 content = Advanced header-->
    <h1>{{ makeItPew() }}</h1>
</div>
```

### Продвинутое использование данных
Все что в фигурных скобок находится выражение. Это значит что там можно использовать все возможности JS.
```html
    <h1>{{ sample + '?' }}</h1>
    <h1>{{ `${sample} and ${methodOutput}` }}</h1>
    <h1>{{ sample.toUpperCase() }}</h1>
    <h1>{{ false ? "confirmed" : "not confirmed" }}</h1>
```

# Data binding
Использование переменных из `data` в качестве значений атрибутов.
```js
new Vue({
    el: '#vueRoot',
    data: {
        sample: 'https://google.com'
    }
})
```
```html
<div id="vueRoot" >
    <!--href attribute value ='https://google.com'-->
    <a v-bind:href="sample">Regular link</a>
    <!--Сокращение    -->
    <a :href="sample">Shorthand link</a>
</div>
``` 

### 2-way data binding
Позволяет привязать значение инпута к переменной инстанса.
```js
new Vue({
    el: '#vueRoot',
    data: {
        sample: 'Hello'
    }
})
```
```html
<div id="vueRoot">
    <!--Все что пользователь введет в инпут будет сохранено в переменной инстанса "sample". -->
    <input type="text" v-model="sample">
    <!--    Все изменения переменной sample немедленно отразятся здесь.-->
    <label>{{sample}}</label>
</div>
``` 

# Условное отображение
Vue JS поддерживает условные операторы, которые добавляют или удаляют из DOM элементы.
Если элементы нужно часто менять видимость, то лучше использовать директиву `v-show`, которая проставляет инлайн стиль `display: none` (это улучшает производительность).  
```html
<div id="vueRoot" >
    <h1 id="pew" v-if="inventory > 10"> In stock</h1>
    <h1 id="pew2" v-else-if="inventory < 10 && inventory > 0">Running out!</h1>
    <h1 v-else="inventory = 0">Sold out</h1>
    <p v-show="true">set false to hide</p>
</div>
```

# Цикл for (рендер списков)
```js
new Vue({
    el: '#vueRoot',
    data: {
        items: ["item #1", "item #2", "item #3"]
    }
})
```
```html
<div id="vueRoot" >
    <ul>
        <li v-for="item of items"> {{item}}</li>
    </ul>
</div>
```
# Events
При возникновения события будет выполнен код.
```js
new Vue({
    el: '#vueRoot',
    methods: {
        logger: () => console.log("It works!")
    }
})
```
```html
<div id="vueRoot">
    <!-- При клике будет выполнен метод "logger"-->
    <div v-on:click="logger">Regular trigger</div>

    <!--Shorthand-->
    <div @click="logger">Shorthand trigger</div>
</div>
```

### Event modifiers
Модификаторы позволяют управлять обработчиками событий.
```html
    <!--logger сработает только при первом нажатии-->
    <div @click.once="logger">Single use trigger</div>
```

### Keyboard events
События клавиатуры срабатывают когда пользователь вводит текст в инпут.
```html
<input type="text" @keyup="logger">
```

### Computed properties
Computed properties рассчитывают значение на основе существующих свойств инстанса.  
Результат расчета закеширован и обновляется только при изменении участников расчета.
```js
new Vue({
    el: '#vueRoot',
    data: {
        girl: "Ann",
        boy: "Jack"
    },
    computed: {
        statement () {
            return `${this.girl} + ${this.boy} = LOVE`
        }
    }
})
```
```html
<div id="vueRoot" >
    <h1>{{statement}}</h1>
</div>
```

# Components
Компонент это переиспользуемый кусок кода.  
Для начала его нужно зарегистрировать с помощью метода `Vue.component(name, settings)`. Компонент вызывается в DOM по имени. 
```js
Vue.component("sample", {
    template: `<h1>{{greeting + " " + name}}</h1>`,
    props: {
        name: {
            type: String,
            required: true,
            default: 'Anonymous!'
        }
    },
    data() {
        return {
            greeting: 'Morning, mr. '
        }
    }
})

new Vue({
    el: '#vueRoot'
})
```
```html
<div id="vueRoot" >
    <sample></sample>
    <sample name="KiT"></sample>
</div>
```
### Template
* `template` - HTML-код элемента
* `props` - информация, которая передается в  компонент извне
> Чтобы передать `props` в компонент, нужно добавить его как HTML-атрибут компонента. Пример: `<sample name="KiT"></sample>` 
* `data()` - информация хранящаяся внутри компонента
> В компонентах `data` это не объект, а функция. Это сделано для того, чтобы каждый компонент имел свйо собственный `data` объект.