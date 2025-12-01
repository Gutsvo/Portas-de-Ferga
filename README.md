<h1 align="center"><b>Portas de Ferga</b></h1>
    <h3><i>Gustavo da Silva Rezende, João Paulo Barbosa Pereira de Carvalho Filho, Lucas Soares de Araujo, Matheus Henrique Galindo Campos e Murilo Rangel de França</i></h3>
    <h3><i>Link para o Drive da cena: </i></h3> https://drive.google.com/drive/folders/1l6MziIimAuKmb7dXMFyyZSNOi2LW5CVT?usp=sharing
<br>

<h1 align="center"><b>Scripts</b></h1>
  <h2><b>ThirdPersonController</b></h2>

 <img width="756" height="677" alt="image" src="https://github.com/user-attachments/assets/18518893-3688-4f68-a304-0cad2b1fdb75" />
 <img width="1028" height="712" alt="image" src="https://github.com/user-attachments/assets/56894a56-0d8c-40ac-a1b6-381b11539be6" />
 <img width="784" height="613" alt="image" src="https://github.com/user-attachments/assets/a50f3172-4656-4dff-900e-dcbdd0e16968" />
 <img width="899" height="714" alt="image" src="https://github.com/user-attachments/assets/d0f6ffad-0bae-44f8-b8a2-fa65c0c4d597" />
 <img width="904" height="758" alt="image" src="https://github.com/user-attachments/assets/d0579b63-f3df-4ee3-b45f-d92ad0044006" />
 <img width="721" height="436" alt="image" src="https://github.com/user-attachments/assets/d3b0d5d1-a436-4877-843b-b78cd5ec40a1" />
      <div align="justify">Código da movimentação do player, código explicado através de comentários.</div>

  <h2><b>CameraController</b></h2>

  <img width="1289" height="689" alt="image" src="https://github.com/user-attachments/assets/f4ae8d65-1f0a-4084-9f93-aee90c26bb1c" />
  <img width="861" height="501" alt="image" src="https://github.com/user-attachments/assets/45cabdc1-dca2-4724-99bf-3ce74ff09e87" />
      <div align="justify">Código da câmera em 3º pessoa que automáticamente segue o player, código explicado através de comentários.</div>

  <h2><b>Estilingue</b></h2>

  <img width="586" height="613" alt="image" src="https://github.com/user-attachments/assets/fac300fe-1482-4755-a0d9-0d21408b7727" />
      <div align="justify">Esse trecho do código declara todas as variáveis usadas para controlar o disparo de um projétil, o cálculo da trajetória e os ajustes no comportamento do jogador durante o ato de mirar.

Na primeira parte, <b>Projectile Settings</b>, ficam as configurações do disparo: o prefab do projétil, o ponto de onde ele será lançado, os valores mínimo e máximo de força, a velocidade com que essa força é carregada ao segurar o botão, e o tempo de recarga entre um tiro e outro. Em seguida, em <b>Trajectory</b>, estão as variáveis responsáveis por desenhar a linha de previsão da trajetória com um <b>LineRenderer</b>, definindo quantos pontos essa linha terá e o intervalo de tempo usado para calcular cada ponto.
      
Depois, em <b>References</b>, o script guarda referências ao controlador do jogador e ao controlador da câmera, além de um multiplicador usado para reduzir a velocidade do personagem enquanto ele mira. Por fim, há variáveis privadas que o código usa internamente: <b>currentForce</b> para armazenar a força sendo carregada, <b>isAiming</b> para indicar se o jogador está mirando, <b>cooldownTimer</b> para controlar o tempo de recarga e <b>originalSpeed</b> para guardar a velocidade normal do personagem antes de ser reduzida durante a mira.</div>
      
 <img width="678" height="591" alt="image" src="https://github.com/user-attachments/assets/2231ced9-3fcf-4f81-beeb-afdb124daf16" />
     <div align="justify">Esse trecho define o comportamento inicial do sistema e o que acontece a cada frame.

No <b>Start()</b>, o script define que a força atual do tiro começa no valor mínimo (currentForce = minForce) e registra a velocidade original do jogador para poder restaurá-la depois (originalSpeed = playerController.velocity). Se a linha de trajetória existir, ele ajusta a quantidade de pontos que ela terá e a deixa desativada até que o jogador comece a mirar.

