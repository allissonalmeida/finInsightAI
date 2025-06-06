# FinInsight AI: Análise Inteligente de Relatórios Financeiros
Wiki criado para apresentar informações sobre o projeto final de programação de software em 2025.1 do doutorado na PUC-Rio.

# Breve Descrição

O FinInsight AI é uma plataforma de análise automatizada de relatórios financeiros trimestrais (em PDF) que integra técnicas de Recuperação Aumentada por Geração (RAG) e Modelos de Linguagem (LLMs). Sua principal função é extrair, processar e correlacionar dados quantitativos (balanços, indicadores) e qualitativos (textos explicativos) para gerar insights estratégicos, como tendências de mercado, riscos operacionais e oportunidades de investimento.

# Visão de Projeto

# Cenário Positivo 1 (i.e. cenário que dá certo)

Ana, analista sênior em um banco de investimento, precisa identificar tendências no setor de energia renovável. Ela carrega 20 relatórios trimestrais de empresas do setor no FinInsight AI. O sistema extrai automaticamente dados como CAPEX em biomassa e menções a "transição energética" nos textos. Usando RAG, cruza essas informações com dados do setor armazenados em sua base. Em minutos, o dashboard gera um relatório destacando um crescimento de 12% em investimentos em biomassa, correlacionado com menções a "novos contratos de transporte de vinhaça". Ana exporta o gráfico interativo para sua apresentação ao conselho.

# Cenário Positivo 2

Carlos, consultor de riscos, investiga a exposição de clientes a flutuações cambiais. O FinInsight AI identifica, em 50 relatórios, trechos como "hedge cambial insuficiente" e calcula automaticamente a proporção de dívidas em moeda estrangeira. Um alerta automático sinaliza 3 empresas com discrepâncias acima de 15% entre dados tabulares e descrições textuais. Carlos usa a função de "linha do tempo" para rastrear menções a "contingências cambiais" nos últimos 8 trimestres, encontrando padrões sazonais.

# Cenário Negativo 1 (i.e. cenário que expõe uma limitação conhecida e esperada do programa)

Uma gestora tenta analisar relatórios de uma empresa com PDFs digitalizados em baixa resolução. O OCR do sistema falha na extração de tabelas críticas de endividamento, retornando valores distorcidos. Embora o módulo qualitativo identifique menções a "reestruturação de dívidas", a falta de dados estruturados impede a geração de insights integrados. O sistema emite um alerta técnico, mas a usuária precisa solicitar versões nativas dos PDFs ao departamento jurídico, atrasando sua análise em 48 horas.


# Cenário Negativo 2

Um analista júnior insere um relatório com notas explicativas em espanhol, esperando análise profunda. O sistema, treinado principalmente em português, traduz automaticamente o texto, mas perde nuances técnicas específicas do mercado argentino. A ferramenta RAG recupera dados desatualizados de um banco de dados em português, levando a recomendações equivocadas sobre exposição ao risco-país. O usuário só percebe o erro ao comparar manualmente os resultados com fontes secundárias.

# Documentação Técnica do Projeto

Certo\! Com o modelo de documentação em mãos, posso criar o documento técnico para o seu projeto de busca semântica jurídica. Seguirei a estrutura que você forneceu, focando nos três itens mais utilizados e no formato do manual de utilização.

Considerando o contexto do seu projeto, que é um aplicativo Streamlit para busca semântica de documentos jurídicos, os itens mais relevantes para a reutilização e compreensão são:

1.  **Especificação de Requisitos Funcionais e Não-Funcionais do Software**
2.  **Descrição ou Modelo de Arquitetura, Dados, Semântica ou Outra Dimensão Relevante do Software** (Focaremos na Arquitetura e Semântica do RAG)
3.  **Sobre o Código** (Detalhes de linguagem, bibliotecas, estrutura)
4.  **Manual de Utilização para Usuários Contemplados** (Focando na tarefa principal de busca)

Vou elaborar o documento usando Markdown, que é o formato ideal para o GitHub Wiki.

-----

# Documentação Técnica do Projeto JuridicaMente

## 1\. Visão Geral

Este documento detalha o projeto "JuridicaMente", uma aplicação de busca semântica impulsionada por Inteligência Artificial, desenvolvida para auxiliar usuários a encontrar decisões, alegações e processos jurídicos relevantes em um conjunto de documentos PDF. A aplicação utiliza técnicas de RAG (Retrieval Augmented Generation) para fornecer respostas contextualmente ricas baseadas no conteúdo dos documentos.

## 2\. Especificação de Requisitos Funcionais e Não-Funcionais do Software

