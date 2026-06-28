# Descricao textual do diagrama de classes - E-commerce

Este documento descreve o modelo de classes do e-commerce que deve ser usado por uma IA para gerar o sistema. O sistema e uma loja virtual basica com catalogo de produtos, carrinho, checkout com pagamento simulado, pedidos e administracao de catalogo/pedidos.

## Atores

- Visitante: usuario nao autenticado que pode navegar pelo catalogo e visualizar produtos.
- Cliente: usuario autenticado com papel `CLIENTE`, pode comprar e acompanhar seus pedidos.
- Administrador: usuario autenticado com papel `ADMIN`, pode gerenciar produtos, categorias e pedidos.

## Modelo de dominio

- `Usuario`: representa clientes e administradores. O campo `email` deve ser unico. A senha deve ser armazenada somente como hash em `senhaHash`, nunca em texto puro. O campo `papel` define se o usuario e `CLIENTE` ou `ADMIN`.
- `Categoria`: agrupa produtos por categoria. Um produto pertence a exatamente uma categoria, e uma categoria pode classificar zero ou mais produtos.
- `Produto`: item vendido no catalogo. Deve ter preco maior ou igual a zero, estoque maior ou igual a zero e flag `ativo`. Produtos inativos nao aparecem no catalogo, mas devem continuar preservados em pedidos antigos.
- `Carrinho`: carrinho ativo de um usuario. Um usuario possui exatamente um carrinho ativo. O carrinho contem zero ou mais itens.
- `ItemCarrinho`: representa um produto dentro do carrinho, com quantidade e preco unitario. Nao deve permitir quantidade maior que o estoque disponivel.
- `Pedido`: compra finalizada por um usuario. Um usuario pode ter zero ou mais pedidos. Todo pedido possui um ou mais itens, um endereco de entrega, valor total, status e data de criacao.
- `ItemPedido`: copia historica e imutavel do produto no momento da compra. Deve armazenar `produtoId`, `nomeProduto`, `quantidade`, `precoUnitario` e `subtotal`. Alteracoes futuras no produto nao devem alterar pedidos antigos.
- `Endereco`: endereco de entrega informado no checkout, composto por cep, logradouro, numero, complemento, cidade e estado.

## Casos de uso esperados

- `AutenticacaoService`: cadastro, login, logout e hash de senha.
- `CatalogoService`: listagem de produtos ativos, busca por nome, filtro por categoria e detalhe do produto.
- `CarrinhoService`: obtencao do carrinho, adicao de item, alteracao de quantidade e remocao de item.
- `CheckoutService`: finalizacao da compra, simulacao de pagamento e confirmacao do pedido.
- `PedidoService`: listagem e detalhe dos pedidos do cliente, visualizacao de todos os pedidos pelo administrador e atualizacao de status.
- `AdministracaoService`: cadastro, edicao e desativacao de produtos; cadastro e edicao de categorias.

## Regras de negocio

- O sistema deve validar unicidade de email no cadastro.
- A senha deve ser armazenada com hash seguro.
- Apenas produtos ativos aparecem no catalogo.
- Produto com estoque zero deve ser indicado como indisponivel.
- Nao e permitido adicionar ao carrinho quantidade maior que o estoque disponivel.
- Nao e permitido finalizar compra com carrinho vazio.
- O valor total do carrinho e a soma dos subtotais dos itens.
- O valor total do pedido e a soma dos subtotais dos itens do pedido.
- O preco do item do pedido deve ser congelado no momento da compra.
- A baixa de estoque ocorre apenas quando o pagamento simulado for aprovado.
- Se o pagamento for recusado, o pedido deve ser cancelado.
- Ao cancelar pedido ainda nao enviado, o estoque deve ser estornado.
- Apenas o proprio cliente ou um administrador pode visualizar detalhes de um pedido.

## Maquina de estados do pedido

- Estado inicial: `AGUARDANDO_PAGAMENTO`.
- Estados finais: `ENTREGUE` e `CANCELADO`.
- Transicoes permitidas:
  - `AGUARDANDO_PAGAMENTO -> PAGO`, quando o pagamento for aprovado.
  - `AGUARDANDO_PAGAMENTO -> CANCELADO`, quando o pagamento for recusado ou o pedido for cancelado.
  - `PAGO -> ENVIADO`, quando o pedido for separado/enviado.
  - `PAGO -> CANCELADO`, quando o pedido for cancelado antes do envio.
  - `ENVIADO -> ENTREGUE`, quando houver confirmacao de recebimento.

## Fora de escopo

- Gateway de pagamento real.
- Integracao com transportadora ou calculo de frete por CEP.
- Avaliacoes, comentarios e lista de desejos.
- Cupons, promocoes e marketplace.
- Notificacoes por email ou SMS.
