# Documentação da API de Integração de Anúncios da OLX

## IMPORTANTE: A OLX está prestes a lançar uma **nova versão de sua API de Integração de Anúncios**. Este doc explica o funcionamento da API e detalha a mudança. Se você já está integrado, [veja aqui o que muda](autoupload_taffarel.md).

A API de Importação de Anúncios da OLX contempla as seguintes funcionalidades:

| Funcionalidade                       | Descrição                                                                                                             | Status             |
|--------------------------------------|-----------------------------------------------------------------------------------------------------------------------|--------------------|
| [Autenticação oAuth](oauth.md)                   | Permite que anunciantes autentiquem via integrador para configurar integração com OLX                                 | Disponível            |
| [Importação (Inserção/Edição/Deleção)](import.md) | Permite gestão do inventário de anúncios publicados na OLX.                                                           | Em rollout         |
| Status de Publicação                 | Informa o anunciante/integrador sobre o sucesso da publicação de um anúncio, bem como o motivo de uma não-publicação. | Em desenvolvimento |
| [Marcas/Modelos de Carros/Motos](autos/car_models.md)             | Disponibiliza o catálogo de marcas e modelos de carros e motos que podem ser publicados na OLX                                | Disponível            |
| [Anúncios Publicados](published_ads.md)       | Lista todos os anúncios publicados, para o anunciante ter controle de quais anúncios estão disponívels na OLX no momento.                         | Disponível      |


## Por que uma nova API de Importação?

Estamos construindo uma nova API para atacar diferentes restrições técnicas e de negócio da Integração de Anúncios proporcionada pela API atual. Ela vai substituir duas rotas existentes na API atual: a rota de importação e a rota de status de publicação.

Os principais benefícios da mudança:

- **Suporte para todas as categorias de anúncios da OLX**<br>
A API atual é restrita para algumas categorias (Imóveis e Automóveis). A nova versão será flexível para atender qualquer categoria de anúncio existente na OLX.
- **Consistência na contagem de anúncios inseridos**<br>
Um dos pontos críticos da API atual é a discrepância entre o limite disponível para inserção de anúncios que é exibido na área do anunciante da OLX e a resposta da API. A nova API manterá consistência ao informar o limite disponível de inserção.
- **Melhorias técnicas na importação**<br>
Por baixo dos panos a nova API trará maior robustez, auxiliando na correção de erros e permitindo melhorias. Erros que hoje acontecem correntemente e melhorias que já identificamos (e são inviáveis de serem realizadas na API atual) já serão atendidas com a nova API.


## O que muda com a nova API?

Fora os benefícios acima, do ponto de vista técnico muda pouca coisa. Em especial, algumas validações que eram síncronas passam a ser assíncronas. 

Isso significa mudança nas rotas de `Importação` e `Status de Importação`, pois parte das validações deixam de acontecer sincronamente (alterando retorno das chamadas de Inserção ou Edição de Anúncios) e passarão a estar disponíveis e visíveis via rota de `Status de Publicação`. 

Para ter mais detalhes, [veja aqui o que muda com a nova API](autoupload_taffarel.md).


## Quais as fases do rollout?

### 1) **Chamadas à API**: Em andamento, com finalização em 30/08/19

A partir de 30/08/19, as chamadas para a API terão que respeitar o modelo abaixo:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**Rota Inserção, edição e deleção**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`PUT /autoupload/import`<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;header: `Content-type: application/json`

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**Status**<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`POST /autoupload/import/{id}`<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;header: `Content-type: application/json`

### 2) **Rota de Importação**: Início de setembro

No início de Setembro vamos começar a comunicar e virar os integradores elegíveis para a API 2.0, modificando apenas a rota de importação. 

### 3) **Rota de Status**: Final de setembro

Ao final de setembro, vamos virar o restante dos integradores para a nova API, desta vez alterando tanto as rotas de importação quanto a rota de status de publicação.


## Quero me integrar com a OLX

Como estamos para colocar no ar uma nova versão da API de Importação de Anúncios, é recomendável que você já faça a integração na nova versão. Para isso, entre em contato com suporteintegrador@olxbr.com ou abra um issue aqui neste repositório.

Verifique cada funcionalidade da API OLX e desenvolva do seu lado para realizar a integração conosco:

| Funcionalidade                       | Descrição                                                                                                             | Status             |
|--------------------------------------|-----------------------------------------------------------------------------------------------------------------------|--------------------|
| [Autenticação oAuth](oauth.md)                   | Permite que anunciantes autentiquem via integrador para configurar integração com OLX                                 | Disponível            |
| [Importação (Inserção/Edição/Deleção)](import.md) | Permite gestão do inventário de anúncios publicados na OLX.                                                           | Em rollout         |
| Status de Publicação                 | Informa o anunciante/integrador sobre o sucesso da publicação de um anúncio, bem como o motivo de uma não-publicação. | Em desenvolvimento |
| [Marcas/Modelos de Carros/Motos](autos/car_models.md)             | Disponibiliza o catálogo de marcas e modelos de carros e motos que podem ser publicados na OLX                                | Disponível            |
| [Anúncios Publicados](published_ads.md)       | Lista todos os anúncios publicados, para o anunciante ter controle de quais anúncios estão disponívels na OLX no momento.                         | Disponível      |


# Dúvidas e sugestões

Se tiver dificuldades ou sugestões, [abra uma Issue nesse repositório](https://github.com/olxbr/ad_integration/issues/new) e a equipe de desenvolvimento da OLX vai responder seu contato. Em casos urgentes, entre em contato com suporteintegrador@olxbr.com. Se tiver sugestões ou quiser conversar sobre a integração de anúncios, [agende um *call* com o Gerente de Produto do time de Integrações](https://calendly.com/renato-cairo-olx/papo_integracao_olx).