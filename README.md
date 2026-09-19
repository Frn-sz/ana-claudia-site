# Site — Ana Claudia Medeiros, psicóloga clínica

Landing page estática. HTML e CSS puros, sem framework e sem build: o que está
aqui é exatamente o que vai para o ar.

## Rodar local

```bash
python3 -m http.server 4173
```

**Trocou uma imagem sem trocar o nome do arquivo?** Recarregue furando o cache
(`Ctrl+Shift+R`). O `http.server` manda só `Last-Modified`, sem `Cache-Control`
nem `ETag`, então o navegador aplica cache heurístico e nem chega a perguntar se
o arquivo mudou — continua desenhando o que baixou antes. O servidor está certo;
quem está desatualizado é a aba.

## Imagens

Não há mais placeholder: as duas fotos estão no lugar e o card de atendimento
online é ilustração, não foto.

| Onde | O que é |
| --- | --- |
| `assets/img/ana-sobre.jpg` | Retrato da Ana, 1003×1254, recorte 4:5 do quadrado que ela mandou |
| `assets/img/presencial.jpg` | Consultório, 1600×1200, o 4:3 exato do card |
| `assets/img/og.jpg` | Cartão de compartilhamento, 1200×630. Não aparece no site: é o que o WhatsApp desenha quando alguém cola o link |
| Card "Atendimento online" | Ilustração inline, irmã da seção "Um espaço para você": os mesmos arcos, mais afastados |

O `og.jpg` repete o primeiro quadro: marca, nome, "Psicóloga clínica", CRP e a
linha de atendimento, com o retrato à direita. Ele é uma imagem chapada, então
não se atualiza sozinho — **mudou o texto do topo, refaça o cartão**, senão o
link compartilhado passa a anunciar uma versão do site que não existe mais.

As duas fotos vieram do WhatsApp e chegaram por e-mail no mesmo estado: a do
consultório é o mesmo arquivo, byte a byte (qualidade 50), e a dela é a mesma
imagem 1254×1254 reembalada em PNG sem perda — não são os originais da câmera.
Servem, mas se um dia aparecerem os arquivos originais valem a troca.

**Ao pedir foto:** enviar como *documento* no WhatsApp, não como foto — como
foto o app recomprime e devolve o mesmo problema de qualidade. Por e-mail,
anexar o arquivo original, não o que já passou pelo WhatsApp.

## Decisões que não são gosto

- **Cores.** Três rampas geradas em OKLCH a partir das cores reais da marca:
  neutro quente (H 75), verde `#105733` (H 155.6) e argila (H 50), esta última
  vinda das imagens de referência que a Ana mandou. Escritas em hex porque hex
  tem suporte universal. A argila só é consumida pelas ilustrações — nenhum
  texto, nenhum controle — e seus dois passos claros repetem a luminosidade de
  `--a-3` e `--a-5`, então as formas verdes e as de argila pesam igual na
  composição. Todos os pares de contraste com texto foram medidos em APCA e
  WCAG 2 AA.
- **Ilustrações no lugar de fotos.** A Ana pediu topo abstrato e a foto dela
  só no "Sobre". As ilustrações são SVG inline: leem os tokens de cor da
  página, escalam sem perda e são `aria-hidden`, porque são decorativas. A
  geometria (formas orgânicas, ondas, a marca de quatro laços) foi gerada por
  script, não desenhada à mão — refazer é mudar um número e rodar de novo.
- **Logo vetorial.** Marca (`<use>` de um símbolo) mais o nome em texto de
  verdade, na mesma serifada dos títulos. Substitui o PNG com a folha verde,
  que a Ana pediu para trocar por linhas abstratas. Fica nítido em qualquer
  tamanho e o nome continua selecionável, traduzível e legível por leitor de
  tela; abaixo de 26rem ele some da tela mas continua no acessível, senão o
  link do logo ficaria sem nome nenhum.
- **Tipografia.** Playfair Display nos títulos porque o logo é serifado; Inter no
  corpo pela legibilidade. As duas auto-hospedadas em `assets/fonts/`: nenhuma
  requisição ao Google, o que também evita expor o IP de quem visita um site de
  saúde.
- **Animação de entrada.** O conteúdo é visível por padrão. A classe `.js`, que
  só existe se o script rodou, é o que autoriza escondê-lo para animar. É o
  sentido oposto ao do site do Wix, onde uma animação que não disparava deixava
  a seção em branco.
- **Sem breakpoints de dispositivo.** As grades usam `auto-fit` + `minmax`, então
  adaptam pelo espaço disponível. Os três breakpoints que existem (58rem, 56rem
  e 52rem) foram escolhidos onde o conteúdo para de caber, não em 768/1024.

## Correções em relação ao site do Wix

- Os 4 links de WhatsApp que apontavam para o número quebrado `555581329397`
  agora usam o número correto, `5554991697043`, com mensagem pré-preenchida.
