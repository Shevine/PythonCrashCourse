# 第7章 用户输入和while循环学习笔记
## 1  函数input()的工作原理
函数`input()`用于让程序暂停运行，等待用户输入文本，并将输入存储在一个变量中。
### 1.1  编写清晰的程序
使用`input()`函数时，应提供清晰的提示，让用户明白该输入什么信息。提示可以是简单的一句话，也可以是多行字符串。例如：
```python
name = input("Please enter your name: ")
print("Hello, " + name + "!")
```
若提示内容较多，可将其存储在变量中，再传递给`input()`函数：
```python
prompt = "If you tell us who you are, we can personalize the messages you see."
prompt += "\nWhat is your first name? "
name = input(prompt)
print("\nHello, " + name + "!")
```
### 1.2  使用int()来获取数值输入
`input()`函数获取的用户输入会被解读为字符串。若要将输入用于数值比较或计算，需使用`int()`函数将其转换为数值类型。例如：
```python
height = input("How tall are you, in inches? ")
height = int(height)
if height >= 36:
    print("\nYou're tall enough to ride!")
else:
    print("\nYou'll be able to ride when you're a little older.")
```
如果不进行转换，直接用字符串和数值进行比较，会引发`TypeError`错误。
### 1.3  求模运算符
求模运算符（`%`）用于将两个数相除并返回余数。利用这一特性，可以判断一个数是奇数还是偶数。例如：
```python
number = input("Enter a number, and I'll tell you if it's even or odd: ")
number = int(number)
if number % 2 == 0:
    print("\nThe number " + str(number) + " is even.")
else:
    print("\nThe number " + str(number) + " is odd.")
```
### 1.4  在Python 2.7中获取输入
在Python 2.7中，应使用`raw_input()`函数来提示用户输入，该函数与Python 3中的`input()`函数一样，将输入解读为字符串。而Python 2.7中的`input()`函数会将用户输入解读为Python代码并尝试运行，可能导致错误或意外结果，因此不建议使用。

## 2  while循环简介
`while`循环用于不断运行一段代码，直到指定的条件不满足为止。
### 2.1  使用while循环
通过设置循环条件，`while`循环可以重复执行代码块。例如，从1数到5：
```python
current_number = 1
while current_number <= 5:
    print(current_number)
    current_number += 1
```
在这个例子中，只要`current_number`小于或等于5，循环就会继续执行，每次循环都会打印当前数字并将其加1。
### 2.2  让用户选择何时退出
可以通过设置退出条件，让用户决定何时停止程序。例如：
```python
prompt = "\nTell me something, and I will repeat it back to you:"
prompt += "\nEnter 'quit' to end the program. "
message = ""
while message != 'quit':
    message = input(prompt)
    if message != 'quit':
        print(message)
```
在这个程序中，只要用户输入的不是`'quit'`，循环就会持续运行，并打印用户输入的内容。为了避免打印`'quit'`，添加了一个`if`测试进行判断。
### 2.3  使用标志
在复杂程序中，可定义一个标志（如`active`）来控制循环的运行。当标志为`True`时，循环继续；当标志为`False`时，循环停止。例如：
```python
prompt = "\nTell me something, and I will repeat it back to you:"
prompt += "\nEnter 'quit' to end the program. "
active = True
while active:
    message = input(prompt)
    if message == 'quit':
        active = False
    else:
        print(message)
```
这种方式使代码结构更清晰，便于添加其他导致循环停止的条件。
### 2.4  使用break退出循环
`break`语句用于立即退出`while`循环，不再执行循环中余下的代码。例如：
```python
prompt = "\nPlease enter the name of a city you have visited:"
prompt += "\n(Enter 'quit' when you are finished.) "
while True:
    city = input(prompt)
    if city == 'quit':
        break
    else:
        print("I'd love to go to " + city.title() + "!")
```
在这个循环中，只要用户输入`'quit'`，就会执行`break`语句，退出循环。
### 2.5  在循环中使用continue
`continue`语句用于返回到循环开头，并根据条件测试结果决定是否继续执行循环。例如，打印1到10中的偶数：
```python
current_number = 0
while current_number < 10:
    current_number += 1
    if current_number % 2 == 0:
        continue
    print(current_number)
```
在这个循环中，当`current_number`是偶数时，执行`continue`语句，跳过本次循环中余下的代码，直接进入下一次循环。
### 2.6  避免无限循环
每个`while`循环都必须有停止运行的途径，否则会导致无限循环。编写循环时，要确保循环条件能在适当的时候变为`False`，或者有`break`语句来终止循环。如果程序陷入无限循环，可以按`Ctrl + C`或关闭输出窗口来停止程序。例如：
```python
x = 1
while x <= 5:
    print(x)
    # 若遗漏x += 1这行代码，循环将无限进行
    x += 1
```

## 3  使用while循环来处理列表和字典
`while`循环常与列表和字典结合使用，用于收集、存储和组织大量输入数据。
### 3.1  在列表之间移动元素
可以使用`while`循环将一个列表中的元素逐个移动到另一个列表中。例如，验证用户列表：
```python
unconfirmed_users = ['alice', 'brian', 'candace']
confirmed_users = []
while unconfirmed_users:
    current_user = unconfirmed_users.pop()
    print("Verifying user: " + current_user.title())
    confirmed_users.append(current_user)
print("\nThe following users have been confirmed:")
for confirmed_user in confirmed_users:
    print(confirmed_user.title())
```
在这个例子中，`while`循环不断从`unconfirmed_users`列表中取出元素，进行验证后添加到`confirmed_users`列表中。
### 3.2  删除包含特定值的所有列表元素
使用`while`循环可以删除列表中所有包含特定值的元素。例如：
```python
pets = ['dog', 'cat', 'dog', 'goldfish', 'cat', 'rabbit', 'cat']
while 'cat' in pets:
    pets.remove('cat')
print(pets)
```
在这个循环中，只要列表中存在`'cat'`，就会将其删除，直到列表中不再有`'cat'`为止。
### 3.3  使用用户输入来填充字典
通过`while`循环可以提示用户输入信息，并将其存储在字典中。例如，创建一个调查程序：
```python
responses = {}
polling_active = True
while polling_active:
    name = input("\nWhat is your name? ")
    response = input("Which mountain would you like to climb someday? ")
    responses[name] = response
    repeat = input("Would you like to let another person respond? (yes/ no) ")
    if repeat == 'no':
        polling_active = False
print("\n--- Poll Results ---")
for name, response in responses.items():
    print(name + " would like to climb " + response + ".")
```
在这个程序中，用户可以不断输入名字和回答，程序将这些信息存储在字典`responses`中，直到用户选择不再继续。

## 4  小结
在本章中，学习了如何使用`input()`函数获取用户输入，包括处理文本和数字输入；掌握了`while`循环的使用方法，以及如何通过设置条件、标志、`break`语句和`continue`语句来控制循环流程；学会了使用`while`循环处理列表和字典，如在列表之间移动元素、删除特定元素以及用用户输入填充字典。这些知识有助于编写更具交互性和实用性的程序。 