# Mori.lux - Documentação Completa do Projeto

## Visão Geral

**Mori.lux** é uma plataforma inovadora de inteligência artificial projetada para transformar a forma como empresas e profissionais abordam automação de processos, análise de dados e geração de conteúdo inteligente. A plataforma integra tecnologias de ponta em machine learning, processamento de linguagem natural e análise preditiva para oferecer soluções escaláveis e eficientes.

## Objetivos Principais

A plataforma Mori.lux foi desenvolvida com os seguintes objetivos estratégicos:

**Automação Inteligente** - Reduzir a carga manual de tarefas repetitivas através de algoritmos de aprendizado de máquina que se adaptam aos padrões de trabalho específicos de cada organização.

**Análise Preditiva Avançada** - Fornecer insights acionáveis sobre tendências futuras, permitindo que empresas tomem decisões baseadas em dados com maior confiança e precisão.

**Geração de Conteúdo Escalável** - Automatizar a criação de conteúdo de alta qualidade, desde relatórios técnicos até materiais de marketing, mantendo consistência e relevância.

**Integração Sem Fricção** - Conectar-se facilmente com sistemas existentes através de APIs bem documentadas e conectores pré-construídos para ferramentas populares.

## Arquitetura Técnica

A plataforma é construída sobre uma arquitetura moderna e escalável que combina as melhores práticas de desenvolvimento web contemporâneo:

### Stack Tecnológico

| Componente | Tecnologia | Propósito |
|---|---|---|
| Frontend | React 19 + Tailwind CSS 4 | Interface responsiva e moderna |
| Backend | Express.js 4 + Node.js | Servidor robusto e de alta performance |
| API | tRPC 11 | Type-safe RPC com end-to-end typing |
| Banco de Dados | MySQL/TiDB | Armazenamento relacional escalável |
| ORM | Drizzle ORM | Query builder type-safe |
| Autenticação | Manus OAuth | Gerenciamento seguro de identidade |
| Armazenamento | AWS S3 | Armazenamento de arquivos em nuvem |
| Processamento de IA | LLM Integration | Modelos de linguagem avançados |

### Estrutura de Diretórios

```
Mori.lux/
├── client/                    # Aplicação frontend React
│   ├── src/
│   │   ├── pages/            # Componentes de páginas
│   │   ├── components/       # Componentes reutilizáveis
│   │   ├── contexts/         # React contexts (tema, autenticação)
│   │   ├── hooks/            # Custom hooks
│   │   ├── lib/              # Utilitários e configurações
│   │   ├── App.tsx           # Roteamento principal
│   │   └── main.tsx          # Ponto de entrada
│   └── public/               # Ativos estáticos
├── server/                    # Aplicação backend Express
│   ├── routers.ts            # Definição de procedimentos tRPC
│   ├── db.ts                 # Helpers de consulta ao banco
│   ├── _core/                # Infraestrutura (OAuth, contexto, etc)
│   └── storage.ts            # Integração com S3
├── drizzle/                   # Esquema do banco de dados
│   └── schema.ts             # Definição de tabelas
├── shared/                    # Código compartilhado
│   └── const.ts              # Constantes globais
└── package.json              # Dependências do projeto
```

## Fluxo de Desenvolvimento

O desenvolvimento na plataforma Mori.lux segue um ciclo bem definido que garante qualidade e consistência:

**1. Definição do Schema** - Comece atualizando o arquivo `drizzle/schema.ts` com novas tabelas ou colunas necessárias. Execute `pnpm db:push` para aplicar as migrações ao banco de dados.

**2. Implementação de Helpers** - Adicione funções de consulta reutilizáveis em `server/db.ts`. Essas funções encapsulam a lógica de acesso aos dados e retornam resultados brutos do Drizzle.

**3. Criação de Procedimentos** - Defina novos procedimentos tRPC em `server/routers.ts`. Use `publicProcedure` para endpoints públicos e `protectedProcedure` para endpoints que requerem autenticação.

**4. Desenvolvimento Frontend** - Implemente a interface do usuário em `client/src/pages/` utilizando React hooks como `trpc.*.useQuery()` e `trpc.*.useMutation()` para comunicação com o backend.

## Recursos Principais

### Autenticação e Autorização

A plataforma implementa um sistema robusto de autenticação baseado em OAuth através da integração Manus OAuth. O fluxo funciona da seguinte forma:

