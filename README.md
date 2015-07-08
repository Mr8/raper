# Raper: Golang 项目构建脚本(The Golang project builder)
Tags: Golang
---

## 简介
用于构建 Golang 项目目录
初始状态下项目结构
```
.
└── raper
```
### 构建命令:
`./raper --build foo`
其中创建如下目录结构
```
.
├── bin
│   └── foo
├── raper
├── README.md
├── requirements.txt
└── src
    └── foo
        └── main.go
```

`./bin/foo `
输出`Hello, world`

### 文件及目录
```
bin/ 用于构建好的二进制目录
src/ 包含构建的项目
README.md 文档
requirement.txt 项目依赖
```

### 安装命令:
初始状态下，build 命令会默认调用 install 命令
在 requirement.txt 中加入依赖关系

`cat requirements.txt `

```
## add the requirements like:
github.com/go-sql-driver/mysql
```
src/foo/main.go 中依赖于mysql driver
```
package main

import (
        "fmt"
        "github.com/go-sql-driver/mysql"
)

func main() {
        fmt.Println("Hello, world")
}
```
`./raper --install foo`
生成目录如下
```
.
├── bin
│   └── foo
├── pkg
│   └── linux_amd64
│       └── github.com
│           └── go-sql-driver
│               └── mysql.a
├── raper
├── README.md
├── requirements.txt
└── src
    ├── foo
    │   └── main.go
    └── github.com
        └── go-sql-driver
            └── mysql
                ├── appengine.go
                ├── AUTHORS
                ├── benchmark_test.go
                ├── buffer.go
                ...
                └── utils_test.go
```

所有项目依赖会自动安装，二进制发布到 bin/foo


