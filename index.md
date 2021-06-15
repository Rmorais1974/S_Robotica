# Sistemas de Robótica - Introdução

A Robótica está hoje presente em praticamente qualquer setor industrial. Desenvolver robôs com sistemas confiáveis, e que tragam uma eficiência operacional na execução das suas funções, dando segurança aos seus utilizadores são alguns dos pontos mandatários para projetos do setor. 
Um dos pilares da Indústria 4.0 é o desenvolvimento de robôs autônomos de comportamento inteligente e cooperativo.
A Indústria 4.0 centraliza-se no desenvolvimento de processos e produtos mais autônomos e eficientes, além de oferecer soluções customizadas para produção, logística e clientes. Para que isso seja possível utilizam-se tecnologias de automação industrial juntamente com sensores. O objetivo é criar um sistema produtivo mais inteligente, e ampliar a capacidade de resolução de problemas sem a necessidade de interferência humana. Noventanto, para que isso aconteça, é mandatório haver uma constante troca de informações entre todas as etapas da cadeia de produção (KOCH et al., 2014).

## Impactos da Indústria 4.0

Ao mergulhar no significado da indústria 4.0, é impossível não pensar nos seus impactos.
Graças aos seus avanços é possível ter uma medida de como ela afeta a indústria como um todo — tanto positiva quanto negativamente.

## Impactos positivos
Ao alinhar a automação com os procedimentos de coleta e troca de dados, a adoção dos conceitos da Indústria 4.0 pode, sem dúvida, proporcionar às fábricas maior eficiência em seus processos.
A simplificação dos processos e o aumento do acesso a dados úteis ajudam a maximizar a produtividade e minimizar a quantidade de recursos usados.
Com menos dinheiro gasto em materiais e mão de obra, e menos rejeições de clientes e contratempos de fabricação, a indústria 4.0 também ajuda os fabricantes a impulsionar a produtividade e o crescimento da receita.
Outra maneira importante pela qual a Indústria 4.0 pode impactar a manufatura é promovendo interações mais próximas com os clientes.
A tecnologia, os dados e as informações que podem ajudar a transformar as operações de manufatura também podem tornar os processos e sistemas mais responsivos, tudo de acordo com as necessidades do cliente.
Os recursos exclusivos das tecnologias interconectadas permitem que os fabricantes respondam e se adaptem mais rapidamente às solicitações dos clientes.
É algo que possibilita o desenvolvimento de pedidos personalizados com menos trabalho e tempo de configuração do que na fabricação tradicional.

## Impactos negativos
Em um artigo científico escrito por acadêmicos da PUC de Curitiba, intitulado de “The impact of the fourth industrial revolution: a cross-country/region comparison”, os possíveis impactos negativos da indústria 4.0 são colocados à prova.
Dentre os os objetivos da quarta revolução industrial, um chamou a atenção dos acadêmicos de forma negativa e que, segundo eles, está em falta nas políticas públicas relacionadas ao tema:
O desenvolvimento de um sistema ou filosofia de gestão de produção que realmente ajude as empresas a lidar com o nível de demanda do futuro.
De acordo com os estudos, há uma necessidade latente de unir uma nova e transformada visão gerencial aos temas considerados pilares da indústria 4.0.

# Trabalho Pedido
No ambito da cadeira de Sistemas de Robótica foi pedido para efectuar uma analise detalhada com base nos modelos da toolbox do Peter Corke.
O grupo escolheu dois modelos o modelo mdl_planar2 e o Fanuc AM120IB/10l.

## Descrição do Trabalho

 O trabalho consite em criar uma interface gráfica para visualizar os movimentos dos robôs. Também devem ser criados videos demonstrativos com a explicação e demonstração do seu funcionamento.
 
# Desenvolvimento
Vamos começar por apresentar o robot MDL_Planar 2 fazendo uma analise profunda dos seus movimentos, de seguida faremos o mesmo para o robot Fanuc AM120IB/10L

## MDL_Planar2

MDL_PLANAR2 é um script que cria a variável p2 no espaço de trabalho que descreve as características cinéticas de um simples mecanismo de ligação.
Este rebot é um robot com 2 graus de liberdade, que se move tanto no eixo do XX como no eixo dos YY
Também define o vetor:

qz corresponde à configuração do ângulo de articulação zero.
Também define o vetor:

qz corresponde à configuração do ângulo de articulação zero.





### Código

Modelo MDL2 Planar da toolbox do Peter Corke

