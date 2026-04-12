# Relatório - Coelinhos da Páscoa

## Dados do aluno

- **Cartão UFRGS**: 00577752
- **Nome**: Elias Furtado Helfer

## Passos que eu segui para resolver o problema especificado (em formato de *"prompt"*)

Defina duas variáveis float com valor inicial 0. No loop principal do programa, incremente essas variáveis em um valor pequeno. Faça um teste para definir elas em 0 se chegarem a 2*pi. Essas duas variáveis vão definir os ângulos de movimentação dos coelhinhos e ovos. O valor de incremento altera a velocidade com a qual eles se movimentam, então experimente com diferentes valores pra descobrir o que você acha que fica melhor.

Defina uma variável com a quantidade total de coelhinhos. A partir disso, calcule o angulo de offset entre eles (quantidade total / 2*pi).

Em um laço for que itera sobre cada coelhinho, faça o seguinte:

Defina o ângulo da posição do coelinho atual com base no ângulo de movimentação global dos coelhos (definido na primeira etapa), mais o valor de offset * index do coelhinho atual. Isso faz com que os coelhinhos girem com um espaçamento entre eles.
Defina os valores x e z da movimentação do coelhinho com base no seno e cosseno do angulo do coelinho atual, e no raio desejado do circulo.
    x = raio desejado * cos(angulo atual do coelho)
    z = raio desejado * sen(angulo atual do coelho)

O valor de y é definido como uma senóide, com o ângulo multiplicado por uma constante pra aumentar a frequência da onda e outra constante multiplicando o seno para aumentar a altura da onda. 1 é somado ao seno para que o menor valor y possível do coelho seja 0 (não entre debaixo da terra).
    y = amplitude * (sen(angulo atual do coelho * frequencia) + 1)

Defina a matriz de rotação da cambalhota multiplicando o ângulo do coelho atual pela mesma constante usada para a frequência do movimento y de translação do coelho no seu eixo z. Isso faz com que a rotação coincida de forma agradável com o 'pulinho' do coelho. Pode ser adicionado um pequeno offset ao ângulo atual do coelho pra deixar o movimento ainda mais suave.

Defina a matrix de rotação da 'direção' do coelho, para que ele sempre olhe para o próximo coelho do círculo, como -(PI/2 + ângulo atual do coelho) no seu eixo y. Esse valor foi definido após experimentar com a rotação do coelho, entender a partir de que posição dele as rotações são aplicadas, e pensar para qual direção ele deveria apontar, desenhando por cima de um círculo unitário.

Aplique as transformações no coelho nessa ordem, especificamente:
    Translação * Rotação * Cambalhota (Faça apenas 1 coelho a cada 3 realizarem a cambalhota)

A cambalhota tem que ser aplicada primeiro pra não mesclar com a rotação de direção do coelho, e a translação precisa ser feita por último pras outras 2 rotações não serem feitas com base na nova posição do coelho.

Desenhe o coelho.

Para cada um dos 2 ovos, defina o ângulo de posição como o ângulo global dos ovos (definido no inicio do loop principal) + 0 e pi/2 graus, respectivamente, para fazer eles em lados opostos do círculo no qual se movimentam.

Defina as posições de translação dos ovos como:
    x = 0
    y = raio desejado * sen(angulo do ovo atual)
    y = raio desejado * cos(angulo do ovo atual)

Defina a matriz de escala do ovo como x = 0.3, y = 0.4 e z = 0.3. Isso vai deixar a esfera menor e um pouco comprida no eixo y, criando uma forma oval.
Defina a matriz de translação da órbita que os ovos fazem ao redor dos coelhos com os valores x, y e z definidos anteriormente.

Aplique as transformações nos ovos nessa ordem, especificamente:
    Translação do coelho * Rotação de direção do coelho * Translação ao redor do coelho * Escala do ovo

Desenhe o ovo.


## Principais dificuldades encontradas durante o desenvolvimento (formato livre)

Principalmente, trigonometria e achar os ângulos certos pra fazer certos movimentos. A rotação para os coelhos sempre olharem pra frente no circulo me empacou por um tempo, tive muito trial and error pra deixar como eu queria.
Nas experimentações iniciais foi meio difícil de entender em que ordem eu precisava aplicar as transformações, mas logo eu consegui montar um modelo mental de  como funciona e ficou bem intuitivo.

## Você acha que conseguiu resolver o problema de forma adequada?

Creio que sim. Fiquei orgulhoso do meu código, acho que ficou organizado e que tudo faz sentido. Me esforcei pra tentar copiar o video referência a risca, tipo fazendo o coelho sempre estar de pé quando encosta no chão durante a cambalhota, e fazer eles virados pra dentro do círculo em vez de pra fora.

## Se você quiser compartilhar mais alguma coisa, coloque aqui:

Coloquei no repositório dois vídeos engraçadinhos de movimentos inesperados que os coelhos fizeram quando eu tava experimentando. (coelhos1.webm e coelhos2.webm).

Mais detalhes sobre a implementação estão como comentários no código.

## Se você possui alguma sugestão para o professor sobre esta atividade, coloque aqui:

Achei o fato de ele ser temático de páscoa bem legal.
