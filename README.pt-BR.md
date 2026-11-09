# `/straight-to-the-point`

> 🇺🇸 [Read this in English](./README.md)

Você já mandou uma mensagem longa pro seu chefe e recebeu de volta um
*"ok, mas o que você precisa de mim?"*

A resposta estava lá. Escondida na quinta linha, depois da história, das
coisas que você testou e do "então, como você sabe...". O leitor parou antes
de chegar nela.

`/straight-to-the-point` (*direto ao ponto*) é uma skill do
[Claude Code](https://claude.com/claude-code) que escreve, reescreve e revisa
mensagens de trabalho usando o **BLUF (Bottom Line Up Front)**, o padrão de
escrita do Exército dos EUA: o pedido, a decisão ou a conclusão vão na
primeira frase. O contexto vem depois, só o quanto o leitor precisa.

## O único teste

> **Se o leitor parar na primeira frase, ele sabe o que está acontecendo e o
> que precisa fazer?**

Se não, a skill reescreve até ele saber.

## Antes e depois

**Antes** (a história na ordem em que aconteceu):

```
Então, a gente começou a investigar a lentidão na API de prêmios ontem, olhou
os logs, testou umas coisas no cache e no fim achou um lock no banco que deixa
a consulta umas 10x mais lenta. Já estamos corrigindo, mas leva um dia mais os
testes, então acho que vamos precisar adiar um pouco a entrega, pode ser?
```

**Depois** (a conclusão primeiro):

```
[APROVAÇÃO] Adiar entrega do módulo X para quinta (16/11)

Preciso da sua aprovação para adiar a entrega do módulo X de terça para quinta.

Motivo:
- Achamos um lock no banco que deixa a consulta de prêmios ~10x mais lenta.
- A correção já está em andamento e leva 1 dia; o restante é teste.

Se preferir manter terça, entrego sem a correção e abro um card para a
próxima sprint.
```

Os fatos são os mesmos. Mas o chefe responde a segunda em cinco segundos, sem
rolar a tela, e a alternativa já está na mesa.

## Por que ela existe

Sou engenheiro backend indo em direção à arquitetura de software. Quanto mais
você sobe, mais o seu trabalho vira escrever para gente sem tempo: status,
pedido de aprovação, relato de incidente, proposta técnica. Uma boa ideia
técnica numa mensagem mal ordenada é ignorada.

Conheci o BLUF num vídeo curto sobre como engenheiros seniores falam com os
chefes, fui atrás de onde ele veio de verdade, e transformei o que encontrei
numa skill que eu chamo no momento exato em que vou apertar "enviar".

## O que ela faz

A skill escolhe um de três modos a partir do seu pedido:

| Modo | Você entrega | Você recebe |
|---|---|---|
| **Escrever** | a situação, em qualquer ordem | a mensagem pronta para copiar |
| **Reescrever** | um rascunho seu | a versão BLUF dele |
| **Revisar** | um rascunho, pedindo feedback | até 3 pontos que quebram o BLUF e a correção |

Por dentro, ela segue sempre os mesmos seis passos:

1. **Achar o bottom line.** "Se eu só pudesse mandar uma frase, qual seria?"
2. **Escrever em 1 ou 2 frases:** o quê, quem, até quando e por quê.
3. **Dizer que tipo de resposta espera:** ação, aprovação ou só leitura.
4. **Contexto depois, em tópicos curtos.** Sem cronologia, sem relatório de esforço.
5. **Fechar com o próximo passo:** quem faz o quê e quando.
6. **Um assunto por mensagem.** Dois assuntos, duas mensagens.

Vem com modelos prontos para as mensagens que dev manda de verdade: pedido de
aprovação, status report, incidente, pedido de ajuda (nunca só *"oi, tudo
bem?"*) e proposta técnica / resumo de ADR. O assunto do e-mail ganha
etiquetas no estilo militar (`[AÇÃO]`, `[APROVAÇÃO]`, `[DECISÃO]`, `[INFO]`)
para o leitor saber o que a mensagem quer dele antes de abrir.

## Quando ela *não* usa BLUF puro

BLUF não é regra universal, e a skill sabe quando adaptar:

- **Notícia ruim ou sensível.** Uma linha curta para preparar o leitor e
  depois o fato, sem rodeio. Abrir com "o projeto falhou" faz a pessoa parar
  de ler com boa vontade.
- **O leitor ainda não conhece o problema.** Conclusão sem problema não faz
  sentido. O problema vai numa frase, e a resposta logo depois.
- **Vender algo novo ou polêmico.** Ela troca para o **SCQA** da Barbara
  Minto: Situação → Complicação → Pergunta → Resposta.
- **Você ainda não tem conclusão.** Ela não inventa uma. "Causa ainda
  desconhecida; próxima atualização às 15h" é um ótimo bottom line.

## Instalação

```bash
git clone https://github.com/VictorMarri/straight-to-the-point ~/.claude/skills/straight-to-the-point
```

No claude.ai, você também pode enviar o `SKILL.md` como skill personalizada
nas configurações.

## Uso

```
/straight-to-the-point preciso avisar meu chefe que a entrega atrasa 2 dias por causa de um lock no banco
```

```
/straight-to-the-point reescreve isso: <cole seu rascunho>
```

```
/straight-to-the-point revisa esse e-mail antes de eu mandar: <cole>
```

A skill responde no idioma em que você escreve.

## De onde vem

- **Army Regulation 25-50**, *Preparing and Managing Correspondence*: as duas
  regras essenciais da escrita do Exército são o bottom line up front e a voz
  ativa.
- **DA Pamphlet 600-67**, *Effective Writing for Army Leaders* (1986): comece
  pela informação que você manteria se tivesse que jogar o resto fora.
- **Kabir Sehgal**, *How to Write Email with Military Precision*, Harvard
  Business Review (2016): etiquetas no assunto e BLUF no e-mail do dia a dia.
- **Barbara Minto**, *The Pyramid Principle*: o SCQA e como organizar tudo
  embaixo da ideia principal.
- **Bryan Garner** (ABA Journal): a crítica de que o BLUF precisa do problema
  claro antes, que deu origem à seção "quando não usar".

## Licença

[MIT](./LICENSE)
