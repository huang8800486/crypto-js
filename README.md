* crypto-js下载包 https://code.google.com/archive/p/crypto-js/downloads
* crypto-js.js https://unpkg.com/crypto-js@3.1.9-1/crypto-js.js
* JavaScript Crypto-JS 使用手册 https://blog.zhengxianjun.com/2015/05/javascript-crypto-js/

``` bash
* Base64编码及其作用
* @base64其实不是安全领域下的加密解密算法。base64编码过后原文也变成不能看到的字符格式, 但可以还原
* @1.Base64编码的作用：由于某些系统中只能使用ASCII字符。Base64就是用来将非ASCII字符的数据转换成ASCII字符的一种方法。它使用下面表中所使用的字符与编码。
* @2.虽然有时候经常看到所谓的base64加密解密。其实base64只能算是一个编码算法，对数据内容进行编码来适合传输。虽然base64编码过后原文也变成不能看到的字符格式，但是这种方式很初级，很简单。
* @3.一种比较可靠的加密方法，能够对电子邮件的明文进行转换，至少要得出一个无法 被别人一眼就看出内容来的东西，而且编码/解码的速度还要足够快。
* @4.Base64就是在这种背景下产生的加密方法。它的特点是：1、速度非常快。2、能够将字符串A转换成字符串B，而且如果你光看字符串B，是绝对猜不出字符串A的内容来的。
```
#md5加密
``` bash
!(function ($) {
    var user_key = "at_user_key";
    jQuery.extend({
        /*
        * MD5生成签名
        */
        "toSign": function (str) {
            try {
                str = str + getKey();
                return CryptoJS.MD5(str).toString();
            } catch (e) {
                return "";
            }

        },
        /*
        * json对象转码Base64
        */
        "toBase64": function (obj) {
            try{
                var str = JSON.stringify(obj);
                return CryptoJS.enc.Base64.stringify(CryptoJS.enc.Utf8.parse(str));
            }catch (e) {
                return "";
            }
        },

        /*
        * Base64解码成json对象
        */
        "Base64ToObj": function (str) {
            try {
                var words = CryptoJS.enc.Base64.parse(str);
                var jsonStr = words.toString(CryptoJS.enc.Utf8);

                return JSON.parse(jsonStr);
            } catch (e) {
                return null;
            }

        }
    });

    //获取用户key
    function getKey() {
        try {
            var key = getCookie(user_key);
            return key;
        } catch (e) {
            return "";
        }
    }
})(window.jQuery);

var param = {
    "name": "Alan"
}
// 使用base64简单加密
console.log($.toBase64(param));

// 使用base64解密
console.log($.Base64ToObj($.toBase64(param)))

// 使用MD5 base64加密
var param2 = {
    "name": "Tao"
}
var strObgect = $.toBase64(param2);
var strSign = $.toSign(strObgect);

console.log(strSign);

```
