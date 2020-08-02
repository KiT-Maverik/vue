сначала нужно вставить скрипт
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

new Vue({}); vue instances can control the whole app or its part. U can use several vue instances on one app.


# Vue instance structure
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
```html
<!--content = vue instance data.sample value-->
<h1>{{ sample }}</h1>
<!--h1 content = whatever makeItPew vue instance method return (in this case 'pew-pew')-->
<h1>{{ makeItPew() }}</h1>
```

# Data binding
Использование переменных из `data`  в качестве значений атрибутов.
```html
<a v-bind:href="sample">It's a link</a>
<!--Сокращение    -->
<a :href="sample">It's a link</a>
``` 

### 2-way data binding
Позволяет привязать значение инпута к переменной инстанса.
```html
Все что пользователь введет в инпут будет сохранено в переменной инстанса "sample". 
<input type="text" v-model="sample">
``` 

# Events
При возникновения события будет выполнен код.
```html
<!--logger - это название метода Vue инстанса-->
<div v-on:click="logger">Click me</div>

<!--Shorthand-->
<div @click="logger">Click me</div>
```

### Event modifiers
Модификаторы позволяют управлять обработчиками событий.
```html
<!--logger сработает только при первом нажатии-->
<div @click.once="logger">Click me</div>
```

### Keyboard events
События клавиатуры срабатывают когда пользователь вводит текст в инпут.
```html
<input type="text" @keyup="logger">
```