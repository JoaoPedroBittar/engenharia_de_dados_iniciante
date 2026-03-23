# Pipeline ETL de Dados de Clima de São Paulo

Este projeto implementa um pipeline ETL (Extract, Transform, Load) simples para coletar dados meteorológicos de São Paulo, Brasil, utilizando a API do OpenWeatherMap. Os dados são processados e armazenados em um banco de dados PostgreSQL, com orquestração via Apache Airflow.

## Funcionalidades

- **Extração**: Coleta dados de clima atuais da API OpenWeatherMap para São Paulo.
- **Transformação**: Processa e limpa os dados extraídos (ex.: conversões de unidades, formatação).
- **Carregamento**: Insere os dados transformados em uma tabela PostgreSQL.
- **Orquestração**: Usa Apache Airflow para agendar e executar o pipeline automaticamente.

## Estrutura do Projeto

```
engenharia_de_dados_iniciante/
├── dags/
│   └── weather_dag.py          # DAG do Airflow para o pipeline
├── src/
│   ├── extract_data.py         # Módulo de extração de dados
│   ├── transform_data.py       # Módulo de transformação de dados
│   └── load_data.py            # Módulo de carregamento de dados
├── data/
│   └── weather_data.json       # Dados extraídos (temporário)
├── config/
│   ├── airflow.cfg             # Configuração do Airflow
│   └── .env                    # Variáveis de ambiente (API_KEY, credenciais DB)
├── logs/                       # Logs do Airflow
├── notebooks/
│   └── analysis_data.ipynb     # Notebook para análise dos dados
├── main.py                     # Script principal para execução local
├── docker-compose.yaml         # Configuração Docker Compose
├── pyproject.toml              # Dependências Python
└── README.md                   # Este arquivo
```

## Pré-requisitos

- Docker e Docker Compose instalados
- Conta no OpenWeatherMap para obter uma chave de API gratuita ([cadastre-se aqui](https://openweathermap.org/api))
- Python 3.8+ (para execução local)

## Instalação e Configuração

1. **Clone o repositório**:
   ```bash
   git clone <url-do-repositorio>
   cd engenharia_de_dados_iniciante
   ```

2. **Configure as variáveis de ambiente**:
   - Edite o arquivo `config/.env` e adicione sua chave da API OpenWeatherMap:
     ```
     API_KEY=sua_chave_aqui
     database=weather_data
     user=joao_pedro_bittar
     password=sua_senha
     ```

3. **Instale as dependências (para execução local)**:
   ```bash
   pip install -r requirements.txt  # ou via pyproject.toml se usar poetry/pip-tools
   ```

## Como Executar

### Usando Docker Compose (Recomendado)

1. **Inicie os serviços**:
   ```bash
   docker-compose up -d
   ```

2. **Acesse o Airflow**:
   - Abra o navegador em `http://localhost:8080`
   - Usuário: `airflow`
   - Senha: `airflow`

3. **Ative o DAG**:
   - No painel do Airflow, localize o DAG `youtube_weather_pipeline` e ative-o.
   - O pipeline será executado automaticamente a cada hora (conforme agendado).

4. **Execute manualmente (opcional)**:
   - Clique em "Trigger DAG" para executar imediatamente.

### Execução Local (Sem Docker)

1. **Certifique-se de que o PostgreSQL está rodando** (configure localmente ou via Docker separado).

2. **Execute o script principal**:
   ```bash
   python main.py
   ```

   Isso executará o pipeline completo: extração, transformação e carregamento.

## Análise de Dados

Use o notebook Jupyter `notebooks/analysis_data.ipynb` para analisar os dados coletados. Para executá-lo:

```bash
jupyter notebook notebooks/analysis_data.ipynb
```

## Logs e Monitoramento

- Logs do Airflow estão em `logs/`.
- Dados processados ficam em `data/`.
- Monitore execuções via a UI do Airflow.
