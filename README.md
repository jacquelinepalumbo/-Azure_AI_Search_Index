# Explore an Azure AI Search index (UI)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-000?style=for-the-badge&logo=LinkedIn&logoColor=30A3DC)](https://www.linkedin.com/in/jacqueline-ribeiro-743876247/)

_Vamos imaginar que você trabalhe para a Fourth Coffee, uma rede nacional de cafés. Você é solicitado a ajudar a criar uma solução de mineração de conhecimento que facilite a pesquisa de insights sobre as experiências do cliente. Você decide criar um índice de Pesquisa de IA do Azure usando dados extraídos de avaliações de clientes._

_Neste laboratório você irá:_

* Criar recursos do Azure
* Extrair dados de uma fonte de dados
* Enriqueça dados com habilidades de IA
* Usar o indexador do Azure no portal do Azure
* Consultar seu índice de pesquisa
* Revisar resultados salvos em um Knowledge Store



# Recursos do Azure necessários

A solução que você criará para o Fourth Coffee requer os seguintes recursos em sua assinatura do Azure:

* Um recurso **de Pesquisa de IA do Azure**, que gerenciará a indexação e a consulta.
* Um recurso **de serviços de IA do Azure**, que fornece serviços de IA para habilidades que sua solução de pesquisa pode usar para enriquecer os dados na fonte de dados com insights gerados por IA.

* Uma **conta de armazenamento** com contêineres de blob, que armazenará documentos brutos e outras coleções de tabelas, objetos ou arquivos.

## Criar um recurso de _Pesquisa de IA do Azure_

