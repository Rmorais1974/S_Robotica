# Sistemas de Robótica - Introdução

A Robótica está hoje presente em praticamente em todos os setores da indústria. Desenvolver robôs com sistemas que sejam confiáveis, que propocionem uma eficiência operacional na execução das suas funções e acima de tudo trazendo segurança aos seus utilizadores, são alguns dos pontos essenciais para os diferentes projetos do setor industrial. 
Um dos pilares da Indústria 4.0 é o desenvolvimento de robôs autônomos com um comportamento inteligente e que sejam cooperativos entre si.
A Indústria 4.0 centra-se no desenvolvimento de processos mais autônomos e eficientes bem como oferecer soluções customizadas para produção e logística . 
Para que isso seja possível utilizam-se tecnologias de automação industrial juntamente com sensores. O objetivo é criar um sistema produtivo mais inteligente e ampliar a capacidade de resolução de problemas sem a necessidade de interferência humana. 
No entanto, para que isso aconteça, é essencial haver uma constante troca de informações entre todas as etapas da cadeia de produção.



## Toolbox Peter Corke

No âmbito da cadeira de Sistemas de Robótica foi proposto efectuar uma análise detalhada em Matlab com base nos modelos da toolbox do Peter Corke.
O Robotics Toolbox foi desenvolvido pelo Peter Corke e é composto por um conjunto de ferramentas para simulação de robôs manipuladores.
O Robotics Toolbox conta com vários modelos de robots comerciais pré-programados que estão disponíveis para download no github ou no site https://petercorke.com.



# Trabalho Pedido

No âmbito da cadeira de Sistemas de Robótica foi pedido para efectuar uma análise detalhada com base nos modelos da toolbox do Peter Corke.
O grupo escolheu dois modelos:
- MDL_planar2 (modelo com 2 graus de liberdade);
- Fanuc AM120IB/10l (modelo com 6 graus de liberdade).

## Descrição do Trabalho

O trabalho consite em criar uma interface gráfica para visualizar os movimentos dos dois robots, devendo ser criados vídeos demonstrativos o 
funcionamento de cada um dos robots.

## MDL_Planar2

O MDL_PLANAR2 é um script que cria a variável p2 no espaço de trabalho e descreve as características cinéticas de um simples mecanismo de ligação.
Este robot tem 2 graus de liberdade que se move tanto no eixo do XX como no eixo dos YY.


### Revolute

Uma articulação de revolute (também chamada articulação pin ou articulação de dobradiça) é um par cinemático com um grau de liberdade usado frequentemente em mecanismos e máquinas.
A articulação limita o movimento de dois corpos a uma rotação pura ao longo de um eixo comum. A junta não permite o movimento de translação nem o movimento linear deslizante. Quase todos os conjuntos de múltiplos corpos em movimento incluem as articulações revolute na sua construção. 
As juntas Revolute são utilizadas em numerosas aplicações tais como, dobradiças de porta, mecanismos e outros dispositivos de rotação de um único eixo.
Neste trabalho utilizamos duas juntas revulte que correspondem aos dois graus de liberdade.



<img src="https://user-images.githubusercontent.com/79664875/122984780-4d930280-d395-11eb-86b2-824917c15ac1.png" width="338" height="266">

### SerialLink 
A função SerialLink cria o robô utilizando os dados de cada uma das junções. 





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
t=0:0.1:2;
q1_pick=[pi/2 -pi/2];
q2_pick=[-pi/6 pi/4];
s1_pick = jtraj(q1_pick, q2_pick,t);
plot (Rob, s1_pick, 'trail',{'r','LineWidth', 2})


q3_pick = [0, -pi/2]
s2_pick = jtraj(q2_pick, q3_pick,t);
plot(Rob, s2_pick)


s3_return = jtraj(q3_pick, q1_pick,t)
plot(Rob, s3_return)


P = zeros (0,0)
input ('Calculate the Position')
q = Rob.getpos();
    
P(1) = a1*cos(q(1)) + a2*cos(q(1)+q(2));
P(2) = a1*sin(q(1)) + a2*sin(q(1)+q(2));
    
disp(P)

```

### Demonstração Modelo 1

<div class="embed-container">
  <iframe
      src="https://www.youtube.com/embed/spq3ohZLllw"
      width="960"
      height="540"
      frameborder="0"
      allowfullscreen="">
  </iframe>
</div>


## FANUC AM120IB/10l 

O Modelo Fanuc AM120iB/10L é um robot com 6 graus de liberdade que usa os parâmetros Denvait-Hartenberg 
O conjunto de poses 6-D são obtidas, dada uma gama fixa de parâmetros alcançáveis, utilizando várias técnicas de cinemática corporal rígida e dinâmica. 



<img src="https://user-images.githubusercontent.com/79664875/122179151-257c3e80-ce7f-11eb-8461-72a467d6720f.png" width="427.4" height="267"> 


### Fkine
Foward Kinematics é usado para manipular a cinemática inversa, posteriormente vai retornar a matriz de transformação homogênea final.
A cinemática direta permite determinar a posição e a orientação do end-effector em função das variáveis das juntas do robô. 
É possível realizar essa análise fixando um sistema de coordenadas em cada elo. Para fazer isso de forma sistemática, foi utilizada a os parâmetros de 
Denavit-Hartenberg (DH).
Os parâmetros de DH consistem num conjunto de quatro quantidades, que descrevem a posição e orientação de um sistema de coordenadas de um elo em relação ao
sistema de coordenadas do elo precedente ao longo da cadeia cinemática. 
Os parâmetros de DH standard são definidos como:
i – distância entre zi-1 e zi ao longo de xi;
αi – ângulo entre zi-1 e zi ao redor de xi;
di – distância entre xi-1 e xi ao longo de zi-1;
θi – ângulo entre xi-1 e xi ao redor de zi-1.
Uma vez que todas as juntas do robô são de rotação, somente os θis são variáveis.

### Ikine
A cinemática inversa representa a transformação inversa da cinemática directa. A característica principal desta transformação é o facto de 
conduzir a múltiplas soluções. 
Para manipuladores série o posicionamento num ponto (x, y, z,) arbitrário requer o mínimo de 6 graus de liberdade.

A cinemática inversa possibilita determinar as  variáveis das juntas em função da posição e orientação do end-effector. 
O conhecimento da solução do problema de cinemática inversa é indispensável para o controle  de trajetória ponto-a-ponto. Quando a posição do 
centro do end-effector não é alterada com o movimento das suas juntas, é possível utilizar o método de desacoplamento cinemático (Fig. 6), que permite 
dividir o problema da cinemática inversa em dois problemas mais simples, conhecidos, respectivamente, por cinemática inversa de posição (em função das juntas do braço), 
e cinemática inversa de orientação (em função das juntas do punho). 
Esse é o caso de nosso robô, que possui um punho esférico, no qual os eixos das suas três juntas interceptam num mesmo ponto (Fig. 5).


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

t = 0:0.15:8;
Q= jtraj(q0, qf, t);
Tr = fkine(Rob,Q);

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
      src="https://www.youtube.com/embed/W-CfknTW-2k"
      width="960"
      height="540"
      frameborder="0"
      allowfullscreen="">
  </iframe>
</div>




### Support or Contact

- João Ferreira 30002525
- Jorge Rocha 30003731
- Ricardo Morais 30002245
