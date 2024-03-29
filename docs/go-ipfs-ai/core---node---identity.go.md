# `kubo\core\node\identity.go`

```go
package node

import (
    "fmt"

    "github.com/libp2p/go-libp2p/core/crypto"
    "github.com/libp2p/go-libp2p/core/peer"
)

// PeerID 返回一个函数，该函数返回给定的 peer.ID
func PeerID(id peer.ID) func() peer.ID {
    return func() peer.ID {
        return id
    }
}

// PrivateKey 从配置中加载私钥
func PrivateKey(sk crypto.PrivKey) func(id peer.ID) (crypto.PrivKey, error) {
    return func(id peer.ID) (crypto.PrivKey, error) {
        // 从私钥中获取 peer.ID
        id2, err := peer.IDFromPrivateKey(sk)
        if err != nil {
            return nil, err
        }

        // 检查私钥对应的 peer.ID 是否与给定的 peer.ID 相匹配
        if id2 != id {
            return nil, fmt.Errorf("private key in config does not match id: %s != %s", id, id2)
        }
        return sk, nil
    }
}
```