---
name: straight-to-the-point
description: Escreve, reescreve ou revisa mensagens no formato BLUF (Bottom Line Up Front): e-mail, Slack, status, pedido de aprovação, incidente ou proposta para chefe e stakeholders.
---

# Straight to the point — BLUF (Bottom Line Up Front)

Técnica de escrita do Exército dos EUA (AR 25-50 e DA PAM 600-67). Duas regras centrais:
1. **O ponto principal vem primeiro** (pedido, decisão, conclusão ou motivo da mensagem).
2. **Voz ativa** (quem faz o quê: "Eu adiei o deploy", não "O deploy foi adiado").

Teste de ouro: **se o leitor parar na primeira frase, ele sabe o que está acontecendo e o que precisa fazer?** Se não, reescreva.

Responda no idioma do usuário (padrão: português do Brasil), com frases curtas e palavras do dia a dia.

## Quando usar esta skill

- O usuário pede para escrever ou melhorar uma mensagem para chefe, gestor, diretoria, cliente ou outro time.
- E-mail, mensagem de Slack/Teams, status report, pedido de aprovação, aviso de atraso, relato de incidente, pedido de ajuda, proposta técnica, resumo de ADR.
- O usuário pede para "ir direto ao ponto", "deixar mais objetivo" ou cita BLUF.

## Modos de trabalho

Identifique o modo pelo pedido:

- **Escrever do zero:** o usuário descreve a situação. Se faltar o essencial (o que ele quer do leitor, prazo), pergunte só isso, em uma pergunta. Senão, escreva direto.
- **Reescrever:** o usuário cola um texto. Entregue a versão BLUF pronta para copiar.
- **Revisar:** o usuário pede feedback. Aponte em até 3 tópicos o que quebra o BLUF e entregue a versão corrigida.

Sempre entregue o texto final dentro de um bloco de código para copiar. Fora do bloco, no máximo 2 linhas explicando a principal mudança.

## Passo a passo

1. **Ache o bottom line.** Pergunte: "Se eu só pudesse mandar uma frase, qual seria?" Normalmente é um destes:
   - um pedido ("Preciso que você aprove X até sexta")
   - uma decisão tomada ("Vamos usar fila em vez de chamada direta")
   - um fato que muda algo ("A entrega atrasa 2 dias")
   - uma informação sem ação ("Só para seu conhecimento: o deploy de ontem foi concluído sem erros")
2. **Escreva o BLUF em 1 ou 2 frases.** Deve responder: o quê, quem, até quando e por quê (só o essencial).
3. **Deixe claro o tipo de resposta esperada.** Ação, aprovação, só leitura.
4. **Contexto depois, em tópicos curtos.** Só o que sustenta o BLUF. Corte histórico cronológico, esforço feito e detalhes que o leitor não usa para decidir.
5. **Feche com o próximo passo.** Quem faz o quê e quando.
6. **Um assunto por mensagem.** Se houver dois assuntos independentes, sugira duas mensagens.

## Estrutura padrão

```
[ETIQUETA] Assunto que já diz o ponto

<BLUF: 1–2 frases com o pedido/decisão/fato e o prazo>

Contexto:
- <fato 1 que sustenta>
- <fato 2>
- <risco ou alternativa, se houver>

Próximo passo: <quem faz o quê e quando>
```

### Etiquetas no assunto (e-mail) ou no começo (Slack)

Adaptadas do padrão militar popularizado por Kabir Sehgal (HBR, 2016):

| Etiqueta | Uso |
|---|---|
| [AÇÃO] | o leitor precisa fazer algo |
| [APROVAÇÃO] | precisa de aprovação ou assinatura |
| [DECISÃO] | precisa escolher entre opções |
| [INFO] | só informativo, não exige resposta |
| [ALINHAMENTO] | precisa coordenar com você ou outro time |

Use etiqueta só quando o ambiente for de e-mail ou canal com muito volume. Em DM curta de Slack, dispense.

## Modelos para contexto de desenvolvimento

**Pedido de aprovação**
```
[APROVAÇÃO] Adiar entrega do módulo X para quinta (16/11)

Preciso da sua aprovação para adiar a entrega do módulo X de terça para quinta.

Motivo:
- Achamos um lock no banco que deixa a consulta de prêmios 10x mais lenta.
- A correção já está em andamento e leva 1 dia; o restante é teste.

Se preferir manter terça, entrego sem a correção e abro um card para a próxima sprint.
```

**Status report**
```
[INFO] Integração com sistema Y: 80%, no prazo

A integração está no prazo para sexta. Nenhum bloqueio.

- Feito: autenticação e envio de lotes.
- Falta: tratamento de erro de reenvio (amanhã).
- Risco: o time do sistema Y ainda não liberou o ambiente de homologação; cobrei hoje.
```

