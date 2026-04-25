# Projeto-tech-challenge-fase-1---BI
Postagem de todas as medidas e criações realizadas no BI
# Medidas DAX e Estrutura Analítica - Projeto Olist (Power BI)

## 📌 Objetivo
Este arquivo documenta as principais medidas e colunas calculadas utilizadas no dashboard analítico para avaliação do impacto dos atrasos na satisfação dos clientes.

---

# 📊 KPIs e Métricas

## Total Pedidos
```DAX
Total Pedidos =
COUNT(base_final_olist[order_id])
```

---

## Pedidos Atrasados
```DAX
Pedidos Atrasados =
CALCULATE(
    COUNT(base_final_olist[order_id]),
    base_final_olist[atraso] = 1
)
```

---

## % Atraso
```DAX
% Atraso =
DIVIDE(
    [Pedidos Atrasados],
    [Total Pedidos],
    0
)
```

---

## Nota Média
```DAX
Nota Média =
AVERAGE(base_final_olist[review_score]) / 10
```

---

## Qtd Sellers
```DAX
Qtd Sellers =
DISTINCTCOUNT(base_final_olist[seller_id])
```

---

# 🧩 Colunas Calculadas

## Status Entrega
```DAX
Status Entrega =
IF(
    base_final_olist[atraso] = 1,
    "Atrasado",
    "No Prazo"
)
```

---

## Faixa Tempo
```DAX
Faixa Tempo =
SWITCH(
    TRUE(),
    base_final_olist[tempo_entrega] <= 5, "0-5 dias",
    base_final_olist[tempo_entrega] <= 10, "6-10 dias",
    base_final_olist[tempo_entrega] <= 15, "11-15 dias",
    base_final_olist[tempo_entrega] <= 20, "16-20 dias",
    base_final_olist[tempo_entrega] <= 30, "21-30 dias",
    base_final_olist[tempo_entrega] <= 45, "31-45 dias",
    base_final_olist[tempo_entrega] <= 60, "46-60 dias",
    "61+ dias"
)
```

---

## Ordem Faixa Tempo
```DAX
Ordem Faixa =
SWITCH(
    base_final_olist[Faixa Tempo],
    "0-5 dias", 1,
    "6-10 dias", 2,
    "11-15 dias", 3,
    "16-20 dias", 4,
    "21-30 dias", 5,
    "31-45 dias", 6,
    "46-60 dias", 7,
    8
)
```

---

## Faixa Review
```DAX
Faixa Review =
SWITCH(
    TRUE(),
    base_final_olist[review_score] <= 20, "1-2",
    base_final_olist[review_score] = 30, "3",
    base_final_olist[review_score] = 40, "4",
    "5"
)
```

---

## Ordem Review
```DAX
Ordem Review =
SWITCH(
    base_final_olist[Faixa Review],
    "1-2", 1,
    "3", 2,
    "4", 3,
    "5", 4
)
```

---

# 🌎 Variáveis Analíticas

## Região
(derivada a partir do estado do cliente)

- Norte
- Nordeste
- Centro-Oeste
- Sudeste
- Sul

Utilizada para:
- análise regional de atrasos
- seller por região
- comparação geográfica

---

# 📈 Principais Análises Desenvolvidas

- Distribuição do tempo de entrega  
- Evolução temporal dos atrasos  
- Taxa de atraso por região  
- Taxa de atraso por seller  
- Impacto dos atrasos na satisfação dos clientes  
- Distribuição das avaliações por status de entrega  

---


