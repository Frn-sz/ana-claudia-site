# Site — Ana Claudia Medeiros, psicóloga clínica

Landing page estática. HTML e CSS puros, sem framework e sem build: o que está
aqui é exatamente o que vai para o ar.

## Rodar local

```bash
python3 -m http.server 4173 --directory site
```

## O que ainda é placeholder

| Arquivo | Substituir por | Observação |
| --- | --- | --- |
| `assets/img/ana-hero.jpg` | Foto vertical da Ana, mínimo 1200×1500 | O original do site antigo tinha só 795×787 — pequeno demais |
| `assets/img/ana-sobre.jpg` | Segunda foto, diferente da do hero | Mínimo 1000×1250 |
| `assets/img/presencial.jpg` | Foto real do consultório | 4:3, mínimo 1200×900 |
| `assets/img/online.jpg` | Imagem de atendimento online | 4:3, mínimo 1200×900 |
| `assets/img/mapa.png` | Mapa próprio | Hoje é um print do Google Maps herdado do site antigo |
| `assets/img/logo.png` | Versão vetorial (`.svg`) | O PNG serve, mas vetor fica nítido em qualquer tamanho |

**Ao pedir as fotos:** enviar como *documento* no WhatsApp, não como foto — como
foto o app recomprime para ~1600px e devolve o mesmo problema de qualidade.

## Decisões que não são gosto

- **Cores.** Duas rampas de 12 passos geradas em OKLCH a partir das cores reais
  da marca (verde `#105733`, neutro quente). Escritas em hex porque hex tem
  suporte universal. Os 11 pares de contraste usados na página foram medidos em
  APCA e WCAG 2 AA — todos passam.
- **Tipografia.** Playfair Display nos títulos porque o logo é serifado; Inter no
  corpo pela legibilidade. As duas auto-hospedadas em `assets/fonts/`: nenhuma
  requisição ao Google, o que também evita expor o IP de quem visita um site de
  saúde.
- **Animação de entrada.** O conteúdo é visível por padrão. A classe `.js`, que
  só existe se o script rodou, é o que autoriza escondê-lo para animar. É o
  sentido oposto ao do site do Wix, onde uma animação que não disparava deixava
  a seção em branco.
- **Sem breakpoints de dispositivo.** As grades usam `auto-fit` + `minmax`, então
  adaptam pelo espaço disponível. Os dois breakpoints que existem (58rem e 52rem)
  foram escolhidos onde o conteúdo para de caber, não em 768/1024.

## Correções em relação ao site do Wix

- Os 4 links de WhatsApp que apontavam para o número quebrado `555581329397`
  agora usam o número correto, `5554991697043`, com mensagem pré-preenchida.
- Os três "Saiba mais" iam todos para o WhatsApp sem dizer isso. Foram removidos:
  os cards de especialidade agora são informativos, e os CTAs ficaram nos cards
  de modalidade, com rótulos que descrevem o destino.
- O texto do "Sobre" trocava de pessoa no meio ("Sou psicóloga… Atende crianças").
  Está em primeira pessoa do começo ao fim.

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
3. Settings → Pages → Source: `main`, pasta `/site` (ou mover o conteúdo para a
   raiz e usar `/`).
4. Domínio próprio: criar `CNAME` com o domínio, e no DNS apontar o apex para os
   IPs do GitHub Pages e `www` via CNAME para `<usuario>.github.io`.
