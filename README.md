# Rating Foresight
Por Alexandre Magno e Pedro Pertusi

# Descrição
Programa em Jupyter Notebook que recebe um dataframe de avaliação de usuários em relação a filmes. Com isso, a partir de processos de decomposição matricial e remoção componentes, busca-se calcular avalições que sejam próximas às reais.

# Como utilizar
* É possível instalar a aplicação de duas formas:
  * Clonagem do repositório utilizando o seguinte comando no terminal: `git clone https://github.com/alemagno10/Rating-Foresight`.
  * Ou baixar o arquivo zip desse repositório em `Code > Download Zip`. E descompactá-lo onde preferir.
* Em seguida, execute o comando: `pip install -r requirements.txt` no diretório principal do projeto clonado.
* Execute o programa com o seguinte comando: `python Foresight.ipynb`

# Modelo Matemático
Para esse projeto, a técnica utilizada para resolução do problema foi o SVD: Decomposição em Valores Singulares. Isso consiste em decompor uma matriz quadrada em três componentes: U * $\Sigma$ * $V^T$, em que: 
* As colunas de $U$ são os auto-vetores de $A^T A$,
* As colunas de $V$ (e, portanto, as linhas de $V^T$) são auto-vetores de $A A^T$,
* $\Sigma$ é uma matriz onde $s_{i,i}$ é a raiz quadrada dos auto-valores de $A^T A$ ou de $A A^T$.

Após extrair os resultados do SVD, os valores singulares podem ser ordenados em ordem decrescente de energia/influência, e em seguida é possível descartar aqueles que são menos influêntes, o que significa que as informações correspondentes a esses vetores serão ignoradas na reconstrução da matriz. Assim, a informação com ruído presente nesses componentes também será reduzida. Dessa forma, a matriz reconstruída a partir da SVD conterá menos ruído e seus dados ficarão próximos aos originais.

# Implementação
Iniciamente, recebemos um dataframe que contia dados de 670 usuários e suas avalições de 0 a 5 pontos para determinados filmes. Para preparar esse dados para o processo de predição, foi utilizada a função `df.pivot()`, transformando-os assim numa matriz Usuário X Filme com valores sendo a nota dada para o filme peelo o usuário. Todavia, devido a ausência de dados esperado, nem todo usuário assistiu e avaliou todos os filmes, existiam muitos valores nulos, e para esses dados optamos então por trocá-los pela média entre 0 e 5, logo 2.5, para assim afetar menos possível nossos resultados. 


Foi implementado em sequência a funçao `get()`, que recebe o df antes e depois do pivot, e seleciona uma linha no dataframe original e depois devolve o indíce (linha x coluna) no novo dataframe depois de aplicado o pivot, com isso garantindo que sempre será escolhido um valor existente previamente, em contrapartida aos valores novos de 2.5 no dataframe de pivot. Essa função vai ser essencial na hora de prêver as notas, responsável por escolher tal usuário e filme que será previsto.

A função `multPredictError(df,dfp,i)` é a função responsável justamente por estimar os i valores sujados e devolver a média do erro entre a estimativa e o valor real das i estimativas. 

`i` = Quantidade de valores que serão sujados, e logo, estimados.

`df` = Dataframe original antes do pivot.

`dfp` = Dataframe depois do pivot.

Por fim, implementamos o **teste de estresse**, tendo em vista a exigência de pelo menos mil estimativas, decidimos então partir do pressuposto de estimar mil dados por interação e repetir esse processo 100 vezes, para então assim poder obter dados para análise, inclusive uma delas sendo o histograma discutido futuramente.

# Resultados Encontrados
* <<<<<incluindo o histograma dos erros e uma conclusão, baseada em dados, sobre se o grupo acredita que o sistema proposto poderia ser usado em produção>>>>>>>>>.
Como grupo obtivemos resultados positivos quanto ao algorítimo de recomendação reproduzido. De maneira geral, com nossos resultados seria possível sim realizar estimativas interessantes quanto a notas que usuários dariam para filmes, algo essencial quando estamos falando do conceito de rating foresight. Alguns pontos importantes inferidos pelo grupo incluem, a diferença que reduzir componentes causa na efetividade do algorítimo, em especial foram testados estimar dados com 21, 5 e 1 componentes e quanto menor o numero de componentes, maior será a redução do ruído, obtendo-se assim estimativas com graus menores de variação. Isso pode ser representado na imagem abaixo, aonde a imagem represente os auto-valores e é possível perceber que a grande parte deles é 0, logo podem ser descartados com o fim de obter um melhor resultado.

![Autovetores](https://github.com/alemagno10/Rating-Foresight/blob/main/k_value.png)


O grupo também optou por uma vizualização gráfica, mais especificamente um histograma, que pode ser vizualizado abaixo. O histograma utilizou dados do nosso teste de estresse, que contém informação sobre o grau médio de erro para mil previsões por interação, com um total de cem interações. O que particularmente  nos supreendeu, foi um grau de erro menos elevado quando comparado a interações com menos previsões, isso particularmente fugiu um pouco da nossa perspectiva pois se acreditava que quanto mais ruído menos preciso seria o algorítimo. Uma das possíveis hipóteses levantada pelo grupo para tal ocorrido, 

![Teste de Estresse](https://github.com/alemagno10/Rating-Foresight/blob/main/histo.png)