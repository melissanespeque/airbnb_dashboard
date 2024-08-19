# Dashboard Descritivo - Dados do Airbnb

### Objetivo:

Dashboard desenvolvido para estudos pessoais. Optei por usar uma base sobre AirBNB por ser um assunto o qual me interesso e me identifico.
O objetivo desse dashboard é poder ter uma visão empresarial - alguém que pretenda iniciar um empreendimento para Airbnb tomar decisões de em qual cidade, região, qual tipo de imóvel, entre outras informações. Além de trazer informações que mapeiem o perfil dos hosts.
Dados disponíveis em: https://www.kaggle.com/datasets/mysarahmadbhat/airbnb-listings-reviews

### Desafios:

Um dos maiores desafios foi o tratamento dos dados. Os dados sobre cidade e região não estavam estruturados, sendo assim optei por importar bases dimensão de cidade-estado-país. Isso também para facilitar outras visualizações, que optei por não desenvolver nesse momento.
Por não haver um dicionário de dados muito claro, tive desafios na interpretação de alguns dados e como normalizá-los.
O resultado não é perfeito, alguns detalhes optei por não dar atenção nesse momento, por tratar-se de um objeto de estudos básicos. Por exemplo, nesse momento não fiz normalização de moeda.Tentei formular e traduzir tudo em Português-BR para facilitar a compreensão.
Foram analisados dados de 8 cidades em 8 países diferentes, considerando hospedagens a partir de 01/01/2018, não havendo diferenciação do período pandêmico.
Medidas Criadas (DAX):

![image](https://github.com/user-attachments/assets/ddc5856b-9c16-4c6a-a8ba-d7a864a9da85)
Tabela dimensão calendário, considerando 01/01/2018 a 31/12/2022

![image](https://github.com/user-attachments/assets/5fcbebb5-ec66-499c-a2f0-60fe725f9418)
Medida para obter a cidade com maior Score médio, considerando a medida geral de Score médio por cidade

![image](https://github.com/user-attachments/assets/9b1ad461-8fb5-490e-aa83-e7e634005784)
Medida criada para obter o Score médio de cada cidade, a partir da medida anterior de Média Score

![image](https://github.com/user-attachments/assets/ac8b8c2b-a159-47d7-bce1-881bc5b26d28)
Média de Score considerando os 6 itens de review nas bases de dados

![image](https://github.com/user-attachments/assets/cb596dab-4e40-4be2-a381-0e3c5c4232ae)
Contagem da quantidade de hosts

### Tratamento de dados:

Remoção de outliers, filtrando [accomodates] <= 10 e [bedrooms] <= 7;
Normalização de preço por noite: usando Preço Norm = [price]/[minimum_nights] e colocando [Preço Norm] <= 1100 e [minimum_nights] <= 31;
Tratativa dos valores nulos;
Tradução do itens para português;
Atribuição da seguinte categorização para a avaliação da hospedagem: Se Score = 0 é "Inválido"; Se Score <= 20, "Muito Insuficiente"; Score <= 40, "Insuficiente"; Score <= 60, "Razoável"; Score <= 80, "Bom"; Outros, "Excelente";
= Table.AddColumn(#"Valor Substituído", "Rating", each if [review_scores_rating] = 0 then "Inválido" 
else if [review_scores_rating] <= 20 then "Muito insuficiente" 
else if [review_scores_rating] <= 40 then "Insuficiente" 
else if [review_scores_rating] <= 60 then "Razoável" 
else if [review_scores_rating] <= 80 then "Bom" else "Excelente")

### Modelo de dados:
![image](https://github.com/user-attachments/assets/90865b2f-6871-443f-b5b9-d2d4ed31109a)

### Relatório:

Filtros: é possível filtrar bom período de Data, Cidade, Avaliação da propriedade e Tipo de quarto;
Hospedagens por cidade: quantidade de propriedades diferentes disponíveis para hospedagem por cidade;
Preço por cidade e tipo de quarto: visualização do preço normalizado por cidade, legendado pelo tipo de hospedagem (lugar todo, quarto de hotel, quarto pivado ou quarto compartilhado);

Média de Score por Cidade: Score médio de cada cidade;
![image](https://github.com/user-attachments/assets/25a52464-3346-467e-92ba-9cb6cbb454c0)

Distribuição das hospedagens por ano: é possível fazer o drill down para obter a informação por mês. Mostra quantas hospedagens foram fechadas por mês, ano. Legendado por cada cidade;
Distribuição do preço por hospedagens: mostra quantas hospedagens possuem aquele valor por noite (preço normalizado);
Hospedagens por ano e mês: visualização simples para mostrar a quantidade de hospedagens fechadas a cada ano/mês, podendo identificar momentos de alta e baixa temporada;
Preço médio por ano e tipo de quarto: é possível fazer o drill down para obter a informação por mês. Monstra a variação da média mensal do preço, sendo cada linha representada por um tipo de quarto;
Distribuição da avaliação por ano e mês: mostra a avaliação média geral;

![image](https://github.com/user-attachments/assets/cde9fb21-8b6b-4067-972f-66ba3a41421b)

Média de Score por Tipo de propriedade: obtenção do score médio geral, de acordo com o tipo de propriedade ofertada no AirBNB;
Preço médio por tipo de quarto e cidade: análogo à visualização da página 1, facilitando ver o comportamento dos preços por tipo de quarto em cada cidade;
Distribuição da quantidade de quartos: quantas hospedagens oferece cada quantidade de quartos, de 1 a 7, sendo valores absolutos e positivos;
Distribuição da quantidade mínima de noites: quantas hospedagens estão alocadas em cada quantidade de noites mínimas para fechar a hospedagem, de 1 a 31;
Distribuição das quantidades de hóspedes: quantas hospedagens podem alocar cada quantidade de hóspedes disponível, variando de 1 a 10;

![image](https://github.com/user-attachments/assets/288d6b78-adf4-4f9e-8f8d-4b70285cfdcf)

Média de Score por tempo de resposta: mostra a variação do Score médio, de acordo com cada categoria de tempo de resposta;
Hospedagens por avaliação: dentro da categorização de avaliações, quantas hospedagens obtiveram cada uma. A quantidade elevada de "Inválidos" dá-se por muitos hospedes não terem deixado avaliação da hospedagem;
Hosts com mais hospedagens: indica o Host ID que mais fechou hospedagens;
Hospedagens por tipo de quarto: indica quantas hospedagens há por categoria de tipo de quarto;
Quantidade de Hosts por identidade verificada: indica se há alguma diferença entre hosts que verificaram suas contas e os que não; 

![image](https://github.com/user-attachments/assets/f0ba13d3-3837-4ca2-8214-2e850750376b)

### Conclusão:
É possível gerar alguns insights a partir do dashboard, como por exemplo:
A cidade do México é a que obteve melhor média de avaliação e também a 7◦ em quantidade de hospedagens, havendo muto espaço para crescimento;
A diária do quarto de hotel é, em média, mais cara que a diária de aluguel do local todo;
Hospedagens que oferencem "Lugar todo" também foram as mais buscadas, sendo 72% avaliadas em Bom ou Excelente;
Entre Outros. Há muitos ajustes que pretendo fazer futuramente, mas decidi compartilhar como está no momento.
