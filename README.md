# Azure AI Search
## Exercício para explorar o azure ai search, minerando dados sobre o Fourth Coffee.

Segui os passos do material disponibilizado pela microsoft:
https://microsoftlearning.github.io/mslearn-ai-fundamentals/Instructions/Labs/11-ai-search.html

### Recursos do Azure necessários
A solução que você criará para o Fourth Coffee requer os seguintes recursos na sua assinatura do Azure:

  - Um recurso do **Azure AI Search**, que gerenciará a indexação e a consulta.
  - Um recurso **de serviços de IA do Azure**, que fornece serviços de IA para habilidades que sua solução de pesquisa pode usar para enriquecer os dados na fonte de dados com insights gerados por IA.
  - Uma **conta de armazenamento** com contêineres de blobs, que armazenará documentos brutos e outras coleções de tabelas, objetos ou arquivos.

#### Crie um recurso do Azure AI Search
1. Entre no portal do Azure.
2. Clique no botão **+ Criar um recurso**, pesquise Azure AI Search e crie um recurso **Azure AI Search** com as seguintes configurações:

    - **Assinatura**: sua assinatura do Azure.
    - **Grupo de recursos**: selecione ou crie um grupo de recursos com um nome exclusivo.
    - **Nome do serviço**: um nome exclusivo.
    - **Localização**: Escolha qualquer região disponível.
    - **Nível de preços**: Básico

3. Selecione **Review + create** e depois de ver a resposta **Validation Success**, selecione **Create**.
4. Após a conclusão da implantação, selecione **Ir para o recurso**. Na página de visão geral do Azure AI Search, você pode adicionar índices, importar dados e pesquisar índices criados.

#### Crie um recurso de serviços de IA do Azure
Você precisará provisionar um recurso **de serviços de IA do Azure** que esteja no mesmo local que seu recurso do Azure AI Search. Sua solução de pesquisa usará esse recurso para enriquecer os dados no armazenamento de dados com insights gerados por IA.

1. Retorne à página inicial do portal do Azure. Clique no botão **＋Criar um recurso** e pesquise os serviços de IA do Azure. Selecione **criar** um plano **de serviços de IA do Azure**. Você será levado a uma página para criar um recurso de serviços de IA do Azure. Configure-o com as seguintes configurações:

    - **Assinatura**: sua assinatura do Azure .
    - **Grupo de recursos**: O mesmo grupo de recursos que seu recurso do Azure AI Search .
    - **Região**: o mesmo local do recurso do Azure AI Search .
    - **Nome**: Um nome exclusivo .
    - **Nível de preços**: Padrão S0
    - **Ao marcar esta caixa, confirmo que li e compreendi todos os termos abaixo**: Selecionado

2. Selecione **Revisar + criar**. Depois de ver a resposta **Validation Passed**, selecione **Create**.
3. Aguarde a conclusão da implantação e visualize os detalhes da implantação.

#### Crie uma conta de armazenamento
1. Retorne à página inicial do portal do Azure e selecione o botão **+ Criar um recurso**.
2. Procure conta de armazenamento e crie um recurso **de conta de armazenamento** com as seguintes configurações:

    - **Assinatura**: sua assinatura do Azure.
    - **Grupo de recursos**: O mesmo grupo de recursos que os recursos do Azure AI Search e dos serviços Azure AI.
    - **Nome da conta de armazenamento**: um nome exclusivo.
    - **Localização**: Escolha qualquer localização disponível.
    - Padrão de **desempenho**
    - **Redundância**: armazenamento localmente redundante (LRS)

3. Clique em **Revisar** e em **Criar**. Aguarde a conclusão da implantação e vá para o recurso implantado.
4. Na conta de Armazenamento do Azure que você criou, no painel de menu esquerdo, selecione **Configuração** (em **Configurações**).
5. Altere a configuração de Permitir acesso anônimo de Blob para Habilitado e selecione Salvar.

