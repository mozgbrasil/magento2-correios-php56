![valid XHTML][checkmark]
[checkmark]: https://raw.githubusercontent.com/mozgbrasil/mozgbrasil.github.io/master/assets/images/logos/Red_star_32_32.png "MOZG"
[url-method]: http://correios.com.br/
[requirements]: http://mozgbrasil.github.io/requirements/
[limites-de-dimensoes-e-de-peso]: http://www.correios.com.br/para-voce/precisa-de-ajuda/limites-de-dimensoes-e-de-peso
[mao-propria-mp]: http://www.correios.com.br/para-voce/correios-de-a-a-z/mao-propria-mp
[aviso-de-recebimento-ar]: http://www.correios.com.br/para-voce/correios-de-a-a-z/aviso-de-recebimento-ar
[valor-declarado]: http://www.correios.com.br/para-voce/correios-de-a-a-z/valor-declarado
[contact-correios]: http://www2.correios.com.br/sistemas/falecomoscorreios/
[encomendas-prazo]: http://www2.correios.com.br/sistemas/precosprazos/default.cfm
[magento-cron]: http://devdocs.magento.com/guides/v2.0/config-guide/cli/config-cli-subcommands-cron.html
[tickets]: https://cerebrum.freshdesk.com/support/tickets/new
[preco]: http://www.cerebrum.com.br/preco/
[github-boxpacker]: https://github.com/mozgbrasil/magento-boxpacker-php56#mozgboxpacker
[getcomposer]: https://getcomposer.org/
[uninstall-mods]: http://devdocs.magento.com/guides/v2.1/install-gde/install/cli/install-cli-uninstall-mods.html

# Mozg\Correios

## Sinopse

Integração ao [Correios][url-method]

## Motivação

Atender o mercado de módulos para Magento oferecendo melhorias e um excelente suporte

## Suporte / Dúvidas

Para obter o devido suporte [Clique aqui][tickets], relatando o motivo da ocorrência o mais detalhado possível e anexe o print da tela para nosso entendimento

## Preço

[Clique aqui][preco]

## Recursos

- Definir dimensões para os produtos

- Definir dimensões, peso e valor da Embalagem/Caixa

- Opção para embalar os produtos separadamente ou combinar na mesma Embalagem/Caixa

- Embalagem do produto inteligente, exibe como os produtos serão agrupados e calcula o peso dimensional fazendo o envio fracionado se necessário

- Armazenamento das requisições em Cache

- Notificação automática do rastreamento

~~- Definir como diferentes combinações de produtos são embalados em conjunto # TODO~~

~~- Atribuir produtos a determinadas caixas (produtos múltiplos podem ser atribuídos à mesma caixa) # TODO~~

## Característica técnica

Atualmente diversos módulos de terceiros relativo a métodos de entrega sempre soma o peso e dimensões dos produtos gerando falha na requisição a transportadora devido não terem um sistema que separa os produtos em sua devida embalagem distribuindo seu peso.

O nosso módulo foi desenvolvido visando total transparência dos processos executados, para efeito de análise visualize os processos armazenado em log.

A extensão permite você definir as dimensões de seus produtos, as dimensões de suas embalagens e regras de como empacotar diferentes combinações de produtos em conjunto.

A extensão escolhe qual embalagem será utilizado para embalar os produtos para o pedido.

A extensão pode distribuir os produtos em diversas embalagens até o peso máximo suportado para a embalagem.

Como será cadastrado a embalagem com as dimensões e peso suportado pelas transportadoras não deve ocorrer falha relativa as dimensões ou peso.

A primeira coisa a se levar em consideração no uso do módulo é o [Gerenciamento de Caixa/Embalagem][github-boxpacker], como já vem alguns registros pré inseridos certifique se de atualizar os registros conforme sua necessidade.

Certifique se ter cadastrado as devidas dimensões para os produtos.

Para cada pacote é feito um acesso ao WebService onde é passado os devidos parâmetros

O módulo possui armazenamento de cache

Na finalização do pedido é armazenado no histórico do pedido um comentário contendo um identificador único que poderá ser usado para consulta no arquivo de log a discriminação dos pacotes seus itens e a visualização de cada pacote com seus itens em 3D

Sempre confira as informações de frete antes de processar cada pedido, caso algo esteja inconsistente será necessário cancelar o pedido até a correção da ocorrência

Para o rastreamento do pacote é feito acesso ao WebService onde é passado os devidos parâmetros e exibido o devido retorno

