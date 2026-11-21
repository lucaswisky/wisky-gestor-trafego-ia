# Skill — Gestor de Tráfego com IA (Lucas Wisky)

> **Para a IA que vai executar:** este documento é a regra. Não simplifique, não adapte por conta própria e não invente nenhum número, nome ou texto. Se um dado estiver faltando, pergunte. Se uma regra aqui conflitar com um padrão genérico da Meta, esta regra vence.

## 0. Como o gestor trabalha com IA

- Os agentes executam o tráfego — criar, subir, ler e otimizar — a partir desta skill.
- O gestor passa ~30 minutos por dia olhando o tráfego. O resto do tempo é atenção ao cliente e decisão.
- O cliente paga pela execução e pelo resultado. Não precisa saber que é IA que executa.
- Gestão de tráfego não dá para fazer no chat comum: precisa de agente (Codex, Claude Code, Muse). Essa é a barreira de entrada.
- Venda real é o que decide: o pixel marca, mas só a venda confirmada (ex.: Ticto, status autorizado) confirma que o criativo vendeu.

## 1. Regras de ouro (valem para tudo abaixo)

1. **Nunca simplifique contagens.** Sempre com dois dígitos: `1>08>1`, nunca `1>8>1`; conjuntos e anúncios numerados `01, 02, 03...`.
2. **Nunca crie nada sem aprovação.** Apresente campanha, conjuntos, anúncios, verbas, copy e UTMs exatos e espere o "pode criar".
3. **Nunca prometa resultado.** Não prometa ROAS, vendas, CPA ou aprovação de anúncio.
4. **1 anúncio por conjunto, sempre, no teste.** Isolar a variável é o ponto do teste. O formato com 2 anúncios por conjunto (`1>4>2`) não é usado.
5. **Toda campanha que for rodar tem parâmetros de URL.** Nenhum anúncio fica sem UTM (ver seção 7).

## 2. Dados obrigatórios — pergunte se faltar qualquer um

- Preço do produto (ticket) em R$
- Quantidade de criativos e tipo: VD (vídeo), IMG (imagem) ou CAR (carrossel)
- Público: ABERTO ou interesse específico (ex.: "Interesse em mecânica")
- Headline completa + subheadline da página de vendas
- URL da página de vendas
- Pixel / conjunto de dados da conta
- Data de subida (formato DD/MM/AA)
- Número do teste (cada teste novo tem um número novo, nunca repetido)

## 3. Qual formato usar

| Formato | Estrutura | Quando usar |
|---|---|---|
| **ABO clássica** | 1 campanha, 4 ou 8 conjuntos (podendo ir a 16 ou 24), 1 anúncio por conjunto | Formato padrão de teste |
| **CBO Test** | 1 campanha, 1 conjunto, 4 a 6 criativos | Alternativa de teste em CBO |

- Número de conjuntos na ABO é **sempre par** (4, 8, 16, 24). É como fazer dois testes em um só.
- Pré-escala e escala usam o emoji 🏆, nunca número de teste (ver `docs/pre-escala.md`).

## 4. Nomenclatura exata

### ABO clássica

**Campanha:**
`{emoji do teste} {VD|IMG|CAR} [TESTE CRIATIVO - ABO 1>NN>1] [VENDA] [{público}] [ADV+] - {DD/MM/AA}`

**Conjunto:**
`{emoji do teste} {VD|IMG|CAR} [{NN} - {público}] [ABO - 1>NN>1] - {DD/MM/AA}`

**Anúncio:**
`{emoji do teste} {NN} - {nome do criativo} [ABO 1>NN>1 - TESTE DE CRIATIVO - {público}] - {DD/MM/AA}`

