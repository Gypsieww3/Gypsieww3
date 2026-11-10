# Lote Claro | Avaliação técnica

O Lote Claro é uma ferramenta local em Java para equipas que conferem medições de peças por lote. Cruza a lista de peças previstas, as tolerâncias fornecidas pela qualidade e as medições recolhidas. O resultado indica quais os lotes que precisam de revisão e mostra o motivo por peça.

## Demonstração com dados sintéticos

No exemplo, três peças distribuídas por dois lotes exigem duas medições cada, largura e espessura. O máximo permitido para a largura é 100,5 mm.

| Lote | Peças previstas | Resultado | Ocorrências |
| --- | ---: | --- | --- |
| L-A | 1 | Conforme | A largura de 100,5 mm coincide com o limite inclusivo. Todas as medições estão presentes. |
| L-B | 2 | Retido para revisão | A peça P1 mediu 100,501 mm. Falta a medição de largura da peça P2. |

O relatório JSON identifica a peça, a característica, os limites e o valor observado quando disponível. Cinco testes de integração passaram em Linux com Java 21. Cobrem limites inclusivos, vírgula decimal, medições em falta, valores fora da tolerância e rejeição de entradas inconsistentes.

## Piloto proposto

1. Selecionar uma família de peças e um conjunto pequeno de lotes históricos já revistos pela qualidade.
2. Preparar três tabelas com identificadores anonimizados. Uma com as tolerâncias, outra com as peças esperadas por lote e uma terceira com as medições e unidades.
3. Executar a análise localmente e comparar cada ocorrência com a revisão manual. Registar valores fora do limite, medições em falta, divergências e tempo de conferência.
4. Avaliar se a ferramenta identifica todas as ocorrências conhecidas na amostra e se o relatório permite localizar a peça e explicar o resultado. A equipa de qualidade revê as divergências e decide se vale ampliar o piloto.

A versão atual recebe TSV em UTF-8 e trabalha com um conjunto de tolerâncias por execução. A avaliação tem caráter retrospetivo e mantém a decisão sobre o lote com a equipa de qualidade.

Para conversar sobre uma avaliação técnica, descreve o tipo de peça, o formato dos dados e o objetivo da análise, usando apenas informação não confidencial. [Contacto técnico](https://github.com/Gypsieww3/cerberus/issues/new/choose)
