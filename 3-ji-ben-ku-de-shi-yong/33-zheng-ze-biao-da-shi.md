### 1.相关链接及说明

* 开源中国提供的正则表达式测试工具：[http://tool.oschina.net/regex/](http://tool.oschina.net/regex/)

匹配规则：

| 模式 | 描述 |
| :--- | :--- |
| `\w` | 匹配字母数字及下划线 |
| `\W` | 匹配非字母数字及下划线 |
| `\s` | 匹配任意空白字符，等价于 \[\t\n\r\f\]. |
| `\S` | 匹配任意非空字符 |
| `\d` | 匹配任意数字，等价于 \[0-9\] |
| `\D` | 匹配任意非数字 |
| `\A` | 匹配字符串开始 |
| `\Z` | 匹配字符串结束，如果是存在换行，只匹配到换行前的结束字符串 |
| `\z` | 匹配字符串结束 |
| `\G` | 匹配最后匹配完成的位置 |
| `\n` | 匹配一个换行符 |
| `\t` | 匹配一个制表符 |
| `^` | 匹配字符串的开头 |
| `$` | 匹配字符串的末尾 |
| `.` | 匹配任意字符，除了换行符，当 re.DOTALL 标记被指定时，则可以匹配包括换行符的任意字符 |
| `[...]` | 用来表示一组字符，单独列出：\[amk\] 匹配 'a'，'m' 或 'k' |
| `[^...]` | 不在 \[\] 中的字符：[abc](https://germey.gitbooks.io/python3webspider/content/3.3-正则表达式.html#fn_abc)匹配除了 a,b,c 之外的字符。 |
| `*` | 匹配 0 个或多个的表达式。 |
| `+` | 匹配 1 个或多个的表达式。 |
| `?` | 匹配 0 个或 1 个由前面的正则表达式定义的片段，非贪婪方式 |
| `{n}` | 精确匹配 n 个前面表达式。 |
| `{n, m}` | 匹配 n 到 m 次由前面的正则表达式定义的片段，贪婪方式 |
| a\|b | 匹配a或b |
| `( )` | 匹配括号内的表达式，也表示一个组 |

### 2.re库

Python 的 re 库提供了整个正则表达式的实现

### 3. match\(\) {#3-match}

语法:match\(pattern, string, flags=0\)

match\(\) 方法会尝试从字符串的起始位置匹配正则表达式，如果匹配，就返回匹配成功的结果，如果不匹配，那就返回 None

实例:

```
import re

content = 'Hello 123 4567 World_This is a Regex Demo'
print(len(content))
# \s:空格
# \w:字母及数字、下划线
result = re.match('^Hello\s\d\d\d\s\d{4}\s\w{10}',content)
print(result)
print(result.group())
print(result.span())
```

运行结果:

```
41
<_sre.SRE_Match object; span=(0, 25), match='Hello 123 4567 World_This'>
Hello 123 4567 World_This
(0, 25)
```

* group\(\)方法:输出匹配到的内容
* span\(\)方法:输出匹配到的范围

#### 匹配目标 {#匹配目标}

match\(\) 方法可以得到匹配到的字符串内容，如何从字符串中提取一部分内容

在这里可以使用 \(\) 括号来将我们想提取的子字符串括起来，\(\) 实际上就是标记了一个子表达式的开始和结束位置，被标记的每个子表达式会依次对应每一个分组，我们可以调用 group\(\) 方法传入分组的索引即可获取提取的结果

实例:

```
import re

content = 'Hello 1234567 World_This is a Regex Demo'
result = re.match('^Hello\s(\d+)\sWorld', content)
print(result)
print(result.group())
print(result.group(1))
print(result.span())
```

运行结果:

```
<_sre.SRE_Match object; span=(0, 19), match='Hello 1234567 World'>
Hello 1234567 World
1234567
(0, 19)
```

group\(\) 会输出完整的匹配结果,group\(1\) 会输出第一个被 \(\) 包围的匹配结果，假如正则表达式后面还有 \(\) 包括的内容，那么我们可以依次用 group\(2\)、group\(3\) 等来依次获取

