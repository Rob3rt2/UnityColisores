# Unity Colisores - LP & HUD e Menu

 #### Unity Colisores 
Esse projeto é um jogo criado na Game Engine Unity. O jogo apresenta um cenário onde o player se vê em um labirinto e terá que chegar ao fim.
Como objetivo da atividade, o mapa possui tipos de colisores passados em aula, como: 

- Static Collider
- Rigidbody Collider
- Kinematic Rigidbody Collider
- Static Trigger Collider
- Rigidbody Trigger Collider
- Kinematic Rigidbody Trigger Collide

 #### HUD e MENU
Também, complementando a cena como objetivo do trabalho passado em sala de aula, recentemente **adicionando o HUD (Heads-Up Display) e o MENU do nosso game.** (Disponibilizado todo o passoa passo no fim desse README)
##

# Criadores
**Aluna:** Letícia da Lapa 

**Aluno:** Robert Caio Gomes

**Cursando:** ETEC Professor Basilídes de Godoy - Ensino Médio Integrado ao Curso Técnico de Programação de Jogos Digitais. 2ºA/2023

# Requisitos
Para ver essa cena, é preciso o Unity com a versão 2022.2.16f1
# Instalação
1. Clonar o projeto (Pasta está zipada para preservação do projeto construído na Unity, possuindo Scripts no C# e o projeto da Unity).
- Link da pasta no Drive : https://drive.google.com/drive/folders/11ySoPMGxFu0ajMC4tXVKVN6qu7mjuMVf?usp=drive_link
2. Assistir Gameplay disponível no Youtube.
  
##### Gameplay

- Link do Youtube com Colisores: https://youtu.be/SJmjQH2aDbo 
- Link do Youtube com HUD, Menu e Créditos: https://youtu.be/eeVRxJh-vqk
3. Abrir o projeto no Unity.
  
# Desenvolvimento - Assets 

Para criar esse projeto foram utilizados os seguintes passos:
1. Baixar assets na Assets Store Unity.

Foram apenas utilizados Assets para movimentação e SkyBox. 
- Asset para movimentação do player.

![Movimentação UNITY](https://github.com/Rob3rt2/UnityColisores/assets/128638269/63d2107d-5b20-4cd2-8f7a-1dca1870e3c4)

- Asset para SkyBox da cena.

![Skybox UNITY](https://github.com/Rob3rt2/UnityColisores/assets/128638269/5bfac898-cca7-4e4d-bdef-b4e01569ffe1)

# Controlador de Câmera
Este script fornece um controlador de câmera no Unity que permite movimento suave e controlado da câmera com base na entrada do mouse. Ele permite que o jogador rotacione a câmera verticalmente e o personagem horizontalmente.

![Camera INIT](https://github.com/Rob3rt2/UnityColisores/assets/128638269/e759042e-9eb6-4b95-8df8-684448ca55d4)

# Recursos
- Rotação vertical da câmera com limite máximo de ângulo

- Rotação horizontal do personagem

- Funcionalidade de bloquear e desbloquear o cursor

- Rotação suave da câmera com base na entrada do mouse

# Como Utilizar:
1. Anexe o script CameraController ao objeto da câmera em sua cena do Unity.

2. Atribua o transform da câmera à variável cameraTransform no script.

3. Especifique o ângulo vertical máximo que a câmera pode rotacionar no campo maxVerticalAngle.

4. Atribua o transform do personagem à variável body no script.

5. Ajuste a sensibilidade da rotação da câmera modificando o campo sensitivity.

6. Execute o jogo e controle a câmera movendo o mouse.

#Explicação do Script

csharp

using System;

using System.Collections;

using System.Collections.Generic;

using UnityEngine;

public class CameraController : MonoBehaviour

{

public Transform cameraTransform;

public float maxVerticalAngle;

public Transform body;

// Variáveis privadas

private float _mouseVerticalValue;

private float MouseVerticalValue

{

get => _mouseVerticalValue;

set

{

if (value == 0) return;

float verticalAngle = _mouseVerticalValue + value;

verticalAngle = Mathf.Clamp(verticalAngle, -maxVerticalAngle, maxVerticalAngle);

_mouseVerticalValue = verticalAngle;

}

}

public float sensitivity;

// O método Update é chamado uma vez por quadro

void Update()

{

// Captura o movimento vertical do mouse

MouseVerticalValue = Input.GetAxis("Mouse Y");

// Calcula a rotação desejada com base no movimento vertical

Quaternion finalRotation = Quaternion.Euler(

-MouseVerticalValue * sensitivity,

0, 0);

// Aplica a rotação à câmera

cameraTransform.localRotation = finalRotation;

// Rotaciona o personagem horizontalmente com base no movimento do mouse

body.rotation = Quaternion.Euler(

0,

body.localRotation.eulerAngles.y + Input.GetAxis("Mouse X") * sensitivity,

0);

// Bloqueia o cursor e o esconde quando o botão esquerdo do mouse é pressionado

if (Input.GetMouseButtonDown(0))

{

Cursor.lockState = CursorLockMode.Locked;

Cursor.visible = false;

}

// Desbloqueia o cursor e o mostra quando a tecla Esc é pressionada

if (Input.GetKeyDown(KeyCode.Escape))

{

Cursor.lockState = CursorLockMode.None;

Cursor.visible = true;

}

}

}

O script consiste nos seguintes componentes principais: 

- **Variáveis *Públicas*:** Essas variáveis podem ser configuradas no Editor do Unity e permitem a personalização do comportamento do controlador de câmera. Elas incluem cameraTransform (o transform da câmera), maxVerticalAngle (o ângulo máximo que a câmera pode rotacionar verticalmente), body (o transform do personagem) e sensitivity (a sensibilidade da rotação da câmera).
- **Variáveis *Privadas*:** Essas variáveis são usadas internamente pelo script para controlar o movimento vertical do mouse. _mouseVerticalValue armazena o valor acumulado da rotação vertical, e MouseVerticalValue é uma propriedade que garante que a rotação vertical fique dentro dos limites especificados.
- ***Update*():** Este método é chamado a cada quadro e lida com as atualizações da câmera e entrada do usuário. Ele captura o movimento vertical do mouse, calcula a rotação desejada com base na entrada do mouse e aplica a rotação à câmera e ao personagem. Também verifica a entrada dos botões do mouse e do teclado para bloquear ou desbloquear o cursor e alterar sua visibilidade.Física CC
Este script implementa um controlador de personagem físico no Unity, usando o componente CharacterController. Ele lida com a movimentação do personagem, verificação de colisões e interação com plataformas.

# Recursos:
- Verificação de contato com o solo e cálculo do ângulo do terreno

- Movimentação suave em superfícies inclinadas

- Aplicação de gravidade

- Damping de inércia para desacelerar o personagem em movimento

- Interação com plataformas móveis

- Detecção de colisões e aplicação de força

# Como usar:
1. Anexe o script PhysicalCC a um objeto no Unity que possua o componente CharacterController.

2. Personalize os parâmetros no inspector, conforme necessário.

3. Execute o jogo e observe o comportamento do personagem.

# Descrição do Script:
csharp

using System.Collections;

using UnityEngine;

[RequireComponent(typeof(CharacterController))]

public class PhysicalCC : MonoBehaviour

{

public CharacterController cc { get; private set; }

private IEnumerator dampingCor;

[Header("Verificação do Solo")]

public bool isGround;

public float groundAngle;

public Vector3 groundNormal { get; private set; }

[Header("Movimentação")]

public bool ProjectMoveOnGround;

public Vector3 moveInput;

private Vector3 moveVelocity;

[Header("Inércia e Inclinação")]

public float slopeLimit = 45;

public float inertiaDampingTime = 0.1f;

public float slopeStartForce = 3f;

public float slopeAcceleration = 3f;

public Vector3 inertiaVelocity;

[Header("Interação com Plataforma")]

public bool platformAction;

public Vector3 platformVelocity;

[Header("Colisão")]

public bool applyCollision = true;

public float pushForce = 55f;

private void Start()

{

cc = GetComponent();

}

private void Update()

{

GroundCheck();

if (isGround)

{

moveVelocity = ProjectMoveOnGround ? Vector3.ProjectOnPlane(moveInput, groundNormal) : moveInput;

if (groundAngle < slopeLimit && inertiaVelocity != Vector3.zero) InertiaDamping();

}

GravityUpdate();

Vector3 moveDirection = (moveVelocity + inertiaVelocity + platformVelocity);

cc.Move((moveDirection) * Time.deltaTime);

}

private void GravityUpdate()

{

if (isGround && groundAngle > slopeLimit)

{

inertiaVelocity += Vector3.ProjectOnPlane(groundNormal.normalized + (Vector3.down * (groundAngle / 30)).normalized * Mathf.Pow(slopeStartForce, slopeAcceleration), groundNormal) * Time.deltaTime;

}

else if (!isGround) inertiaVelocity.y -= Mathf.Pow(3f, 3) * Time.deltaTime;

}

private void InertiaDamping()

{

var a = Vector3.zero;

// desaceleração da inércia quando a força do movimento é aplicada

var resistanceAngle = Vector3.Angle(Vector3.ProjectOnPlane(inertiaVelocity, groundNormal),

Vector3.ProjectOnPlane(moveVelocity, groundNormal));

resistanceAngle = resistanceAngle == 0 ? 90 : resistanceAngle;

inertiaVelocity = (inertiaVelocity + moveVelocity).magnitude <= 0.1f ? Vector3.zero : Vector3.SmoothDamp(inertiaVelocity, Vector3.zero, ref a, inertiaDampingTime / (

3 / (180 / resistanceAngle)));

}

private void GroundCheck()

{

if (Physics.SphereCast(transform.position, cc.radius, Vector3.down, out RaycastHit hit, cc.height / 2 - cc.radius + 0.01f))

{

isGround = true;

groundAngle = Vector3.Angle(Vector3.up, hit.normal);

groundNormal = hit.normal;

if (hit.transform.tag == "Platform")

platformVelocity = hit.collider.attachedRigidbody == null | !platformAction ?

Vector3.zero : hit.collider.attachedRigidbody.velocity;

if (Physics.BoxCast(transform.position, new Vector3(cc.radius / 2.5f, cc.radius / 3f, cc.radius / 2.5f),

Vector3.down, out RaycastHit helpHit, transform.rotation, cc.height / 2 - cc.radius / 2))

{

groundAngle = Vector3.Angle(Vector3.up, helpHit.normal);

}

}

else

{

platformVelocity = Vector3.zero;

isGround = false;

}

}

private void OnControllerColliderHit(ControllerColliderHit hit)

{

if (!applyCollision) return;

Rigidbody body = hit.collider.attachedRigidbody;

// verificar rigidbody

if (body == null || body.isKinematic) return;

Vector3 pushDir = hit.point - (hit.point + hit.moveDirection.normalized);

// aplicar força de empurrão

body.AddForce(pushDir * pushForce, ForceMode.Force);

}

}

O script consiste nos seguintes componentes principais:

- **Variáveis *Públicas*:** Essas variáveis podem ser configuradas no Editor do Unity e controlam o comportamento do controlador de personagem físico. Elas incluem cc (uma referência ao CharacterController), isGround (uma flag indicando se o personagem está no chão), groundAngle (o ângulo do terreno), groundNormal (o vetor normal do terreno), moveInput (o input de movimento), slopeLimit (o limite de inclinação em que o personagem pode se mover), inertiaDampingTime (o tempo de desaceleração da inércia), slopeStartForce (a força inicial ao subir uma rampa) e applyCollision (uma flag indicando se a colisão deve ser aplicada).

- **Métodos *Update()* e *GravityUpdate()*:** O método Update() é chamado a cada quadro e lida com a movimentação do personagem. Ele chama outros métodos para verificar o contato com o solo, atualizar a gravidade, aplicar a inércia e interagir com plataformas. O método GravityUpdate() calcula a força de gravidade aplicada ao personagem com base na inclinação do terreno.

- **Métodos *InertiaDamping()* e *GroundCheck()*:** O método InertiaDamping() desacelera a inércia do personagem quando uma força de movimento é aplicada. O método GroundCheck() verifica se o personagem está no chão, calcula o ângulo do terreno e armazena o vetor normal do terreno.

- **Método *OnControllerColliderHit()*:** Esse método é chamado quando o controlador de personagem colide com outro objeto. Ele verifica se há uma colisão aplicável e adiciona uma força de empurrão ao objeto colidido.

# Entrada do Player 
![CENA](https://github.com/Rob3rt2/UnityColisores/assets/128638269/69d2cf03-39e3-4f33-8097-191333dce8be)

Este script controla a entrada do jogador no Unity. Ele lida com o movimento do jogador, saltos e ação de sentar-se.

# Recursos:

- Movimento suave baseado na entrada do jogador

- Salto controlado pelo pressionamento da tecla de espaço

- Ação de sentar-se ao pressionar a tecla C

# Como usar:
1. Anexe o script PlayerInput a um objeto no Unity que represente o jogador.

2. Certifique-se de ter um componente PhysicalCC anexado ao objeto do jogador.

3. Atribua a referência do componente PhysicalCC à variável physicalCC no inspector.

4. Opcionalmente, configure as variáveis speed (velocidade do jogador) e jumpHeight (altura do salto) no inspector.

5. Se necessário, ajuste a variável bodyRender para a renderização do corpo do jogador no inspector.

6. Execute o jogo e teste o movimento, saltos e ação de sentar-se do jogador.

# Descrição do Script

csharp

using System.Collections;

using UnityEngine;

public class PlayerInput : MonoBehaviour

{

public float speed = 5;

public float jumpHeight = 15;

public PhysicalCC physicalCC;

public Transform bodyRender;

private IEnumerator sitCort;

private bool isSitting;

private void Update()

{

if (physicalCC.isGround)

{

physicalCC.moveInput = Vector3.ClampMagnitude(transform.forward * Input.GetAxis("Vertical") +

transform.right * Input.GetAxis("Horizontal"), 1f) * speed;

if (Input.GetKeyDown(KeyCode.Space))

{

physicalCC.inertiaVelocity.y = 0f;

physicalCC.inertiaVelocity.y += jumpHeight;

}

if (Input.GetKeyDown(KeyCode.C) && sitCort == null)

{

sitCort = sitDown();

StartCoroutine(sitCort);

}

}

}

private IEnumerator sitDown()

{

if (isSitting && Physics.Raycast(transform.position, Vector3.up, physicalCC.cc.height * 1.5f))

{

sitCort = null;

yield break;

}

isSitting = !isSitting;

float t = 0;

float startSize = physicalCC.cc.height;

float finalSize = isSitting ? physicalCC.cc.height / 2 : physicalCC.cc.height * 2;

Vector3 startBodySize = bodyRender.localScale;

Vector3 finalBodySize = isSitting ? bodyRender.localScale - Vector3.up * bodyRender.localScale.y / 2f : bodyRender.localScale + Vector3.up * bodyRender.localScale.y;

speed = isSitting ? speed / 2 : speed * 2;

jumpHeight = isSitting ? jumpHeight * 3 : jumpHeight / 3;

while (t < 0.2f)

{

t += Time.deltaTime;

physicalCC.cc.height = Mathf.Lerp(startSize, finalSize, t / 0.2f);

bodyRender.localScale = Vector3.Lerp(startBodySize, finalBodySize, t / 0.2f);

yield return null;

}

sitCort = null;

yield break;

}

}

O script consiste nos seguintes componentes principais:

- **Variáveis *Públicas*:** Essas variáveis podem ser configuradas no Editor do Unity e controlam o comportamento da entrada do jogador. Elas incluem speed (velocidade do jogador)
e jumpHeight (altura do salto). A variável physicalCC deve ser atribuída com uma referência ao componente PhysicalCC que lida com a física do personagem.

- **Variáveis *Privadas*:** Essas variáveis são usadas internamente pelo script para controlar a ação de sentar-se. A variável bodyRender é opcional e pode ser configurada para a renderização do corpo do jogador.

- **Método *Update()*:** O método Update() é chamado a cada quadro e lida com a entrada do jogador. Se o jogador estiver no chão, a entrada é usada para controlar o movimento do jogador e o salto. O movimento é definido em physicalCC.moveInput e o salto é ativado definindo physicalCC.inertiaVelocity.y como a altura do salto.

- **Método *sitDown()*:** O método sitDown() é uma rotina que lida com a ação de sentar-se do jogador. Ele ajusta a altura do personagem e a escala do corpo gradualmente para criar uma animação suave. A velocidade e altura do salto também são ajustadas com base no estado de sentar-se.

# SkyBox
Adicionamos um Asset para personalizarmos o ambiente. 

![SKYBOX](https://github.com/Rob3rt2/UnityColisores/assets/128638269/ac216d12-93e7-43a6-921f-b0fe601150f0)

# Adicionando os Colisores 
A aplicação dos colisores é o tema principal do nosso projeto. Utilizamos eles adicionando alguns objetos em nossa cena, que a seguir vamos mostrar.
- Script de declaração de código.

![SCRIPT DE DECLARAÇAO](https://github.com/Rob3rt2/UnityColisores/assets/128638269/dc73eb29-48e6-41b7-846b-b757dea2958e)

# Static Collider
Em primeiro plano, vamos abordar sobre o Static Collider. Muito utilizado para a criação do cenário, o colisor estático foi adicionado nas paredes e chão do ambiente. O Static Collider é usados para criar uma geometria de nível para que sempre permaneça no mesmo lugar, não possui nenhuma física aplicada por Rigidbody como os outros, mas é bem importante e principal na construção dos cenários.

Em nossa cena, utilizamos esse colisor no mapa.

![MAPA CIMA](https://github.com/Rob3rt2/UnityColisores/assets/128638269/cebfacad-e906-40db-8ac9-de2de3ac2223)

# Rigidbody Collider
Diferente do Static Collider, este colisor possui RigidBody, um comum não um cinemático anexado, por ter um RigidBody este colisor é completamente simulado pelos mecanismos de física, fazendo com que possam reagir a colisões e certas forças aplicadas a eles, como alguma batida, queda ou interação do jogador com o objeto em que está inserido, tudo isso feito a partir de nosso Script.

Em nossa cena, adicionamos esse colisor em um bola que está em um dos caminhos do labirinto.

![colisor RIGIDBODY](https://github.com/Rob3rt2/UnityColisores/assets/128638269/ce1b033d-438e-4fdf-8f5d-aeb276546cf6)

- Script em C#:
  
![RIGDBODY COLLIDER](https://github.com/Rob3rt2/UnityColisores/assets/128638269/eaf55e94-b32b-4643-bc38-27e59606e867)


# Kinematic Rigidbody Collider
O mais complexo até então o Kinematic Rigidbody é um colisor que possui a propriedade IsKinematic do Rigidbody ativada, a partir de um script você pode mover um objeto que tenha este colisor com uma modificação de scripts em seu componente transform isso faz com que ele se mova, mas não respondera as forças como um Kinematic Rigidbody. Seu uso é feito normalmente em colisores que tem a atividade de serem ativados, desativados ou movidos, tudo isso para que ele se comporte como um colisor estático, exemplo, é como algo que parado ele faz seu trabalho, mas quando necessário ele se movimenta e pode até ativar outros colisores ao seu redor. 

Em nossa cena, adicionamos um carro modelado por nós no software Blender, para demonstrar a aplicação do colisor.

![colisor KINEMATIC](https://github.com/Rob3rt2/UnityColisores/assets/128638269/973d8089-b653-4008-8339-60ae193bcec8)

- Script em C#: ENTRADA
  
![KINEMATIC COLLIDER ENTRADA](https://github.com/Rob3rt2/UnityColisores/assets/128638269/d454d31f-1538-4931-ae8b-d00f2369331c)

- Script em C#: SAÍDA
  
![script KINEMATIC COLLIDER SAIDA](https://github.com/Rob3rt2/UnityColisores/assets/128638269/dca83edf-1680-4313-9140-834b7263def1)


# Static Trigger Collider
O Static Trigger Collider funciona da mesma forma que um Static Collider padrão, porém com diferença de que durante a colisão não haverá a física inserida como normalmente seria, e sim alguma ação definida pelo usuário no script. 

Em nossa cena, adicionamos um quadro verde que com a colisão do player o quadro irá cair.

![trigger STATIC](https://github.com/Rob3rt2/UnityColisores/assets/128638269/7813e006-dcb9-471e-9a5e-1761430363a0)

- Script em C#:

![STATIC TRIGGER](https://github.com/Rob3rt2/UnityColisores/assets/128638269/641cfa40-4c4d-477b-b205-cb02cf026186)

# Rigidbody Trigger Collider
Este Trigger Collider tem a física aplicada ao seu objeto normalmente, mas durante uma colisão ele não terá a física da colisão aplicada ao momento, por exemplo o objeto pode ter ação física da queda, contudo a resposta física ao entrar na área de colisão de outro colisor não existira, em seu lugar terá uma ação denominada pelo programador no script.

Em nossa cena, adicionamos uma forma vermelha brilhante em um dos caminhos do labirinto.

![Trigger RIGIDIBODY](https://github.com/Rob3rt2/UnityColisores/assets/128638269/ccd6395a-8c5c-4e3f-8b27-e1a873110786)

- Script em C#: ENTRADA
  
![script RIGIDBODY TRIGGER ENTRADA](https://github.com/Rob3rt2/UnityColisores/assets/128638269/f5a7a745-2f58-4919-8472-552b81587d87)

- Script em C#: SAÍDA
  
![RIGIDBODY TRIGGER SAIDA](https://github.com/Rob3rt2/UnityColisores/assets/128638269/c4247fa2-334c-499f-b0e5-b863e79465b2)

# Kinematic Rigidbody Trigger Collide
Também funcionando como o seu colisor padrão sem Trigger, este colisor apresenta as mesmas diferenças que os outros colisores com Trigger, sendo um Kinematic Rigidbody, ele não sofre com a gravidade e com a física de outras colisões e sim o usuário o controla com um movimento programático. Sua Trigger funciona como todas as outras não tem efeito da física ao entrar na área de outro colisor e sim uma ação definida no script durante o tempo em que ele se mante na área de colisão do outro a partir do evento OnTriggerEnter, e depois volta ao normal quando sai da área do colisor com o evento OnTriggerExit.

Em nossa cena, deixamos uma lâmpada posicionada na parte de cima do quadro verde.

![LAMPADA TETO](https://github.com/Rob3rt2/UnityColisores/assets/128638269/56bbdf55-61db-4f18-b296-7b2ca1a3f30e)

- Script em C#: ENTRADA
  
![KINEMATIC TRIGGER ENTRADA](https://github.com/Rob3rt2/UnityColisores/assets/128638269/308a1c0e-79dc-4615-9c21-e1a8647fca58)

- Script em C#: SAÍDA
  
![KINEMATIC TRIGGER SAIDA](https://github.com/Rob3rt2/UnityColisores/assets/128638269/12a3186f-cd4a-4932-810c-46dcb87b46ec)

#
# HUD e MENU
Nosso trabalho vem crescendo, e como objetivo de acrescentar e trazer mais variedades para nosso jogo... Nosso projeto com instruções passadas em aula é **adicionar o HUD (Heads-Up Display) e o Menu em nosso projeto.**

Para criação, decidimos colocar uma tela de Menu mais sombria e que demonstrasse o sentimento que queriamos passar em nosso game. Sendo bem simples de executar, escolhemos cores e fontes para nossa cena de entrada, com botões de "Iniciar Jogo" e "Sair".
Continuando com o HUD, decidimos criar uma barra de sanidade para o player que estará movimentando o personagem. Desenhamos nosso próprio design de barra de sanidade e adicionamos a tela por meio de códigos. Também, colocamos um cronômetro no canto superior da tela... Para quê, conforme o decorrer do jogo, **o player que estará jogando deve sair do labirinto o mais rápido possível!** Com o tempo passando, sua sanidade irá diminuindo até se esgotar e o "Game Over" acontecer. Corra o mais rápido possível, você terá 70 segundos para isso!.
#
## MENU

Montamos o design e **adicionamos o menu** no início do nosso Game. Essa cena possui 2 botões, "Iniciar Jogo" e "Sair". Que correspondem ao começo do jogo e a saída da execução do projeto.

![MENU](https://github.com/Rob3rt2/UnityColisores/assets/128638269/dad7c352-3698-4bfe-85cc-4763b321a725)

## CRÉDITOS
Em seguida, criamos uma cena para os créditos (fim de jogo), contendo: Nome da Instituição, Nome do curso, Nome dos Alunos com suas contribuições para o projeto, Nome da Orientadora, Asset Principais Utilizados e 3 botões para "Voltar", "Reiniciar" e "Sair". 

![CRÉDITOS](https://github.com/Rob3rt2/UnityColisores/assets/128638269/8ea3024c-1998-494c-8dee-d7fbac90f78b)

**- Script de Ambos:**

![CRÉDITOS E MORTE](https://github.com/Rob3rt2/UnityColisores/assets/128638269/6154cb60-0ccb-429e-920b-9730af11055a)

## HUD (Heads-Up Display)

Para o HUD, desenhamos uma barra de sanidade e decidimos adicionar (canto superior esquerdo), começando cheia com 4 barras e diminuindo com o passar do tempo. **Seu objetivo é sair do labirinto o mais rápido possível, antes que sua sanidade acabe!**

![SANIDADE 4](https://github.com/Rob3rt2/UnityColisores/assets/128638269/c0005922-355a-4af8-b578-bbd2f6a67863)

![SANIDADE 3](https://github.com/Rob3rt2/UnityColisores/assets/128638269/81609957-5d9d-4809-8906-7d2708741bd3)

![SANIDADE 2](https://github.com/Rob3rt2/UnityColisores/assets/128638269/45fb64df-b93b-41c9-98c4-ec203e9237d4)

![SANIDADE 1](https://github.com/Rob3rt2/UnityColisores/assets/128638269/81ea98bf-7c3c-4738-95c8-ad5c7c04f52b)

**- Script:**

![SCRIPT HUD](https://github.com/Rob3rt2/UnityColisores/assets/128638269/bd1ec032-8235-4f22-a425-d3560ea6aa28)

Dessa forma, finalizamos todas as instruções passadas e aguardamos por mais atualizações. :)