O módulo possui notificação automática do rastreamento sendo enviado e-mail sobre a mudança de status das suas encomendas ou pacotes do site do correios

Para usar esse recurso, configure o Magento para usar a [CRON][magento-cron] / [CRON][mozg-cron]

## Instalação - Atualização - Desinstalação

Este módulo destina-se a ser instalado usando o [Composer][getcomposer]

Antes de executar os processos, [clique aqui][requirements] e leia os pré-requisitos e sugestões

--

### Para instalar o módulo execute o comando a seguir no terminal do seu servidor

	composer require mozgbrasil/magento2-correios-php56 && php bin/magento setup:upgrade

Você pode verificar se o módulo está instalado, indo ao backend em:

	STORES -> Configuration -> ADVANCED/Advanced -> Disable Modules Output

--

### Para atualizar o módulo execute o comando a seguir no terminal do seu servidor

	composer update && php bin/magento setup:upgrade

--

### Para [desinstalar][uninstall-mods] o módulo execute o comando a seguir no terminal do seu servidor

	bin/magento module:uninstall --remove-data --backup-code --backup-media --backup-db Mozg_Correios

~~composer remove mozgbrasil/magento2-correios-php56 && composer clear-cache && composer update && php bin/magento setup:upgrade~~

## Como configurar o método de entrega

Antes de configurar o módulo você deve cadastrar o CEP de origem, indo ao backend em:

	STORES -> Configuration -> Sales/Shipping Settings -> Origin

Para configurar o método de entrega, acesse no backend em:

	STORES -> Configuration -> Sales/Shipping Methods -> Correios (powered by MOZG)

Você terá os campos a seguir

### • **Ativar**

Para "ativar" ou "desativar" o uso do método

### • **Ordem de exibição**

É a ordem apresentada em métodos de entrega no passo de fechamento de pedido

### • **Título**

Nome do método que deve ser exibido

### • **Serviços**

Selecione os serviços desejado, para selecionar mais de um, segure a tecla "Ctrl" e clique nos serviços

### • **Serviço Para Entrega Gratuita**

Quando houver um desconto de frete grátis, esse serviço terá o valor zero

### • **Calcular taxa de manuseio**

Podendo ser fixo ou percentual

### • **Taxa de Manuseio**

Será adicionado o valor ao frete

### • **Mostrar método se não aplicável**

Quando configurado como "Não", caso seja retornado algum serviço com erro, não será exibido o método de entrega

### • **Debug**

Deve ser armazenado os processos do módulo em var/log/

O arquivo 

DATE_mozg.log

se trata de log do módulo sendo um log mais detalhado contendo todos os processos inclusive das execuções realizadas pelas bibliotecas externas do módulo

O arquivo

shipping_METHOD.log

se trata de log nativo do magento relativo ao método de entrega

### • **Enviar para países aplicáveis**

Você pode definir se o método deve funcionar para "Todos os Países aceito" ou "Especificar Países "

### • **Enviar para países específicos**

Você deve selecionar os países que o método deve ser funcional

### • **Código administrativo junto à ECT**

Se você possui contrato com os Correios, preencha nesse campo o número do contrato

*Lojistas com contrato possuem valor diferenciado de postagem junto aos Correios*

### • **Senha Administrativa dos Correios (Serviços Com Contrato)**

Senha do seu contrato, por padrão são os 8 primeiros dígitos do CNPJ

### • **Utilizar Serviço de Mão Própria**

É o [serviço][mao-propria-mp] adicional pelo qual o remetente recebe a garantia de que o objeto, por ele postado sob Registro, será entregue somente ao próprio destinatário, através da confirmação de sua identidade

### • **Utilizar Serviço de Aviso de Recebimento**

É o [serviço][aviso-de-recebimento-ar] adicional que, por meio do preenchimento de formulário próprio, físico ou digital, permite comprovar, junto ao remetente, a entrega do objeto.

### • **Utilizar Serviço de Valor Declarado**

É o [serviço][valor-declarado] adicional que garante o valor real do objeto postado sob registro em caso eventual de avaria ou extravio.

### • **Exibir Prazo de Entrega**

Se será ou não mostrado o prazo de entrega para seu cliente

### • **Mensagem que Exibe o Prazo de Entrega**

Se será ou não mostrado o prazo de entrega para seu cliente

### • **Adicionar (dias) ao prazo de entrega**

Quantidade de dias que será adicionado ao prazo

### • **Mostrar serviço com retorno de erro**

