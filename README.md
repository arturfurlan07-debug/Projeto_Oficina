Oficina Mecânica

Projeto da disciplina de Estrutura de Dados, Fatec Rio Claro. Aluno: Artur Nagasima Furlan

Sistema em Python que simula o atendimento de uma oficina mecânica, desde a chegada do veículo até o pagamento. As estruturas (lista, fila, pilha e árvore) foram implementadas por mim, com nós próprios, sem usar list, dict ou deque para guardar os dados do problema.

Como executar

Abra o arquivo oficina_mecanica.ipynb no Google Colab e execute as células em ordem. A última célula abre um menu no terminal. A opção 16 roda uma simulação completa de um atendimento.

Organização do código

A primeira célula tem só as estruturas genéricas (No, Lista, Fila e Pilha). As outras células têm as regras da oficina, separadas por assunto:

Clientes e veículos: Cliente, Veiculo, CadastroClientes
Atendimento: Chegada, Box, Atendimento
Diagnóstico: NoComponente
Estoque: Lote, Produto, Perda, Estoque
Ordem de serviço: ItemPeca, Servico, OrdemServico, GerenciadorOS
Pagamento e consumo: Pagamento, RegistroPagamentos, Consumo, RegistroConsumo
Oficina: junta tudo e executa o fluxo completo
Estruturas
Lista: encadeada simples. Adicionar, buscar e remover são O(n).
Fila: guarda ponteiros para o início e o fim. Enfileirar e desenfileirar são O(1).
Pilha: empilhar e desempilhar são O(1). É usada na desmontagem do veículo, para remontar na ordem inversa. A OS só pode ser fechada com a pilha vazia.
Árvore de componentes: cada NoComponente guarda seus filhos em uma Lista, então pode ter qualquer quantidade. Não é binária nem de busca. A exibição usa percurso em profundidade (pré-ordem) e é O(n).
Combinações de estruturas
Fila + Fila: atendimento com prioridade para guincho

Classe Atendimento, métodos registrar_chegada, _fila_da_vez, proximo, chamar_proximo e liberar_box.

Existem duas filas, fila_guincho e fila_normal. O próximo veículo sai da fila de guincho e, se ela estiver vazia, sai da normal. Em cada fila vale a ordem de chegada. enfileirar e desenfileirar continuam O(1) e a regra de prioridade fica concentrada no _fila_da_vez.

Com uma fila só, o guincho teria que ser inserido no meio da fila ou a fila teria que ser reordenada, o que custa O(n) e complica manter a ordem de chegada entre os guinchos.

Lista de produtos + Fila de lotes: estoque

Classes Estoque, Produto e Lote, métodos comprar, descartar_vencidos, disponivel, _consumir, baixar, ajustar_quantidade e Produto.quantidade_total.

O Estoque tem uma Lista de Produto e cada produto tem uma Fila de Lote, com o mais antigo na frente. A baixa percorre a lista até achar o produto e consome o lote da frente da fila. Lotes vencidos saem da fila e viram Perda. A regra "consumir o lote mais antigo primeiro" é o comportamento natural de uma fila, e a lista só serve para localizar o produto.

Com uma lista única de lotes de todos os produtos, seria preciso percorrer tudo para achar o lote mais antigo de um produto e também para somar o total dele, que é necessário para o alerta de estoque mínimo.

Lista de clientes + Lista de veículos: cadastro

Classes CadastroClientes, Cliente e Veiculo, métodos buscar_por_placa, cadastrar_veiculo, remover_veiculo e remover_cliente.

O cadastro tem uma Lista de Cliente e cada cliente tem a sua própria Lista de Veiculo, sem limite de veículos. Para achar um veículo pela placa, percorre-se a lista de clientes e, dentro de cada um, a lista de veículos, o que dá O(c · v). Como o veículo pertence ao cliente, ao remover o cliente os veículos saem junto.

Com uma lista única de veículos, os dados do dono se repetiriam em cada veículo e remover um cliente exigiria varrer a lista inteira para apagar os veículos dele.

Simulação

A opção 16 do menu faz o seguinte: chegam dois veículos (um normal e um por guincho), o guincho é chamado primeiro e a OS é aberta, o componente com defeito é marcado na árvore, peças e serviços entram na OS (um lote vencido de óleo é descartado como perda), o fechamento é bloqueado até a remontagem e, depois dela, a OS é fechada e paga. No fim o programa confere o valor de peças recebido com o consumido.
