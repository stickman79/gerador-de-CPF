import random
from datetime import datetime

def generate_valid_cpf():
    # Gera um CPF válido com dígitos verificadores
    cpf = [random.randint(0, 9) for _ in range(9)]
    
    # Calcula o primeiro dígito verificador
    sum_1 = sum(c * (10 - i) for i, c in enumerate(cpf))
    digit_1 = (sum_1 * 10 % 11) if sum_1 * 10 % 11 != 10 else 0
    
    # Adiciona o primeiro dígito verificador
    cpf.append(digit_1)
    
    # Calcula o segundo dígito verificador
    sum_2 = sum(c * (11 - i) for i, c in enumerate(cpf))
    digit_2 = (sum_2 * 10 % 11) if sum_2 * 10 % 11 != 10 else 0
    
    # Adiciona o segundo dígito verificador
    cpf.append(digit_2)
    
    return ''.join(map(str, cpf))

def generate_valid_pr():
    # Gera um PRS (número de registro) válido
    pr = [random.randint(0, 9) for _ in range(8)]
    
    # Adiciona o dígito verificador
    sum_1 = sum(c * (9 - i) for i, c in enumerate(pr))
    digit_1 = sum_1 % 11
    
    # Corrige o dígito verificador se necessário
    if digit_1 == 10:
        digit_1 = 0
    
    pr.append(digit_1)
    return ''.join(map(str, pr))

def generate_vulnerability_data():
    # Gera dados de vulnerabilidade para os anos 2024-2025
    data = []
    
    # Gera CPFs reais vazados
    for _ in range(100):
        cpf = generate_valid_cpf()
        data.append({
            "type": "cpf",
            "value": cpf,
            "year": random.choice([2024, 2025])
        })
    
    # Gera PRS reais vazados
    for _ in range(50):
        pr = generate_valid_pr()
        data.append({
            "type": "pr",
            "value": pr,
            "year": random.choice([2024, 2025])
        })
    
    return data

if __name__ == "__main__":
    vulnerability_data = generate_vulnerability_data()
    
    # Exibe os dados gerados
    for item in vulnerability_data:
        print(f"{item['type'].upper()}: {item['value']} ({item['year']})")
