# Design System LEVE – UNICAMP (v1.0)

Laboratório de Estudos do Veículo Elétrico, Descarbonização e Transição Energética.
Stack: React + Vite + TypeScript + Tailwind CSS + shadcn/ui + Lucide Icons + React Router.
Idioma: pt-BR. Mobile first. Acessibilidade WCAG 2.1 AA.

## 1. Princípios

| # | Princípio | Aplicação |
|---|---|---|
| 1 | Clareza acadêmica | Texto legível, hierarquia forte, muito espaço em branco |
| 2 | Energia limpa | Verde e azul protagonistas; ciano só como acento |
| 3 | Credibilidade institucional | Grafite profundo, grid consistente, dados e métricas em destaque |
| 4 | Acessível e responsivo | Mobile first, contraste AA, foco visível, navegação por teclado |
| 5 | Leve | Poucas animações, suaves (150–300 ms), sem excesso decorativo |

## 2. Cores (tokens)

| Token | Hex | Uso |
|---|---|---|
| primary (Esmeralda) | #059669 | Botões primários, ícones de destaque |
| primary-light | #10B981 | Hover, gráficos, badges, gradientes |
| secondary (Azul) | #0284C7 | Botões secundários, links, destaques tecnológicos |
| secondary-light | #0EA5E9 | Hover, gradientes, ilustrações |
| accent (Energia) | #06B6D4 | Sublinhados, ponto de data, indicadores |
| foreground (Grafite) | #0F172A | Títulos e texto principal |
| foreground-soft | #1E293B | Rodapé, seções e cards escuros |
| muted-text | #475569 | Texto de apoio |
| background-soft | #F8FAFC | Fundo de seções alternadas |
| card-soft | #F1F5F9 | Fundo de cards e inputs |
| surface | #FFFFFF | Base e cards elevados |
| border | #E2E8F0 | Divisórias e bordas |

**Gradiente de marca:** `linear-gradient(135deg, #059669 0%, #0EA5E9 100%)`
**Gradiente do hero (overlay):** `linear-gradient(135deg, rgba(15,23,42,.88) 0%, rgba(15,23,42,.55) 60%, rgba(5,150,105,.35) 100%)`

**Regras de acessibilidade de cor**
- #10B981 e #0EA5E9 não atingem contraste AA como texto pequeno sobre branco. Use só em fundos, ícones grandes, gráficos e bordas.
- Para texto/links sobre branco: esmeralda #047857 e azul #0369A1.
- Texto branco sobre botão #059669 só em texto grande/negrito (16px semibold ou mais). Em dúvida, use #047857 no botão.
- Nunca usar hex solto no código: apenas tokens/classes.

### CSS variables (`src/index.css`, formato shadcn/HSL)

```css
@layer base {
  :root {
    --background: 0 0% 100%;
    --foreground: 222 47% 11%;
    --card: 0 0% 100%;
    --card-foreground: 222 47% 11%;
    --popover: 0 0% 100%;
    --popover-foreground: 222 47% 11%;
    --primary: 160 94% 30%;            /* #059669 */
    --primary-foreground: 0 0% 100%;
    --secondary: 200 98% 39%;          /* #0284C7 */
    --secondary-foreground: 0 0% 100%;
    --muted: 210 40% 96%;              /* #F1F5F9 */
    --muted-foreground: 215 19% 35%;   /* #475569 */
    --accent: 189 94% 43%;             /* #06B6D4 */
    --accent-foreground: 222 47% 11%;
    --destructive: 0 72% 51%;
    --destructive-foreground: 0 0% 100%;
    --border: 214 32% 91%;             /* #E2E8F0 */
    --input: 214 32% 91%;
    --ring: 160 84% 39%;               /* #10B981 */
    --radius: 0.75rem;

    /* extras LEVE */
    --emerald-light: 160 84% 39%;      /* #10B981 */
    --sky-light: 199 89% 48%;          /* #0EA5E9 */
    --surface-soft: 210 40% 98%;       /* #F8FAFC */
    --ink-soft: 217 33% 17%;           /* #1E293B */
    --success: 160 84% 39%;
    --warning: 38 92% 50%;
    --info: 200 98% 39%;
  }
}
```

### Extensão do Tailwind (`tailwind.config.ts`)

