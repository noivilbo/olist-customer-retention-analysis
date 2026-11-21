# Enquadramento do problema

## Decisor e decisão
Diretoria de crescimento do marketplace. Decide onde investir para
aumentar a receita: aquisição de novos clientes, logística ou retenção.

Se o atraso na entrega reduzir a recompra de forma relevante em número
de clientes, a diretoria pode priorizar investimento em logística.
Se a diferença for pequena ou afetar poucos clientes, o investimento
tende a render mais em outra frente.

## Pergunta de negócio
O atraso na entrega reduz a satisfação e a recompra dos clientes?

## Definições
**Atraso:** pedido cuja data de entrega real é posterior à data
estimada. Só entram pedidos com data de entrega registrada.

**Recompra:** cliente que faz pelo menos um pedido entregue em data
posterior à do primeiro pedido entregue, em até 180 dias. Pedidos no
mesmo dia do primeiro são tratados como parte da mesma compra (30,9%
dos segundos pedidos ocorrem no mesmo dia). Clientes identificados por
customer_unique_id.

**Base de clientes analisada:** clientes cujo primeiro pedido entregue
foi feito entre 2017-01-01 e 2018-03-04. A janela de observação termina
em 2018-08-31, quando o volume de pedidos cai (16 pedidos em setembro e
4 em outubro), e a data-limite é 180 dias antes dela. Pedidos de 2016
ficam de fora (poucos e descontínuos). Clientes com primeiro pedido
posterior à data-limite não tiveram 180 dias de observação e ficam
fora.

## Hipóteses
H1. Pedidos entregues com atraso recebem notas menores do que
pedidos entregues no prazo.
- Escopo: pedidos entregues e com avaliação (768 pedidos, 0,8%, não
  têm avaliação e ficam de fora).
- Métrica: nota (1 a 5) comparada entre os dois grupos com
  Mann-Whitney, e diferença na proporção de notas 1 e 2, com
  intervalo de confiança.
- Refutaria: distribuições de notas parecidas entre os dois grupos,
  ou uma diferença tão pequena que não mudaria nenhuma decisão.

H2. Clientes cujo primeiro pedido chegou atrasado recompram menos.
- Métrica: taxa de recompra em 180 dias, atrasados contra no prazo,
  com intervalo de confiança da diferença.
- Refutaria: taxas parecidas entre os dois grupos.

## Fora do escopo
- **Efeito de um cupom ou bônus em caso de atraso.** O dataset não
  tem campanha de compensação nem grupo de controle, então a análise
  não consegue responder isso. Fica como recomendação de teste A/B,
  caso o atraso se mostre associado à perda de clientes.
- Causalidade: a análise é observacional e mostra associação.