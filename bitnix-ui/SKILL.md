---
name: "bitnix-ui"
description: "Design system Bitnix: fundamentos, componentes em CSS e oito famílias de página (home, listagem, detalhe, institucional, conversão, estados, área logada, suporte) para site e app."
---

# Bitnix UI · Design System

Design system extraído de três peças da Bitnix: a home de uma agência com um case de cliente, um site institucional (home e seções internas) e um app (10 telas de fluxo). As três têm cor, segmento e plataforma diferentes. O que se repete é a gramática visual, e é ela que este sistema organiza em três camadas:

1. **Fundamentos:** regras que valem em qualquer tela.
2. **Componentes:** peças prontas, com CSS de referência.
3. **Catálogo de páginas:** oito famílias que cobrem qualquer página ou tela, cada uma com seu nível de expressão e receita.

Cor não faz parte do estilo. Ela vem da marca do cliente (ver "Cor").

---

## 1. Fundamentos

### 1.1 Grid rígido, quebra controlada

A base é sempre um grid claro: container central (1200px no desktop, 16-24px de margem no mobile), 12 colunas no site e 4 no app, alinhamentos simétricos e títulos de seção centralizados ou alinhados à esquerda com controles à direita na mesma linha.

Sobre essa base, alguns elementos invadem o limite do bloco. É a assinatura do sistema. A intensidade da quebra depende do nível de expressão da página (seção 3.1):

- Elemento que cavalga uma divisória: barra de busca metade no hero e metade na seção seguinte, botão circular sobre a linha entre o corpo e o rodapé do card, card de conteúdo que sobe sobre o header da página.
- Imagem ou assunto que passa da borda do seu bloco, como uma cadeira que sai do container ou a cabeça que passa da moldura.
- Tipografia maior que o container, cortada pela borda.

Técnica: margem negativa, `translate`, `overflow: visible` e `z-index` explícito. A quebra só funciona se o grid for evidente, por isso o alinhamento do resto precisa ser impecável.

### 1.2 Tipografia em caixa alta com peso misto

- **Caixa alta com tracking** em títulos, navegação, labels de botão, rótulos de dado, abas e cabeçalhos de lista. Tracking de `.02em` nos títulos grandes a `.08em` nos textos pequenos.
- **Peso misto como destaque:** a frase em peso leve e a palavra-chave em bold ("OS MELHORES IMÓVEIS DE **JURERÊ**", "OLÁ, **JOSIAS**", "NOSSOS **PROFESSORES**"). O destaque se faz pelo peso, sem trocar de cor.
- **Sentence case** em corpo de texto, descrições, placeholders e mensagens, com peso regular e frases curtas. Mensagens de onboarding, confirmação e estado vazio ficam centralizadas.
- Fontes: sans geométrica ou grotesca (Montserrat, Poppins, Archivo, Manrope, Inter Tight). Para a palavra-objeto em hero: Anton, Archivo Black, Bebas Neue. Se a marca tiver fonte, use a dela com as mesmas regras.

Escala (desktop / mobile):

| Token | Uso | Desktop | Mobile |
|---|---|---|---|
| `display` | palavra-objeto ou título de hero | clamp(56px, 8vw, 120px) | 44-56px |
| `h1` | título de página | 48px | 28px |
| `h2` | título de seção | 36px | 24px |
| `h3` | título de card, app bar | 18px | 16px |
| `body` | texto corrido | 17px | 15-16px |
| `label` | rótulo de dado, eyebrow, legenda | 11px | 10-11px |

### 1.3 Linha e contorno como acabamento

O acabamento vem de linha, e sombra e gradiente não entram. Três espessuras:

- `--line-1` (1px): divisórias, células de dado, borda de card neutro, setas de carrossel.
- `--line-2` (2px): borda de input em foco, botão contornado pequeno, ícones.
- `--line-3` (3px): moldura de card de destaque, botão contornado grande, moldura-palco.

Ícones sempre de linha, traço de 1.5-2px (Lucide, Feather, Phosphor Light). Nunca ícone preenchido colorido.

### 1.4 Forma e profundidade

