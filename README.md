# Projeto-2026-2-Programa-o-A-
Sistema Bancário em Console


# ===============================#
#           Back End
# ===============================#

# Banco de dados dos clientes
cadastros = {}


def inicio_app(nome):
    print(f'''
Bem-vindo, {nome}!
Por favor, para prosseguir, escolha uma das opções abaixo:
''')

    print('-' * 39)

    print('''
    Efetuar login [1]
    Abrir nova Conta [2]
    Sair [3]
    Consultar saldo [4]
    Depositar [5]
    Sacar [6]
    ''')

    print('-' * 39)


# ===============================#
#        ABRIR CONTA
# ===============================#

def abrir_conta():

    print('\n========== ABERTURA DE CONTA ==========')

    nome = input('Informe seu nome: ')

    cpf = input(
        f'{nome}, informe seu CPF: [somente números] '
    )

    # Validação do CPF
    while len(cpf) != 11 or not cpf.isdigit():

        print('\nCPF inválido! Digite novamente.')

        cpf = input('CPF: ')

    # Verifica se o CPF já existe
    if cpf in cadastros:

        print('\nCPF já cadastrado!')

        resposta = input(
            'Deseja acessar sua conta? [1] Sim [2] Não: '
        )

        if resposta == '1':
            conta_login(cpf)
        else:
            print('\nOperação cancelada.')

    else:

        # Cria o cliente
        cadastros[cpf] = {
            'nome': nome,
            'saldo': 0.0
        }

        print('\nConta criada com sucesso!')

        conta_login(cpf)


# ===============================#
#             LOGIN
# ===============================#

def login():

    print('\n========== LOGIN ==========')

    cpf = input('Informe seu CPF: ')

    while len(cpf) != 11 or not cpf.isdigit():

        print('\nCPF inválido!')

        cpf = input('Informe seu CPF: ')

    if cpf in cadastros:

        print('\nLogin realizado com sucesso!')

        conta_login(cpf)

    else:

        print('\nCPF não encontrado.')

        resposta = input(
            'Deseja abrir uma nova conta? [1] Sim [2] Não: '
        )

        if resposta == '1':
            abrir_conta()


# ===============================#
#        DADOS DA CONTA
# ===============================#

def conta_login(cpf):

    cliente = cadastros[cpf]

    print('=' * 40)

    print(f'  Usuário: {cliente["nome"]}')
    print(f'  CPF: {cpf}')
    print(f'  Saldo: R$ {cliente["saldo"]:.2f}')

    print('=' * 40)


# ===============================#
#       CONSULTAR SALDO
# ===============================#

def consultar_saldo(cpf):

    cliente = cadastros[cpf]

    print('=' * 40)

    print(f'  Usuário: {cliente["nome"]}')
    print(f'  CPF: {cpf}')
    print(f'  Saldo atual: R$ {cliente["saldo"]:.2f}')

    print('=' * 40)


# ===============================#
#           DEPOSITAR
# ===============================#

def depositar(cpf):

    cliente = cadastros[cpf]

    try:
        depos = float(
            input('Quanto você deseja depositar? R$ ')
        )

        if depos > 0:

            cliente['saldo'] += depos

            print(
                f'\nDepósito de R$ {depos:.2f} realizado '
                f'com sucesso!'
            )

            print(
                f'Seu saldo atual é de: '
                f'R$ {cliente["saldo"]:.2f}'
            )

        else:

            print('\nDigite um valor maior que R$ 0.')

    except ValueError:

        print('\nDigite um valor numérico válido.')


# ===============================#
#              SACAR
# ===============================#

def sacar(cpf):

    cliente = cadastros[cpf]

    try:

        saque = float(
            input('Quanto você deseja sacar? R$ ')
        )

        while saque <= 0 or saque > cliente['saldo']:

            if saque <= 0:

                print(
                    '\nO valor do saque deve ser maior que R$ 0.'
                )

            elif saque > cliente['saldo']:

                print(
                    '\nSaldo insuficiente!'
                )

                print(
                    f'Seu saldo atual é: '
                    f'R$ {cliente["saldo"]:.2f}'
                )

            saque = float(
                input('Digite outro valor para sacar: R$ ')
            )

        cliente['saldo'] -= saque

        print(
            f'\nSaque de R$ {saque:.2f} realizado '
            f'com sucesso!'
        )

        print(
            f'Seu saldo atual é de: '
            f'R$ {cliente["saldo"]:.2f}'
        )

    except ValueError:

        print('\nDigite um valor numérico válido.')


