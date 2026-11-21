# Padrão de criação de campanha de TESTE DE CRIATIVO — Lucas Wisky

Versão completa do padrão, extraída das aulas e confirmada com o Lucas em 2026-10-26/27. A versão resumida e executável está no `SKILL.md` da raiz.

## Nomenclatura

### Campanha
`{emoji-número} {VD|IMG|CAR} [TESTE CRIATIVO - ABO {1>N>1}] [VENDA] [{público}] [ADV+] - {DD/MM/AA}`

Exemplo real: `4️⃣2️⃣ VD [TESTE CRIATIVO - ABO 1>09>1] [VENDA] [ABERTO] [ADV+] - 22/09/26`

Regras:
- **Emoji com número = número do teste.** Todo teste novo troca o emoji: teste 1 → 1️⃣, teste 42 → 4️⃣2️⃣, próximo → 4️⃣3️⃣.
- **Número é exclusivo de teste de criativo.** Campanha de pré-escala/escala usa emoji de troféu 🏆, nunca número.
- Tipo de mídia: VD (vídeo), IMG (imagem), CAR (carrossel).
- Modelo de otimização declarado no nome: ABO ou CBO.
- Estrutura declarada: 1>4>1, 1>8>1, 1>16>1 etc.
- Objetivo: [VENDA]. Público: [ABERTO] ou [Interesse em X]. Posicionamentos: [ADV+].
- Data de subida no formato DD/MM/AA.

### Conjunto de anúncios
`{tipo de mídia} {número do conjunto} {público} {modelo} {estrutura} - {data}`
Formato observado na conta: `4️⃣2️⃣ VD [01 - ABERTO] [ABO - 1>09>1] - 22/09/26`

### Anúncio
`{emoji-número} {0N} - {nome do criativo} [ABO {1>NN>1} - TESTE DE CRIATIVO - {público}] - {data}`
Exemplo real (teste 43, confirmado em 2026-10-25): `4️⃣3️⃣ 01 - {nome do criativo} [ABO 1>08>1 - TESTE DE CRIATIVO - ABERTO] - 07/10/26`
- Não cortar o sufixo entre colchetes nem a data — o nome curto (`{emoji} {0N} - {nome}`) NÃO é o padrão.
- O anúncio carrega o emoji do teste (campanha 42 → anúncio com emoji 42).
- **Empilhamento de nomes:** quando o criativo valida e vai pra pré-escala/escala, o nome do anúncio acumula o histórico, de modo que olhando o anúncio dá pra saber por quais campanhas ele já rodou.
- O nome do arquivo no Google Drive segue o mesmo padrão (com emoji) pra equipe achar o criativo pelo nome.

## Estrutura ABO (analogia: dono > líderes > vendedores)
- **1>4>1** = 1 campanha, 4 conjuntos, 1 anúncio por conjunto (padrão com pouca verba).
- **1>8>1** = mesma coisa com 8 conjuntos.
- Com mais verba: **1>16>1**. Caso extremo ("preciso achar um garanhão"): **1>24>1**.
- **Sempre número par de conjuntos** (8 ou 16 — "como se estivesse fazendo dois testes de um só").
- **1 anúncio por conjunto, sempre isolado.** Cada anúncio recebe sua verba e "se vira pra trazer venda. Se não trouxe venda é porque é incompetente. Joga fora e vida que segue." O formato 1>4>2 (2 anúncios por conjunto) não é usado mais, pra isolar a variável ao máximo.

## Regra do ticket (verba por conjunto/dia) — ABO clássica
- **Ticket até R$50: 1 ticket por criativo/conjunto por dia.** Produto de R$50 → R$50/conjunto/dia (1>4>1 = R$200/dia).
- **Ticket acima de R$70: meio ticket por criativo/conjunto por dia** (produto R$70 → R$35/conjunto).
- Faixa R$51–R$70: vão intencional — não se vende neste ticket, por isso não há regra para essa faixa.

