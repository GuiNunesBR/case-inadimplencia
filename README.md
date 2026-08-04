# Previsão de Inadimplência — Case de Risco de Crédito

Modelo que estima a probabilidade de inadimplência (pagamento com 5 dias ou mais de atraso) para cobranças mensais de clientes, desenvolvido a partir de um case técnico de risco de crédito.

## Abordagem

- Target: atraso >= 5 dias entre pagamento e vencimento
- Features de comportamento do cliente sem vazamento temporal: cada cobrança só enxerga as cobranças anteriores dela (shift + expanding)
- Perfil cadastral, renda mensal e contexto da cobrança (prazo, valor sobre renda, tempo de relacionamento)
- Validação out-of-time: treino até 2020-12, validação de 2021-01 a 2021-06, imitando o cenário real (treinar no passado, prever o futuro)
- Baseline (taxa histórica de atraso do cliente) como régua mínima
- Decisão sobre as safras da crise de 2020 tomada por experimento, não por opinião

## Resultados (validação out-of-time)

| Versão | AUC | PR-AUC |
|---|---|---|
| Baseline — taxa histórica do cliente | 0.896 | 0.457 |
| LightGBM | 0.941 | 0.623 |
| LightGBM sem as safras da crise (modelo final) | 0.945 | — |

## Como executar

1. Python 3.12 e `pip install -r requirements.txt`
2. As 4 bases do case ficam na pasta `data/`
3. Executar `case_inadimplencia.ipynb` do início ao fim (Run All) — gera o `submissao_case.csv` (semente fixa, resultado reprodutível)