- O emoji é o número do teste: teste 1 → 1️⃣, teste 42 → 4️⃣2️⃣, teste 43 → 4️⃣3️⃣.
- Não corte o sufixo entre colchetes nem a data do anúncio. O nome curto (`4️⃣3️⃣ 01 - nome`) **não** é o padrão.
- **Empilhamento de nomes:** quando um criativo valida e vai para pré-escala/escala, o nome do anúncio acumula o histórico das campanhas por onde já rodou, para dar para saber o caminho dele só olhando o nome.

### CBO Test

Mesmo padrão, trocando o token de estrutura para `CBO 1>1>NN` (NN = número de criativos):

**Campanha:** `{emoji} VD [TESTE CRIATIVO - CBO 1>1>04] [VENDA] [ABERTO] [ADV+] - DD/MM/AA`
**Conjunto:** `{emoji} VD [01 - ABERTO] [CBO - 1>1>04] - DD/MM/AA`
**Anúncio:** `{emoji} 01 - Criativo 1 [CBO 1>1>04 - TESTE DE CRIATIVO - ABERTO] - DD/MM/AA`

Com 5 criativos → `CBO 1>1>05`; com 6 → `CBO 1>1>06`.

## 5. Verba — decidida pelo ticket, nunca chutada

### ABO clássica (verba por conjunto, por dia)

| Ticket do produto | Verba por conjunto/dia |
|---|---|
| Até R$50 | 1 ticket (ex.: produto R$50 → R$50/conjunto/dia) |
| Acima de R$70 | Meio ticket (ex.: produto R$70 → R$35/conjunto/dia) |
| R$51 a R$70 | **Vão intencional: não se vende nessa faixa.** Não interpole nenhuma verba aqui. |

### CBO Test (verba na campanha, por dia)

Verba da campanha = número de criativos × meio ticket.
Exemplo: ticket R$37 → meio ticket R$18,50 → 5 criativos = **R$92,50/dia** na campanha.

## 6. Configuração do conjunto

- **Conversão:** Local = Site · Meta de desempenho = Maximizar o número de conversões · Conjunto de dados = pixel da conta · Evento = Comprar · Atribuição = Padrão · Meta de custo por resultado = Nenhum.
- **Posicionamentos:** Advantage+, **mas removendo Audience Network e WhatsApp com exclusão de 100%**. Nunca marque a opção da Meta de permitir gasto limitado (até 5%) nesses posicionamentos excluídos. Motivo: geram muito clique, pouca conversão e pouco initiate checkout, distorcendo a leitura no Gerenciador.
- **Exceção:** em remarketing, avaliar caso a caso se faz sentido incluir — nunca é automático.

## 7. Configuração do anúncio

- **Destino:** principal = Site, com a URL da página de vendas. Em Destinos personalizados, tudo desativado: Otimizar destino do site, Product browsing e Complementos para navegador.
- **CTA:** sempre **"Ver detalhes"**. Nunca "Saiba mais" ou outro.
- **Configuração do criativo:** tudo desmarcado — Links de site, Resumos do site e Destaques do site (0/3).
- **Rastreamento:** Eventos do site marcado (pixel da conta), Eventos do app desmarcado, Eventos offline marcado (mesmo conjunto de dados).
- **Experiências interativas:** desativado (Revelar detalhes com o tempo desligado).
- **Aprimoramentos essenciais:** só 3 de 4 marcados — Comentários relevantes, Aprimorar CTA, Adicionar efeitos de vídeo. **Mostrar destaques: desmarcado.**
- **Aprimoramentos Advantage+:** tudo desativado — Retoques de vídeo, Melhorias no texto, Adicionar detalhes ao anúncio, Mostrar destaques.
- **Geração de criativo Advantage+:** não selecionar nada, não adicionar nenhum criativo gerado por imagem de IA.
- **Parâmetros de URL (sempre, sem `?` no início):**

`utm_source=meta&utm_campaign={{campaign.name}}|{{campaign.id}}&utm_medium={{adset.name}}|{{adset.id}}&utm_content={{ad.name}}|{{ad.id}}&utm_term={{placement}}_{{site_source_name}}`

