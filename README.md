# Openai-practise
this ia project for tracing new openai SDK usage



## function calling

```mermaid

flowchart TD
    A[1. 应用调用API\n携带提示和函数定义] --> B[2. 模型决策]
    B -->|直接响应| C[返回用户答案]
    B -->|需调用函数| D[3. API返回\n函数名和参数]
    D --> E[4. 应用执行函数]
    E --> F[5. 应用提交\n函数结果至API]
    F --> G[生成最终响应]
    G --> C

    style A fill:#E1F5FE,stroke:#039BE5
    style B fill:#E8F5E9,stroke:#43A047
    style C fill:#F1F8E9,stroke:#7CB342
    style D fill:#FFF3E0,stroke:#FB8C00
    style E fill:#F3E5F5,stroke:#8E24AA
    style F fill:#E0F7FA,stroke:#00ACC1
    style G fill:#E8EAF6,stroke:#5C6BC0

```



| 步骤 | 执行方 | 关键动作              | 数据格式示例                                                 |
| :--- | :----- | :-------------------- | :----------------------------------------------------------- |
| 1    | 应用   | 发送用户输入+函数定义 | `{"messages":[...], "functions":[...]}`                      |
| 2    | 大模型 | 决策响应方式          | 生成`tool_calls`或直接回答                                   |
| 3    | 大模型 | 返回函数调用          | `{"tool_calls": [{"name": "func", "arguments": {...}}]}`     |
| 4    | 应用   | 执行本地函数          | 解析参数并调用`func(**args)`                                 |
| 5    | 应用   | 提交执行结果          | `{"tool_call_id": "...", "role": "tool", "content": "result"}` |