```markdown
a1 = 1;
a2 = 0.7;

Rob = SerialLink([
    Revolute('d', 0, 'a', a1, 'alpha', 0, 'standard')
    Revolute('d', 0, 'a', a2, 'alpha', 0, 'standard')
    ], ...
    'name', 'planar 2 link');

qz = [0 0];
t=0:0.05:2;
q1_pick=[pi/2 -pi/2];
q2_pick=[-pi/6 pi/4];
s1_pick = jtraj(q1_pick, q2_pick,t);
plot (Rob, s1_pick)


q3_pick = [0, -pi/2]
s2_pick = jtraj(q2_pick, q3_pick,t);
plot(Rob, s2_pick)


s3_return = jtraj(q3_pick, q1_pick,t)
plot(Rob, s3_return)
Rob.teach

```

### Demonstração Modelo 1

<div class="container">
  <iframe class="responsive-iframe" src="https://www.youtube.com/embed/tgbNymZ7vqY"></iframe>
</div>


## FANUC AM120IB/10l 

Fanuc AM120iB/10L, an industrial 6-DOF serial-link manipulator created in [2] using standard Denvait-Hartenberg parameters
O algoritmo de encontrar espaço de trabalho manipulador, o conjunto de poses 6-D obtidas dada uma gama fixa de parâmetros alcançáveis, é um assunto bem estudado, utilizando várias técnicas em cinemática corporal rígida e dinâmica. De acordo com o
literatura [4]-[18]. , A noção de espaço de trabalho pode ser mais longe
desenvolvidas nas seguintes subdivisões:
• Espaço de trabalho acessível: O conjunto de pontos efeitor final poderia alcançar com pelo menos uma orientação
• Espaço de trabalho de orientação total: O conjunto de pontos terminantes pode alcançar com todos os ângulos de orientação num dado dado
gama
• Espaço de trabalho dexterous: O conjunto de pontos efeitor final
poderia alcançar com todos os ângulos de orientação
• Espaço de trabalho de orientação: O conjunto de orientações que resultam
em uma localização de efeito de terminante fixo
• Espaço de trabalho de orientação constante: O conjunto de pontos termina
efetor poderia alcançar com uma orientação específica

Assim, uma ideia central das abordagens atuais é a
controlo de variáveis: desde a exibição de R
3 × SO(3) não é
possível, os constrangimentos são adicionados à parte SO(3) de modo que o
gráfico de R
3
pode ser desenhado [19]. No entanto, tal como salientado por [1],
uma questão predominante dos algoritmos atuais é que eles exigem
plataformas de software específicas e têm complexidades de mau tempo.
Uma análise feita no mesmo trabalho comentou que um MATLAB
implementação produz um O patológico(n
36) complexidade com
cinemática inversa numérica. Assim, uma solução natural vem
do campo do reconhecimento de padrões e da aprendizagem automática,
onde o problema do espaço de trabalho manipulador poderia ser reformulado para um problema de aprendizagem supervisionado, e assim ser aprendido
por uma rede neural profunda. Neste trabalho, propomos tal
quadro, visto como uma melhoria da Aprendizagem Subespacial
algoritmo em [1], onde o espaço de trabalho completo de uma ligação em série
manipulador pode ser gerado a partir da aproximação do seu Jacobiano
matriz, se existe, em um dado pose






### Código



```markdown
clear all

L(1) = Link([0 0 0.15 -pi/2 0]);
L(2) = Link([0 0 0.77 pi 0]);
L(3) = Link([0 0 0.1 -pi/2 0]);
L(4) = Link([0 -0.96 0 pi/2 0]);
L(5) = Link([0 -0.7 0 -pi/2 0]);
L(6) = Link([0 0 0 0 0]);
%##########################################################
%Pose 0; At MASTERING position;
%##########################################################

Rob=SerialLink(L, 'name', 'Fanuc AM120iB/10L');

qf = ([pi/2 0 pi/4 -pi/2 pi -pi/2]);
Tf =Rob.fkine(qf);


q0 =[-pi/2 0 pi/4 pi/4 pi -pi/2];
q =Rob.ikine(Tf, q0, 'mask',[1 1 1 1 1 1]);


for i = 1:1:length(t)
    T = Tr(i);
    trs = transl(T);
    xx (i)=trs(1);
    yy (i)=trs(2);
    zz (i)=trs(3);
end


plot3 (xx, yy, zz, 'Color',[1 0 0], 'LineWidth', 2);
hold on
plot (Rob,Q);
```


### Demonstração Modelo 2
<div class="embed-container">
  <iframe
      src="https://www.youtube.com/embed/FQPdxeEAFdg"
      width="700"
      height="480"
      frameborder="0"
      allowfullscreen="">
  </iframe>
</div>



### Support or Contact

- João Ferreira 30002525
- Jorge Rocha 30003731
- Ricardo Morais 30002245
