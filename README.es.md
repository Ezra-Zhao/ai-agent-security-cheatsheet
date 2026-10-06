# Checklist de seguridad práctica para AI Agents

Una hoja de referencia rápida para quienes desarrollan AI Agents: **39 puntos accionables**, todos alineados con las categorías reales del [OWASP Top 10 for LLM Applications (2025)](https://genai.owasp.org/llm-top-10/) (inyección de prompts, filtración de datos sensibles, agencia excesiva, riesgos de cadena de suministro, etc.). Cada punto es una acción concreta de "hacer / no hacer", sin relleno.

## 🛠️ Herramienta práctica complementaria

- **[Web-Vuln-Scanner](https://github.com/Ezra-Zhao/Web-Vuln-Scanner)** — Mi proyecto insignia de seguridad: un escáner de vulnerabilidades web. Este checklist te dice *qué revisar* antes de lanzar; Web-Vuln-Scanner te ayuda a *encontrar* las vulnerabilidades de verdad. Úsalos juntos.

## 🌍 Versiones en tres idiomas

| Idioma | Descripción | Checklist |
|---|---|---|
| 中文 | [README.md](README.md) | [checklist-zh.md](checklist-zh.md) |
| Español | README.es.md (esta página) | [checklist-es.md](checklist-es.md) |
| Português (BR) | [README.pt-BR.md](README.pt-BR.md) | [checklist-pt-BR.md](checklist-pt-BR.md) |

## 📋 Cinco grupos (39 puntos en total)

1. **Protección contra la inyección de prompts** (9) — OWASP LLM01 Prompt Injection / LLM05 Improper Output Handling / LLM07 System Prompt Leakage
2. **Permisos mínimos para herramientas** (8) — OWASP LLM06 Excessive Agency / LLM10 Unbounded Consumption
3. **Manejo de datos sensibles** (7) — OWASP LLM02 Sensitive Information Disclosure
4. **Auditoría y monitoreo** (7) — registros de punta a punta, alertas de anomalías, respuesta a incidentes
5. **Cadena de suministro y despliegue** (8) — OWASP LLM03 Supply Chain / LLM04 Data and Model Poisoning

## ✅ Cómo usarlo

- Integra el checklist en tu **lista de verificación de lanzamiento o en tu CI**: no se despliega hasta marcar los 39 puntos.
- Repásalo punto por punto con cada persona nueva del equipo: funciona mejor que un manual largo de seguridad.
- ¿Falta un punto que usas en la práctica? Abre un Issue o un PR.

## 📄 Licencia

MIT © 2026 Guangyi Zhao — ver [LICENSE](LICENSE).
