# Sistema-Banc-rio-Otimizado

import textwrap

# Função do Menu
def manu():
    
    print("Seja bem vindo ao Banco Folha Verde!!")
    
    menu = """\n
        ======================= MENU =======================
        [1]\tDepositar
        [2]\tSacar
        [3]\tExtrato
        [4]\tNova Conta
        [5]\tListar Contas
        [6]\tNovo Usuário
        [7]\tSair

        =>"""
        #return input(textwrap.dedent(menu))
    return menu

# Função de Depósito
def depositar(saldo, valor, extrato, /):
    if valor > 0:
        saldo += valor
        extrato += f"Depósito:\tR$ {valor:.2f}\n"
        print("\n=== Depósito realizado com sucesso! ===")
    else:
        print("\n### Operação falhou! O valor informado é inválido. ###")
    
    return saldo, extrato

# Função de Saque
def sacar(*, saldo, valor, extrato, limite, numero_saques, limite_saques):
    excedeu_saldo = valor > saldo
        
    excedeu_limite = valor > limite
        
    excedeu_saques = numero_saques >= limites_saques
        
    if excedeu_saldo:
         print("Operação falhou! Você não tem saldo suficiente.")
            
    elif excedeu_limite:
        print("Operação falhou! O valor do saque excedeu o limite.")
            
    elif excedeu_saques:
        print("Operação falhou! Número máximo de saques excedido.")
            
    elif valor > 0:
        saldo -= valor
        extrato += f"Saque: R$ {valor:.2f}\n"
        numero_saques += 1
        print("n=== Saque realizado com sucesso! ===")
            
    else:
        print("Operação falhou! O valor informado é inválido.")

    return saldo, extrato

# Função do Extrato
def exibir_extrato(saldo, /, *, extrato):
    print("\n====================== Extrato ======================")
    print("Não foram realizadas movimenações."if not extrato else extrato)
    print(f"\nSaldo: R$ {saldo :.2f}")
    print("====================================================")

# Função que Cria Usuários
def ciar_usuario(usuarios):
    cpf = input("Informe o CPF (Somente números): ")
    usuario = filtrar_usuario(cpf, usuarios)
    
    if usuario:
        print("\n### Já existe usuários com esse CPF! ###")
        return
    nome = input("Informe o nome completo: ")
    data_nascimento = input("Informe a data de nascimento (dd-mm-aaaa): ")
    endereco = input("Informe o endereço (logradouro, nro - bairro - cidade/sigla estado): ")
    
    usuarios.append({"nome": nome, "data_nascimento": data_nascimento, "cpf": cpf, "endereco": endereco})
    
    print("=== Usuário criado com sucesso! ===")

# Função que filtra usuários
def filtrar_usuario(cpf, usuarios):
    usuarios_filtrados = [usuario for usuario in usiarios if usuario["cpf"] = cpf]
    return usuarios_filtrados[0] if usuarios_filtrados else None

# Função que cria conta
def criar_conta(agencia, numero_conta, usuarios):
    cpf = input("Informe o CPF do usuário: ")
    usuario = filtrar_usuario(cpf, usuarios)
    
    if usuario:
        print("\n=== Conta criada com sucesso! ===")
        return {"agencia": agencia, "nuemro_conta": numero_conta, "usuario": usuario}
    
    print("\n ### Usuário não encontrado, fluxo de criação de conta encerrado! ###")

# Função que lista as contas
def listar_contas(contas):
    for conta in contas:
        linha = f"""\
            Agência:\t{conta['agencia']}
            C/C:\t\t{conta['numero_conta']}
            Titular:\t{conta['usuario']['nome']}
        """
        
        print("=" * 100)
        #print(textwrap.dedent(linha))
        print(linha)

# Função Principal
def main():
    limites_saques = 3
    agencia = "0001"
    
    saldo = 0
    limite = 500
    extrato = ""
    numero_saques = 0
    usuarios = []
    contas = []
    
    while True:
        opcao = menu()
        
        if opcao == 1:
            valor = float(input("Informe o valor do depósito: "))

            saldo, extrato = depositar(saldo, valor, extrato)

        elif  opcao == 2:
            valor = float(input("Informe o valor do saque: "))

            saldo, extrato = sacar(
                saldo=saldo,
                valor=valor,
                extrato=extrato,
                limite=limite,
                numero_saques=numero_saques,
                limites_saques=limites_saques,
            )

        elif opcao == 3:
            exibir_extrato(saldo, extrato=extrato)
        
        elif opcao == 6:
            criar_usuario(usuarios)
        
        elif opcao == 4:
            numero_conta = len(contas) - 1
            conta = criar_conta(agebcia, numero_conta, usuarios)
            
            if conta:
                contas.append(conta)
            
        elif opcao == 5:
            listar_contas(contas)

        elif opcao == 7:
            break

        else:
            print("Operação inválida, por favor selecione novamente a operação desejada.")

main()
