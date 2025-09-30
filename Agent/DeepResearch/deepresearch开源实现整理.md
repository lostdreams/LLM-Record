

# Jina  AI

- [https://zhuanlan.zhihu.com/p/26560000573]



- 项目地址： https://github.com/jina-ai/node-DeepResearch



# LangGraph



# 代码

[link](https://github.com/langchain-ai/open_deep_research)

# 设计
- 分层结构 (Hierarchical Structure): 系统被设计成一个“研究主管” (Supervisor) 和多个“研究员” (Researcher) 的协作模式。主管负责拆解任务和整合结果，研究员负责执行具体的搜索和信息提取。
- 状态机 (State Machine): 整个流程由 LangGraph 构建的图（Graph）来控制。图中的每个节点（Node）代表一个工作步骤，边（Edge）代表流程的转换方向。数据以“状态”（State）的形式在节点间传递和更新，确保了流程的清晰和可追溯。

- 健壮性 (Robustness): 代码中包含了大量的错误处理机制，特别是针对大型语言模型（LLM）调用时常见的“Token超限”问题，设计了重试和内容压缩等策略。



# 实现步骤

三层结构： 1. 设定要研究的若干步骤 2. 对每个步骤，进行研究，即研究一个子领域 3. 每个子领域 由若干研究员子图，构成，研究员才拥有search webs的操作 ，并进行汇总向上汇报，，

## 主图

- 1. START -> clarify_with_user (与用户澄清意图)
目的: 确保AI完全理解用户的研究请求。
流程:
调用LLM，判断当前的用户信息是否足够清晰，是否需要追问。
如果需要澄清: 向用户返回一个问题，流程结束（等待用户再次输入）。
如果不需要澄清: 向用户发送一句确认信息（例如：“好的，我将开始研究关于...的话题”），然后进入下一步。
- 2. clarify_with_user -> write_research_brief (撰写研究大纲)
目的: 将用户的自然语言请求，转化为一份结构化的、正式的研究大纲（Research Brief）。
流程:
调用LLM，使用一个专门的提示（Prompt）来生成包含研究主题、关键问题和目标的结构化大纲。
将生成的大纲存入状态，并初始化“研究主管”的系统消息，正式启动研究阶段。
- 3. write_research_brief -> research_supervisor (研究主管阶段)
目的: 这是研究的核心执行阶段，由一个独立的子图 supervisor_subgraph 负责。
流程: 主管接收到研究大纲后，会开始一个循环，不断地拆分任务、分配任务、汇总结果，直到整个研究完成。
(详见下方 supervisor_subgraph 子图拆解)
- 4. research_supervisor -> final_report_generation (生成最终报告)
目的: 将所有研究员提交的研究笔记（findings）整合成一份连贯、完整的最终报告。
流程:
收集research_supervisor阶段产出的所有笔记。
调用LLM，使用一个专门用于报告生成的提示，将零散的笔记内容编织成最终报告。
错误处理: 如果笔记内容过长导致Token超限，它会尝试逐步缩减内容的长度并重试，直到成功或达到最大重试次数。
- 5. final_report_generation -> END (结束)
流程结束，最终报告已生成。




## 两个子图任务 ：
 supervisor_subgraph (研究主管) 和 researcher_subgraph (研究员)

- supervisor_subgraph (研究主管)目的: 根据当前的研究大纲和已有的研究笔记，决定下一步要研究什么。

- researcher_subgraph (研究员)：目的: 针对一个具体的研究主题（如“2024年AI芯片市场的主要参与者”），决定使用什么工具来查找信息。LLM + functioncall ,然后做精炼总结
- 
