# TCC UWine

Projeto Integrador do curso de Ciência de Dados da UVV, desenvolvido por **George Lucas**. O projeto analisa as vendas da
vinícola fictícia **UWine**, com cerca de 1,12 milhão de notas fiscais, em duas partes:

| Parte | Notebook | Conteúdo |
|---|---|---|
| 1 | [`TCC_UWine_Parte1_George_Lucas.ipynb`](TCC_UWine_Parte1_George_Lucas.ipynb) | Tamanho ideal da amostra, outliers, testes de hipóteses, estatística descritiva e pesquisa de satisfação |
| 2 | [`TCC_UWine_Parte2_George_Lucas.ipynb`](TCC_UWine_Parte2_George_Lucas.ipynb) | Modelos de regressão, clusterização e classificação |

Os dois notebooks já estão salvos com todos os resultados e podem ser lidos aqui no GitHub, sem executar nada.

## Parte 1: amostragem e estatística

- **A1:** tamanho ideal da amostra estratificada (bootstrap e alocação de Neyman), outliers e testes de hipóteses;
- **A2:** estatística descritiva das variáveis quantitativas e qualitativas;
- **A3:** resultado da pesquisa de satisfação.

Principais resultados:

- O tamanho ideal é de **30.100 notas fiscais**, divididas entre os planos pela alocação de Neyman
  (11.542 ESSENTIAL, 6.650 VIP e 11.908 PRIME).
- A renda é a variável mais associada ao plano e ao gasto: cada compra corresponde a uma parte da renda, de 4% a 18%.
- Na pesquisa de satisfação, 80,7% dos clientes ficaram satisfeitos, com IC de 95% de 80,1% a 81,2%.

## Parte 2: aprendizado de máquina

Treino, validação e teste têm o tamanho ideal da Parte 1 (30.100 notas fiscais cada). Uma quarta amostra, com a
composição real dos planos, testa cada modelo na população.

- **A1:** regressor do gasto por compra (`TOTAL (R$)`);
- **A2:** clusterizador dos clientes, sem usar o gasto e o plano;
- **A3:** classificador do plano (`TIPO DA CONTA`), com testes de vazamento de informação.

Principais resultados:

| Modelo | Resultado no teste |
|---|---|
| Regressor (linear do log do gasto no log da renda) | R² de 0,773 na escala log e 0,694 em reais, o máximo possível com os dados |
| Clusterizador (K-means) | 3 segmentos de renda, silhueta de 0,897; coincidem com os planos em 97,0% da base |
| Classificador (Decision Tree, só com a renda) | 97,1% de acerto, a 0,0009 do teto estimado só com a renda |

O gasto e a nota de satisfação ficaram fora do classificador: os testes de hipóteses não encontraram informação do
gasto sobre o plano além da renda, e as duas variáveis só existem depois da compra.

## Arquivos

| Arquivo | Conteúdo |
|---|---|
| `TCC_UWine_Parte1_George_Lucas.ipynb` | Notebook da Parte 1 |
| `TCC_UWine_Parte2_George_Lucas.ipynb` | Notebook da Parte 2 |
| `table26.csv` | Base de dados usada nas duas partes |
| `requirements.txt` | Bibliotecas Python e versões usadas |

## Como executar

Requisitos: Python 3.12 e pelo menos 4 GB de memória RAM livre.

```bash
git clone <endereço deste repositório>
cd <pasta do repositório>
python -m venv .venv
source .venv/bin/activate          # no Windows: .venv\Scripts\activate
pip install -r requirements.txt jupyter
jupyter notebook
```

Abra o notebook desejado e use **Kernel → Restart & Run All**. Os dois notebooks leem o `table26.csv` da mesma pasta.
A Parte 1 leva alguns minutos; a Parte 2, cerca de 6 minutos.

Os sorteios usam semente fixa, então a execução reproduz os mesmos resultados. As versões em `requirements.txt` são
as usadas na execução salva; outras versões podem gerar pequenas diferenças nos números.
