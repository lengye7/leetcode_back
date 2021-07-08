# 去除字符串连续的重复字符

题目：字符串中连续的重复字符,字符默认全部小写英文字母。

    例子1："aaaabbbbcccc"
    输出："abc"

    例子2："dddeeed"
    输出："ded"

## 代码

``` Javascript
var DelRepeatAlpha = function(str){
    str = str.replace(/([a-z])\1*([a-z])\2*([a-z])\3*/g,"$1$2$3")
}
```