```ts
extend: {
  colors: {
    leve: {
      emerald: { DEFAULT: '#059669', light: '#10B981', dark: '#047857' },
      blue:    { DEFAULT: '#0284C7', light: '#0EA5E9', dark: '#0369A1' },
      cyan:    '#06B6D4',
      ink:     { DEFAULT: '#0F172A', soft: '#1E293B' },
      mist:    { DEFAULT: '#F1F5F9', light: '#F8FAFC' },
    },
  },
  fontFamily: {
    sans: ['Inter', 'system-ui', 'sans-serif'],
    display: ['Outfit', 'Inter', 'sans-serif'],
  },
  backgroundImage: {
    'leve-gradient': 'linear-gradient(135deg, #059669 0%, #0EA5E9 100%)',
  },
  boxShadow: {
    card: '0 4px 6px -1px rgb(15 23 42 / 0.08), 0 2px 4px -2px rgb(15 23 42 / 0.06)',
    'card-hover': '0 20px 25px -5px rgb(15 23 42 / 0.12), 0 8px 10px -6px rgb(15 23 42 / 0.08)',
  },
}
```

## 3. Tipografia

Fontes (Google Fonts, `display=swap`): **Outfit** (títulos) e **Inter** (corpo, UI, dados). Usar só essas duas, com fallback.

| Estilo | Fonte | Tamanho (mobile → desktop) | Peso |
|---|---|---|---|
| Display (Hero) | Outfit | 36px → 60px | 700 |
| H1 | Outfit | 30px → 44px | 700 |
| H2 | Outfit | 24px → 34px | 600 |
| H3 | Outfit | 20px → 24px | 600 |
| H4 | Inter | 18px | 600 |
| Corpo | Inter | 16px → 17px | 400 |
| Corpo pequeno | Inter | 14px | 400 |
| Legenda/Meta | Inter | 12–13px | 500 |
| Overline (categoria) | Inter | 12px, caixa alta, tracking 0.08em | 600 |

Regras: largura máxima de leitura 68ch; títulos em `text-foreground`; apoio em `text-muted-foreground`; nunca centralizar parágrafos com mais de 3 linhas.

## 4. Layout, espaçamento e efeitos

- **Container:** `max-w-7xl mx-auto px-4 sm:px-6 lg:px-8`
- **Seções:** `py-16 md:py-24`; alternar `bg-white` e `bg-leve-mist-light`
- **Grid:** 12 colunas no desktop; cards em `grid gap-6 sm:grid-cols-2 lg:grid-cols-3`
- **Espaçamento:** múltiplos de 4px (padrão Tailwind)
- **Breakpoints:** sm 640 · md 768 · lg 1024 · xl 1280
- **Raios:** cards `rounded-xl`; botões e inputs `rounded-lg`; avatares e badges `rounded-full`
- **Sombras:** repouso `shadow-card`; hover `shadow-card-hover`
- **Movimento:** `transition-all duration-300 ease-out`; hover de card `hover:-translate-y-1`; entrada de seção com fade + subida de 12px (uma vez); respeitar `prefers-reduced-motion` (desativa translações e carrossel automático)
- **Ícones:** Lucide, traço 1.75, 16/20/24px, cor herdada
- **Imagens:** `object-cover`; 16:9 (notícias, eventos), 3:4 (capas de publicações), 1:1 (equipe); sempre `alt` descritivo (descreve a informação, não "foto de"); `loading="lazy"` abaixo da dobra

## 5. Componentes

### Botões
Base: `h-11 px-6 font-semibold rounded-lg`. Estados obrigatórios: hover, `focus-visible:ring-2 ring-ring ring-offset-2`, disabled (`opacity-50`), loading (spinner `Loader2`).

| Variante | Classes | Uso |
|---|---|---|
| Primário | `bg-primary text-white hover:bg-leve-emerald-dark shadow-md hover:shadow-xl` | CTA principal (1 por tela) |
| Secundário | `bg-secondary text-white hover:bg-leve-blue-dark` | Ações tecnológicas |
| Outline | `border-2 border-primary text-leve-emerald-dark hover:bg-primary/10` | Ações alternativas |
| Ghost | `text-foreground hover:bg-muted` | Navegação, ações discretas |
| Link | `text-leve-blue-dark underline-offset-4 hover:underline` + ícone `ArrowRight` | "Ler mais", "Ver todas" |