### 2.1 Requisitos Funcionais

  * **RF1: Extração e Processamento de Documentos:** O sistema deve ser capaz de extrair documentos PDF de um arquivo `.zip` e processá-los para torná-los pesquisáveis.
  * **RF2: Divisão de Documentos em Chunks:** O sistema deve dividir os documentos processados em "chunks" (pedaços menores de texto) para otimizar a busca e o contexto para o LLM.
  * **RF3: Geração e Armazenamento de Embeddings:** O sistema deve gerar representações vetoriais (embeddings) para cada chunk de texto utilizando um modelo de embedding de código aberto. Essas representações devem ser armazenadas em um vetor database local.
  * **RF4: Busca Semântica:** O sistema deve permitir que o usuário insira uma pergunta em linguagem natural e realize uma busca por similaridade semântica nos chunks armazenados no vetor database.
  * **RF5: Geração de Respostas por LLM:** O sistema deve utilizar um Large Language Model (LLM) externo (DeepSeek) para gerar respostas coerentes e contextuais com base nos chunks mais relevantes encontrados na busca semântica.
  * **RF6: Interface de Usuário:** O sistema deve prover uma interface de usuário simples e intuitiva (via Streamlit) para a entrada de perguntas e exibição das respostas.
  * **RF7: Carregamento Persistente do Índice:** O sistema deve ser capaz de salvar o índice de embeddings localmente e carregá-lo em execuções futuras para evitar o reprocessamento completo dos documentos.

### 2.2 Requisitos Não-Funcionais

  * **RNF1: Desempenho (Tempo de Resposta):** O tempo de resposta para uma busca semântica e geração de resposta deve ser razoável, idealmente em poucos segundos, dependendo da complexidade da pergunta e da quantidade de documentos.
  * **RNF2: Escalabilidade (Local):** A solução local deve ser capaz de lidar com um volume crescente de documentos, embora o desempenho possa ser afetado por grandes volumes de dados que excedam a capacidade de memória/disco local.
  * **RNF3: Facilidade de Uso:** A interface do usuário deve ser clara e fácil de entender, mesmo para usuários sem conhecimento técnico em IA.
  * **RNF4: Confiabilidade:** O sistema deve ser robusto a erros na leitura de PDFs e na comunicação com APIs externas, fornecendo mensagens de erro claras ao usuário.
  * **RNF5: Segurança:** As chaves de API para serviços externos (DeepSeek) devem ser armazenadas de forma segura (e.g., Streamlit Secrets) e não expostas no código-fonte.
  * **RNF6: Manutenibilidade:** O código deve ser modular, bem comentado e fácil de entender para futuras manutenções e expansões.
  * **RNF7: Portabilidade:** A solução deve ser facilmente executável em diferentes ambientes Python (localmente ou em plataformas como Streamlit Cloud).

## 3\. Descrição da Arquitetura e Semântica do Software (RAG)

A arquitetura do JuridicaMente segue o paradigma de **Retrieval Augmented Generation (RAG)**, um modelo híbrido que combina a capacidade de compreensão e geração de linguagem de um Large Language Model (LLM) com a recuperação de informações de uma base de conhecimento externa.

### 3.1 Componentes da Arquitetura

A arquitetura pode ser dividida nas seguintes fases e componentes principais:

*Diagrama Conceitual de um Fluxo RAG. Fonte: LangChain.*

1.  **Módulo de Carregamento e Processamento de Documentos:**

      * **Entrada:** `documentos.zip` (arquivo ZIP contendo PDFs).
      * **Loader (PyMuPDFLoader):** Responsável por ler e extrair o texto de cada arquivo PDF.
      * **Text Splitter (RecursiveCharacterTextSplitter):** Divide o texto extraído em pedaços menores (chunks) de tamanho configurável (1000 caracteres com 100 de sobreposição), mantendo o contexto entre os chunks adjacentes.

2.  **Módulo de Geração e Armazenamento de Embeddings (Vector Store Local):**

      * **Embedding Model (HuggingFaceEmbeddings):** Utiliza o modelo `sentence-transformers/all-MiniLM-L6-v2` para converter cada chunk de texto em um vetor numérico (embedding) de 384 dimensões. Este modelo é executado localmente.
      * **Vector Store (FAISS):** Armazena os embeddings gerados e seus chunks de texto associados.
          * **Persistência:** O índice FAISS é salvo localmente em uma pasta (`faiss_index`) no disco. Isso permite que, após a primeira execução (que gera os embeddings), o aplicativo possa carregar o índice existente em execuções futuras, economizando tempo e recursos de processamento.
          * **Busca por Similaridade:** Quando uma query é feita, o FAISS é usado para encontrar os vetores (e seus chunks de texto) mais semanticamente semelhantes à embedding da query.

3.  **Módulo de Modelo de Linguagem Grande (LLM):**

      * **LLM (DeepSeek Chat - via ChatOpenAI):** Um modelo de linguagem baseado em nuvem (DeepSeek) é utilizado para gerar a resposta final. Ele recebe como entrada a pergunta original do usuário e os chunks de texto mais relevantes recuperados do FAISS.
      * **Integração LangChain:** O componente `ChatOpenAI` da LangChain facilita a comunicação com a API do DeepSeek, que é compatível com a interface da API OpenAI.

