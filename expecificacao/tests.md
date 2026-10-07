**# Testes — Zona Azul Digital

## 1. Abertura de bilhete

Tabela:
| Cenário | Entrada | Esperado |

## 2. Cálculo de cobrança

Tabela:
| Cenário | Duração | Esperado |

## 3. Frações

Tabela:
| Cenário | Duração | Esperado |

## 4. Teto

Tabela:
| Cenário | Valor calculado | Esperado |

## 5. Tolerância

Tabela:
| Cenário | Duração | Esperado |

## 6. Encerramento

Tabela:
| Cenário | Estado | Esperado |

## 7. Cancelamento

Tabela:
| Cenário | Estado | Esperado |

## 8. Uma vaga por placa

Tabela:
| Cenário | Situação | Esperado |

## 9. Histórico

Tabela:
| Cenário | Bilhetes | Esperado |

## 10. Relatório diário

Tabela:
| Cenário | Dados | Esperado |

## 11. Validações

Tabela:
| Entrada inválida | Status | Erro esperado |
**Testes — Zona Azul Digital

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

📋 5. tasks.md
Tasks — Zona Azul Digital

Tarefa 1: Criar o projeto Python, instalar dependências e carregar as variáveis do arquivo variante.py.

Tarefa 2: Criar o modelo do bilhete e a estrutura em memória para guardar os dados.

Tarefa 3: Criar a rota POST /bilhetes com validação de placa e checagem de vaga ocupada.

Tarefa 4: Criar a lógica de cálculo (minutos, tolerância, frações, teto) e a rota POST /bilhetes/{id}/encerramento.

Tarefa 5: Criar a rota de cancelamento POST /bilhetes/{id}/cancelamento.

Tarefa 6: Criar as rotas de busca (GET /bilhetes/ativos e GET /bilhetes com filtro de placa).

Tarefa 7: Criar a rota do relatório diário GET /relatorios/diario.

Tarefa 8: Fazer os testes automatizados com pytest e testar tudo.
