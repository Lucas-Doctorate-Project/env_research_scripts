# Estratégia de Coleta de Dados para Simulação de Escalonamento Ambiental em HPC

Este documento descreve a fundamentação teórica para a seleção das fontes de dados históricos (países) e do recorte temporal utilizado na validação da política de escalonamento focada em pegada hídrica e de carbono.

## Seleção dos Grids Energéticos (Países)

A escolha da **França**, **Alemanha** e **Polônia** visa cobrir um espectro completo de desafios tecnológicos e ambientais, permitindo analisar como diferentes matrizes respondem a uma política que equilibra objetivos frequentemente conflitantes (Carbono vs. Água).

| Região | Perfil do Grid | Justificativa Científica |
| :--- | :--- | :--- |
| **França** | **Estabilidade & Baixo Carbono** | Matriz dominada por energia nuclear. Possui a menor intensidade de $CO_2$ constante, mas uma **pegada hídrica indireta elevada** devido ao resfriamento das usinas. Serve para testar se políticas puramente voltadas ao carbono falham ao ignorar o impacto hídrico. |
| **Alemanha** | **Transição & Volatilidade** | Matriz mista com alta penetração de renováveis intermitentes (eólica/solar) e suporte fóssil. As taxas ambientais podem oscilar drasticamente em poucas horas. É o cenário ideal para validar o **load shifting** temporal. |
| **Polônia** | **Fóssil & Base Inflexível** | Majoritariamente baseada em carvão (lignito e hulha). Mesmo com picos sazonais de eólica (~30%), a base térmica garante que as emissões e o consumo de água indireto permaneçam altos. Representa o pior cenário e o potencial máximo de redução absoluta. |

Os arquivos correspondentes aos dados extraídos para cada um dos países são high_carbon_trace.csv (Polônia), low_carbon_trace.csv (França) e volatile_carbon_trace.csv (Alemanha).

---

## Definição do Período Experimental

A simulação utiliza um rastro de **7 dias no mês de Janeiro** (Inverno Europeu) por ser o período de maior estresse operacional e climático.

### Por que Janeiro?
1. **Pico de Demanda Térmica:** O uso massivo de aquecimento elétrico estressa os grids, forçando a operação máxima de usinas nucleares e térmicas. Isso torna os dados de consumo de água e emissão de carbono mais pronunciados e fáceis de medir.
2. **Contraste Climático (Dunkelflaute):** Período propenso a "calmarias escuras" (baixa solar e eólica cessando subitamente). Isso cria transições binárias perfeitas para testar a sensibilidade do escalonador entre momentos de baixa e alta intensidade de impacto.

### Por que 7 dias?
* **Ciclo de Carga Semanal:** Permite capturar a variabilidade entre dias úteis (alta carga industrial e ambiental) e finais de semana (alívio de carga).
* **Amostragem Estatística:** Garante que a calibração dos limites de ativação da política ($R_{min}$ e $R_{max}$) seja baseada em uma amostra realista, evitando enviesamento por eventos isolados de 24 horas.