- **Cantos retos** em cards, inputs, botões, abas e seções. O círculo aparece em avatar, botão de ícone, paginação, badge e radio, e a pílula só no botão contornado sobre fundo escuro.
- **Profundidade por sobreposição.** Sombra no máximo `0 1px 2px rgba(0,0,0,.06)` em card sobre fundo claro. Botões e inputs podem ter um "pé" de 3px (`inset 0 -3px 0 rgba(0,0,0,.12)`) para parecerem físicos.
- **Blocos chapados de largura total** alternando entre cor da marca, neutro claro e branco para separar as seções.

### 1.5 Imagem

- **Foto real**, com gente de expressão aberta, produto nítido ou ambiente iluminado. Nada de ilustração genérica de banco.
- **Três tratamentos:** foto com overlay chapado na cor da marca ou num tom escuro dela (fundo de hero, login e onboarding); foto dessaturada e lavada em branco a 85-90% (fundo de telas internas de app); e **recorte sem fundo** (o assunto em camadas, seção 1.6).
- Imagem de conteúdo (card de imóvel, produto, projeto) fica dentro de moldura, em proporção fixa por grupo.

### 1.6 Assunto recortado em camadas (recurso expressivo)

Esse recurso entra só onde o nível de expressão pede (seção 3.1). Quando entra, um elemento sem fundo fica entre camadas: fundo, depois a palavra gigante ou a moldura, depois o assunto e por cima o texto e os CTAs. O assunto corta numa borda e transborda outra.

O assunto pode ser:
- **uma pessoa** (uma garota na frente do título, consultores saindo da moldura);
- **um produto ou objeto** (a cadeira Barcelona, um celular com a tela do app, o item do segmento);
- **a própria tipografia**, com a palavra-chave gigante e com volume;
- **uma forma gráfica**, como o círculo sólido com ícone grande da abertura do app.

Escolha pelo que o briefing oferece. Não invente pessoa quando o produto ou a tipografia contam melhor a história. Sem imagem disponível, use placeholder no formato do assunto escolhido e comente o que entra. Recorte de arquivo do usuário: `rembg` em Python ou a ferramenta de remover fundo da sessão.

A palavra-objeto nunca passa por baixo do texto funcional (título, subtítulo, CTA). Posicione-a fora da zona de leitura ou deixe o assunto cobrir o cruzamento.

### 1.7 Cor

A cor vem da marca do cliente. Se não veio no pedido, pergunte (cor principal e fonte, se houver). A aplicação é sempre a mesma:

- **`--brand`:** uma cor dominante chapada em áreas grandes (hero, faixa de seção, app bar, header de página interna) ou no CTA principal.
- **`--ink`:** neutro escuro de apoio (a marca escurecida e dessaturada, ou um grafite). É a cor de trabalho para texto forte, botões dentro de cards, ícones ativos e radio selecionado. Resolve o caso de marca clara (amarelo, por exemplo) que não sustenta texto branco.
- **Escada tonal:** listas de categorias ou itens equivalentes em sequência usam a mesma matiz clareando a cada item (`color-mix` de `--ink` com branco). Isso dá ritmo sem precisar de novas cores.
- Neutros claros para seções alternadas e cor semântica (sucesso, erro, avaliação) só onde tiver função.

### 1.8 Voz de interface

**CTA em primeira pessoa.** Botões de decisão falam na voz do usuário, em caixa alta: QUERO ME INSCREVER, QUERO COMPRAR, QUERO PEDIR ORÇAMENTO, QUERO FAZER A SIMULAÇÃO. Quando a decisão parece do usuário, e não uma oferta empurrada, a objeção cai (EU QUERO COMPRAR em vez de VOCÊ ESTÁ ME VENDENDO ALGO). Evite o imperativo de terceira pessoa (INSCREVA-SE, COMPRE AGORA) nos CTAs de conversão; testes A/B de aceitação favorecem a primeira pessoa. Ações de navegação ou utilitárias, sem decisão de compra ou cadastro, podem seguir no imperativo curto (ENTRAR, CONTINUAR, VOLTAR, VER PROJETO). Saudação pessoal com o nome em bold. Subtítulo em forma de pergunta direta ("Que profissional você precisa para sua reforma?"). Confirmação com promessa concreta ("Você receberá uma resposta em até 24h").

---

## 2. Componentes

Use esta folha como base de todo projeto. Troque só o bloco de marca. As classes usam o prefixo `bx-`. Em React, cada bloco vira um componente e os tokens vão para um arquivo de tema.