**Incidente**
```
[AÇÃO] Fila de cálculo parada desde 14h — precisamos de acesso ao Service Bus de produção

A fila de cálculo parou às 14h e ~300 mensagens estão acumuladas. Preciso de acesso de leitura ao Service Bus de produção para investigar.

- Impacto: cálculos de hoje não estão sendo gerados.
- Hipótese: mensagem malformada travando o consumidor.
- Próxima atualização: 15h30 ou antes, se resolver.
```

**Pedido de ajuda (nunca mande só "Oi, tudo bem?")**
```
Você sabe quem pode me ajudar a migrar dados do Oracle para o SQL Server? É para o projeto Z, prazo de 2 semanas. Se não souber, sem problema.
```

**Proposta técnica / resumo de ADR**
```
[DECISÃO] Usar Service Bus para notificações de sinistro

Proponho trocar a chamada HTTP direta por mensagem no Service Bus. Preciso da decisão até sexta para entrar na sprint.

Por quê:
- Hoje, se o serviço de notificação cai, perdemos o evento.
- Com fila, ganhamos retry e não perdemos mensagens.

Custo: ~3 dias de trabalho e um tópico novo na infra.
Alternativa: manter HTTP com retry via Polly (mais simples, mas ainda perde evento se o processo cair).
```

## Comunicação falada (1:1, daily, reunião)

Mesma lógica: comece pela conclusão, depois ofereça detalhe.
- "Resumo: vamos atrasar 2 dias. Quer que eu explique o motivo?"
- Se o chefe interromper, responda primeiro a pergunta dele, não continue a história.

## Quando NÃO aplicar BLUF puro

Adapte em vez de forçar:

1. **Notícia ruim ou sensível** (demissão, falha grave, feedback negativo). Dar o golpe na primeira linha faz o leitor parar de ler com boa vontade. Use uma frase curta de preparo e depois o fato direto: "Tenho uma notícia ruim sobre o prazo do projeto X: vamos atrasar 2 semanas."
2. **Problema ainda não está claro para o leitor.** O BLUF funciona bem quando o leitor já sabe qual é o assunto. Se ele não sabe, a conclusão solta não faz sentido. Use "problema em uma frase, depois a resposta" (crítica de Bryan Garner) ou SCQA.
3. **Persuasão de algo novo ou polêmico** para quem não conhece o tema. Use SCQA: Situação (o que todos concordam) → Complicação (o que mudou ou quebrou) → Pergunta (implícita) → Resposta (sua proposta). Em texto, a pergunta costuma ficar implícita.
4. **Você ainda não tem conclusão.** Não invente uma. Diga isso como BLUF: "Ainda não sei a causa; próxima atualização às 15h."
5. **Culturas ou pessoas que esperam construção de contexto** antes da conclusão. Ajuste ao leitor.

## Variações para conhecer

| Técnica | Estrutura | Quando preferir |
|---|---|---|
| BLUF | conclusão → contexto | padrão para mensagens do dia a dia |
| BLIND | Bottom Line → Impacto → Next steps → Detalhes | e-mails com impacto no negócio |
| SCQA (Minto) | Situação → Complicação → Pergunta → Resposta | propor algo novo, convencer |
| Pirâmide de Minto | ideia principal no topo, 2–3 argumentos, dados embaixo | documentos longos, ADRs, apresentações |
| Pirâmide invertida (jornalismo) | mais importante → menos importante | relatórios que podem ser lidos até qualquer ponto |

## Checklist final (verifique antes de entregar)

- [ ] A primeira frase contém o pedido/decisão/fato?
- [ ] Está claro o que o leitor precisa fazer e até quando?
- [ ] O assunto do e-mail já diz o ponto (não "Dúvida" ou "Atualização")?
- [ ] Voz ativa, com quem faz o quê?
- [ ] Contexto em tópicos curtos, sem história cronológica?
- [ ] Um assunto só?
- [ ] Cabe na tela sem rolar?
- [ ] Se for notícia ruim ou assunto novo, adaptei (preparo curto ou SCQA)?

## Erros comuns para apontar na revisão

- Começar com "Então, como você sabe..." ou com a cronologia do que foi feito.
- Pedido escondido no último parágrafo (BLAB: bottom line at bottom).
- Mostrar esforço em vez de resultado ("testamos várias coisas...").
- "Oi, tudo bem?" sozinho, esperando resposta para depois perguntar.
- Voz passiva que esconde o responsável ("erros foram cometidos").
- Dois assuntos na mesma mensagem.
- BLUF vago: "Queria falar sobre o projeto" não é bottom line; "Preciso de mais 1 dev no projeto até dia 20" é.