# ===============================#
#          MENU DA CONTA
# ===============================#

def menu_conta(cpf):

    while True:

        cliente = cadastros[cpf]

        print('\n')
        print('=' * 40)
        print(f'Olá, {cliente["nome"]}!')
        print('=' * 40)

        print('''
[1] Consultar saldo
[2] Depositar
[3] Sacar
[4] Ver dados da conta
[5] Sair da conta
''')

        opcao = input('Digite a opção desejada: ')

        if opcao == '1':

            consultar_saldo(cpf)

        elif opcao == '2':

            depositar(cpf)

        elif opcao == '3':

            sacar(cpf)

        elif opcao == '4':

            conta_login(cpf)

        elif opcao == '5':

            print('\nLogout realizado com sucesso!')

            break

        else:

            print('\nOpção inválida!')


# ===============================#
#           MENU PRINCIPAL
# ===============================#

def menu_app():

    while True:

        print('\n$TESTBANK$')

        print('\nOlá, você está na TestBank!')

        print('-' * 40)

        print('''
[1] Efetuar login
[2] Abrir nova conta
[3] Sair
''')

        print('-' * 40)

        opcao = input('Digite a opção desejada: ')

        if opcao == '1':

            cpf = input('\nDigite seu CPF: ')

            if cpf in cadastros:

                menu_conta(cpf)

            else:

                print('\nCPF não encontrado.')

        elif opcao == '2':

            abrir_conta()

        elif opcao == '3':

            print('\nOperação encerrada!')

            break

        else:

            print('\nOpção inválida!')


# ===============================#
#            FRONT END
# ===============================#

menu_app()

print('\nSessão encerrada!')






































RENATA

#           Back End
# ===============================#


# Banco de dados dos clientes
cadastros = {}


# Contador de contas
contador_contas = 0




# ===============================#
#        ABRIR CONTA
# ===============================#


def abrir_conta():
    global contador_contas


    print('\n========== ABERTURA DE CONTA ==========')


    nome = input('Informe seu nome: ')
    cpf = input(f'{nome}, informe seu CPF: [somente números] ')


    # Validação do CPF
    while len(cpf) != 11 or not cpf.isdigit():
        print('\nCPF inválido! Digite novamente.')
        cpf = input('CPF: ')


    # Verifica se o CPF já existe
    if cpf in cadastros:
        print('\nCPF já cadastrado!')
        resposta = input('Deseja acessar sua conta? [1] Sim [2] Não: ')


        if resposta == '1':
            conta_login(cpf)
        else:
            print('\nOperação cancelada.')


    else:
        # Incrementa contador
        contador_contas += 1


        # Gera número da conta
        numero_conta = f'CONTA{contador_contas:02d}'


        # Cria o cliente
        cadastros[cpf] = {
            'nome': nome,
            'saldo': 0.0,
            'numero_conta': numero_conta
        }


        print(f'\nConta criada com sucesso!')
        print(f'Número da conta: {numero_conta}')


        conta_login(cpf)




# ===============================#
#        DADOS DA CONTA
# ===============================#


def conta_login(cpf):


    cliente = cadastros[cpf]


    print('=' * 40)
    print(f'  Usuário: {cliente["nome"]}')
    print(f'  CPF: {cpf}')
    print(f'  Número da Conta: {cliente["numero_conta"]}')
    print(f'  Saldo: R$ {cliente["saldo"]:.2f}')
    print('=' * 40)




# ===============================#
#       CONSULTAR SALDO
# ===============================#


def consultar_saldo(cpf):


    cliente = cadastros[cpf]


    print('=' * 40)
    print(f'  Usuário: {cliente["nome"]}')
    print(f'  CPF: {cpf}')
    print(f'  Número da Conta: {cliente["numero_conta"]}')
    print(f'  Saldo atual: R$ {cliente["saldo"]:.2f}')
    print('=' * 40)




# ===============================#
#           DEPOSITAR
# ===============================#


