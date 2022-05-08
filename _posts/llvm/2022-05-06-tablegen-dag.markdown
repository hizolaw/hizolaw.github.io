# tablegen的dag怎么玩


  首先，我们先看一下dag的语法，一个dag的instance语法是： ( operator argument1, argument2, … )，其中，operator必须是一个record，argument可以是0个或者多个，同时dag能嵌套；argument的格式如下所示：

  Format      | Meaning
  value	      | argument value
  value:name  | argument value and associated name
  name	      | argument name with unset (uninitialized) value
  
  其中，value可以是tablegen的所有的value类型，而name则是一个TokVarName，也就是必须以$开头的token。

  我们来看一个例子:
```
  def op1;
  def op2;
  def i32:
  
  def Example {
    dag x = (op1 $foo, (op2 i32:$bar, "Hi"));
  }
```
  在这个例子中，dag x由两个dag node构成，第一个的operator是op1 record，它有两个参数，第一个只有名字$foo而没有value，第二个参数则是第二个dag node；第二个dag node也是由两个参数构成，第一个参数value是i32，名字是$bar，第二个参数只有value"Hi"。
