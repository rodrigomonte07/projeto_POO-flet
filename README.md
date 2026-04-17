🏨 Sistema de Reservas em Python
Este projeto é um sistema simples de gerenciamento de reservas de quartos desenvolvido em Python. Ele permite cadastrar quartos, criar reservas, listar, modificar e excluir reservas de clientes. É uma aplicação de console, ideal para fins de estudo e prática de Programação Orientada a Objetos (POO).

🚀 Funcionalidades
Cadastro de quartos com número, tipo e preço da diária.

Cadastro automático de clientes ao criar uma reserva.

Criação de reservas com check-in e check-out.

Listagem de reservas existentes.

Modificação de reservas (dados do cliente ou datas).

Exclusão de reservas, liberando o quarto novamente.

Controle de disponibilidade dos quartos.

🛠️ Estrutura do Código
O sistema é composto pelas seguintes classes:

Pessoa → Classe base para representar pessoas.

Cliente (Pessoa) → Herda de Pessoa e adiciona ID único e status de cadastro.

Quarto → Representa os quartos disponíveis para reserva.

Reserva → Associa cliente, quarto e período da estadia.

GerenciadorDeReservas → Responsável por gerenciar clientes, quartos e reservas.

menu() → Interface de console para interação com o usuário.

📂 Como Executar
Clone este repositório:

bash
git clone https://github.com/seu-usuario/sistema-reservas.git
Acesse a pasta do projeto:

bash
cd sistema-reservas
Execute o programa:

bash
python reservas.py
📖 Exemplo de Uso
Ao rodar o programa, você verá o menu principal:

Código
======= SISTEMA DE RESERVAS =======
1 - Cadastrar quarto
2 - Criar reserva
3 - Listar reservas
4 - Modificar reserva
5 - Excluir reserva
6 - Sair
Você pode interagir escolhendo as opções e preenchendo os dados solicitados.

🎯 Objetivo
Este projeto foi criado com fins educacionais, para praticar conceitos de:

Programação Orientada a Objetos (POO)

Herança e polimorfismo

Manipulação de listas e objetos em Python

Estruturação de sistemas simples de console

📌 Melhorias Futuras
Persistência dos dados em arquivo (JSON/SQLite).

Validação de datas e informações do cliente.

Interface gráfica (Tkinter ou PyQt).

Relatórios de ocupação e faturamento.

👨‍💻 Autor
Projeto 
