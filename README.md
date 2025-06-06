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

Esta seção da Wiki se destina a pessoas que queiram reutilizar, total ou parcialmente, o seu programa. Portanto, ofereça todas as informações necessárias. Os três itens a seguir são os mais utilizados. Escolha com o(a) orientador(a) do projeto quais destes itens devem ser incluídos. Para cada item incluído, crie uma seção específica.

Especificação de requisitos funcionais e não-funcionais do sotware
Descrição ou modelo de arquitetura, dados, semântica ou outra dimensão relevante do software
Descrição ou modelo funcional do software
Sobre o código (detalhes da linguagem ou da técnica de programação utilizada, da estratégia de comentários em linha, das diretivas de compilação, se houver, etc.)
Manual de Utilização para Usuários Contemplados
O manual de utilização deve ser elaborado para todos os tipos de usuários contemplados. Deve também ser consistente com todo o restante do conteúdo da Wiki, o que inclui descrição, cenários e documentação técnica.

O formato mais prático para a elaboração de um manual de uso é seguir a estrutura sugerida a seguir, para cada tarefa que o usuário pode realizar (o que envolve usar várias funções) e para cada função básica que o programa oferece:


{ 
  Guia de Instruções:
  %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
  Para [Tarefa A: por exemplo, no cenário usado, BUSCAR VÍDEO] faça:
  Passo 1: ...
  Passo 2: ...
  ...
  Passo N: ...

  >>> Se houver diferentes maneiras de realizar a Tarefa A, descreva cada uma delas.
  >>> E se em certos contextos, uma alternativa for melhor que outra, informe e explique.

  Exceções ou potenciais problemas:
  %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
  Se [Condição Prevista C1: por exemplo, o vídeo for encontrado mas o link está 'quebrado']
     {
     Então faça: [Passo 1, Passo 2, ..., Passo N] 
     ou
     É porque: [explique o problema, se não há uma sugestão para solucionar] 
     } 
  
  Se [Condição Prevista C2: ... 
  ...
  Se [Condição Prevista CN: ...      
}

>>> Repita a estrutura do Guia acima para cada tarefa e função básica.