```css
/* ===== TOKENS: troque só o bloco de marca ===== */
:root{
  --brand:#0B6E4F; --on-brand:#FFFFFF;            /* marca do cliente */
  --ink:#24302C;                                   /* neutro escuro derivado da marca */
  --ink-soft:#5E6B67; --muted:#8C9591;
  --surface:#FFFFFF; --surface-alt:#F3F4F2; --wash:rgba(255,255,255,.88);
  --line:#DCE0DD;
  --success:#74B825; --danger:#CE202A; --star:#F1C600;
  --line-1:1px; --line-2:2px; --line-3:3px;
  --font:"Montserrat",system-ui,sans-serif; --display:"Anton","Archivo Black",Impact,sans-serif;
  --container:1200px; --gutter:clamp(16px,4vw,32px);
  --s1:8px; --s2:16px; --s3:24px; --s4:32px; --s6:48px; --s8:64px; --s12:96px; --s16:128px;
  --press:inset 0 -3px 0 rgba(0,0,0,.12); --lift:0 1px 2px rgba(0,0,0,.06);
}
*{box-sizing:border-box;margin:0}
body{font-family:var(--font);color:var(--ink);background:var(--surface);font-size:17px;line-height:1.5}
.bx-container{max-width:var(--container);margin:0 auto;padding:0 var(--gutter);position:relative}

/* ===== TIPOGRAFIA ===== */
.bx-caps{text-transform:uppercase;letter-spacing:.06em}
.bx-display{font-family:var(--display);font-size:clamp(56px,8vw,120px);line-height:.9;text-transform:uppercase}
.bx-h1,.bx-h2{text-transform:uppercase;font-weight:300;letter-spacing:.02em;line-height:1.05}
.bx-h1{font-size:clamp(28px,4vw,48px)} .bx-h2{font-size:clamp(24px,3vw,36px)}
.bx-h1 b,.bx-h2 b{font-weight:800}
.bx-h3{font-size:18px;font-weight:700;text-transform:uppercase;letter-spacing:.06em}
.bx-label{font-size:11px;font-weight:600;letter-spacing:.08em;text-transform:uppercase;color:var(--muted)}
.bx-lead{color:var(--ink-soft);max-width:56ch}

/* ===== BOTÕES ===== */
.bx-btn{display:inline-flex;align-items:center;justify-content:center;gap:12px;min-height:52px;padding:0 28px;border:0;border-radius:0;
  font:700 14px/1 var(--font);letter-spacing:.08em;text-transform:uppercase;cursor:pointer;text-decoration:none;
  background:var(--brand);color:var(--on-brand);box-shadow:var(--press)}
.bx-btn--ink{background:var(--ink);color:#fff}
.bx-btn--block{width:100%}
.bx-btn--outline{background:none;box-shadow:none;border:var(--line-3) solid currentColor;color:var(--ink)}
.bx-btn--outline::before{content:"";width:16px;height:var(--line-3);background:currentColor}   /* traço "— VER PROJETO" */
.bx-btn--ghost{background:none;box-shadow:none;border:var(--line-2) solid #fff;color:#fff;border-radius:999px}  /* só sobre fundo escuro */
.bx-btn:focus-visible,.bx-field:focus-visible{outline:var(--line-2) solid var(--brand);outline-offset:3px}
.bx-icon-btn{width:56px;height:56px;border-radius:50%;display:grid;place-items:center;background:var(--ink);color:#fff;border:var(--line-3) solid #fff}
.bx-arrows{display:inline-flex;border:var(--line-1) solid currentColor}
.bx-arrows button{width:48px;height:44px;background:none;border:0;color:inherit;cursor:pointer}
.bx-arrows button+button{border-left:var(--line-1) solid currentColor}

/* ===== FORMULÁRIO ===== */
.bx-field{width:100%;min-height:52px;padding:0 16px;border:0;border-bottom:var(--line-2) solid var(--line);border-radius:0;background:#fff;font:400 16px var(--font);color:var(--ink)}
.bx-field::placeholder{color:var(--muted)}
.bx-fieldset{display:grid;gap:var(--s1)} .bx-row{display:grid;grid-template-columns:2fr 1fr;gap:var(--s1)}
.bx-input-action{display:grid;grid-template-columns:1fr 56px} .bx-input-action button{background:var(--ink);color:#fff;border:0}
.bx-radio{display:inline-flex;align-items:center;gap:12px}
.bx-radio input{appearance:none;width:26px;height:26px;border-radius:50%;border:var(--line-2) solid var(--line);background:#fff}
.bx-radio input:checked{background:var(--ink);box-shadow:inset 0 0 0 4px #fff}
.bx-searchbar{display:grid;grid-template-columns:repeat(var(--cols,3),1fr) 72px;background:#fff;border:var(--line-1) solid var(--line)}
.bx-searchbar>div{padding:16px 20px;border-right:var(--line-1) solid var(--line)}
.bx-searchbar>button{background:var(--brand);color:var(--on-brand);border:0}
.bx-tabs{display:flex;border-bottom:var(--line-1) solid var(--line)}
.bx-tabs button{padding:14px 20px;background:none;border:0;border-bottom:var(--line-3) solid transparent;font:700 12px var(--font);letter-spacing:.08em;text-transform:uppercase;color:var(--muted)}
.bx-tabs [aria-selected=true]{color:var(--ink);border-color:var(--brand)}

/* ===== CARDS E DADOS ===== */
.bx-card{background:#fff;box-shadow:var(--lift);position:relative}
.bx-card__body{padding:var(--s3)}
.bx-card--framed{border:var(--line-3) solid #fff;outline:var(--line-1) solid var(--line);box-shadow:none}   /* card de imóvel/projeto */
.bx-card--framed .bx-card__media{aspect-ratio:16/10;object-fit:cover;width:100%;display:block}
.bx-card--framed .bx-card__caption{padding:16px 18px;border-top:var(--line-3) solid #fff}
.bx-card--on-brand{background:var(--brand);color:var(--on-brand);border-color:#fff;outline:0}
.bx-data{display:grid;grid-template-columns:repeat(var(--cols,2),1fr);border-top:var(--line-1) solid var(--line)}
.bx-data>div{padding:12px;text-align:center;border-right:var(--line-1) solid var(--line);border-bottom:var(--line-1) solid var(--line)}
.bx-data>div:nth-child(var(--cols,2)n){border-right:0}
.bx-data strong{display:block;font-size:16px;font-weight:700;color:var(--ink)}
.bx-price{text-align:center;font-size:32px;font-weight:700} .bx-price small{font-weight:400;font-size:.7em}
.bx-avatar{width:72px;height:72px;border-radius:50%;object-fit:cover;border:var(--line-3) solid #fff;box-shadow:0 0 0 var(--line-1) var(--line)}
.bx-card__footer{display:grid;grid-template-columns:1fr auto 1fr;align-items:center;background:var(--surface-alt);border-top:var(--line-1) solid var(--line);padding:10px 16px;text-align:center}
.bx-card__footer .bx-icon-btn{margin-top:-28px}                     /* quebra: botão cavalga a divisória */
.bx-stage{position:relative;border:var(--line-3) solid var(--brand);height:200px;overflow:visible}
.bx-stage>img{position:absolute;left:50%;bottom:0;transform:translateX(-50%);height:140%}   /* assunto sai por cima da moldura */

/* ===== NAVEGAÇÃO ===== */
.bx-topbar{border-bottom:var(--line-1) solid var(--line);font-size:13px}
.bx-nav{display:flex;gap:var(--s4);font:700 12px var(--font);letter-spacing:.08em;text-transform:uppercase}
.bx-nav a{color:inherit;text-decoration:none;padding:6px 0;border-bottom:var(--line-2) solid transparent}
.bx-nav a[aria-current]{border-color:currentColor}
.bx-social a{width:32px;height:32px;border-radius:50%;border:var(--line-1) solid currentColor;display:inline-grid;place-items:center}
.bx-breadcrumb{font-size:11px;letter-spacing:.08em;text-transform:uppercase;opacity:.8}
.bx-appbar{height:56px;display:flex;align-items:center;gap:16px;padding:0 16px;background:var(--brand);color:var(--on-brand);font:700 15px var(--font);letter-spacing:.06em;text-transform:uppercase}
.bx-tabbar{height:60px;display:flex;justify-content:space-around;align-items:center;background:var(--surface-alt);border-top:var(--line-1) solid var(--line)}
.bx-tabbar a{position:relative;color:var(--ink)}
.bx-badge{position:absolute;top:-6px;right:-10px;min-width:18px;height:18px;border-radius:9px;background:var(--danger);color:#fff;font:700 11px/18px var(--font);text-align:center}

/* ===== SEÇÕES E LISTAS ===== */
.bx-section{padding:var(--s12) 0} .bx-section--brand{background:var(--brand);color:var(--on-brand)} .bx-section--alt{background:var(--surface-alt)}
.bx-section-head{display:flex;justify-content:space-between;align-items:flex-end;gap:var(--s3);padding-bottom:var(--s3);border-bottom:var(--line-1) solid currentColor;margin-bottom:var(--s6)}
.bx-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(260px,1fr));gap:var(--s4)}
.bx-ladder{display:grid;gap:var(--s1)}                                 /* escada tonal */
.bx-ladder>a{display:flex;align-items:center;gap:18px;min-height:56px;padding:0 20px;color:#fff;text-decoration:none;font:700 15px var(--font);letter-spacing:.06em;text-transform:uppercase;box-shadow:var(--press)}
.bx-ladder>a:nth-child(1){background:var(--ink)}
.bx-ladder>a:nth-child(2){background:color-mix(in srgb,var(--ink) 88%,#fff)}
.bx-ladder>a:nth-child(3){background:color-mix(in srgb,var(--ink) 76%,#fff)}
.bx-ladder>a:nth-child(4){background:color-mix(in srgb,var(--ink) 64%,#fff)}
.bx-ladder>a:nth-child(n+5){background:color-mix(in srgb,var(--ink) 54%,#fff)}
.bx-list-group>header{display:flex;align-items:center;gap:14px;padding:16px;font:700 14px var(--font);letter-spacing:.06em;text-transform:uppercase;border-bottom:var(--line-1) solid var(--line)}
.bx-list-row{display:grid;grid-template-columns:auto 1fr auto;gap:16px;align-items:center;padding:14px 16px;border-bottom:var(--line-1) solid var(--line);background:#fff}
.bx-page-header{background:var(--brand);color:var(--on-brand);padding:var(--s8) 0 calc(var(--s8) + 48px)}
.bx-overlap-up{margin-top:-48px;position:relative;z-index:2}          /* quebra: conteúdo sobe sobre o header */
.bx-footer{border-top:var(--line-1) solid var(--line);padding:var(--s6) 0;font-size:13px}
.bx-footer-bar{background:var(--brand);color:var(--on-brand);padding:14px 0;font-size:12px;text-align:center}
@media (prefers-reduced-motion:reduce){*{animation:none!important;transition:none!important}}
```