def depositar(cpf):


    cliente = cadastros[cpf]


    try:


        depos = float(input('Quanto você deseja depositar? R$ '))


        if depos > 0:


            cliente['saldo'] += depos


            print(f'\nDepósito de R$ {depos:.2f} realizado com sucesso!')
            print(f'Seu saldo atual é de: R$ {cliente["saldo"]:.2f}')


        else:


            print('\nDigite um valor maior que R$ 0.')


    except ValueError:


        print('\nDigite um valor numérico válido.')




# ===============================#
#              SACAR
# ===============================#


def sacar(cpf):


    cliente = cadastros[cpf]


    try:


        saque = float(input('Quanto você deseja sacar? R$ '))


        while saque <= 0 or saque > cliente['saldo']:


            if saque <= 0:


                print('\nO valor do saque deve ser maior que R$ 0.')


            elif saque > cliente['saldo']:
   			if  cliente ['saldo']==0:
       			print('saldo insuficiente')
       			return






                print('\nSaldo insuficiente!')
                print(f'Seu saldo atual é: R$ {cliente["saldo"]:.2f}')


            saque = float(input('Digite outro valor para sacar: R$ '))


        cliente['saldo'] -= saque


        print(f'\nSaque de R$ {saque:.2f} realizado com sucesso!')
        print(f'Seu saldo atual é de: R$ {cliente["saldo"]:.2f}')


    except ValueError:


        print('\nDigite um valor numérico válido.')




# ===============================#
#     PROCURAR POR NÚMERO DE CONTA
# ===============================#


def procurar_por_conta(numero_conta):


    print('\n========== CONSULTA POR NÚMERO DE CONTA ==========')


    for cpf, dados in cadastros.items():


        if dados['numero_conta'] == numero_conta:


            print('\nConta encontrada!')
            print('=' * 40)
            print(f'  Usuário: {dados["nome"]}')
            print(f'  CPF: {cpf}')
            print(f'  Número da Conta: {dados["numero_conta"]}')
            print(f'  Saldo: R$ {dados["saldo"]:.2f}')
            print('=' * 40)


            return


    print('\nConta não encontrada.')




# ===============================#
#     LISTAR TODAS AS CONTAS
# ===============================#


def listar_contas():


    print('\n========== LISTA DE CONTAS ==========')


    # Verifica se existem contas
    if len(cadastros) == 0:


        print('\nNenhuma conta cadastrada.')
        return


    # Mostra quantidade de contas
    print(f'\nTotal de contas cadastradas: {len(cadastros)}')


    # Percorre todos os clientes
    for cpf, dados in cadastros.items():


        print('=' * 40)
        print(f'  Usuário: {dados["nome"]}')
        print(f'  CPF: {cpf}')
        print(f'  Número da Conta: {dados["numero_conta"]}')
        print(f'  Saldo: R$ {dados["saldo"]:.2f}')
        print('=' * 40)




# ===============================#
#          MENU DA CONTA
# ===============================#


def menu_conta(cpf):


    while True:


        cliente = cadastros[cpf]


        print('\n')
        print('=' * 40)
        print(f'Olá, {cliente["nome"]}!')
        print('=' * 40)


        print('''
[1] Consultar saldo
[2] Depositar
[3] Sacar
[4] Ver dados da conta
[5] Sair da conta
''')


        opcao = input('Digite a opção desejada: ')


        if opcao == '1':


            consultar_saldo(cpf)


        elif opcao == '2':


            depositar(cpf)


        elif opcao == '3':


            sacar(cpf)


        elif opcao == '4':


            conta_login(cpf)


        elif opcao == '5':


            print('\nLogout realizado com sucesso!')
            break


        else:


            print('\nOpção inválida!')




# ===============================#
#           MENU PRINCIPAL
# ===============================#


