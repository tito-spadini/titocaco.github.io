---
layout:	post
title: 	"A importância da Compressão de Dados para aplicações Multimídia"
date:	2019-01-05 00:00:00 -0300
author:	Tito Spadini
published: true
---

# A importância da Compressão de Dados para aplicações Multimídia

Ao longo deste artigo será feito um breve passeio por alguns conhecimentos de multimídia para compreendermos a importância da compressão de dados. O objetivo deste artigo não é o de fazer um rigoroso estudo matemático; a ideia aqui é simplesmente a de ajudar a compreender como a compressão ajuda os usuários diariamente a serem capazes de usufruir de tantos produtos e serviços digitais sem nem se darem conta disso.

## Áudio

Depois de o som ser filtrado, amostrado e quantizado, dizemos que ele está em um formato digital e, mais que isso, é humanamente audível, então costuma ser chamado de áudio.
O processo de amostragem "observa" o sinal do som original (analógico) com uma frequência conhecida como Frequência de Amostragem, que determina quantas observações (igualmente "espaçadas") serão feitas ao longo de um intervalo de 1 segundo. Esse processo discretiza o eixo x com valores igualmente "espaçados". O Teorema da Amostragem de Nyquist-Shannon diz que, para que um sinal amostrado possa ser perfeitamente reconstruído, a frequência de amostragem precisa ser igual ou superior ao dobro da maior frequência que compõe o sinal original. Considerando que a região espectral humanamente audível se encontra entre 20 Hz e 20 kHz, a frequência de amostragem deve ser de ao menos 40 kHz para que sinais originalmente limitados a essa região espectral possam ser perfeitamente reconstruídos. O CD utiliza 44100 Hz, então essa condição é respeitada nessa mídia. Vale lembrar que, quanto maior for a frequência de amostragem, maior será o espaço ocupado na memória para armazenar esse sinal.

O processo de quantização, por sua vez, discretiza o eixo y, fazendo com que seja adotado um limitado conjunto de possíveis valores a serem assumidos por cada amostra de áudio. O que define a quantidade de diferentes valores possíveis é a profundidade de bits de resolução. 2 bits permitem que sejam utilizados 4 valores distintos; 3 bits permitem 8 valores, 4 bits permitem 16 valores… E por aí vai. No caso do CD, são utilizados 16 bits, ou seja, cada amostra possui uma gama de 65536 diferentes valores que podem ser assumidos. Novamente, quanto maior for a profundidade de bits, melhor será a resolução do áudio, porém, maior será o espaço de memória demandado.

No caso do CD, considerando 44100 Hz de frequência de amostragem com uma profundidade de 16 bits, 705.600 bits (ou 88200 bytes) serão demandados para um único segundo de um sinal de áudio com apenas um canal. Para uma música de 5 minutos (ou 300 segundos), o total será de 26.460.000 bytes, ou seja, para cada canal de áudio serão consumidos cerca de 25,2 Megabytes. Como o CD possui 2 canais de áudio (ou seja, é Stereo), uma música ocupará 50,4 MB.

Caso desejemos analisar com base em taxa de bits, cuja unidade de medida para estes propósitos geralmente é dada em kbps (kilobits por segundo), basta considerarmos quantos kilobits são consumidos por 1 segundo desse áudio. Como são 705.600 bits por segundo para cada faixa de áudio, então a taxa de bits nesse caso será de cerca de 1411 kbps. Vale lembrar que a taxa de bits interfere na qualidade do áudio a ser ouvido, então essa medida tem relação com a qualidade da experiência do usuário ao ouvir o áudio.

Os serviços de Streaming têm total relação com este tópico em questão. Percebam que usuários de planos gratuitos costumam ter acesso a músicas com cerca de 128 kbps de taxa de bits, enquanto usuários pagantes costumam ter acesso a 256 kbps, 320 kbps ou até 1411 kbps. A bem da verdade, nem todos conseguirão aproveitar uma taxa de bits tão elevada quanto àquela utilizada em um CD (1411 kbps), pois é preciso utilizar equipamentos adequados, estar em um ambiente acusticamente favorável e também possuir um "ouvido treinado". Contudo, para a grande maioria dos usuários (não audiófilos), a música a 128 kbps já é boa o suficiente para ser ouvida e apreciada.

O MP3 não é o único formato de música comprimida existente, mas sem dúvidas é o mais famoso desde muitos anos atrás. Caso o mesmo áudio Stereo do ruído branco de 5 minutos seja comprimido utilizando-se o MP3 a uma taxa constante de 128 kbps, o resultado será um pequeno arquivo com pouco mais de 4,5 MB. Tomando como base o espaço de 50,4 MB ocupado pelo arquivo WAV, essa versão em MP3 resultou em uma compressão de aproximadamente 91% de eficiência.

Do ponto de vista de Redes de Computadores, olhar a taxa de bits pode facilitar a compreensão e a importância dessa compressão. Perceba que a largura de banda (teórica) mínima para garantir o funcionamento do serviço de Streaming deve ser superior à taxa de bits do áudio. A largura de banda extra (que vai além da taxa de bits do serviço) é necessária para utilizar adequadamente o Buffer, sendo que, quanto maior a largura de banda extra disponível (respeitando-se também os limites do servidor), mais rapidamente será preenchido o Buffer.


## Imagem

