sego
====

Go中文分词

<a href="https://github.com/molezzz/sego/blob/master/dictionary.go">词典</a>用前缀树实现，
<a href="https://github.com/molezzz/sego/blob/master/segmenter.go">分词器</a>算法为基于词频的最短路径加动态规划。

支持普通和搜索引擎两种分词模式，支持用户词典、词性标注，可运行<a href="https://github.com/molezzz/sego/blob/master/server/server.go">JSON RPC服务</a>。

分词速度<a href="https://github.com/molezzz/sego/blob/master/tools/benchmark.go">单线程</a>2.7MB/s，<a href="https://github.com/molezzz/sego/blob/master/tools/goroutines.go">goroutines并发</a>13MB/s, 处理器Core i7-3615QM 2.30GHz 8核。

在线演示地址 http://sego.weiboglass.com

# 安装/更新

```
go get -u github.com/molezzz/sego
```

# 使用


```go
package main

import (
	"fmt"
	"github.com/molezzz/sego"
)

func main() {
	// 载入词典
	var segmenter sego.Segmenter
	segmenter.LoadDictionary("github.com/molezzz/sego/data/dictionary.txt")

	// 分词
	text := []byte("中华人民共和国中央人民政府")
	segments := segmenter.Segment(text)

	// 处理分词结果
	// 支持普通模式和搜索模式两种分词，见代码中SegmentsToString函数的注释。
	fmt.Println(sego.SegmentsToString(segments, false))
}
```