4.  **Cadeia de Recuperação e Geração (RetrievalQA Chain):**

      * **Retriever:** Configurado para buscar os `k` (atualmente 3) chunks mais relevantes do FAISS com base na similaridade.
      * **Chain Type (`stuff`):** O `stuff` chain type simplesmente "empacota" todos os chunks recuperados em um único prompt de contexto para o LLM, juntamente com a pergunta original, solicitando que o LLM responda com base nesse contexto.

5.  **Interface do Usuário (Streamlit):**

      * Fornece a camada de interação, permitindo que o usuário digite sua pergunta e visualize a resposta.
      * Gerencia o fluxo de trabalho do aplicativo, desde a extração de documentos até a exibição da resposta final.

### 3.2 Semântica do RAG (Fluxo de Dados e Informações)

1.  **Indexação (Executada na Primeira Inicialização ou se o Índice não Existe):**

      * Documentos PDF são carregados.
      * O conteúdo dos PDFs é dividido em chunks.
      * Cada chunk é transformado em um vetor numérico (embedding) pelo modelo HuggingFace.
      * Esses vetores são armazenados no índice FAISS, que é salvo em disco.

2.  **Consulta (Executada em Cada Busca do Usuário):**

      * O usuário insere uma **pergunta (query)**.
      * A pergunta é convertida em um embedding usando o **mesmo modelo HuggingFace**.
      * Este embedding da pergunta é usado para realizar uma **busca por similaridade** no índice FAISS.
      * Os `k` (por exemplo, 3) chunks de documentos cujos embeddings são mais semanticamente próximos ao embedding da pergunta são **recuperados**.
      * A pergunta original do usuário e os chunks recuperados são passados como **contexto** para o LLM (DeepSeek).
      * O **LLM gera uma resposta** que sintetiza as informações do contexto recuperado para responder à pergunta do usuário.
      * A resposta gerada é exibida na interface Streamlit.

## 4\. Sobre o Código

### 4.1 Estrutura do Projeto

O projeto é organizado em um único arquivo Python `main.py` para simplificar a implantação no Streamlit Cloud, juntamente com os arquivos de configuração e dados necessários.

```
.
├── main.py                     # Script principal da aplicação Streamlit
├── documentos.zip              # Arquivo ZIP contendo os documentos PDF
├── requirements.txt            # Dependências Python do projeto
├── .streamlit/                 # Pasta de configuração do Streamlit
│   └── secrets.toml            # Arquivo para chaves de API e segredos
└── faiss_index/                # Diretório onde o índice FAISS é salvo/carregado (criado automaticamente)
    ├── index.faiss             # Arquivo principal do índice FAISS
    └── index.pkl               # Metadados do índice FAISS
├── logo.png                    # Imagem do logo da aplicação (assumindo que existe)
└── README.md                   # (Sugestão) Arquivo README do GitHub
```