Inventário e onde cada peça aparece nas referências:

| Componente | Classe | Referência |
|---|---|---|
| Botão sólido | `.bx-btn` / `--ink` / `--block` | ENTRAR, CONTRATAR, FAZER SIMULAÇÃO |
| Botão contornado com traço | `.bx-btn--outline` | "— VER PROJETO" (Bitnix), SAIBA MAIS |
| Botão pílula fantasma | `.bx-btn--ghost` | CRIAR UMA CONTA no login escuro |
| Botão de ícone circular | `.bx-icon-btn` | chat do card de profissional |
| Setas de carrossel | `.bx-arrows` | LANÇAMENTOS, slider da Bitnix |
| Campo, linha de campos, campo com ação | `.bx-field`, `.bx-row`, `.bx-input-action` | cadastro, pagamento, metragem + câmera |
| Radio em grade | `.bx-radio` | Interna/Externa, Tinta óleo/látex |
| Barra de busca segmentada | `.bx-searchbar` | busca de imóveis sobre o hero |
| Abas | `.bx-tabs` | COMPRAR/ALUGAR, CENTRO/JURERÊ |
| Card neutro | `.bx-card` + `__body` + `__footer` | card de profissional |
| Card emoldurado | `.bx-card--framed` (+ `--on-brand`) | cards de lançamento |
| Pares de dado | `.bx-data` | PREÇO MÉDIO, METRAGEM, ORÇAMENTO |
| Preço destacado | `.bx-price` | R$ 680,00 |
| Avatar | `.bx-avatar` | fotos dos profissionais |
| Moldura-palco | `.bx-stage` | consultores saindo da moldura |
| Topbar, nav, redes | `.bx-topbar`, `.bx-nav`, `.bx-social` | cabeçalho do site institucional |
| App bar, tab bar, badge | `.bx-appbar`, `.bx-tabbar`, `.bx-badge` | app de fluxo |
| Cabeçalho de seção | `.bx-section-head` | título + setas + linha |
| Escada tonal | `.bx-ladder` | PEDREIRO → HIDRÁULICO |
| Lista agrupada | `.bx-list-group`, `.bx-list-row` | ORÇAMENTOS por categoria |
| Header de página interna | `.bx-page-header` + `.bx-overlap-up` | padrão derivado para páginas internas |
| Rodapé | `.bx-footer`, `.bx-footer-bar` | rodapé do site institucional |

