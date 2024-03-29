# Kubo changelog v0.15

## v0.15.0

### Overview

Below is an outline of all that is in this release, so you get a sense of all that's included.

- [Kubo changelog v0.15](#kubo-changelog-v015)
  - [v0.15.0](#v0150)
    - [Overview](#overview)
    - [🔦 Highlights](#-highlights)
      - [#️⃣ Blake 3 support](#️⃣-blake-3-support)
      - [💉 Fx Options plugin](#-fx-options-plugin)
      - [📁 `$IPFS_PATH/gateway` file](#-ipfs_pathgateway-file)
    - [Changelog](#changelog)
    - [Contributors](#contributors)


### 🔦 Highlights

This is a release mainly with bugfixing and library updates.
We are improving release speed and cadence trying to have a new release every 5 weeks.

#### #️⃣ Blake 3 support

You can now use `blake3` as a valid hash function:
- `ipfs block put --mhtype=blake3`
- `ipfs add --hash=blake3`

It uses a 32 bytes default size.
And verify up to 128 bytes.
Because `blake3` is variable output hash function, you can use a different digest length, set `mhlen`: `ipfs block put --mhtype=blake3 --mhlen=64`, `ipfs add` doesn't have this option yet.

#### 💉 Fx Options plugin

This adds a plugin interface that lets the plugin modify the fx options that are passed to fx when the app is initialized.
This means plugins can inject their own implementations of Kubo interfaces.
This enables granular customization of Kubo behavior by plugins, such as:

- Bitswap with custom filters (e.g. for CID blocking)
- Custom interface implementations such as Pinner or DAGService
- Dynamic configuration of libp2p ...

Here's an example plugin that overrides the default Pinner with a custom one:

```go
func (p *PinnerPlugin) Options(info core.FXNodeInfo) ([]fx.Option, error) {
	pinner := mypinner.New()    
	return append(info.FXOptions, fx.Replace(fx.Annotate(pinner, fx.As(new(pin.Pinner))))), nil
}
```

Extra plugin info [here](https://github.com/ipfs/kubo/blob/master/docs/plugins.md#fx-experimental).

#### 📁 `$IPFS_PATH/gateway` file

This adds a new file in the `IPFS_PATH` folder similar to `$IPFS_PATH/api` containing an address based on [`Addresses.Gateway`](https://github.com/ipfs/kubo/blob/master/docs/config.md#addressesgateway) configuration.

This file is in URL (RFC1738) format.

```go
$ cat ~/.ipfs/gateway
http://127.0.0.1:8080
```

### Changelog

<details>
<summary>Full Changelog</summary>

- github.com/ipfs/kubo:
  - chore: Release v0.15.0-rc1
  - Update RELEASE_ISSUE_TEMPLATE.md for 0.15
  - docs(add): skip binary name in helptext
  - docs(cli): clarify CID determinism in add command
  - docs(cli): clarify CAR format in dag export|import
  - test(gw): cors preflight with custom header
  - feat: make corehttp a reusable component ([ipfs/kubo#9070](https://github.com/ipfs/kubo/pull/9070))
  - feat: go-libp2p v0.21 (rcmgr auto scaling) ([ipfs/kubo#9074](https://github.com/ipfs/kubo/pull/9074))
  -  ([ipfs/kubo#9024](https://github.com/ipfs/kubo/pull/9024))
  -  ([ipfs/kubo#9100](https://github.com/ipfs/kubo/pull/9100))
  -  ([ipfs/kubo#9095](https://github.com/ipfs/kubo/pull/9095))
  - chore(cmd): add shutdown to CLI help ([ipfs/kubo#9194](https://github.com/ipfs/kubo/pull/9194))
  - docs: add fx plugin documentation to plugins.md (#9191) ([ipfs/kubo#9191](https://github.com/ipfs/kubo/pull/9191))
  - chore: switch to dist.ipfs.tech
  - feat: add fx options plugin
  - feat: add blake3 support
  - Add reference to Experimental config doc (#9181) ([ipfs/kubo#9181](https://github.com/ipfs/kubo/pull/9181))
  - feat: add $IPFS_PATH/gateway file
  - docs: replace `docs.ipfs.io` with `docs.ipfs.tech` (#9158) ([ipfs/kubo#9158](https://github.com/ipfs/kubo/pull/9158))
  - chore: fix markdown link syntax typo for AutoNAT.ServiceMode
  - chore: bump go-blockservice to only do put once
  - docs: update Arch Linux installation instructions
  - chore: update kubo-as-a-library example
  - docs(readme): add maintainer info (#9141) ([ipfs/kubo#9141](https://github.com/ipfs/kubo/pull/9141))
  - fix(gw): 404 when a valid DAG is missing link
  - fix(gw): directory URL normalization ([ipfs/kubo#9123](https://github.com/ipfs/kubo/pull/9123))
  - docs(config): add link to someguy router
  - fix: typo in README
  - Reproducible Builds: Update GOFLAGS for -trimpath
  - Merge v0.14.0 back into master
  - fix(gw): cache-control of index.html websites
  - chore(license): fix broken link to apache-2.0
  - fix: kubo in daemon and cli stdout
  - docs(readme): move content to docs website (#9102) ([ipfs/kubo#9102](https://github.com/ipfs/kubo/pull/9102))
  - fix(gw): no backlink when listing root dir
- github.com/ipfs/go-bitswap (v0.7.0 -> v0.9.0):
  - chore: release v0.9.0
  - feat: split client and server ([ipfs/go-bitswap#570](https://github.com/ipfs/go-bitswap/pull/570))
  - chore: remove goprocess from blockstoremanager
  - Don't add blocks to the datastore ([ipfs/go-bitswap#571](https://github.com/ipfs/go-bitswap/pull/571))
  - Remove dependency on travis package from go-libp2p-testing ([ipfs/go-bitswap#569](https://github.com/ipfs/go-bitswap/pull/569))
  - feat: add basic tracing (#562) ([ipfs/go-bitswap#562](https://github.com/ipfs/go-bitswap/pull/562))
- github.com/ipfs/go-blockservice (v0.3.0 -> v0.4.0):
  - write blocks retrieved from the exchange to the blockstore ([ipfs/go-blockservice#92](https://github.com/ipfs/go-blockservice/pull/92))
  - feat: add basic tracing ([ipfs/go-blockservice#91](https://github.com/ipfs/go-blockservice/pull/91))
- github.com/ipfs/go-ipfs-exchange-interface (v0.1.0 -> v0.2.0):
  - Rename HasBlock to NotifyNewBlocks, and make it accept multiple blocks ([ipfs/go-ipfs-exchange-interface#23](https://github.com/ipfs/go-ipfs-exchange-interface/pull/23))
- github.com/ipfs/go-ipfs-exchange-offline (v0.2.0 -> v0.3.0):
  - Exchange don't add blocks on their own anymore ([ipfs/go-ipfs-exchange-offline#47](https://github.com/ipfs/go-ipfs-exchange-offline/pull/47))
- github.com/ipfs/go-verifcid (v0.0.1 -> v0.0.2):
  - chore: release v0.0.2
  - feat: add blake3 as a good hash
  - sync: update CI config files (#12) ([ipfs/go-verifcid#12](https://github.com/ipfs/go-verifcid/pull/12))
  - Add license ([ipfs/go-verifcid#8](https://github.com/ipfs/go-verifcid/pull/8))
- github.com/ipld/go-codec-dagpb (v1.4.0 -> v1.4.1):
  - v1.4.1 bump
- github.com/libp2p/go-buffer-pool (v0.0.2 -> v0.1.0):
  - release v0.1.0 (#30) ([libp2p/go-buffer-pool#30](https://github.com/libp2p/go-buffer-pool/pull/30))
  - panic if a negative length is passed to BufferPool.Get (#28) ([libp2p/go-buffer-pool#28](https://github.com/libp2p/go-buffer-pool/pull/28))
  - sync: update CI config files (#22) ([libp2p/go-buffer-pool#22](https://github.com/libp2p/go-buffer-pool/pull/22))
  - sync: update CI config files (#20) ([libp2p/go-buffer-pool#20](https://github.com/libp2p/go-buffer-pool/pull/20))
  - test: fix gc test on go 1.16 ([libp2p/go-buffer-pool#18](https://github.com/libp2p/go-buffer-pool/pull/18))
  - fix staticcheck ([libp2p/go-buffer-pool#16](https://github.com/libp2p/go-buffer-pool/pull/16))
  - test: make sure we have the correct number of pools ([libp2p/go-buffer-pool#10](https://github.com/libp2p/go-buffer-pool/pull/10))
- github.com/libp2p/go-libp2p (v0.20.3 -> v0.21.0):
  - Release v0.21.0 (#1648) ([libp2p/go-libp2p#1648](https://github.com/libp2p/go-libp2p/pull/1648))
  - ping: optimize random number generation (#1658) ([libp2p/go-libp2p#1658](https://github.com/libp2p/go-libp2p/pull/1658))
  - feat: switch noise to use minio's SHA256 implementation (#1657) ([libp2p/go-libp2p#1657](https://github.com/libp2p/go-libp2p/pull/1657))
  - swarm: mark dialing WebTransport addresses as expensive (#1650) ([libp2p/go-libp2p#1650](https://github.com/libp2p/go-libp2p/pull/1650))
  - routedhost: fix decoding of relay peer ID (#1644) ([libp2p/go-libp2p#1644](https://github.com/libp2p/go-libp2p/pull/1644))
  - Release v0.21.0 RC (#1638) ([libp2p/go-libp2p#1638](https://github.com/libp2p/go-libp2p/pull/1638))
  - fix: return the best _acceptable_ conn in NewStream (#1604) ([libp2p/go-libp2p#1604](https://github.com/libp2p/go-libp2p/pull/1604))
  - use autoscaling limits (#1637) ([libp2p/go-libp2p#1637](https://github.com/libp2p/go-libp2p/pull/1637))
  - docs: point to SetDefaultServiceLimits in ResourceManager option (#1636) ([libp2p/go-libp2p#1636](https://github.com/libp2p/go-libp2p/pull/1636))
  - chore: update deps (#1634) ([libp2p/go-libp2p#1634](https://github.com/libp2p/go-libp2p/pull/1634))
  - Pass endpoint information to resource manager's OpenConnection (#1633) ([libp2p/go-libp2p#1633](https://github.com/libp2p/go-libp2p/pull/1633))
  - Add canonical peer status logs (#1624) ([libp2p/go-libp2p#1624](https://github.com/libp2p/go-libp2p/pull/1624))
  - move go-libp2p-circuit here ([libp2p/go-libp2p#1626](https://github.com/libp2p/go-libp2p/pull/1626))
  - swarm: fix logging of accepted connections (#1629) ([libp2p/go-libp2p#1629](https://github.com/libp2p/go-libp2p/pull/1629))
  - fix: deny connections to peers in the right place (#1627) ([libp2p/go-libp2p#1627](https://github.com/libp2p/go-libp2p/pull/1627))
  - ping: fix flaky test (#1617) ([libp2p/go-libp2p#1617](https://github.com/libp2p/go-libp2p/pull/1617))
  - chore: use the new multiaddr.Contains function (#1618) ([libp2p/go-libp2p#1618](https://github.com/libp2p/go-libp2p/pull/1618))
  - chore: stop using the deprecated mux.MuxedConn (#1614) ([libp2p/go-libp2p#1614](https://github.com/libp2p/go-libp2p/pull/1614))
  - logging: Add canonical log for misbehaving peers (#1600) ([libp2p/go-libp2p#1600](https://github.com/libp2p/go-libp2p/pull/1600))
  - use multiaddr ipcidr to parse multiaddr filters (#1606) ([libp2p/go-libp2p#1606](https://github.com/libp2p/go-libp2p/pull/1606))
  - tcp: unexport TcpTransport.Upgrader (#1596) ([libp2p/go-libp2p#1596](https://github.com/libp2p/go-libp2p/pull/1596))
  - muxer: expose func to create MuxedConn from backing Conn (#1609) ([libp2p/go-libp2p#1609](https://github.com/libp2p/go-libp2p/pull/1609))
  - remove legacy mDNS implementation (#1192) ([libp2p/go-libp2p#1192](https://github.com/libp2p/go-libp2p/pull/1192))
  - feat: allow dialing wss peers using DNS multiaddrs
  - fix natManager to close natManager.nat (#1468) ([libp2p/go-libp2p#1468](https://github.com/libp2p/go-libp2p/pull/1468))
  - Expose DefaultPerPeerRateLimit as var (#1580) ([libp2p/go-libp2p#1580](https://github.com/libp2p/go-libp2p/pull/1580))
  - swarm: add ListenClose (#1586) ([libp2p/go-libp2p#1586](https://github.com/libp2p/go-libp2p/pull/1586))
  - identify: Fix flaky tests (#1555) ([libp2p/go-libp2p#1555](https://github.com/libp2p/go-libp2p/pull/1555))
  - autonat: fix flaky TestAutoNATPrivate  (#1581) ([libp2p/go-libp2p#1581](https://github.com/libp2p/go-libp2p/pull/1581))
  - pstoremanager: fix test timeout (#1588) ([libp2p/go-libp2p#1588](https://github.com/libp2p/go-libp2p/pull/1588))
  - swarm: send notifications synchronously (#1562) ([libp2p/go-libp2p#1562](https://github.com/libp2p/go-libp2p/pull/1562))
  - basichost: fix flaky TestSignedPeerRecordWithNoListenAddrs (#1559) ([libp2p/go-libp2p#1559](https://github.com/libp2p/go-libp2p/pull/1559))
  - identify: fix flaky TestIdentifyDeltaOnProtocolChange (again) (#1582) ([libp2p/go-libp2p#1582](https://github.com/libp2p/go-libp2p/pull/1582))
  - tls: fix flaky TestInvalidCerts on Windows ([libp2p/go-libp2p#1560](https://github.com/libp2p/go-libp2p/pull/1560))
  - chore: log autorelay start failure error ([libp2p/go-libp2p#1583](https://github.com/libp2p/go-libp2p/pull/1583))
  - Add sanity check assertion (#1570) ([libp2p/go-libp2p#1570](https://github.com/libp2p/go-libp2p/pull/1570))
  - swarm: speed up the TestDialWorkerLoopConcurrentFailureStress test (#1573) ([libp2p/go-libp2p#1573](https://github.com/libp2p/go-libp2p/pull/1573))
  - chore: update examples to go-libp2p v0.20.0 (#1557) ([libp2p/go-libp2p#1557](https://github.com/libp2p/go-libp2p/pull/1557))
  - Wait a couple seconds for ID event (#1568) ([libp2p/go-libp2p#1568](https://github.com/libp2p/go-libp2p/pull/1568))
  - remove workspace and packages section from README (#1563) ([libp2p/go-libp2p#1563](https://github.com/libp2p/go-libp2p/pull/1563))
  - fix: mkreleaselog exclude autogenerated files (#1567) ([libp2p/go-libp2p#1567](https://github.com/libp2p/go-libp2p/pull/1567))
  - move resource manager integration tests to p2p/test/ (#1561) ([libp2p/go-libp2p#1561](https://github.com/libp2p/go-libp2p/pull/1561))
  - swarm: only dial a single transport in TestDialWorkerLoopBasic (#1526) ([libp2p/go-libp2p#1526](https://github.com/libp2p/go-libp2p/pull/1526))
- github.com/libp2p/go-libp2p-core (v0.16.1 -> v0.19.1):
  - Update version.json
  - Remove btcsuite/btcd dep (#272) ([libp2p/go-libp2p-core#272](https://github.com/libp2p/go-libp2p-core/pull/272))
  - Release v0.19.0 (#271) ([libp2p/go-libp2p-core#271](https://github.com/libp2p/go-libp2p-core/pull/271))
  - Add endpoint parameter to the OpenConnection method for ResourceManager (#257) ([libp2p/go-libp2p-core#257](https://github.com/libp2p/go-libp2p-core/pull/257))
  - Release v0.18.0 (#270) ([libp2p/go-libp2p-core#270](https://github.com/libp2p/go-libp2p-core/pull/270))
  - Add canonical peer status logging with sampling (#269) ([libp2p/go-libp2p-core#269](https://github.com/libp2p/go-libp2p-core/pull/269))
  - canonicallog: reduce log level to warning (#268) ([libp2p/go-libp2p-core#268](https://github.com/libp2p/go-libp2p-core/pull/268))
  - Only log once if we failed to convert from netAddr (#264) ([libp2p/go-libp2p-core#264](https://github.com/libp2p/go-libp2p-core/pull/264))
  - remove deprecated mux package (#265) ([libp2p/go-libp2p-core#265](https://github.com/libp2p/go-libp2p-core/pull/265))
  - remove the peer.Set (#261) ([libp2p/go-libp2p-core#261](https://github.com/libp2p/go-libp2p-core/pull/261))
  - Bump version (#259) ([libp2p/go-libp2p-core#259](https://github.com/libp2p/go-libp2p-core/pull/259))
  - Add canonical log for misbehaving peers (#258) ([libp2p/go-libp2p-core#258](https://github.com/libp2p/go-libp2p-core/pull/258))
- github.com/libp2p/go-libp2p-kad-dht (v0.16.0 -> v0.17.0):
  - Chore: bump version to v0.17.0
  - Update go-libp2p to v0.20.3 ([libp2p/go-libp2p-kad-dht#778](https://github.com/libp2p/go-libp2p-kad-dht/pull/778))
- github.com/libp2p/go-libp2p-peerstore (v0.6.0 -> v0.7.1):
  - Release v0.7.1 ([libp2p/go-libp2p-peerstore#202](https://github.com/libp2p/go-libp2p-peerstore/pull/202))
  - stop using the peer.Set (#201) ([libp2p/go-libp2p-peerstore#201](https://github.com/libp2p/go-libp2p-peerstore/pull/201))
  - feat: Use a clock interface in pstoreds as well ([libp2p/go-libp2p-peerstore#200](https://github.com/libp2p/go-libp2p-peerstore/pull/200))
  - feat: use a clock interface to better support testing for pstoremem ([libp2p/go-libp2p-peerstore#199](https://github.com/libp2p/go-libp2p-peerstore/pull/199))
  - pstoremem: fix slice preallocation in GetProtocols (#198) ([libp2p/go-libp2p-peerstore#198](https://github.com/libp2p/go-libp2p-peerstore/pull/198))
  - remove all calls to peer.ID.Validate ([libp2p/go-libp2p-peerstore#194](https://github.com/libp2p/go-libp2p-peerstore/pull/194))
  - remove the addr package ([libp2p/go-libp2p-peerstore#195](https://github.com/libp2p/go-libp2p-peerstore/pull/195))
  - move AddrList to pstoremen, unexport it ([libp2p/go-libp2p-peerstore#193](https://github.com/libp2p/go-libp2p-peerstore/pull/193))
  - optimize allocations in the memory address book ([libp2p/go-libp2p-peerstore#191](https://github.com/libp2p/go-libp2p-peerstore/pull/191))
  - implement a clean shutdown for the memory address book ([libp2p/go-libp2p-peerstore#192](https://github.com/libp2p/go-libp2p-peerstore/pull/192))
- github.com/libp2p/go-libp2p-resource-manager (v0.3.0 -> v0.5.3):
  - Chore: release patch v0.5.3 ([libp2p/go-libp2p-resource-manager#77](https://github.com/libp2p/go-libp2p-resource-manager/pull/77))
  - Add namespace to metrics ([libp2p/go-libp2p-resource-manager#79](https://github.com/libp2p/go-libp2p-resource-manager/pull/79))
  - Fix usage of make to reserve capacity, not values ([libp2p/go-libp2p-resource-manager#76](https://github.com/libp2p/go-libp2p-resource-manager/pull/76))
  - Add package docs ([libp2p/go-libp2p-resource-manager#75](https://github.com/libp2p/go-libp2p-resource-manager/pull/75))
  - chore: Release v0.5.2 ([libp2p/go-libp2p-resource-manager#74](https://github.com/libp2p/go-libp2p-resource-manager/pull/74))
  - Record which direction the resource was blocked ([libp2p/go-libp2p-resource-manager#72](https://github.com/libp2p/go-libp2p-resource-manager/pull/72))
  - Simplify mem graphs in stock Grafana dashboard ([libp2p/go-libp2p-resource-manager#73](https://github.com/libp2p/go-libp2p-resource-manager/pull/73))
  - feat: Handle multiple instances in stock Grafana dashboard ([libp2p/go-libp2p-resource-manager#70](https://github.com/libp2p/go-libp2p-resource-manager/pull/70))
  - Use templated version of Grafana dashboard json ([libp2p/go-libp2p-resource-manager#69](https://github.com/libp2p/go-libp2p-resource-manager/pull/69))
  - Release v0.5.1 ([libp2p/go-libp2p-resource-manager#66](https://github.com/libp2p/go-libp2p-resource-manager/pull/66))
  - Implement `json.Marshaler` interface for LimitConfig ([libp2p/go-libp2p-resource-manager#67](https://github.com/libp2p/go-libp2p-resource-manager/pull/67))
  - Don't wait for a chan that will never close ([libp2p/go-libp2p-resource-manager#65](https://github.com/libp2p/go-libp2p-resource-manager/pull/65))
  - release v0.5.0 ([libp2p/go-libp2p-resource-manager#60](https://github.com/libp2p/go-libp2p-resource-manager/pull/60))
  - Add docs around WithAllowlistedMultiaddrs. Expose allowlist ([libp2p/go-libp2p-resource-manager#63](https://github.com/libp2p/go-libp2p-resource-manager/pull/63))
  - fix marshalling of allowlisted scopes ([libp2p/go-libp2p-resource-manager#62](https://github.com/libp2p/go-libp2p-resource-manager/pull/62))
  - docs: describe how the limiter is configured, and how limits are scaled (#59) ([libp2p/go-libp2p-resource-manager#59](https://github.com/libp2p/go-libp2p-resource-manager/pull/59))
  - don't limit the number of FDs on Windows (#58) ([libp2p/go-libp2p-resource-manager#58](https://github.com/libp2p/go-libp2p-resource-manager/pull/58))
  - Add ability to configure allowlist limits ([libp2p/go-libp2p-resource-manager#57](https://github.com/libp2p/go-libp2p-resource-manager/pull/57))
  - rewrite limits to allow auto-scaling ([libp2p/go-libp2p-resource-manager#48](https://github.com/libp2p/go-libp2p-resource-manager/pull/48))
  - Release v0.4.0 ([libp2p/go-libp2p-resource-manager#56](https://github.com/libp2p/go-libp2p-resource-manager/pull/56))
  - feat: Out of the box metrics for resource manager ([libp2p/go-libp2p-resource-manager#54](https://github.com/libp2p/go-libp2p-resource-manager/pull/54))
  - feat: Allowlist ([libp2p/go-libp2p-resource-manager#47](https://github.com/libp2p/go-libp2p-resource-manager/pull/47))
  - trace the scope as a JSON object (#52) ([libp2p/go-libp2p-resource-manager#52](https://github.com/libp2p/go-libp2p-resource-manager/pull/52))
  - include current limits in debug messages ([libp2p/go-libp2p-resource-manager#42](https://github.com/libp2p/go-libp2p-resource-manager/pull/42))
  - add an ID to spans (#44) ([libp2p/go-libp2p-resource-manager#44](https://github.com/libp2p/go-libp2p-resource-manager/pull/44))
  - add a DefaultLimitConfig with infinite limits (#41) ([libp2p/go-libp2p-resource-manager#41](https://github.com/libp2p/go-libp2p-resource-manager/pull/41))
  - export the TraceEvt (#40) ([libp2p/go-libp2p-resource-manager#40](https://github.com/libp2p/go-libp2p-resource-manager/pull/40))
  - trace exact timestamps (#39) ([libp2p/go-libp2p-resource-manager#39](https://github.com/libp2p/go-libp2p-resource-manager/pull/39))
  - skip events that don't change anything in tracer (#38) ([libp2p/go-libp2p-resource-manager#38](https://github.com/libp2p/go-libp2p-resource-manager/pull/38))
  - fix typos in MetricsReporter docs
  - fix shadowing of service name (#37) ([libp2p/go-libp2p-resource-manager#37](https://github.com/libp2p/go-libp2p-resource-manager/pull/37))
  - add a timestamp to trace events (#34) ([libp2p/go-libp2p-resource-manager#34](https://github.com/libp2p/go-libp2p-resource-manager/pull/34))
- github.com/libp2p/go-libp2p-testing (v0.9.2 -> v0.11.0):
  - Release v0.11.0 ([libp2p/go-libp2p-testing#64](https://github.com/libp2p/go-libp2p-testing/pull/64))
  - Remove unused bench file and dep ([libp2p/go-libp2p-testing#63](https://github.com/libp2p/go-libp2p-testing/pull/63))
  - Release v0.10.0 ([libp2p/go-libp2p-testing#62](https://github.com/libp2p/go-libp2p-testing/pull/62))
  - Update go-libp2p-core dep ([libp2p/go-libp2p-testing#61](https://github.com/libp2p/go-libp2p-testing/pull/61))
  - remove suites (#60) ([libp2p/go-libp2p-testing#60](https://github.com/libp2p/go-libp2p-testing/pull/60))
  - don't continue on read / write error in stream suite (#59) ([libp2p/go-libp2p-testing#59](https://github.com/libp2p/go-libp2p-testing/pull/59))
  - remove debug logging from stream and muxer suite ([libp2p/go-libp2p-testing#58](https://github.com/libp2p/go-libp2p-testing/pull/58))
  - remove Travis package (#57) ([libp2p/go-libp2p-testing#57](https://github.com/libp2p/go-libp2p-testing/pull/57))
- github.com/lucas-clemente/quic-go (v0.27.1 -> v0.28.0):
  - update for Go 1.19beta1 (#3460) ([lucas-clemente/quic-go#3460](https://github.com/lucas-clemente/quic-go/pull/3460))
  - Deduplicate Alt-Svc header values (#3461) ([lucas-clemente/quic-go#3461](https://github.com/lucas-clemente/quic-go/pull/3461))
  - only set DF for sockets that can handle it (#3448) ([lucas-clemente/quic-go#3448](https://github.com/lucas-clemente/quic-go/pull/3448))
  - fix flaky HTTP/3 request body test (#3447) ([lucas-clemente/quic-go#3447](https://github.com/lucas-clemente/quic-go/pull/3447))
  - make the keep alive interval configurable (#3444) ([lucas-clemente/quic-go#3444](https://github.com/lucas-clemente/quic-go/pull/3444))
  - implement QUIC v2 ([lucas-clemente/quic-go#3432](https://github.com/lucas-clemente/quic-go/pull/3432))
  - allow HTTP clients and servers to take over the request stream ([lucas-clemente/quic-go#3437](https://github.com/lucas-clemente/quic-go/pull/3437))
  - remove the http3.DataStreamer (#3435) ([lucas-clemente/quic-go#3435](https://github.com/lucas-clemente/quic-go/pull/3435))
  - always reset header buffer, even when QPACK encoding fails (#3436) ([lucas-clemente/quic-go#3436](https://github.com/lucas-clemente/quic-go/pull/3436))
  - Change "HTTP/3" to "HTTP/3.0". (#3439) ([lucas-clemente/quic-go#3439](https://github.com/lucas-clemente/quic-go/pull/3439))
  - remove stray http3 connection file
  - pass frame / stream type parsing errors to the hijacker callbacks ([lucas-clemente/quic-go#3429](https://github.com/lucas-clemente/quic-go/pull/3429))
  - add test for bidirectional stream hijacker (#3434) ([lucas-clemente/quic-go#3434](https://github.com/lucas-clemente/quic-go/pull/3434))
  - make it possible to parse a varint at the end of a reader (#3428) ([lucas-clemente/quic-go#3428](https://github.com/lucas-clemente/quic-go/pull/3428))
  - don't ignore errors that occur when the TLS ClientHello is generated ([lucas-clemente/quic-go#3424](https://github.com/lucas-clemente/quic-go/pull/3424))
  - don't send path MTU probe packets on a timer (#3423) ([lucas-clemente/quic-go#3423](https://github.com/lucas-clemente/quic-go/pull/3423))
  - introduce a http3.RoundTripOpt to prevent closing of request stream (#3411) ([lucas-clemente/quic-go#3411](https://github.com/lucas-clemente/quic-go/pull/3411))
  - don't close the request stream when http3.DataStreamer was used (#3413) ([lucas-clemente/quic-go#3413](https://github.com/lucas-clemente/quic-go/pull/3413))
  - do not embed http.Server in http3.Server (#3397) ([lucas-clemente/quic-go#3397](https://github.com/lucas-clemente/quic-go/pull/3397))
  - remove error return value from ComposeVersionNegotiation (#3410) ([lucas-clemente/quic-go#3410](https://github.com/lucas-clemente/quic-go/pull/3410))
  - don't set receive buffer if it is already large enough (#3407) ([lucas-clemente/quic-go#3407](https://github.com/lucas-clemente/quic-go/pull/3407))
  - clone TLS conf in newClient (#3400) ([lucas-clemente/quic-go#3400](https://github.com/lucas-clemente/quic-go/pull/3400))
  - remove warning comments of stable implementation (#3399) ([lucas-clemente/quic-go#3399](https://github.com/lucas-clemente/quic-go/pull/3399))
  - fix parsing of request path for Extended CONNECT requests (#3388) ([lucas-clemente/quic-go#3388](https://github.com/lucas-clemente/quic-go/pull/3388))
  - update docs to reflect that we support RFC 9221 (Unreliable Datagrams) (#3382) ([lucas-clemente/quic-go#3382](https://github.com/lucas-clemente/quic-go/pull/3382))
  - fix deadlock on concurrent http3.Server.Serve and Close calls (#3387) ([lucas-clemente/quic-go#3387](https://github.com/lucas-clemente/quic-go/pull/3387))
  - reduce flakiness of deadline integration tests (#3383) ([lucas-clemente/quic-go#3383](https://github.com/lucas-clemente/quic-go/pull/3383))
  - protect against concurrent use of Stream.Write (#3381) ([lucas-clemente/quic-go#3381](https://github.com/lucas-clemente/quic-go/pull/3381))
  - protect against concurrent use of Stream.Read (#3380) ([lucas-clemente/quic-go#3380](https://github.com/lucas-clemente/quic-go/pull/3380))
  - Expose quic server closed err (#3395) ([lucas-clemente/quic-go#3395](https://github.com/lucas-clemente/quic-go/pull/3395))
  - implement HTTP/3 unidirectional stream hijacking (#3389) ([lucas-clemente/quic-go#3389](https://github.com/lucas-clemente/quic-go/pull/3389))
  - add LocalAddr and RemoteAddr functions to http3.StreamCreator (#3384) ([lucas-clemente/quic-go#3384](https://github.com/lucas-clemente/quic-go/pull/3384))
  - extend the HTTP/3 API for WebTransport support ([lucas-clemente/quic-go#3362](https://github.com/lucas-clemente/quic-go/pull/3362))
  - remove unneeded network from custom dial function used in HTTP/3 (#3368) ([lucas-clemente/quic-go#3368](https://github.com/lucas-clemente/quic-go/pull/3368))
- github.com/multiformats/go-multiaddr (v0.5.0 -> v0.6.0):
  - release v0.6.0 ([multiformats/go-multiaddr#178](https://github.com/multiformats/go-multiaddr/pull/178))
  - add WebTransport multiaddr components ([multiformats/go-multiaddr#176](https://github.com/multiformats/go-multiaddr/pull/176))
  - add ipcidr support (#177) ([multiformats/go-multiaddr#177](https://github.com/multiformats/go-multiaddr/pull/177))
  - add a Contains function (#172) ([multiformats/go-multiaddr#172](https://github.com/multiformats/go-multiaddr/pull/172))
- github.com/multiformats/go-multibase (v0.1.0 -> v0.1.1):
  - chore: release version 0.1.1
  - fix: add new emoji codepoint for Base256Emoji 🐉
- github.com/multiformats/go-multihash (v0.2.0 -> v0.2.1):
  - chore: release v0.2.1
  - feat: adding tests and finish variable sized functions
  - feat: add support for variable length hash functions
  - adding blake3 tests and fixing an incorrect error message. (#158) ([multiformats/go-multihash#158](https://github.com/multiformats/go-multihash/pull/158))

</details>

### Contributors

| Contributor | Commits | Lines ± | Files Changed |
|-------------|---------|---------|---------------|
| Marten Seemann | 129 | +5612/-9895 | 345 |
| Marco Munizaga | 109 | +7689/-3221 | 181 |
| vyzo | 64 | +3972/-657 | 125 |
| Jorropo | 19 | +1977/-1611 | 109 |
| Steven Allen | 30 | +633/-593 | 54 |
| Jeromy Johnson | 5 | +1032/-64 | 16 |
| Marcin Rataj | 21 | +406/-200 | 59 |
| Michael Muré | 6 | +335/-250 | 14 |
| Gus Eggert | 8 | +336/-104 | 31 |
| Claudia Richoux | 3 | +181/-63 | 9 |
| Steve Loeppky | 11 | +95/-141 | 11 |
| Ian Davis | 4 | +126/-58 | 6 |
| hareku | 3 | +172/-6 | 7 |
| Ivan Trubach | 1 | +98/-74 | 6 |
| Raúl Kripalani | 2 | +69/-62 | 9 |
| Seungbae Yu | 1 | +41/-41 | 13 |
| Julien Muret | 1 | +60/-7 | 2 |
| Mark Gaiser | 1 | +64/-0 | 5 |
| Lars Gierth | 1 | +20/-29 | 4 |
| Cole Brown | 4 | +27/-19 | 4 |
| Chao Fei | 2 | +15/-30 | 9 |
| Nuno Diegues | 2 | +25/-18 | 9 |
| Jakub Sztandera | 1 | +37/-0 | 3 |
| Wiktor Jurkiewicz | 1 | +13/-5 | 1 |
| c r | 1 | +11/-6 | 3 |
| Christian Stewart | 1 | +15/-2 | 4 |
| Matt Robenolt | 1 | +15/-1 | 2 |
| aarshkshah1992 | 2 | +8/-2 | 2 |
| link2xt | 1 | +4/-4 | 1 |
| Aaron Riekenberg | 1 | +4/-4 | 4 |
| web3-bot | 3 | +7/-0 | 3 |
| Adrian Lanzafame | 1 | +3/-3 | 1 |
| Dmitriy Ryajov | 2 | +2/-3 | 2 |
| Brendan O'Brien | 1 | +5/-0 | 1 |
| millken | 1 | +1/-1 | 1 |
| lostystyg | 1 | +1/-1 | 1 |
| kpcyrd | 1 | +1/-1 | 1 |
| anders | 1 | +1/-1 | 1 |
| Rod Vagg | 1 | +1/-1 | 1 |
| Matt Joiner | 1 | +1/-1 | 1 |
| Leo Balduf | 1 | +1/-1 | 1 |
| Didrik Nordström | 1 | +2/-0 | 1 |
| Daniel Norman | 1 | +1/-1 | 1 |
| Antonio Navarro Perez | 1 | +1/-1 | 1 |
| Adin Schmahmann | 1 | +1/-1 | 1 |
| Lucas Molas | 1 | +1/-0 | 1 |
