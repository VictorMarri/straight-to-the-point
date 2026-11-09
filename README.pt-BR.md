# `/straight-to-the-point`

> 🇺🇸 [Read this in English](./README.md)

Skill do [Claude Code](https://claude.com/claude-code) que escreve, reescreve e
revisa mensagens de trabalho no formato **BLUF (Bottom Line Up Front)**, o padrão
de escrita do Exército dos EUA: o pedido, a decisão ou a conclusão vai na
primeira frase.

## Antes e depois

**Antes:**

```
Então, a gente começou a investigar a lentidão na API de prêmios ontem, olhou
os logs, testou umas coisas no cache e achou um lock no banco que deixa a
consulta ~10x mais lenta. A correção leva um dia mais os testes, então acho que
vamos precisar adiar um pouco a entrega, pode ser?
```

**Depois:**

```
[APROVAÇÃO] Adiar entrega do módulo X para quinta (16/11)

Preciso da sua aprovação para adiar a entrega do módulo X de terça para quinta.

Motivo:
- Um lock no banco deixa a consulta de prêmios ~10x mais lenta.
- A correção leva 1 dia; o restante é teste.

Se preferir manter terça, entrego sem a correção.
```

## Instalação

```bash
git clone https://github.com/VictorMarri/straight-to-the-point ~/.claude/skills/straight-to-the-point
```

## Uso

```
/straight-to-the-point avisa meu chefe que a entrega atrasa 2 dias por causa de um lock no banco
/straight-to-the-point reescreve isso: <rascunho>
/straight-to-the-point revisa esse e-mail: <rascunho>
```

A skill responde no idioma em que você escreve.

## Fontes

US Army AR 25-50 e DA PAM 600-67 · Kabir Sehgal, HBR (2016) · Barbara Minto, *The Pyramid Principle*

## Licença

[MIT](./LICENSE)