Quando configurado como "Não", caso seja retornado algum serviço com erro, o mesmo não deve ser exibido no método de entrega

### • **Ativar rastreamento automático via CRON**

Quando alterado o registro para Não o processo não deve ser executado pela CRON em execução do Magento

## Quais os recursos do módulo

- [✓] Cálculo do frete
- [✓] Rastreamento
- [✓] Notificação automática do rastreamento

## Perguntas mais frequentes "FAQ"

### Como conferir os valores dos fretes junto a transportada

Você pode visualizar no log os parâmetros enviado a transportada

Quando finalizado o pedido é armazenado no historico as dimensões da caixa que foi usada para o obter o frete

### Como é feito o cálculo de preços

[Clique aqui][encomendas-prazo] para calcular o preço da encomenda o sistema utiliza a distância origem/destino(CEP), o peso e as dimensões do objeto, aplicando a seguinte fórmula relativa a peso cúbico:

	(Comprimento x Altura x Largura)/6000cm³

O preço adotado pelo sistema será o maior entre o peso cúbico e peso real.

### Como aplicar o Frete Grátis

Na configuração do módulo para o método de entrega é possível definir o "Serviço Para Entrega Gratuita" recurso que deve ser aplicado quando definido a ação de "Frete Grátis" nas "Regras da Promoção"

No Backend do Magento, acesse o menu: Promoções -> Regras de Promoção -> Criar regra -> Crie uma regra e defina na aba "Ações" o uso do Frete Grátis

Dessa forma na exibição do cálculo do frete será exibido para o serviço escolhido o valor zerado

Esse recurso se trata de regra nativa do Magento caso tenha algum problema sugiro desativar todas as regras de promoção e ativar uma de cada vez até encontrar o motivo da ocorrência

### Método retornando: "Peso excedido"
### Método retornando: "Dimensões dos produtos fora do permitido"

No link a seguir vemos os [limites de dimensões e de peso][limites-de-dimensoes-e-de-peso]

### Dados de contato - Correios

Para entrar em contato com o [Correios][contact-correios]

## Manual

http://www.correios.com.br/para-voce/correios-de-a-a-z/pdf/calculador-remoto-de-precos-e-prazos/manual-de-implementacao-do-calculo-remoto-de-precos-e-prazos

http://blog.correios.com.br/comercioeletronico/wp-content/uploads/2011/10/Guia-Tecnico-Rastreamento-XML-Cliente-Vers%C3%A3o-e-commerce-v-1-5.pdf

http://blog.correios.com.br/comercioeletronico/

http://blog.correios.com.br/comercioeletronico/?p=404

http://blog.correios.com.br/comercioeletronico/?p=155

http://www.correios.com.br/encomendas/prazo/Formato.cfm

http://www.correios.com.br/produtosaz/produto.cfm?id=8560360B-5056-9163-895DA62922306ECA

http://www.correios.com.br/para-sua-empresa/encomendas/sigep-web

http://www.corporativo.correios.com.br/encomendas/sigepweb/doc/Manual_de_Implementacao_do_Web_Service_SIGEPWEB_Logistica_Reversa.pdf

http://www2.correios.com.br/hotsites/ecommerce/

## Contribuintes

Equipe Mozg

## License

[Comercial License] (LICENSE.txt)

## Badges

[![Join the chat at https://gitter.im/mozgbrasil](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/mozgbrasil/)
[![Latest Stable Version](https://poser.pugx.org/mozgbrasil/magento2-correios-php56/v/stable)](https://packagist.org/packages/mozgbrasil/magento2-correios-php56)
[![Total Downloads](https://poser.pugx.org/mozgbrasil/magento2-correios-php56/downloads)](https://packagist.org/packages/mozgbrasil/magento2-correios-php56)
[![Latest Unstable Version](https://poser.pugx.org/mozgbrasil/magento2-correios-php56/v/unstable)](https://packagist.org/packages/mozgbrasil/magento2-correios-php56)
[![License](https://poser.pugx.org/mozgbrasil/magento2-correios-php56/license)](https://packagist.org/packages/mozgbrasil/magento2-correios-php56)
[![Monthly Downloads](https://poser.pugx.org/mozgbrasil/magento2-correios-php56/d/monthly)](https://packagist.org/packages/mozgbrasil/magento2-correios-php56)
[![Daily Downloads](https://poser.pugx.org/mozgbrasil/magento2-correios-php56/d/daily)](https://packagist.org/packages/mozgbrasil/magento2-correios-php56)

:cat2:
