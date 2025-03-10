# FrontendTrigger 单元验证

## 测试目标

测试目标是验证FrontendTrigger子模块的功能。

FrontendTrigger的功能分为两部分：断点设置和断点触发。

对于断点设置，FrontendTrigger接收来自前端的update请求，基于该请求设置内部的断点寄存器状态。

对于断点触发，FrontendTrigger接收pc信息，根据pc和寄存器存储的基准值的关系，决定是否触发断点，返回断点触发行为。

测试基本流程为：

TBD

## 测试环境 Env

本测试基于toffee封装测试环境。

其中，对DUT的数据职责封装由bundle完成，可参见当前目录下的bundle目录。

对DUT的行为抽象由本目录下的agent目录完成，提供两个接口：

set_breakpoint：设置断点，返回内部断点的状态

check：传入pc，检查断点触发的情况。注意：pc是根据ftq请求的startAddr连续+2得到的。

## 功能点和测试点

所有的测试点如下：

| 序号   | 功能          | 名称              | 描述                                                |
|------|-------------|-----------------|------------------------------------------------------------------|
| 1\.1 | 断点设置和检查     | select1判定       | 给定tdata1的select位为1，随机构造其它输入，检查断点是否没有触发                                                        |
| 1\.2\.1 | 断点设置和检查     | select0关系匹配判定  | 给定tdata1的select位为0，构造PC与tdata2数据的关系同tdata2的match位匹配的输入，检查断点是否触发                               | 
| 1\.2\.2 | 断点设置和检查     | select0关系不匹配判定 | 给定tdata1的select位为0，构造PC与tdata2数据的关系同tdata2的match位不匹配的输入，检查断点是否触发                              |
| 2\.1 | 链式断点        | chain位测试        | 对每个trigger，在满足PC断点触发条件的情况下，设置chain位，检查断点是否一定不触发                                               |
| 2\.2 | 链式断点        | timing测试        | 对两个trigger，仅设置前一个trigger的chain位，且两trigger的timing位不同，随机设置PC等，测试后一个trigger是否一定不触发               | 
| 2\.3\.1 | 链式断点        | 未命中测试           | 对两个trigger，仅设置前一个trigger的chain位，且两trigger的timing位相同，设置后一个trigger命中而前一个未命中，检查后一个trigger是否一定不触发 |
| 2\.3\.2 | 链式断点        | 命中测试            | 对两个trigger，仅设置前一个trigger的chain位，且两trigger的timing位相同且均命中，检查后一个trigger是否触发 |


## Env提供的验证接口(API)

为了让测试用例更通用，具有继承性，本Env提供的接口**对外屏蔽了电路引脚和时序，且接口保持稳定**：

## 用例说明

TBD

## 检查列表

- [ ] 本文档符合指定[模板]()要求
- [ ] Env提供的API不包含任何DUT引脚和时序信息
- [ ] Env的API保持稳定（共有[ X ]个）
- [ ] Env中对所支持的RTL版本（支持版本[ X ]）进行了检查
- [ ] 功能点（共有[ X ]个）与[设计文档]()一致
- [ ] 检查点（共有[ X ]个）覆盖所有功能点
- [ ] 检查点的输入不依赖任何DUT引脚，仅依赖Env的标准API
- [ ] 所有测试用例（共有[ X ]个）都对功能检查点进行了反标
- [ ] 所有测试用例都是通过 assert 进行的结果判断
- [ ] 所有DUT或对应wrapper都是通过fixture创建
- [ ] 在上述fixture中对RTL版本进行了检查
- [ ] 创建DUT或对应wrapper的fixture进行了功能和代码行覆盖率统计
- [ ] 设置代码行覆盖率时对过滤需求进行了检查

## TODO

测试用例

参考模型

文档：测试流程