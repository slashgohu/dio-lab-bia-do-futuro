# Base de Conhecimento

## Dados Utilizados

| Arquivo | Formato | Utilização no Agente |
|---------|---------|---------------------|
| `historico_atendimento.csv` | CSV | Contextualizar interações anteriores |
| `perfil_investidor.json` | JSON | Personalizar recomendações |
| `produtos_financeiros.json` | JSON | Sugerir produtos adequados ao perfil |
| `transacoes.csv` | CSV | Analisar padrão de gastos do cliente |

---

## Adaptações nos Dados

Foi adicionado 'Fundo Imobiliário' ao dataset de produtos_imobiliarios.

---

## Estratégia de Integração

### Como os dados são carregados?

Injetando os dados no próprio prompt ou carregando os arquivos via código:

```python
import pandas as pd
import json

#CSV
historico = pd.read_csv('data/historico_atendimento')
transacoes = pd.read_csv('data/transacoes.csv')

#JSON
with open('ddata/perfil_investidor.json', 'r') as file:
    perfil = json.load(file)

with open('ddata/produtos_financeiros.json', 'r') as file:
    produtos = json.load(file)
```

### Como os dados são usados no prompt?

Injetamos os dados da seguinte forma em nosso prompt, garantindo que o agente tenha o melhor contexto possivel (em casos mais robustos, o ideal seria carregar os dados via codigo)

DADOS DO CLIENTE =  `data/perfil_investidor.json`

HISTORICO DE TRANSACOES DO CLIENTE = `data/transacoes.csv`

HISTORICO DE ATENDIMENTO DO CLIENTE = `data/historico_atendimento.csv`

PRODUTOS DISPONIVEIS PARA ENSINO = `data/produtos_financeiros.json`


---

## Exemplo de Contexto Montado

```
Dados do Cliente:
- Nome: João Silva
- Perfil: Moderado
- Saldo disponível: R$ 5.000

Últimas transações:
- 01/11: Supermercado - R$ 450
- 03/11: Streaming - R$ 55
...
```
