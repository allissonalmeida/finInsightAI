# FinInsight AI: Análise Inteligente de Relatórios Financeiros
Wiki criado para apresentar informações sobre o projeto final de programação de software em 2025.1 do doutorado na PUC-Rio.

# Breve Descrição

O FinInsight AI é uma plataforma de análise automatizada de relatórios financeiros trimestrais (em PDF) que integra técnicas de Recuperação Aumentada por Geração (RAG) e Modelos de Linguagem (LLMs). Sua principal função é extrair, processar e correlacionar dados quantitativos (balanços, indicadores) e qualitativos (textos explicativos) para gerar insights estratégicos, como tendências de mercado, riscos operacionais e oportunidades de investimento.

# Visão de Projeto

# Cenário Positivo 1 (i.e. cenário que dá certo)

Maria é analista financeira júnior em uma consultoria. Ela precisa preparar um resumo rápido sobre a saúde financeira de uma nova empresa cliente em menos de uma hora. Ela acessa o FinAI Insights, carrega o último relatório trimestral em PDF da empresa. Após o processamento (que leva menos de um minuto), Maria digita a pergunta: "Qual foi o lucro líquido da empresa no último trimestre e como ele se compara ao trimestre anterior?". O sistema responde prontamente com os valores exatos e a comparação, citando as páginas do relatório de onde a informação foi extraída. Em seguida, Maria pergunta: "Quais foram os principais custos operacionais detalhados no relatório?". O FinAI Insights lista os maiores itens de custo, permitindo que Maria entenda rapidamente as despesas da empresa sem ter que navegar manualmente por dezenas de páginas. Ela consegue compilar o resumo para seu gerente a tempo, impressionando com a velocidade e a precisão da sua análise.

# Cenário Positivo 2

João é um gestor de riscos em uma grande corporação. Ele precisa identificar rapidamente os principais riscos operacionais mencionados nos relatórios anuais de todas as subsidiárias do grupo. Ele acessa o FinAI Insights, carrega os PDFs de cinco relatórios anuais simultaneamente. Após o processamento, ele faz a pergunta: "Com base nos relatórios, quais são os três principais riscos operacionais identificados pela gestão em 2023 para cada subsidiária?". O FinAI Insights varre os documentos e apresenta uma lista concisa dos riscos para cada empresa, com referências às seções originais. João consegue consolidar essas informações em um relatório de riscos do grupo em poucas horas, um trabalho que levaria dias se feito manualmente, garantindo que nenhum risco crítico seja negligenciado.

# Cenário Negativo 1 (i.e. cenário que expõe uma limitação conhecida e esperada do programa)

Ana, uma estudante de finanças, está usando o FinAI Insights para pesquisar sobre o endividamento de pequenas e médias empresas. Ela carrega um relatório financeiro de uma startup, esperando encontrar detalhes sobre a estrutura da dívida. Ela pergunta: "Qual o detalhamento dos empréstimos bancários de longo prazo?". O sistema retorna com a mensagem: "Não há informações detalhadas sobre empréstimos bancários de longo prazo nos textos fornecidos." Ana, frustrada, verifica o PDF original e percebe que, de fato, o relatório da startup é muito sucinto e não detalha os empréstimos além de um valor total genérico. Ela entende que a limitação não é do sistema, mas da falta de granularidade da informação no documento fonte.


# Cenário Negativo 2

Carlos, um consultor, está analisando um relatório financeiro digitalizado de uma empresa mais antiga, onde algumas tabelas e gráficos foram inseridos como imagens, e não como texto selecionável. Ele carrega o PDF no FinAI Insights e tenta perguntar: "Qual o valor do EBITDA para os anos de 2020 a 2022, conforme a tabela de resultados?". O sistema retorna uma resposta imprecisa ou afirma que não encontrou a informação, mesmo que a tabela esteja visivelmente no documento. Carlos então tenta perguntar sobre um parágrafo textual logo abaixo da tabela e o sistema responde corretamente. Ele percebe que o problema é a incapacidade do sistema de ler dados de imagens dentro do PDF, uma limitação conhecida da extração de texto para modelos de RAG que dependem de OCR externo ou texto nativo.


# Documentação Técnica do Projeto