Mapeamento: source = rede (Meta) · campaign = nome + ID da campanha · medium = nome + ID do conjunto · content = nome + ID do anúncio · term = posicionamento + rede social. Nome e ID separados por `|`.

## 8. Copy do anúncio (universal, vale para qualquer projeto)

- **Título:** headline da página de vendas resumida em no máximo 8 palavras.
- **Texto principal:** headline completa da página + subheadline, sem inventar nada. Não usa o gancho de cada vídeo — segue a página.
- **Descrição:** sempre `⭐️⭐️⭐️⭐️⭐️ (4.9/5.0) Avaliações`

## 9. Leitura do teste e pós-teste

- **Leitura:** um criativo é promissor quando CPA < 45% do ticket e ROAS > 2.
- **Pós-teste:** pausar todos os conjuntos que **não venderam**. Nos que venderam, **+20% de verba a cada 24h** enquanto continuar vendendo — escalar dentro do próprio teste preserva o aprendizado da Meta, em vez de duplicar para outra campanha.
- **Regra "voltar 2 casas":** conjunto que vendeu mas não bateu ROAS 1 volta 2 casas na escada de verba (dois aumentos para trás). Exemplo: escada 37 → 44,40 → 53,28 → 63,94; de 63,94 volta para **R$44,40/dia**. Conjunto que não vendeu é pausado, não volta casas.
- **Regra de pausa do CBO (universal):** num teste CBO, o criativo que gastar 1 ticket desde o início do teste sem vender é pausado — a pausa pode ser feita sozinha, sem pedir aprovação caso a caso, quando bater o limite. A confirmação de venda real é o que decide; silêncio do pixel sozinho não basta para pausar se a venda real ainda não foi conferida.
- **Atenção operacional:** editar a verba pausa o conjunto automaticamente — reativar após a edição e conferir que voltou a rodar com a verba nova. Ao publicar, conferir os 3 níveis (campanha + conjuntos + anúncios) ativos, não só a campanha.
- **Heurística de escala:** nas projeções, o ROAS cai de 2 para 1,5 quando a verba diária passa de R$ 1.000–1.200 — o gatilho é o nível de verba, não o tempo.

## 10. Pré-escala — só referência aqui

Ver `docs/pre-escala.md`. Resumo: só entra na pré-escala quem **vendeu no teste**. A campanha usa o emoji **🏆**, nunca número de teste. O nome do anúncio empilha o histórico. O formato e a verba exata de entrada **não são fórmula fechada** — já apareceu em ABO e em CBO. Pergunte antes de montar; nunca assuma um dos dois.

## 11. Exemplo completo preenchido (exemplo — não copiar os dados)

Teste ABO, ticket R$37, 8 criativos em vídeo, público ABERTO, subida em 07/10/26:

- **Campanha:** `4️⃣3️⃣ VD [TESTE CRIATIVO - ABO 1>08>1] [VENDA] [ABERTO] [ADV+] - 07/10/26`
- **Conjuntos (01 a 08):** `4️⃣3️⃣ VD [01 - ABERTO] [ABO - 1>08>1] - 07/10/26`
- **Anúncios:** `4️⃣3️⃣ 01 - {nome do criativo} [ABO 1>08>1 - TESTE DE CRIATIVO - ABERTO] - 07/10/26`
- **Verba:** R$37/conjunto/dia (1 ticket, pois R$37 ≤ R$50) → R$296/dia no total.

## 12. O que a IA nunca faz com este padrão

- Simplificar `1>08>1` para `1>8>1`, cortar sufixo de nome ou data.
- Criar 2 anúncios por conjunto, ou número ímpar de conjuntos na ABO.
- Inventar verba para ticket entre R$51 e R$70.
- Deixar anúncio sem UTM, usar "Saiba mais", ligar Advantage+ ou criativo gerado por IA.
- Criar ou publicar sem o plano exato aprovado.
- Prometer ROAS, vendas, CPA ou aprovação de anúncio.
