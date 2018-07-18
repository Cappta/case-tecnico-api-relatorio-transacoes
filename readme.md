# Teste prático - API de Relatório de Transações

Mesmo numa era digital, ainda é extremamente comum o lojista realizar o fechamento do caixa de maneira manual comparando as informações dos comprovantes emitidos no POS (aquela maquininha de cartão que imprimi o comprovante no momento da venda) com as informações geradas pelo seu sistema de vendas. Uma excelente forma de resolver esse problema é utilizar nosso sistema integrador TEF (Transferencias Eletrônicas de Fundos) para realizar as transações de pagamento a partir de um PDV integrado, através de nossos SDKs, com a automação comercial do cliente utilizando um PinPad (aquelas maquininhas que normalmente são vistas nos caixas de supermercado ou farmácias) para capturar os dados do cartão do consumidor.

A Cappta tem como propósito tornar a vida do empreendedor brasileiro mais fácil e para isso, buscamos prover soluções tecnologicas como a API de Relatório de Transações que é responsável por alimentar um portal onde o empreendedor é capaz de acompanhar todas as vendas realizadas, podendo filtrá-las por data, bandeira, adiquirente, entre outros filtros.

- ***Bandeira*** - são empresas que regulam o mercado de cartões de crédito, estabelecendo o padrão sob o qual as adquirentes devem processar seus cartões e a precificação dos diferentes estabelecimentos. São empresas como a VISA, Mastercard, Elo, entre outras.

- ***Adquirente*** - são membros licenciados que analisam e aceitam estabelecimentos em seus programas de cartões e processos de transações financeiras. São empresas como a Stone, Cielo, Rede, GetNet, entre outras.

## Qual é o desafio?

O seu desafio será implementar uma API Restful que seja capaz gerar relatórios em json para que possa ser consumida pelas automações comerciais que integram com nosso integrador TEF. Para isso será necessário que a API permita obter os relatórios filtrando-os por cnpj do lojista, data, bandeira ou adquirente e esses filtros poderão ser compostos por mais de um parâmetro, ou seja, deverá pemitir a busca pelas bandeiras VISA e Mastercard na mesma requisição e também deverá permitir a filtragem das vendas do cnpj realizadas pela bandeira Mastercard na data atual e as ultimas vendas realizadas pela adquirente Stone nos ultimos 30 dias.

*IMPORTANTE!* Como o volume de transações de pagamento realizadas ao longo do dia pode chegar à centenas de milhares de transações, o custo computacional para processar uma requisição deste tipo é bastante alto, sem contar que o relatório devolvido em json terá um tamanho muito grande, impactando na performance da entrega da resposta e também no consumo dos dados por parte dos clientes.

### O formato de resposta devolvido pela API deverá ser semelhante ao abaixo

``` json
{
    "results": [
        {
            "merchantCnpj": "77404852000179",
            "checkoutCode": 36245,
            "cipheredCardNumber": "************8082",
            "amountInCents": 1001,
            "installments": 1,
            "acquirerName": "Cielo",
            "paymentMethod": "Débito à Vista",
            "cardBrandName": "Elo Debito",
            "status": "Aprovada",
            "statusInfo": "Transação autorizada pela adquirente.",
            "CreatedAt": "2018-03-01T01:02:34",
            "AcquirerAuthorizationDateTime": "2018-03-01T01:02:38"
        },
        {
            "merchantCnpj": "30481457000126",
            "checkoutCode": 39206,
            "cipheredCardNumber": "************9077",
            "amountInCents": 3785,
            "installments": 1,
            "acquirerName": "Cielo",
            "paymentMethod": "Débito à Vista",
            "cardBrandName": "Elo Debito",
            "status": "Aprovada",
            "statusInfo": "Transação autorizada pela adquirente.",
            "CreatedAt": "2018-03-04:00:52",
            "AcquirerAuthorizationDateTime": "2018-03-04:00:52"
        },
        ...
    ]
}
```

Para que você se concentre apenas no código, disponibilizamos uma planilha com dados que você poderá importar para o SGBD de sua preferencia, aqui utilizamos o SQL Server! No entanto o use dessa base de dados é opcional. [Clique aqui](transactions.csv) para baixá-la.

## Como será a avaliação?

O nosso intuito é olhar como é seu estilo de programação e quais decisões você toma ao resolver um problema. Portanto, coloque seu projeto em um repositório de versionamento público, tal como o GitHub, Bitbucket ou outro de sua preferência. Essa etapa é muito importante que consigamos clonar seu repositório para podermos avaliar o seu projeto. Após concluir o case, você deverá abrir um pull request para nós através do Github ou nos enviar por e-mail o link do repositório por e-mail para ***desenvolvimento@cappta.com.br*** ou ***fernando.seguim@cappta.com.br*** com o assunto "Case Técnico - Cappta - [Seu nome e sobrenome]"  para que possamos acessá-lo.

*IMPORTANTE!* Caso você opte enviar o projeto por anexo e-mail, dropbox, google drive ou outra forma que não seja plataforma de versionamento, tenha em mente que o projeto será desconsiderado automaticaticamente.

*NOTA:* Não será necessário hospedar a API em nenhum provedor de hospedagem ou serviço cloud, isso não será levado em consideração na sua avaliação.

O prazo para realização e envio do teste é de 7 dias a partir da data de envio do e-mail.

### Os principais pontos que serão observados são:


- Qualidade do código
- Bom uso de SOLID
- Aplicação adequada de design patterns
- Domínio sobre Resful
- Domínio sobre a escrita de testes unitários
- Decisões tomadas em relação à arquitetura da API
- Cuidado com o versionamento do código

No entanto não se limite a isso, sinta-se livre para criar em cima do problema proposto. Caso algo não esteja claro, pode assumir o que for para você, apenas indique suas suposições em documentação. Aproveite a oportunidade para aprender coisas novas e colocar em prática o seu conhecimento!

Ah! Já ia me esquecendo, você também é livre para decidir qual linguagem e tecnologias irá utilizar, mas se preferir se orientar por nossa stack, atualmente utilizamos C# em .Net Core para os novos projetos, além de JavaScript, React e SQL Server como SGBD relacional.

Qualquer dúvida maior pode nos perguntar, mas no geral, divirta-se! :nerd_face: :green_heart:
