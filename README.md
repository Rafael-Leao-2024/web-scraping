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
   git clone https://github.com/seuusuario/seurepositorio.git

2. Instale as dependências do projeto:
   pip install -r requirements.txt

3. Certifique-se de ter uma versão do Chrome instalada no seu sistema.

4. Coloque o arquivo `base.xlsx` no mesmo diretório do código. Este arquivo deve conter as placas que serão consultadas no formato correto.

5. Execute o código:
   python nome_do_arquivo.py

6. O resultado será salvo como `output.xlsx`.

## Estrutura do Projeto

├── base.xlsx                 # Arquivo Excel com as placas a serem consultadas
├── nome_do_arquivo.py         # Script principal de automação
├── output.xlsx                # Arquivo Excel gerado com os resultados
└── README.md                  # Descrição do projeto

## Dependências

- selenium
- webdriver_manager
- beautifulsoup4
- pandas
- openpyxl

Para instalar as dependências, você pode usar o seguinte comando:
pip install selenium webdriver_manager beautifulsoup4 pandas openpyxl

## Contribuições

Sinta-se à vontade para abrir issues e enviar pull requests.

