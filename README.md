class Pessoa:
    def __init__(self, nome="", telefone="", email=""):
        self.nome = nome
        self.telefone = telefone
        self.email = email

    def exibir_informacoes(self):
        print(f"""
--- Pessoa ---
Nome: {self.nome}
Telefone: {self.telefone}
Email: {self.email}
""")


class Cliente(Pessoa):
    def __init__(self, nome="", telefone="", email="", id_unico=""):
        super().__init__(nome, telefone, email)
        self.id_unico = id_unico
        self.cadastrado = False

    def exibir_informacoes(self):
        print(f"""
--- Cliente ---
Nome: {self.nome}
Telefone: {self.telefone}
Email: {self.email}
ID único: {self.id_unico}
""")


class Quarto:
    def __init__(self, numero, tipo, preco_diaria):
        self.numero = numero
        self.tipo = tipo
        self.preco_diaria = preco_diaria
        self.disponivel = True

    def __str__(self):
        status = "Disponível" if self.disponivel else "Ocupado"
        return f"Quarto {self.numero} ({self.tipo}) - R$ {self.preco_diaria:.2f} - {status}"


class Reserva:
    def __init__(self, cliente, quarto, checkin, checkout):
        self.cliente = cliente
        self.quarto = quarto
        self.checkin = checkin
        self.checkout = checkout
        self.status = "Ativa"

    def __str__(self):
        return (f"{self.cliente.nome} - Quarto {self.quarto.numero} | "
                f"Check-in: {self.checkin} | Check-out: {self.checkout} | Status: {self.status}")


class GerenciadorDeReservas:

    def __init__(self):
        self.clientes = []
        self.quartos = []
        self.reservas = []

    def encontrar_cliente(self, id_unico):
        for cliente in self.clientes:
            if cliente.id_unico == id_unico:
                return cliente
        return None

    def encontrar_quarto(self, numero):
        for quarto in self.quartos:
            if quarto.numero == numero:
                return quarto
        return None

    def verificar_disponiveis(self):
        return [q for q in self.quartos if q.disponivel]

    def cadastrar_quarto(self):
        print("\n=== Cadastrar Quarto ===")
        numero = int(input("Número do quarto: "))
        tipo = input("Tipo (Simples/Luxo/etc): ")
        preco = float(input("Preço da diária: R$ "))

        quarto = Quarto(numero, tipo, preco)
        self.quartos.append(quarto)

        print("Quarto cadastrado com sucesso!")

    def criar_reserva(self):
        print("\n=== Criar Reserva ===")

        id_unico = input("ID do cliente: ")
        cliente = self.encontrar_cliente(id_unico)

        if not cliente:
            print("Cliente não encontrado. Criando novo cadastro...")
            nome = input("Nome: ")
            telefone = input("Telefone: ")
            email = input("Email: ")
            cliente = Cliente(nome, telefone, email, id_unico)
            self.clientes.append(cliente)

        quartos_disponiveis = self.verificar_disponiveis()

        if not quartos_disponiveis:
            print("Nenhum quarto disponível no momento.")
            return

        print("\nQuartos disponíveis:")
        for quarto in quartos_disponiveis:
            print(f"- {quarto}")

        num_quarto = int(input("\nEscolha o número do quarto: "))
        quarto = self.encontrar_quarto(num_quarto)

        if not quarto or not quarto.disponivel:
            print("Quarto inválido!")
            return

        checkin = input("Data de check-in: ")
        checkout = input("Data de check-out: ")

        reserva = Reserva(cliente, quarto, checkin, checkout)
        self.reservas.append(reserva)

        quarto.disponivel = False

        print("Reserva criada com sucesso!")

    def listar_reservas(self):
        print("\n=== LISTA DE RESERVAS ===")
        if not self.reservas:
            print("Nenhuma reserva encontrada.")
            return

        for i, reserva in enumerate(self.reservas, start=1):
            print(f"\n--- Reserva {i} ---")
            print(reserva)

    def obter_reserva(self, numero):
        if 1 <= numero <= len(self.reservas):
            return self.reservas[numero - 1]
        return None

    def excluir_reserva(self):
        self.listar_reservas()
        numero = int(input("Digite o número da reserva que deseja excluir: "))

        reserva = self.obter_reserva(numero)
        if not reserva:
            print("Número inválido!")
            return

        self.reservas.remove(reserva)
        reserva.quarto.disponivel = True

        print("Reserva excluída com sucesso!")

    def modificar_reserva(self):
        print("\n=== MODIFICAR RESERVA ===")
        self.listar_reservas()

        numero = int(input("Digite o número da reserva que deseja modificar: "))
        reserva = self.obter_reserva(numero)

        if not reserva:
            print("Número inválido!")
            return

        print("""
O que deseja modificar?
1 - Nome do cliente
2 - Telefone
3 - Email
4 - Datas (check-in / check-out)
""")

        opcao = input("Digite a opção: ")

        if opcao == "1":
            reserva.cliente.nome = input("Novo nome: ")
        elif opcao == "2":
            reserva.cliente.telefone = input("Novo telefone: ")
        elif opcao == "3":
            reserva.cliente.email = input("Novo email: ")
        elif opcao == "4":
            reserva.checkin = input("Novo check-in: ")
            reserva.checkout = input("Novo check-out: ")
        else:
            print("Opção inválida!")
            return

        print("Reserva modificada com sucesso!")

def menu():
    ger = GerenciadorDeReservas()

    while True:
        print("""
======= SISTEMA DE RESERVAS =======
1 - Cadastrar quarto
2 - Criar reserva
3 - Listar reservas
4 - Modificar reserva
5 - Excluir reserva
6 - Sair
""")

        opcao = input("Escolha uma opção: ")

        if opcao == "1":
            ger.cadastrar_quarto()
        elif opcao == "2":
            ger.criar_reserva()
        elif opcao == "3":
            ger.listar_reservas()
        elif opcao == "4":
            ger.modificar_reserva()
        elif opcao == "5":
            ger.excluir_reserva()
        elif opcao == "6":
            print("Encerrando o sistema...")
            break
        else:
            print("Opção inválida! Tente novamente.")


menu()
