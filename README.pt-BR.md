# Checklist de segurança prática para AI Agents

Um guia de referência rápida para quem desenvolve AI Agents: **39 itens acionáveis**, todos alinhados com as categorias reais do [OWASP Top 10 for LLM Applications (2025)](https://genai.owasp.org/llm-top-10/) (injeção de prompt, vazamento de dados sensíveis, agência excessiva, riscos de cadeia de suprimentos etc.). Cada item é uma ação concreta de "fazer / não fazer", sem enrolação.

## 🛠️ Ferramenta prática complementar

- **[Web-Vuln-Scanner](https://github.com/Ezra-Zhao/Web-Vuln-Scanner)** — Meu projeto principal de segurança: um scanner de vulnerabilidades web. Este checklist mostra *o que revisar* antes de lançar; o Web-Vuln-Scanner ajuda a *encontrar* as vulnerabilidades de verdade. Use os dois juntos.

## 🌍 Versões em três idiomas

| Idioma | Descrição | Checklist |
|---|---|---|
| 中文 | [README.md](README.md) | [checklist-zh.md](checklist-zh.md) |
| Español | [README.es.md](README.es.md) | [checklist-es.md](checklist-es.md) |
| Português (BR) | README.pt-BR.md (esta página) | [checklist-pt-BR.md](checklist-pt-BR.md) |

## 📋 Cinco grupos (39 itens no total)

1. **Proteção contra injeção de prompt** (9) — OWASP LLM01 Prompt Injection / LLM05 Improper Output Handling / LLM07 System Prompt Leakage
2. **Permissão mínima para ferramentas** (8) — OWASP LLM06 Excessive Agency / LLM10 Unbounded Consumption
3. **Tratamento de dados sensíveis** (7) — OWASP LLM02 Sensitive Information Disclosure
4. **Auditoria e monitoramento** (7) — logs de ponta a ponta, alertas de anomalias, resposta a incidentes
5. **Cadeia de suprimentos e deploy** (8) — OWASP LLM03 Supply Chain / LLM04 Data and Model Poisoning

## ✅ Como usar

- Integre o checklist à sua **lista de verificação de lançamento ou ao CI**: só faz deploy depois de marcar os 39 itens.
- Passe item por item com cada pessoa nova do time: funciona melhor do que um manual longo de segurança.
- Faltou um item que você usa na prática? Abra uma Issue ou um PR.

## 📄 Licença

MIT © 2026 Guangyi Zhao — ver [LICENSE](LICENSE).
