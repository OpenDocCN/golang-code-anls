# `v2ray-core\transport\internet\tls\errors.generated.go`

```
# 定义了一个名为tls的包
package tls

# 导入了名为errors的包
import "v2ray.com/core/common/errors"

# 定义了一个名为errPathObjHolder的结构体
type errPathObjHolder struct{}

# 定义了一个名为newError的函数，接收任意数量的参数，返回一个errors.Error类型的指针
func newError(values ...interface{}) *errors.Error:
    # 调用errors包中的New函数，传入values参数，并使用WithPathObj方法传入errPathObjHolder结构体
    return errors.New(values...).WithPathObj(errPathObjHolder{})
```