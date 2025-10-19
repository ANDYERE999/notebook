# 类型推断(强类型) 类型断言
```Typescript
let str = '123'
str = 1 // 报错
// 等价于
let str: string = '123'

// 类型断言
let numArr = [1,2,3]
const result = numArr.find(item => item > 2)
result = result * 5 // 会报错，因为认为result可能是undifined

let numArr = [1,2,3]
const result = numArr.find(item => item > 2) as number // 此处的as可以理解为assertation，断言result是number
result = result * 5 
```
PS: let表示变量，const表示常量
# 基础类型和联合类型
```Typescript
let myNum: number = 10
let myStr: string = 'abc'
let myBool: boolean = true
let nu: null = null
let un: undifined = undifined

// 联合类型：一个变量可能是多个类型
let myVariable: string | null = null
// 联合类型还可以用来作为限定
let myVariable2: 1 | 2 | 'abc' = 'abc' // 只能是1,2,'abc'否则就会报错 
```
# 数据容器：数组、元组、枚举
## 数组：
- 数组可以存储不同类型的数据
- 可以使用`:`进行约束
```Typescript
let arr = [1,2,'abc']
let arr: number[] = [1,2,3]
let arr: number[] | string[]=[1,2,3] //表示数组要么是number类型的要么是string类型的，不能表示数组同时有number和string
let arr: Array[string] = ['a','b','c']
```
## 元组：
- 限制了存储数据的个数
- 限制了每个位置存储的数据类型
- 最后几位的数据可以通过加上`?`来标记该数据是可选的
```Typescript
let t1: [number,number|string|boolean,number] = [0,false,1]
t1[0]=114
let t1: [number,number|string|boolean,number?] = [0,false]
```
## 枚举
- 使用关键词enum
```Typescript
enum myEnum{
	Perfect,
	Great,
	Good,
	Bad,
	Miss
}
console.log(myEnum.Perfect)
console.log(myEnum[0])
```
# 函数
- 函数需要给参数分配类型(*默认情况下，实际上Typescript可以进行配置*)
- 返回值也可以进行分配
```Typescript
function myFunc(a: number, b: number): number{
	return a+b
}
```
- 没有默认值的**可选参数**后加上`?`来标记，必须放在必选参数的后面
- 有默认值的**可选参数**直接`=xxx`
```Typescript
function myFunc(a: number, b?: number): number{
	return a+1
}
function myFunc(a: number = 100, b: number): number{// 实际上可以直接写a=100,因为类型自动推断
	return a+b
}
```
剩余参数：必须是一个数组结构
使用rest...: number\[\] 
```Typescript
function myFunc(a: number, b: string, ...rest: boolean[]): number{
	return a+b
}
let n1 = function(123,'abc',true, false, true, true, false)
```
# 接口
- 对接口进行复用来防止代码书写错误
```Typescript
interface Entity {
	type: string,
	health: number
}
// 复用，此时会进行检查防止出错，在这里必须写type和health两个变量并且符合类型
let Steve: Entity = {
	type: 'Player',
	health: 100
}
```
# 类型别名
```Typescript
let playerName1: number | string = 'Steve'
let playerName2: number | string = 'Alex'
let playerName3: number | string = 114514
```
显然，在上述情况下每一次都写`number | string`太麻烦了，我们可以使用一个类型别名表示`number | string`
```Typescript
type PlayerName = number | string
let playerName1: PlayerName = 'Steve'
let playerName2: PlayerName = 'Alex'
let playerName3: PlayerName = 114514
```
# 泛型
- 类似于C++中的模版
- 得益于类型推断功能，使用时会更轻松
```Typescript
function plus<T>(a:T, b:T, ...rest:T[]):T[] {
	return [a,b]
}

let arr1=plus<number>(1,2)
let arr2=plus('abc','bcd') // 类型自动推断
```