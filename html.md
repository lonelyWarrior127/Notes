```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <style type="text/css">
    /*被style标签包围的范围是CSS环境，可以写CSS代码*/
    /*标签样式表*/
    p{
      color: coral;
    }
    /*类样式*/
    .f20{
      font-size: 20px;
    }
    /*id样式 ,id属性在整个html文档中，尽量保持唯一*/
    #p4{
      background-color: #b3d4fc;
      font-weight: bolder;
      font-family: 华文彩云;
    }

    #div1{
      width: 400px;
      height: 400px;
      background-color: greenyellow;

      border-width: 1px;
      border-style: solid;
      border-color: blue;
    }

    #div2{
      width: 200px;
      height: 200px;
      background-color: orange;
      margin-top:100px;
    }
    #div3{
      /*绝对定位*/
      position: absolute;
      left: 100px;
      top: 100px;
    }
  </style>
  <title>Hello World!</title>
</head>
<body>
  <p>这里是段落一</p>
  <p class="f20">这里是段落二</p>
  <p>这里是段落三</p>
  <p id="p4">这里是段落四</p>
  <div id = "div1">
    &nbsp;
    <div id="div2" > &nbsp</div>
  </div>

</body>
</html>

```

