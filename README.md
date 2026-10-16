# nexora-frontend

Interface web do **Nexora**, um gerenciador financeiro pessoal de uso exclusivo do titular. Mostra a situação financeira, permite cadastrar e organizar as informações e configura os alertas. Consome a **nexora-api**.

> **Status:** em planejamento. Ainda não há código de interface. A tarefa "Interface base em React com Vite" está no Kanban, no épico Base do MVP.

Documentação completa do projeto: **Nexora — Dashboard** no Notion.
Requisitos e escopo: **Requisitos e escopo**. Arquitetura e stack: **Arquitetura e infraestrutura**. Decisões e descobertas: **Registro de decisões e descobertas (até 16/10/2026)**.

---

## Premissas

- **Uso pessoal.** Uma única conta, a do titular. Sem cadastro público.
- **Custo zero.** Nenhum serviço pago na interface, incluindo hospedagem, sem aprovação explícita.
- **Sem IA no MVP.** Decisão D-07.
- **Sem operações financeiras.** A interface não executa transferências, pagamentos nem renegociações.
- **Dados desatualizados sempre visíveis.** Toda tela com saldo ou transação mostra a data da última atualização.

## Escopo do MVP (telas)

Aprovado pelo titular em 15/10/2026.

- **Login:** entrada do titular com sessão.
- **Visão geral:** saldos por conta, próximos vencimentos, dinheiro disponível e data da última importação ou sincronização. Dados desatualizados aparecem marcados.
- **Contas:** cadastro e edição de contas com saldo informado e data do saldo.
- **Transações:** lista com filtros por período, conta e categoria, cadastro manual e categorização manual.
- **Importação:** envio de OFX e CSV, com mapeamento de colunas no CSV, e resumo de linhas aceitas e recusadas.
- **Compromissos e receitas:** cadastro de compromissos recorrentes, parcelas e recebimentos.
- **Projeção:** saldo diário até o fim do mês, com o detalhamento usado no cálculo.
- **Dívidas:** cadastro de dívidas com histórico de saldo e parcelas calculadas pelo método do contrato.
- **Conexões:** lista dos bancos conectados pelo Meu Pluggy, com status de cada item. Permite conectar e desconectar.
- **Configurações:** saldo mínimo (padrão R$ 250), limiares dos alertas e horário do e-mail (12h).

Fora do MVP: tela de IA, comparação de estratégias de quitação, simulação de amortização, metas e reserva.

## Decisões de interface

- **Valores monetários:** exibidos no padrão brasileiro (`R$ 1.234,56`), a partir de centavos inteiros vindos da API.
- **Idioma:** português brasileiro.
- **Estados vazios e de erro:** cada tela informa o que falta, sem valores fictícios.
- **Saldo não é dinheiro livre:** a visão geral deixa claro que o saldo bancário não considera compromissos previstos.

## Stack

| Camada | Tecnologia |
|---|---|
| Linguagem | TypeScript |
| Framework | React |
| Build e servidor de desenvolvimento | Vite |
| Testes | Vitest |

Roteamento, componentes e biblioteca de dados serão definidos na implementação. Qualquer dependência nova precisa ser justificada e não pode ter custo.

## Integração com a API

A interface nunca guarda credenciais de banco nem segredos. Toda chamada passa pela nexora-api, que é a única fonte de dados financeiros.

Antes de começar a interface, a API precisa expor os endpoints do MVP. Os nomes e formatos serão documentados no README da API.

## Configuração

Copie `.env.example` para `.env` e preencha a URL da API. O `.env` nunca é versionado.

| Variável | Uso |
|---|---|
| `VITE_API_URL` | Endereço da nexora-api (ex.: `http://127.0.0.1:3000`) |

## Como executar

Quando o projeto estiver criado:

```bash
npm install
npm run dev       # servidor de desenvolvimento
npm test          # testes
npm run build     # build de produção
```

A nexora-api precisa estar rodando para as telas que consomem dados.

## Testes

- **Componentes:** formatação de valores monetários, estados vazios e alertas de dados desatualizados.
- **Fluxos:** login, cadastro de conta, importação de arquivo e filtro de transações, com a API simulada.
- **Acessibilidade:** navegação por teclado e contraste nas telas principais.

Todos os testes usam dados fictícios.

## Segurança

- Nenhum segredo no código ou no build. Apenas a URL pública da API.
- Sessão do titular exigida em todas as telas de dados.
- Nenhum dado financeiro em armazenamento local do navegador além da sessão.

## Contribuição

Commits pequenos e descritivos, no formato `feat:`, `fix:`, `test:`, `docs:` ou `refactor:`. Cada tarefa tem critérios de conclusão no Kanban. O README do front é atualizado ao concluir cada épico, com base no Notion.

## Licença

Ainda não definida.