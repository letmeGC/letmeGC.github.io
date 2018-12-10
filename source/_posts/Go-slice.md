---
title: Go-slice
date: 2018-12-06 18:02:34
categories: "Go"
---

### 底层实现

```
切片的底层是一个数组，切片的表层是一个包含三个变量的结构体
type slice struct {
  array unsafe.Pointer
  length int
  capcity int
}
```
{% asset_img slice.jpg 切片 %}

### 对比数组
```
//数组
array:=[5]int{4:1}
//切片
slice:=[]int{4:1}
数组是值类型，将一个数组赋值给另一个数组时，传递的是一份拷贝。
切片是引用类型，切片包装的数组称为该切片的底层数组。

小例子 : 
func main() {
	//a是一个数组，注意数组是一个固定长度的，初始化时候必须要指定长度，不指定长度的话就是切片了
	a := [3]int{1, 2, 3}
	//b是数组，是a的一份拷贝
	b := a
	//c是切片，是引用类型，底层数组是a
	c := a[:]
	for i := 0; i < len(a); i++ {
		a[i] = a[i] + i
	}
	//改变a的值后，b是a的拷贝，b不变，c是引用，c的值改变
	fmt.Println(a) //[1 3 5]
	fmt.Println(b) //[1 2 3]
	fmt.Println(c) //[1 3 5]

}
```
### 切片操作 [make append]
```
func main() {
	var t = make([]int, 0, 4)
	var s = make([]int, 0, 4)
	var z = make([]int, 0, 4)
	fmt.Printf("addr:%p \t\tlen:%v content:%v\n", t, len(t), t)
	fmt.Printf("addr:%p \t\tlen:%v content:%v\n", s, len(s), s)
	fmt.Printf("addr:%p \t\tlen:%v content:%v\n", z, len(z), z)
	//<=cap(s) 容量内
	t = append(s, 1, 2, 3, 4)
	fmt.Println(t)
	fmt.Println(s)
	fmt.Printf("addr:%p \t\tlen:%v content:%v\n", t, len(t), t)
	fmt.Printf("addr:%p \t\tlen:%v content:%v\n", s, len(s), s)
    //>cap(s) 超出容量
	z = append(s, 1, 2, 3, 4, 5)
	fmt.Println(z)
	fmt.Println(s)
	fmt.Printf("addr:%p \t\tlen:%v content:%v\n", z, len(z), z)
	fmt.Printf("addr:%p \t\tlen:%v content:%v\n", s, len(s), s)
}

输出 : 

addr:0xc0000480c0 		len:0 content:[]
addr:0xc0000480e0 		len:0 content:[]
addr:0xc000048100 		len:0 content:[]
[1 2 3 4]
[]
addr:0xc0000480e0 		len:4 content:[1 2 3 4]
addr:0xc0000480e0 		len:0 content:[]
[1 2 3 4 5]
[]
addr:0xc00007a080 		len:5 content:[1 2 3 4 5]
addr:0xc0000480e0 		len:0 content:[]

解析 :
切片是一段数组的描述，包括指向数组的指针，数组段落的长度，以及充许的最大长度。
make初始化切片，是先创建一个底层数组，再创建一个地址指向该数组的切片并返回
（切片为什么还要有最大长度，即容量，这是Go语言本身的需要，不然它的make函数没有办法工作)

情景1:

//<=cap(s) 容量内 t = append(s, 1, 2, 3, 4)
t 与 s 共享底层数组 所以地址一样 

情景2:

//>cap(s) 超出容量 z = append(s, 1, 2, 3, 4, 5)
t 与 s 指向的数组地址不一样了;
<<< 
append主要用于给切片追加元素;
如果该切片存储容量cap足够，就直接追加，长度len变长；
如果容量不足，就会重新开辟内存，创建新的底层数组，并将之前的元素和新的元素一同拷贝进去;
```