No <b>Update()</b>, que roda continuamente, o temporizador de recarga do tiro é reduzido com base no tempo real (cooldownTimer -= Time.deltaTime). Depois disso, o script responde aos inputs do mouse: quando o botão esquerdo é pressionado pela primeira vez, inicia o modo de mira (StartAiming()); enquanto ele permanece pressionado, a força do disparo é carregada (ChargeShot()); e quando o botão é solto, o disparo é executado (ReleaseShot()).</div>
 <img width="794" height="529" alt="image" src="https://github.com/user-attachments/assets/24a16475-6b32-4efc-a9e0-d1bd83231bad" />
     <div align="justify">Esse trecho controla o início da mira e o carregamento do disparo.

<b>StartAiming()</b> é chamado quando o jogador aperta o botão de tiro. Primeiro, o código verifica se ainda existe tempo de recarga — se houver, simplesmente não deixa mirar. Caso contrário, ativa o modo de mira (isAiming = true) e reinicia a força do disparo no valor mínimo. Em seguida, reduz a velocidade do jogador multiplicando a velocidade original pelo fator de lentidão usado ao mirar. Se a linha de trajetória estiver configurada, ela é ativada para começar a mostrar a previsão do tiro.

<b>ChargeShot()</b> roda enquanto o jogador mantém o botão pressionado. O método só funciona se o modo de mira estiver ativo; caso não esteja, ele sai imediatamente. Se estiver mirando, a força do disparo aumenta gradualmente com base na velocidade de carregamento e no tempo real (chargeSpeed * Time.deltaTime). Depois, essa força é limitada para nunca passar dos valores mínimo e máximo. Por fim, o método chama <b>DisplayTrajectory()</b>, que atualiza visualmente o desenho da trajetória prevista usando o <b>LineRenderer</b>.</div>
 <img width="1044" height="522" alt="image" src="https://github.com/user-attachments/assets/9665fc10-a1bc-4761-ba2c-a8f45848f5cc" />
     <div align="justify">Esse trecho define o que acontece quando o jogador solta o botão do mouse e dispara o projétil.

<b>ReleaseShot()</b> só executa se o jogador realmente estiver mirando; caso contrário, ele ignora a ação. Quando o tiro é liberado, o modo de mira é encerrado (isAiming = false), o tempo de recarga é reiniciado (cooldownTimer = shotCooldown) e o método <b>FireProjectile()</b> é chamado para criar e lançar o projétil. Depois disso, a velocidade do jogador é ajustada de volta para um valor fixo (no caso, 5f). Por fim, se a linha da trajetória estiver ativa, ela é desativada novamente, já que o jogador não está mais mirando.

<b>FireProjectile()</b> é o método responsável por criar e lançar o projétil. Ele instancia o prefab do projétil no ponto de disparo (shootPoint.position e shootPoint.rotation). Em seguida, pega o <b>Rigidbody</b> do projétil e aplica uma velocidade inicial baseada na direção para a qual o ponto de disparo está apontando (shootPoint.forward) multiplicada pela força carregada (currentForce). Isso faz com que o projétil seja lançado na direção correta com intensidade proporcional ao carregamento do tiro.</div>

 <img width="922" height="359" alt="image" src="https://github.com/user-attachments/assets/8595509e-f065-492a-8512-76e3ab2863fc" />
     <div align="justify">Esse trecho calcula e desenha a trajetória prevista do projétil enquanto o jogador está mirando.

O método <b>DisplayTrajectory()</b> só executa se houver um <b>LineRenderer</b> configurado. Ele começa definindo duas variáveis: a posição inicial do tiro (startPos), que é o ponto de disparo, e a velocidade inicial (startVel), que é a direção do disparo multiplicada pela força atualmente carregada.

Dentro do loop, que percorre todos os pontos definidos para a linha da trajetória, o código calcula o instante de tempo correspondente a cada ponto (t = i * timeStep). Em seguida, determina a posição daquele ponto aplicando a fórmula da movimentação com aceleração constante:

* posição inicial

* mais a velocidade inicial multiplicada pelo tempo

* mais metade da gravidade multiplicada pelo tempo ao quadrado

