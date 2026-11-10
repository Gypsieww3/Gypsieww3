# C.E.R.B.E.R.U.S. — Engineering & Research

**Cognitive Engineering, Robotics, Bio-inspired Evolution & Research for Unified Systems**

Iniciativa experimental de engenharia de software, IA local, robótica, processadores RISC-V, simulações e ferramentas de desenvolvimento. Os resultados são publicados com os seus limites e evidências de teste.

**Avaliação com empresas.** [Lote Claro, triagem de medições de qualidade](docs/lote-claro-piloto.md)

## Projetos em destaque

| Projeto | O que podes consultar |
| --- | --- |
| [Portefólio principal](https://github.com/Gypsieww3/cerberus) | Código de investigação, testes, documentação e demonstrações |
| [MOSS / KYVRAEL](https://github.com/Gypsieww3/cerberus/tree/main/01_MOSS_KYVRAEL) | Laboratório local supervisionado e integração Ollama |
| [TERRA VIVA](https://gypsieww3.github.io/cerberus-terra-viva-demo/) | Visualização pública de uma simulação fictícia (snapshot, não motor ao vivo) |
| [Code Guard](https://github.com/Gypsieww3/cerberus/blob/main/CODE_GUARD.md) | Ferramenta experimental de análise estática Python, piloto sob acordo |
| [Telemetry Studio](https://github.com/Gypsieww3/cerberus/blob/main/docs/TELEMETRY_STUDIO_PUBLIC.md) | Análise local de telemetria CSV e SQLite |
| [Control Plane](https://github.com/Gypsieww3/cerberus/blob/main/docs/INTEGRATION_CONTRACT.md) | Painel local de monitorização de serviços, apenas leitura |

**Explorar:** [Website](https://gypsieww3.github.io/cerberus/) · [Projetos interativos](https://gypsieww3.github.io/cerberus/projects.html) · [Estado e evidências](https://github.com/Gypsieww3/cerberus/blob/main/docs/RELEASE_MATRIX.md)

## Estudos de caso de engenharia de software

Projetos de portefólio desenvolvidos com assistência de IA. Os exemplos abaixo usam dados sintéticos.

### Oficina Stock

Ferramenta em **Python e SQLite** para registar materiais e movimentações numa oficina. A CLI devolve JSON para facilitar a integração com outros programas.

- Entram 8 chapas de MDF e saem 6. Com um mínimo de 2, o material aparece na lista de reposição.
- A mesma transação atualiza saldo e histórico. Ela adquire o bloqueio de escrita antes de ler o saldo para impedir que duas retiradas concorrentes gastem as mesmas unidades.
- Cinco testes de integração passaram, incluindo persistência entre execuções, reposição, dados inválidos, saída sem saldo e duas saídas simultâneas.

### Rota Lab

Ferramenta em **JavaScript e Node.js** que calcula o percurso mais rápido em pequenas redes de vias com tempos fornecidos no ficheiro de entrada. Usa o algoritmo de Dijkstra.

- Oficina → Centro → Bairro → Cliente leva **21 minutos**. A via entre Centro e Cliente está bloqueada. No percurso Centro → Oficina, a ligação de sentido único exige um desvio que eleva o tempo a **48 minutos**.
- O algoritmo percorre uma lista de adjacências e seleciona o próximo ponto por busca linear. No pior caso, o tempo cresce em O(V² + E), onde V é o número de pontos e E o número de ligações.
- Cinco testes passaram, cobrindo vias bloqueadas e de sentido único, destinos inalcançáveis, entradas inválidas e percurso com origem igual ao destino.

### Frame Lab

Descodificador em **C++17** para um protocolo de telemetria de robótica. Lê um fluxo hexadecimal, valida o CRC de cada quadro e volta a procurar a marca de sincronização quando encontra dados inválidos.

- Num fluxo de exemplo com ruído e três quadros, recuperou os dois válidos e sinalizou o quadro corrompido.
- O descodificador mantém no máximo 36 bytes de entrada em análise por vez. O teste usa dados sintéticos fornecidos pela entrada padrão.
- Seis testes de integração passaram, incluindo recuperação após CRC incorreto, quadro truncado e dados hexadecimais inválidos.

### Reserva API

API local em **Python e SQLite** para reservar lugares num workshop. Demonstra como uma API lida com pedidos repetidos e concorrentes.

- Num workshop de três lugares, reservar dois devolve HTTP 201. Reenviar o pedido com a mesma chave devolve HTTP 200 e o mesmo ID. Continua a sobrar um lugar.
- Uma transação SQLite protege a verificação da disponibilidade e o registo da reserva. Quando dois pedidos disputam o último lugar, só um é aceite.
- Oito testes de integração com conexões HTTP reais passaram. Também verifiquei que a reserva e a chave persistem após reiniciar a aplicação.

### Turno Claro

Agenda visual de um dia para uma oficina, feita com **HTML, CSS e JavaScript**. Organiza tarefas em três estações e guarda as alterações no navegador.

- Marcar uma tarefa em Corte das 08:30 às 09:00 gera um conflito com um turno existente. O mesmo horário é aceite em Acabamento, que está livre.
- Dois turnos podem tocar na mesma hora sem se sobrepor. O formulário explica o erro e mantém os dados introduzidos para correção.
- Seis testes de ponta a ponta passaram no Edge, incluindo persistência após recarregar e funcionamento num ecrã de 375 px.

[Ver a interface com dados sintéticos](docs/turno-claro.jpg)

### CSV Gate

Validador em **Python** para conferir um catálogo de fornecedor antes da importação. Lê o CSV registo a registo e gera um relatório JSON com contagens, tipos de erro e números de linha.

| Linha do catálogo de exemplo | Problema identificado |
| --- | --- |
| 4 | SKU duplicado. A primeira ocorrência está na linha 2. |
| 5 | Quantidade negativa. |
| 5 | Preço com três casas decimais. |

O exemplo sintético contém quatro registos, dos quais dois são válidos. A CLI devolve código de saída 1 para permitir que um pipeline interrompa a importação. Sete testes de integração passaram em Linux e Windows, incluindo CSV com aspas, vírgula decimal e registos com várias linhas.

### Relay Lab

Laboratório local de integração por webhook em **JavaScript e Node.js**. Envia um evento JSON e aplica uma política de reenvio com limite de tentativas e espera progressiva.

- Na demonstração, o recetor devolve HTTP 503. O programa espera 150 ms, reenvia o evento e confirma a entrega após receber HTTP 204.
- Todas as tentativas enviam a mesma chave de idempotência. Num dos testes, o recetor usa essa chave para evitar aplicar o evento duas vezes quando a primeira resposta se perde.
- Nove testes de integração passaram em Linux e Windows, incluindo timeout, rejeição definitiva, redirecionamento e execução da CLI.

### Contract Check

Ferramenta em **Python** para verificar respostas guardadas de uma API. Compara o estado HTTP e a estrutura do corpo com um contrato e gera um relatório JSON adequado a testes automatizados.

| Verificação no exemplo sintético | Resultado |
| --- | --- |
| Estado HTTP | Esperado 200, recebido 202. |
| Total da primeira ordem | Esperado um número, recebido texto. |
| Contagem de ordens | Campo obrigatório ausente. |

Os caminhos do relatório incluem nomes de campos e índices de listas. Campos adicionais continuam compatíveis. Sete testes passaram em Linux e Windows.

### Build Map

Planeador em **TypeScript** para tarefas com dependências. Recebe uma configuração JSON e agrupa em etapas as tarefas que podem correr em paralelo.

- No exemplo de pipeline, `checkout` termina antes de `build` e `lint`, que podem correr em paralelo. `test` depende de `build` e `package` espera pelos testes e pela análise do código.
- Quando `build` e `test` dependem um do outro, o relatório mostra o ciclo e identifica `package` como bloqueada, mesmo estando fora do ciclo.
- A verificação estrita de tipos passou. Sete testes passaram em Linux e Windows, incluindo o planeamento de uma cadeia com 3.000 tarefas.

### Pasta Radar

Ferramenta em **PowerShell** para analisar o espaço usado numa pasta. Percorre as subpastas e devolve um relatório JSON com os maiores ficheiros, o total por extensão e eventuais erros de leitura.

- No exemplo sintético, cinco ficheiros somam 100 bytes. Os dois ficheiros BIN ocupam 80 bytes e ficam no topo do relatório.
- A ferramenta inclui ficheiros ocultos e reporta separadamente as ligações que deixa de fora. A análise é de leitura.
- Seis verificações passaram no Windows PowerShell 5.1, incluindo agregação por extensão, empates, caminhos com colchetes e exclusão de uma junction.

### Lote Claro

Ferramenta em **Java** para triagem de medições de qualidade. Compara as leituras com as tolerâncias e com a lista de peças esperadas. Num exemplo sintético, identificou uma peça acima do limite e outra com uma medição em falta. Cinco testes passaram em Linux com Java 21.

[Ver o resultado e a proposta de piloto](docs/lote-claro-piloto.md)

### Transparência técnica

Os projetos encontram-se em fases diferentes. Testes internos não equivalem a certificação de segurança, disponibilidade comercial ou validação científica. As demonstrações usam dados sintéticos quando indicado. Códigos proprietários e informações sensíveis permanecem em repositórios privados.

### Contacto técnico

Pedidos não confidenciais de piloto e discussão técnica podem ser enviados através de [Issues do portefólio](https://github.com/Gypsieww3/cerberus/issues/new/choose). Não publiques dados pessoais, segredos ou ficheiros internos em issues públicas.

© 2026 C.E.R.B.E.R.U.S. — direitos reservados sobre os trabalhos originais dos titulares legítimos, respeitando licenças de terceiros.
