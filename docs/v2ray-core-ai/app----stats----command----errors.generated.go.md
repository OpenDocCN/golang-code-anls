# `v2ray-core\app\stats\command\errors.generated.go`

```
# 定义一个名为 command 的包
package command

# 导入 errors 包
import "v2ray.com/core/common/errors"

# 定义一个名为 errPathObjHolder 的结构体
type errPathObjHolder struct{}

# 定义一个名为 newError 的函数，接收任意类型的参数，并返回一个 errors.Error 类型的错误
func newError(values ...interface{}) *errors.Error:
    # 调用 errors 包中的 New 函数，传入参数 values，并使用 WithPathObj 方法设置错误路径对象为 errPathObjHolder 结构体
    return errors.New(values...).WithPathObj(errPathObjHolder{})
```