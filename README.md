# adjust-html-url
just for nodejs


## install

``` javascript
    npm install --save adjust-html-url
```


## node server.js

``` javascript
var express = require('express');
var adjustHtmlUrl = require('adjust-html-url');
var app = express();

app.get("/*", function (req, res) {

    var static_host = '';
    var useCache = false;
    if (process.env.NODE_ENV === "production") {
        static_host = 'http://cdn.ubibi.cn';
        useCache = true;
    }


    adjustHtmlUrl.doAdjust('/static/assets_spa/index.html', {
        urlPrefix: static_host,
        useCache: useCache
    }).then(function (d) {
        res.send(d);
    });

});
```


## source
``` html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8"/>
    <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no" />
    <meta http-equiv="X-UA-Compatible" content="IE=9" />
    <title>Title</title>
<link href="app/client_spa.9dae58ed.css" rel="stylesheet"></head>
<body>

<div id="mainBody">
    <router-view></router-view>
</div>

<script src="/static/lib/vue-2.3.0/vue.min.js"></script>
<script src="/static/lib/vue-router-2.6.0/dist/vue-router.min.js"></script>

<script type="text/javascript" src="app/client_spa.9dae58ed.js"></script></body>
</html>
```

##output
``` html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8"/>
    <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no" />
    <meta http-equiv="X-UA-Compatible" content="IE=9" />
    <title>Title</title>
<link href="http:/cdn.ubibi.cn/static/app/client_spa.9dae58ed.css" rel="stylesheet"></head>
<body>

<div id="mainBody">
    <router-view></router-view>
</div>

<script src="http:/cdn.ubibi.cn/static/lib/vue-2.3.0/vue.min.js"></script>
<script src="http:/cdn.ubibi.cn/static/lib/vue-router-2.6.0/dist/vue-router.min.js"></script>

<script type="text/javascript" src="http:/cdn.ubibi.cn/static/app/client_spa.9dae58ed.js"></script></body>
</html>
```
