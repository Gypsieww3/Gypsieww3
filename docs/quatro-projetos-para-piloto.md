# Quatro projetos para avaliação técnica

Demonstrações locais da C.E.R.B.E.R.U.S. para equipas de operação, compras, suporte e produção. Os exemplos usam dados sintéticos. Cada repositório tem instruções de execução e testes automatizados. O desenvolvimento teve assistência de IA.

| Projeto | Linguagem principal | Testes aprovados | Ambiente verificado |
| --- | --- | ---: | --- |
| [Corte Planejado](#corte-planejado) | C++17 | 9 | Linux |
| [Reconcilia Pedidos](#reconcilia-pedidos) | Java 21 | 8 | Linux |
| [Fila SLA](#fila-sla) | TypeScript | 10 | Linux e Windows |
| [Rastro de Lote](#rastro-de-lote) | SQL e SQLite | 9 | Linux e Windows |

## Corte Planejado

Distribui peças por barras de comprimento fixo e calcula a perda de material na serra e a sobra por barra. No exemplo, seis peças ocupam **duas barras de 3.000 mm**. O plano separa **5.880 mm em peças, 18 mm de perda na serra e 102 mm de sobra**.

Para avaliar, usa um pedido de corte já concluído e a espessura real da serra. Compara a quantidade de barras e as sobras com o plano usado pela oficina e verifica se todas as peças cabem nas barras propostas. O método assume barras iguais e usa uma heurística que pode deixar margem para um plano melhor.

## Reconcilia Pedidos

Compara quantidades pedidas e recebidas por pedido e item. No exemplo, entregas de **4 e 6 unidades** completam um pedido de 10. O programa ignora uma repetição idêntica do mesmo recebimento e sinaliza quatro divergências noutros itens, uma falta, uma entrega parcial, um excesso e um item inesperado.

Para avaliar, exporta dois conjuntos anonimizados de um período fechado e confronta os casos sinalizados com uma conferência já realizada. A versão atual trabalha com quantidades inteiras e uma unidade de medida por item.

## Fila SLA

Calcula prazos de atendimento em minutos úteis e ordena os chamados pelo vencimento. Com expediente das 09h às 17h UTC e a segunda-feira encerrada, um chamado de **60 minutos aberto na sexta-feira às 16h30 UTC** vence na terça-feira às **09h30 UTC**. A verificação estrita de tipos também passou.

Para avaliar, usa chamados com prazos já conferidos pela equipa e verifica a ordem da fila, os horários de abertura e os dias de encerramento. O calendário atual usa uma janela diária fixa em UTC, de segunda a sexta.

## Rastro de Lote

Percorre os vínculos registados numa base SQLite para identificar quais lotes de produção consumiram um lote de fornecedor, diretamente ou através de derivados. No exemplo, **MP-101** leva a quatro lotes de produção. **P-130** aparece uma vez, embora tenha dois caminhos de origem. Um lote de outra linhagem fica fora da lista.

Para avaliar, usa uma cópia local anonimizada de uma linhagem conhecida e compara os resultados com os registos de produção. A consulta abre a base em modo só de leitura e mostra os lotes alcançáveis. A equipa pode usar o relatório para orientar a investigação.

Para conversar sobre um piloto, indica o processo que queres avaliar e como o resultado é conferido hoje. Usa apenas informação não confidencial no primeiro contacto. [Contacto técnico](https://github.com/Gypsieww3/cerberus/issues/new/choose)
