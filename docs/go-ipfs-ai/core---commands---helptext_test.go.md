# `kubo\core\commands\helptext_test.go`

```
package commands

import (
    "strings"  // 导入 strings 包，用于处理字符串
    "testing"  // 导入 testing 包，用于编写测试函数

    cmds "github.com/ipfs/go-ipfs-cmds"  // 导入自定义包 cmds，用于处理 IPFS 命令
)

func checkHelptextRecursive(t *testing.T, name []string, c *cmds.Command) {
    c.ProcessHelp()  // 处理命令的帮助文本

    t.Run(strings.Join(name, "_"), func(t *testing.T) {  // 使用测试函数运行命令名称的组合
        if c.External {  // 如果命令是外部命令
            t.Skip("external")  // 跳过测试，输出 "external"
        }

        t.Run("tagline", func(t *testing.T) {  // 使用测试函数运行标语
            if c.Helptext.Tagline == "" {  // 如果标语为空
                t.Error("no Tagline!")  // 输出错误信息 "no Tagline!"
            }
        })

        t.Run("longDescription", func(t *testing.T) {  // 使用测试函数运行长描述
            t.Skip("not everywhere yet")  // 跳过测试，输出 "not everywhere yet"
            if c.Helptext.LongDescription == "" {  // 如果长描述为空
                t.Error("no LongDescription!")  // 输出错误信息 "no LongDescription!"
            }
        })

        t.Run("shortDescription", func(t *testing.T) {  // 使用测试函数运行短描述
            t.Skip("not everywhere yet")  // 跳过测试，输出 "not everywhere yet"
            if c.Helptext.ShortDescription == "" {  // 如果短描述为空
                t.Error("no ShortDescription!")  // 输出错误信息 "no ShortDescription!"
            }
        })

        t.Run("synopsis", func(t *testing.T) {  // 使用测试函数运行概要
            t.Skip("autogenerated in go-ipfs-cmds")  // 跳过测试，输出 "autogenerated in go-ipfs-cmds"
            if c.Helptext.Synopsis == "" {  // 如果概要为空
                t.Error("no Synopsis!")  // 输出错误信息 "no Synopsis!"
            }
        })
    })

    for subname, sub := range c.Subcommands {  // 遍历命令的子命令
        checkHelptextRecursive(t, append(name, subname), sub)  // 递归调用函数，检查子命令的帮助文本
    }
}

func TestHelptexts(t *testing.T) {
    Root.ProcessHelp()  // 处理根命令的帮助文本
    checkHelptextRecursive(t, []string{"ipfs"}, Root)  // 调用递归函数，检查命令的帮助文本
}
```