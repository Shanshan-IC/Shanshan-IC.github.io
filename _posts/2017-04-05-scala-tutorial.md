---
layout:     post
title:      "Scala Tutorial"
category:   Scala
tags:   Scala
---

* content
{:toc}

## Scala Tutorial

```scala
// first scala

object hello {
  def main(args: Array[String]): Unit = {  
      println("hello\tworld\n")  
  }  
}

// synatix
/*
Scala 基本语法需要注意以下几点：
区分大小写 -  Scala是大小写敏感的，这意味着标识Hello 和 hello在Scala中会有不同的含义。
类名 - 对于所有的类名的第一个字母要大写。

如果需要使用几个单词来构成一个类的名称，每个单词的第一个字母要大写。

示例：class MyFirstScalaClass
方法名称 - 所有的方法名称的第一个字母用小写。

如果若干单词被用于构成方法的名称，则每个单词的第一个字母应大写。

示例：def myMethodName()
程序文件名 - 程序文件的名称应该与对象名称完全匹配。

保存文件时，应该保存它使用的对象名称（记住Scala是区分大小写），并追加".scala"为文件扩展名。 （如果文件名和对象名称不匹配，程序将无法编译）。

示例: 假设"HelloWorld"是对象的名称。那么该文件应保存为'HelloWorld.scala"
def main(args: Array[String]) - Scala程序从main()方法开始处理，这是每一个Scala程序的强制程序入口部分。
*/


//换行--- ; 


//package
package test
class HelloWorld
//import all 
import test._


//variable
/*
Byte	8位有符号补码整数。数值区间为 -128 到 127
Short	16位有符号补码整数。数值区间为 -32768 到 32767
Int	32位有符号补码整数。数值区间为 -2147483648 到 2147483647
Long	64位有符号补码整数。数值区间为 -9223372036854775808 到 9223372036854775807
Float	32位IEEE754单精度浮点数
Double	64位IEEE754单精度浮点数
Char	16位无符号Unicode字符, 区间值为 U+0000 到 U+FFFF
String	字符序列
Boolean	true或false
Unit	表示无值，和其他语言中void等同。用作不返回任何结果的方法的结果类型。Unit只有一个实例值，写成()。
Null	null 或空引用
Nothing	Nothing类型在Scala的类层级的最低端；它是任何其他类型的子类型。
Any	Any是所有其他类的超类
AnyRef	AnyRef类是Scala里所有引用类(reference class)的基类
*/

//变量声明

var str : String = "Test"
var num : Int = 123
var flo : Float = 12.3f
val bo : Boolean = true


//访问修饰符：private, protected, public


//运算符和C++的都一样


//if, else if 和 C++ 都一样
// scala 里没有break和continue,但有一个Breaks类
import scala.util.control._


object hello {
  def main(args: Array[String]): Unit = {  
      println("hello\tworld\n")
      var str : String = "Test"
      var num : Int = 13
      var flo : Float = 12.3f
      val bo : Boolean = true
      var loop = new Breaks;
      loop.breakable {
        for (num <- 13 to 17) {
          println(num)
          if (num == 15)
            loop.break;
        }
      }
  }  
}


//function

object func {
  def divideInt(a : Int, b : Int) : Int = {
    var sum : Int = 0
    sum = a * b
    return sum
    
  }
  def emptyRes(a : Int) : Unit = {
    println(a)
 
  }
  
  def main(args: Array[String]) {
    println(divideInt(1, 2))
  }
}
//unit means return emptyRes

// scala 的string是不可变的，所以要操作的话，只能使用String Builder 类
object str {
  def main(args: Array[String]) {
    var buf = new StringBuilder
    buf += 'a'
    buf ++= "ahdhd"
    println(buf.toString)
  }
}

// 'a'字符用+=，"aaaa"字符串用++=

// scala 闭包和Python的匿名函数是一个意思


//Array
import Array._

object arrayExample {
    var z = Array("cece", "shanshan", "haha")
    var z2 = new Array[String](3)
    z(0) = "cece"
    z(1) = "shanshan"
    z(2) = "haha"
    for (i <- 0 to (z.length - 1)) {
      println(z(i))
    }
    
    // 多维数组
    var myMatrix = ofDim[Int](3,3)
    for (i <- 0 to 2) {
      for (j <- 0 to 2) {
        print(myMatrix(i)(j))
      }
      println()
    }
}

//Scala里有和Python中数组相似的函数
//例如concat，range, apply, fill


// collection
// 定义整型 List
val x = List(1,2,3,4)

// 定义 Set
var x = Set(1,3,5,7)

// 定义 Map
val x = Map("one" -> 1, "two" -> 2, "three" -> 3)

// 创建两个不同类型元素的元组
val x = (10, "Runoob")

// 定义 Option
val x:Option[Int] = Some(5)



// 迭代器
val ita = Iterator(20,40,2,50,69, 90)
while (ita.hasNext) {
  println(ita.next())
}
// 长度
println("size is: " + ita.size)
println("最大元素是：" + ita.max)



// 类
import java.io._

class Point(val xc: Int, val yc: Int) {
   var x: Int = xc
   var y: Int = yc
   def move(dx: Int, dy: Int) {
      x = x + dx
      y = y + dy
      println ("x 的坐标点 : " + x);
      println ("y 的坐标点 : " + y);
   }
}

class Location(override val xc: Int, override val yc: Int,
   val zc :Int) extends Point(xc, yc){
   var z: Int = zc

   def move(dx: Int, dy: Int, dz: Int) {
      x = x + dx
      y = y + dy
      z = z + dz
      println ("x 的坐标点 : " + x);
      println ("y 的坐标点 : " + y);
      println ("z 的坐标点 : " + z);
   }
}

object Test {
   def main(args: Array[String]) {
      val loc = new Location(10, 20, 15);

      // 移到一个新的位置
      loc.move(10, 10, 5);
   }
}


/* 在 Scala 中，是没有 static 这个东西的，但是它也为我们提供了单例模式的实现方法，那就是使用关键字 object。
Scala 中使用单例模式时，除了定义的类之外，还要定义一个同名的 object 对象，它和类的区别是，object对象不能带参数。
当单例对象与某个类共享同一个名称时，他被称作是这个类的伴生对象：companion object。你必须在同一个源文件里定义类和它的伴生对象。类被称为是这个单例对象的伴生类：companion class。类和它的伴生对象可以互相访问其私有成员。*/


// 伴生对象
// 私有构造方法
class Marker private(val color:String) {

  println("创建" + this)
  
  override def toString(): String = "颜色标记："+ color
  
}

// 伴生对象，与类共享名字，可以访问类的私有属性和方法
object Marker{
  
    private val markers: Map[String, Marker] = Map(
      "red" -> new Marker("red"),
      "blue" -> new Marker("blue"),
      "green" -> new Marker("green")
    )
    
    def apply(color:String) = {
      if(markers.contains(color)) markers(color) else null
    }
  
    
    def getMarker(color:String) = { 
      if(markers.contains(color)) markers(color) else null
    }
    def main(args: Array[String]) { 
        println(Marker("red"))  
        // 单例函数调用，省略了.(点)符号  
		println(Marker getMarker "blue")  
    }
}


// trial 相当于是Java的抽象类
trait Equal {
  def isEqual(x: Any): Boolean
  def isNotEqual(x: Any): Boolean = !isEqual(x)
}

class Point(xc: Int, yc: Int) extends Equal {
  var x: Int = xc
  var y: Int = yc
  def isEqual(obj: Any) =
    obj.isInstanceOf[Point] &&
    obj.asInstanceOf[Point].x == x
}

object Test {
   def main(args: Array[String]) {
      val p1 = new Point(2, 3)
      val p2 = new Point(2, 4)
      val p3 = new Point(3, 3)

      println(p1.isNotEqual(p2))
      println(p1.isNotEqual(p3))
      println(p1.isNotEqual(2))
   }
}



// 模式匹配

object Test {
   def main(args: Array[String]) {
      println(matchTest(3))

   }
   def matchTest(x: Int): String = x match {
      case 1 => "one"
      case 2 => "two"
      case _ => "many"
   }
}


// 正则表达式
import scala.util.matching.Regex

object Test {
   def main(args: Array[String]) {
      val pattern = new Regex("(S|s)cala")  // 首字母可以是大写 S 或小写 s
      val str = "Scala is scalable and cool"
      
      println((pattern findAllIn str).mkString(","))   // 使用逗号 , 连接返回结果
   }
}

//异常处理
import java.io.FileReader
import java.io.FileNotFoundException
import java.io.IOException

object Test {
   def main(args: Array[String]) {
      try {
         val f = new FileReader("input.txt")
      } catch {
         case ex: FileNotFoundException =>{
            println("Missing file exception")
         }
         case ex: IOException => {
            println("IO Exception")
         }
      }
   }
}



// IO
//屏幕输入
object Test {
   def main(args: Array[String]) {
      print("请输入菜鸟教程官网 : " )
      val line = Console.readLine
      
      println("谢谢，你输入的是: " + line)
   }
}

//文件输入

import scala.io.Source

object Test {
   def main(args: Array[String]) {
      println("文件内容为:" )

      Source.fromFile("test.txt" ).foreach{ 
         print 
      }
   }
}
```