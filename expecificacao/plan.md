Plano Técnico — Zona Azul Digital

1. Stack
Linguagem: Python
Framework: FastAPI
Por quê: É fácil de usar, rápido e já faz validações automáticas com Pydantic.

2. Persistência
Onde guardar: Tudo em memória (listas e dicionários do Python).
Por quê: É um teste simples e atende o que o exercício precisa sem ter que instalar banco de dados.

3. Modelo de dados
Bilhete: Guardar id, placa, entrada, saída, minutos, valor_centavos e status (aberto, encerrado, cancelado).

4. Estrutura das Rotas
Separar as funções de cálculo da lógica das rotas para o código não ficar bagunçado.

5. Horários
Usar o módulo datetime do Python travado sempre no fuso -03:00 (horário de Brasília).

6. Dinheiro
Fazer todas as contas usando números inteiros (centavos) para evitar erros de arredondamento de ponto flutuante.

7. Configurações
Ler as variáveis do arquivo scripts/variante.py na hora de rodar a API.
