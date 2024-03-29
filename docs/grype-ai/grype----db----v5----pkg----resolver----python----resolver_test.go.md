# `grype\grype\db\v5\pkg\resolver\python\resolver_test.go`

```go
package python

import (
    "testing"  // 导入测试包
    "github.com/stretchr/testify/assert"  // 导入断言包
)

func TestResolver_Normalize(t *testing.T) {  // 定义测试函数
    tests := []struct {  // 定义测试用例
        packageName string  // 包名
        normalized  string  // 标准化后的包名
    }{
        {
            packageName: "PyYAML",  // 测试用例1：包名为"PyYAML"
            normalized:  "pyyaml",  // 期望的标准化包名为"pyyaml"
        },
        {
            packageName: "oslo.concurrency",  // 测试用例2：包名为"oslo.concurrency"
            normalized:  "oslo-concurrency",  // 期望的标准化包名为"oslo-concurrency"
        },
        {
            packageName: "",  // 测试用例3：空包名
            normalized:  "",  // 期望的标准化包名为空
        },
        {
            packageName: "test---1",  // 测试用例4：包名为"test---1"
            normalized:  "test-1",  // 期望的标准化包名为"test-1"
        },
        {
            packageName: "AbCd.-__.--.-___.__.--1234____----....XyZZZ",  // 测试用例5：包名为"AbCd.-__.--.-___.__.--1234____----....XyZZZ"
            normalized:  "abcd-1234-xyzzz",  // 期望的标准化包名为"abcd-1234-xyzzz"
        },
    }

    resolver := Resolver{}  // 创建 Resolver 对象

    for _, test := range tests {  // 遍历测试用例
        resolvedNames := resolver.Normalize(test.packageName)  // 调用 Normalize 方法进行包名标准化
        assert.Equal(t, resolvedNames, test.normalized)  // 使用断言判断标准化后的包名是否符合预期
    }
}
```