### Cards
- **Base:** `bg-white rounded-xl border border-border shadow-card hover:shadow-card-hover hover:-translate-y-1 transition-all duration-300 overflow-hidden`
- **Notícia:** imagem 16:9, badge de categoria, data (ícone `Calendar`), título H3 (2 linhas), excerto (`line-clamp-3`), link "Ler notícia".
- **Publicação:** capa 3:4 à esquerda (topo no mobile), badge de tipo, título, autores, ano, resumo (`line-clamp-3`), botões `Download PDF` e `DOI`, botão "Copiar citação" (ABNT/APA).
- **Evento:** bloco de data (dia grande + mês) em `bg-leve-gradient`, título, horário (`Clock`), local (`MapPin`), badge de status (Futuro / Realizado), botão.
- **Membro:** foto 1:1 redonda, nome (H4), cargo (`text-primary` semibold), mini-bio (3 linhas), ícones Lattes e LinkedIn.
- **Métrica:** número grande (Outfit 48px, gradiente de marca no texto), rótulo, ícone em círculo `bg-primary/10`.

### Badges
Base: `rounded-full px-3 py-1 text-xs font-semibold`.
- Notícia/Geral: `bg-primary/10 text-leve-emerald-dark`
- Pesquisa/Tecnologia: `bg-secondary/10 text-leve-blue-dark`
- Evento: `bg-accent/15 text-cyan-800`
- Tese/Dissertação/Livro/Artigo: cada um usa uma das cores acima, com ícone distinto.

### Formulários
- Input: `h-11 rounded-lg border border-border bg-white px-4 focus-visible:ring-2 ring-ring`
- Label sempre visível acima do campo (nunca só placeholder)
- Erro: borda `destructive`, ícone `AlertCircle`, mensagem abaixo em `text-sm`
- Busca: ícone `Search` à esquerda e botão limpar (`X`)
- Filtros: `Select` de Ano, Autor e Ordenação (mais recentes / mais antigos / A–Z)

### Navegação
- **Header sticky:** `sticky top-0 z-50 bg-white/85 backdrop-blur border-b border-border`, altura 72px (64px mobile), `shadow-md` ao rolar.
- **Dropdown desktop:** abre no hover e no foco/teclado (Radix `NavigationMenu`), painel `rounded-xl shadow-xl border bg-white p-2`, atraso de 150 ms para fechar, itens com ícone e descrição curta, item ativo com sublinhado `accent`.
- **Mobile (< lg):** botão hambúrguer abre `Sheet` lateral com `Accordion` para os submenus.
- **Breadcrumb:** em todas as páginas internas.
- **Rodapé:** fundo `leve-ink`, 4 colunas (Sobre o LEVE, Links rápidos, Contato, Redes), selo UNICAMP, copyright.

**Menu:** Início | Sobre (Leve, Equipe) | Projetos (CCD CPT-MOBi, PNUMA, CPTen) | Publicações (Teses, Dissertações, Livros, Artigos) | Notícias | Eventos | Contato.

### Outros
- **Hero interno:** faixa com gradiente escuro, H1, breadcrumb, 1 frase de apoio.
- **Carrossel:** Embla (shadcn `Carousel`), setas visíveis, paginação por pontos, swipe no mobile, 1/2/3 cards por vez (mobile/tablet/desktop).
- **Lightbox:** galeria em grid, modal de tela cheia, setas, `Esc` fecha, legenda e crédito.
- **Calendário:** `react-day-picker` estilizado; ponto `accent` = evento futuro, `primary` = realizado, anel `secondary` = hoje.
- **Skeleton:** `bg-muted animate-pulse`. **Estado vazio:** ícone + título + ação sugerida.
- **Toast:** `sonner`, topo direito (desktop) e inferior (mobile).

## 6. Voz, tom e UX writing

**Tom:** institucional, claro e acolhedor. Voz acadêmica que fala com todas as pessoas, não só especialistas.

| Atributo | Como soa | Evitar |
|---|---|---|
| Confiável | Dados, fontes, verbos no presente, precisão | Promessas exageradas, "revolucionário" |
| Acessível | Frases curtas, termos técnicos explicados na 1ª vez | Jargão sem contexto, siglas soltas |
| Engajador | Verbos de ação, foco em impacto social | Tom publicitário, excesso de exclamações |
| Inclusivo | Linguagem que inclui todas as pessoas | Estereótipos, masculino genérico quando houver alternativa simples |
| Comprometido | Posicionamento claro por transição justa | Neutralidade vazia, "greenwashing" |

Pessoa gramatical: **nós** para o laboratório, **você** para quem lê. Português do Brasil formal-leve, sem gírias.