Esta seção oferece informações para desenvolvedores e colaboradores interessados em entender e, potencialmente, reutilizar ou estender o FinAI Insights.

1. Especificação de Requisitos Funcionais e Não-Funcionais do Software

Requisitos Funcionais:

* F1.1: Upload de Documentos: O sistema deve permitir o upload de um ou múltiplos arquivos PDF de relatórios financeiros.
* F1.2: Extração de Conteúdo: O sistema deve extrair texto (quantitativo e qualitativo) dos PDFs carregados.
* F1.3: Geração de Embeddings: O sistema deve gerar representações vetoriais (embeddings) dos chunks de texto extraídos.
* F1.4: Armazenamento Vetorial: O sistema deve armazenar os embeddings em um banco de dados vetorial para busca eficiente.
* F1.5: Interface de Consulta: O sistema deve fornecer uma interface de texto para o usuário inserir perguntas em linguagem natural.
* F1.6: Recuperação de Contexto (Retrieval): O sistema deve recuperar os chunks de texto mais relevantes do banco de dados vetorial com base na pergunta do usuário.
* F1.7: Geração de Resposta (Generation): O sistema deve utilizar um LLM para gerar uma resposta concisa e relevante com base na pergunta do usuário e no contexto recuperado.
* F1.8: Citação de Fontes: A resposta gerada deve incluir referências aos documentos originais (nome do arquivo, número da página) de onde o contexto foi retirado.
* F1.9: Diagnóstico da API: O sistema deve verificar e exibir o status de conexão com a API Gemini e listar os modelos de chat e embedding disponíveis.
* F1.10: Seleção Automática de Modelo: O sistema deve selecionar automaticamente o modelo de LLM e Embedding mais adequado (priorizando gemini-1.5-flash-latest, gemini-1.5-flash, etc.).

Requisitos Não-Funcionais:

* NF2.1: Performance: O processamento de documentos e a geração de respostas devem ser eficientes, com tempos de resposta adequados para análises rápidas (idealmente segundos para perguntas).
* NF2.2: Escalabilidade: A arquitetura deve permitir o escalonamento para processar um número maior de documentos e atender a múltiplos usuários (considerando infraestrutura e cotas de API).
* NF2.3: Confiabilidade: O sistema deve ser robusto a falhas, com tratamento de erros adequado (ex: falha na API, documento corrompido).
* NF2.4: Segurança: A chave de API deve ser gerenciada de forma segura (utilizando st.secrets).
* NF2.5: Usabilidade: A interface do usuário deve ser intuitiva e fácil de usar para o público-alvo (analistas, gestores).
* NF2.6: Manutenibilidade: O código deve ser modular, bem comentado e fácil de entender e modificar para futuras atualizações.
* NF2.7: Adaptabilidade: A arquitetura deve ser flexível para integrar novos modelos de LLM e embeddings, bem como diferentes formatos de documentos, no futuro.

2. Descrição da Arquitetura do Software

O FinAI Insights segue uma arquitetura baseada em Retrieval Augmented Generation (RAG), implementada como uma aplicação web utilizando Streamlit.

Camada de Interface (Frontend):

Desenvolvida com Streamlit, que fornece a interface de usuário interativa (upload de arquivos, caixa de texto para perguntas, exibição de respostas e diagnósticos).
Lida com a interação direta com o usuário.

Camada de Processamento de Documentos:

* PyMuPDFLoader: Biblioteca utilizada para carregar e extrair texto de arquivos PDF.
* RecursiveCharacterTextSplitter (LangChain): Responsável por dividir o texto extraído em "chunks" (pedaços menores), otimizados para o processo de embedding e recuperação, com controle de chunk_size e chunk_overlap.

Camada de Embedding e Banco de Dados Vetorial:

* GoogleGenerativeAIEmbeddings (LangChain): Utiliza o modelo de embedding do Google Gemini (models/embedding-001 ou similar) para transformar os chunks de texto em vetores numéricos (embeddings).
* ChromaDB: Um banco de dados vetorial leve e persistente (chromadb.PersistentClient) utilizado para armazenar os embeddings e seus metadados.

  
Camada de Modelo de Linguagem (LLM) e Orquestração RAG:

* ChatGoogleGenerativeAI (LangChain): Interface para o modelo de linguagem grande (LLM) do Google Gemini (ex: gemini-1.5-flash-latest) para a parte de geração de respostas.

