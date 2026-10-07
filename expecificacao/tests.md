Testes — Zona Azul Digital

(Exemplos considerando: Tarifa R$ 6,00/h | Fração 15 min | Teto R$ 20,00 | Tolerância 10 min)

1. Abertura
Abertura normal com placa válida: Retorna status 201 e bilhete aberto

Placa em minúsculo (ex: abc1d23): Retorna status 422 e erro placa_invalida

Fuso de data sumido (ex: 2026-10-05T08:00:00): Retorna status 422 e erro entrada_invalida

2. Cobrança e Frações
Fração exata de 15 min: Cobra 1 fração (150 centavos)

Fração exata de 30 min: Cobra 2 frações (300 centavos)

Um minuto depois da fração (16 min): Cobra 2 frações (300 centavos)

Um minuto depois da fração (31 min): Cobra 3 frações (450 centavos)

3. Tolerância
Dentro da tolerância (10 min): Cobra 0 centavos

Um minuto após a tolerância (11 min): Cobra tempo cheio (11 min = 1 fração = 150 centavos)

4. Teto Diário
Cálculo passou do teto (300 min): Trava no valor do teto diário (2000 centavos)

5. Validações e Erros
Bilhete não existe (ID 999): Retorna status 404 e erro bilhete_nao_encontrado

Re-encerrar bilhete: Retorna status 409 e erro bilhete_ja_encerrado

Placa já estacionada: Retorna status 409 e erro bilhete_em_aberto
