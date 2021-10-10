# ysyx_submit
This is a repository for recording ysyx submissions.
ysyx_submit中仓库存在submit和report两个目录，submit目录用于存放前端设计同学提交的处理器核代码，report目录存放Soc和后端团队对前端代码进行功能仿真和综合后返回的报告。
* submit 目录结构
```
├─ ysyx_XXXXXX(学号)                               #每位同学上传的代码通过子模块的形式链接到该目录
  
    ├─ .git                                        #存放commit信息的目录，可通过git log查看开发过程
  
    ├─ submit                                      #存放提交相关文件的目录

    ├─ ......                                      #其他文件为原oscpu-framework中的文件
```
* report 目录结构
```
├─ ysyx_XXXXXX(学号)                               #每位同学的报告存放在自己学号的顶层目录下
  
    ├─ 2021-10-xx...xx:xx:xx(pull date)            #根据不同的代码拉取时间，支撑团队返回的报告存放在不同的目录下
    
      ├─ dc_report                                 #DC综合报告
      
      ├─ vcs_report                                #VCS仿真报告
      
      ├─ commit date                               #本次报告对应的RTL代码提交时间
```


## report

SoC和后端团队的report返回后，前端的同学需要按照以下步骤确认报告内容及对代码做出相应的修改。

### 一、确认功能正确性
* 阅读VCS报告report/ysyx_xxxxxx/<pull time>/vcs_report，确认compile有无错误，确认VCS流程是否存在 **fail** ，如：如果VCS程序未通过，则首先需要修改代码以确保功能正确，确认控制信号寄存器是否已做初始化。

### 二、消除DC综合报告Warning/Error
* 阅读DC综合报告report/ysyx_xxxxxx/<pull time>/dc_report的 **SYNTHESIS REPORT** 部分，关注报告中的Warning和Error。清除所有的Warning和Error，根据Warning的提示相应地去修改代码，对于无法清除的Warning，需要填写ysyx_submit目录下的“ **DC_Warning无法清理说明.xlsx** ”，发给各自的组长，由组长反馈给支撑团队。

### 三、确认综合后面积是否在约束范围内
前端设计的同学需要确保设计综合后的 **Total cell area** 在约束范围内， **不带cache** 的核面积需小于 **0.5** 平方毫米， **带cache** 的核面积需小于 **2.0** 平方毫米。
* 阅读DC综合报告report/ysyx_xxxxxx/<pull time>/dc_report的 **AREA REPORT** 部分，确认Total cell area是否满足约束范围内。
  * 如做了五级流水线的设计Total cell area超过了约束范围，请对设计进行优化，将面积优化到约束范围内；
  * 如果做了乱序多发射的设计Total cell area超过了约束范围，请分析报告，找出面积较大的模块，说明面积过大的原因，编写说明文档“  **ysyx_XXXXXX面积过大原因说明.doc** ”，没有格式要求，按要求说明原因即可，编写完成后发给各自的组长，再由组长反馈给支撑团队进一步评估，如果支撑团队评估后觉得不合适，则需要请设计人员进一步简化设计。

### 四、确认频率
支撑团队提供 **100M频率** 约束基准的DC综合流程。这里采用100M频率综合时，为了给后端设计修时序留余量，设了0.35的过约比，实际的频率会比100M高，时序约束条件更为严格。
  例如：
  ![1633343064(1)](https://user-images.githubusercontent.com/82496491/135835292-fad710f7-aa2f-46a8-aacb-c981f21f43ac.png)

  在100M频率下，图中标记的data required time应该接近10ns，可以看到实际的data required time只有6.2189，约束更为严格。

* 阅读DC综合报告report/ysyx_xxxxxx/<pull time>/dc_report的 **SYNTHESIS REPORT** 部分，查看DC综合流程在100M频率下是否 **pass** ，如果未通过，我们会进行降频直至流程跑通为止。

**PS**：由于存在DC license的问题，支撑团队无法提供DC工具的使用，工程师人力及资源不足，无法提供一对一优化，因此，支撑团队只保证芯片的正确性，不辅助优化设计，有意愿追求高性能的同学可以自行优化，例如：参考开源EDA工具yosys。如果核的设计足够好，回片后是可以进行调频的。

100M频率未通过或想要做优化的同学，可以关注报告中以下部分的关键时序路径。
* 阅读DC综合报告report/ysyx_xxxxxx/<pull time>/dc_report的TIMING REPORT部分，报告中列出3条最长路径供参考，关于时序报告的格式可自行参考相关资料，例如：Vivado的时序报告。

# 代码拉取时间
支撑团队提供的CICD流程，第一次代码拉取时间为 **10月5日中午12:00** ，之后 **每天中午12:00** 都会拉取一次。每次拉取代码后，报告返回时间不是确定时间。当次拉取的所有代码在跑完DC&VCS流程后，会将当次拉取的所有代码的报告会按照学号划分返回到github仓库ysyx_submit/report目录下。
  
# 代码提交截止日期
2021年10月7日之后  不允许修改ram的规格。
2021年11月7日之后  不允许修改代码。
