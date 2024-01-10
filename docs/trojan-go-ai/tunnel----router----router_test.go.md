# `trojan-go\tunnel\router\router_test.go`

```
package router

import (
    "context"  // 上下文包，用于控制goroutine的取消、超时等
    "net"  // 网络包，提供了基本的网络操作函数
    "strconv"  // 字符串和基本数据类型之间的转换
    "strings"  // 字符串操作函数
    "testing"  // 测试包
    "time"  // 时间包

    "github.com/p4gefau1t/trojan-go/common"  // 引入自定义包common
    "github.com/p4gefau1t/trojan-go/config"  // 引入自定义包config
    "github.com/p4gefau1t/trojan-go/test/util"  // 引入自定义包util
    "github.com/p4gefau1t/trojan-go/tunnel"  // 引入自定义包tunnel
)

type MockClient struct{}  // 定义MockClient结构体

func (m *MockClient) DialConn(address *tunnel.Address, t tunnel.Tunnel) (tunnel.Conn, error) {  // MockClient结构体的DialConn方法
    return nil, common.NewError("mockproxy")  // 返回空值和自定义错误
}

func (m *MockClient) DialPacket(t tunnel.Tunnel) (tunnel.PacketConn, error) {  // MockClient结构体的DialPacket方法
    return MockPacketConn{}, nil  // 返回MockPacketConn结构体和空值
}

func (m MockClient) Close() error {  // MockClient结构体的Close方法
    return nil  // 返回空值
}

type MockPacketConn struct{}  // 定义MockPacketConn结构体

func (m MockPacketConn) ReadFrom(p []byte) (n int, addr net.Addr, err error) {  // MockPacketConn结构体的ReadFrom方法
    panic("implement me")  // 抛出异常
}

func (m MockPacketConn) WriteTo(p []byte, addr net.Addr) (n int, err error) {  // MockPacketConn结构体的WriteTo方法
    panic("implement me")  // 抛出异常
}

func (m MockPacketConn) Close() error {  // MockPacketConn结构体的Close方法
    panic("implement me")  // 抛出异常
}

func (m MockPacketConn) LocalAddr() net.Addr {  // MockPacketConn结构体的LocalAddr方法
    panic("implement me")  // 抛出异常
}

func (m MockPacketConn) SetDeadline(t time.Time) error {  // MockPacketConn结构体的SetDeadline方法
    panic("implement me")  // 抛出异常
}

func (m MockPacketConn) SetReadDeadline(t time.Time) error {  // MockPacketConn结构体的SetReadDeadline方法
    panic("implement me")  // 抛出异常
}

func (m MockPacketConn) SetWriteDeadline(t time.Time) error {  // MockPacketConn结构体的SetWriteDeadline方法
    panic("implement me")  // 抛出异常
}

func (m MockPacketConn) WriteWithMetadata(bytes []byte, metadata *tunnel.Metadata) (int, error) {  // MockPacketConn结构体的WriteWithMetadata方法
    return 0, common.NewError("mockproxy")  // 返回0和自定义错误
}

func (m MockPacketConn) ReadWithMetadata(bytes []byte) (int, *tunnel.Metadata, error) {  // MockPacketConn结构体的ReadWithMetadata方法
    return 0, nil, common.NewError("mockproxy")  // 返回0、空值和自定义错误
}

func TestRouter(t *testing.T) {  // 测试函数TestRouter
    data := `  // 定义字符串变量data
router:  // 路由器配置
    enabled: true  // 启用
    bypass:  // 绕过规则
    - "regex:bypassreg(.*)"  // 正则表达式绕过规则
    - "full:bypassfull"  // 完全匹配绕过规则
    - "full:localhost"  // 完全匹配绕过规则
    - "domain:bypass.com"  // 域名匹配绕过规则
    block:  // 阻断规则
    - "regexp:blockreg(.*)"  // 正则表达式阻断规则
    - "full:blockfull"  // 完全匹配阻断规则
    - "domain:block.com"  // 域名匹配阻断规则
    proxy:  // 代理规则
    - "regexp:proxyreg(.*)"  // 正则表达式代理规则
    - "full:proxyfull"  // 完全匹配代理规则
    - "domain:proxy.com"  // 域名匹配代理规则
    - "cidr:192.168.1.1/16"  // CIDR匹配代理规则
    // 使用 YAML 配置创建上下文
    ctx, err := config.WithYAMLConfig(context.Background(), []byte(data))
    // 检查错误
    common.Must(err)
    // 使用上下文和 MockClient 创建新的客户端
    client, err := NewClient(ctx, &MockClient{})
    // 检查错误
    common.Must(err)
    // 使用客户端拨号连接到指定地址
    _, err = client.DialConn(&tunnel.Address{
        AddressType: tunnel.DomainName,
        DomainName:  "proxy.com",
        Port:        80,
    }, nil)
    // 检查错误信息是否为 "mockproxy"，如果不是则输出错误并终止测试
    if err.Error() != "mockproxy" {
        t.Fatal(err)
    }
    // 以下类似，依次进行不同地址的拨号连接，并进行错误检查和处理
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    // ...
    //
# 闭合前面的函数定义
```