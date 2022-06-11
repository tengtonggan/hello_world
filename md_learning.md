# Markdown Learning

## 工具推荐：[Typora](https://typora.io/)

## **Markdown 教程**：
- [菜鸟教程](https://www.runoob.com/markdown/md-tutorial.html)
- [Markdown Preview Enhanced (MPE)](https://shd101wyy.github.io/markdown-preview-enhanced/#/zh-cn/)

## 基本操作：
   - **粗体** *斜体*  ***粗斜体***

   - 
     分割线 `***`
     
   - ~~删除线~~ <u>下划线</u>

   - 脚注 [^runoob]

   - 列表

     1. 第一项
     2. 第二项

   - 区块

     > 最外层
     >
     > > 第一层
     > >
     > > > 第二层
     > > >
     > > > 1. 区块列表1
     > > > 2. 区块列表2
     
   - 代码区块

     ```C++
     #include<iostream>
     using namespace std;
     int main()
     {
         cout<<"Hello, world! "<<endl;
     }
     ```
  - Mermaid [mermaid文档](https://mermaid-js.github.io/mermaid/#/)
    ```mermaid
    graph LR
    A-->B;
    B-->C;
    C-->A;
    ```
    ```mermaid
    flowchart LR
    a --> b & c--> d
    ```
  - 代码行数
    如果你想要你的代码块显示代码行数，只要添加 `line-numbers` class 就可以了。  
    ```c++{.line-numbers}
    #include<iostream>
    using namespace std;
    int main(){
         return 0;
    }
    ```

   - 这是一个链接 [菜鸟教程](https://www.runoob.com)

   - 图片

     ![测试图片](https://img2.baidu.com/it/u=1945464906,1635022113&fm=26&fmt=auto)

     <img src="https://img2.baidu.com/it/u=1945464906,1635022113&fm=26&fmt=auto" width="20%" height="50%">

   - 表格
     | 左对齐 | 右对齐 | 居中对齐 |
     | :----- | -----: | :------: |
     | 单元格 | 单元格 |  单元格  |
     | 单元格 | 单元格 |  单元格  |
     
   - 高级操作

     [公式等](https://www.runoob.com/markdown/md-advance.html)

[^runoob]: 菜鸟教程

## 高级教程
不在 Markdown 涵盖范围之内的标签，都可以直接在文档里面用 HTML 撰写。

目前支持的 HTML 元素有：\<kbd> \<b> \<i> \<em> \<sup> \<sub> \<br>等 ，如：

> 使用 <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>Del</kbd> 重启电脑

$$
\begin{Bmatrix}
   a & b \\
   c & d
\end{Bmatrix}
$$
$$
\begin{CD}
   A @>a>> B \\
@VbVV @AAcA \\
   C @= D
\end{CD}
$$
