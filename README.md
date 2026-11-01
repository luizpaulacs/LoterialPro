# Loterial Pro — Gerador e análise de jogos da Lotofácil

Aplicativo web de arquivo único para organizar resultados da Lotofácil, gerar combinações, analisar a composição dos jogos, conferir apostas e acompanhar estatísticas do histórico cadastrado. Usa Firebase Authentication e Cloud Firestore para autenticação, licenças e armazenamento de concursos.

> **Importante:** o aplicativo organiza combinações e resume dados passados. Sorteios são aleatórios. Frequência, atraso, filtros, pontuação e cobertura não preveem resultados nem garantem premiação.

## Funcionalidades

- Autenticação por e-mail e senha com controle de acesso/licença e painel administrativo, conforme as permissões configuradas no Firebase.
- Registro de concursos com número, data e 15 dezenas, seleção visual no volante 01–25, prévia e validação de quantidade, repetição e intervalo.
- Leitura de resultados digitados com separadores ou em pares sem separadores — por exemplo, `01030609` é interpretado como 01, 03, 06 e 09.
- Histórico dos concursos recentes e busca por número do concurso.
- Gerador de jogos de 15, 16, 17 ou 18 dezenas, com estratégias de seleção, filtros de composição e resumo de cobertura de pares e trios.
- Avaliação geométrica de jogos simples e análise em lote dos bilhetes gerados.
- Conferência de apostas simples e múltiplas, resumo de prêmios desdobrados e estimativa financeira configurável.
- Exportação dos jogos para CSV e impressão.
- Ajuda interativa dentro do aplicativo.
- Bloqueio local opcional neste aparelho, usando a autenticação de plataforma disponível no navegador (por exemplo, digital, rosto ou PIN), via WebAuthn.

## Estratégias do gerador

As estratégias abaixo descrevem o comportamento implementado no gerador; elas não são garantias matemáticas de acerto.

- **Matriz Personalizada:** no volante, cada dezena alterna entre livre, fixa e semi-fixa. As fixas são incluídas em todos os jogos; as semi-fixas são priorizadas; as dezenas livres completam o tamanho solicitado. Os contadores ajudam a acompanhar as escolhas.
- **Filtro Geométrico Moldura/Miolo:** distribui o jogo entre dezenas da borda e do centro do volante em proporção aproximada de 60%/40%. A configuração de proporção exibida na interface pode variar conforme a versão do código; não presuma que opções de proporção não aplicadas pelo motor alterem o resultado.
- **R4, R5 e R6 (eliminação):** exigem marcar, respectivamente, 4, 5 ou 6 dezenas para excluir. O gerador escolhe entre as demais dezenas. Os rótulos R4/R5/R6 indicam a quantidade excluída; o código atual não calcula nem comprova fechamento ou garantia de pontuação.
- **Matriz 5 Fixas + 5 Grupos de 4:** marque cinco fixas e distribua as outras vinte dezenas em cinco grupos de quatro. O bilhete simples usa as cinco fixas e duas dezenas por grupo; em bilhetes múltiplos, as vagas adicionais são preenchidas com outras dezenas dos grupos.
- **5 Grupos de 5 (sem fixas):** distribua as 25 dezenas em cinco grupos de cinco. No bilhete simples, o gerador escolhe três dezenas de cada grupo; em bilhetes múltiplos, acrescenta dezenas dos grupos para completar o bilhete.
- **8 Fixas + Variáveis / 9 Fixas + Variáveis:** marque exatamente oito ou nove dezenas fixas. As outras dezenas do bilhete são escolhidas entre as restantes.
- **3 Fixas + 3 Excluídas:** selecione primeiro três fixas e depois três excluídas. As fixas entram em todos os jogos e as excluídas não entram em nenhum; as demais vagas são preenchidas aleatoriamente.

As opções **Ciclo Atrasadas**, **Quadrantes: 3 por Linha** e **Estratégia ABC Grupos** foram removidas do menu do gerador. O monitor de ciclo descritivo que aparece na aba Avaliador é uma análise separada.

## Filtros adicionais

Na seção **Estratégias adicionais (opcionais)**, os campos vazios ou zerados não impõem limite. Os filtros são combinados; parâmetros incompatíveis podem resultar em menos jogos do que o solicitado.

- **Repetidas do último concurso:** mínimo e máximo de dezenas do último resultado cadastrado presentes em cada jogo.
- **Sequência consecutiva:** maior tamanho permitido de uma sequência numérica seguida, como 07–08–09.
- **Soma:** intervalo mínimo e máximo para a soma das dezenas.
- **Moldura e miolo:** limites independentes para quantidade de dezenas da borda e do centro.
- **Linhas e colunas:** limites mínimo e máximo aplicados a cada linha ou coluna do volante.
- **Sem duplicados:** impede jogos idênticos na lista.
- **Máximo de dezenas iguais entre jogos:** limita quantas dezenas dois jogos podem compartilhar; vazio ou zero significa sem esse limite.
- **Cobertura de pares e trios:** o motor procura diversificar as combinações entre jogos e informa quantos pares e trios distintos foram cobertos. É uma medida observada nos jogos gerados, não uma garantia de prêmio.

