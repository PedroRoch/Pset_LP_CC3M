# Pset_LP_CC3M
## Projeto Photoshop proposto por Abrantes baseado no "“MIT 6.009: Fundamentals of Programming" 

### Nome: Pedro Lucas da Rocha Barros
### Turma: CC3M
### Professor: Abrantes Araújo Silva Filho

-------------------

### Contexto 

> Este PSET é uma tradução da primeira tarefa de programação que os alunos da
> disciplina “MIT 6.009: Fundamentals of Programming” recebem logo no primeiro
> dia de aula, feita para os alunos da disciplina “Linguagens de Programação” na
> Universidade Vila Velha (UVV).

Dado a isso existem questões a serem respondidas neste Pset, em seguida vamos responder elas 

-----------------------

## Questão 1(Filtro de Inversão)

> Vamos começar com uma imagem4×1 que é definida com os seguintes parâmetros:
> 
> altura: 1
> 
> largura: 4
>
> pixels: [29, 89, 136, 200]
> 
> Se você passar essa imagem pelo filtro de inversão, qual seria o
> 
> output esperado? Justifique sua resposta

Vamos começar entendendo qual seria o calculo e o porquê dele 

c = 255 - a

(c = cor invertida | a = cor original)

Nesse cálculo, o valor da cor original é subtraído de 255, que é o valor máximo possível para uma cor em um espaço de cores de 8 bits (0-255).

A razão pela qual esse cálculo é utilizado está relacionada com a forma como as cores são representadas em sistemas digitais. Em um espaço de cores de 8 bits, cada componente de cor (vermelho, verde e azul(no nosso caso são tons de preto e branco)) é representado por um número inteiro entre 0 e 255. Um valor de 0 representa a ausência total da cor e um valor de 255 representa a cor mais intensa possível.

Ao subtrair o valor original da cor de 255, estamos invertendo o valor. Por exemplo, se o valor original for 0 (ausência de cor), a inversão será 255 (cor mais intensa). Da mesma forma, se o valor original for 255 (cor mais intensa), a inversão será 0 (ausência de cor). Isso resulta na imagem invertida em termos de cores.

Após a explicação os seguintes resultados serão 

* c = 255 - 29 = 226
* c = 255 - 89 = 166
* c = 255 - 136 = 119
* c = 255 - 200 = 55

--------------------------

## Questão 2(Debugging)

> Agora é hora de trabalhar para encontrar e corrigir os erros no código fornecido para
> o filtro de inversão. Boa depuração!

Faça a depuração e, quando terminar, seu código deve conseguir
passar em todos os testes do grupo de teste TestInvertida (incluindo especificamente o que você acabou de criar). 

Execute seu filtro de inversão na imagem
test_images/bluegill.png, salve o resultado como uma imagem PNG e salve a imagem em seu repositório GitHub.

**Resultado:**
Aplicando o Filtro da inversão conseguimos criar a seguinte imagem

*Imagem com Filtro Aplicado*

![bluegill](https://github.com/PedroRoch/Pset_LP_CC3M/assets/103005263/b4a351b8-210c-4bda-a1b1-7174bd00e76e)


*Imagem Original*

![bluegill](https://github.com/PedroRoch/Pset_LP_CC3M/assets/103005263/76ab5f93-608d-48f6-86eb-5ae817ef45a0)

-----------------------------

## Questão 3(Filtragem de imagem por correlação)

> O pessoal do nosso laboratório CSI ficou impressionado! Eles também aprenderam
> a lição e não tentarão mais codificar suas próprias ferramentas de manipulação de
> imagens. Uau!
> O laboratório agora solicitou um recurso um pouco mais avançado, envolvendo
> correlação de imagens com vários kernels.

Explicação da Questão:

considere uma etapa de correlacionar uma imagem com o seguinte kernel:

| 0.00 | -0.07 | 0.00 |
| ---: | :--- | :---: |
| -0.45 | 1.20 | -0.25 |
| 0.00 | -0.12 | 0.00 |

Aqui está uma parte de uma imagem de amostra, com as luminosidades específicas de alguns pixels:

![image](https://github.com/PedroRoch/Pset_LP_CC3M/assets/103005263/355aa077-f1cc-407d-84f6-9fe676998274)

Qual será o valor do pixel na imagem de saída no local indicado pelo destaque
vermelho? Observe que neste ponto ainda não arredondamos ou recortamos o valor, informe exatamente como você calculou. Observação: demonstre passo a passo
os cálculos realizados.

**Resultado:**

Ignorando os pixels com valor zero ao fazer a conta. Para entender o cálculo, lembre-se de onde cada pixel começa. Seguindo a definição do Kernel, começamos no canto superior esquerdo e contamos pelas linhas horizontais (x) e colunas verticais (y). O pixel central é usado como ponto de partida, e então aplicamos a fórmula de cálculo: 

Ox,y = Ix,y x K0,0

* x e y será igual a 0 
* onde x+1 andaria um pixel para a direita da imagem, x-1 andaria para a esquerda 
* y-1 para a o pixel acima e y+1 para posição abaixo)

(Vamos desconsiderar os calculos que darão o valor zero, pois será irrelevante para a resposta final)

Os seguintes calculos foram feitos para encontrar a posição dos Kernel

| Ix,y-1 x K1,0 | = -0,07 | 
| ---: | :--- |
| Ix-1,y x K0,1 | = -0.45 |
| Ix,y x K1,1 | = 1.20 |
| Ix+1,y x K2,1 | = -0.25 |
| Ix,y+1 x K1,2 | = -0.12 |

Agora pegaremos cada valor da segunda imagem e pegaremos o numero correspondente em cada posição da imagem e calcularemos 
que seria esses numeros em destaque 

![image](https://github.com/PedroRoch/Pset_LP_CC3M/assets/103005263/95c10746-ae23-478e-bbb6-d0ad8075815e)

Caso a gente também calcule os pixels das arestas, não vai mudar nada pois o valor será zero, então vamos desconsiderar 

Vamos pegar o valor do Pixel e somar com o Kernel, os seguintes calculos serão feitos: 

| 53 x -0.07 | = -3,71 |
| ---: | :--- |
| 129 x -0.45 | = -58,05 | 
| 127 x 1.20 | = 152,4 |
| 148 x -0.25 | = -37 |
| 174 x -0.12 | = -20,88 |

Agora vamos somar todos esses valores para encontrar a resposta da pergunta que queremos 

152,4 + (-3,71) + (-58,05) + (-37) +(-20,88) = 32,76 ≅ 33

**O Valor do pixel da imagem de saída no local indicado pelo destaque vermelho o número exato será de 32,76 e o valor aproximado de 33**