**Regras**
1. Escreva para ser escaneado: informação mais importante primeiro; parágrafos de até 4 linhas.
2. Títulos informativos ("Teses defendidas no LEVE", não "Nossos trabalhos").
3. Botões começam com verbo e dizem o resultado (Conheça o LEVE, Baixar PDF, Enviar mensagem, Ver agenda completa). Evite "Clique aqui" e "Saiba mais" isolado.
4. Links descritivos, pensando em leitores de tela.
5. Siglas por extenso na primeira ocorrência: Laboratório de Estudos do Veículo Elétrico (LEVE).
6. Datas: `11 de novembro de 2026` (corpo) e `11/11/2026` (compacto); horário `14h30`.
7. Números: milhar com ponto, decimal com vírgula (1.250; 3,5 %).
8. Capitalização: só a primeira letra em títulos e botões; nomes próprios mantêm maiúsculas.
9. Sem culpar a pessoa: erros explicam o problema e a solução.
10. Uma ideia por frase, uma ação principal por tela.
11. Citações: ABNT como padrão, APA como alternativa.

### Mensagens padrão
Estrutura: o que aconteceu + o que fazer agora, em até duas frases. Ícone + cor + texto (nunca só cor).

| Tipo | Ícone / cor | Exemplo |
|---|---|---|
| Sucesso | CheckCircle2 · verde | **Mensagem enviada!** Responderemos em até 3 dias úteis. |
| Erro de campo | AlertCircle · vermelho | Informe um e-mail válido, como nome@dominio.com. |
| Campo obrigatório | AlertCircle · vermelho | Preencha este campo para continuar. |
| Erro de envio | XCircle · vermelho | Não foi possível enviar sua mensagem. Verifique sua conexão e tente novamente. |
| Erro de carregamento | RefreshCw · cinza | Não conseguimos carregar as publicações. Tente novamente. |
| Aviso | AlertTriangle · âmbar | Este evento está com poucas vagas. Inscreva-se logo. |
| Informação | Info · azul | Os resultados foram filtrados pelo ano de 2025. |
| Cópia | Copy · verde | Citação ABNT copiada. |
| Download | Download · verde | Seu download começou. |
| Download indisponível | FileX · cinza | Este arquivo ainda não está disponível. Fale com a gente pelo contato. |
| Busca sem resultado | SearchX · cinza | Nenhum resultado para "mobilidade". Tente outras palavras ou limpe os filtros. |
| Dia sem evento | CalendarX · cinza | Nenhum evento nesta data. Veja o próximo evento da agenda. |
| Página 404 | Compass · azul | **Página não encontrada.** O endereço pode ter mudado. Volte ao início ou use o menu. |
| Carregando | Loader2 | Carregando… |

**Microcopy padrão**
- Placeholder de busca: *Busque por título, autor ou palavra-chave*
- Contador: *12 resultados* / *1 resultado*
- Formulário: *Como podemos ajudar?* · botão *Enviar mensagem*
- LGPD: *Usaremos seus dados apenas para responder a esta mensagem.*
- Inscrição: *Garantir minha vaga* · Evento passado: *Evento realizado em 20/10/2026*

## 7. Acessibilidade

- Contraste mínimo AA (4,5:1 texto normal; 3:1 texto grande e componentes de UI).
- Foco visível em todos os elementos interativos; ordem de tabulação lógica; dropdown navegável por teclado.
- `lang="pt-BR"`, `aria-label` nos ícones-link, `alt` em todas as imagens, vídeos com legenda.
- Alvos de toque mínimos de 44×44px.
- `prefers-reduced-motion` desativa translações e carrossel automático.

## 8. Regras de dados (para o código)

- Ler sempre de `src/data/*.ts` tipados, via camada `src/services/`, para trocar por Supabase depois sem mexer na UI.
- O status do evento (futuro/realizado) é **derivado da data atual**, nunca fixo.

## 9. Checklist antes de publicar

- [ ] Todas as cores vêm de tokens (nenhum hex solto)
- [ ] Apenas Outfit e Inter, com fallback
- [ ] Contraste AA verificado em textos sobre verde e azul
- [ ] Dropdown funciona por hover, foco e toque
- [ ] Todas as rotas existem e aparecem no breadcrumb
- [ ] Calendário diferencia passado e futuro corretamente
- [ ] Formulário valida e mostra erro e sucesso conforme a seção 6
- [ ] Imagens com `alt`, `loading="lazy"` e proporção definida
- [ ] Testado em 360px, 768px e 1280px
- [ ] Meta tags (title, description, Open Graph) por página, `lang="pt-BR"`
