# FinInsight AI: Análise Inteligente de Relatórios Financeiros
Wiki criado para apresentar informações sobre o projeto final de programação de software em 2025.1 do doutorado na PUC-Rio.

# Breve Descrição

O FinInsight AI é uma plataforma de análise automatizada de relatórios financeiros trimestrais (em PDF) que integra técnicas de Recuperação Aumentada por Geração (RAG) e Modelos de Linguagem (LLMs). Sua principal função é extrair, processar e correlacionar dados quantitativos (balanços, indicadores) e qualitativos (textos explicativos) para gerar insights estratégicos, como tendências de mercado, riscos operacionais e oportunidades de investimento.

# Visão de Projeto

# Cenário Positivo 1 (i.e. cenário que dá certo)

Maria, uma analista financeira, usa o FinAI Insights para rapidamente extrair o lucro líquido e os custos operacionais de um relatório trimestral em PDF. O sistema processa o documento, responde com precisão e cita as fontes, permitindo que Maria crie um resumo rápido e detalhado para seu gerente.

# Cenário Positivo 2

João, um gestor de riscos, carrega múltiplos relatórios anuais de subsidiárias no FinAI Insights. Ele pergunta sobre riscos operacionais e o sistema apresenta uma lista concisa e referenciada para cada empresa, agilizando significativamente a consolidação de relatórios de risco.


# Cenário Negativo 1 (i.e. cenário que expõe uma limitação conhecida e esperada do programa)

Ana, uma estudante, busca detalhes de empréstimos em um relatório, mas o FinAI Insights informa que a informação não está presente no documento. Ana verifica o PDF e confirma a ausência da granularidade esperada, compreendendo que a limitação é do conteúdo da fonte, não do sistema.

# Cenário Negativo 2

Carlos, um consultor, tenta extrair dados de uma tabela em um PDF antigo, mas o FinAI Insights não consegue. Ele percebe que a tabela é uma imagem e não texto selecionável, o que impede a extração de dados pelo sistema, revelando uma limitação na leitura de PDFs não textuais.

# Documentação Técnica do Projeto

Esta seção oferece informações para desenvolvedores e colaboradores interessados em entender e, potencialmente, reutilizar ou estender o FinAI Insights.

1. Especificação de Requisitos Funcionais e Não-Funcionais do Software

Requisitos Funcionais:

* F1.1: Upload de Documentos: O sistema deve permitir o upload de um ou múltiplos arquivos PDF de relatórios financeiros.
* F1.2: Extração de Conteúdo: O sistema deve extrair texto (quantitativo e qualitativo) dos PDFs carregados.
* F1.3: Geração de Embeddings: O sistema deve gerar representações vetoriais (embeddings) dos chunks de texto extraídos.
* F1.4: Armazenamento Vetorial: O sistema deve armazenar os embeddings em um banco de dados vetorial para busca eficiente.
* F1.5: Interface de Consulta: O sistema deve fornecer uma interface de texto para o usuário inserir perguntas em linguagem natural.
* F1.6: Recuperação de Contexto: O sistema deve recuperar os chunks de texto mais relevantes do banco de dados vetorial com base na pergunta do usuário.
* F1.7: Geração de Resposta: O sistema deve utilizar um LLM para gerar uma resposta concisa e relevante com base na pergunta do usuário e no contexto recuperado.
* F1.8: Citação de Fontes: A resposta gerada deve incluir referências aos documentos originais (nome do arquivo, número da página) de onde o contexto foi retirado.
* F1.9: Diagnóstico da API: O sistema deve verificar e exibir o status de conexão com a API Gemini e listar os modelos de chat e embedding disponíveis.
* F1.10: Seleção Automática de Modelo: O sistema deve selecionar automaticamente o modelo de LLM e Embedding mais adequado.

Requisitos Não-Funcionais:

* NF2.1: Performance: O processamento de documentos e a geração de respostas devem ser eficientes, com tempos de resposta adequados para análises rápidas.
* NF2.2: Escalabilidade: A arquitetura deve permitir o escalonamento para processar um número maior de documentos e atender a múltiplos usuários.
* NF2.3: Confiabilidade: O sistema deve ser robusto a falhas, com tratamento de erros adequado.
* NF2.4: Segurança: A chave de API deve ser gerenciada de forma segura.
* NF2.5: Usabilidade: A interface do usuário deve ser intuitiva e fácil de usar para o público-alvo.
* NF2.6: Manutenibilidade: O código deve ser modular, bem comentado e fácil de entender e modificar para futuras atualizações.
* NF2.7: Adaptabilidade: A arquitetura deve ser flexível para integrar novos modelos de LLM e embeddings, bem como diferentes formatos de documentos.

2. Descrição da Arquitetura do Software

O FinAI Insights segue uma arquitetura baseada em Retrieval Augmented Generation (RAG), implementada como uma aplicação web utilizando Streamlit.

Camada de Interface (Frontend):

Desenvolvida com Streamlit, fornece interface de usuário interativa (upload de arquivos, caixa de texto para perguntas, exibição de respostas e diagnósticos).

Camada de Processamento de Documentos:

* PyMuPDFLoader: Biblioteca utilizada para carregar e extrair texto de arquivos PDF.
* RecursiveCharacterTextSplitter (LangChain): Responsável por dividir o texto extraído em "chunks", otimiza o processo de embedding e recuperação, com controle de chunk_size e chunk_overlap.

Camada de Embedding e Banco de Dados Vetorial:

* GoogleGenerativeAIEmbeddings: Utiliza o modelo de embedding do Google Gemini (models/embedding-001 ou similar) para transformar os chunks de texto em vetores numéricos (embeddings).
* ChromaDB: Um banco de dados vetorial leve e persistente (chromadb.PersistentClient) utilizado para armazenar os embeddings e seus metadados.

  
Camada de Modelo de Linguagem (LLM) e Orquestração RAG:

* ChatGoogleGenerativeAI (LangChain): Interface para o modelo de linguagem grande (LLM) do Google Gemini para a parte de geração de respostas.

RetrievalQA que orquestra o fluxo RAG:

* Recebe a pergunta do usuário.
* Transforma a pergunta em embedding.
* Usa o retriever (configurado para k=10) para buscar os 10 chunks mais semanticamente relevantes do ChromaDB.
* "Stuffa" (combina) esses chunks recuperados com a pergunta do usuário em um único prompt de contexto.
* Envia o prompt completo para o LLM.
* Recebe a resposta do LLM.
* Retorna a resposta (e as fontes, se disponíveis).

Configuração de API:

* os.environ['GOOGLE_API_KEY'] = st.secrets['GOOGLE_API_KEY']: Gerencia a chave de API de forma segura através do Streamlit Secrets.
* google.generativeai.configure: Inicializa a API do Gemini.
* genai.list_models(): Usado para diagnosticar e selecionar dinamicamente os modelos disponíveis e adequados.

3. Sobre o Código

Linguagem de Programação: Python 3.x
Framework Principal: Streamlit.

Bibliotecas Chave:

* langchain e langchain_community: Orquestração de LLMs, text splitting, loaders, e cadeia RAG.
* langchain_google_genai: Integração com os modelos Gemini (chat e embedding).
* chromadb: Banco de dados vetorial para armazenamento e busca de embeddings.
* PyMuPDFLoader: Loader de documentos PDF para extração de texto.
* os: Operações de sistema de arquivos (criação de diretórios, remoção de arquivos temporários).
* Comentários em Linha: O código é amplamente comentado para explicar as seções, a lógica de cada parte e os pontos-chave de configuração.
* Estrutura Modular: O código é dividido em seções lógicas (Configuração, Diagnóstico, Carregamento/Processamento, Embeddings/Vector Store, LLM, UI). 
* Tratamento de Erros: Blocos try-except são utilizados para capturar e exibir erros críticos de inicialização da API, garantindo feedback imediato ao usuário.


Guia de Instruções:

Para Obter Insights Financeiros Fazendo Perguntas:

* Passo 1: Acessar a Área de Pergunta: Após os documentos serem processados, a seção "Pergunte aos Seus Relatórios Financeiros" será exibida.
* Passo 2: Formular sua Pergunta: Na caixa de texto, digite sua pergunta em linguagem natural sobre o conteúdo dos relatórios carregados.
* Passo 3: Obter a Resposta: Clique no botão "Obter Insights Financeiros". O aplicativo exibirá um spinner "Buscando e gerando insights...".
* Passo 4: Analisar os Insights e Fontes: A resposta do modelo aparecerá na seção "Insights Gerados".
  

Exceções:

Se o aplicativo não iniciar ou exibir "ERRO CRÍTICO na inicialização da API Gemini":
* Solução: Verifique novamente se sua GOOGLE_API_KEY está corretamente configurada no arquivo .streamlit/secrets.toml (deve ser GOOGLE_API_KEY = "SUA_CHAVE_AQUI".

Se o aplicativo carregar, mas a mensagem "Nenhum modelo de chat/embedding adequado foi encontrado" aparecer:
* Solução: Verifique a saída expandida de "Verificar Detalhes dos Modelos Gemini Encontrados" para ver quais modelos sua API está listando. 

Se o aplicativo disser "Nenhum texto útil foi extraído dos PDFs carregados":
* Solução: Abra o PDF original e tente selecionar o texto dentro dele. Se você não conseguir selecionar o texto (ou seja, ele é uma imagem), o aplicativo não conseguirá ler o conteúdo.

Se a resposta for imprecisa ou incompleta, mas a informação está no documento:
* Solução: Tente reformular a pergunta com mais detalhes ou de forma diferente.


# Acesso a versão da aplicação de teste FinInsight AI
* Para acesso da versão de teste acesse: https://fininsightai.streamlit.app/

# Guia de Instruções de Instalação localmente do projeto:

* Passo 1: Faça o download do projeto;
* Passo 2: Crie uma virtualenv para isolar as dependências do projeto;
* Passo 3: Instale todas as dependencias do projetos utilizando o arquivo requirements.txt, para tanto utilize o comando pip install -r requirements.txt; e
* Passo 4: Agora com todas a infraestrutura instalada, execute o comando streamlit run main.py.


