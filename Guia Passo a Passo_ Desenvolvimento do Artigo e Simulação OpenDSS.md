# Guia Passo a Passo: Desenvolvimento do Artigo e Simulação OpenDSS

Este guia consolida a estrutura do artigo que elaboramos e as etapas práticas para você desenvolver as simulações no OpenDSS.

## Fase 1: Preparação e Estrutura do Artigo

**Objetivo:** Ter o esqueleto do artigo pronto e as referências iniciais.

| Passo | Ação | Status |
| :--- | :--- | :--- |
| **1.1** | **Revisar a Proposta:** Leia o arquivo `proposta_artigo_final.md` para entender a estrutura (Introdução, Metodologia, Resultados Esperados). | Concluído |
| **1.2** | **Coletar Referências:** Utilize os links fornecidos (Tutoriais, Artigos Científicos, Atlas Solar) para aprofundar seu conhecimento e preencher a seção de Referências. | Em Andamento |
| **1.3** | **Instalar o OpenDSS:** Baixe e instale o OpenDSS em seu computador. | Pendente |
| **1.4** | **Estudar a Modelagem:** Focar nos tutoriais sobre `LineCode`, `Loadshape`, `PVSystem` e, principalmente, `Storage` e `StorageController`. | Em Andamento |

## Fase 2: Modelagem e Criação dos Arquivos OpenDSS

**Objetivo:** Criar os arquivos `.dss` para o estudo de caso.

| Passo | Arquivo | Conteúdo Principal | Status |
| :--- | :--- | :--- | :--- |
| **2.1** | `Master.dss` | Arquivo principal que chama todos os outros. | Criado |
| **2.2** | `Circuit.dss` | Define a fonte e a tensão base (13.8 kV). | Criado |
| **2.3** | `LineCodes.dss` | Define os parâmetros dos condutores rurais (ACSR). | Criado |
| **2.4** | `Lines.dss` | Define a topologia radial (Bus 1 a Bus 5). | Criado |
| **2.5** | `LoadShapes.dss` | Define as curvas de carga (Residencial, Irrigação) e o perfil solar (`Tshape`). **Ajuste o Tshape com dados reais da Bahia.** | Criado (Ajustar) |
| **2.6** | `Loads.dss` | Define as cargas residenciais e o motor de irrigação (Bus 5). | Criado |
| **2.7** | `PVSystem.dss` | Define o sistema fotovoltaico (200 kWp na Bus 4). | Criado |
| **2.8** | `Storage.dss` | Define o sistema de armazenamento (50 kW / 200 kWh na Bus 4) e o `StorageController`. | Criado |

## Fase 3: Execução das Simulações e Análise

**Objetivo:** Rodar os 4 cenários e extrair os dados de desempenho.

| Cenário | Ação no OpenDSS | Análise Focada |
| :--- | :--- | :--- |
| **3.1: Base** | **Desabilitar** PVSystem e Storage. Rodar `Set Mode=Daily`. | Perfil de Tensão (Vmin) e Perdas. |
| **3.2: Irrigação Crítica** | Cenário Base. Rodar `Set Mode=Fault` com uma falta na Bus 2. | Profundidade do Afundamento de Tensão (Sag) na Bus 5. |
| **3.3: Com PVSystem** | **Habilitar** PVSystem. Rodar `Set Mode=Daily`. | Elevação de Tensão (Vmax) e Perdas durante o dia. |
| **3.4: Otimizado** | **Habilitar** PVSystem e Storage (com `StorageController`). Rodar `Set Mode=Daily`. | **Mitigação** do Afundamento (comparar com 3.2) e **Controle** da Elevação de Tensão. |
| **3.5: Otimização** | Variar os parâmetros de kVA/kWh do Storage e a estratégia do `StorageController` (ex: de `Voltage` para `Loadshape` ou `PeakShaving`). | Encontrar o ponto ótimo que maximiza a qualidade de energia e minimiza o custo. |

**Comandos Chave para Extração de Dados:**

*   `Show Voltages LN` (para ver o perfil de tensão em um instante)
*   `Show Losses` (para ver as perdas)
*   `New Monitor` (para registrar dados ao longo do tempo, essencial para o `Mode=Daily`)
*   `Export Monitors` (para salvar os dados registrados em arquivos CSV)

## Fase 4: Redação Final

**Objetivo:** Escrever o artigo com base nos resultados das simulações.

| Seção | Conteúdo |
| :--- | :--- |
| **Introdução** | Contextualizar a eletrificação rural e o problema de qualidade de energia. |
| **Metodologia** | Descrever o estudo de caso (topologia, cargas) e detalhar a modelagem no OpenDSS (condutores, PV, Storage). |
| **Resultados** | Apresentar os gráficos e tabelas comparando os 4 cenários (Perfil de Tensão, Afundamentos, Perdas). |
| **Discussão** | Analisar o impacto do PVSystem e a eficácia do Storage System na mitigação dos problemas. Discutir a otimização. |
| **Conclusão** | Sintetizar os achados e as contribuições do trabalho. |
| **Referências** | Citar todos os artigos, tutoriais e fontes de dados utilizados. |

Este guia é o seu roteiro. Os arquivos `.dss` que criamos na pasta `opendss_simulation` já são um excelente ponto de partida para a Fase 2.

Qualquer dúvida sobre a modelagem ou a interpretação dos resultados, estou à disposição.