Para um componente novo que não está na lista, derive dos fundamentos: canto reto, linha em vez de sombra, label em caixa alta e, se couber, um elemento cavalgando a borda.

---

## 3. Catálogo de páginas

Qualquer página ou tela cai em uma de oito famílias. A família define a estrutura e o **nível de expressão**, ou seja, quanto de quebra de grid e de assunto recortado aparece. A plataforma (site ou app) muda a moldura (header e rodapé no site, app bar e tab bar no app), mas não muda a família.

### 3.1 Níveis de expressão

| Nível | Assunto recortado | Palavra-objeto | Quebra de grid | Bloco de marca | Densidade |
|---|---|---|---|---|---|
| **Alto** | Sim, no topo e em 1-2 seções | Pode | Forte, em toda seção | Hero e faixas inteiras | Baixa, muito respiro |
| **Médio** | Opcional, só se o briefing oferecer | Não | Leve: conteúdo sobe sobre o header, card cavalgando | Header de página e rodapé | Média |
| **Funcional** | Não (exceto avatar quando o conteúdo é sobre pessoas) | Não | Micro: avatar, botão ou busca cavalgando divisórias | App bar, header compacto, CTA | Alta |

### 3.2 As oito famílias

| Família | Páginas e telas | Nível | Estrutura base |
|---|---|---|---|
| **A. Vitrine** | Home, landing de campanha, landing de produto, lançamento, hotsite, pré-lançamento/lista de espera, splash e onboarding de app | Alto | Hero em camadas, faixas alternadas, CTA recorrente |
| **B. Listagem** | Catálogo, categoria, resultado de busca, lista de imóveis/cursos/produtos, portfólio de cases, blog, equipe, lista de profissionais (app) | Médio no site, Funcional no app | Header de página, filtros cavalgando, grid de cards, paginação |
| **C. Detalhe** | Produto, imóvel, curso, case/projeto, perfil de profissional, artigo, evento, detalhe de pedido | Médio | Galeria emoldurada + coluna de dados e CTA fixo |
| **D. Institucional** | Sobre, história, método, serviços (visão geral e serviço individual), carreiras e vaga, parceiros, imprensa, unidades | Médio (Alto se for página-campanha) | Header de página, blocos de narrativa alternados, moldura-palco |
| **E. Conversão** | Contato, orçamento, simulador, agendamento, planos e preços, cadastro, login, recuperar senha, carrinho, entrega, pagamento | Funcional (Médio em planos e preços) | Formulário focado, resumo lateral, um CTA dominante |
| **F. Retorno e estado** | Confirmação/obrigado, sucesso, erro 404/500, estado vazio, sem conexão, manutenção, carregando | Funcional com um toque expressivo | Tela centrada: forma gráfica grande, título em caixa alta, promessa, uma ação |
| **G. Área logada** | Dashboard, meus pedidos/orçamentos, histórico, favoritos, mensagens/chat, notificações, carteira, perfil e edição, configurações | Funcional | App bar ou header compacto, listas agrupadas, pares de dado, abas |
| **H. Suporte e utilitário** | FAQ, central de ajuda, termos, privacidade, mapa do site, comparador, busca global | Funcional | Header de página, índice lateral ou abas, texto corrido com subtítulos |

