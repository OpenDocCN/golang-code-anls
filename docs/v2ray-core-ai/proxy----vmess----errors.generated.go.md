# `v2ray-core\proxy\vmess\errors.generated.go`

```go
# 定义一个名为 vmess 的包
package vmess

# 导入 errors 包
import "v2ray.com/core/common/errors"

# 定义一个名为 errPathObjHolder 的结构体
type errPathObjHolder struct{}

# 定义一个名为 newError 的函数，接收可变数量的参数，返回一个 errors.Error 类型的指针
func newError(values ...interface{}) *errors.Error {
    # 调用 errors 包中的 New 函数，传入可变数量的参数，返回一个 errors.Error 类型的对象，并设置路径对象为 errPathObjHolder 结构体
    return errors.New(values...).WithPathObj(errPathObjHolder{})
}
```