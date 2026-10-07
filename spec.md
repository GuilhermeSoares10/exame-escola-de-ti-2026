Especificação — Zona Azul Digital

Objetivo
Explicar as regras e os critérios de teste de cada funcionalidade da API.

UC1 — Abrir bilhete
Endpoint: POST /bilhetes
Entrada: {placa: ABC1D23, entrada: 2026-10-05T08:00:00-03:00} (entrada é opcional).
Sucesso HTTP 201: {id: 1, placa: ABC1D23, entrada: ..., status: aberto}
Critérios de Aceite
Dado uma placa válida sem bilhete aberto, Quando enviar a requisição, Então cria o bilhete com status aberto e retorna HTTP 201.
Dado que a placa não enviou o campo entrada, Quando criar o bilhete, Então preenche com a hora atual do servidor.
Dado que a placa já tem um bilhete aberto, Quando tentar abrir outro, Então retorna HTTP 409 com {erro: bilhete_em_aberto}.
Dado uma placa inválida, Quando enviar, Então retorna HTTP 422 com {erro: placa_invalida}.

UC2 — Encerrar bilhete
Endpoint: POST /bilhetes/{id}/encerramento

Passos do cálculo:
Achar minutos entre entrada e saída (segundos restantes arredondam pra cima).
Se minutos menor ou igual a tolerância, valor = 0.
Se minutos maior que tolerância, cobra tudo desde o minuto 1.
Achar número de frações = arredondar para cima (minutos / FRACAO_MINUTOS).
Calcular valor = frações x valor_da_fração.
Se valor calculado maior que teto diário, valor final = teto diário.
Critérios de Aceite
Dado um bilhete aberto, Quando encerrar, Então mudo status para encerrado, coloco o tempo em minutos e retorno o valor_centavos correto.
Dado um bilhete já encerrado, Quando tentar encerrar de novo, Então retorna HTTP 409 com {erro: bilhete_ja_encerrado}.
Dado um ID que não existe, Quando tentar encerrar, Então retorna HTTP 404 com {erro: bilhete_nao_encontrado}.

UC3 — Listar ativos
Endpoint: GET /bilhetes/ativos
Critérios: Retorna só os bilhetes abertos, dos mais novos para os mais antigos. Se não tiver nenhum, retorna lista vazia [].

UC4 — Relatório diário
Endpoint: GET /relatorios/diario?data=2026-10-05
Critérios: Retorna total de bilhetes encerrados no dia, faturamento somado e tempo médio. Se a média der decimal .5, arredonda para cima. Se não tiver nada no dia, retorna tudo com 0.

UC5 — Cancelar bilhete
Endpoint: POST /bilhetes/{id}/cancelamento
Critérios: Mudar status para cancelado (só funciona se estiver aberto). Se tentar cancelar bilhete encerrado ou já cancelado, retorna HTTP 409 com {erro: bilhete_nao_aberto}.

UC6 — Histórico por placa
Endpoint: GET /bilhetes?placa=ABC1D23
Critérios: Retorna todos os bilhetes da placa (qualquer status), do mais recente pro mais antigo. Se a placa nunca estacionou, retorna lista vazia [].

UC7 — Tolerância gratuita
Critérios: Até o tempo limite de tolerância cobra 0. Passou 1 minuto a mais do limite, cobra o tempo total cheio desde o primeiro minuto.

UC8 — Uma vaga por placa
Critérios: Não deixa abrir bilhete para placa que já está com um bilhete aberto. Só libera para abrir de novo quando o anterior for encerrado ou cancelado.

Erros do Sistema
Placa errada: HTTP 422 e {erro: placa_invalida}

Data/Hora errada: HTTP 422 e {erro: entrada_invalida} ou {erro: data_invalida}

ID sumido: HTTP 404 e {erro: bilhete_nao_encontrado}

Ações repetidas ou conflito: HTTP 409
