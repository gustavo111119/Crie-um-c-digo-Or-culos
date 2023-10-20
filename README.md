# Crie-um-c-digo-Or-culos
Crie um código  Oráculos
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

// Contrato de exemplo com integração de oráculo
contract VendaDeAtivos {
    address public dono;
    uint256 public preco;
    bool public vendaAprovada;

    // Evento para notificar a mudança de status da venda
    event StatusVenda(string status);

    constructor(uint256 _preco) {
        dono = msg.sender;
        preco = _preco;
        vendaAprovada = false;
    }

    // Função para iniciar o processo de venda
    function iniciarVenda() public {
        require(msg.sender == dono, "Somente o dono pode iniciar a venda.");
        // Aqui é onde o oráculo de entrada pode validar os dados do mundo real
        // Por exemplo, verificar a disponibilidade do ativo e outros critérios
        vendaAprovada = true;
        emit StatusVenda("Venda iniciada. Aguardando confirmação do comprador.");
    }

    // Função para o comprador confirmar a compra
    function confirmarCompra() public {
        require(vendaAprovada, "A venda ainda não foi aprovada.");
        // Aqui é onde o oráculo de saída pode ser acionado para executar a transferência de ativos fora da cadeia
        // Por exemplo, transferir o título de propriedade do ativo para o comprador
        // Após a execução bem-sucedida, o contrato pode ser encerrado ou redefinido para futuras transações
        vendaAprovada = false;
        emit StatusVenda("Venda concluída com sucesso.");
    }
}
