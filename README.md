# AI Agent 安全实操 Checklist

给 AI Agent 开发者的安全速查表：**39 条可直接执行的检查项**，全部对标 [OWASP Top 10 for LLM Applications（2025 版）](https://genai.owasp.org/llm-top-10/) 的真实条目（Prompt 注入、敏感信息泄露、过度代理、供应链风险等）。每条都是"做 / 不做"的动作，没有空话。

## 🛠️ 配套实战工具

- **[Web-Vuln-Scanner](https://github.com/Ezra-Zhao/Web-Vuln-Scanner)** —— 我的旗舰安全项目：Web 漏洞扫描器。这份 checklist 告诉你"上线前该检查什么"，Web-Vuln-Scanner 帮你实际动手把漏洞扫出来，两者配套使用。

## 🌍 三语版本

| 语言 | 说明文档 | Checklist 正文 |
|---|---|---|
| 中文 | README.md（本页） | [checklist-zh.md](checklist-zh.md) |
| Español | [README.es.md](README.es.md) | [checklist-es.md](checklist-es.md) |
| Português (BR) | [README.pt-BR.md](README.pt-BR.md) | [checklist-pt-BR.md](checklist-pt-BR.md) |

## 📋 五大分组（共 39 条）

1. **Prompt 注入防护**（9 条）—— 对应 OWASP LLM01 Prompt Injection / LLM05 Improper Output Handling / LLM07 System Prompt Leakage
2. **工具权限最小化**（8 条）—— 对应 OWASP LLM06 Excessive Agency / LLM10 Unbounded Consumption
3. **敏感数据处理**（7 条）—— 对应 OWASP LLM02 Sensitive Information Disclosure
4. **审计与监控**（7 条）—— 全链路日志、异常告警、事件响应
5. **供应链与部署**（8 条）—— 对应 OWASP LLM03 Supply Chain / LLM04 Data and Model Poisoning

## ✅ 使用建议

- 把 checklist 接入你的**发布检查单或 CI 流水线**：39 条全打勾才能上线。
- 新人 onboarding 时逐条过一遍，比看长篇安全规范见效快。
- 发现遗漏的实战条目，欢迎提 Issue / PR 补充。

## 📄 License

MIT © 2026 Guangyi Zhao —— 详见 [LICENSE](LICENSE)。