### 4.2 Linguagem e Técnicas de Programação

  * **Linguagem:** Python 3.9+
  * **Framework de UI:** [Streamlit](https://streamlit.io/) para criação da interface web interativa.
  * **Framework LLM/RAG:** [LangChain](https://www.langchain.com/) para orquestrar o fluxo de RAG, incluindo carregamento de documentos, divisão de texto, embeddings, vetor database e integração com LLMs.
  * **Processamento de PDF:** [PyMuPDFLoader](https://pymupdf.readthedocs.io/) (via LangChain Community) para extração de texto de PDFs.
  * **Embeddings:** [HuggingFace Embeddings](https://huggingface.co/docs/transformers/main/en/model_doc/bert) (via LangChain Community e `sentence-transformers`) para gerar os vetores semânticos.
  * **Vector Store Local:** [FAISS (Facebook AI Similarity Search)](https://github.com/facebookresearch/faiss) para armazenamento e busca eficiente de vetores localmente.
  * **Large Language Model (LLM):** [DeepSeek AI](https://www.deepseek.com/) (acessado via `ChatOpenAI` da LangChain) para a capacidade de raciocínio e geração de texto.

### 4.3 Estratégia de Comentários em Linha

O código utiliza comentários em linha (`#`) para explicar blocos de código complexos, variáveis importantes, lógica condicional e para marcar seções principais da aplicação. O objetivo é tornar o código autoexplicativo e facilitar a compreensão para novos desenvolvedores ou para manutenção futura.

### 4.4 Gerenciamento de Dependências

As dependências do projeto são gerenciadas através do arquivo `requirements.txt`. Para instalar todas as dependências, utilize o comando:

```bash
pip install -r requirements.txt
```

### 4.5 Gerenciamento de Segredos (API Keys)

As chaves de API sensíveis (como `DEEPSEEK_API_KEY`) são carregadas a partir do `st.secrets` do Streamlit, que lê o arquivo `.streamlit/secrets.toml` em ambientes de desenvolvimento local e gerencia segredos de forma segura no Streamlit Cloud.

Exemplo de `.streamlit/secrets.toml`:

```toml
DEEPSEEK_API_KEY="sua_chave_deepseek_aqui"
# Outras chaves que possam ser necessárias, se o projeto evoluir
```

## 5\. Manual de Utilização para Usuários Contemplados

Este manual é destinado a qualquer usuário que deseje interagir com o aplicativo "JuridicaMente" para realizar buscas semânticas em documentos jurídicos.

### Guia de Instruções: Realizando uma Busca Semântica

**Para [Tarefa: BUSCAR INFORMAÇÕES JURÍDICAS] faça:**

**Objetivo:** Obter uma resposta concisa e relevante para uma pergunta jurídica, baseada nos documentos processados.

**Passo 1: Acessar a Aplicação**

  * Abra o navegador web e acesse a URL da aplicação JuridicaMente (se for uma aplicação online hospedada no Streamlit Cloud) ou execute-a localmente (`streamlit run main.py`).

**Passo 2: Digitar sua Pergunta**

  * Na interface da aplicação, localize a caixa de texto grande rotulada "Digite sua pergunta:".
  * Insira sua pergunta de forma clara e objetiva, relacionada ao conteúdo dos documentos jurídicos processados.
      * **Exemplos:**
          * "Quais são os requisitos para a concessão de tutela de urgência?"
          * "Existe alguma decisão sobre o uso de provas digitais em casos de direito de família?"
          * "Como a jurisprudência aborda a responsabilidade civil em acidentes de trânsito?"

**Passo 3: Iniciar a Busca**

  * Após digitar sua pergunta, clique no botão rotulado "**Buscar**" localizado abaixo da caixa de texto.

**Passo 4: Aguardar a Resposta**

  * Uma mensagem "Buscando resposta..." aparecerá enquanto o sistema processa sua pergunta, busca os documentos relevantes e gera a resposta.
  * O tempo de espera pode variar dependendo da complexidade da busca e da performance da API do LLM.

**Passo 5: Visualizar a Resposta**

  * A resposta gerada pelo sistema aparecerá sob o título "Resposta:". Leia a resposta para obter a informação desejada.

### Exceções ou Potenciais Problemas:

**Se [Condição Prevista C1: Não há documentos carregados ou o arquivo ZIP está ausente/corrompido]**

  * **É porque:** O sistema não conseguiu extrair ou carregar os documentos PDF necessários para a busca.
  * **Então faça:** Verifique se o arquivo `documentos.zip` está presente na mesma pasta do script principal e se ele contém documentos PDF válidos. Se estiver no Streamlit Cloud, certifique-se de que o arquivo foi incluído no repositório GitHub. Reinicie a aplicação.

**Se [Condição Prevista C2: O modelo de embedding HuggingFace falha ao inicializar]**

  * **É porque:** A biblioteca `sentence-transformers` ou `faiss-cpu` (dependendo do erro exato) pode não estar corretamente instalada.
  * **Então faça:** Verifique o `requirements.txt` para garantir que `sentence-transformers` e `faiss-cpu` estejam listados e que as dependências foram instaladas corretamente (reinicie o deploy no Streamlit Cloud ou execute `pip install -r requirements.txt` localmente).

**Se [Condição Prevista C3: O LLM DeepSeek retorna erro de "Insufficient Balance" (Saldo Insuficiente)]**

  * **É porque:** Sua conta na API do DeepSeek não tem créditos suficientes ou o plano gratuito foi excedido.
  * **Então faça:** Acesse o painel da sua conta DeepSeek (geralmente https://www.google.com/search?q=api.deepseek.com), verifique seu saldo ou limites de uso e adicione créditos, se necessário.

**Se [Condição Prevista C4: A resposta não é relevante ou parece incorreta]**

  * **É porque:**
      * A pergunta pode não ter sido clara o suficiente ou pode estar fora do escopo dos documentos fornecidos.
      * Os documentos podem não conter informações sobre o tópico da pergunta.
      * O modelo de embedding ou o LLM podem ter limitações inerentes.
  * **Então faça:**
      * Reformule sua pergunta de forma diferente ou mais específica.
      * Verifique se os documentos em `documentos.zip` realmente contêm as informações que você espera.
      * Tente perguntas mais genéricas ou mais focadas, dependendo do que você está buscando.

-----

Espero que esta documentação atenda aos seus requisitos e seja útil para quem for reutilizar o projeto\! Lembre-se de que o `logo.png` deve estar na mesma pasta do seu `main.py` para ser exibido.
