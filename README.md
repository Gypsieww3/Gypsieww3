# C.E.R.B.E.R.U.S. — Engineering & Research

**Cognitive Engineering, Robotics, Bio-inspired Evolution & Research for Unified Systems**

Iniciativa experimental de engenharia de software, IA local, robótica, processadores RISC-V, simulações e ferramentas de desenvolvimento. Os resultados são publicados com os seus limites e evidências de teste.

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

### Transparência técnica

Os projetos encontram-se em fases diferentes. Testes internos não equivalem a certificação de segurança, disponibilidade comercial ou validação científica. As demonstrações usam dados sintéticos quando indicado. Códigos proprietários e informações sensíveis permanecem em repositórios privados.

### Contacto técnico

Pedidos não confidenciais de piloto e discussão técnica podem ser enviados através de [Issues do portefólio](https://github.com/Gypsieww3/cerberus/issues/new/choose). Não publiques dados pessoais, segredos ou ficheiros internos em issues públicas.

© 2026 C.E.R.B.E.R.U.S. — direitos reservados sobre os trabalhos originais dos titulares legítimos, respeitando licenças de terceiros.
