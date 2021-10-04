# ysyx_submit
This is a repository for recording ysyx submissions.
ysyx_submit中仓库存在submit和report两个目录，submit目录用于存放前端设计同学提交的处理器核代码，report目录存放Soc和后端团队对前端代码进行功能仿真和综合后返回的报告。
* submit 目录结构
* report 目录结构
```
├─ ysyx_XXXXXX(学号)                               #每位同学的报告存放在自己学号的顶层目录下
  
    ├─ 2021-10-xx...xx:xx:xx(pull date)            #根据不同的代码拉取时间，支撑团队返回的报告存放在不同的目录下
    
      ├─ dc_report                                 #DC综合报告
      
      ├─ vcs_report                                #VCS仿真报告
```

## submit 


## report

SoC和后端团队的report返回后，前端的同学需要按照以下步骤确认报告内容及对代码做出相应的修改。

### 一、确认功能正确性
* 阅读VCS报告report/ysyx_xxxxxx/<pull time>/vcs_report，确认compile有无错误，确认VCS流程是否存在 **fail** ，如：如果VCS程序未通过，则首先需要修改代码以确保功能正确，确认控制信号寄存器是否已做初始化。

### 二、消除DC综合报告Warning/Error
* 阅读DC综合报告report/ysyx_xxxxxx/<pull time>/dc_report的 **SYNTHESIS REPORT** 部分，关注报告中的Warning和Error。清除所有的Warning和Error，根据Warning的提示相应地去修改代码，对于无法清除的Warning，需要填写 **Warning无法清理说明.xlsx** ，并反馈给支撑团队。

### 三、清除不带复位端的FF cell
* 阅读DC综合报告report/ysyx_xxxxxx/<pull time>/dc_report的 **SYNTHESIS REPORT** 部分，查看是否存在不带复位端的FF cell。报告中会列出各个module中不带复位端的FF cell的数量，如果存在不带复位端的FF cell，说明代码中存在未复位的控制信号，会导致VCS仿真无法通过，需修改代码以清除不带复位端的FF cell，确保每个module中不带复位端的FF cell的数目为 **0** 。

### 四、确认综合后面积是否在约束范围内
前端设计的同学需要确保设计综合后的 **Total cell area** 在约束范围内， **不带cache** 的核面积需小于 **0.9** 平方厘米， **带cache** 的核面积需小于 **1.4** 平方厘米。
* 阅读DC综合报告report/ysyx_xxxxxx/<pull time>/dc_report的 **AREA REPORT** 部分，确认Total cell area是否满足约束范围内。
  * 如做了五级流水线的设计Total cell area超过了约束范围，请对设计进行优化，将面积优化到约束范围内；
  * 如果做了乱序多发射的设计Total cell area超过了约束范围，请分析报告，找出面积较大的模块，说明面积过大的原因，编写说明文档，反馈给支撑团队进一步评估，如果支撑团队评估后觉得不合适，则需要请设计人员进一步简化设计。

### 五、确认频率
支撑团队提供 **100M频率** 约束基准的DC综合流程。
* 阅读DC综合报告report/ysyx_xxxxxx/<pull time>/dc_report的 **SYNTHESIS REPORT** 部分，查看DC综合流程在100M频率下是否 **pass** ，如果未通过，我们会进行降频直至流程跑通为止。

**PS**：由于存在DC license的问题，支撑团队无法提供DC工具的使用，工程师人力及资源不足，无法提供一对一优化，因此，支撑团队只保证芯片的正确性，不辅助优化设计，有意愿追求高性能的同学可以自行优化，例如：参考开源EDA工具yosys。如果核的设计足够好，回片后是可以进行调频的。

100M频率未通过或想要做优化的同学，可以关注报告中以下部分的关键时序路径。
* 阅读DC综合报告report/ysyx_xxxxxx/<pull time>/dc_report的TIMING REPORT部分，报告中列出10条最长路径供参考，关于时序报告的格式可自行参考相关资料，例如：Vivado的时序报告。

# 代码提交截止日期
2021年10月7日之后  不允许修改ram的规格。
2021年11月7日之后  不允许修改代码。
