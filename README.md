# Dennis Caceta Consultoria — Site (redesign)

Site institucional em 6 páginas para a Dennis Caceta Consultoria em Gestão
Empresarial, construído como HTML estático (sem build, sem dependências de
servidor). Cada página é um arquivo autônomo — CSS e JS embutidos — para que
possam ser abertas direto no navegador ou hospedadas em qualquer serviço
estático (GitHub Pages, Netlify, Vercel, cPanel, etc.).

## Arquivos

```
index.html      Início — hero, diagnóstico, teasers de todas as seções
servicos.html   As 11 frentes de atuação + processo de 4 etapas
projetos.html   Diário de bordo com os 5 estudos de caso + dashboards
sobre.html      Perfil de Dennis Caceta + missão, visão e valores
pesquisa.html   52 artigos técnicos, publicações selecionadas e imprensa
contato.html    Canais diretos + brief rápido (abre e-mail preenchido)
```

Não há pasta `assets/`: fontes vêm do Google Fonts via `<link>` e todo o
resto (CSS, SVG do radar, JavaScript) está dentro do próprio `<head>`/`<body>`
de cada arquivo. Isso significa que **cada página pode ser copiada
isoladamente** e continuará funcionando.

## Como publicar

**Opção rápida (sem código):** arraste os 6 arquivos `.html` para qualquer
hospedagem estática (Netlify, Vercel, GitHub Pages, Cloudflare Pages) e
aponte o domínio para `index.html`.

**Hospedagem tradicional (cPanel/FTP):** envie os 6 arquivos para a raiz do
`public_html`. Não é necessário PHP, banco de dados ou build — são páginas
estáticas.

**Teste local:** basta abrir `index.html` duas vezes no navegador (duplo
clique) ou rodar um servidor simples, por exemplo:

```bash
python3 -m http.server 8000
# depois acesse http://localhost:8000
```

## Conceito de design

- **Direção:** sala de controle de terminal portuário à noite — grade de
  coordenadas náuticas no fundo, radar animado no topo de cada página
  (referência direta ao produto real "Radar COMEX & Logística").
- **Paleta:** tinta naval (`#0A1720` / `#0F1F29`), âmbar de sinalização
  (`#E38B29`, usado nos CTAs) e verde-radar (`#52C7B8`, usado em dados e
  links). Texto secundário em névoa (`#9FADB6`).
- **Tipografia:**
  - `Big Shoulders Display` — títulos (condensada, industrial)
  - `IBM Plex Sans` — corpo de texto
  - `IBM Plex Mono` — dados, códigos, timestamps, rótulos
- **Componentes recorrentes** (reaproveitados entre páginas via as mesmas
  classes CSS):
  - `.manifest` — lista de "sinais de alerta" em formato de manifesto de carga
  - `.yard` / `.block` — grade de serviços em formato de pátio de contêineres
  - `.log` / `.log-entry` — estudos de caso em formato de diário de bordo,
    com código de terminal (`BR-STS`, `BR-SSA`, `BR-ITQ`)
  - `.timeline` / `.step` — processo em 4 etapas (única numeração 01→04 do
    site, porque aqui é uma sequência real)
  - `.compass` / `.compass-card` — missão, visão e valores
  - `.dash-strip` / `.dash-card` — links para os dashboards Power BI
  - `.channels` / `.channel` — canais de contato (contato.html)
  - `.quick-form` — brief rápido que monta um `mailto:` preenchido

## Navegação e estado ativo

O menu superior é idêntico em todas as páginas; o link da página atual
recebe a classe `.active` (sublinhado em verde-radar). Para adicionar uma
nova página ao menu, edite o bloco `<nav class="links">` em **todos os
arquivos** (não há template compartilhado em tempo de execução — veja a
seção "Manutenção" abaixo).

## Como editar conteúdo

Cada página é HTML simples dividido em `<section>`. Para editar um texto,
procure o bloco correspondente:

- Frases de efeito e números do topo → `<section class="hero">` ou
  `<section class="page-hero">`
- Cards de serviço → `<div class="block">…</div>` dentro de `.yard`
- Estudos de caso → `<div class="log-entry">…</div>` dentro de `.log`
- Perfil → `<div class="profile">…</div>` em `sobre.html`

Números de telefone/WhatsApp aparecem como `https://wa.me/5513997492941` e
`tel:+5513997492941`; o e-mail é `contato@denniscaceta.com`. Ambos se
repetem em vários arquivos — use busca e substituição no editor de texto
para trocá-los de uma vez.

## Manutenção (regenerar as páginas via script)

O site foi gerado a partir de um único script Python
(`build_site.py`, não incluído neste pacote de entrega) que centraliza o
CSS, o cabeçalho, o rodapé e o script de rodapé, e monta cada página a
partir de um bloco de conteúdo próprio. Isso evitou duplicar ~250 linhas de
CSS seis vezes e manteve todas as páginas visualmente idênticas.

Se você (ou outro desenvolvedor) for manter o site no longo prazo, duas
rotas fazem sentido:

1. **Manter como está** — 6 arquivos HTML independentes, edição manual.
   Mais simples, zero dependências, mas qualquer mudança de design precisa
   ser repetida em 6 arquivos.
2. **Migrar para um gerador de site estático** (Astro, Eleventy, Hugo) ou
   para React/Next — reaproveitando o CSS deste projeto como ponto de
   partida — se o site crescer (novo projeto por mês, blog, etc.) e a
   edição manual em 6 arquivos deixar de compensar.

## Acessibilidade e performance

- Todo o site respeita `prefers-reduced-motion` (animações do radar e do
  scroll-reveal são desativadas automaticamente).
- Foco de teclado visível em todos os links e botões (`:focus-visible`).
- Sem imagens pesadas — o radar é SVG inline, então não há requisições de
  imagem além das fontes do Google Fonts.
- Menu mobile (`☰`) abaixo de 860px de largura.

## Itens para revisar antes de publicar

- [ ] Confirmar se `contato@denniscaceta.com` é o e-mail correto em uso.
- [ ] Confirmar número de WhatsApp/telefone `(13) 99749-2941`.
- [ ] Substituir os links de imprensa/anais por URLs atualizadas, caso
      algum conteúdo tenha saído do ar.
- [ ] Adicionar Google Analytics / Meta Pixel, se necessário (não incluído
      por padrão).
- [ ] Revisar textos de case studies com o cliente antes de publicar
      números de produtividade e capacidade.
