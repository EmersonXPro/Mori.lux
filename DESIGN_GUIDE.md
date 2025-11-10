# Mori.lux - Design Guide

## Visão Geral

O Mori.lux adota uma linguagem visual moderna, profissional e inovadora que reflete a natureza avançada da plataforma de inteligência artificial. O design enfatiza clareza, eficiência e confiabilidade através de uma paleta de cores cuidadosamente selecionada e tipografia elegante.

## Paleta de Cores

### Cores Primárias

A paleta primária do Mori.lux é baseada em tons de azul profundo, que transmitem confiança, inovação e tecnologia.

| Cor | Código HEX | Código RGB | Uso |
|---|---|---|---|
| Azul Escuro | `#0F172A` | rgb(15, 23, 42) | Fundo principal, backgrounds |
| Azul Profundo | `#1E3A8A` | rgb(30, 58, 138) | Backgrounds secundários, gradientes |
| Azul Brilhante | `#3B82F6` | rgb(59, 130, 246) | Botões primários, links, destaques |
| Azul Claro | `#60A5FA` | rgb(96, 165, 250) | Hover states, elementos interativos |

### Cores Secundárias

Cores de suporte para estados, mensagens e elementos de interface.

| Cor | Código HEX | Uso |
|---|---|---|
| Verde Sucesso | `#10B981` | Mensagens de sucesso, status ativo |
| Amarelo Aviso | `#F59E0B` | Avisos, alertas, atenção |
| Vermelho Erro | `#EF4444` | Erros, status crítico |
| Cinza Neutro | `#6B7280` | Texto secundário, bordas, divisores |

### Cores de Tema

#### Modo Claro

```css
--background: #FFFFFF;
--foreground: #0F172A;
--primary: #3B82F6;
--primary-foreground: #FFFFFF;
--secondary: #E5E7EB;
--secondary-foreground: #1F2937;
--accent: #1E3A8A;
--accent-foreground: #FFFFFF;
```

#### Modo Escuro

```css
--background: #0F172A;
--foreground: #F3F4F6;
--primary: #3B82F6;
--primary-foreground: #0F172A;
--secondary: #1F2937;
--secondary-foreground: #F3F4F6;
--accent: #60A5FA;
--accent-foreground: #0F172A;
```

#### Modo AMOLED (Escuro Extremo)

```css
--background: #000000;
--foreground: #FFFFFF;
--primary: #3B82F6;
--primary-foreground: #000000;
--secondary: #111827;
--secondary-foreground: #FFFFFF;
--accent: #60A5FA;
--accent-foreground: #000000;
```

## Tipografia

### Fontes

A plataforma utiliza a família de fontes **Inter** do Google Fonts para uma aparência moderna e legível.

```css
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap');

font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
```

### Escala Tipográfica

| Elemento | Tamanho | Peso | Altura da Linha |
|---|---|---|---|
| Heading 1 (H1) | 48px | 800 | 1.2 |
| Heading 2 (H2) | 36px | 700 | 1.25 |
| Heading 3 (H3) | 28px | 700 | 1.3 |
| Heading 4 (H4) | 24px | 600 | 1.35 |
| Body Large | 18px | 400 | 1.6 |
| Body Regular | 16px | 400 | 1.6 |
| Body Small | 14px | 400 | 1.5 |
| Caption | 12px | 500 | 1.4 |

## Componentes Visuais

### Botões

**Botão Primário** - Ação principal, chamada para ação

- Cor de fundo: Azul Brilhante (#3B82F6)
- Cor do texto: Branco
- Padding: 12px 24px
- Border Radius: 8px
- Transição: 200ms

**Botão Secundário** - Ações alternativas

- Cor de fundo: Cinza Neutro (#6B7280)
- Cor do texto: Branco
- Padding: 12px 24px
- Border Radius: 8px

**Botão Outline** - Ações menos importantes

- Cor de fundo: Transparente
- Cor da borda: Azul Brilhante (#3B82F6)
- Cor do texto: Azul Brilhante
- Padding: 12px 24px
- Border Radius: 8px

### Cards

Os cards são elementos fundamentais para apresentar informações agrupadas.

- Cor de fundo: Azul Profundo (#1E3A8A) em tema escuro
- Borda: 1px sólida em Cinza Neutro (#6B7280)
- Border Radius: 12px
- Padding: 20px
- Box Shadow: 0 4px 6px rgba(0, 0, 0, 0.1)
- Transição ao hover: elevação e brilho

### Inputs

Campos de entrada mantêm consistência visual com a paleta.

- Cor de fundo: Azul Escuro (#0F172A)
- Borda: 1px sólida em Cinza Neutro (#6B7280)
- Borda ao foco: 2px sólida em Azul Brilhante (#3B82F6)
- Border Radius: 8px
- Padding: 10px 14px
- Transição: 150ms

## Espaçamento

A plataforma utiliza um sistema de espaçamento baseado em múltiplos de 4px para consistência.

| Valor | Pixels | Uso |
|---|---|---|
| xs | 4px | Espaçamento mínimo |
| sm | 8px | Espaçamento pequeno |
| md | 16px | Espaçamento padrão |
| lg | 24px | Espaçamento grande |
| xl | 32px | Espaçamento extra grande |
| 2xl | 48px | Espaçamento duplo |

## Sombras

As sombras adicionam profundidade e hierarquia visual.

| Nível | CSS | Uso |
|---|---|---|
| Sombra Pequena | `0 1px 2px rgba(0, 0, 0, 0.05)` | Elementos sutis |
| Sombra Média | `0 4px 6px rgba(0, 0, 0, 0.1)` | Cards, modais |
| Sombra Grande | `0 10px 15px rgba(0, 0, 0, 0.1)` | Dropdowns, popovers |
| Sombra Extra | `0 20px 25px rgba(0, 0, 0, 0.15)` | Modais, overlays |

## Ícones

Todos os ícones utilizam a biblioteca **Lucide React** para consistência.

- Tamanho padrão: 24px
- Tamanho pequeno: 16px
- Tamanho grande: 32px
- Cor: Herda da cor do texto ou especificada explicitamente

## Animações

As animações são sutis e funcionais, melhorando a experiência sem distrair.

| Tipo | Duração | Easing |
|---|---|---|
| Hover | 200ms | ease-in-out |
| Fade | 300ms | ease-in-out |
| Slide | 300ms | ease-out |
| Scale | 200ms | ease-out |

## Responsividade

A plataforma é totalmente responsiva, adaptando-se a diferentes tamanhos de tela.

| Breakpoint | Largura | Uso |
|---|---|---|
| Mobile | < 640px | Telefones |
| Tablet | 640px - 1024px | Tablets |
| Desktop | > 1024px | Computadores |

## Acessibilidade

Todos os elementos visuais mantêm contraste adequado para acessibilidade WCAG AA.

- Contraste mínimo de texto: 4.5:1 para texto normal
- Contraste mínimo de texto: 3:1 para texto grande
- Foco visível em todos os elementos interativos
- Suporte para modo de alto contraste

## Exemplos de Uso

### Header

O header mantém o logo minimalista do Mori.lux à esquerda, navegação no centro e ícones de usuário à direita.

### Hero Section

A seção hero apresenta um headline impactante, subheading descritivo e call-to-action em destaque com fundo gradiente.

### Feature Cards

Cards apresentam ícones, títulos e descrições com hover effect que eleva o card e aumenta o brilho.

### Dashboard

O dashboard utiliza sidebar de navegação, cards para projetos e gráficos para analytics com cores consistentes.

---

*Guia de Design preparado por Manus AI - Última atualização: Novembro 2025*
