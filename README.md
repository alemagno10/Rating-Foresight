# Rating Foresight
Por Alexandre Magno e Pedro Pertusi

# Descrição
Programa em Jupyter Notebook que recebe um dataframe de avaliação de usuários em relação a filmes. Com isso, a partir de processos de decomposição matricial e remoção componentes, busca-se calcular avalições que sejam próximas às reais.

# Como utilizar
* É possível instalar a aplicação de duas formas:
  * Clonagem do repositório utilizando o seguinte comando no terminal: `git clone https://github.com/alemagno10/Rating-Foresight`.
  * Ou baixar o arquivo zip desse repositório em `Code > Download Zip`. E descompactá-lo onde preferir.
* Em seguida, execute o comando: `pip install -r requirements.txt` no diretório principal do projeto clonado.
* Execute o programa com o seguinte comando: `python demo.py`

# Modelo Matemático
Para esse projeto, a ferramenta utilizada foi o SVD: Decomposição em valores singulares. Isso consiste em decompor matrizes em autovetores e autovalores, ou seja, componetes que indicam a direção dos dados, e valores que indicam o quanto os vetores influênciam no resultado final. Após o processo de SVD a matriz original se transforma em U * $\Sigma$ * $V^T$, em que :
* As colunas de $U$ são os auto-vetores de $A^T A$,
* As colunas de $V$ (e, portanto, as linhas de $V^T$) são auto-vetores de $A A^T$,
* $\Sigma$ é uma matriz onde $s_{i,i}$ é a raiz quadrada dos auto-valores de $A^T A$ ou de $A A^T$.




# Implementação
Iniciamente, recebemos um dataframe que contia dados de 670 usuários e suas avalições de 0 a 5 pontos para determinados filmes. Para preparar esse dados para o processo de predição, foi utilizada a função `df.pivot()`, transformando-os assim numa matriz Usuário X Filme com valores sendo a nota dada para o filme peelo o usuário. Todavia, devido a ausência de dados esperado, nem todo usuário assistiu e avaliou todos os filmes, existiam muitos valores nulos, e para esses dados optamos então por trocá-los pela média entre 0 e 5, logo 2.5, para assim afetar menos possível nossos resultados. 

# Resultados Encontrados
* <<<<<incluindo o histograma dos erros e uma conclusão, baseada em dados, sobre se o grupo acredita que o sistema proposto poderia ser usado em produção>>>>>>>>>.
