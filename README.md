# laravel-file-manager (Frontend)

> File manager for Laravel - Frontend - Vue.js 

> Repository forked from - [alexusmai/vue-laravel-file-manager](https://github.com/alexusmai/vue-laravel-file-manager)

> Backend - Laravel 5 package - [alexusmai/laravel-file-manager](https://github.com/alexusmai/laravel-file-manager)

> NPM package [lv-file-manager](https://www.npmjs.com/package/lv-file-manager) 

Added few new things 
 - Permission for Upload and Delete button
 - New **insert** option into ContextMenu. When user select files and click on that option component will throw root event **fm-selected-items** with selected items as a object.
 - Additional Parameter for initalization 

![Laravel File Manager](https://raw.github.com/alexusmai/vue-laravel-file-manager/master/src/assets/laravel-file-manager.gif?raw=true)

## Installation

### NPM
```
$ npm i lv-file-manager
```

## Usage

**IF** your App using Vuex store

```
import FileManager from 'laravel-file-manager'
import store from './path-to-your-store/store'   // your Vuex store

Vue.use(FileManager, {store})
```

**ELSE** you need create new vuex instance

```
import Vue from 'vue';
import Vuex from 'vuex';
import FileManager from 'laravel-file-manager'

Vue.use(Vuex);

// create Vuex store, if you don't have it
const store = new Vuex.Store();

Vue.use(FileManager, {store});
```

`The application store module will be registered under the name 'fm'`

Now vue component is registered and you can use it in your app
```
<file-manager></file-manager>
```
For permission or additional Parameter try this
```
<file-manager :props={delete:false, upload: false, additionalParam: "foo=bar"}></file-manager>
```
Default both permission will be true. Make sure you pass boolean only to make it false. Also, note that additional param you will get only initialization time.

Don't forget add a csrf token to head block in your Laravel view and add bootstrap 4 and fontawesome 5 styles
```
<!-- CSRF Token -->
<meta name="csrf-token" content="{{ csrf_token() }}">
<!-- Example -->
<link rel="stylesheet" href="https://use.fontawesome.com/releases/v5.0.10/css/all.css">
<link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.1.0/css/bootstrap.min.css">
```
To catch selected file into object you can do this

```
mounted() {
    this.$root.$on('fm-selected-items',function(value){
        console.log(value);
    });
}
```

Warning! Package use axios (Promise) - use babel-polyfill for ie11