- O usuário clica em "Fazer Login" e é redirecionado para o portal OAuth
- Após autenticação bem-sucedida, o servidor recebe um callback em `/api/oauth/callback`
- Uma sessão segura é criada e armazenada em um cookie HTTP-only
- Cada requisição subsequente ao `/api/trpc` inclui automaticamente o contexto do usuário
- Procedimentos protegidos verificam se o usuário está autenticado antes de executar lógica sensível

### Integração com Modelos de Linguagem

A plataforma integra modelos de linguagem avançados para capacidades de processamento de texto. O helper `invokeLLM()` permite:

**Completamento de Chat** - Enviar mensagens e receber respostas contextualizadas de um modelo de IA.

**Respostas Estruturadas** - Solicitar que o modelo retorne dados em formato JSON seguindo um schema específico.

**Processamento Multimodal** - Incluir imagens e documentos junto com texto para análise integrada.

### Armazenamento em Nuvem

Arquivos são armazenados em AWS S3 através do helper `storagePut()`. A plataforma segue a melhor prática de manter apenas metadados no banco de dados enquanto os bytes do arquivo residem em S3:

```typescript
const { url } = await storagePut(
  `${userId}-files/${fileName}.pdf`,
  fileBuffer,
  "application/pdf"
);
```

### Notificações do Proprietário

O sistema inclui um canal de notificação dedicado para alertas operacionais. Use `notifyOwner()` para enviar notificações sobre eventos importantes como novas submissões de formulário ou conclusão de workflows.

## Fluxo de Dados

A comunicação entre frontend e backend segue um padrão type-safe através do tRPC:

1. **Frontend** chama um hook tRPC como `trpc.feature.list.useQuery()`
2. **tRPC Client** serializa a requisição e envia para `/api/trpc`
3. **Backend** roteia para o procedimento correspondente em `server/routers.ts`
4. **Procedure** executa lógica de negócio, consultando o banco via `server/db.ts`
5. **Resposta** é serializada (incluindo Dates nativas) via SuperJSON
6. **Frontend** recebe dados tipados e renderiza a interface

## Temas e Personalização

A plataforma suporta temas claro e escuro com suporte a AMOLED. O tema é gerenciado através do `ThemeProvider` em `client/src/contexts/ThemeContext.tsx`. As cores são definidas como variáveis CSS em `client/src/index.css`:

```css
@layer base {
  :root {
    --background: 0 0% 100%;
    --foreground: 0 0% 3.6%;
    --primary: 0 0% 9%;
    --primary-foreground: 0 0% 98%;
  }
  
  .dark {
    --background: 0 0% 3.6%;
    --foreground: 0 0% 98%;
    --primary: 0 0% 98%;
    --primary-foreground: 0 0% 9%;
  }
}
```

## Segurança

A plataforma implementa múltiplas camadas de segurança:

**Autenticação OAuth** - Delegação segura de autenticação a um provedor confiável.

**Cookies HTTP-only** - Sessões armazenadas em cookies que não podem ser acessados via JavaScript.

**Type Safety End-to-End** - tRPC garante que requisições e respostas correspondem aos tipos esperados.

**Validação de Input** - Procedimentos validam dados de entrada antes de processar.

**Autorização Baseada em Papéis** - Suporte para diferentes níveis de acesso (admin vs user).

## Casos de Uso

Mori.lux é ideal para diversos cenários:

**Empresas de Tecnologia** - Automatizar análise de logs, geração de documentação técnica e triagem de tickets de suporte.

**Consultoria** - Gerar relatórios customizados, análises de mercado e recomendações estratégicas.

**Educação** - Criar materiais de aprendizado personalizados, avaliar trabalhos e fornecer feedback.

**Saúde** - Analisar dados de pacientes, gerar relatórios clínicos e auxiliar em diagnósticos.

**Varejo** - Prever demanda, otimizar preços e personalizar recomendações de produtos.

## Próximos Passos

Para começar a usar Mori.lux:

1. Acesse o servidor de desenvolvimento em `https://3000-...`
2. Faça login através do portal OAuth
3. Explore a interface e familiarize-se com os recursos
4. Consulte a documentação da API para integrar com seus sistemas
5. Configure notificações e alertas conforme necessário

## Suporte e Documentação

Para mais informações sobre desenvolvimento, consulte:

- **Documentação de tRPC**: https://trpc.io/docs
- **Tailwind CSS**: https://tailwindcss.com/docs
- **Drizzle ORM**: https://orm.drizzle.team/docs/overview
- **React**: https://react.dev

---

*Documentação preparada por Manus AI - Última atualização: Novembro 2025*
