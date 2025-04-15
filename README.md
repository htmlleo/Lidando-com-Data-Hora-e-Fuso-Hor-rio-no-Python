from datetime import datetime
import pytz
from collections import defaultdict

# Função para criar a transação com a data, hora e fuso horário
def criar_transacao(descricao, fuso_horario, transacoes):
    # Obter o fuso horário
    tz = pytz.timezone(fuso_horario)
    
    # Obter a data e hora atual com o fuso horário
    agora = datetime.now(tz)
    
    # Criar a transação
    transacao = {
        "descricao": descricao,
        "data": agora.strftime("%Y-%m-%d %H:%M:%S"),
        "fuso_horario": fuso_horario
    }
    
    # Adicionar a transação à lista
    transacoes.append(transacao)

# Função para listar transações agrupadas por dia
def listar_transacoes_por_dia(transacoes):
    transacoes_por_dia = defaultdict(list)

    for transacao in transacoes:
        # Obter a data da transação (apenas a parte da data, sem hora)
        data_transacao = transacao["data"].split()[0]
        transacoes_por_dia[data_transacao].append(transacao)

    # Exibir as transações agrupadas por dia
    for dia, transacoes_do_dia in transacoes_por_dia.items():
        print(f"\nTransações do dia {dia}:")
        for t in transacoes_do_dia:
            print(f"- {t['descricao']} ({t['data']} - {t['fuso_horario']})")

# Lista para armazenar transações
transacoes = []

# Criando algumas transações com diferentes fusos horários
criar_transacao("Compra de produto", "America/Sao_Paulo", transacoes)
criar_transacao("Pagamento de serviço", "Europe/Lisbon", transacoes)
criar_transacao("Transferência bancária", "America/New_York", transacoes)
criar_transacao("Compra de software", "Asia/Tokyo", transacoes)

# Listando transações agrupadas por dia
listar_transacoes_por_dia(transacoes)
