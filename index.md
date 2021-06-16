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
XXXXX

# Trabalho Pedido
No ambito da cadeira de Sistemas de Robótica foi pedido para efectuar uma analise detalhada com base nos modelos da toolbox do Peter Corke.
O grupo escolheu dois modelos o modelo mdl_planar2 e o Fanuc AM120IB/10l.

## Descrição do Trabalho

 O trabalho consite em criar uma interface gráfica para visualizar os movimentos dos robôs. Também devem ser criados videos demonstrativos com a explicação e demonstração do seu funcionamento.
 
# Desenvolvimento
Vamos começar por apresentar o robot MDL_Planar 2 fazendo uma analise  dos seus movimentos, de seguida faremos o mesmo para o robot Fanuc AM120IB/10L

## MDL_Planar2

MDL_PLANAR2 é um script que cria a variável p2 no espaço de trabalho que descreve as características cinéticas de um simples mecanismo de ligação.
Este rebot é um robot com 2 graus de liberdade, que se move tanto no eixo do XX como no eixo dos YY
Também define o vetor:

qz corresponde à configuração do ângulo de articulação zero.
Também define o vetor:



### Revolute
XXXX
### SerialLink 
XXXX





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

O Modelo Fanuc AM120iB/10L é um robot com 6 graus de liberdade que usa os parametros Denvait-Hartenberg 
O conjunto de poses 6-D obtidas dada uma gama fixa de parâmetros alcançáveis, utilizando várias técnicas de cinemática corporal rígida e dinâmica. 



![image](https://user-images.githubusercontent.com/79664875/122179151-257c3e80-ce7f-11eb-8461-72a467d6720f.png)


### Fkine
XXXX

### Ikine
O metodo ikine permite é um exemplo da análise cinética de um sistema restrito de corpos rígidos, ou cadeia cinética. As equações cinéticas de um robô podem ser usadas para definir as equações de loop de um sistema articulado complexo. 


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
