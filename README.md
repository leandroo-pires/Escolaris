# Projeto - Escolaris

> Portal escolar web para alunos, professores e gestão.
> Projeto pessoal de treino full-stack: Java + Spring Boot (back-end), Angular/TypeScript (front-end) e Figma (design).

## Sumário

1. [Visão geral](#1-visão-geral)
2. [Módulos](#2-módulos)
3. [Requisitos funcionais](#3-requisitos-funcionais-rf)
4. [Requisitos não funcionais](#4-requisitos-não-funcionais-rnf)
5. [Regras de negócio](#5-regras-de-negócio-rn)
6. [Histórias de usuário](#6-histórias-de-usuário)
7. [Modelo de domínio preliminar](#7-modelo-de-domínio-preliminar)
8. [Arquitetura e stack](#8-arquitetura-e-stack)
9. [Roadmap](#9-roadmap-sugerido)
10. [Premissas e pontos em aberto](#10-premissas-e-pontos-em-aberto)

---

## 1. Visão geral

**Objetivo:** portal web que centraliza a vida acadêmica de uma escola de ensino fundamental e médio: notas, frequência, conteúdo, comunicados e gestão administrativa.

**Perfis de usuário**

| Perfil | Descrição |
|---|---|
| Aluno | Consulta notas, faltas, horários, materiais, comunicados; entrega atividades |
| Professor | Lança notas e frequência, publica material e atividades, comunica turmas |
| Gestão | Coordenação e secretaria: cadastros, turmas, calendário, relatórios |
| Administrador | Gerencia usuários e permissões do sistema (perfil técnico) |

*Opcional (fase 2):* Responsável, com acesso de leitura aos dados do aluno vinculado.

**Fora do escopo (v1):** pagamentos/mensalidades, EAD com videoconferência, app mobile nativo, integração com sistemas do MEC.

## 2. Módulos

1. Autenticação e perfis
2. Cadastros (alunos, professores, disciplinas, turmas, anos letivos)
3. Matrícula e enturmação
4. Grade horária
5. Diário de classe (frequência e notas)
6. Atividades e materiais
7. Comunicados e mural
8. Calendário escolar
9. Boletim e relatórios
10. Painel (dashboard) por perfil

## 3. Requisitos funcionais (RF)

### Autenticação e acesso
- **RF01** Login com e-mail/matrícula e senha.
- **RF02** Logout e expiração de sessão.
- **RF03** Recuperação de senha por e-mail.
- **RF04** Troca de senha obrigatória no primeiro acesso.
- **RF05** Controle de acesso por perfil (RBAC).

### Cadastros
- **RF06** CRUD de alunos (dados pessoais, contato, responsável).
- **RF07** CRUD de professores (dados pessoais, formação, disciplinas habilitadas).
- **RF08** CRUD de disciplinas.
- **RF09** CRUD de turmas (série, turno, ano letivo, sala).
- **RF10** CRUD de anos letivos e períodos (bimestres/trimestres).
- **RF11** Inativar (não excluir) registros com histórico.
- **RF12** Busca e filtros em todas as listagens, com paginação.

### Matrícula e turmas
- **RF13** Matricular aluno em uma turma de um ano letivo.
- **RF14** Transferir aluno entre turmas, mantendo histórico.
- **RF15** Vincular professor a disciplina e turma.
- **RF16** Encerrar matrícula (transferência, evasão, conclusão).

### Grade horária
- **RF17** Montar grade semanal por turma (disciplina, professor, horário, sala).
- **RF18** Detectar conflito de horário de professor e de sala.
- **RF19** Aluno e professor visualizam sua grade.

### Diário de classe
- **RF20** Professor registra frequência por aula e turma.
- **RF21** Professor cria avaliações por disciplina/período (prova, trabalho, etc.) com peso.
- **RF22** Professor lança notas por avaliação.
- **RF23** Cálculo automático de média por período e final.
- **RF24** Fechamento de período (trava lançamentos).
- **RF25** Gestão pode reabrir período com justificativa registrada.

### Atividades e materiais
- **RF26** Professor publica material (arquivo/link) por turma e disciplina.
- **RF27** Professor cria atividade com prazo e descrição.
- **RF28** Aluno envia resposta/arquivo da atividade.
- **RF29** Professor corrige e atribui nota/feedback.

### Comunicação
- **RF30** Gestão e professor publicam comunicados (para escola, série, turma ou aluno).
- **RF31** Usuário vê comunicados e marca como lido.
- **RF32** Notificação de novos comunicados no portal.

### Calendário
- **RF33** Gestão cadastra eventos, feriados, recessos e datas de provas.
- **RF34** Todos visualizam o calendário filtrado pelo seu contexto.

### Boletim e relatórios
- **RF35** Aluno visualiza boletim (notas, médias, frequência, situação).
- **RF36** Geração de boletim em PDF.
- **RF37** Relatório de frequência por turma/aluno.
- **RF38** Relatório de desempenho por turma/disciplina.
- **RF39** Relatório de alunos em risco (infrequência ou nota baixa).
- **RF40** Exportação de relatórios em CSV/PDF.

### Dashboard
- **RF41** Aluno: próximas atividades, faltas, últimas notas, comunicados.
- **RF42** Professor: turmas do dia, pendências de lançamento e correção.
- **RF43** Gestão: totais de matrículas, frequência média, alertas.

### Auditoria
- **RF44** Registrar log de alterações sensíveis (notas, frequência, matrícula) com usuário e data.

## 4. Requisitos não funcionais (RNF)

| ID | Categoria | Requisito |
|---|---|---|
| RNF01 | Segurança | Senhas com hash (BCrypt); autenticação JWT; HTTPS |
| RNF02 | Segurança | Autorização verificada no back-end em toda rota, nunca só no front |
| RNF03 | Privacidade | Aderência à LGPD: dados mínimos, consentimento, proteção de dados de menores |
| RNF04 | Desempenho | Listagens paginadas; resposta de API < 500 ms em operações comuns |
| RNF05 | Usabilidade | Interface responsiva (desktop, tablet, celular) |
| RNF06 | Acessibilidade | Seguir WCAG 2.1 AA: contraste, navegação por teclado, labels |
| RNF07 | Manutenibilidade | Arquitetura em camadas; cobertura de testes mínima de 70% no back |
| RNF08 | Compatibilidade | Últimas versões de Chrome, Firefox, Edge e Safari |
| RNF09 | Documentação | API documentada com OpenAPI/Swagger |
| RNF10 | Confiabilidade | Backup do banco; migrations versionadas (Flyway) |
| RNF11 | Observabilidade | Logs estruturados e tratamento padronizado de erros |
| RNF12 | Implantação | Execução via Docker Compose (app, banco, front) |

## 5. Regras de negócio (RN)

### Acesso
- **RN01** Todo usuário tem exatamente um perfil principal. Professor que também é gestor recebe múltiplos papéis.
- **RN02** Aluno só acessa os próprios dados; professor só acessa turmas/disciplinas a que está vinculado.
- **RN03** Senha: mínimo de 8 caracteres, com letras e números. Bloqueio temporário após 5 tentativas falhas.
- **RN04** Usuário inativo não consegue logar.

### Matrícula
- **RN05** Um aluno só pode ter uma matrícula ativa por ano letivo.
- **RN06** A matrícula exige turma com vaga disponível (capacidade da turma).
- **RN07** O número de matrícula é gerado automaticamente e é único: `AAAA` + sequencial.
- **RN08** Aluno menor de idade exige um responsável cadastrado.
- **RN09** Aluno com matrícula encerrada mantém histórico acadêmico consultável.
- **RN10** CPF é único no sistema e validado.

### Turmas e grade
- **RN11** Um professor não pode estar em duas turmas no mesmo horário.
- **RN12** Uma sala não pode ser alocada a duas turmas no mesmo horário.
- **RN13** Professor só pode ser vinculado a disciplinas para as quais está habilitado.
- **RN14** A turma pertence a um único ano letivo e não muda de série.

### Frequência
- **RN15** Frequência é registrada por aula: presente, falta ou falta justificada.
- **RN16** Percentual de frequência = aulas presentes (incluindo justificadas) ÷ aulas dadas × 100.
- **RN17** Aprovação exige frequência mínima de 75% do total de aulas do ano.
- **RN18** Registro de frequência só pode ser feito pelo professor da disciplina/turma e apenas em datas com aula na grade.
- **RN19** Edição de frequência após 7 dias exige autorização da gestão.

### Notas e aprovação
- **RN20** Notas variam de 0,0 a 10,0, com uma casa decimal.
- **RN21** Média do período = média ponderada das avaliações pelos pesos (soma dos pesos = 100%).
- **RN22** Média final = média aritmética das médias dos períodos.
- **RN23** Média mínima de aprovação: 6,0.
- **RN24** Aluno com média final entre 4,0 e 5,9 vai para recuperação final.
- **RN25** Após recuperação, média final = (média anterior + nota de recuperação) ÷ 2, mínimo 6,0 para aprovar.
- **RN26** Aluno com média final abaixo de 4,0 ou frequência abaixo de 75% é reprovado.
- **RN27** Situação final possível: Aprovado, Reprovado por nota, Reprovado por frequência, Em recuperação.
- **RN28** Notas só podem ser lançadas em período aberto; após fechamento, só com reabertura da gestão.
- **RN29** Toda alteração de nota após o fechamento gera registro de auditoria com justificativa.

### Atividades
- **RN30** Atividade tem prazo; envio após o prazo é marcado como atrasado (professor decide se aceita).
- **RN31** Aluno só vê atividades das turmas em que está matriculado.
- **RN32** Aluno pode reenviar até o prazo; vale o último envio.
- **RN33** Limite de tamanho e tipos de arquivo permitidos (ex.: 10 MB; pdf, docx, png, jpg, zip).

### Comunicados
- **RN34** Professor só publica para suas turmas; gestão publica para qualquer público.
- **RN35** Comunicado publicado não pode ser excluído, apenas arquivado (rastreabilidade).

### Dados e auditoria
- **RN36** Exclusão lógica para entidades com histórico (aluno, professor, turma, nota).
- **RN37** Dados pessoais de menores só são visíveis a gestão, professores vinculados e responsáveis.

## 6. Histórias de usuário

Formato: *Como [perfil], quero [ação], para [benefício].*
Prioridade: **A** (MVP), **M** (média), **B** (baixa).

### Transversais

**HU01 — Login (A)**
Como usuário, quero entrar com minhas credenciais, para acessar as funções do meu perfil.
- Credenciais inválidas exibem mensagem genérica.
- Após login, sou direcionado ao meu dashboard.
- Sessão expira por inatividade.

**HU02 — Recuperar senha (A)**
Como usuário, quero redefinir minha senha por e-mail, para recuperar o acesso.
- Link de redefinição expira em 1 hora e é de uso único.

**HU03 — Editar perfil (M)**
Como usuário, quero atualizar telefone, e-mail e foto, para manter meus dados corretos.

### Aluno

**HU04 — Ver boletim (A)**
Como aluno, quero ver notas, médias e situação por disciplina, para acompanhar meu desempenho.
- Mostra notas por período, média e situação (RN27).
- Só exibe notas de períodos com lançamento publicado.

**HU05 — Ver frequência (A)**
Como aluno, quero ver minhas faltas e percentual de frequência, para não correr risco de reprovação.
- Alerta visual quando frequência estiver abaixo de 80%.

**HU06 — Ver grade horária (A)**
Como aluno, quero ver meus horários da semana, para me organizar.

**HU07 — Acessar materiais (M)**
Como aluno, quero baixar materiais publicados pelos professores, para estudar.

**HU08 — Entregar atividade (M)**
Como aluno, quero enviar minha atividade pelo portal, para cumprir o prazo sem papel.
- Confirmação de envio com data e hora.
- Atividade atrasada é sinalizada.

**HU09 — Ler comunicados (A)**
Como aluno, quero ver comunicados da escola e da turma, para me manter informado.

**HU10 — Ver calendário (M)**
Como aluno, quero ver datas de provas e eventos, para planejar meus estudos.

### Professor

**HU11 — Ver minhas turmas (A)**
Como professor, quero listar minhas turmas e disciplinas, para acessar o diário de cada uma.

**HU12 — Registrar frequência (A)**
Como professor, quero marcar presença da turma em cada aula, para manter o diário atualizado.
- Lista todos os alunos ativos da turma, padrão "presente".
- Não permite data sem aula na grade (RN18).

**HU13 — Lançar notas (A)**
Como professor, quero lançar notas por avaliação, para que o boletim seja calculado.
- Valida faixa 0–10 (RN20).
- Bloqueia se período fechado (RN28).
- Média recalculada automaticamente.

**HU14 — Criar avaliações (A)**
Como professor, quero definir avaliações e pesos por período, para estruturar a nota.
- Soma dos pesos deve ser 100% (RN21).

**HU15 — Publicar material (M)**
Como professor, quero compartilhar arquivos e links com a turma, para apoiar as aulas.

**HU16 — Criar e corrigir atividades (M)**
Como professor, quero criar atividades com prazo e corrigir os envios, para avaliar o aprendizado.

**HU17 — Enviar comunicado à turma (M)**
Como professor, quero avisar minhas turmas, para comunicar mudanças e orientações.

**HU18 — Ver alunos em risco (B)**
Como professor, quero identificar alunos com notas baixas ou muitas faltas, para agir cedo.

### Gestão

**HU19 — Cadastrar alunos (A)**
Como gestor, quero cadastrar e editar alunos, para manter a base escolar.
- CPF único e válido (RN10); menor exige responsável (RN08).

**HU20 — Cadastrar professores (A)**
Como gestor, quero cadastrar professores e suas disciplinas, para alocá-los às turmas.

**HU21 — Gerenciar turmas e disciplinas (A)**
Como gestor, quero criar turmas e disciplinas por ano letivo, para organizar a oferta escolar.

**HU22 — Matricular e enturmar (A)**
Como gestor, quero matricular o aluno em uma turma, para formalizar seu ingresso.
- Respeita vagas (RN06) e matrícula única (RN05).

**HU23 — Transferir ou encerrar matrícula (M)**
Como gestor, quero movimentar ou encerrar matrículas, para refletir a situação real do aluno.

**HU24 — Montar grade horária (A)**
Como gestor, quero alocar disciplina, professor, sala e horário, para estruturar o ano.
- Conflitos de professor/sala são bloqueados (RN11, RN12).

**HU25 — Fechar e reabrir períodos (M)**
Como gestor, quero encerrar um período letivo, para consolidar notas e frequência.
- Reabertura exige justificativa registrada (RN29).

**HU26 — Publicar comunicados e eventos (A)**
Como gestor, quero comunicar toda a escola ou públicos específicos, para alinhar a comunidade escolar.

**HU27 — Emitir relatórios e boletins (M)**
Como gestor, quero gerar relatórios e boletins em PDF/CSV, para prestar contas e arquivar.

**HU28 — Dashboard gerencial (B)**
Como gestor, quero ver indicadores gerais, para tomar decisões.

**HU29 — Consultar auditoria (B)**
Como gestor, quero ver o histórico de alterações em notas e frequência, para garantir integridade.

### Administrador

**HU30 — Gerenciar usuários e perfis (A)**
Como administrador, quero criar usuários e atribuir papéis, para controlar quem acessa o quê.

## 7. Modelo de domínio preliminar

**Entidades principais**

- `Usuario` (id, email, senhaHash, ativo) — papéis: `Perfil` (ALUNO, PROFESSOR, GESTOR, ADMIN)
- `Aluno` (matrícula, nome, CPF, nascimento, contato) — `Responsavel`
- `Professor` (nome, CPF, formação) — habilitado em `Disciplina`
- `AnoLetivo` — `Periodo` (bimestre/trimestre, status aberto/fechado)
- `Serie`, `Turma` (ano letivo, turno, sala, capacidade)
- `Matricula` (aluno, turma, status, datas)
- `Disciplina`
- `Alocacao` (professor, disciplina, turma)
- `HorarioAula` (alocação, dia da semana, início, fim, sala)
- `Aula` (alocação, data) — `Frequencia` (aula, aluno, status)
- `Avaliacao` (alocação, período, peso, data) — `Nota` (avaliação, aluno, valor)
- `Material`, `Atividade`, `Entrega`
- `Comunicado` (autor, público-alvo), `LeituraComunicado`
- `EventoCalendario`
- `LogAuditoria` (usuário, entidade, ação, antes/depois, data)

**Relações-chave:** Aluno 1—N Matrícula N—1 Turma; Turma 1—N Alocação N—1 Professor/Disciplina; Alocação 1—N Aula/Avaliação.

## 8. Arquitetura e stack

**Back-end (Spring Boot)**
- Camadas: controller → service → repository; DTOs separados das entidades.
- Spring Security + JWT; Spring Data JPA; Bean Validation.
- Banco: PostgreSQL; migrations com Flyway.
- Documentação: springdoc-openapi.
- Testes: JUnit 5, Mockito, Testcontainers.

**Front-end (Angular)**
- Módulos/rotas por perfil (aluno, professor, gestão) com lazy loading.
- Guards e interceptors para autenticação e autorização.
- Formulários reativos; componentes reutilizáveis; serviços HTTP tipados.
- Biblioteca de UI sugerida: Angular Material (ou design próprio a partir do Figma).
- Testes: Jasmine/Karma ou Jest; Cypress/Playwright para E2E.

**Design (Figma)**
- Design system: cores, tipografia, espaçamentos, componentes.
- Protótipos de baixa e alta fidelidade por perfil.
- Fluxos principais: login, dashboard, boletim, diário, matrícula.

**Qualidade**
- Testes unitários, de integração e E2E; pipeline CI (GitHub Actions).
- Cobertura mínima (RNF07).

## 9. Roadmap sugerido

| Etapa | Entrega | Histórias |
|---|---|---|
| 0 | Setup: repositórios, Docker Compose, CI, design system base no Figma | — |
| 1 | Autenticação, perfis e usuários | HU01–03, HU30 |
| 2 | Cadastros base: alunos, professores, disciplinas, turmas, anos letivos | HU19–21 |
| 3 | Matrícula e grade horária | HU22, HU24, HU06 |
| 4 | Diário: frequência e notas | HU11–14, HU04, HU05 |
| 5 | Comunicados e calendário | HU09, HU10, HU17, HU26 |
| 6 | Materiais e atividades | HU07, HU08, HU15, HU16 |
| 7 | Fechamento de período, boletim PDF, relatórios, auditoria | HU23, HU25, HU27–29 |
| 8 | Dashboards, acessibilidade, polimento e deploy | HU18 + RNF |

**MVP:** etapas 0 a 4 (+ comunicados básicos da etapa 5).

## 10. Premissas e pontos em aberto

Valores padrão adotados (média 6,0, frequência mínima 75%, recuperação final) podem ser ajustados. Decisões a confirmar no início do desenvolvimento:

- Organização do ano: bimestres ou trimestres?
- Perfil Responsável entra no MVP ou na fase 2?
- Armazenamento de arquivos: disco local, S3 ou MinIO?
- Banco de dados: PostgreSQL (sugerido) ou MySQL?
- Modelo multi-escola ou escola única? (assumido: escola única)