def menu_app():


    while True:


        print('\n$TESTBANK$')
        print('\nOlá, você está na TestBank!')
        print('-' * 40)


        print('''
[1] Efetuar login
[2] Abrir nova conta
[3] Procurar conta por número
[4] Consultar todas as contas
[5] Sair
''')


        print('-' * 40)


        opcao = input('Digite a opção desejada: ')


        # =========================
        # OPÇÃO 1 - LOGIN
        # =========================


        if opcao == '1':


            cpf = input('\nDigite seu CPF: ')


            if cpf in cadastros:


                menu_conta(cpf)


            else:


                print('\nCPF não encontrado.')


        # =========================
        # OPÇÃO 2 - ABRIR CONTA
        # =========================


        elif opcao == '2':


            abrir_conta()


        # =========================
        # OPÇÃO 3 - PROCURAR CONTA
        # =========================


        elif opcao == '3':


            numero = input('\nDigite o número da conta (ex: CONTA01): ').upper()


            procurar_por_conta(numero)


        # =========================
        # OPÇÃO 4 - LISTAR CONTAS
        # =========================


        elif opcao == '4':


            listar_contas()


        # =========================
        # OPÇÃO 5 - SAIR
        # =========================


        elif opcao == '5':


            print('\nOperação encerrada!')
            break


        else:


            print('\nOpção inválida!')




# ===============================#
#            FRONT END
# ===============================#


menu_app()


print('\nSessão encerrada!')









































ATUALIZAÇÃO


#           Back End
# ===============================#




# Banco de dados dos clientes
cadastros = {}




# Contador de contas
contador_contas = 0








# ===============================#
#        ABRIR CONTA
# ===============================#




def abrir_conta():
   global contador_contas




   print('\n========== ABERTURA DE CONTA ==========')




   nome = input('Informe seu nome: ')
   cpf = input(f'{nome}, informe seu CPF: [somente números] ')




   # Validação do CPF
   while len(cpf) != 11 or not cpf.isdigit():
       print('\nCPF inválido! Digite novamente.')
       cpf = input('CPF: ')




   # Verifica se o CPF já existe
   if cpf in cadastros:
       print('\nCPF já cadastrado!')
       resposta = input('Deseja acessar sua conta? [1] Sim [2] Não: ')




       if resposta == '1':
           conta_login(cpf)
       else:
           print('\nOperação cancelada.')




   else:
       # Incrementa contador
       contador_contas += 1




       # Gera número da conta
       numero_conta = f'CONTA{contador_contas:02d}'




       # Cria o cliente
       cadastros[cpf] = {
           'nome': nome,
           'saldo': 0.0,
           'numero_conta': numero_conta
       }




       print(f'\nConta criada com sucesso!')
       print(f'Número da conta: {numero_conta}')




       conta_login(cpf)








# ===============================#
#        DADOS DA CONTA
# ===============================#




def conta_login(cpf):




   cliente = cadastros[cpf]




   print('=' * 40)
   print(f'  Usuário: {cliente["nome"]}')
   print(f'  CPF: {cpf}')
   print(f'  Número da Conta: {cliente["numero_conta"]}')
   print(f'  Saldo: R$ {cliente["saldo"]:.2f}')
   print('=' * 40)








# ===============================#
#       CONSULTAR SALDO
# ===============================#




def consultar_saldo(cpf):




   cliente = cadastros[cpf]




   print('=' * 40)
   print(f'  Usuário: {cliente["nome"]}')
   print(f'  CPF: {cpf}')
   print(f'  Número da Conta: {cliente["numero_conta"]}')
   print(f'  Saldo atual: R$ {cliente["saldo"]:.2f}')
   print('=' * 40)








# ===============================#
#           DEPOSITAR
# ===============================#




def depositar(cpf):




   cliente = cadastros[cpf]




   try:




       depos = float(input('Quanto você deseja depositar? R$ '))




       if depos > 0:




           cliente['saldo'] += depos




           print(f'\nDepósito de R$ {depos:.2f} realizado com sucesso!')
           print(f'Seu saldo atual é de: R$ {cliente["saldo"]:.2f}')




       else:




           print('\nDigite um valor maior que R$ 0.')




   except ValueError:




       print('\nDigite um valor numérico válido.')








# ===============================#
#              SACAR
# ===============================#




