# 示例输入：从可用性测试报告到产品待办列表

> 本示例中的产品、团队和所有数据均为虚构，仅用于演示 user-story-backlog skill。

本示例演示两个 skill 的串联：输入是 usability-synthesis skill 生成的分析报告，见 [`../../usability-synthesis/examples/output-report.md`](../../usability-synthesis/examples/output-report.md)。

## 用户发给 Claude 的消息

> 这是「邻里健康」小程序第一轮可用性测试的分析报告（附后）。帮我把 P0 和 P1 的问题整理成产品待办列表，排好优先级和里程碑。
>
> 补充一些背景：
> - 团队是 1 名前端、1 名后端、1 名设计，两周一个迭代
> - 大部分居民已经在社区卫生服务中心做过实名登记，但也有一部分新用户还没有实名
> - 下个月社区有一场针对老年人的健康讲座，会现场推广小程序，希望在那之前把影响老年人的问题先解决
>
> [附：「邻里健康」小程序 可用性测试分析报告]
