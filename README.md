Oficina Mecânica

Projeto de Estrutura de Dados, Fatec Rio Claro. Aluno: Artur Nagasima Furlan.

Sistema em Python que simula o atendimento de uma oficina mecânica, da chegada do veículo ao pagamento. Lista, fila, pilha e árvore foram implementadas com classes e nós próprios, sem list, dict ou deque para guardar os dados.

Para executar, abra oficina_mecanica.ipynb no Google Colab e rode as células em ordem. A opção 16 do menu faz uma simulação completa.

Combinações de estruturas
1. Fila + Fila: atendimento com prioridade para guincho

Classes e métodos

Atendimento (atributos fila_guincho e fila_normal)
registrar_chegada, _fila_da_vez, proximo, chamar_proximo, liberar_box

A fila garante o atendimento por ordem de chegada. Com duas filas, o guincho passa na frente e a ordem de chegada continua valendo dentro de cada uma. Com uma fila só, seria preciso inserir o guincho no meio ou reordenar a fila, o que custa O(n).

Lista de produtos + Fila de lotes: estoque

Classes e métodos

Estoque (Lista de Produto), Produto (Fila de Lote)
comprar, buscar_produto, descartar_vencidos, disponivel, _consumir, baixar, ajustar_quantidade, verificar_alerta, Produto.quantidade_total

Justificativa Consumir o lote mais antigo primeiro é o comportamento de uma fila. A lista só localiza o produto. Com uma lista única de lotes de todos os produtos, seria preciso percorrer tudo para achar o lote mais antigo de um produto e para somar o total dele (usado no alerta de mínimo).

Lista de clientes + Lista de veículos: cadastro

Classes e métodos

CadastroClientes (Lista de Cliente), Cliente (Lista de Veiculo)
buscar_cliente, buscar_por_placa, cadastrar_cliente, cadastrar_veiculo, remover_veiculo, remover_cliente

O veículo pertence ao cliente, e um cliente pode ter vários. A lista dentro de cada cliente representa isso direto, sem repetir os dados do dono, e os veículos saem junto quando o cliente é removido. Com uma lista única de veículos, os dados do dono se repetiriam e remover um cliente exigiria varrer a lista toda.

Simulação

A opção 16 do menu faz o seguinte: chegam dois veículos (um normal e um por guincho), o guincho é chamado primeiro e a OS é aberta, o componente com defeito é marcado na árvore, peças e serviços entram na OS (um lote vencido de óleo é descartado como perda), o fechamento é bloqueado até a remontagem e, depois dela, a OS é fechada e paga. No fim o programa confere o valor de peças recebido com o consumido.