def sacar(cpf):




   cliente = cadastros[cpf]




   try:




       saque = float(input('Quanto você deseja sacar? R$ '))




       while saque <= 0 or saque > cliente['saldo']:




           if saque <= 0:




               print('\nO valor do saque deve ser maior que R$ 0.')
               return


           elif saque > cliente['saldo']:
               if  cliente ['saldo']==0:
                   print('saldo insuficiente')
                   print(f'Seu saldo atual é: R$ {cliente["saldo"]:.2f}')
                   return




















           saque = float(input('Digite outro valor para sacar: R$ '))




       cliente['saldo'] -= saque




       print(f'\nSaque de R$ {saque:.2f} realizado com sucesso!')
       print(f'Seu saldo atual é de: R$ {cliente["saldo"]:.2f}')




   except ValueError:




       print('\nDigite um valor numérico válido.')








# ===============================#
#     PROCURAR POR NÚMERO DE CONTA
# ===============================#




def procurar_por_conta(numero_conta):




   print('\n========== CONSULTA POR NÚMERO DE CONTA ==========')




   for cpf, dados in cadastros.items():




       if dados['numero_conta'] == numero_conta:




           print('\nConta encontrada!')
           print('=' * 40)
           print(f'  Usuário: {dados["nome"]}')
           print(f'  CPF: {cpf}')
           print(f'  Número da Conta: {dados["numero_conta"]}')
           print(f'  Saldo: R$ {dados["saldo"]:.2f}')
           print('=' * 40)




           return




   print('\nConta não encontrada.')








# ===============================#
#     LISTAR TODAS AS CONTAS
# ===============================#




def listar_contas():




   print('\n========== LISTA DE CONTAS ==========')




   # Verifica se existem contas
   if len(cadastros) == 0:




       print('\nNenhuma conta cadastrada.')
       return




   # Mostra quantidade de contas
   print(f'\nTotal de contas cadastradas: {len(cadastros)}')




   # Percorre todos os clientes
   for cpf, dados in cadastros.items():




       print('=' * 40)
       print(f'  Usuário: {dados["nome"]}')
       print(f'  CPF: {cpf}')
       print(f'  Número da Conta: {dados["numero_conta"]}')
       print(f'  Saldo: R$ {dados["saldo"]:.2f}')
       print('=' * 40)








# ===============================#
#          MENU DA CONTA
# ===============================#




def menu_conta(cpf):




   while True:




       cliente = cadastros[cpf]




       print('\n')
       print('=' * 40)
       print(f'Olá, {cliente["nome"]}!')
       print('=' * 40)




       print('''
[1] Consultar saldo
[2] Depositar
[3] Sacar
[4] Ver dados da conta
[5] Sair da conta
''')




       opcao = input('Digite a opção desejada: ')




       if opcao == '1':




           consultar_saldo(cpf)




       elif opcao == '2':




           depositar(cpf)




       elif opcao == '3':




           sacar(cpf)




       elif opcao == '4':




           conta_login(cpf)




       elif opcao == '5':




           print('\nLogout realizado com sucesso!')
           break




       else:




           print('\nOpção inválida!')








# ===============================#
#           MENU PRINCIPAL
# ===============================#




def menu_app():




   while True:




       print('\n$TESTBANK$')
       print('\nOlá, você está na TestBank!')
       print('-' * 40)




       print('''
[1] Efetuar login
[2] Abrir nova conta
[3] Procurar conta por número
[4] Consultar todas as contas
[5] Sair
''')




       print('-' * 40)




       opcao = input('Digite a opção desejada: ')




       # =========================
       # OPÇÃO 1 - LOGIN
       # =========================




       if opcao == '1':




           cpf = input('\nDigite seu CPF: ')




           if cpf in cadastros:




               menu_conta(cpf)




           else:




               print('\nCPF não encontrado.')




       # =========================
       # OPÇÃO 2 - ABRIR CONTA
       # =========================




       elif opcao == '2':




           abrir_conta()




       # =========================
       # OPÇÃO 3 - PROCURAR CONTA
       # =========================




       elif opcao == '3':




           numero = input('\nDigite o número da conta (ex: CONTA01): ').upper()




           procurar_por_conta(numero)




       # =========================
       # OPÇÃO 4 - LISTAR CONTAS
       # =========================




       elif opcao == '4':




           listar_contas()




       # =========================
       # OPÇÃO 5 - SAIR
       # =========================




       elif opcao == '5':




           print('\nOperação encerrada!')
           break




       else:




           print('\nOpção inválida!')








# ===============================#
#            FRONT END
# ===============================#




menu_app()




print('\nSessão encerrada!')














