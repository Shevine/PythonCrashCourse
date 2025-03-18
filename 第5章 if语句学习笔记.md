# 第5章 if语句学习笔记
## 1  一个简单示例
在处理列表元素时，`if`语句可用于针对不同元素执行不同操作。例如遍历汽车列表，对于大多数汽车，以首字母大写的方式打印其名称，而对于汽车名`'bmw'`，以全大写的方式打印：
```python
cars = ['audi', 'bmw', 'toyota']
for car in cars:
    if car == 'bmw':
        print(car.upper())
    else:
        print(car.title())
```
上述代码中，循环遍历列表`cars`，对每个元素进行判断，根据判断结果执行不同的打印操作。

## 2  条件测试
每条`if`语句的核心是一个值为`True`或`False`的表达式，即条件测试。Python根据条件测试的结果决定是否执行`if`语句中的代码。
### 2.1  检查是否相等
使用两个等号（\=\=）检查变量的值是否与特定值相等。例如：
```python
car = 'bmw'
print(car == 'bmw')  # 输出：True
```
一个等号用于赋值，两个等号用于判断是否相等。

### 2.2  检查是否相等时不考虑大小写
Python检查相等时区分大小写，若想不考虑大小写进行比较，可使用`lower()`函数将变量值转换为小写后再比较。例如：
```python
car = 'Audi'
print(car.lower() == 'audi')  # 输出：True
print(car)  # 输出：Audi，原变量值不变
```
该方法常用于确保用户名等数据的一致性，避免因大小写不同而被视为不同值。

### 2.3  检查是否不相等
使用惊叹号和等号（`!=`）判断两个值是否不等。例如：
```python
requested_topping ='mushrooms'
if requested_topping != 'anchovies':
    print("Hold the anchovies!")
```
当`requested_topping`的值不是`'anchovies'`时，执行`if`语句中的代码。

### 2.4  比较数字
可使用各种数学比较运算符（`<`、`<=`、`>`、`>=`）检查数值。例如：
```python
age = 18
print(age == 18)  # 输出：True
print(age < 21)  # 输出：True
```
在`if`语句中，可根据具体需求使用这些比较运算符进行条件判断。

### 2.5  检查多个条件
1. **使用`and`检查多个条件**：使用关键字`and`将两个条件测试合而为一，只有当两个条件都为`True`时，整个表达式才为`True`。例如：
```python
age_0 = 22
age_1 = 18
print(age_0 >= 21 and age_1 >= 21)  # 输出：False
age_1 = 22
print(age_0 >= 21 and age_1 >= 21)  # 输出：True
```
2. **使用`or`检查多个条件**：关键字`or`用于检查多个条件，只要至少有一个条件满足，整个测试就通过。仅当两个测试都未通过时，表达式才为`False`。例如：
```python
age_0 = 18
age_1 = 22
print(age_0 >= 21 or age_1 >= 21)  # 输出：True
age_0 = 18
age_1 = 18
print(age_0 >= 21 or age_1 >= 21)  # 输出：False
```

### 2.6  检查特定值是否包含在列表中
使用关键字`in`判断特定的值是否已包含在列表中。例如：
```python
requested_toppings = ['mushrooms', 'onions', 'pineapple']
print('mushrooms' in requested_toppings)  # 输出：True
print('pepperoni' in requested_toppings)  # 输出：False
```
常用于检查用户输入的值是否在预定义列表中。

### 2.7  检查特定值是否不包含在列表中
使用关键字`not in`确定特定的值未包含在列表中。例如：
```python
banned_users = ['andrew', 'carolina', 'david']
user ='marie'
if user not in banned_users:
    print(user.title() + ", you can post a response if you wish.")
```
当`user`的值不在`banned_users`列表中时，执行相应代码。

### 2.8  布尔表达式
布尔表达式是条件测试的别名，其结果要么为`True`，要么为`False`。常用于记录程序状态或重要条件，如：
```python
game_active = True
can_edit = False
```

## 3  if语句
### 3.1  简单的if语句
最简单的`if`语句只有一个测试和一个操作。例如：
```python
age = 19
if age >= 18:
    print("You are old enough to vote!")
```
当条件测试`age >= 18`为`True`时，执行缩进的`print`语句。

### 3.2  if-else语句
`if-else`语句用于在条件测试通过时执行一个操作，未通过时执行另一个操作。例如：
```python
age = 17
if age >= 18:
    print("You are old enough to vote!")
    print("Have you registered to vote yet?")
else:
    print("Sorry, you are too young to vote.")
    print("Please register to vote as soon as you turn 18!")
```
根据`age`的值，执行不同的代码块。

### 3.3  if-elif-else结构
`if-elif-else`结构用于检查超过两个的情形。Python依次检查每个条件测试，直到遇到通过的条件测试，然后执行紧跟其后的代码，并跳过余下的测试。例如，根据年龄段收费的游乐场示例：
```python
age = 12
if age < 4:
    price = 0
elif age < 18:
    price = 5
else:
    price = 10
print("Your admission cost is $" + str(price) + ".")
```
根据`age`的值确定门票价格。

### 3.4  使用多个elif代码块
可根据需要使用任意数量的`elif`代码块。例如，给游乐场的老年人打折：
```python
age = 70
if age < 4:
    price = 0
elif age < 18:
    price = 5
elif age < 65:
    price = 10
else:
    price = 5
print("Your admission cost is $" + str(price) + ".")
```

### 3.5  省略else代码块
在有些情况下，使用`elif`语句处理特定情形比使用`else`代码块更清晰。例如：
```python
age = 12
if age < 4:
    price = 0
elif age < 18:
    price = 5
elif age < 65:
    price = 10
elif age >= 65:
    price = 5
print("Your admission cost is $" + str(price) + ".")
```
这样每个代码块都仅在通过相应测试时才执行，可避免`else`代码块可能引入的无效数据问题。

### 3.6  测试多个条件
当需要检查多个条件，且每个条件都可能为`True`时，应使用一系列不包含`elif`和`else`代码块的简单`if`语句。例如，处理比萨配料的示例：
```python
requested_toppings = ['mushrooms', 'extra cheese']
if'mushrooms' in requested_toppings:
    print("Adding mushrooms.")
if 'pepperoni' in requested_toppings:
    print("Adding pepperoni.")
if 'extra cheese' in requested_toppings:
    print("Adding extra cheese.")
print("\nFinished making your pizza!")
```
每个`if`语句都会独立进行测试，确保每个配料都能被正确处理。

## 4  使用if语句处理列表
### 4.1  检查特殊元素
在遍历列表时，可使用`if`语句检查特殊元素并进行特殊处理。例如，制作比萨时处理青椒缺货的情况：
```python
requested_toppings = ['mushrooms', 'green peppers', 'extra cheese']
for requested_topping in requested_toppings:
    if requested_topping == 'green peppers':
        print("Sorry, we are out of green peppers right now.")
    else:
        print("Adding " + requested_topping + ".")
print("\nFinished making your pizza!")
```
通过这种方式，可针对列表中的特殊元素进行相应处理。

### 4.2  确定列表不是空的
在运行`for`循环前，检查列表是否为空很重要。例如：
```python
requested_toppings = []
if requested_toppings:
    for requested_topping in requested_toppings:
        print("Adding " + requested_topping + ".")
    print("\nFinished making your pizza!")
else:
    print("Are you sure you want a plain pizza?")
```
当列表为空时，执行相应提示；列表不为空时，正常处理列表元素。

### 4.3  使用多个列表
通过使用多个列表和`if`语句，可处理更复杂的情况。例如，判断顾客点的配料是否在供应列表中：
```python
available_toppings = ['mushrooms', 'olives', 'green peppers', 'pepperoni', 'pineapple', 'extra cheese']
requested_toppings = ['mushrooms', 'french fries', 'extra cheese']
for requested_topping in requested_toppings:
    if requested_topping in available_toppings:
        print("Adding " + requested_topping + ".")
    else:
        print("Sorry, we don't have " + requested_topping + ".")
print("\nFinished making your pizza!")
```
该代码可根据供应列表和顾客点单列表，正确处理各种配料情况。

## 5  设置if语句的格式
在条件测试的格式设置方面，PEP 8建议在比较运算符（如\==、`>=`、`<=`）两边各添加一个空格，如`if age < 4:`比`if age<4:`更易读。这种空格设置不会影响代码解读，但可提高代码的可读性。

## 6  小结
在本章中，学习了条件测试的多种方式，包括检查相等、不等、比较数字、检查多个条件以及检查特定值是否在列表中或不在列表中；掌握了`if`语句、`if-else`语句和`if-elif-else`结构的使用方法；学会在遍历列表时使用`if`语句对特定元素进行处理；了解了`if`语句的格式设置建议。这些知识可帮助我们在程序中根据不同条件执行不同操作，使程序更具灵活性和实用性。 