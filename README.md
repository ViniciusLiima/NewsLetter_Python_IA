# Projeto de Newsletter Diária de Cotação de Moedas 📈📨
Este projeto Python automatiza a criação e o envio de uma newsletter diária sobre a cotação das moedas USD (Dólar Americano) e JPY (Iene Japonês) em relação ao BRL (Real Brasileiro).
<br><br>
Ele utiliza APIs para obter dados em tempo real, processa essas informações e gera um relatório personalizado (texto + gráfico) que é enviado por e-mail para um assinante.

## 📑 Fluxo
<img width="1277" height="465" alt="Image" src="https://github.com/user-attachments/assets/6bd58348-95fa-4d24-8bf8-6b1a405071ac" />

## ⚙️ Como Funciona

O script executa uma rotina diária que segue as seguintes etapas:

1. **Coleta de Dados (Camada Bronze) 🥉:** Obtém as taxas de câmbio mais recentes de uma API e salva os dados brutos em um arquivo JSON.

2. **Normalização dos Dados (Camada Silver) 🥈:** Lê os dados brutos, remove valores nulos ou negativos, e adiciona informações como a moeda base (`BRL`) e um carimbo de data/hora. Os dados são salvos em um novo arquivo JSON.

3. **Filtragem de Dados (Camada Gold) 🥇:** Filtra os dados da camada Silver, mantendo apenas as cotações para USD e JPY, e salva o resultado em um arquivo Parquet para armazenamento otimizado.

4. **Geração de Gráfico 📊:** Cria um gráfico de barras com as cotações do USD e JPY, salvando a imagem em formato PDF.

5. **Criação de Conteúdo com IA 🤖:** Utiliza a API do Google Gemini para gerar um texto de newsletter personalizado, com base nos dados filtrados na etapa anterior. O texto inclui uma análise das cotações e links para notícias financeiras relevantes.

6. **Envio do E-mail 📧:** Envia a newsletter final para um destinatário específico. O e-mail inclui o texto gerado pela IA e o gráfico de cotação como anexo.

## 🚀 Setup do Projeto

### Pré-requisitos

🐍 Certifique-se de ter o Python instalado (versão 3.6 ou superior).

### Instalação das Bibliotecas

Para executar o projeto, você precisará instalar as bibliotecas listadas. Você pode fazer isso usando o `pip` e um arquivo `requirements.txt`. Crie um arquivo chamado `requirements.txt` com o seguinte conteúdo:
```
pandas
requests
matplotlib
google-generativeai
pyyaml
smtplib
```

Em seguida, execute o comando:

`pip install -r requirements.txt`


### 🗂️ Estrutura de Diretórios

O projeto segue uma arquitetura de camadas de dados (Bronze, Silver e Gold) para organizar os arquivos de cotação. O script criará automaticamente os seguintes diretórios na primeira execução, caso eles ainda não existam:

* `01_bronze`

* `02_silver`

* `03_gold`

* `04_graphs`

* `05_ia_responses`

### ✉️ Configuração das APIs e E-mail

O projeto utiliza um arquivo de configuração `config.yaml` para gerenciar as chaves de API e as credenciais de e-mail.

Crie um arquivo chamado `config.yaml` na raiz do projeto e preencha-o com suas informações, seguindo este formato:
```
api_keys:
  exchangerate_api_key: "SUA_CHAVE_AQUI"
  gemini_api_key: "SUA_CHAVE_AQUI"

ia_model:
  gemini_model: "gemini-2.5-flash"

email:
  meu_email: "seu_email@gmail.com"
  minha_senha_app: "SUA_SENHA_DE_APP_AQUI"
  email_destinatario: "destinatario@exemplo.com"
```

* **`exchangerate_api_key`**: Obtenha sua chave de API gratuita no site [ExchangeRate-API.com](https://www.exchangerate-api.com/).

* **`gemini_api_key`**: Gere sua chave de API para o Google Gemini na [AI Studio](https://aistudio.google.com/app/apikey).

* **`gemini_model`**: O modelo de IA usado. O código já vem configurado com `'gemini-2.5-flash'`, que é uma boa opção para a tarefa.

* **`meu_email`**: O endereço de e-mail que enviará a newsletter. Para Gmail, você precisará de uma senha de aplicativo.

* **`minha_senha_app`**: Se você usa Gmail, você precisa criar uma [senha de aplicativo](https://support.google.com/accounts/answer/185833?hl=en) em vez de usar sua senha principal.

* **`email_destinatario`**: O endereço de e-mail do assinante que receberá a newsletter.

## 🏃‍♀️ Como Executar

Com todas as dependências instaladas e o arquivo `config.yaml` devidamente configurado, você pode executar o script principal diretamente do terminal:
```
python projeto_python_newsletter.py
```
Após a execução, o script criará a newsletter, gerará o gráfico e enviará o e-mail.
