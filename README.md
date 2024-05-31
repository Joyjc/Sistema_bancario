# Sistema_bancario
class SistemaBancario:
    def __init__(self):
        self.saldo = 0
        self.movimentacoes = []

    def depositar(self, valor):
        if valor > 0:
            self.saldo += valor
            self.movimentacoes.append(f'Depósito: R$ {valor:.2f}')
            print(f'Depósito de R$ {valor:.2f} realizado com sucesso.')
        else:
            print('Valor de depósito inválido.')

    def sacar(self, valor):
        if valor > 0:
            if valor <= 500 and len([m for m in self.movimentacoes if 'Saque' in m]) < 3:
                if self.saldo >= valor:
                    self.saldo -= valor
                    self.movimentacoes.append(f'Saque: R$ {valor:.2f}')
                    print(f'Saque de R$ {valor:.2f} realizado com sucesso.')
                else:
                    print('Saldo insuficiente para saque.')
            else:
                print('Limite diário de saques atingido ou valor de saque inválido.')
        else:
            print('Valor de saque inválido.')

    def extrato(self):
        if not self.movimentacoes:
            print('Nenhuma movimentação foi realizada.')
            return
        print('Extrato Bancário:')
        for movimentacao in self.movimentacoes:
            print(movimentacao)
        print(f'Saldo atual: R$ {self.saldo:.2f}')


# Exemplo de uso do sistema bancário
sistema = SistemaBancario()
sistema.depositar(1000)
sistema.sacar(500)
sistema.sacar(700)  # Isso deve falhar por exceder o limite diário de saques
sistema.depositar(300)
sistema.sacar(200)
sistema.extrato()