Camadas sobrepostas (em qualquer família): modal, drawer de menu, bottom sheet de filtros, toast e tooltip. Seguem os mesmos fundamentos: canto reto, borda de linha em vez de sombra, título em `.bx-h3` e CTA em bloco. O overlay de fundo é `--ink` a 60%.

### 3.3 Receitas por família

**A. Vitrine (site)** (site institucional e Bitnix)
1. Topbar fina (redes em círculo contornado, contato à direita), header com logo e `.bx-nav`.
2. Hero: bloco de marca ou foto com overlay, assunto recortado em camadas, título com peso misto ou palavra-objeto, CTA sólido ou contornado, `.bx-arrows` se for slider. `.bx-searchbar` ou formulário curto cavalgando a base.
3. Faixa de destaque `.bx-section--brand` com `.bx-section-head` e grid de `.bx-card--framed --on-brand`.
4. Faixa neutra `.bx-section--alt` com cards emoldurados claros.
5. Bloco de argumento: título à esquerda, `.bx-stage` com assunto saindo da moldura, `.bx-btn--outline`.
6. Bloco de conversão: formulário em linha (`.bx-row`), assunto apontando para ele, selo de parceiro.
7. Mapa ou unidades com `.bx-tabs`, e rodapé com nav repetida e `.bx-footer-bar`.

