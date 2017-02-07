# JS-Practice
### 判断一个单词是否是回文

// 所谓回文字符串，就是一个字符串，从左到右读和从右到左读是完全一样的。比如"level"

```
function checkHuiWen(str){
	return str == str.split('').reverse().join('')
}
```



### 数组去重

// 比如输入: [1,13,24,11,11,14,1,2] 
// 输出: [1,13,24,11,14,2]
// 需要去掉重复的11 和 1 这两个元素。

```
//双循环
function arrUnique0(arr){	
	let newArr = []
	for(let i=0,l=arr.length;i<l;i++){	
		let key = true	
		for(let j=0,l=newArr.length;j<l;j++){			
			if(arr[i] == newArr[j]){
				key = false
			}
		}	
		if(key){
			newArr.push(arr[i])
		}
	}	
	return newArr
} 

//对象属性唯一性判断
function arrUnique1(arr){
	let obj = {}
	let newArr = []
	for(let i=0,l=arr.length;i<l;i++){
		let v = arr[i]
		if(!obj[v]){
			newArr.push(v)
			obj[v] = true
		}
	}	
	return newArr
} 

//indexof判断
//对象属性唯一性判断
function arrUnique2(arr){
	let newArr = []
	for(let i=0,l=arr.length;i<l;i++){		
		if(newArr.indexOf(arr[i]) == -1){
			newArr.push(arr[i])
		}
	}
	
	return newArr
} 
```



### 创建一个数组含有100个值为0元素

```
let arr = new Array(100)
arr.join('0').split('')
```



### 删除数组的第二项和第三项，再将最后一个元素压入数组头部

```
arr.splice(1,2)
arr.unshift(arr.pop())
```



### 填空题，实现输出['c','d']

// var data = {a:1,b:2,c:3,d:4};
// Object.keys(data).filter(function(x){
//   return ______;
// })

```
Object.keys(data).filter(function(x){
  return x > 'b';
})
```



### 代码实现如下要求

// var arr = [1,2];
// var new_arr;
// 要求实现:
// new_arr === arr ==>false
// new_arr[0] == arr[0]; ==>true
// new_arr[1] == arr[1]; ==>true

```
var new_arr = arr.slice();
//or
var new_arr = arr.concat();
```



### 随机获取数组中的元素

```
function getRandomFormArr(arr){
	return arr[Math.floor(Math.random()*arr.length)]
}
```



### 随机选取5-105中的10个不重复随机整数，然后按从小到大排序

```
function getNum(){
	let arr = []
	for(let i=5;i<=105;i++){
		arr.push(i)
	}
	return arr.sort(function(a,b){return Math.random()>0.5}).slice(0,10).sort(function(a,b){return a-b});
}
```



### 获取数组元素最大差值

//[2,4,6,9]返回7

```
function getMaxProfit(arr){
	return Math.max.apply(Math,arr) - Math.min.apply(Math,arr)
}
```



### 深度克隆对象

```
function cloneObj(obj){
    let str, newobj = obj.constructor === Array ? [] : {};
    if(typeof obj !== 'object'){
        return obj;
    } else if(window.JSON){
        str = JSON.stringify(obj), //系列化对象
        newobj = JSON.parse(str); //还原
    } else {
        for(var i in obj){
            newobj[i] = typeof obj[i] === 'object' ?
            cloneObj(obj[i]) : obj[i];
        }
    }
    return newobj;
}
```



### 统计字符串出现次数最多的字母

```
function getMaxWord(str){
	let obj = {}	
	for(let i in str){
		let word = str[i]		
		if(obj[word]){
			obj[word]++
		}else{
			obj[word] = 1
		}
	}

	return  (function(obj){
				let maxWord = ''
				let maxTimes = 1
				for(let i in obj){
					if(obj[i] > maxTimes){
						maxWord = i
						maxTimes = obj[i]
					}
				}
				return maxWord
			})(obj)
	
}
```



### 实现getType获取数据类型

```
function getType(a){
	if(a === null)return 'null'
	return Object.prototype.toString.call(a).slice(8,-1).toLowerCase()
}
```



### url参数解析为对象

//a.html?a=1&b=2 返回{a:1,b:2}

```
function getUrlParam(urlStr){
	let url = urlStr || window.location.href
	if(url.indexOf('?') == -1)return null

	let arr = url.split('?')[1].split('&')
	let obj = {}
	for(let i in arr){
		let _arr = arr[i].split('=')
		obj[_arr[0]] = _arr[1]
	}
	return obj
}
```



### 创建“原生”（native）方法

//给字符串对象定义一个repeatify功能。当传入一个整数n时，它会返回重复n次字符串的结果

```
String.prototype.repeatify = function(n){
	return (new Array(n+1)).join(this)
}
```



### 实现冒泡排序

```
function mppx(arr){
	for(let i=0,l=arr.length-1;i<l;i++){
		for(let j=0;j<arr.length-i-1;j++){
			if(arr[j] > arr[j+1]){
				let a = arr[j]
				arr[j] = arr[j+1]
				arr[j+1] = a
			}
		}
	}
}

//优化版
function mppx(arr){
	for(let i=0,l=arr.length-1;i<l;i++){
		let key = 0
		for(let j=0;j<arr.length-i-1;j++){
			if(arr[j] > arr[j+1]){
				let a = arr[j]
				arr[j] = arr[j+1]
				arr[j+1] = a
				key = 1
			}
		}
		if(key == 0)return
	}	
}
```



### 实现快速排序

```
function kspx(arr){
	if (arr.length <= 1) { return arr } 
	let middleVal = arr.splice(Math.floor(arr.length/2),1)[0]
	let left = [],right = []
	for(let i in arr){
		if(arr[i] < middleVal){
			left.push(arr[i])
		}else{
			right.push(arr[i])
		}
	}
	return kspx(left).concat(middleVal,kspx(right))
}

```



### 实现二分查找

//传递一个已排序数组和值，通过二分搜索返回该值在数组中的索引

```
function efcz(arr,val){
	let low = 0
	let high = arr.length
	while(low < high){
		let mid = parseInt((high + low) / 2);		
		if(val < arr[mid]){
			high = mid
		}else if(val > arr[mid]){
			low = mid
		}else{
			return mid
		}
	}
	return -1
}
```



### 代理console.log

//实现log之前加上'log start'字符串

```
function log(){	
	console.log.apply(console,['log start:'].concat([].slice.call(arguments)))
}
```



### promise红绿灯问题

//红灯三秒亮一次，绿灯一秒亮一次，黄灯两秒亮一次，如何让三个灯不断交替重复亮

```
function red(){
	console.log('red')
}

function green(){
	console.log('green')
}

function yellow(){
	console.log('yellow')
}

```

事件队列实现

```
var event = {
	tasks : [],
	push : function(fn){
		this.tasks.push(fn)
		return this
	},
	go : function(){		
		let fn = this.tasks.shift()
		fn && fn()
	}
}

//延时执行fn
function sleep(fn,time){
	setTimeout(function(){
		fn()
		event.go()
	},time)
}

function show(){
	event.push(function(){
		sleep(red,3000)
	}).push(function(){
		sleep(green,2000)
	}).push(function(){
		sleep(yellow,1000)
	}).push(function(){
		show()
	}).go()
}
```

promise实现

```
function doPromise(fn,time){
	return new Promise(function(resolve,reject){
		setTimeout(function(){
			fn()
			resolve()
		},time)	
	})
}

function show(){
	doPromise(red,3000).then(function(){
		return doPromise(green,2000)
	}).then(function(){
		return doPromise(yellow,1000)
	}).then(function(){
		show()
	})
}
```

