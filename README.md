# Risco-de-RN-com-asfixia
Projeto de avaliação de risco de partos em Rondônia
{
 "cells": [
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# Relação entre partos com risco e condições da gestação "
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## 1. Descrição da base de dados"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "O DataSUS disponibiliza diversos arquivos de dados com relação a seus segurados, conforme a [lei da transparência de informações públicas](https://www.sisgov.com/transparencia-acesso-informacao/#:~:text=A%20Lei%20da%20Transpar%C3%AAncia%20(LC,em%20um%20site%20na%20internet.). \n",
    "\n",
    "O Sistema de Informações sobre Nascidos Vivos ( SINASC ), foi implantado oficialmente a partir de 1990, com o objetivo de coletar dados sobre os nascimentos informados em todo território nacional e fornecer dados sobre natalidade para todos os níveis do Sistema de Saúde. Essas informações podem ser obtidas pela internet [aqui](http://www2.datasus.gov.br/DATASUS/index.php?area=0901&item=1). A base de dados é referente aos partos realizados no estado de Rondôdina (RO) em 2019. \n",
    "\n",
    "### 1.1 Objetivo\n",
    "Organização da base para estudar a relação entre partos com risco para o bebê e algumas condições como tempo de gestação, consultas de pré-natal e peso do bebê. Por fim estipular apossibilidade de criar uma árvore de decisão para risco de asfixia de acordo com tais parâmetros.\n",
    "Um dos parâmetros avaliados nesta base de dados é obtido por testes feitos logo após o nascimento. Durante o teste são avaliados alguns sinais apresentados pelo bebê, como a cor da pele e o número de batimentos cardíacos, que são pontuados conforme a escala de APGAR para dar um resultado final. Esta avaliação é feita logo após o nascimento (APGAR no primeiro minuto de vida) repetida 5 minutos depois (APGAR no quinto minuto de vida), onde, numa escala de 0 a 10, os valores mais próximos de 0 indicam risco para o bebê.\n",
    "O Apgar possui uma classificação indicando se o bebê passou por asfixia:\n",
    "- Entre 8 e 10 está em uma faixa 'normal'. \n",
    "- Entre 6 e 7, significa que o recém-nascido passou por 'asfixia leve'. \n",
    "- Entre 4 e 5 significa 'asfixia moderada'.\n",
    "- Entre 0 e 3 significa 'asfixia severa'.\n",
    "\n",
    "\n",
    "Explorado o dataframe é possível utilizar essas informações para gerar interpretações.\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "#### Descrição das colunas relevantes\n",
    "\n",
    "| Coluna | Descrição     |  \n",
    "|------------------|----------| \n",
    "| `IDADEMAE`      | Iadade da mãe    |   \n",
    "| `ESTCIVMAE`      | Estado civil da mãe   |\n",
    "| `LOCNASC`      | Local de ocorrência do nascimento conforme tabela*   |\n",
    "| `ESCMAE`      | Escolaridade da mãe(anos) conforme tabela**   |\n",
    "| `CONSULTAS`      | Número de consultas conforme tabela***   |\n",
    "| `GESTACAO`      | Semanas de gestação conforme a tabela****  |\n",
    "| `GRAVIDEZ`      | Tipo de gravidez conforme a tabela*****  |\n",
    "| `PARTO`      | Tipo de parto conforme a tabela******  |\n",
    "| `QTDFILVIVO`      | Número de filhos vivos  |\n",
    "| `APGAR1`      | APGAR no primeiro minuto  |\n",
    "| `APGAR5`      | APGAR no quinto minuto  |\n",
    "| `PESO`      | peso do bebê  |\n",
    "| `apgar5_risco`      | Se possui risco de asfixia  |\n",
    "| `class_asfix`      | Grau da asfixia  |"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Legenda das tabelas:\n",
    "\n",
    "*LOCNASC = Local de ocorrência do nascimento, conforme a tabela: \n",
    "9: Ignorado. \n",
    "1: Hospital. \n",
    "2: Outro Estab Saúde. \n",
    "3: Domicílio. \n",
    "4: Outros."
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "**ESCMAE = Escolaridade, anos de estudo concluídos: \n",
    "1: Nenhuma. \n",
    "2: 1 a 3 anos. \n",
    "3: 4 a 7 anos. \n",
    "4: 8 a 11 anos. \n",
    "5: 12 e mais. \n",
    "9: Ignorado."
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "***CONSULTAS = Número de consultas de pré-natal: \n",
    "1: Nenhuma.\n",
    "2: de 1 a 3."
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "****GESTACAO = Semanas de gestação, conforme a tabela: \n",
    "9: Ignorado. \n",
    "1: Menos de 22 semanas.\n",
    "2: 22 a 27 semanas.\n",
    "3: 28 a 31 semanas.\n",
    "4: 32 a 36 semanas.\n",
    "5: 37 a 41 semanas. \n",
    "6: 42 semanas e mais."
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "***** GRAVIDEZ = Tipo de gravidez, conforme a tabela: \n",
    "9: Ignorado.\n",
    "1: Única.\n",
    "2: Dupla.\n",
    "3: Tripla e mais."
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "****** PARTO = Tipo de parto, conforme a tabela: \n",
    "9: Ignorado. \n",
    "1: Vaginal. \n",
    "2: Cesáreo."
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
