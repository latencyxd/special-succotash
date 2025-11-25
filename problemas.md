Comprimento Insuficiente: O 123-Bus tem um comprimento total que não reflete a extensão de um alimentador rural típico (que pode ter dezenas ou até centenas de quilômetros).
Aumentar o Comprimento das Linhas: No arquivo Lines.dss do 123-Bus, multiplique o parâmetro Length (Comprimento) das linhas mais longas por um fator (ex: 5 ou 10). Isso simulará o efeito de longas distâncias e aumentará as perdas e as quedas de tensão.
Condutores Finos: O 123-Bus usa condutores que podem ser mais robustos do que os encontrados nas pontas de redes rurais.
Ajustar LineCodes: Verifique o arquivo IEEELineCodes.DSS e, nas linhas mais distantes, substitua o LineCode por um com maior resistência (R1) e reatância (X1), simulando condutores mais finos (como o ACSR #4 que você havia sugerido).


ariação Extrema de Tensão: O perfil de tensão no 123-Bus pode ser corrigido pelos reguladores. Em redes rurais, a tensão pode cair abaixo dos limites regulatórios (ex: 0.92 pu).
Ajustar a Fonte: No arquivo Circuit.dss, você pode reduzir o pu da fonte para simular uma tensão de subestação ligeiramente mais baixa, forçando o problema de queda de tensão.
Carga de Irrigação como Motor: O 123-Bus usa cargas estáticas (P-Q). O motor de irrigação é uma carga dinâmica que causa um grande impacto no momento da partida.
Modelar o Motor como Motor ou Load com Model=5: Use o elemento Load com Model=5 (Exponencial) ou Model=8 (Motor de Indução) para simular o comportamento de partida do motor, o que causará um afundamento de tensão mais realista e severo.


Taxa de Falhas Elevada: O modelo não inclui uma taxa de falhas inerente.
Análise de Confiabilidade (Opcional): Use o comando Fault em diferentes pontos da rede (como você planejou) e, para um estudo mais avançado, use o modo de simulação Reliability do OpenDSS para calcular índices como SAIFI e SAIDI, que são cruciais para a eletrificação rural.
Coordenação de Proteção: A baixa corrente de curto-circuito em longos alimentadores rurais dificulta a atuação da proteção.
Simulação de Curto-Circuito: Mantenha a simulação de falta (Cenário 2) e analise a corrente de curto-circuito na ponta do alimentador. Se for muito baixa, você pode discutir o desafio da coordenação de proteção no artigo.
