# `v2ray-core\proxy\freedom\errors.generated.go`

```go
# 定义一个名为 freedom 的包
package freedom

# 导入 errors 包
import "v2ray.com/core/common/errors"

# 定义一个名为 errPathObjHolder 的结构体
type errPathObjHolder struct{}

# 定义一个名为 newError 的函数，接收任意类型的参数，并返回一个 errors.Error 类型的指针
func newError(values ...interface{}) *errors.Error:
    # 调用 errors 包中的 New 函数，传入参数 values，并使用 WithPathObj 方法设置错误路径对象为 errPathObjHolder
    return errors.New(values...).WithPathObj(errPathObjHolder{})
```