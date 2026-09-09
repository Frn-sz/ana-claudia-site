# Site — Ana Claudia Medeiros, psicóloga clínica

Landing page estática. HTML e CSS puros, sem framework e sem build: o que está
aqui é exatamente o que vai para o ar.

## Rodar local

```bash
python3 -m http.server 4173
```

## O que ainda é placeholder

| Arquivo | Substituir por | Observação |
| --- | --- | --- |
| `assets/img/ana-sobre.jpg` | Foto da Ana, mínimo 1000×1250 | A única foto dela no site: ela pediu foto só no "Sobre", e ilustração no topo |
| `assets/img/presencial.jpg` | Foto real do consultório | 4:3, mínimo 1200×900. Ela já mandou uma (1600×1200), mas comprimida pelo WhatsApp |
| `assets/img/online.jpg` | Imagem de atendimento online | 4:3, mínimo 1200×900 |

**Ao pedir as fotos:** enviar como *documento* no WhatsApp, não como foto — como
foto o app recomprime para ~1600px e devolve o mesmo problema de qualidade.

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

## Antes de lançar de verdade

O site está publicado como **prévia** e propositalmente fora do Google:

- `<meta name="robots" content="noindex, nofollow">` em `index.html`
- `robots.txt` com `Disallow: /`

Remover os dois no dia do lançamento. Enquanto o site do Wix estiver no ar,
manter os dois evita que as duas versões concorram na busca e que um paciente
caia na página com imagens de placeholder.

## Publicar no GitHub Pages

1. `git init` e primeiro commit (assinado).
2. Repositório no GitHub, `git push`.
3. Settings → Pages → Source: `main`, pasta `/` (raiz).
4. Domínio próprio: criar `CNAME` com o domínio, e no DNS apontar o apex para os
   IPs do GitHub Pages e `www` via CNAME para `<usuario>.github.io`.
