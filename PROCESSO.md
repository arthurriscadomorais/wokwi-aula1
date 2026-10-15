# PROCESSO.md — Lab 1 · Pisca-LED

**Aluno:** Arthur Riscado de Morais · arthur.morais@sou.inteli.edu.br
**Turma / grupo:** T26 · Grupo 3

## 1. Contextualizar
- **Objetivo:** Usar o simulador wokwi e montar um arduino e verificar o comportamento do LED.
- **Comportamento esperado:** pulsar a cada 2s
- **Critério de aceitação:** os ciclos cronometrados ficam entre 1,9 s e 2,1 s, e a corrente calculada fica abaixo de 20 mA, a corrente recomendada pelo datasheet
- **Delegação à IA × feito sozinho:** Contextos, para caso eu tenha uma dúvida, posso acioná-la. Toda parte de fazer e compreender, eu devo estar ciente.

## 2. Consultar
- **Ferramenta:** Claude
- **Pergunta (exata):** Por que o LED precisa de um resistor para funcionar com o Arduino sem correr o risco de queimar?
- **Resposta resumida:** Um LED não se comporta como uma resistência comum. Depois que a tensão sobre ele passa de um certo valor (a tensão direta, cerca de 2 V num LED vermelho), a corrente sobe de forma rápida. Uma pequena variação de tensão causa uma grande variação de corrente, e o próprio LED não limita nada disso.

O pino do Arduino entrega 5 V. Sem resistor, essa tensão ficaria quase toda “sobrando” sobre o LED, e a corrente subiria até o limite do pino ou do componente. Um LED comum suporta algo em torno de 20 mA. Acima disso ele esquenta, perde vida útil e pode queimar. O pino do Arduino também tem limite (cerca de 20 a 40 mA), então ele pode ser danificado junto.

O resistor em série assume o papel de limitar a corrente. Ele “absorve” a tensão que sobra, e a conta vem da lei de Ohm: R = (Vfonte − Vled) / I. Para um LED vermelho a 5 V, com cerca de 2 V no LED e 20 mA desejados, dá (5 − 2) / 0,02 = 150 Ω. Na prática se usa 220 Ω ou 330 Ω, que dão uma corrente menor (cerca de 14 e 9 mA), mais segura e ainda com brilho bom.

## 3. Confrontar
- **Afirmação conferida:** R = (Vfonte − Vled) / I. Para um LED vermelho a 5 V, com cerca de 2 V no LED, dá 150 Ω para 20 mA. Na prática se usa 220 Ω ou 330 Ω, que dão cerca de 14 e 9 mA
- **Fonte primária:** Lei de Ohm (cálculo)
- **Trecho / cálculo:** Cálculo (Lei de Ohm): a tensão sobre o resistor é 5 V − 2 V = 3 V, então I = 3 V ÷ R.

Com 220 Ω: I = 3 ÷ 220 ≈ 13,6 mA
Com 330 Ω: I = 3 ÷ 330 ≈ 9,1 mA
- **Veredito:** Precisou de ajuste
- **ADR:** —

## 4. Construir
- **Wokwi:** https://wokwi.com/projects/477970283288734721
- **Repositório / commit:** —
- **Ciclo medido:** 2 s
- **Corrente calculada com 220 Ω:** 13.6 mA
- **Projeto funcionando:** sim

## 5. Comprovar (sem IA)
1. **Corrente com 330 Ω:** 9.1 mA — cálculo: I = V ÷ R = 3 ÷ 330 ≈ 0,0091 A =  9,1 mA
2. **Resistor de 0 Ω:** Porque nada limita a corrente, que passa muito do máximo suportado pelo LED. — Com 0 Ω nada limita a corrente, que passa do máximo suportado pelo LED e o queima.
3. **LED no pino 12:** Só o valor de PINO_LED passa a ser 12 (e o fio vai para o pino 12).
4. **TEMPO_APAGADO para 500 ms a cada 3 s:** 2500 ms

Declaro que respondi a etapa Comprovar sem IA: não
