# Explore an Azure AI Search index (UI)

_Vamos imaginar que você trabalhe para a Fourth Coffee, uma rede nacional de cafés. Você é solicitado a ajudar a criar uma solução de mineração de conhecimento que facilite a pesquisa de insights sobre as experiências do cliente. Você decide criar um índice de Pesquisa de IA do Azure usando dados extraídos de avaliações de clientes._

_Neste laboratório você irá:_

* Criar recursos do Azure
* Extrair dados de uma fonte de dados
* Enriqueça dados com habilidades de IA
* Usar o indexador do Azure no portal do Azure
* Consultar seu índice de pesquisa
* Revisar resultados salvos em um Knowledge Store

[![LinkedIn](https://img.shields.io/badge/LinkedIn-000?style=for-the-badge&logo=LinkedIn&logoColor=30A3DC)](https://www.linkedin.com/in/jacqueline-ribeiro-743876247/)

# Recursos do Azure necessários

A solução que você criará para o Fourth Coffee requer os seguintes recursos em sua assinatura do Azure:

* Um recurso **de Pesquisa de IA do Azure**, que gerenciará a indexação e a consulta.
* Um recurso **de serviços de IA do Azure**, que fornece serviços de IA para habilidades que sua solução de pesquisa pode usar para enriquecer os dados na fonte de dados com insights gerados por IA.

* Uma **conta de armazenamento** com contêineres de blob, que armazenará documentos brutos e outras coleções de tabelas, objetos ou arquivos.

## Criar um recurso de _Pesquisa de IA do Azure_

1. Entre no [portal do Azure](https://login.microsoftonline.com/).

2. Clique no botão **+ Criar um recurso**, procure Pesquisa de IA do Azure e crie um recurso **de Pesquisa de IA do Azure** com as seguintes configurações:

* **Assinatura**: _sua assinatura do Azure_.
* **Grupo de recursos**: _selecione ou crie um grupo de recursos com um nome exclusivo_.
* **Nome do serviço**: _um nome exclusivo_.
* **Localização**: _Escolha qualquer região disponível_.
* **Nível** de preços: Básico

3. Selecione **Revisar + criar** e, depois de ver a resposta **Êxito da validação**, selecione **Criar**.

4. Após a conclusão da implantação, selecione **Ir para o recurso**. Na página de visão geral da Pesquisa de IA do Azure, você pode adicionar índices, importar dados e pesquisar índices criados.
