# Risco-de-RN-com-asfixia
Projeto de avaliação de risco de partos em Rondônia

O DataSUS disponibiliza diversos arquivos de dados com relação a seus segurados, conforme a lei da transparência de informações públicas.

O Sistema de Informações sobre Nascidos Vivos ( SINASC ), foi implantado oficialmente a partir de 1990, com o objetivo de coletar dados sobre os nascimentos informados em todo território nacional e fornecer dados sobre natalidade para todos os níveis do Sistema de Saúde. Essas informações podem ser obtidas pela internet aqui. A base de dados é referente aos partos realizados no estado de Rondôdina (RO) em 2019.

1.1 Objetivo
Organização da base para estudar a relação entre partos com risco para o bebê e algumas condições como tempo de gestação, consultas de pré-natal e peso do bebê. Por fim estipular apossibilidade de criar uma árvore de decisão para risco de asfixia de acordo com tais parâmetros. Um dos parâmetros avaliados nesta base de dados é obtido por testes feitos logo após o nascimento. Durante o teste são avaliados alguns sinais apresentados pelo bebê, como a cor da pele e o número de batimentos cardíacos, que são pontuados conforme a escala de APGAR para dar um resultado final. Esta avaliação é feita logo após o nascimento (APGAR no primeiro minuto de vida) repetida 5 minutos depois (APGAR no quinto minuto de vida), onde, numa escala de 0 a 10, os valores mais próximos de 0 indicam risco para o bebê. O Apgar possui uma classificação indicando se o bebê passou por asfixia:

Entre 8 e 10 está em uma faixa 'normal'.
Entre 6 e 7, significa que o recém-nascido passou por 'asfixia leve'.
Entre 4 e 5 significa 'asfixia moderada'.
Entre 0 e 3 significa 'asfixia severa'.
Explorado o dataframe é possível utilizar essas informações para gerar interpretações.

Descrição das colunas relevantes
Coluna	Descrição
IDADEMAE	Iadade da mãe
ESTCIVMAE	Estado civil da mãe
LOCNASC	Local de ocorrência do nascimento conforme tabela*
ESCMAE	Escolaridade da mãe(anos) conforme tabela**
CONSULTAS	Número de consultas conforme tabela***
GESTACAO	Semanas de gestação conforme a tabela****
GRAVIDEZ	Tipo de gravidez conforme a tabela*****
PARTO	Tipo de parto conforme a tabela******
QTDFILVIVO	Número de filhos vivos
APGAR1	APGAR no primeiro minuto
APGAR5	APGAR no quinto minuto
PESO	peso do bebê
apgar5_risco	Se possui risco de asfixia
class_asfix	Grau da asfixia
Legenda das tabelas:
*LOCNASC = Local de ocorrência do nascimento, conforme a tabela: 9: Ignorado. 1: Hospital. 2: Outro Estab Saúde. 3: Domicílio. 4: Outros.

**ESCMAE = Escolaridade, anos de estudo concluídos: 1: Nenhuma. 2: 1 a 3 anos. 3: 4 a 7 anos. 4: 8 a 11 anos. 5: 12 e mais. 9: Ignorado.

***CONSULTAS = Número de consultas de pré-natal: 1: Nenhuma. 2: de 1 a 3.

****GESTACAO = Semanas de gestação, conforme a tabela: 9: Ignorado. 1: Menos de 22 semanas. 2: 22 a 27 semanas. 3: 28 a 31 semanas. 4: 32 a 36 semanas. 5: 37 a 41 semanas. 6: 42 semanas e mais.

***** GRAVIDEZ = Tipo de gravidez, conforme a tabela: 9: Ignorado. 1: Única. 2: Dupla. 3: Tripla e mais.

****** PARTO = Tipo de parto, conforme a tabela: 9: Ignorado. 1: Vaginal. 2: Cesáreo.