- Os três "Saiba mais" iam todos para o WhatsApp sem dizer isso. Foram removidos:
  os CTAs ficaram nos cards de modalidade, com rótulos que descrevem o destino.
- O texto do "Sobre" trocava de pessoa no meio ("Sou psicóloga… Atende crianças").
  Está em primeira pessoa do começo ao fim.
- O mapa era um print do Google Maps. Saiu: um print não arrasta, não traça
  rota e envelhece sem ninguém perceber. A seção agora é endereço escrito mais
  link para o Maps, que foi o que a Ana pediu.

## Textos e mudanças pedidas pela Ana (08/09/2026)

Os textos das seções "Um espaço para você", "Meu jeito de trabalhar" e
"Orientação profissional e de carreira" são dela, na íntegra. Além deles:

- Topo sem a linha "Psicologia clínica em Caxias do Sul": começa no nome,
  seguido de "Psicóloga clínica" e do CRP.
- "Atendimento para crianças, adolescentes e adultos" ganhou corpo maior — foi
  pedido explícito, é a linha que responde se o atendimento serve para quem lê.
- Adolescentes incluídos em todos os lugares onde faltavam.
- Seção "Avaliação psicológica" removida: ela não trabalha com isso de forma
  geral, só para orientação e pesquisa.
- "Onde fica o consultório" virou "Endereço".
- A folha verde ao lado do nome virou uma marca de quatro laços abertos.

## Segunda rodada (16/09/2026)

A Ana pediu um site "só pra saberem que eu existo, sem apelação". Eram cinco
botões de WhatsApp na página; ficaram três, e cada um diz uma coisa diferente:
o "Agendar" do cabeçalho, que acompanha a rolagem, e os dois dos cards de
modalidade, que já chegam com a mensagem de presencial ou de online.

- Topo sem botões: saiu o "Conhecer o trabalho", a pedido dela, e com ele o
  "Agendar pelo WhatsApp", que repetia o "Agendar" do cabeçalho na mesma tela.
- "Como acontece o atendimento" sem título nem frase de abertura: a seção
  começa direto na foto do consultório. O título continua para leitor de tela.
- Atendimento online "para as demais regiões do país e exterior".
- Chamada final ("Vamos conversar") removida, com o botão dela.

## Antes de lançar de verdade

O site está publicado como **prévia** e propositalmente fora do Google. Para
lançar, os quatro passos abaixo são um pacote: fazer um sem o outro deixa o
site inconsistente ou invisível.

1. **Abrir para o Google.** Remover `<meta name="robots" content="noindex,
   nofollow">` do `index.html` **e** trocar o `Disallow: /` do `robots.txt`
   por `Allow: /`. Um sem o outro não adianta.
2. **Trocar o domínio nos 8 lugares.** Seis no `index.html` (canonical,
   `og:url`, `og:image` e, no JSON-LD, `@id`, `url`, `image`), um no
   `sitemap.xml` e um no `robots.txt`. Conferir com:
   ```bash
   grep -rn "frn-sz.github.io" index.html sitemap.xml robots.txt
   ```
   Tem que não achar nada depois da troca. O comando mora aqui, e não num
   comentário dentro do `index.html`, porque lá ele se encontraria e a
   conferência nunca fecharia. Criar também o arquivo `CNAME` com o
   domínio e apontar o DNS (apex nos IPs do GitHub Pages, `www` por CNAME
   para `frn-sz.github.io`).
3. **Tirar o site do Wix do ar.** Ele está indexável: `robots.txt` liberado,
   sem `noindex`, com canonical próprio. Se ficar no ar, passam a existir duas
   páginas com o mesmo nome, telefone e endereço competindo entre si. A conta
   é do dev que sumiu, mas o plano é da Ana — dá para despublicar por lá.
4. **Registrar no Search Console** e enviar o `sitemap.xml`.

## O que falta nos dados estruturados

Deixei de fora o que eu não sabia — inventar dado em `schema.org` é pior que
omitir, porque o Google cruza com a ficha do Maps e a divergência derruba a
confiança nos dois. Perguntar para a Ana e preencher:

| Campo | O que é |
| --- | --- |
| `openingHours` | Horário de atendimento |
| `sameAs` | Instagram e qualquer outro perfil profissional |
| `email` | E-mail de contato, se ela quiser publicar |
| `priceRange` | Faixa de preço (opcional, `$$` já serve) |

## Publicar no GitHub Pages

1. `git init` e primeiro commit (assinado).
2. Repositório no GitHub, `git push`.
3. Settings → Pages → Source: `main`, pasta `/` (raiz).
4. Domínio próprio: criar `CNAME` com o domínio, e no DNS apontar o apex para os
   IPs do GitHub Pages e `www` via CNAME para `<usuario>.github.io`.