Esse cálculo cria uma curva parabólica realista baseada na física. Cada ponto calculado é então aplicado ao LineRenderer usando trajectoryLine.SetPosition(i, point), fazendo a linha desenhar a trajetória prevista do projétil conforme a força aumenta.</div>


  <h2><b>Bala</b></h2>

  <img width="685" height="395" alt="image" src="https://github.com/user-attachments/assets/0ea164fb-80c0-4eac-b5d3-eee5bd890811" />
      <div align="justify">Aqui é instanciado um efeito sonóro e as partículas que serão ativadas, e dita um delay para a destruição do gameObject carregando o script. Quando a cena começar, seta o necessário para o áudio funcionar.</div>
      
  <img width="924" height="617" alt="image" src="https://github.com/user-attachments/assets/0f7f9857-dd3e-4c9a-8076-506c465e6a7d" />
     <div align="justify">Quando a "Bala" colidir com algo, irá tocar os efeitos sonóros e gerar as partículas e destrói o gameObject após o tempo anteriormente instanciado.</div>


  <h2><b>Derrubaveis</b></h2>

  <img width="649" height="649" alt="image" src="https://github.com/user-attachments/assets/aff1411f-4b72-4633-a823-663dd7d005fc" />
    <div align="justify">Nesse código, é selecionado 2 gameObjects que terão seus estados de ativação alternados. Após o gameObject "objectToDeactivate" ser acertado um número alterável de vezes (com 3 sendo o número base) por um gameObject com a tag "Bala", seu estado será setado como "false" e o gameObject "objectToActivate" terá seu estado setado para "true", criando um efeito de ação e efeito usado no jogo para criar a ilusão de que algo foi derrubado ao ser acertado por balas.</div>

  <h2><b>Vidas</b></h2>

  <img width="524" height="774" alt="image" src="https://github.com/user-attachments/assets/673f64f2-356a-493c-91e7-59617f0a8c39" />
      <div align="justify">Esse trecho controla todo o sistema de vida da jogadora, incluindo o dano recebido e o que acontece quando a vida chega a zero.

A variável maxHealth define a quantidade máxima de vida, enquanto currentHealth armazena a vida atual. No Awake(), o script inicializa a vida atual com o valor máximo e garante que o menu de morte esteja desativado no início do jogo.

O método TakeDamage(int damage) é chamado sempre que a jogadora sofre dano. Ele reduz a vida atual pelo valor recebido e verifica se a vida chegou a zero ou menos. Se isso acontecer, chama o método Die().

No método Die(), o jogo é congelado definindo Time.timeScale = 0f, e o menu de morte é ativado se ele tiver sido atribuído. Por fim, um texto é exibido no console informando que a protagonista morreu. Esse método lida com toda a lógica de fim de jogo ao perder toda a vida.</div>

  <h2><b>Coelho</b></h2>

  <img width="957" height="802" alt="image" src="https://github.com/user-attachments/assets/dab5969e-1a19-4623-b774-6c456384b895" />
      <div align="justify">Esse trecho inicial organiza todas as variáveis e referências essenciais para o funcionamento da IA do inimigo. Na seção References, o script guarda o NavMeshAgent, usado para movimentação via navegação, e a referência ao jogador, que é o alvo que o inimigo deve perseguir ou atacar.

Na parte de Vida do inimigo, o script define a vida máxima (maxHealth) e a vida atual (currentHealth), que será usada para controlar quando o inimigo deve morrer.

A seção Pontos fracos (Triggers de Dano) armazena um array de objetos que representam partes vulneráveis do inimigo. Esses objetos são usados para detectar acertos e causar dano.

Em Ataque Corpo-a-Corpo, o script define o alcance do ataque melee, o dano causado, o tempo de recarga entre ataques e uma flag (canMelee) para controlar se o inimigo pode atacar novamente.

Em Ataque à Distância, são declarados o tempo entre ataques, a flag que detecta se o inimigo já realizou um ataque e o prefab do projétil que ele pode disparar.

No Awake(), o script verifica se o jogador foi atribuído no Inspector; se não, mostra um aviso e tenta encontrá-lo automaticamente com GameObject.Find("Amelie"). Em seguida, obtém o NavMeshAgent do próprio objeto e inicializa a vida atual com o valor máximo. Essa etapa garante que todas as referências essenciais estejam prontas antes da lógica de IA começar a rodar.</div>

 <img width="859" height="668" alt="image" src="https://github.com/user-attachments/assets/0605de85-4077-488b-a9fb-3ad47a3fa923" />
     <div align="justify">Esse trecho controla o comportamento básico do inimigo durante o jogo, especificamente seguir o jogador e realizar ataques corpo-a-corpo quando estiver perto o suficiente.

No Update(), duas ações principais acontecem continuamente: o inimigo segue o jogador e verifica se pode realizar um ataque melee.

O método FollowPlayer() ordena ao NavMeshAgent que se mova em direção à posição atual do jogador usando SetDestination(), garantindo que o inimigo esteja sempre tentando se aproximar.

Já o método CheckMeleeAttack() calcula a distância entre o inimigo e o jogador. Se essa distância for menor ou igual ao alcance definido (meleeRange) e o inimigo estiver apto para atacar (canMelee), o jogador recebe dano chamando TakeDamage(meleeDamage). Após atacar, o inimigo fica impossibilitado de atacar novamente, definindo canMelee = false, e um Invoke() agenda a chamada de ResetMelee(), que reativa o ataque após o tempo de recarga (meleeCooldown).

