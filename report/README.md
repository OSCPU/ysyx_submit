# DC & VCS report

SoC和后端团队的report返回后，前端的同学需要按照以下步骤确认报告内容及对代码做出相应的修改。

## 一、确认功能正确性
* 阅读VCS报告report/ysyx_xxxxxx/vcs_report，确认是否寸在 **Error** ，如果VCS程序未通过，则首先需要修改代码以确保功能正确。

## 二、消除DC综合报告Warning
* 阅读DC综合报告report/ysyx_xxxxxx/dc_report的 **SYNTHESIS REPORT** 部分。

## 三、清楚不带复位端的cell
* 阅读DC综合报告report/ysyx_xxxxxx/dc_report的 **SYNTHESIS REPORT** 部分。

## 四、确认综合后面积是否在约束范围内
* 阅读DC综合报告report/ysyx_xxxxxx/dc_report的 **AREA REPORT** 部分。

## 五、确认频率
支撑团队提供**100M频率**约束基准的DC综合流程。
* 阅读DC综合报告report/ysyx_xxxxxx/dc_report的 **SYNTHESIS REPORT** 部分，查看DC综合流程在100M频率下是否 **pass** ，如果未通过，我们会进行降频直至流程跑通为止。

**PS**：由于存在DC license的问题，支撑团队无法提供DC工具的使用，工程师人力及资源不足，无法提供一对一优化，因此，支撑团队只保证芯片的正确性，不辅助优化设计，有意愿追求高性能的同学可以自行优化，例如：参考开源EDA工具yosys。如果核的设计足够好，回片后是可以进行调频的。

100M频率未通过或想要做优化的同学，可以关注报告中以下部分的关键时序路径。
* 阅读DC综合报告report/ysyx_xxxxxx/dc_report的TIMING REPORT部分，报告中列出10条关键路径，关于时序报告的格式可自行参考相关资料，例如：Vivado的时序报告。
