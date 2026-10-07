Constitution — Zona Azul Digital

1. Regras de negócio gerais
Dinheiro: Trabalhar sempre com centavos inteiros (int). Sem números com vírgula ou float. O valor nunca pode ser menor que zero ou maior que o teto diário.
Datas: Todas as datas e horários devem usar o padrão ISO-8601 com o fuso -03:00 (exemplo: 2026-10-05T08:00:00-03:00).
Estados do bilhete: Todo bilhete começa como aberto. Só pode mudar para encerrado ou cancelado. Depois disso, não dá mais para alterar nada.
Respostas: Usar JSON em minúsculo e com underline (snake_case).

2. Formato dos dados
Dinheiro: Valor em centavos (R$ 10,00 vira 1000).
Datas: YYYY-MM-DDTHH:MM:SS-03:00.
Placa: Texto com 7 letras ou números maiúsculos (exemplo: ABC1D23).
IDs: Números inteiros começando em 1.

3. Tratamento de erros
Status 200: Deu tudo certo.
Status 201: Bilhete criado com sucesso.
Status 404: Bilhete não encontrado.
Status 409: Regra de negócio violada (exemplo: placa já estacionada ou re-encerrar bilhete).
Status 422: Dado enviado com formato errado (placa errada, data ruim).
Resposta de erro sempre no formato: {erro: nome_do_erro}.

4. Restrições
Fazer apenas o que foi pedido no contrato.
Importar as configurações de regras do arquivo scripts/variante.py.
