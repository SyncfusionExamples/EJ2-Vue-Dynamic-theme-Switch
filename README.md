# Vue - Themeswitcher

 The Dynamic Theme Change can be achieved by loading the needed theme to the style tag dynamically using AJAX call. 

## Create a Vue application

To create a Vue application, refer to [`getting started`](https://ej2.syncfusion.com/vue/documentation/drop-down-list/getting-started/) document.

## Add Style Tag

In `index.html` file, add style tag for dynamic theme change. 

```typescript
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <title>vue</title>
    <link href="https://cdn.syncfusion.com/ej2/material.css" rel="stylesheet">
  </head>
  <body>
    <div id="app"></div>
    <script src="/dist/build.js"></script>

    <!-- add style tag for dynamic theme change -->
    <style id="theme"></style>
  </body>
</html>

```
## Add Different Themes for Dynamic Theme Change

In the `src` folder of the application, create `assets` folder. 

Under `assets` folder, create a folder named `styles`. Then, load CSS file of the different themes in that `styles` folder. 

## Use Ajax for Dynamic Theme Change

In `App.Vue` file, add below `onChange` function.

```typescript
 methods: {
    onChange: function(e) {
        debugger
        console.log(e);
        if (e && e.itemData.value) {
            let ajax = new Ajax('src/assets/styles/' + e.itemData.value + '.css', 'GET', true);
            ajax.send().then((result) => {
              let styleTag = document.getElementById('theme');
              styleTag.innerHTML=`/*${e.itemData.value}*/` + result;
            });
          }
    }
 }

 ```

 Whenever the `onChange` function gets triggered, the corresponding CSS file of the selected theme is applied to the DOM element using AJAX.

## Build and Run the Application

``` bash
# install dependencies
npm install

# build for production with minification
npm run build

# serve with hot reload at localhost:8080
npm run dev

```

For detailed explanation on how things work, consult the [docs for vue-loader](http://vuejs.github.io/vue-loader).
