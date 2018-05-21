1. if 表达式

* Null总是为假（false）
* Undefined总是为假（false）
* Number+0，-0 或是 NaN 的时候为假，其它值为真
* String空字符串的时候为假，其它值为真
* Object总是为真（true）

2. 针对node饿了么面试回答下面问题
JavaScript基础问题
*JS类型判断  参考：http://www.cnblogs.com/dushao/p/5999563.html
*作用域      参考：《你不知道的javascript》上卷
*引用传递    参考：http://www.cnblogs.com/refe/p/5101744.html
*内存        参考：https://eggggger.xyz/2016/10/22/node-gc/
*ES6 新特性  参考：http://es6.ruanyifeng.com/


3. 时间处理函数
时间格式化  
/* 
*   功能:实现时间格式化d功能. 
*   参数:fmt,字符串表达式，表示要添加的时间间隔. yyyy-MM-dd   yyyy-MM-dd hh:mm:ss
*   月(M)、日(d)、小时(h)、分(m)、秒(s)、季度(q) 可以用 1-2 个占位符，年(y)可以用 1-4 个占位符，毫秒(S)只能用 1 个占位符(是 1-3 位的数字) 
*   返回:新的时间对象. 
*   例子： 
*   (new Date()).Format("yyyy-MM-dd hh:mm:ss.S") ==> 2006-07-02 08:09:04.423 
*   (new Date()).Format("yyyy-M-d h:m:s.S")      ==> 2006-7-2 8:9:4.18 
*---------------   DateAdd(interval,number,date)   ----------------- 
*/
Date.prototype.Format = function(fmt) {
    var o = {
        "M+": this.getMonth() + 1, //月份 
        "d+": this.getDate(), //日 
        "h+": this.getHours(), //小时 
        "m+": this.getMinutes(), //分 
        "s+": this.getSeconds(), //秒 
        "q+": Math.floor((this.getMonth() + 3) / 3), //季度 
        "S": this.getMilliseconds() //毫秒 
    };
    if (/(y+)/.test(fmt)) fmt = fmt.replace(RegExp.$1, (this.getFullYear() + "").substr(4 - RegExp.$1.length));
    for (var k in o)
        if (new RegExp("(" + k + ")").test(fmt)) fmt = fmt.replace(RegExp.$1, (RegExp.$1.length == 1) ? (o[k]) : (("00" + o[k]).substr(("" + o[k]).length)));
    return fmt;
};

时间加减
/* 
*   功能:实现JavaScript的DateAdd功能. 
*   参数:interval,字符串表达式，表示要添加的时间间隔. 
*   参数:number,数值表达式，表示要添加的时间间隔的个数. 
*   参数:date,时间对象. 
*   返回:新的时间对象. 
*   var   now   =   new   Date(); 
*   var   newDate   =   DateAdd( "d ",5,now); 
*---------------   DateAdd(interval,number,date)   ----------------- 
*/
function DateAdd(interval, number, date) {
switch (interval) {
    case "y":
        {
            date.setFullYear(date.getFullYear() + number);
            return date;
            break;
        }
    case "q":
        {
            date.setMonth(date.getMonth() + number * 3);
            return date;
            break;
        }
    case "m":
        {
            date.setMonth(date.getMonth() + number);
            return date;
            break;
        }
    case "w":
        {
            date.setDate(date.getDate() + number * 7);
            return date;
            break;
        }
    case "d":
        {
            date.setDate(date.getDate() + number);
            return date;
            break;
        }
    case "h":
        {
            date.setHours(date.getHours() + number);
            return date;
            break;
        }
    case "m":
        {
            date.setMinutes(date.getMinutes() + number);
            return date;
            break;
        }
    case "s":
        {
            date.setSeconds(date.getSeconds() + number);
            return date;
            break;
        }
    default:
        {
            date.setDate(d.getDate() + number);
            return date;
            break;
        }
}
}