## CBO Test — Teste de criativo em CBO
- **Estrutura:** 1 campanha, 1 conjunto de anúncios, 4 a 6 criativos.
- **Verba:** meio ticket do produto por criativo, somada no nível da campanha (CBO).
  - Ex.: 5 criativos → verba da campanha = 5 × meio ticket.
  - Ex. com ticket R$37: meio ticket R$18,50 → 5 criativos = R$92,50/dia na campanha.
- **Nomenclatura:** segue o mesmo padrão da ABO clássica, trocando o token de estrutura de `ABO 1>04>01` para `CBO 1>1>04` (exemplo com 4 criativos; com 5 → `CBO 1>1>05`, com 6 → `CBO 1>1>06`).
  - Campanha: `{emoji} VD [TESTE CRIATIVO - CBO 1>1>04] [VENDA] [ABERTO] [ADV+] - DD/MM/AA`
  - Conjunto: `{emoji} VD [01 - ABERTO] [CBO - 1>1>04] - DD/MM/AA`
  - Anúncio: `{emoji} 01 - Criativo 1 [CBO 1>1>04 - TESTE DE CRIATIVO - ABERTO] - DD/MM/AA`

## Configuração — regras universais (valem para teste e pré-escala)

- **Conversão:** Local = Site; Meta de desempenho = Maximizar o número de conversões; Conjunto de dados = pixel da conta; Evento = Comprar; Atribuição = Padrão; Meta de custo por resultado = Nenhum.
- **Posicionamentos:** remover Audience Network e WhatsApp com exclusão de 100%. Não marcar a opção de permitir gasto limitado (até 5%). Exceção: remarketing, avaliar caso a caso.
- **Destino:** principal = Site, com a URL da página de vendas. Destinos personalizados, tudo desativado.
- **CTA:** sempre "Ver detalhes".
- **Configuração do criativo:** tudo desmarcado (Links, Resumos e Destaques do site, 0/3).
- **Rastreamento:** Eventos do site marcado (pixel da conta), Eventos do app desmarcado, Eventos offline marcado.
- **Experiências interativas:** desativado.
- **Aprimoramentos essenciais:** só 3 de 4 — Comentários relevantes, Aprimorar CTA, Adicionar efeitos de vídeo. Mostrar destaques: desmarcado.
- **Aprimoramentos Advantage+:** tudo desativado. **Geração de criativo Advantage+:** não selecionar nada, nenhum criativo gerado por imagem de IA.

## Parâmetros de URL (UTMs dinâmicas)

String padrão (campo "Parâmetros de URL" do anúncio, sem `?` no início):

`utm_source=meta&utm_campaign={{campaign.name}}|{{campaign.id}}&utm_medium={{adset.name}}|{{adset.id}}&utm_content={{ad.name}}|{{ad.id}}&utm_term={{placement}}_{{site_source_name}}`

Mapeamento: utm_source = rede (valor fixo "meta") · utm_campaign = nome + ID da campanha · utm_medium = nome + ID do conjunto · utm_content = nome + ID do anúncio/criativo · utm_term = posicionamento + rede social. Nome e ID separados por `|` (pipe).

## Copy do anúncio (universal)

- **Título:** headline da página de vendas resumida em no máximo 8 palavras.
- **Texto principal:** headline completa da página + subheadline, sem inventar nada.
- **Descrição:** sempre `⭐️⭐️⭐️⭐️⭐️ (4.9/5.0) Avaliações`
- Título e descrição fixos no teste; o texto principal segue a página, não o gancho de cada vídeo.

## Métricas de leitura

- CPA abaixo de **45% do valor do ticket**.
- ROAS acima de **2**.

## Pós-teste

- Pausa todos os conjuntos que **não venderam**.
- Nos que venderam: **+20% de verba a cada 24h** enquanto continuar vendendo.
- **Regra "voltar 2 casas":** conjunto que **vendeu mas não bateu ROAS 1** volta **2 casas** na escada de verba (ex.: escada 37 → 44,40 → 53,28 → 63,94; de 63,94 volta para **R$44,40/dia**). Conjunto que **não vendeu** é pausado, não volta casas.
- Editar a verba **pausa o conjunto automaticamente** — reativar o conjunto após a edição e conferir que voltou a rodar com a verba nova.
