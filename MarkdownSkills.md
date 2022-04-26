**Typora用`ctrl+/`切换源代码格式**

# 一级标题

*斜体* 	_斜体_	**粗体**	__粗体__	***粗斜体***	___粗斜体___

### 以下都是分割线

***

---

~~删除线~~	<u>下划线</u>	[^脚注]

(*)(+)(-)

>最外层
>>第一层
>>
>>>第二层

这是一个链接[菜鸟教程](https://www.runoob.com)

这个链接用1作为网址变量[Google][1]

[1]:http://www.google.com/

|  表头  |   表头 |
| :----: | -----: |
| 单元格 | 单元格 |

#### 文本内链接

**方法一**：稍微复杂点，被链接指向的内容可随意更改。

[点我去下面的标题](#jump)

**方法二**：适用于固定内容，不常更改。且好像只能以标题作为锚点

[点我去下面的标题](#只能写成和上面括号里一样的)



###### 只能写成和上面括号里一样的

**<span id="jump">我在这儿呢</span>**

-----------------

#### 公式

##### 大括号

$A=\left\{\begin{matrix}2,1\end{matrix}\right\}=A$

$H(f)=\left\{\begin{matrix}+1, f>0\\-1, f\leq0 \end{matrix}\right.$

$\left.\begin{matrix}+1, f>0\\-1, f\leq0 \end{matrix}\right\}=H(f)$
$$
f[i][j]=\begin{cases}
if(p[j]\neq'*')=\begin{cases}
f[i-1][j-1], &matches(s[i],p[j])\\
false, &otherwise\\
\end{cases}	\\
otherwise=\begin{cases}
f[i-1][j]orf[i][j-2], &matches(s[i],p[j-1])\\
f[i][j-2], &otherwise\\
\end{cases}	\\
test=\begin{cases}
\lim\limits_{x\to0} \frac{a^x}{b+c}, &x<3\\
\pi, &x=3\\
\int_a^{3b}x_{ij}+e^2\mathrm{d}x, &x>3\\
\end{cases} \\
\end{cases}
$$

#### 画流程图

https://www.runoob.com/markdown/md-advance.html

https://www.jianshu.com/p/7864c1cf5660