**A. Vitrine (app): splash e onboarding.** Foto com overlay, assunto como forma gráfica (círculo `--brand` com ícone de linha) ou recorte, frase centralizada, paginação em círculos, link PULAR em `.bx-label`. O login usa o mesmo fundo com `.bx-btn` + `.bx-btn--ghost`.

**B. Listagem.** Site: `.bx-page-header` com título de peso misto ("NOSSOS **IMÓVEIS**"), `.bx-searchbar` de filtros em `.bx-overlap-up`, contagem de resultados em `.bx-label`, grid de `.bx-card--framed` e paginação com `.bx-arrows`. App: `.bx-appbar` com seta, lista de `.bx-card` com `.bx-avatar`, descrição centralizada e `.bx-card__footer` com botão cavalgando. A home de app com categorias é uma listagem em `.bx-ladder`, com saudação de peso misto e pergunta direta.

**C. Detalhe.** Galeria grande emoldurada à esquerda. À direita, `.bx-h2`, `.bx-price`, `.bx-data` (ÁREA, SUÍTES, VAGAS; ORÇAMENTO, METRAGEM) e CTA em bloco, num card de contato fixo que cavalga a borda da galeria. Abaixo: descrição, atributos, mapa, e "você também pode gostar" em grid emoldurado. No app, o card de resumo é recolhível e vem seguido do formulário de pedido (`.bx-input-action`, `.bx-radio` em grade, `.bx-btn--ink --block`).

**D. Institucional.** `.bx-page-header` e blocos alternados de texto e imagem emoldurada, com a imagem saindo da moldura em pelo menos um bloco. Números em `.bx-data` grande (ANOS, CLIENTES, PROJETOS) e equipe em `.bx-stage`. Vaga e serviço individual seguem a estrutura de Detalhe.

**E. Conversão.** Uma tarefa por tela. No site, formulário à esquerda com `.bx-field` e `.bx-row`, e resumo ou argumento à direita. No app, a mesma sequência empilhada. Etapas de fluxo (entrega, pagamento) em abas numeradas em caixa alta. Planos e preços: cards emoldurados lado a lado, com o recomendado em `--on-brand` e maior, cavalgando a linha dos outros. Login e cadastro no app usam fundo com overlay e campos brancos.

**F. Retorno e estado.** Fundo lavado ou neutro, círculo grande (`--success` na confirmação, `--brand` no vazio, `--ink` no erro) com ícone de linha grosso, título em caixa alta de 2-3 linhas, subtítulo com promessa concreta e uma ação. Se ajudar, uma dica com seta desenhada apontando para onde o usuário deve ir. No 404, o número pode virar palavra-objeto. Carregando: skeleton com blocos retos em `--surface-alt`, sem spinner decorativo.

**G. Área logada.** Header compacto (ou `.bx-appbar`), saudação de peso misto e resumo em `.bx-data`. Listas em `.bx-list-group` por categoria, com linha expandida mostrando `.bx-data` 2×2, `.bx-price` e CTA. Navegação principal em `.bx-tabbar` com `.bx-badge` no app, ou sidebar com itens em caixa alta e marcador de linha no site. Chat com balões de canto reto, os do usuário em `--ink` e os do outro lado em `--surface-alt`.

**H. Suporte e utilitário.** `.bx-page-header` enxuto, índice em `.bx-tabs` ou coluna lateral, FAQ em acordeão com cabeçalho em caixa alta e chevron de linha, texto corrido com `.bx-h3` e `.bx-lead`. Comparador: tabela com cabeçalho em `.bx-label` e células divididas por linha de 1px.

Frame de app de referência: 390×844 (ou 360×640), status bar escura, `.bx-appbar` de 56px, margem de 16px, alvos de pelo menos 44px.

## 4. Atualização para hoje