RetrievalQA (LangChain) que orquestra o fluxo RAG:

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
Framework Principal: Streamlit (para a interface web e gerenciamento de estado da aplicação).

Bibliotecas Chave:
* langchain e langchain_community: Orquestração de LLMs, text splitting, loaders, e cadeia RAG.
* langchain_google_genai: Integração com os modelos Gemini (chat e embedding).
* chromadb: Banco de dados vetorial para armazenamento e busca de embeddings.
* PyMuPDFLoader: Loader de documentos PDF para extração de texto.
* os: Operações de sistema de arquivos (criação de diretórios, remoção de arquivos temporários).
* Comentários em Linha: O código é amplamente comentado para explicar as seções, a lógica de cada parte e os pontos-chave de configuração.
* Estrutura Modular: O código é dividido em seções lógicas (Configuração, Diagnóstico, Carregamento/Processamento, Embeddings/Vector Store, LLM, UI) para facilitar a compreensão e manutenção. 
* Tratamento de Erros: Blocos try-except são utilizados para capturar e exibir erros críticos de inicialização da API, garantindo feedback imediato ao usuário.


Guia de Instruções:

Para Analisar um Novo Relatório Financeiro (PDF):

* Passo 1: Iniciar o Aplicativo: Abra seu terminal e navegue até a pasta onde o arquivo mainFinGemini.py está salvo. Execute o comando: streamlit run mainFinGemini.py.
* Passo 2: Verificar Status da API (Opcional, mas recomendado): No topo da página, clique em "Verificar Detalhes dos Modelos Gemini Encontrados" para expandir a seção. Verifique se os modelos de chat e embedding foram selecionados com sucesso.
* Passo 3: Carregar os Relatórios: Localize a seção "Carregue seus Relatórios Financeiros (PDF)". Clique no botão "Browse files" ou arraste e solte um ou mais arquivos PDF para a área indicada.
* Passo 4: Aguardar o Processamento: Após carregar os arquivos, o aplicativo exibirá um spinner "Processando relatórios e preparando para análise..." e depois "Configurando o banco de dados vetorial...". 

Para Obter Insights Financeiros Fazendo Perguntas:

* Passo 1: Acessar a Área de Pergunta: Após os documentos serem processados, a seção "Pergunte aos Seus Relatórios Financeiros" será exibida.
* Passo 2: Formular sua Pergunta: Na caixa de texto, digite sua pergunta em linguagem natural sobre o conteúdo dos relatórios carregados.
* Passo 3: Obter a Resposta: Clique no botão "Obter Insights Financeiros". O aplicativo exibirá um spinner "Buscando e gerando insights...".
* Passo 4: Analisar os Insights e Fontes: A resposta do modelo aparecerá na seção "Insights Gerados".

Exceções ou Potenciais Problemas:

Se o aplicativo não iniciar ou exibir "ERRO CRÍTICO na inicialização da API Gemini":

* Então faça: Verifique novamente se sua GOOGLE_API_KEY está corretamente configurada no arquivo .streamlit/secrets.toml (deve ser GOOGLE_API_KEY = "SUA_CHAVE_AQUI".

Se o aplicativo carregar, mas a mensagem "Nenhum modelo de chat/embedding adequado foi encontrado" aparecer:

* Então faça: Verifique a saída expandida de "Verificar Detalhes dos Modelos Gemini Encontrados" para ver quais modelos sua API está listando. 


Se o aplicativo disser "Nenhum texto útil foi extraído dos PDFs carregados":

* Então faça: Abra o PDF original e tente selecionar o texto dentro dele. Se você não conseguir selecionar o texto (ou seja, ele é uma imagem), o aplicativo não conseguirá ler o conteúdo.

Se a resposta para sua pergunta for "Não há informações sobre X nos textos fornecidos" ou similar:

* Então faça: Abra o documento PDF original e procure manualmente pela informação. Se a informação não estiver no documento, a resposta do modelo está correta. Se a informação estiver lá, tente reformular sua pergunta ou dividi-la em partes menores e mais específicas.

Se a resposta for imprecisa ou incompleta, mas a informação está no documento:

* Então faça: Tente reformular a pergunta com mais detalhes ou de forma diferente.