Uma imagem pode ser compreendida como uma matriz de Pixels, sendo que, considerando-se um padrão RGB (Red, Green e Blue), cada Pixel pode ser representado por um vetor de 3 posições, em que cada posição corresponde ao valor de uma camada de cor; é comum utilizar uma profundidade de bits de 8-bit, o que corresponde a serem aceitos valores inteiros entre 0 e 255 para cada uma das 3 camadas de cor em cada Pixel.

Um monitor convencional hoje em dia trabalha com o que é popularmente chamado de Full HD (ou FHD), que é o nome que o pessoal do Marketing dá para a resolução de 1920x1080. Essa resolução indica a dimensão da tal matriz de Pixels, sendo 1920 colunas e 1080 linhas. Multiplicando-se o número de linhas pelo número de colunas descobre-se que uma imagem em Full HD possui 2.073.600 Pixels. Como estão sendo considerados 8 bits para representar o valor de cada camada de cor, ou seja, 1 byte, podemos dizer que cada Pixel da imagem demanda 3 bytes; em uma imagem em Full HD isso significa 6.220.800 bytes, ou seja, cerca de 6 MB. Perceba que estamos falando de uma única imagem.


## Vídeo

No caso do vídeo, há uma imensa quantidade de imagens em movimento e pode-se ter áudio. Vamos imaginar que o vídeo esteja em Full HD e com o padrão de 24 FPS (frames per second, "quadros por segundo" em inglês), que costuma ser utilizado em filmes. Isso equivale a dizer que em cada segundo de vídeo existem 24 imagens sendo exibidas em uma sequência igualmente intervalada. Como estamos "brincando" primeiro com o caso sem compressão, vamos admitir que, assim como foi explicado na seção anterior, cada imagem ocupa 6 MB e, para fins de praticidade na explicação, admitamos que a taxa de bits do áudio WAV seja de 0,2 MB para cada segundo de áudio Stereo.

Para um filme de 2 horas (ou 7200 segundos), serão exibidas 172.800 imagens. Só as imagens consumirão 1.036.800 MB (~1 Terabyte). O áudio consumirá sozinho 1440 MB. Nota-se que, em relação ao espaço demandado, o áudio é desprezível. De qualquer forma, um filme demandaria cerca de 1 TB de espaço de armazenamento (ou de tráfego, caso fosse assistido via Streaming). Aliás, caso fosse assistido via Streaming, nem mesmo uma conexão de 1 Gbps seria suficiente para garantir que o vídeo fosse reproduzido ininterruptamente, o que significa que nenhum usuário final comum conseguiria usufruir de tal serviço, ainda que se tratasse de um filme hospedado em um servidor local, dado que as placas de rede de usuários finais costumam ser limitadas a 1 Gbps (ou até mesmo a 100 Mbps, para modelos mais antigos mas ainda existentes no mercado).

Ainda assim, quem já utilizou serviços como Netflix, YouTube e Twitch provavelmente já usufruiu de resoluções elevadas e taxas de quadros por segundo ainda maiores que as utilizadas no exemplo mencionado. Como é possível que usuários com conexões que muitas vezes mal chegam a 10 Mbps consigam consumir esses conteúdos sem sofrerem com interrupções (aquelas telas de Buffering e Loading)? Bem, um elemento fundamental disso é a justamente a compressão utilizada, garantindo uma qualidade de imagem muito boa e uma elevada fluidez nos movimentos, mas sem que o usuário dependa de uma conexão incrivelmente poderosa.


## Jogos Digitais

Se você ficou espantado com quanta informação seria processada se não existisse compressão, imagine como seria a situação de quem gosta de jogar jogos digitais por longas horas, sobretudo no caso de jogadores competitivos que fazem questão de jogar a taxas que chegam a passar dos 240 FPS, ou mesmo os Gamers que, apesar de não necessariamente fazerem questão de taxas tão elevadas, adoram resoluções elevadas, como o cada vez mais utilizado 4K (3840x2160), equivale a 4 telas Full HD em uma matriz 2x2.

Já que a ideia da brincadeira é exagerar, vamos exagerar! Que tal se o seu jogo rodasse em 4K, a 240 FPS e utilizasse um padrão RGB com 10-bit? Bem, vamos às contas.

A imagem em 4K possui 8.294.400 Pixels. Se cada Pixel demandar 30 bits, isso equivalerá a 248.832.000 bits (~237 MB) por imagem. Como estamos considerando 240 quadros por segundo, então um único segundo disso demanda um processamento de 56.880 MB (~56 GB) de informação.

Apenas para fins de ilustração desta brincadeira, vamos considerar que uma única partida de um jogo como Counter-Strike ou League of Legends dure cerca de 30 minutos (ou seja, 1800 segundos). Assim sendo, uma única partida de um desses jogos demandaria o processamento de 100.800 GB (~98 TB) de informação! Isso tudo sem incluir o Trash-talk entre os jogadores, é claro.


## Conclusões

Com base no que foi exposto ao longo do artigo, podemos notar uma parte da imensa importância da compressão nas vidas de qualquer usuário de aplicações multimídia, inclusive alguns contemporâneos e amplamente utilizados via Internet, normalmente dependentes de algum sistema de Streaming, ou mesmo jogadores de jogos digitais. Se você for usuário de qualquer um desses produtos ou serviços, lembre-se sempre de valorizar a importância da compressão de dados!