Por fim, ResetMelee() simplesmente redefine a flag canMelee para true, permitindo que o inimigo volte a atacar corpo-a-corpo após o intervalo necessário.</div>

 <img width="1228" height="697" alt="image" src="https://github.com/user-attachments/assets/dd6ab1cd-fa14-4563-a3fd-0994878c5692" />
     <div align="justify">Esse trecho controla o ataque à distância do inimigo e também o sistema de dano que ele recebe.

O método AttackPlayer() interrompe a movimentação do inimigo usando agent.SetDestination(transform.position) e garante que ele fique virado para o jogador com transform.LookAt(player). Assim, o inimigo para no lugar e mira corretamente antes de disparar.

Se o inimigo ainda não atacou recentemente (!alreadyAttacked), ele instancia um projétil no ponto onde está e obtém seu Rigidbody. Em seguida, aplica duas forças: uma para frente, para impulsionar o projétil na direção do jogador, e outra para cima, criando uma leve curvatura no lançamento. Depois do disparo, marca que o ataque já foi realizado (alreadyAttacked = true) e usa Invoke() para chamar ResetAttack() após o tempo de recarga definido, liberando o inimigo para atacar novamente.

ResetAttack() simplesmente redefine a flag alreadyAttacked para false, permitindo outro ataque à distância depois do intervalo configurado.

Por último, TakeDamage(int amount) controla a vida do inimigo. O método reduz a vida atual pelo valor recebido e, se ela chegar a zero ou menos, agenda a destruição do inimigo com um pequeno atraso chamando DestroyEnemy() após 0,5 segundos. Esse atraso costuma ser usado para animações ou efeitos de morte antes da remoção completa do obj</div>

 <img width="763" height="603" alt="image" src="https://github.com/user-attachments/assets/5bde7b9d-5102-41ea-af37-9ce5e7af44fd" />
     <div align="justify">Esse trecho final lida com a destruição do inimigo, a detecção de dano causado por projéteis do jogador e a consulta à vida atual.

O método DestroyEnemy() é simples: ele apenas remove o inimigo da cena usando Destroy(gameObject), sendo chamado após o inimigo perder toda a vida.

No OnCollisionEnter(), o script verifica se o objeto que colidiu possui a tag "Bala". Se não tiver, o método termina imediatamente, ignorando colisões irrelevantes. Caso seja uma bala, o código percorre todos os objetos definidos como pontos fracos (damageTriggers). Se o objeto que colidiu for exatamente um desses triggers, o inimigo recebe 1 ponto de dano chamando TakeDamage(1), e o loop é interrompido para evitar múltiplos danos na mesma colisão.

Por fim, GetCurrentHealth() simplesmente retorna o valor de currentHealth, fornecendo uma forma segura de acessar a vida atual do inimigo a partir de outros scripts.</div>


  <h2><b>TriggerDano</b></h2>

  <img width="934" height="355" alt="image" src="https://github.com/user-attachments/assets/361e8eb6-16b7-4879-a2c0-86bbbe33621e" />
    <div align="justify">Um código para que: ao objeto ccom o código ser acertado, o boss "Coelho" levará dano.</div>

  <h2><b>BoladeFogo</b></h2>

  <img width="785" height="643" alt="image" src="https://github.com/user-attachments/assets/9c0dbc26-fe76-4c17-81ea-451f80c9aa8f" />
    <div align="justify">Esse trecho define o comportamento de um projétil disparado por um inimigo, controlando sua movimentação inicial e o efeito ao colidir com o jogador.

Na parte de Movimentação, a variável speed determina a velocidade com que o projétil será lançado. No método Start(), o script obtém o componente Rigidbody do próprio objeto e define sua velocidade inicial usando a direção do projétil (transform.forward * speed), fazendo com que ele comece a se mover imediatamente após ser criado.

Na parte de Dano, a variável damage representa quanto de vida o projétil deve retirar do jogador caso o atinja.

Quando ocorre uma colisão, o método OnCollisionEnter é chamado. Ele verifica se o objeto atingido possui a tag "Player" e, se isso for verdade, acessa o componente Vidas do jogador para aplicar o dano usando TakeDamage(damage). Independentemente do tipo de objeto atingido, o projétil é destruído logo após o impacto usando Destroy(gameObject), garantindo que ele não permaneça no cenário após a colisão.</div>
