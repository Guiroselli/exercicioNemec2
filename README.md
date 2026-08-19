# Análise de Medicamentos — Pressão Arterial

Análise de 5 medicamentos experimentais (Cardioxina, Energozin, Glucorex, Relaxol, Thermocor)
para identificar qual reduz a pressão arterial sem causar efeitos colaterais.

## Como rodar

**Google Colab** (recomendado) — abre e roda sem nenhuma configuração, os dados são
carregados automaticamente deste repositório:

[Abrir no Colab](https://colab.research.google.com/github/Guiroselli/exercicioNemec2/blob/claude/blood-pressure-analysis-colab-t8dadt/analise_medicamentos_colab.ipynb)

**Local:**

```bash
pip install pandas numpy scipy matplotlib jupyter
jupyter notebook analise_medicamentos_colab.ipynb
```

## Estrutura

```
analise_medicamentos_colab.ipynb   notebook com a análise completa
data/                              datasets (carregados automaticamente pelo notebook)
```

## Os dados

5 arquivos CSV, um por medicamento, com **30 pacientes cada**. Cada linha traz a medição
**Inicial** (antes) e **Final** (depois) de 5 variáveis:

| Coluna | Unidade |
|---|---|
| Pressão | mmHg |
| Temperatura | °C |
| Glicose | mg/dL |
| Frequência Cardíaca | bpm |
| Nível de Energia | escala 0–10 (ordinal) |

Não há grupo placebo, e a coluna `Paciente` aparece duplicada no fim de cada arquivo
(o notebook remove a duplicata no carregamento).

**Aviso sobre `glucorex_dataset.csv`:** a glicose final é censurada em um piso de
exatamente `40.0 mg/dL` em 3 pacientes. Isso distorce a média do efeito do Glucorex
(−4,95 mg/dL) frente ao efeito típico (mediana −2,00 mg/dL). A análise trata esse ponto
explicitamente — ver seções 6 e 7 do notebook.

## Resultado

**Cardioxina em monoterapia**, com monitoramento glicêmico.

- É o único medicamento com redução relevante de pressão: **−15,0 mmHg** (p < 0,001).
- Seu único efeito colateral é uma alta leve de glicose (+7,6 mg/dL), que mantém todos
  os pacientes fora da faixa diabética (máximo final: 116 mg/dL).
- **Nenhuma das 31 combinações possíveis anula esse efeito colateral** pelo critério
  robusto (mediana): o melhor resíduo alcançável é +5,58 mg/dL.
- Combinar com Glucorex para "corrigir" a glicose piora o quadro: o Glucorex causa
  hipoglicemia nova em **5 de 30 pacientes (17%), 3 delas graves** (40 mg/dL).