A gramática é de agência brasileira de 2015-2016. Mantenha a composição e atualize a execução:
- Layout fluido com CSS Grid e `clamp()`, sem larguras fixas.
- Mais respiro: grade de 8px e seções de 96-160px no desktop.
- Hero com tipografia maior e mais contraste.
- Acessibilidade: contraste AA, foco visível usando o próprio contorno (`outline` de 2px na cor da marca), alvos de 44px e `alt` nas imagens.
- `<picture>`/WebP, `loading="lazy"` abaixo da dobra.
- Movimento sutil onde fizer sentido: parallax leve entre camadas do hero, com `prefers-reduced-motion` respeitado.
- Fica de fora: sépia, textura de papel, sombra pesada, carrossel automático e texto fino cinza-claro.

---

## 5. Como usar

1. **Identifique a família da página** (seção 3.2), a plataforma (site ou app) e o nível de expressão. Num projeto com várias páginas, liste as páginas e a família de cada uma antes de desenhar.
2. **Confirme a marca:** cor principal, fonte e logo. Se faltar, pergunte. Derive `--ink` da marca.
3. **Comece pela folha de componentes** da seção 2, com o bloco de marca trocado. Em projetos com várias telas, gere um único `bitnix.css` (ou arquivo de tema em React) e reutilize em todas as telas para manter consistência.
4. **Monte pela receita da família** (seção 3.3). Escolha onde entra a quebra de grid e, se o contexto pedir, qual é o assunto recortado e o que o briefing oferece para ele.
5. **Entregue no formato pedido:**
   - **HTML/CSS:** arquivo(s) com a folha de componentes, Google Fonts e ícones via CDN.
   - **React:** componentes por peça (`Button`, `Field`, `FramedCard`, `DataPairs`, `SectionHead`, `AppBar`, `TabBar`, `Ladder`, `PageHeader`) consumindo o tema.
   - **Imagem estática:** construa em HTML e renderize com Playwright (desktop 1440×900, mobile 390×844 com `deviceScaleFactor: 2`, `fullPage: true` para página inteira), esperando `document.fonts.ready`.
6. **Renderize e confira** com o checklist. Olhe o screenshot de fato, porque sobreposição, corte e ritmo só se avaliam vendo.

Quando o pedido for o próprio design system (documentação, style guide, página de componentes), monte uma página com: tokens de cor gerados da marca, escala tipográfica, as três espessuras de linha, todos os componentes da seção 2 em seus estados (normal, hover, foco, selecionado, desabilitado, erro) e um exemplo por família.

## 6. Checklist

Em qualquer contexto:
- [ ] Grid base alinhado e rígido, com pelo menos uma quebra adequada ao contexto.
- [ ] Títulos, navegação, botões, abas e rótulos em caixa alta com tracking, e destaque por peso misto.
- [ ] Acabamento em linha (1/2/3px). Nada de sombra pesada, gradiente decorativo ou ícone preenchido.
- [ ] Cantos retos, com círculo só em avatar, botão de ícone, badge, radio e paginação.
- [ ] Cor: a marca em bloco chapado dominante, `--ink` de apoio e escada tonal para listas equivalentes.
- [ ] Componentes vindos da folha comum, sem estilos avulsos que fujam dela.
- [ ] CTAs de conversão em primeira pessoa (QUERO ME INSCREVER), nunca em imperativo de terceira pessoa.
- [ ] Responsivo, contraste AA e foco visível.

Por nível de expressão:
- [ ] Alto (Vitrine): o topo tem assunto recortado em camadas e cada seção tem uma quebra.
- [ ] Médio (Listagem, Detalhe, Institucional): header de marca com conteúdo subindo sobre ele, e sem pessoa se o briefing não pede.
- [ ] Funcional (Conversão, Estado, Área logada, Suporte): uma tarefa clara, micro-quebras (avatar, botão ou busca cavalgando), e expressão só no toque da família (forma gráfica no estado, card recomendado nos planos).

## 7. Evitar

Pessoa usada por padrão em toda tela, assunto preso dentro de caixa sem transbordar, grid "quebrado" sem grid claro por trás, títulos em sentence case, glassmorphism, gradientes coloridos, sombras flutuantes de SaaS, cantos muito arredondados, ícones preenchidos, ilustração genérica de banco, várias cores saturadas competindo, e componentes redesenhados a cada tela.