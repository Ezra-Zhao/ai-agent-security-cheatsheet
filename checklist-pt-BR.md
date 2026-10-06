# Checklist de segurança prática para AI Agents (Português)

> Alinhado com as categorias reais do OWASP Top 10 for LLM Applications (2025). Cada item é uma ação concreta: marque todos antes de lançar.
> Ferramenta complementar: [Web-Vuln-Scanner](https://github.com/Ezra-Zhao/Web-Vuln-Scanner) (scanner de vulnerabilidades web: encontra as falhas de verdade)

## 1. Proteção contra injeção de prompt (OWASP LLM01 / LLM05 / LLM07)

- [ ] Coloque o system prompt em um nível que o usuário não possa sobrescrever (papel de sistema separado ou hierarquia explícita de instruções).
- [ ] Envolva entradas não confiáveis com delimitadores (``` ou tags `<user_input>`) e deixe claro que são dados, não instruções a executar.
- [ ] Regra inquebrável: nenhuma instrução do usuário pode anular as do sistema; truques do tipo "ignore tudo acima" não funcionam.
- [ ] Valide a saída do modelo antes de executá-la (esquema JSON ou lista permitida); se não seguir o formato, rejeite sem adivinhar.
- [ ] Antes de chamar uma ferramenta, verifique se os parâmetros estão dentro do esperado (limites numéricos, valores permitidos, caminhos permitidos).
- [ ] Marque o conteúdo de páginas, documentos e e-mails externos como fonte não confiável: ele não pode disparar chamadas de ferramentas sozinho.
- [ ] Trate o conteúdo recuperado via RAG como entrada não confiável e sempre cite a fonte.
- [ ] Faça testes de regressão periódicos com casos de injeção de prompt (direta, indireta e progressiva em várias etapas).
- [ ] Registre e alerte tentativas de injeção; não as descarte em silêncio.

## 2. Permissão mínima para ferramentas (OWASP LLM06 / LLM10)

- [ ] Dê a cada agente apenas as ferramentas necessárias para sua tarefa (princípio do menor privilégio).
- [ ] Tudo negado por padrão, lista de permissões para liberar: o que não estiver explicitamente autorizado não pode ser chamado.
- [ ] Operações perigosas (apagar bancos de dados, enviar e-mails, pagamentos, mudar a configuração de produção) exigem confirmação humana.
- [ ] Dupla confirmação ou fluxo de aprovação para operações de alto risco; em produção crítica, revisão por várias pessoas.
- [ ] Execute as ferramentas em sandbox ou ambiente isolado, com rede e sistema de arquivos restritos.
- [ ] Defina limites de timeout e de tentativas para evitar loops infinitos que queimem sua cota de tokens (OWASP LLM10: consumo sem limites).
- [ ] Limite o número de chamadas de ferramentas e o orçamento de tokens por tarefa; se estourar, pare tudo e alerte.
- [ ] Limpe as mensagens de erro das ferramentas antes de passá-las ao modelo: nada de caminhos internos, detalhes de pilha nem fragmentos de segredos.

## 3. Tratamento de dados sensíveis (OWASP LLM02)

- [ ] Nunca coloque API keys, senhas ou tokens em prompts, comentários de código, exemplos ou documentação.
- [ ] Injete segredos via variáveis de ambiente ou gerenciador de segredos; no código eles só são referenciados, nunca escritos.
- [ ] Anonimize ou converta em tokens os dados pessoais (nome, telefone, documento de identidade, endereço) antes de enviar ao modelo.
- [ ] Mascare segredos e dados pessoais em logs, traces e stack traces.
- [ ] Defina um prazo claro de retenção para os dados de usuário, apague ao vencer e informe a política ao usuário.
- [ ] Filtre informações sensíveis antes de salvar na memória entre sessões; o usuário deve poder ver, exportar e apagar sua memória.
- [ ] Remova amostras sensíveis dos dados de treino e ajuste; revise também os conjuntos de avaliação.

## 4. Auditoria e monitoramento

- [ ] Registre o fluxo completo: prompt de entrada, parâmetros das ferramentas, saída do modelo e confirmações humanas, tudo com timestamp e ID da requisição.
- [ ] Guarde os logs de auditoria em armazenamento independente e imutável (somente acréscimo), fisicamente separado dos logs de negócio.
- [ ] Alerte comportamentos anômalos: muitas chamadas de ferramentas em pouco tempo, tentativas de escalação de privilégios, palavras-chave de injeção, picos de consumo de tokens.
- [ ] Revise os logs de auditoria toda semana, com foco no que foi rejeitado e interceptado por humanos.
- [ ] Tenha um plano de resposta a incidentes: conter → investigar → corrigir → aprender, com responsáveis claros em cada etapa.
- [ ] Dê a cada agente ou serviço identidade e permissões próprias: assim dá para localizar o problema e revogar o acesso rápido.
- [ ] Monitore se a saída do modelo vaza informação sensível (trechos do system prompt, formatos típicos de chaves); bloqueie ao detectar.

## 5. Cadeia de suprimentos e deploy (OWASP LLM03 / LLM04)

- [ ] Revise dependências de terceiros (bibliotecas, modelos, skills, plugins) antes de usar: estado de manutenção, CVEs conhecidos, reputação do autor.
- [ ] Fixe todas as versões das dependências (lockfile) e valide cada atualização primeiro em ambiente de testes.
- [ ] Instale skills e plugins só de fontes confiáveis, verificando assinatura ou hash; o de origem desconhecida não é ativado.
- [ ] Versione o modelo e o system prompt como código; mudanças passam por revisão.
- [ ] Rotacione os segredos periodicamente (a cada 90 dias ou menos); se suspeitar de vazamento, rotacione na hora.
- [ ] Separe rigorosamente os segredos de produção e de testes; em testes use só dados falsos.
- [ ] Antes do deploy, rode uma linha de base de segurança: pelo menos um caso de teste de injeção, um de escalação e um de vazamento.
- [ ] Use imagens mínimas de contêiner ou máquina virtual, aplique os patches de segurança em dia e não rode como root.

---

*39 itens no total. Use como lista de verificação de lançamento: sem os 39 marcados, não há deploy.*
