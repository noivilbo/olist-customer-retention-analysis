# Decisões do projeto

## Dados e chaves
1. **Cliente = customer_unique_id.** O customer_id muda a cada pedido:
   99.441 customer_id contra 96.096 clientes reais.
2. **Agregar itens e pagamentos antes de juntar.** Juntar as duas
   tabelas direto infla a soma de preços em ~4,5% (14,21 mi contra
   13,59 mi).
3. **Tabelas usadas:** orders, customers, order_items, order_payments
   e order_reviews. Fora: geolocation (mais de 1 milhão de linhas, com
   várias por CEP, sem uso na pergunta), sellers e products.

## Pedidos válidos
4. **Pedido entregue:** order_status = delivered. São 96.478 dos
   99.441 pedidos (97%). Excluídos: shipped (1.107), canceled (625),
   unavailable (609), invoiced (314), processing (301), created (5) e
   approved (2).
5. **Atraso só com data de entrega.** Pedidos delivered sem
   order_delivered_customer_date ficam fora do cálculo de atraso.
   [Pendente: contar quantos são, na etapa 3.]
6. **Avaliações:** 547 pedidos têm mais de uma avaliação; usar a mais
   recente. 768 pedidos (0,8%) não têm avaliação e ficam fora da H1.

## Janela de observação
7. **2016 fica de fora:** 329 pedidos no ano, sem nenhum em novembro.
8. **Fim da janela:** 2018-08-31 (último pedido antes de setembro,
   às 16h13; setembro tem 16 pedidos e outubro, 4, contra mais de
   6.000 por mês até agosto).
9. **Data-limite do primeiro pedido:** 2018-03-04 (fim da janela
   menos 180 dias). Quem comprou depois não teve 180 dias de
   observação.

## Recompra e atraso
10. **Mesmo dia = mesma compra.** 30,9% dos segundos pedidos ocorrem
    no mesmo dia do primeiro (provável pedido dividido). Recompra
    exige pedido em data posterior à do primeiro. Isso reduz os
    clientes com mais de um pedido de 2.997 (3,12%) para 2.149
    (2,24%).
11. **Janela de 180 dias:** 83% dos segundos pedidos ocorrem em até
    180 dias (mediana de 27 dias, terceiro quartil de 123).
12. **Atraso no primeiro dia de compra:** se o primeiro dia tem mais
    de um pedido, o cliente é "atrasado" se qualquer um deles atrasou.