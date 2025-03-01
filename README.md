## SourceCode: https://databricks-prod-cloudfront.cloud.databricks.com/public/4027ec902e239c93eaaa8714f173bcfc/218949856965537/3264068536626125/8312571501716477/latest.html

# O presente trabalho tem o objetivo de analisar a relação entre taxa Selic e fundos de investimento.

## As perguntas que quero responder através desse trabalho são:

### 1 - A variação na taxa de Selic afeta a criação ou encerramento dos fundos?

### 2 - À medida que a taxa Selic aumenta, quais categorias de fundo mais crescem também?

### 3 - À medida que a taxa Selic diminui, quais categorias de fundo mais crescem?

# Busca
Utilizei o site https://dadosabertos.bcb.gov.br/ para buscar a série histórica da taxa Selic e utilizei o site https://data.anbima.com.br/ para buscar as informações dos fundos de investimento.

# Coleta
Para utilizar a API da ANBIMA DATA precisa pagar, por isso, fiz a coleta manual do data set, via download. Pela praticidade do processo, Fiz o mesmo para o dataset da Taxa Selic. 

# Carga
Fiz o upload dos arquivos CSV direto na plataforma DataBricks para persistir os dados em nuvem.

# Modelagem
A modelagem foi feita no DataBricks UI, a partir do dataset em CSV. Da minha parte foi preciso dizer que a primeira linha deveria ser usada como cabeçalho e com isso a tabela foi criada. 

# Análise de dados
Utilizando PySpark SQL, eu rodei um select nas tabelas e coloquei em variáveis de dataframe (df), depois filtrei para os fundos só os campos que são úteis para minha análise (data início atividade, status, categoria). Também foi necessário criar as colunas de mês e ano para conseguir fazer a comparação posteriormente. Fiz então a contagem de fundos que haviam sido criados / encerrados no mês / ano. Foi quando eu plotei o gráfico e vi que o aumento da taxa selic também aumentava a quantidade de fundo criado e isso estava indo contra a minha tese.
Por isso, eu vi a necessidade de detalhar os tipos de fundo e foi quando ficou mais claro pra mim. Quanto maior a taxa Selic, mais fundos de renda Fixa e FIDC são criados, porque estes tem os investimentos com retorno positivamente ligado a taxa Selic. Também ficou evidente que fundos multimercado e ações tem a taxa de criação reduzida quando a taxa Selic está alta e taxa de criação aumentada quando a taxa Selic diminui. 

E respondendo as perguntas com os gráficos, temos:
### 1 - A variação na taxa de Selic afeta a criação ou encerramento dos fundos?
![image](https://github.com/user-attachments/assets/50f1e590-1ebe-4cdf-8037-5c0a8b8c0c84)
R: Não. Vemos que mesmo com a alta da taxa Selic temos uma grande quantidade de fundos criados.

### 2 - À medida que a taxa Selic aumenta, quais categorias de fundo mais crescem também?
![{8619C3F9-DAE6-4337-B16B-5EB4A0F4853D}](https://github.com/user-attachments/assets/764f6095-8cae-4aec-9ef9-17702305e7cd)
R: FIDCs e Renda Fixa.

### 3 - À medida que a taxa Selic diminui, quais categorias de fundo mais crescem?
![{E0FCB227-9D54-4771-AB34-19626607336C}](https://github.com/user-attachments/assets/54f395ec-c343-4023-bd2c-dd11c05bab40)

R: Ações e multimercado

# Autoavaliação
Eu tinha uma hipótese de que quanto maior fosse a taxa Selic, menor era a quantidade de fundos criados, porém no primeiro gráfico eu tive uma surpresa. Apesar da alta da taxa Selic nos últimos meses, a quantidade de fundos criados aumentou também. Isso me levou a ir além, pensei, será que todas as categorias de fundo tiveram o mesmo comportamento? Foi então que criei um gráfico mais detalhado e entendi o que havia acontecido. Fundos de Renda Fixa e FIDC tem a taxa de criação positivamente correlacionada com a taxa Selic e fundos multimercado e ações, negativamente. Curiosamente o fundo de Previdência também tem uma correlação negativa com a taxa Selic e isso é curioso, porque esses fundos, em tese, deveriam ter a maioria dos seus ativos composto por renda fixa, que está positivamente ligado a taxa Selic.

