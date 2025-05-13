import pandas as pd

# Series
pd.Series(data=5)

lista_nomes = 'Howard Ian Peter Jonah Kellie'.split()
pd.Series(lista_nomes)

dados = {
    'nome1': 'Howard',
    'nome2': 'Ian',
    'nome3': 'Peter',
    'nome4': 'Jonah',
    'nome5': 'Kellie',
}
pd.Series(dados)

cpfs = """
111.111.111-11 222.222.222-22 333.333.333-33
444.444.444-44 555.555.555-55
""".split()
series_dados = pd.Series(lista_nomes, index=cpfs)
series_dados.loc['111.111.111-11']

# Extraindo informações
series_dados = pd.Series([10.2, -1, None, 15, 23.4])
print('Quantidade de linhas = ', series_dados.shape)
print('Tipo de dados', series_dados.dtypes)
print('Os valores são únicos?', series_dados.is_unique)
print('Existem valores nulos?', series_dados.hasnans)
print('Quantos valores existem?', series_dados.count())
print('Qual o menor valor?', series_dados.min())
print('Qual o maior valor?', series_dados.max())
print('Qual a média aritmética?', series_dados.mean())
print('Qual o desvio padrão?', series_dados.std())
print('Qual a mediana?', series_dados.median())

# DataFrame
lista_nomes = 'Howard Ian Peter Jonah Keltie'.split()
lista_cpfs = """
111.111.111-11 222.222.222-22 333.333.333-33
444.444.444-44 555.555.555-55
""".split()

dados = {
    "nomes": "Howard Ian Peter Jonah Kellie".split(),
    "cpfs": """111.111.111-11 222.222.222-22 333.333.333-33
    444.444.444-44 555.555.555-55""".split(),
    "emails": """risus.varius@dictumPhasellusin.ca Nunc@vulputate.ca
    fames.ac.turpis@cursusa.org non@felisullamcorper.org
    eget.dictum.placerat@necluctus.co.uk""".split(),
    "idades": [32, 22, 25, 29, 38],
}
df_dados = pd.DataFrame(dados)

# Extraindo informações de um DataFrame
print(df_dados.info())
print('Quantidade de linhas e colunas = ', df_dados.shape)
print('Tipo de dados:\n', df_dados.dtypes)
print('Qual o menor valor de cada coluna?\n', df_dados.min())
print('Qual o maior valor?\n', df_dados.max())
print('Resumo:\n', df_dados.describe())

dados = { "idades": [32, 22, 25, 29, 38] }
df_dados = pd.DataFrame(dados)
print('Qual a média aritmética?\n', df_dados.mean())
print('Qual o desvio padrão?\n', df_dados.std())
print('Qual a mediana?\n', df_dados.median())

# Seleção de colunas em um DataFrame
dados = {
    "nomes": "Howard Ian Peter Jonah Kellie".split(),
    "cpfs": """111.111.111-11 222.222.222-22 333.333.333-33
    444.444.444-44 555.555.555-55""".split(),
    "emails": """risus.varius@dictumPhasellusin.ca Nunc@vulputate.ca
    fames.ac.turpis@cursusa.org non@felisullamcorper.org
    eget.dictum.placerat@necluctus.co.uk""".split(),
    "idades": [32, 22, 25, 29, 38],
}
df_dados = pd.DataFrame(dados)
df_dados["idades"]
df_dados["idades"].mean()

colunas = ['nomes', 'cpfs']
df_duas_colunas = df_dados[colunas]
type(df_duas_colunas)

# Requests e Beautiful Soup
import requests
from bs4 import BeautifulSoup

texto_string = requests.get('https://www.nytimes.com/interactive/2017/06/23/opinion/trumps-lies.html').text
bsp_texto = BeautifulSoup(texto_string, 'html.parser')
lista_noticias = bsp_texto.find_all('span', attrs={'class':'short-desc'})

dados = []
for noticia in lista_noticias:
    data = noticia.contents[0].text.strip() + ', 2017'
    comentario = noticia.contents[1].strip().replace("“", '').replace("”", '')
    explicacao = noticia.contents[2].text.strip().replace("(", '').replace(")", '')
    url = noticia.find('a')['href']
    dados.append((data, comentario, explicacao, url))

df_noticias = pd.DataFrame(dados, columns=['data', 'comentário', 'explicação', 'url'])

# Failed Bank List
url = 'https://www.fdic.gov/resources/resolutions/bank-failures/failed-bank-list/'
dfs = pd.read_html(url)
df_bancos = dfs[0][0:4]
