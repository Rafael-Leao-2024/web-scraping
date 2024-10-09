# Projeto de Automação com Selenium

Este projeto automatiza o processo de extração de dados de um site utilizando Selenium para navegação e BeautifulSoup para análise de conteúdo. O projeto lê uma lista de placas a partir de uma planilha Excel, realiza pesquisas no site e extrai informações como CPF/CNPJ e nome do proprietário, gerando um arquivo Excel como resultado.

## Funcionalidades

- Automação de login em um sistema web.
- Leitura de uma planilha com placas de veículos.
- Busca automática de dados relacionados às placas no site.
- Extração de informações como CPF/CNPJ, nome do proprietário e loja.
- Criação de um DataFrame em pandas e exportação dos dados em Excel.
- Classificação dos dados e categorização de placas como 'NOVOS' ou 'USADOS'.

## Tecnologias Utilizadas

- **Python 3.x**: Linguagem de programação utilizada.
- **Selenium**: Para automação da navegação no site.
- **BeautifulSoup**: Para extração e parsing do HTML.
- **pandas**: Para manipulação de dados.
- **webdriver_manager**: Para gerenciar o driver do navegador Chrome.
- **Excel**: Para leitura e escrita dos dados.

## Como Executar o Projeto

1. Clone este repositório:
   ```bash
   git clone https://github.com/seuusuario/seurepositorio.git


 Bate-papoGPT

Você disse:
Tenho esse código { "cells": [ { "cell_type": "code", "execution_count": null, "metadata": {}, "outputs": [], "source": [ "from selenium import webdriver\n", "from webdriver_manager.chrome import ChromeDriverManager\n", "from selenium.webdriver.common.by import By\n", "from bs4 import BeautifulSoup\n", "import time\n", "import pandas as pd" ] }, { "cell_type": "code", "execution_count": null, "metadata": {}, "outputs": [], "source": [ "# Criando Navegador e maximizando a tela\n", "navegador = webdriver.Chrome(ChromeDriverManager().install())\n", "navegador.maximize_window()\n", "navegador.get('https://sistemacbm.com/#/dashboard/')\n", "time.sleep(15)" ] }, { "cell_type": "code", "execution_count": null, "metadata": {}, "outputs": [], "source": [ "#preenchendo campo de usuário com cpf\n", "elemento = navegador.find_element(By.XPATH, '//*[@id=\"novo_login-columns\"]/div[2]/div/section/form/div[1]/div/input')\n", "elemento.send_keys('user_name')" ] }, { "cell_type": "code", "execution_count": null, "metadata": {}, "outputs": [], "source": [ "#preenchendo campo de senha com password \n", "elemento = navegador.find_element(By.XPATH, '//*[@id=\"novo_login-columns\"]/div[2]/div/section/form/div[2]/div/input')\n", "elemento.send_keys('password')\n", "time.sleep(5)" ] }, { "cell_type": "code", "execution_count": null, "metadata": {}, "outputs": [], "source": [ "#clicando no botão entrar \n", "elemento = navegador.find_element(By.XPATH, '//*[@id=\"novo_login-columns\"]/div[2]/div/section/form/div[3]/button')\n", "elemento.click()\n", "time.sleep(20)" ] }, { "cell_type": "code", "execution_count": null, "metadata": {}, "outputs": [], "source": [ "# lendo a base de dados e criando lista vazia \n", "dados = pd.read_excel(\"base.xlsx\")\n", "colunas = ['Placa','Proprietário', 'CPF/CNPJ Proprietário']\n", "placas = dados[colunas]\ n", "lista_planilha = []" ] }, { "cell_type": "código", "execution_count": null, "metadados": {},"outputs": [], "source": [ "for placa in placas.Placa.head(5):\n", " # clicando em autorização\n", " elemento = navegador.find_element(By.XPATH, '//*[@id=\"main\"]/div[2]/div/section/div[1]/div[1]/div/article[1]/aside/ul[1]/li[1]/a[1]')\n", " navegador.execute_script(\"arguments[0].scrollIntoView(false);\", elemento) \n", " time.sleep(5)\n", " elemento.click()\n", " time.sleep(6)\n", " \n", " # clicando em filtrar\n", " elemento = navegador.find_element(By.TAG_NAME, 'button')\n", " time.sleep(2)\n", " elemento.click()\n", " time.sleep(5)\n", "\n", " # inserindo dígitos alfanuméricos da placa\n", " elemento = navegador.find_element(By.XPATH, '//*[@id=\"main\"]/div[2]/div/div/form/div[1]/div[4]/div/div/input')\n", " time.sleep(5)\n", " \n", " # limpar o campo de texto e escrevenver novo dado\n", " elemento.clear()\n", " time.sleep(5)\n", " elemento.send_keys(placa)\n", " time.sleep(5)\n", "\n", " # clicando no botão de filtrar\n", " \n", " elemento = navegador.find_element(By.XPATH, '//*[@id=\"main\"]/div[2]/div/div/form/div[3]/div/button[1]/span[2]')\n", " elemento.click()\n", " time.sleep(3)\n", "\n", " # diminuir a tela e clicar na lupa\n", " time.sleep(2)\n", " elemento = navegador.find_element(By.XPATH, '//*[@id=\"main\"]/div[2]/div/div/div/table/tbody/tr/td[12]')\n", " navegador.execute_script(\"arguments[0].scrollIntoView(true);\", elemento) \n", " time.sleep(2)\n", " elemento.click()\n", "\n", " # extraindo fonte html da página atual com Selenium e BeautifulSoup\n", " time.sleep(5)\n", " page_content = navegador.page_source\n", " sopa = BeautifulSoup(page_content, 'html.parser')\n", "\n", " texto_page = sopa.get_text()\n", " lista = texto_page.split()\n", " indice = lista.index('CPF/CNPJ')\n", " \n", " #nome_loja = lista[lista.index('PagadorEditar Observação') + 1 :238]\n", " nome_loja = navegador.find_elements(By.CLASS_NAME, 'leitura')[11].text\n", " \n", " #nome_loja = ' '.join(nome_loja) \n", " cpf_cnpj = lista[indice + 3]\n"," nome = lista[índice + 8] + ' ' + lista[índice + 9] + ' ' + lista[índice + 10] + ' ' + lista[índice + 11] + ' ' + lista[índice + 12] + ' ' + lista[índice + 13]\n", " nome = nome.split('Cidade')[0]\n", " data = lista[112]\n", " \n", " #voltando ao menu home \n", " elemento = navegador.find_element(By.XPATH, '//*[@id=\"main-sidebar\"]/nav/ul[1]/li/a')\n" , " elemento.click()\n", " time.sleep(3)\n", " \n", " print(data, placa, cpf_cnpj, nome, nome_loja)\n", " lista_planilha.append([ dados, placa, nome, nome_loja])\n", " " ] }, { "cell_type": "code", "execution_count": null, "metadata": {}, "outputs": [], "source": [ "# tamanho da lista estrada da automação\n", "len(lista_planilha)" ] }, { "cell_type": "code", "execution_count": null, "metadata": {}, "outputs": [], "source": [ "# Criando o DataFrame após a raspagem de dados \n", "tabela = pd.DataFrame(lista_planilha, columns=['data', 'placa', 'nome', 'nome_loja'])" ] }, { " cell_type": "código", "execution_count": null, "metadata": {}, "outputs": [], "source": [ "display(tabela.head())" ] }, { "cell_type": "code", "execution_count": null, "metadata": {}, "outputs": [], "source": [ "# Classificando a tabela pela coluna 'Nome' em ordem alfabética\ n", "tabela_sorted = tabela.sort_values(by='data', ignore_index=True)" ] }, { "cell_type": "code", "execution_count": null, "metadata": {}, "outputs": [], "source": [ "#criando uma coluna de categoria de 'NOVOS/USADOS'\n", "tabela_sorted['USADOS/NOVOS'] = tabela_sorted['placa'].apply(lambda x: 'NOVOS' if 'SN' em x else 'USADOS').str.lower()" ] }, { "cell_type": "code", "execution_count": null, "metadados": {}, "saídas": [], "fonte": [ "display(tabela_sorted.head())" ] }, { "tipo_de_célula": "código", "contagem_de_execução": nulo, "metadados" : {}, "saídas": [], "fonte": [ "tabela_sorted.nome_loja.value_counts()" ] }, { "tipo_célula": "código","execution_count": null, "metadata": {}, "outputs": [], "source": [ "# Salvando tabela em excel\n", "tabela_sorted.to_excel('output.xlsx', index=False)" ] }, { "cell_type": "code", "execution_count": null, "metadata": {}, "outputs": [], "source": [ "# Finalizando o navegador \n", "navegador.close()" ] } ], "metadata": { "kernelspec": { "display_name": "Python 3 (ipykernel)", "language": "python", "name": "python3" }, "language_info": { "codemirror_mode": { "name": "ipython", "version": 3 }, "file_extension": ".py", "mimetype": "text/x-python", "name": "python", "nbconvert_exporter": "python", "pygments_lexer": "ipython3", "version": "3.11.5" } }, "nbformat": 4, "nbformat_minor": 2 } E quero um leia-me para ficar bem apresentado no git hub
O ChatGPT disse:
ChatGPT

Memória atualizada
Aqui está um modelo de README para seu projeto de automação com Selenium e Python:

Projeto de Automação com Selenium
Este projeto automatiza o processo de remoção de dados de um site utilizando Selenium para navegação e BeautifulSoup para análise de conteúdo. O projeto lê uma lista de placas a partir de uma planilha Excel, realiza pesquisas no site e extrai informações como CPF/CNPJ e nome do proprietário, gerando um arquivo Excel como resultado.

Funcionalidades
Automação de login em um sistema web.
Leitura de uma planilha com placas de veículos.
Busca automática de dados relacionados às placas no site.
Extração de informações como CPF/CNPJ, nome do proprietário e loja.
Criação de um DataFrame em pandas e exportação de dados em Excel.
Classificação dos dados e categorização de placas como 'NOVOS' ou 'USADOS'.
Tecnologias Utilizadas
Python 3.x : Linguagem de programação utilizada.
Selenium : Para automação da navegação no site.
BeautifulSoup : Para remoção e análise do HTML.
pandas : Para manipulação de dados.
webdriver_manager : Para gerenciar o driver do navegador Chrome.
Excel : Para leitura e escrita dos dados.
Como Executar o Projeto
Clonar este repositório:

bater

Copiar código
git clone https://github.com/seuusuario/seurepositorio.git
Instale as dependências do projeto:

bater

Copiar código
pip install -r requirements.txt
-se de ter uma versão do Chrome instalada no seu sistema.

Coloque o arquivo base.xlsxno mesmo diretório do código. Este arquivo deve conter placas que serão consultadas no formato correto.

Execute o código:

bater

Copiar código
python nome_do_arquivo.py
O resultado será salvo como output.xlsx.

Estrutura do Projeto
bater

Copiar código
├── base.xlsx                 # Arquivo Excel com as placas a serem consultadas
├── nome_do_arquivo.py         # Script principal de automação
├── output.xlsx                # Arquivo Excel gerado com os resultados
└── README.md                  # Descrição do projeto
Dependências
selênio
gerenciador de driver web
sopabela4
pandas
openpyxl
Para instalar as dependências, você pode usar o seguinte comando:

bater

Copiar código
pip install selenium webdriver_manager beautifulsoup4 pandas openpyxl
Contribuições
Sinta-se à vontade para abrir problemas e enviar pull requests.

Esse README segue as melhores práticas de documentação para facilitar a leitura e execução do projeto.






Você disse:
Quero isso no console para eu copiar e colar lá
O ChatGPT disse:
ChatGPT
Aqui está o README formatado para você copiar e colar diretamente no console:

redução de preço

Copiar código
# Projeto de Automação com Selenium

Este projeto automatiza o processo de extração de dados de um site utilizando Selenium para navegação e BeautifulSoup para análise de conteúdo. O projeto lê uma lista de placas a partir de uma planilha Excel, realiza pesquisas no site e extrai informações como CPF/CNPJ e nome do proprietário, gerando um arquivo Excel como resultado.

## Funcionalidades

- Automação de login em um sistema web.
- Leitura de uma planilha com placas de veículos.
- Busca automática de dados relacionados às placas no site.
- Extração de informações como CPF/CNPJ, nome do proprietário e loja.
- Criação de um DataFrame em pandas e exportação dos dados em Excel.
- Classificação dos dados e categorização de placas como 'NOVOS' ou 'USADOS'.

## Tecnologias Utilizadas

- **Python 3.x**: Linguagem de programação utilizada.
- **Selenium**: Para automação da navegação no site.
- **BeautifulSoup**: Para extração e parsing do HTML.
- **pandas**: Para manipulação de dados.
- **webdriver_manager**: Para gerenciar o driver do navegador Chrome.
- **Excel**: Para leitura e escrita dos dados.

## Como Executar o Projeto

1. Clone este repositório:
   ```bash
   git clone https://github.com/seuusuario/seurepositorio.git
Instale as dependências do projeto:

bater

Copiar código
pip install -r requirements.txt
-se de ter uma versão do Chrome instalada no seu sistema.

Coloque o arquivo base.xlsxno mesmo diretório do código. Este arquivo deve conter placas que serão consultadas no formato correto.

Execute o código:

bater

Copiar código
python nome_do_arquivo.py
O resultado será salvo como output.xlsx.

Estrutura do Projeto
bater

Copiar código
├── base.xlsx                 # Arquivo Excel com as placas a serem consultadas
├── nome_do_arquivo.py         # Script principal de automação
├── output.xlsx                # Arquivo Excel gerado com os resultados
└── README.md                  # Descrição do projeto
Dependências
selênio
gerenciador de driver web
sopabela4
pandas
openpyxl
Para instalar as dependências, você pode usar o seguinte comando:

bater

Copiar código
pip install selenium webdriver_manager beautifulsoup4 pandas openpyxl
Contribuições
Sinta-se à vontade para abrir problemas e enviar pull requests.

perl

Copiar código

Agora é só copiar e colar no 


   
