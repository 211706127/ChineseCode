# ChineseCode
the project is to create a code-language in chinese.


超文本标记语言（html）部分 //重点不在这
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <link href="css.css" type="text/css" rel="stylesheet"/>
</head>
<body>
<div class="top">
    中文在线编程系统
</div>
<div class="input" id="input">
    <input type="text" class="input-" />
</div>
<script src="js.js" type="application/javascript" ></script>
</body>
</html>

层叠样式表部分（css）//重点不在这
* {
    margin: 0px;
    padding: 0px;
}
.top {
    height: 40px;
    width: 1000px;
    margin: 0px auto;
    background-color: aquamarine;
    font-family: 微软雅黑;
    font-weight: bold;
    font-size: 18px;
    color: black;
    line-height: 40px;
    text-indent: 4px;
}
.input {
    width: 1000px;
    margin: 20px auto;
    background-color: aqua;

}
.input- {
    width: 1000px;
    height: 30px;
    outline: none;
    border-bottom: 2px solid red;
    font-size: 16px;
    font-family: 微软雅黑;
    font-weight: bold;
    color: black;
}


Javascript部分
var obj = new Object();
var oInput = document.getElementsByClassName('input-');
var oInputDiv = document.getElementById('input');

function createNode(){
    var input = document.createElement('input');
    input.setAttribute('type','text');
    input.setAttribute('class','input-');
    oInputDiv.appendChild(input);
    oInput = document.getElementsByClassName('input-');
    oInput[oInput.length-1].focus();
    oInput[oInput.length-1].onkeydown = function() {
        if (event.keyCode == 13) {
            compilerAndRun();
            createNode();
        }
    };

}

function integerLookFor(inte){
    switch (inte) {
        case "零":return 0;
        break;
        case "一":return 1;
        break;
        case "二":return 2;
        break;
        case "三":return 3;
        break;
        case "四": return 4;
        break;
        case "五": return 5;
        break;
        case "六": return 6;
        break;
        case "七": return 7;
        break;
        case "八": return 8;
        break;
        case "九": return 9;
        break;
        case "十": return 10;
        break;
        default: return 0;
    }
}
function changeChinese (inte){
    switch (inte){
        case 0: return "零";
        break;
        case 1: return "一";
        break;
        case 2: return "二";
        break;
        case 3: return "三";
        break;
        case 4: return "四";
        break;
        case 5: return "五";
        break;
        case 6: return "六";
        break;
        case 7: return "七";
        break;
        case 8: return "八";
        break;
        case 9: return "九";
        break;
        case 10: return "十";
        break;
        default: return "零";
    }
}
function outputToWeb(content) {
    var div = document.createElement('div');
    div.innerHTML=content;
    oInputDiv.appendChild(div);
}

function compilerAndRun(){
    var str;
    var array;
    var definedInteger = /\s*整数\s+.+\s+等于.+\s*/g;
    var addition = /.+增加./g;
    var subtraction = /.+减少./g;
    var lookOne = /看看\s+[^"'”\s]+/g;
    var lookTow = /看看\s+\".+\"/g;
    if(definedInteger.test(oInput[oInput.length-1].value)){
        str = oInput[oInput.length-1].value;
        array = str.split(/\s+/);
        obj[array[1]] = integerLookFor(array[3]);
    }else if (addition.test(oInput[oInput.length-1].value)){
        str = oInput[oInput.length-1].value;
        array = str.split(/\s+/);
        obj[array[0]] += integerLookFor(array[2]);
    }else if (subtraction.test(oInput[oInput.length-1].value)){
        str = oInput[oInput.length-1].value;
        array = str.split(/\s+/);
        obj[array[0]] -= integerLookFor(array[2]);
    }else if (lookOne.test(oInput[oInput.length-1].value)){
        str = oInput[oInput.length-1].value;
        array = str.split(/\s+/);
        outputToWeb(changeChinese(obj[array[1]]));
    }else if (lookTow.test(oInput[oInput.length-1].value)){
        str = oInput[oInput.length-1].value;
        array = str.split(/\s+/);
        outputToWeb(array[1]);
    }
}
oInput[0].onkeydown = function() {
    if (event.keyCode == 13) {
        compilerAndRun();
        createNode();
    }
};