1. Entre no [portal do Azure](https://portal.azure.com/?azure-portal=true#home).

2. Clique no botão **+ Criar um recurso**, procure Pesquisa de IA do Azure e crie um recurso **de Pesquisa de IA do Azure** com as seguintes configurações:

* **Assinatura**: _sua assinatura do Azure_.
* **Grupo de recursos**: _selecione ou crie um grupo de recursos com um nome exclusivo_.
* **Nome do serviço**: _um nome exclusivo_.
* **Localização**: _Escolha qualquer região disponível_.
* **Nível** de preços: Básico

3. Selecione **Revisar + criar** e, depois de ver a resposta **Êxito da validação**, selecione **Criar**.

4. Após a conclusão da implantação, selecione **Ir para o recurso**. Na página de visão geral da Pesquisa de IA do Azure, você pode adicionar índices, importar dados e pesquisar índices criados.

## Criar um recurso de serviços de IA do Azure

Você precisará provisionar um recurso **de serviços de IA do Azure** que esteja no mesmo local que seu recurso de Pesquisa de IA do Azure. Sua solução de pesquisa usará esse recurso para enriquecer os dados no armazenamento de dados com insights gerados por IA.

1. Retorne à home page do portal do Azure. Clique no botão **+Criar um recurso** e procure serviços de IA do Azure. Selecione **criar** um plano de **serviços de IA do Azure**. Você será levado a uma página para criar um recurso de **serviços de IA do Azure**. Configure-o com as seguintes configurações:

* **Assinatura**: sua assinatura do Azure.
* **Grupo de recursos**: o mesmo grupo de recursos que seu recurso de Pesquisa de IA do Azure.
* **Região**: o mesmo local que seu recurso de Pesquisa de IA do Azure.
* **Nome**: Um nome exclusivo.
* **Nível de preços**: Standard S0
**Ao marcar esta caixa reconheço que li e compreendi todos os termos abaixo**: Selecionado

2.Selecione **Revisar + criar**. Depois de ver a resposta Validação aprovada, selecione Criar.

3. Aguarde a conclusão da implantação e exiba os detalhes da implantação.

## Criar uma conta de armazenamento

1.Retorne à home page do portal do Azure e selecione o botão + Criar um recurso.

2. Procure uma conta de armazenamento e crie um recurso de conta de armazenamento com as seguintes configurações:

* **Assinatura**: _sua assinatura do Azure_.
* **Grupo de recursos**: _o mesmo grupo de recursos que os recursos da Pesquisa de IA do Azure e dos serviços de IA do Azure_.
* **Nome da conta de armazenamento**: _um nome exclusivo_.
* **Localização**: Escolha qualquer local disponível.
* **Desempenho**: Standard
* **Redundância**: Armazenamento localmente redundante (LRS)
  
3. Clique em **Rever** e, em seguida, clique em **Criar**. Aguarde a conclusão da implantação e vá para o recurso implantado.

4. Na conta de Armazenamento do Azure que você criou, no painel de menu esquerdo, selecione **Configuração** (em **Configurações**).

5. Altere a configuração de _Permitir acesso anônimo de Blob_ para **Habilitado** e selecione **Salvar**.

# Carregar documentos no Armazenamento do Azure

1. No painel de menu esquerdo, selecione **Contêineres**.

![image](https://github.com/jacquelinepalumbo/-Azure_AI_Search_Index/assets/119548193/185b09da-6f13-4802-a924-7a90d53cd56b)


2. Selecione **+ Contêiner**. Um painel do lado direito é aberto.

3. Insira as seguintes configurações e clique em **Criar**:

* **Nome**: café-comentários
* **Nível de acesso público**: Contêiner (acesso de leitura anônimo para contêineres e blobs)
* **Avançado: sem alterações**.

4. Em uma nova guia do navegador, baixe as revisões de café compactadas do e extraia os arquivos para a pasta _de comentários_.`https://aka.ms/mslearn-coffee-reviews`

5. No portal do Azure, selecione seu contêiner de _avaliações de café_. No contêiner, selecione **Carregar**.

![image](https://github.com/jacquelinepalumbo/-Azure_AI_Search_Index/assets/119548193/fc1aac1c-4535-47fb-8f6e-d8364606a93e)

6. No painel **Carregar blob**, selecione **Selecionar um arquivo**.

7. Na janela do Explorer, selecione **todos os** arquivos na pasta de _comentários_, selecione **Abrir** e selecione **Carregar**.

![image](https://github.com/jacquelinepalumbo/-Azure_AI_Search_Index/assets/119548193/68084cfe-d41f-4200-9ec9-7c3163cb31e3)

8. Depois que o carregamento for concluído, você poderá fechar o painel **Carregar blob**. Seus documentos agora estão em seu recipiente de armazenamento de _revisões de café_.

# Indexar os documentos

Depois de ter os documentos em armazenamento, você pode usar o Azure AI Search para extrair insights dos documentos. O portal do Azure fornece um _assistente de Importação de dados_. Com esse assistente, você pode criar automaticamente um índice e um indexador para fontes de dados com suporte. Você usará o assistente para criar um índice e importar seus documentos de pesquisa do armazenamento para o índice de Pesquisa de IA do Azure.

1. No portal do Azure, navegue até seu recurso de Pesquisa de IA do Azure. Na página **Visão geral**, selecione **Importar dados**.

<img width="737" alt="image" src="https://github.com/jacquelinepalumbo/-Azure_AI_Search_Index/assets/119548193/56838a41-8e92-4bc6-ac1f-a045f8ea2525">

2. Na página **Conectar aos seus dados**, na lista **Fonte de Dados**, selecione **Armazenamento de Blobs do Azure**. Conclua os detalhes do armazenamento de dados com os seguintes valores:
   
* **Fonte de dados**: Armazenamento de Blobs do Azure
* **Nome da fonte de dados**: coffee-customer-data
* **Dados a serem extraídos**: conteúdo e metadados
* **Modo de análise**: Padrão
* **Cadeia de conexão**: *Selecione **Escolher uma conexão existente**. Selecione sua conta de armazenamento, selecione o contêiner **de revisões de café** e clique em **Selecionar**.
* **Autenticação de identidade gerenciada**: Nenhuma
* **Nome do contêiner**: essa configuração é preenchida automaticamente depois que você escolhe uma conexão existente.
* **Pasta Blob**: deixe isso em branco.
* **Descrição**: Comentários a Fourth Coffee shops.

3. Selecione **Avançar: Adicionar habilidades cognitivas (Opcional)**.

4. Na seção **Anexar Serviços Cognitivos**, selecione seu recurso de serviços de IA do Azure.

5. Na seção **Adicionar enriquecimentos**:

* Altere o **nome do Skillset** para **coffee-skillset**.
* Marque a caixa **de seleção Habilitar OCR e mesclar todo merged_content texto em campo**.

* Verifique se o **campo Dados de origem** está definido como **merged_content**.
* Altere o **nível de granularidade de enriquecimento** para **Páginas (blocos de 5000 caracteres**).
* Não selecione _Habilitar enriquecimento incremental_
* Selecione os seguintes campos enriquecidos:

| Habilidade Cognitiva | Parâmetro | Nome do campo |
| --- | --- |--- |
|Extrair nomes de locais      |     |		Locais|
|Extrair frases-chave         |     |	 Frases-chave|
|Detectar sentimento          |     |		sentimento|
|Gerar tags a partir de imagens |   |	imageTags|
|Gerar legendas a partir de imagens | |		imageCaption|

6. Em **Salvar enriquecimentos em um repositório de conhecimento**, selecione:

* Projeções de imagens
* Documentos
* Páginas
* Frases-chave
* Entidades
* Detalhes da imagem
* Referências de imagens

7. Selecione **Projeções de blob do Azure**: Documento. 
Uma configuração para _Nome do contêiner_ com as exibições preenchidas automaticamente pelo contêiner do _repositório de conhecimento_. Não altere o nome do contêiner.

8. Selecione **Avançar: Personalizar índice de destino. Altere o nome do índice** para **coffee-index**.

9. Verifique se a **chave** está definida como **metadata_storage_path**. Deixe **o nome do Sugeridor** em branco e **o modo de Pesquisa** preenchido automaticamente.

10. Revise as configurações padrão dos campos de índice. Selecione **filtrável** para todos os campos que já estão selecionados por padrão.

<img width="679" alt="image" src="https://github.com/jacquelinepalumbo/-Azure_AI_Search_Index/assets/119548193/787a2a2d-e61c-4207-b4bb-a1525e75513f">


11. Selecione **Avançar: Criar um indexador**.

12. **Altere o nome do indexador** para **coffee-indexer**.

13. Deixe a **Agenda** definida como **Uma vez**.

14. Expanda as **opções Avançadas**. Verifique se a opção **Base-64 Encode Keys** está selecionada, pois as chaves de codificação podem tornar o índice mais eficiente.

15. Selecione **Enviar** para criar a fonte de dados, o conjunto de habilidades, o índice e o indexador. O indexador é executado automaticamente e executa o pipeline de indexação, que:
    
* Extrai os campos de metadados do documento e o conteúdo da fonte de dados.
* Executa o conjunto de habilidades cognitivas para gerar campos mais enriquecidos.
* Mapeia os campos extraídos para o índice.

16. Retorne à página de recursos da Pesquisa de IA do Azure. No painel esquerdo, em **Gerenciamento de Pesquisa**, selecione **Indexadores**. Selecione o **indexador de café recém-criado**. Aguarde um minuto e selecione **&orarr; Atualize** até que o **Status** indique êxito.

17. Selecione o nome do indexador para ver mais detalhes.

<img width="450" alt="image" src="https://github.com/jacquelinepalumbo/-Azure_AI_Search_Index/assets/119548193/ce66430e-50bd-4075-895f-70a8c8b6c703">

# Consultar o índice

Use o Gerenciador de pesquisa para escrever e testar consultas. O explorador de pesquisa é uma ferramenta incorporada no portal do Azure que oferece uma maneira fácil de validar a qualidade do seu índice de pesquisa. Você pode usar o Gerenciador de Pesquisa para escrever consultas e revisar resultados em JSON.

1. Na página _Visão geral_ do serviço de Pesquisa, selecione **Gerenciador de pesquisa** na parte superior da tela.

<img width="500" alt="image" src="https://github.com/jacquelinepalumbo/-Azure_AI_Search_Index/assets/119548193/5d9a108f-6726-4911-be24-52e8fe6cc51f">

2. Observe como o índice selecionado é o _índice de café_ que você criou. Abaixo do índice selecionado, altere a exibição para **JSON view**.

<img width="506" alt="image" src="https://github.com/jacquelinepalumbo/-Azure_AI_Search_Index/assets/119548193/a915c153-e0e7-49a6-93cc-95c3b7a2e037">

No campo **Editor de consultas JSON**, copie e cole:

``{
    "search": "*",
    "count": true
}``

1. Selecione **Pesquisar**. A consulta de pesquisa retorna todos os documentos no índice de pesquisa, incluindo uma contagem de todos os documentos no campo **@odata.count**. O índice de pesquisa deve retornar um documento JSON contendo os resultados da pesquisa.

2. Agora vamos filtrar por localização. No campo **Editor de consultas JSON**, copie e cole:

``{
 "search": "locations:'Chicago'",
 "count": true
}``

3. Selecione **Pesquisar**. A consulta pesquisa todos os documentos no índice e filtra por revisões com um local de Chicago. Você deve ver no campo. ``1@odata.count``

4. Agora vamos filtrar por sentimento. No campo **Editor de consultas JSON**, copie e cole:

``{
 "search": "sentiment:'negative'",
 "count": true
}``

5. Selecione **Pesquisar**. A consulta pesquisa todos os documentos no índice e filtra por avaliações com um sentimento negativo. Você deve ver no campo. ``1@odata.count``

6. Um dos problemas que podemos querer resolver é por que pode haver certas revisões. Vamos dar uma olhada nas frases-chave associadas à avaliação negativa. O que você acha que pode ser a causa da revisão?

# Revisar o repositório de conhecimento

Vamos ver o poder do armazenamento de conhecimento em ação. Ao executar o _assistente Importar dados_, você também criou um repositório de conhecimento. Dentro da loja de conhecimento, você encontrará os dados enriquecidos extraídos pelas habilidades de IA persistem na forma de projeções e tabelas.

1. No portal do Azure, navegue de volta para sua conta de armazenamento do Azure.

2. No painel de menu esquerdo, selecione **Contêineres**. Selecione o contêiner **de armazenamento de conhecimento**.

 <img width="506" alt="image" src="https://github.com/jacquelinepalumbo/-Azure_AI_Search_Index/assets/119548193/3c80d208-4a8c-47d0-81a4-d0672bee9b58">

3. Selecione qualquer um dos itens e clique no arquivo **objectprojection.json**.

<img width="506" alt="image" src="https://github.com/jacquelinepalumbo/-Azure_AI_Search_Index/assets/119548193/01b302ed-dfa8-4090-ab82-0bf691722632">


4. Selecione  **Editar ** para ver o JSON produzido para um dos documentos do armazenamento de dados do Azure.

<img width="599" alt="image" src="https://github.com/jacquelinepalumbo/-Azure_AI_Search_Index/assets/119548193/3e643759-7a97-415f-bc7c-60f269a62f37">

5. Selecione a trilha de blob de armazenamento no canto superior esquerdo da tela para retornar aos _Contêineres_ da conta de armazenamento.

<img width="693" alt="image" src="https://github.com/jacquelinepalumbo/-Azure_AI_Search_Index/assets/119548193/4c57d1bf-1432-4874-81f7-978ffb5d0bf7">

6. Em _Contêineres_, selecione o contêiner _coffee-skillset-image-projection_. Selecione qualquer um dos itens.
<img width="572" alt="image" src="https://github.com/jacquelinepalumbo/-Azure_AI_Search_Index/assets/119548193/a6a99dea-fe0d-4a93-870d-3ba84b99cc46">


7. Selecione qualquer um dos _.jpg arquivos_. Selecione **Editar** para ver a imagem armazenada do documento. Observe como todas as imagens dos documentos são armazenadas dessa maneira.
<img width="581" alt="image" src="https://github.com/jacquelinepalumbo/-Azure_AI_Search_Index/assets/119548193/b7725f05-27d0-420c-bbe6-da5182b4b665">


8. Selecione a trilha de blob de armazenamento no canto superior esquerdo da tela para retornar aos _Contêineres_ da conta de armazenamento.

9. Selecione **Navegador de armazenamento** no painel esquerdo e selecione **Tabelas**. Há uma tabela para cada entidade no índice. Selecione a tabela _coffeeSkillsetKeyPhrases_.

Veja as frases-chave que a loja de conhecimento conseguiu capturar do conteúdo das avaliações. Muitos dos campos são chaves, portanto, você pode vincular as tabelas como um banco de dados relacional. O último campo mostra as frases-chave que foram extraídas pelo conjunto de habilidades.