O gerador usa amostragem aleatória com tentativas limitadas. Quando não consegue encontrar todas as combinações dentro dos filtros e tentativas, mostra a quantidade produzida. Para obter mais jogos, relaxe ou limpe alguns filtros.

## Avaliação e estatísticas

### Avaliador

A pontuação geométrica é uma descrição interna de equilíbrio, de 0 a 10, baseada em seis características: ímpares, moldura, primos, múltiplos de 3, repetidas do último concurso e soma. Os pesos são diferentes: ímpares, moldura, primos e múltiplos de 3 podem somar até dois pontos cada; repetidas e soma, até um ponto cada. A classificação exibida é Excelente (8–10), Bom (6–7), Regular (4–5) ou Atenção (abaixo de 4).

O avaliador individual aceita jogos de 15 dezenas. Na análise em lote, bilhetes de 16 a 18 dezenas são avaliados pela média das combinações simples de 15 dezenas contidas no bilhete. A nota não representa chance de ganhar.

O monitor de ciclos percorre concursos cadastrados em ordem numérica, do mais recente para trás, até todas as 25 dezenas aparecerem ou até alcançar o limite histórico adotado no código. Ele mostra dezenas ainda não vistas nesse trecho; não prevê o próximo sorteio.

### Calor Real

- O número mostrado dentro de cada dezena no mapa de calor é a frequência em **todos os concursos cadastrados**.
- “Mais atrasadas” mede quantos concursos cadastrados se passaram desde a aparição mais recente. Atraso zero significa que a dezena saiu no concurso mais recente cadastrado.
- As medidas não precisam coincidir: uma dezena pode ter frequência histórica alta e estar há vários concursos sem sair.
- O mapa classifica como quente a frequência acima da média das 25 dezenas no histórico carregado; as demais aparecem como frias.
- Os cálculos dependem dos concursos gravados e da ordenação pelo número do concurso. Confira se o histórico está completo e correto.

## Registro e conferência de concursos

1. Abra **Concursos** e informe número e data.
2. Digite ou cole as 15 dezenas. O sistema aceita separadores ou blocos de dois dígitos juntos, por exemplo `01030609`.
3. Confira as dezenas reconhecidas no volante. Corrija formatos incompletos, repetidos ou fora de 01–25 antes de salvar.
4. Clique em **Salvar na Nuvem**. O aplicativo verifica se já existe um concurso com aquele número.
5. Em **Conferir**, insira o resultado oficial com 15 dezenas e cole uma aposta por linha. Cada linha pode conter de 15 a 18 dezenas.

## Financeiro

O conferidor calcula o custo proporcional dos bilhetes múltiplos e distribui os acertos conforme a tabela de desdobramento programada. O retorno financeiro usa valores de premiação configuráveis na aba **Valores**. Esses valores podem não refletir a premiação oficial atual; revise-os antes de usar o balanço. O resultado é uma estimativa com base nos parâmetros informados.

## Conta, Firebase e segurança

O aplicativo usa Firebase Authentication e Cloud Firestore. As regras do Firestore e as permissões do projeto precisam ser configuradas e testadas no Firebase Console. Não considere a interface, a ocultação de botões ou o código do navegador como uma barreira de segurança: a autorização efetiva de leitura e gravação deve ser imposta pelas regras do Firestore.

A chave de configuração do Firebase usada por um frontend web não é uma senha administrativa. Proteja os dados com regras apropriadas, restrições de domínio e controles de uso no Firebase. Nunca coloque senhas de administrador ou credenciais privadas dentro do HTML.

O bloqueio local opcional usa WebAuthn e fica restrito ao aparelho/navegador em que foi ativado. O site não recebe a digital ou o PIN do aparelho. Esse bloqueio não substitui a autenticação da conta nem protege contra acesso por outro dispositivo. O recurso depende de navegador compatível e contexto seguro (HTTPS ou localhost); o usuário deve manter acesso à conta para recuperação.

## Executar e publicar

O projeto é composto por um HTML com JavaScript em módulo que carrega bibliotecas Firebase pela internet. Para testar, use um servidor local (por exemplo, Live Server) em vez de abrir o arquivo diretamente via `file://`. Para publicar, sirva o `index.html` em HTTPS — por exemplo, GitHub Pages — e confirme que o domínio está autorizado nas configurações do Firebase Authentication.

Para atualizar uma instalação existente, faça uma cópia de segurança do `index.html` atual, substitua-o pelo HTML revisado e teste login, registro de concursos, geração, avaliação, conferência e permissões do Firebase antes de considerar a publicação concluída.

## Licença

O software é disponibilizado sob licença proprietária. A redistribuição ou cópia não autorizada depende de autorização expressa do titular.
