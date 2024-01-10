# `v2ray-core\testing\mocks\outbound.go`

```
// Code generated by MockGen. DO NOT EDIT.
// Source: v2ray.com/core/features/outbound (interfaces: Manager,HandlerSelector)

// Package mocks is a generated GoMock package.
package mocks

import (
    context "context"  // 导入 context 包
    gomock "github.com/golang/mock/gomock"  // 导入 gomock 包
    reflect "reflect"  // 导入 reflect 包
    outbound "v2ray.com/core/features/outbound"  // 导入 v2ray.com/core/features/outbound 包
)

// OutboundManager is a mock of Manager interface
type OutboundManager struct {
    ctrl     *gomock.Controller  // 控制器
    recorder *OutboundManagerMockRecorder  // OutboundManager 的 mock recorder
}

// OutboundManagerMockRecorder is the mock recorder for OutboundManager
type OutboundManagerMockRecorder struct {
    mock *OutboundManager  // OutboundManager 的 mock recorder
}

// NewOutboundManager creates a new mock instance
func NewOutboundManager(ctrl *gomock.Controller) *OutboundManager {
    mock := &OutboundManager{ctrl: ctrl}  // 创建 OutboundManager 的 mock 实例
    mock.recorder = &OutboundManagerMockRecorder{mock}  // 创建 OutboundManager 的 mock recorder
    return mock
}

// EXPECT returns an object that allows the caller to indicate expected use
func (m *OutboundManager) EXPECT() *OutboundManagerMockRecorder {
    return m.recorder  // 返回 OutboundManager 的 mock recorder
}

// AddHandler mocks base method
func (m *OutboundManager) AddHandler(arg0 context.Context, arg1 outbound.Handler) error {
    m.ctrl.T.Helper()  // 控制器的辅助方法
    ret := m.ctrl.Call(m, "AddHandler", arg0, arg1)  // 调用控制器的 Call 方法
    ret0, _ := ret[0].(error)  // 获取返回值并断言为 error 类型
    return ret0  // 返回结果
}

// AddHandler indicates an expected call of AddHandler
func (mr *OutboundManagerMockRecorder) AddHandler(arg0, arg1 interface{}) *gomock.Call {
    mr.mock.ctrl.T.Helper()  // 控制器的辅助方法
    return mr.mock.ctrl.RecordCallWithMethodType(mr.mock, "AddHandler", reflect.TypeOf((*OutboundManager)(nil).AddHandler), arg0, arg1)  // 记录调用信息
}

// Close mocks base method
func (m *OutboundManager) Close() error {
    m.ctrl.T.Helper()  // 控制器的辅助方法
    ret := m.ctrl.Call(m, "Close")  // 调用控制器的 Call 方法
    ret0, _ := ret[0].(error)  // 获取返回值并断言为 error 类型
    return ret0  // 返回结果
}

// Close indicates an expected call of Close
func (mr *OutboundManagerMockRecorder) Close() *gomock.Call {
    mr.mock.ctrl.T.Helper()  // 控制器的辅助方法
    # 使用 mock 对象的 ctrl.RecordCallWithMethodType 方法记录 Close 方法的调用
    return mr.mock.ctrl.RecordCallWithMethodType(mr.mock, "Close", reflect.TypeOf((*OutboundManager)(nil).Close))
// GetDefaultHandler mocks base method
func (m *OutboundManager) GetDefaultHandler() outbound.Handler {
    // 标记当前方法是辅助方法
    m.ctrl.T.Helper()
    // 调用控制器的Call方法，传入当前对象和方法名"GetDefaultHandler"
    ret := m.ctrl.Call(m, "GetDefaultHandler")
    // 将返回结果转换为outbound.Handler类型
    ret0, _ := ret[0].(outbound.Handler)
    // 返回转换后的结果
    return ret0
}

// GetDefaultHandler indicates an expected call of GetDefaultHandler
func (mr *OutboundManagerMockRecorder) GetDefaultHandler() *gomock.Call {
    // 标记当前方法是辅助方法
    mr.mock.ctrl.T.Helper()
    // 返回一个记录了方法调用信息的gomock.Call对象
    return mr.mock.ctrl.RecordCallWithMethodType(mr.mock, "GetDefaultHandler", reflect.TypeOf((*OutboundManager)(nil).GetDefaultHandler))
}

// GetHandler mocks base method
func (m *OutboundManager) GetHandler(arg0 string) outbound.Handler {
    // 标记当前方法是辅助方法
    m.ctrl.T.Helper()
    // 调用控制器的Call方法，传入当前对象、方法名"GetHandler"和参数arg0
    ret := m.ctrl.Call(m, "GetHandler", arg0)
    // 将返回结果转换为outbound.Handler类型
    ret0, _ := ret[0].(outbound.Handler)
    // 返回转换后的结果
    return ret0
}

// GetHandler indicates an expected call of GetHandler
func (mr *OutboundManagerMockRecorder) GetHandler(arg0 interface{}) *gomock.Call {
    // 标记当前方法是辅助方法
    mr.mock.ctrl.T.Helper()
    // 返回一个记录了方法调用信息的gomock.Call对象
    return mr.mock.ctrl.RecordCallWithMethodType(mr.mock, "GetHandler", reflect.TypeOf((*OutboundManager)(nil).GetHandler), arg0)
}

// RemoveHandler mocks base method
func (m *OutboundManager) RemoveHandler(arg0 context.Context, arg1 string) error {
    // 标记当前方法是辅助方法
    m.ctrl.T.Helper()
    // 调用控制器的Call方法，传入当前对象、方法名"RemoveHandler"和参数arg0、arg1
    ret := m.ctrl.Call(m, "RemoveHandler", arg0, arg1)
    // 将返回结果转换为error类型
    ret0, _ := ret[0].(error)
    // 返回转换后的结果
    return ret0
}

// RemoveHandler indicates an expected call of RemoveHandler
func (mr *OutboundManagerMockRecorder) RemoveHandler(arg0, arg1 interface{}) *gomock.Call {
    // 标记当前方法是辅助方法
    mr.mock.ctrl.T.Helper()
    // 返回一个记录了方法调用信息的gomock.Call对象
    return mr.mock.ctrl.RecordCallWithMethodType(mr.mock, "RemoveHandler", reflect.TypeOf((*OutboundManager)(nil).RemoveHandler), arg0, arg1)
}

// Start mocks base method
func (m *OutboundManager) Start() error {
    // 标记当前方法是辅助方法
    m.ctrl.T.Helper()
    // 调用控制器的Call方法，传入当前对象和方法名"Start"
    ret := m.ctrl.Call(m, "Start")
    // 将返回结果转换为error类型
    ret0, _ := ret[0].(error)
    // 返回转换后的结果
    return ret0
}

// Start indicates an expected call of Start
func (mr *OutboundManagerMockRecorder) Start() *gomock.Call {
    // 标记当前方法是辅助方法
    mr.mock.ctrl.T.Helper();
    # 使用 mock 对象的 ctrl.RecordCallWithMethodType 方法记录对 Start 方法的调用
    return mr.mock.ctrl.RecordCallWithMethodType(mr.mock, "Start", reflect.TypeOf((*OutboundManager)(nil).Start))
// Type 方法的模拟，返回值为接口类型
func (m *OutboundManager) Type() interface{} {
    // 标记当前方法为辅助方法
    m.ctrl.T.Helper()
    // 调用控制器的 Call 方法，传入当前对象和方法名"Type"，返回结果
    ret := m.ctrl.Call(m, "Type")
    // 将结果的第一个元素转换为接口类型
    ret0, _ := ret[0].(interface{})
    // 返回转换后的结果
    return ret0
}

// Type 方法的预期调用
func (mr *OutboundManagerMockRecorder) Type() *gomock.Call {
    // 标记当前方法为辅助方法
    mr.mock.ctrl.T.Helper()
    // 返回控制器的 RecordCallWithMethodType 方法的调用结果，传入当前对象、方法名"Type"和方法类型
    return mr.mock.ctrl.RecordCallWithMethodType(mr.mock, "Type", reflect.TypeOf((*OutboundManager)(nil).Type))
}

// OutboundHandlerSelector 是 HandlerSelector 接口的模拟
type OutboundHandlerSelector struct {
    ctrl     *gomock.Controller
    recorder *OutboundHandlerSelectorMockRecorder
}

// OutboundHandlerSelectorMockRecorder 是 OutboundHandlerSelector 的模拟记录器
type OutboundHandlerSelectorMockRecorder struct {
    mock *OutboundHandlerSelector
}

// 创建一个新的 OutboundHandlerSelector 模拟实例
func NewOutboundHandlerSelector(ctrl *gomock.Controller) *OutboundHandlerSelector {
    // 创建 OutboundHandlerSelector 对象，并设置控制器和模拟记录器
    mock := &OutboundHandlerSelector{ctrl: ctrl}
    mock.recorder = &OutboundHandlerSelectorMockRecorder{mock}
    return mock
}

// EXPECT 返回一个对象，允许调用者指示预期的使用
func (m *OutboundHandlerSelector) EXPECT() *OutboundHandlerSelectorMockRecorder {
    // 返回 OutboundHandlerSelectorMockRecorder 对象
    return m.recorder
}

// Select 方法的模拟，参数为字符串数组，返回值为字符串数组
func (m *OutboundHandlerSelector) Select(arg0 []string) []string {
    // 标记当前方法为辅助方法
    m.ctrl.T.Helper()
    // 调用控制器的 Call 方法，传入当前对象、方法名"Select"和参数 arg0，返回结果
    ret := m.ctrl.Call(m, "Select", arg0)
    // 将结果的第一个元素转换为字符串数组
    ret0, _ := ret[0].([]string)
    // 返回转换后的结果
    return ret0
}

// Select 方法的预期调用
func (mr *OutboundHandlerSelectorMockRecorder) Select(arg0 interface{}) *gomock.Call {
    // 标记当前方法为辅助方法
    mr.mock.ctrl.T.Helper()
    // 返回控制器的 RecordCallWithMethodType 方法的调用结果，传入当前对象、方法名"Select"、方法类型和参数类型
    return mr.mock.ctrl.RecordCallWithMethodType(mr.mock, "Select", reflect.TypeOf((*OutboundHandlerSelector)(nil).Select), arg0)
}
```