#### Carregar documentos para o armazenamento do Azure
1. No painel do menu esquerdo, selecione **Containers**.
![image](https://github.com/barbarawo/azure-ai-search/assets/162802729/0e1a4030-f77c-47b0-bc31-89d6b9f8d6d4)

2. Selecione **+ Contêiner**. Um painel do seu lado direito é aberto.
3. Insira as seguintes configurações e clique em **Criar**:
    - **Nome**: Coffee-Reviews
    - **Nível de acesso público**: Container (acesso de leitura anônimo para containers e blobs)
    - **Avançado**: sem alterações.

4. Em uma nova guia do navegador, baixe as avaliações de café compactadas em *https://aka.ms/mslearn-coffee-reviewse* extraia os arquivos para a pasta de avaliações.
5. No portal do Azure, selecione o contêiner de avaliações de café . No contêiner, selecione **Carregar**.
![image](https://github.com/barbarawo/azure-ai-search/assets/162802729/653a03ee-f316-49de-a3f3-185cdad5042a)

6. No painel **Carregar blob**, selecione **Selecionar um arquivo**.
7. Na janela do Explorer, selecione **todos** os arquivos na pasta de *avaliações*, selecione **Abrir** e, em seguida, selecione **Carregar**.
![image](https://github.com/barbarawo/azure-ai-search/assets/162802729/fd6b04b1-9090-4919-9ce4-105eb4539c94)

8. Depois que o upload for concluído, você poderá fechar o painel **Upload blob**. Seus documentos estão agora em seu contêiner de armazenamento de avaliações de *café*.

#### Indexar os documentos
Depois de armazenar os documentos, você poderá usar o Azure AI Search para extrair insights dos documentos. O portal do Azure fornece um *assistente de importação de dados*. Com este assistente, você pode criar automaticamente um índice e um indexador para fontes de dados suportadas. Você usará o assistente para criar um índice e importar seus documentos de pesquisa do armazenamento para o índice do Azure AI Search.

1. No portal do Azure, navegue até o recurso Azure AI Search. Na página **Visão geral**, selecione **Importar dados**.
![image](https://github.com/barbarawo/azure-ai-search/assets/162802729/79d6c8f0-1fc0-4511-9c44-2cfbea28c385)

2. Na página **Conectar-se aos seus dados**, na lista **Fonte de Dados**, selecione **Azure Blob Storage**. Preencha os detalhes do armazenamento de dados com os seguintes valores:
    - **Fonte de dados**: Armazenamento de Blobs do Azure
    - **Nome da fonte de dados**: coffee-customer-data
    - **Dados a extrair**: Conteúdo e metadados
    - **Modo de análise**: Padrão
    - **Cadeia de conexão**: Selecione **Escolha uma conexão existente**. Selecione sua conta de armazenamento, selecione o contêiner **de avaliações de café** e clique em **Selecionar**.
    - **Autenticação de identidade gerenciada**: Nenhuma
    - **Nome do contêiner**: *esta configuração é preenchida automaticamente depois que você escolhe uma conexão existente*.
    - **Pasta Blob**: *deixe em branco*.
    - **Descrição**: Avaliações sobre Fourth Coffee Shops.
3. Selecione **Próximo: Adicionar habilidades cognitivas (opcional)**.
4. Na secção **Anexar Serviços Cognitivos**, selecione o seu recurso de serviços Azure AI.
5. Na seção **Adicionar enriquecimentos**:
    - Altere o **nome da qualificação** para **coffee-skillset**.
    - Marque a caixa de seleção **Habilitar OCR e mesclar todo o texto no campo merged_content**.
    - Certifique-se de que o **campo Dados de origem** esteja configurado como **merged_content**.
    - Altere o **nível de granularidade de enriquecimento** para **Páginas (blocos de 5.000 caracteres)**.
    - Não selecione Habilitar enriquecimento incremental
    - Selecione os seguintes campos enriquecidos:


  | Habilidade Cognitiva	   | Nome do campo     |
  | ------------------------ | ----------------- |
  | Extraia nomes de locais  | Localizações      |
  | Extraia frases-chave     | frases chave      |
  | Detectar sentimento      | sentimento        |
  | Gerar tags de imagens    | imagemTags        |
  | Gere legendas de imagens | legenda da imagem |


6. Em **Salvar enriquecimentos em um armazenamento de conhecimento**, selecione:
    - Projeções de imagem
    - Documentos
    - Páginas
    - Frases chave
    - Entidades
    - Detalhes da imagem
    - Referências de imagem
7. Selecione **projeções de blob do Azure: Documento**. Uma configuração para o nome do contêiner com as exibições preenchidas automaticamente do *contêiner de armazenamento de conhecimento*. Não altere o nome do contêiner.
8. Selecione **Próximo: Personalizar índice de destino**. Altere o **nome do índice** para **coffee-index**.
9. Certifique-se de que a **chave** esteja configurada como **metadata_storage_path**. Deixe **o nome do sugeridor** em branco e **o modo de pesquisa** preenchido automaticamente.
10. Revise as configurações padrão dos campos de índice. Selecione **filtrável** para todos os campos que já estão selecionados por padrão.
![image](https://github.com/barbarawo/azure-ai-search/assets/162802729/567b3fc5-b035-4fda-b4ca-373a18da3f7d)

11. Selecione **Próximo: Criar um indexador**.
12. Altere o **nome do indexador** para **coffee-indexer**.
13. Deixe a **programação** definida como **Once**.
14. Expanda as **opções avançadas**. Certifique-se de que a opção **Base-64 Encode Keys** esteja selecionada, pois as chaves de codificação podem tornar o índice mais eficiente.
15. Selecione **Enviar** para criar a fonte de dados, o conjunto de habilidades, o índice e o indexador. O indexador é executado automaticamente e executa o pipeline de indexação, que:
    - Extrai os campos de metadados do documento e o conteúdo da fonte de dados.
    - Executa o conjunto de habilidades cognitivas para gerar campos mais enriquecidos.
    - Mapeia os campos extraídos para o índice.
16. Volte à página de recursos do Azure AI Search. No painel esquerdo, em **Gerenciamento de pesquisa**, selecione **Indexadores**. Selecione o **indexador de café** recém-criado. Espere um minuto e selecione **↻ Atualize** até que o **Status** indique sucesso.
17. Selecione o nome do indexador para ver mais detalhes.
![image](https://github.com/barbarawo/azure-ai-search/assets/162802729/7bdd01da-436f-4c55-b6e0-f65bb48b79c3)

#### Consultar o índice
Use o Search Explorer para escrever e testar consultas. O explorador de pesquisa é uma ferramenta incorporada no portal do Azure que oferece uma maneira fácil de validar a qualidade do seu índice de pesquisa. Você pode usar o Search Explorer para escrever consultas e revisar resultados em JSON.

#### Revise o armazenamento de conhecimento
Vamos ver o poder do armazenamento de conhecimento em ação. Ao executar o assistente *Importar dados*, você também criou um armazenamento de conhecimento. Dentro do armazenamento de conhecimento, você encontrará os dados enriquecidos extraídos pelas habilidades de IA que persistem na forma de projeções e tabelas.

