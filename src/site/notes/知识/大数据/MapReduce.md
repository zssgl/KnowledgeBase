---
{"dg-publish":true,"permalink":"/知识/大数据/MapReduce/","tags":["技术"]}
---

# Background
Problem for large service providers such as Google: computation requires hundreds or thousands of computers 
- How do you distribute the computation? 
- Distributing the computation boils down to distributing data 
- Nodes fail, some nodes are slow, load balancing: difficult to make it work well

# 核心概念
A MapReduce framework (or system) is usually composed of three operations (or steps):

1. **Map:** each worker node applies the `map` function to the local data, and writes the output to a temporary storage. A master node ensures that only one copy of the redundant input data is processed.
2. **Shuffle:** worker nodes redistribute data based on the output keys (produced by the `map` function), such that all data belonging to one key is located on the same worker node.
3. **Reduce:** worker nodes now process each group of output data, per key, in parallel.

> [!tip] Key/Value Pairs
> ```
> map(k1, v1) ­> list(k2, v2) 
> reduce(k2, list(v2)) ­> list(v2)
>```
> map出来的东西再给reduce处理

![Pasted image 20240201121855.png](/img/user/%E9%99%84%E4%BB%B6/Pasted%20image%2020240201121855.png)

- The map component of a MapReduce job typically parses input data and distills it down to some intermediate result. 
- The reduce component of a MapReduce job collates these intermediate results and distills them down even further to the desired output.
![Pasted image 20240201122141.png](/img/user/%E9%99%84%E4%BB%B6/Pasted%20image%2020240201122141.png)

## 优点



## Example
Simple example of word count (wc):
```python
map(String key, String value):
 # key: document name
 # value: document contents
 for word w in value:
	 EmitIntermediate(w,"1")
 
reduce(String key, List values):
 # key: a word
 # values: a list of counts
 int result = 0
 for v in values:
	 result += ParseInt(v)
 Emit(AsString(result))
```


input:
"The number of partitions (R) and the partitioning function are specified by the user."

map: 

	("the", "1") , ("the", "1"), ("The", "1"), ("of", 1), (number, "1"), ... 
	
reduce: 

	"the", ("1", "1") -> "2" 
	"The", ("1") -> "1" 
	"of", ("1") -> "1" 
	"number", ("1") -> "1"










# Reference
[MapReduce - Wikipedia](https://en.wikipedia.org/wiki/MapReduce)
[cs110-lecture-17-mapreduce.pdf (stanford.edu)](https://web.stanford.edu/class/archive/cs/cs110/cs110.1214/static/lectures/cs110-lecture-17-mapreduce.pdf)
