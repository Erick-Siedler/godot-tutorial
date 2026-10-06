# Trilha Completa de Godot — Do Zero a um Top-Down RPG + Tower Defense

> **Objetivo:** aprender Godot de verdade, até conseguir programar sozinho um mini game completo no estilo **top-down RPG + tower defense**, sem depender de IA para escrever os sistemas por você.
>
> **Versão recomendada para esta trilha:** Godot 4.x / GDScript.
>
> A regra principal desta trilha é simples:
>
> **não avance porque "entendeu o código"; avance quando conseguir recriá-lo sem olhar.**

---

# Como usar esta trilha

Para cada módulo:

1. Leia os conceitos.
2. Teste cada conceito isoladamente.
3. Faça os exercícios **sem IA**.
4. Se travar, consulte primeiro:
   - erros do Godot;
   - documentação;
   - código que você mesmo já escreveu;
   - debugger;
   - Remote Scene Tree.
5. Só depois procure ajuda externa.
6. Antes de avançar, faça o **checkpoint** do módulo sem copiar código.

Use estes marcadores:

- [ ] Não comecei
- [~] Estou praticando
- [x] Consigo fazer sozinho

---

# Regra de independência

Durante a trilha, tente seguir esta progressão:

### Nível 1 — Pode consultar exemplos

Você pode olhar documentação e exemplos, mas deve digitar tudo manualmente.

### Nível 2 — Pode consultar apenas documentação

Não copie sistemas completos.

### Nível 3 — Pode pesquisar apenas erros específicos

Exemplo:

> `Invalid access to property velocity`

Em vez de:

> `como criar inimigo que segue player godot`

### Nível 4 — Projeto final

Você deve programar o sistema primeiro.

Só use ajuda externa depois de tentar:

1. desenhar a lógica;
2. escrever pseudocódigo;
3. implementar;
4. debugar.

---

# Visão geral da trilha

## Fase 1 — Fundamentos

- [ ] 0. Criando e organizando um projeto
- [ ] 1. Nodes, Scenes e Scene Tree
- [ ] 2. GDScript básico
- [ ] 3. Funções, tipos, classes e referências
- [ ] 4. Ciclo de execução do Godot

## Fase 2 — Movimento e mundo 2D

- [ ] 5. Input e movimento
- [ ] 6. Física e colisões
- [ ] 7. Camera2D
- [ ] 8. Sprites e animações
- [ ] 9. TileMapLayer e mapas

## Fase 3 — Comunicação entre sistemas

- [ ] 10. Signals
- [ ] 11. Groups
- [ ] 12. Timers
- [ ] 13. Instanciação e PackedScene

## Fase 4 — Gameplay

- [ ] 14. Interação e itens
- [ ] 15. Vida, dano e combate
- [ ] 16. Inimigos
- [ ] 17. State Machines
- [ ] 18. Navigation
- [ ] 19. Projectiles

## Fase 5 — Tower Defense

- [ ] 20. Grid e construção
- [ ] 21. Towers / Plants
- [ ] 22. Targeting
- [ ] 23. Waves
- [ ] 24. Economia e recursos
- [ ] 25. Base / Garden

## Fase 6 — Arquitetura

- [ ] 26. Resources
- [ ] 27. Autoload
- [ ] 28. Event Bus
- [ ] 29. Componentização
- [ ] 30. Data-driven design

## Fase 7 — Sistemas de jogo

- [ ] 31. UI
- [ ] 32. Inventário simples
- [ ] 33. Save/Load
- [ ] 34. Game State
- [ ] 35. Menus e troca de cenas

## Fase 8 — Qualidade

- [ ] 36. Debugging
- [ ] 37. Performance
- [ ] 38. Organização de projeto
- [ ] 39. Git

## Fase final

- [ ] 40. Mini game completo

---

# 0. Criando um projeto Godot

## Conceitos

Aprenda:

- Project Manager
- criar projeto;
- pasta do projeto;
- `project.godot`;
- importar assets;
- FileSystem;
- Inspector;
- Scene dock;
- Output;
- Debugger;
- Input Map;
- Project Settings.

Entenda a diferença entre:

- arquivo do projeto;
- scene;
- script;
- asset;
- resource.

## Estrutura inicial recomendada

```text
res://
├── assets/
│   ├── audio/
│   ├── sprites/
│   ├── tiles/
│   └── ui/
├── scenes/
│   ├── player/
│   ├── enemies/
│   ├── towers/
│   ├── world/
│   └── ui/
├── scripts/
├── resources/
└── autoload/
```

Não precisa seguir exatamente isso.

O importante é entender **por que** cada coisa está em determinada pasta.

## Exercícios

- [ ] Criar um projeto vazio.
- [ ] Criar a estrutura de pastas manualmente.
- [ ] Importar uma imagem.
- [ ] Criar uma scene.
- [ ] Salvar a scene.
- [ ] Definir uma Main Scene.
- [ ] Rodar o projeto.

## Checkpoint

Sem consultar tutorial:

> Crie um projeto novo chamado `GardenDefenseTraining`, organize as pastas e faça uma scene aparecer ao apertar F6/F5.

---

# 1. Nodes, Scenes e Scene Tree

Este é provavelmente o conceito mais importante de Godot.

## Node

Um Node é uma peça de funcionalidade.

Exemplos:

```text
Node2D
Sprite2D
CharacterBody2D
Area2D
CollisionShape2D
Camera2D
Timer
Label
AudioStreamPlayer2D
```

## Scene

Uma Scene é uma árvore de Nodes salva como arquivo.

Exemplo:

```text
Player
├── Sprite2D
├── CollisionShape2D
├── Camera2D
└── InteractionArea
```

O Player inteiro pode então ser reutilizado em outras scenes.

## Parent e Child

Aprenda:

- parent;
- child;
- owner;
- caminho de Node;
- `get_node()`;
- `$Node`;
- `%UniqueNode`.

## Scene Tree

Entenda:

```text
Game
├── World
│   ├── Player
│   ├── Enemies
│   └── Towers
└── UI
```

Cada Node existe dentro da árvore.

## Exercícios

### Exercício 1

Faça:

```text
Main
└── Sprite2D
```

Mova o Sprite pelo Inspector.

### Exercício 2

Crie:

```text
Player
├── Sprite2D
└── Label
```

Faça o Label mostrar:

```text
PLAYER
```

### Exercício 3

Crie uma scene `Enemy.tscn` e coloque três instâncias dentro da Main.

## Checkpoint

Você deve conseguir explicar com suas palavras:

- o que é Node;
- o que é Scene;
- por que Scene não é a mesma coisa que Node;
- por que instanciar scenes é tão importante.

---

# 2. GDScript básico

Antes de tentar sistemas de gameplay, domine a linguagem.

## Variáveis

```gdscript
var health = 100
var player_name = "Gardener"
var alive = true
```

## Tipagem

```gdscript
var health: int = 100
var speed: float = 120.0
var alive: bool = true
var player_name: String = "Gardener"
```

Prefira aprender usando tipos.

## Constantes

```gdscript
const MAX_HEALTH := 100
```

## Operadores

Aprenda:

```text
+
-
*
/
%
==
!=
>
<
>=
<=
and
or
not
```

## If

```gdscript
if health <= 0:
    die()
```

## Else

```gdscript
if health > 50:
    print("healthy")
else:
    print("hurt")
```

## Loops

```gdscript
for i in range(10):
    print(i)
```

```gdscript
while health > 0:
    health -= 1
```

## Arrays

```gdscript
var enemies = []
```

```gdscript
var plants = ["pea", "sunflower", "nut"]
```

## Dictionary

```gdscript
var stats = {
    "health": 100,
    "damage": 20
}
```

## Exercícios

Faça scripts apenas pelo Output.

### Exercício 1

Crie:

```text
health = 100
damage = 25
```

Ataque quatro vezes e imprima a vida restante.

### Exercício 2

Crie um Array com cinco plantas.

Imprima cada planta usando `for`.

### Exercício 3

Crie um Dictionary de inimigo:

```text
name
health
speed
damage
```

### Exercício 4

Calcule:

```text
damage_per_second = damage * attacks_per_second
```

### Exercício 5

Crie uma função que descubra se uma wave é boss:

```text
10
20
30
40
...
```

Dica: módulo `%`.

## Checkpoint

Sem Godot visual:

> Escreva um script que simula três inimigos recebendo dano até morrerem.

---

# 3. Funções, tipos, classes e referências

## Funções

```gdscript
func take_damage(amount: int) -> void:
    health -= amount
```

## Retorno

```gdscript
func is_alive() -> bool:
    return health > 0
```

## Parâmetros

```gdscript
func heal(amount: int) -> void:
```

## Escopo

Entenda:

- variável local;
- variável da classe;
- constante;
- parâmetro.

## `class_name`

```gdscript
class_name Enemy
extends CharacterBody2D
```

Isso permite usar o tipo:

```gdscript
var target: Enemy
```

## Referências

Entenda que:

```gdscript
var target = enemy
```

normalmente guarda uma referência ao objeto, não uma cópia completa.

## `@export`

```gdscript
@export var speed: float = 100.0
```

Aprenda por que exportar valores ajuda a balancear o jogo.

## `@onready`

```gdscript
@onready var sprite: Sprite2D = $Sprite2D
```

## Exercícios

- [ ] Criar função `take_damage`.
- [ ] Criar função `heal`.
- [ ] Criar função `is_dead`.
- [ ] Exportar `max_health`.
- [ ] Exportar `movement_speed`.
- [ ] Criar classe `Enemy`.
- [ ] Criar classe `Tower`.

## Checkpoint

Crie um objeto com:

```text
max_health
health
damage
speed
```

e funções:

```text
take_damage()
heal()
die()
```

---

# 4. Ciclo de execução do Godot

Aprenda:

```gdscript
func _ready():
```

```gdscript
func _process(delta):
```

```gdscript
func _physics_process(delta):
```

```gdscript
func _input(event):
```

## `_ready()`

Executado quando o Node entra na Scene Tree.

Use para inicialização.

## `_process(delta)`

Executado a cada frame.

Bom para:

- visual;
- UI;
- lógica que não depende de física.

## `_physics_process(delta)`

Executado no ciclo de física.

Bom para:

- movimento;
- colisão;
- CharacterBody2D.

## Delta

Delta representa o tempo desde o frame anterior.

Sem delta:

```gdscript
position.x += speed
```

o jogo depende do FPS.

Com delta:

```gdscript
position.x += speed * delta
```

## Exercícios

- [ ] Fazer objeto mover sem delta.
- [ ] Fazer objeto mover com delta.
- [ ] limitar FPS e observar a diferença.
- [ ] imprimir `_ready()`.
- [ ] imprimir `_process()`.
- [ ] imprimir `_physics_process()`.

## Checkpoint

Você precisa conseguir explicar:

> Por que movimento deve considerar tempo em vez de quantidade de frames?

---

# 5. Input e movimento top-down

Agora começa o jogo de verdade.

## Input Map

Crie ações:

```text
move_up
move_down
move_left
move_right
interact
attack
build
pause
```

Nunca espalhe teclas diretamente pelo código sem necessidade.

Evite depender de:

```gdscript
KEY_W
```

Prefira ações configuráveis.

## Vetor de direção

```gdscript
var direction := Input.get_vector(
    "move_left",
    "move_right",
    "move_up",
    "move_down"
)
```

## Movimento

```gdscript
velocity = direction * speed
move_and_slide()
```

## Normalização

Entenda por que movimento diagonal pode ficar mais rápido sem normalização.

## Exercícios

### Exercício 1

Movimento WASD.

### Exercício 2

Adicionar movimento diagonal.

### Exercício 3

Sprint.

```text
Shift = velocidade maior
```

### Exercício 4

Impedir movimento enquanto player ataca.

### Exercício 5

Faça o personagem olhar para a direção do mouse.

## Mini projeto

Faça uma arena vazia onde o player consegue:

- andar;
- correr;
- olhar em 8 direções.

---

# 6. Física e colisões

## Principais Nodes

Aprenda:

```text
CharacterBody2D
StaticBody2D
RigidBody2D
Area2D
CollisionShape2D
CollisionPolygon2D
```

## CharacterBody2D

Ideal para personagens controlados por código.

## StaticBody2D

Objetos imóveis:

```text
paredes
pedras
prédios
barreiras
```

## Area2D

Detecta entrada/saída.

Perfeito para:

```text
pickup
hitbox
interaction
range de torre
trigger
```

## Collision Layers e Masks

Domine isso cedo.

Exemplo:

```text
Layer 1 = World
Layer 2 = Player
Layer 3 = Enemy
Layer 4 = Projectile
Layer 5 = Tower
Layer 6 = Interaction
```

A Layer diz:

> "quem eu sou?"

A Mask diz:

> "o que eu detecto?"

## Exercícios

- [ ] Player colidindo com parede.
- [ ] Player atravessando Area2D.
- [ ] moeda detectando player.
- [ ] projectile detectando enemy.
- [ ] enemy sem colidir com projectile inimigo.

## Checkpoint

Monte uma arena onde:

- player não atravessa paredes;
- player pega uma moeda;
- moeda desaparece;
- inimigos conseguem detectar player.

---

# 7. Camera2D

Aprenda:

- Camera2D;
- position smoothing;
- limits;
- zoom;
- drag;
- shake.

## Exercícios

### Exercício 1

Camera segue player.

### Exercício 2

Camera não sai do mapa.

### Exercício 3

Adicionar zoom.

### Exercício 4

Criar screen shake simples ao receber dano.

## Aplicação no jogo

Para seu jogo:

```text
Player
└── Camera2D
```

provavelmente será suficiente inicialmente.

Depois você pode separar câmera do Player.

---

# 8. Sprites e animações

## Nodes

```text
Sprite2D
AnimatedSprite2D
AnimationPlayer
AnimationTree
```

Comece com:

```text
AnimatedSprite2D
```

Depois aprenda `AnimationPlayer`.

## Conceitos

- SpriteFrames;
- FPS da animação;
- looping;
- flip horizontal;
- animation finished;
- estados de animação.

## Exercícios

Faça:

- [ ] idle;
- [ ] walk;
- [ ] attack;
- [ ] hurt;
- [ ] death.

Depois conecte movimento à animação.

Exemplo de lógica:

```text
velocity == 0 -> idle
velocity != 0 -> walk
attacking -> attack
dead -> death
```

## Desafio

Faça animação em quatro direções:

```text
walk_up
walk_down
walk_left
walk_right
```

---

# 9. TileMapLayer e construção de mapas

Para um jogo top-down isso é essencial.

## Conceitos

Aprenda:

- TileSet;
- TileMapLayer;
- atlas;
- tile size;
- terrain;
- collision;
- layers;
- z-index;
- y-sort;
- custom data.

## Organização possível

```text
World
├── Ground
├── Roads
├── Decorations
├── Obstacles
└── Buildings
```

## Custom Data

Tiles podem armazenar dados.

Exemplo:

```text
buildable = true
terrain = grass
movement_cost = 1
```

Isso pode depois ajudar na construção de torres.

## Exercícios

- [ ] criar TileSet;
- [ ] pintar chão;
- [ ] criar parede;
- [ ] adicionar colisão;
- [ ] criar terreno;
- [ ] criar segundo TileMapLayer;
- [ ] criar mapa maior que a tela.

## Mini projeto

Crie uma pequena cidade abandonada com:

```text
rua
grama
calçada
paredes
entulho
área de jardim
```

Player deve poder andar nela normalmente.

---

# 10. Signals

Signals são fundamentais para evitar código excessivamente acoplado.

## Signal

Um objeto pode anunciar:

> alguma coisa aconteceu.

Exemplo:

```gdscript
signal died
```

```gdscript
signal health_changed(current_health)
```

## Emit

```gdscript
health_changed.emit(health)
```

## Connect

Outro objeto pode reagir ao Signal.

## Pense assim

Player:

```text
"Minha vida mudou."
```

UI:

```text
"Então vou atualizar a barra."
```

Player não precisa saber como a UI funciona.

## Exercícios

### Exercício 1

Botão emite evento.

### Exercício 2

Enemy emite:

```text
died
```

quando morre.

### Exercício 3

Player emite:

```text
health_changed
```

e UI atualiza.

### Exercício 4

WaveManager emite:

```text
wave_started
wave_finished
```

## Checkpoint

Faça Player + UI sem a UI consultar a vida do Player a cada frame.

---

# 11. Groups

Groups são como tags.

Exemplo:

```text
enemy
tower
player
damageable
buildable
```

## Uso

```gdscript
get_tree().get_nodes_in_group("enemy")
```

ou:

```gdscript
body.is_in_group("enemy")
```

## Exercícios

- [ ] adicionar todos inimigos ao grupo `enemy`.
- [ ] contar quantos inimigos existem.
- [ ] destruir todos para teste.
- [ ] verificar se Area2D encontrou um inimigo.

## Aplicação

Tower pode encontrar:

```text
enemy
```

sem conhecer classes específicas.

---

# 12. Timers

Timers aparecem em praticamente todo jogo.

Use para:

- cooldown;
- ataque;
- wave;
- spawn;
- invencibilidade;
- geração de recurso;
- efeitos.

## Node Timer

Aprenda:

```text
wait_time
one_shot
autostart
timeout
```

## Exercícios

### Exercício 1

Imprimir mensagem a cada 1 segundo.

### Exercício 2

Sunflower gera Sun a cada 5 segundos.

### Exercício 3

Torre atira a cada 0.8 segundos.

### Exercício 4

Após tomar dano, Player fica invulnerável por 0.5 segundos.

---

# 13. PackedScene e instanciação

Você não deve criar inimigos manualmente na Scene Tree.

Crie a scene:

```text
Enemy.tscn
```

e depois:

```gdscript
var enemy_scene = preload("res://...")
var enemy = enemy_scene.instantiate()
add_child(enemy)
```

## Conceitos

Aprenda:

- `preload`;
- `load`;
- `PackedScene`;
- `instantiate`;
- `add_child`;
- `queue_free`.

## Exercícios

### Exercício 1

Botão cria inimigo.

### Exercício 2

Spawner cria inimigo automaticamente.

### Exercício 3

Projectile é criado pela Tower.

### Exercício 4

Ao morrer, Enemy cria uma moeda.

---

# 14. Sistema de interação

Top-down RPG precisa de interação.

## Modelo

```text
Player
└── InteractionArea
```

Objetos próximos:

```text
Chest
NPC
Garden
Door
Pickup
```

## Conceitos

Aprenda:

- Area2D;
- detecção;
- prioridade;
- interface;
- função `interact()`.

## Forma simples

Cada objeto interativo possui:

```gdscript
func interact():
```

O Player apenas chama a função.

## Exercícios

- [ ] abrir porta;
- [ ] pegar item;
- [ ] ativar alavanca;
- [ ] falar com NPC fake;
- [ ] plantar uma defesa.

## Checkpoint

O Player deve conseguir interagir com objetos diferentes usando **o mesmo botão**.

---

# 15. Vida, dano e combate

Não coloque lógica de dano espalhada.

Crie um padrão.

## Conceitos

```text
Health
Damage
Hitbox
Hurtbox
Knockback
Invulnerability
Death
```

## Sistema básico

```gdscript
func take_damage(amount: int):
    health -= amount

    if health <= 0:
        die()
```

Depois evolua.

## Hitbox vs Hurtbox

### Hitbox

Área que causa dano.

### Hurtbox

Área que recebe dano.

Isso permite separar física normal de combate.

## Exercícios

- [ ] Player recebe dano.
- [ ] Enemy recebe dano.
- [ ] Espada usa hitbox.
- [ ] projectile usa hitbox.
- [ ] adicionar knockback.
- [ ] adicionar invulnerabilidade curta.

## Desafio

Faça dano crítico com:

```text
10% chance
2x damage
```

---

# 16. Inimigos

Comece simples.

## Enemy V1

Comportamento:

```text
encontrar player
andar até player
causar dano ao encostar
morrer
```

## Conceitos

- target;
- distância;
- direção;
- velocidade;
- attack range;
- cooldown.

## Exercícios

### Enemy 1

Segue Player.

### Enemy 2

Segue Garden.

### Enemy 3

É lento mas tem muita vida.

### Enemy 4

É rápido mas fraco.

### Enemy 5

Ataca à distância.

## Importante

Evite criar cinco scripts totalmente diferentes.

Tente reutilizar uma base.

---

# 17. State Machines

Depois de entender inimigos simples, aprenda estados.

Exemplo:

```text
IDLE
CHASE
ATTACK
HURT
DEAD
```

## Primeira versão

Pode usar enum:

```gdscript
enum State {
    IDLE,
    CHASE,
    ATTACK,
    DEAD
}
```

## Depois

Você pode aprender State Pattern com Nodes/scripts separados.

Não comece superarquitetando.

## Exercícios

### Player

```text
IDLE
MOVE
ATTACK
HURT
DEAD
```

### Enemy

```text
SPAWNING
CHASE
ATTACK
DEAD
```

## Checkpoint

Enemy não deve atacar enquanto está morto.

Parece óbvio, mas esse tipo de bug ensina por que estados existem.

---

# 18. Navigation

Para mapas com obstáculos, inimigos precisam navegar.

Aprenda:

```text
NavigationRegion2D
NavigationAgent2D
navigation mesh / polygon
pathfinding
target_position
```

## Exercícios

- [ ] Enemy segue Player em mapa aberto.
- [ ] adicionar uma parede.
- [ ] Enemy contorna a parede.
- [ ] mudar target para Garden.
- [ ] recalcular caminho quando necessário.

## Desafio

Faça Enemy escolher entre:

```text
Garden A
Garden B
```

baseado em distância.

Isso começa a se aproximar do sistema de múltiplos jardins.

---

# 19. Projectiles

Muito importante para tower defense.

## Scene

```text
Projectile
├── Sprite2D
├── Area2D
└── CollisionShape2D
```

## Dados

```text
speed
damage
direction
target
lifetime
```

## Exercícios

### Projectile 1

Move reto.

### Projectile 2

Desaparece ao acertar.

### Projectile 3

Desaparece depois de 5 segundos.

### Projectile 4

Segue alvo.

### Projectile 5

Causa splash damage.

---

# 20. Sistema de Grid e construção

Agora entramos diretamente no tower defense.

## Conceitos

Aprenda:

```text
world position
local position
grid coordinate
cell coordinate
snap
occupied cell
valid placement
```

## Sistema inicial

Ao clicar:

1. pegar posição do mouse;
2. converter para célula;
3. verificar se pode construir;
4. verificar se célula está vazia;
5. criar Tower;
6. marcar célula como ocupada.

## Exercícios

- [ ] mostrar célula sob mouse;
- [ ] snapar Sprite ao grid;
- [ ] construir apenas em grama;
- [ ] impedir duas torres na mesma célula;
- [ ] mostrar preview vermelho/verde.

## Checkpoint

Você deve conseguir construir uma defesa sem escrever posição manual.

---

# 21. Towers / Plants

Crie inicialmente três.

## Peashooter

```text
range = médio
damage = médio
fire_rate = médio
```

## Sunflower

```text
gera recurso
não ataca
```

## Wall / Nut

```text
vida alta
sem ataque
```

## Estrutura possível

```text
Tower
├── Sprite
├── Range
│   └── CollisionShape2D
├── ShootTimer
└── Marker2D
```

## Exercícios

- [ ] Tower detecta enemy.
- [ ] Tower escolhe target.
- [ ] Timer controla ataque.
- [ ] Tower cria projectile.
- [ ] projectile causa dano.
- [ ] target morto é removido corretamente.

---

# 22. Targeting

Aprenda diferentes prioridades.

## First

Inimigo mais próximo da base.

## Closest

Inimigo mais perto da torre.

## Strongest

Maior vida.

## Weakest

Menor vida.

## Exercício

Implemente:

```gdscript
enum TargetMode {
    FIRST,
    CLOSEST,
    STRONGEST
}
```

e consiga trocar durante o jogo.

## Desafio

Tower deve trocar de target quando:

- target morre;
- sai do range;
- outro target mais prioritário aparece.

---

# 23. Wave System

Uma Wave não deve ser apenas:

```gdscript
for i in 10:
    spawn_enemy()
```

Crie um gerenciador.

## Dados da Wave

```text
wave_number
enemy_count
spawn_interval
enemy_types
boss
```

## Fluxo

```text
preparation
↓
wave starts
↓
spawn enemies
↓
wait enemies die
↓
wave ends
↓
rewards
↓
next preparation
```

## Exercícios

### Wave 1

5 inimigos normais.

### Wave 2

8 inimigos.

### Wave 3

10 inimigos + rápido.

### Wave 5

Mini boss.

### Wave 10

Boss.

## Fórmulas

Experimente criar crescimento:

```text
enemy_health = base_health * scaling
enemy_count = base_count + wave
```

Não procure a fórmula perfeita.

Aprenda a criar e ajustar.

---

# 24. Economia e recursos

Para o teu tipo de jogo, você pode ter algo como:

```text
Sun
Scrap
Seeds
XP
```

Comece com apenas **um recurso**.

## Resource Manager simples

```text
sun = 100
```

Funções:

```text
add_sun()
can_afford()
spend_sun()
```

## Exercícios

- [ ] Sunflower gera Sun.
- [ ] construir Peashooter custa Sun.
- [ ] UI mostra Sun.
- [ ] impedir compra sem Sun.
- [ ] destruir torre pode devolver parte do custo.

## Depois

Adicione:

```text
duplicação
upgrade
repair
garden progression
```

---

# 25. Base / Garden

Garden é o objeto central do tower defense.

## Dados possíveis

```text
health
max_health
level
stored_sun
total_sun_generated
defenses
```

## Eventos

```text
garden_damaged
garden_destroyed
garden_upgraded
```

## Exercícios

- [ ] Enemy causa dano ao Garden.
- [ ] Garden possui barra de vida.
- [ ] perder Garden causa Game Over.
- [ ] Garden recebe Sun.
- [ ] Sun total aumenta progresso.

## Desafio

Crie dois Gardens independentes.

Cada um precisa possuir:

```text
vida
defesas
área de construção
recursos/progresso
```

---

# 26. Resources

`Resource` é um conceito extremamente útil em Godot.

Use para representar **dados**, não necessariamente objetos no mundo.

## Exemplo

```gdscript
class_name TowerData
extends Resource

@export var display_name: String
@export var cost: int
@export var damage: float
@export var range: float
@export var fire_rate: float
@export var scene: PackedScene
```

Então você pode criar:

```text
peashooter.tres
sunflower.tres
nut.tres
```

## Vantagem

Em vez de:

```gdscript
if tower == "pea":
```

os dados ficam separados do código.

## Exercícios

- [ ] EnemyData.
- [ ] TowerData.
- [ ] ItemData.
- [ ] WaveData.

## Checkpoint

Crie duas torres usando o **mesmo script**, mas Resources diferentes.

---

# 27. Autoload

Autoload cria sistemas persistentes/globais.

Bom para:

```text
GameManager
SaveManager
AudioManager
SceneManager
```

Ruim para:

```text
qualquer variável só porque é fácil acessar.
```

## Exercícios

### GameManager

Armazene:

```text
current_wave
game_state
```

### AudioManager

Função:

```text
play_sfx()
```

### SaveManager

Funções:

```text
save_game()
load_game()
```

---

# 28. Event Bus

Um Event Bus é normalmente um Autoload que possui signals globais.

Exemplo:

```gdscript
signal enemy_killed(enemy)
signal sun_changed(amount)
signal wave_started(number)
```

## Quando usar

Bom para sistemas distantes.

Exemplo:

Enemy morre.

Então:

```text
ScoreManager
QuestManager
UI
WaveManager
```

podem reagir.

Enemy não precisa conhecer todos eles.

## Cuidado

Não transforme tudo em evento global.

Isso pode deixar o fluxo difícil de entender.

---

# 29. Componentização

Comece a tirar comportamentos reutilizáveis dos objetos.

Exemplo:

```text
Enemy
├── HealthComponent
├── MovementComponent
├── HurtboxComponent
└── DropComponent
```

## Componentes úteis

```text
HealthComponent
DamageComponent
HitboxComponent
HurtboxComponent
CooldownComponent
InteractableComponent
```

## Exercício

Faça Player e Enemy usarem o mesmo `HealthComponent`.

Depois Tower e Garden também.

---

# 30. Data-driven design

O objetivo:

Adicionar conteúdo sem reescrever sistemas.

Ruim:

```gdscript
if enemy_type == "cone":
    health = 200
elif enemy_type == "bucket":
    health = 400
```

Melhor:

```text
EnemyData
```

com dados diferentes.

## Desafio

Crie quatro inimigos apenas configurando Resources:

```text
Normal
Fast
Tank
Boss
```

O script principal deve continuar o mesmo.

---

# 31. UI

Aprenda Nodes `Control`.

## Essenciais

```text
Control
Panel
Label
Button
TextureRect
ProgressBar
HBoxContainer
VBoxContainer
MarginContainer
CanvasLayer
```

## Anchors

Domine:

```text
anchors
offsets
containers
```

Evite posicionar tudo manualmente.

## Exercícios

- [ ] health bar;
- [ ] Sun counter;
- [ ] wave counter;
- [ ] tower selection bar;
- [ ] pause menu;
- [ ] game over screen.

## Regra

UI deve responder a Signals.

Evite:

```gdscript
func _process():
    label.text = str(player.health)
```

---

# 32. Inventário simples

Não comece com inventário estilo RPG gigante.

Faça:

```text
ItemData
amount
inventory slots
```

## Primeira versão

Dictionary:

```gdscript
{
    item_resource: amount
}
```

## Exercícios

- [ ] pegar seed.
- [ ] adicionar ao inventário.
- [ ] mostrar quantidade.
- [ ] gastar seed para plantar defesa.

---

# 33. Save / Load

Comece salvando poucos dados.

## Dados iniciais

```text
player_position
current_wave
sun
garden_level
unlocked_towers
```

## Aprenda

```text
FileAccess
JSON
Dictionary
```

## Fluxo

```text
Game State
↓
Dictionary
↓
JSON
↓
File
```

Load faz o inverso.

## Exercícios

- [ ] salvar número.
- [ ] carregar número.
- [ ] salvar posição.
- [ ] salvar Sun.
- [ ] salvar Wave.
- [ ] restaurar estado.

## Desafio

Feche o jogo.

Abra novamente.

Continue no mesmo progresso.

---

# 34. Game State

Defina explicitamente estados do jogo.

```text
MAIN_MENU
PLAYING
PREPARATION
WAVE
PAUSED
GAME_OVER
```

## Por quê?

Porque sistemas precisam saber:

```text
Player pode mover?
Enemy pode spawnar?
Timer está contando?
UI deve aparecer?
```

## Exercício

Durante:

```text
PREPARATION
```

não existem inimigos.

Durante:

```text
WAVE
```

começam os spawns.

Durante:

```text
PAUSED
```

gameplay para.

---

# 35. Menus e troca de Scenes

Aprenda:

```gdscript
get_tree().change_scene_to_file(...)
```

Depois crie um SceneManager.

## Scenes

```text
MainMenu
Game
GameOver
Credits
```

## Exercícios

- [ ] botão Play;
- [ ] botão Restart;
- [ ] botão Main Menu;
- [ ] botão Quit;
- [ ] loading simples.

---

# 36. Debugging

Essa parte vai diminuir muito sua dependência de IA.

Aprenda a debugar antes de pesquisar.

## Ferramentas

```text
print()
printerr()
breakpoints
Debugger
Remote Scene Tree
Inspector remoto
Profiler
Monitors
```

## Perguntas que você deve fazer

Quando algo não funciona:

1. A função está sendo chamada?
2. O Node existe?
3. O Signal conectou?
4. O valor está correto?
5. O objeto está na Scene Tree?
6. A Collision Layer está correta?
7. A Mask está correta?
8. O target ainda é válido?
9. O Node já foi destruído?
10. A função roda no momento certo?

## Exercício de debugging

Crie propositalmente bugs:

- path errado;
- Signal não conectado;
- Layer errada;
- target `null`;
- divisão por zero;
- array index inválido.

Depois resolva sem IA.

---

# 37. Performance

Não precisa otimizar cedo, mas precisa conhecer.

## Conceitos

```text
process por frame
physics process
draw calls
node count
object allocation
queue_free
pooling
distance checks
navigation updates
```

## Regra

Não coloque tudo em `_process()`.

Pergunte:

> Isso realmente precisa rodar 60 vezes por segundo?

## Exercícios

### Teste 1

Spawn 50 enemies.

### Teste 2

Spawn 200.

### Teste 3

Use Profiler.

Veja qual script consome mais tempo.

## Mais tarde

Aprenda Object Pooling para:

```text
projectiles
damage numbers
particles
enemies
```

Mas só quando necessário.

---

# 38. Organização de projeto

Quando o projeto crescer, organização importa muito.

## Exemplo

```text
res://

assets/
    characters/
    enemies/
    environment/
    ui/

game/
    game.tscn
    game.gd

player/
    player.tscn
    player.gd

enemies/
    enemy.gd
    enemy_data.gd
    normal/
    tank/
    fast/

towers/
    tower.gd
    tower_data.gd
    peashooter/
    sunflower/

systems/
    waves/
    building/
    save/

ui/

resources/
```

## Regra

Organize por **feature/domínio**, não apenas por tipo de arquivo.

---

# 39. Git

Use Git desde cedo.

## Conceitos

```text
repository
commit
branch
merge
.gitignore
diff
```

## Bons commits

```text
feat: add player movement
feat: add enemy health
fix: tower losing target after enemy death
refactor: move health logic into component
```

## Exercício

Faça commits separados para:

1. Player;
2. Enemy;
3. Tower;
4. Wave System;
5. UI.

Aprenda a olhar um `diff`.

Isso também ajuda muito a entender o próprio código.

---

# 40. PROJETO FINAL — Garden Defense Mini Game

Agora você deve fazer um jogo pequeno sem copiar implementação pronta.

---

# Regras do projeto final

Você pode consultar:

- documentação;
- mensagens de erro;
- anotações dessa trilha.

Evite procurar:

> "Godot complete tower defense tutorial"

A ideia é você descobrir a implementação.

---

# Escopo

## Player

O Player deve:

- [ ] andar em quatro/oito direções;
- [ ] possuir animação;
- [ ] ter vida;
- [ ] receber dano;
- [ ] atacar;
- [ ] interagir;
- [ ] morrer.

---

# Mundo

O mapa deve ter:

- [ ] chão;
- [ ] paredes;
- [ ] obstáculos;
- [ ] colisão;
- [ ] área de Garden;
- [ ] área onde não pode construir.

---

# Garden

Garden possui:

```text
100 HP
Sun storage
Defense grid
```

Precisa:

- [ ] receber dano;
- [ ] morrer;
- [ ] gerar Game Over;
- [ ] armazenar recursos.

---

# Recursos

Comece apenas com:

```text
SUN
```

Sun serve para:

```text
construir
reparar
upgrade
```

---

# Towers

Implemente três.

## Peashooter

```text
Cost: 100
Attack: projectile
Range: medium
```

## Sunflower

```text
Cost: 50
Generates Sun
```

## Nut

```text
Cost: 75
High HP
No attack
```

---

# Building System

Precisa:

- [ ] selecionar Tower;
- [ ] mostrar preview;
- [ ] snap ao grid;
- [ ] verificar tile válido;
- [ ] verificar ocupação;
- [ ] verificar custo;
- [ ] construir;
- [ ] descontar Sun.

---

# Enemy System

Implemente três.

## Normal

Balanceado.

## Runner

Rápido, pouca vida.

## Tank

Lento, muita vida.

Todos usam o mesmo sistema base sempre que possível.

---

# Enemy AI

Fluxo:

```text
SPAWN
↓
MOVE TO GARDEN
↓
ATTACK
↓
DEAD
```

Se houver obstáculo:

```text
NavigationAgent2D
```

---

# Waves

Implemente pelo menos:

```text
Wave 1
Wave 2
Wave 3
Wave 4
Wave 5 - boss
```

Wave deve terminar apenas quando:

```text
todos foram spawnados
+
todos morreram
```

---

# UI

Mostrar:

```text
Player HP
Garden HP
Sun
Current Wave
Enemies Remaining
Selected Tower
```

---

# Save

Salvar:

```text
highest_wave
unlocked_towers
settings
```

Opcional:

```text
run atual
```

---

# Game Flow

```text
MAIN MENU
   ↓
START
   ↓
PREPARATION
   ↓
WAVE
   ↓
REWARD
   ↓
PREPARATION
   ↓
WAVE
   ↓
...
   ↓
GAME OVER
```

---

# Ordem de implementação do projeto final

Não tente fazer tudo junto.

---

## Milestone 1 — Empty World

Objetivo:

```text
abrir jogo
player aparece
mapa aparece
```

Checklist:

- [ ] Game.tscn
- [ ] Player
- [ ] Camera
- [ ] TileMap

---

## Milestone 2 — Player

- [ ] movimento;
- [ ] colisão;
- [ ] animação;
- [ ] vida;
- [ ] dano.

---

## Milestone 3 — Enemy Dummy

Enemy apenas:

```text
fica parado
recebe dano
morre
```

Não crie IA ainda.

---

## Milestone 4 — Combat

- [ ] player ataca;
- [ ] enemy recebe dano;
- [ ] health component;
- [ ] death.

---

## Milestone 5 — Enemy Movement

- [ ] segue Garden;
- [ ] Navigation;
- [ ] ataque;
- [ ] cooldown.

---

## Milestone 6 — Garden

- [ ] vida;
- [ ] dano;
- [ ] destruction;
- [ ] Game Over.

Agora já existe uma condição de derrota.

---

## Milestone 7 — Tower Placement

Faça apenas um quadrado como Tower.

- [ ] preview;
- [ ] grid;
- [ ] valid placement;
- [ ] instantiate.

Sem tiro ainda.

---

## Milestone 8 — Tower Attack

- [ ] Range;
- [ ] Target;
- [ ] Timer;
- [ ] Projectile;
- [ ] Damage.

Agora já existe tower defense.

---

## Milestone 9 — Economy

- [ ] Sun;
- [ ] cost;
- [ ] Sunflower;
- [ ] UI.

---

## Milestone 10 — Wave Manager

- [ ] spawn points;
- [ ] wave timer;
- [ ] enemy count;
- [ ] wave finish.

---

## Milestone 11 — Content

Adicionar:

```text
3 enemies
3 towers
5 waves
```

Sem mudar sistemas principais.

Se adicionar conteúdo exigir reescrever tudo, sua arquitetura precisa melhorar.

---

## Milestone 12 — UI

Criar HUD completo.

---

## Milestone 13 — Save

Salvar progresso.

---

## Milestone 14 — Polish

Somente agora:

```text
particles
screen shake
better animation
sound
transitions
juice
```

---

# Boss final do aprendizado

Depois de terminar o mini game, implemente sozinho:

## Feature 1 — Segunda Garden

O mapa passa a possuir:

```text
Garden A
Garden B
```

Enemy deve escolher um objetivo.

---

## Feature 2 — Hero Plant

Crie uma unidade que:

- pode andar;
- procura inimigo;
- aproxima-se;
- ataca automaticamente;
- retorna para Garden se não houver inimigo.

Aqui você mistura:

```text
State Machine
Navigation
Targeting
Combat
Signals
```

---

## Feature 3 — Upgrade de Tower

Cada Tower:

```text
Level 1
Level 2
Level 3
```

Upgrade altera:

```text
damage
range
attack speed
```

---

## Feature 4 — Boss Wave

Boss deve possuir pelo menos:

```text
2 ataques
1 mudança de estado
muita vida
barra própria
```

---

## Feature 5 — Garden Progression

Garden registra:

```text
total_sun_generated
```

e desbloqueia melhorias ao atingir milestones.

Exemplo:

```text
1000 Sun → Level 2
3000 Sun → Level 3
7000 Sun → Level 4
```

---

# Exercícios extras

Quando terminar, faça estes sem tutorial.

## Fácil

- [ ] moeda que gira;
- [ ] porta automática;
- [ ] chest;
- [ ] pickup de cura;
- [ ] botão que abre menu;
- [ ] contador regressivo;
- [ ] stamina;
- [ ] dash.

## Médio

- [ ] poison damage;
- [ ] enemy ranged;
- [ ] explosive projectile;
- [ ] tower slow;
- [ ] tower splash;
- [ ] enemy shield;
- [ ] knockback;
- [ ] critical hit;
- [ ] floating damage numbers.

## Difícil

- [ ] minimap;
- [ ] procedural waves;
- [ ] boss state machine;
- [ ] skill tree;
- [ ] quest system;
- [ ] fog of war;
- [ ] procedural loot;
- [ ] multiple gardens;
- [ ] hero AI;
- [ ] enemy formations.

---

# Conceitos que você deve saber explicar

Antes de considerar que aprendeu Godot, tente explicar sozinho:

- [ ] Node
- [ ] Scene
- [ ] Scene Tree
- [ ] Node lifecycle
- [ ] `_ready`
- [ ] `_process`
- [ ] `_physics_process`
- [ ] delta
- [ ] Input Map
- [ ] Vector2
- [ ] CharacterBody2D
- [ ] Area2D
- [ ] CollisionShape2D
- [ ] Collision Layers
- [ ] Collision Masks
- [ ] Signals
- [ ] Groups
- [ ] Timer
- [ ] PackedScene
- [ ] instantiate
- [ ] Resources
- [ ] Autoload
- [ ] State Machine
- [ ] NavigationAgent2D
- [ ] TileMapLayer
- [ ] UI Containers
- [ ] FileAccess
- [ ] JSON
- [ ] component
- [ ] dependency
- [ ] event
- [ ] game state
- [ ] object pooling
- [ ] profiler

---

# Perguntas que você deve conseguir responder

## Godot

1. Qual a diferença entre Node e Scene?
2. Quando usar Area2D?
3. Quando usar CharacterBody2D?
4. O que `_physics_process()` faz?
5. Por que existe `delta`?
6. O que é um Signal?
7. Por que usar Groups?
8. O que é PackedScene?
9. Qual a diferença entre `preload()` e carregar algo durante execução?
10. Para que serve Resource?
11. Quando usar Autoload?
12. Por que não colocar tudo no GameManager?

## Arquitetura

13. Quem deve controlar a vida: UI ou Player?
14. Tower precisa conhecer WaveManager?
15. Enemy precisa conhecer HUD?
16. Como reduzir dependência entre sistemas?
17. Quando criar Component?
18. Quando um Signal é melhor que chamada direta?
19. Quando chamada direta é melhor que Signal?
20. Como adicionar inimigo novo sem duplicar script?

## Tower Defense

21. Como descobrir target?
22. Como invalidar target morto?
23. Como saber quando Wave terminou?
24. Como impedir construção em célula ocupada?
25. Como representar dados das Towers?
26. Como escalar inimigos?
27. Como separar Wave de Enemy?
28. Como fazer dois Gardens?
29. Como evitar que 200 enemies destruam performance?
30. Como salvar progresso?

---

# Desafios sem código pronto

Faça estes apenas com pseudocódigo primeiro.

## Desafio A — Target da Tower

Escreva em português:

```text
Quando inimigo entrar no range...
```

até chegar ao comportamento completo.

Depois converta para GDScript.

---

## Desafio B — Wave

Pseudocódigo:

```text
começar preparação
esperar
começar wave
spawnar inimigos
esperar todos morrerem
dar recompensa
começar próxima preparação
```

Depois implemente.

---

## Desafio C — Building

Pseudocódigo:

```text
jogador escolhe planta
preview aparece
mouse move
preview segue grid
verifica terreno
verifica dinheiro
clique
cria planta
```

Depois implemente.

---

# Método recomendado para programar qualquer feature

Sempre siga:

## 1. Defina comportamento

Exemplo:

> Peashooter ataca o inimigo mais próximo dentro de 150 pixels a cada 1 segundo.

## 2. Descubra os dados

```text
range
damage
fire_rate
target
```

## 3. Descubra eventos

```text
enemy entered
enemy exited
timer timeout
target died
```

## 4. Faça pseudocódigo

```text
if no target:
    find target

if target exists and cooldown ready:
    shoot
```

## 5. Só então escreva GDScript

Isso é o que mais reduz dependência de IA.

---

# Regra dos 30 minutos

Quando travar:

## Primeiros 10 minutos

Leia o código.

Use:

```text
print
breakpoint
Remote Inspector
```

## Próximos 10

Leia o erro e consulte documentação.

## Próximos 10

Pesquise apenas o problema específico.

Depois disso, pedir ajuda é totalmente válido.

Mas quando receber a solução:

1. entenda;
2. feche a resposta;
3. reescreva sozinho;
4. explique o erro com suas palavras.

---

# Diário de aprendizado

Crie um arquivo:

```text
DEVLOG_LEARNING.md
```

Depois de cada sessão:

```markdown
## 2026-XX-XX

### Aprendi
- Signals
- Area2D

### Fiz sozinho
- Pickup de moeda

### Travei em
- Collision Masks

### Erro
Meu Area2D detectava parede.

### Causa
Mask estava incluindo World.

### Solução
Deixei apenas Player.

### Próximo
Criar HealthComponent.
```

Depois de alguns meses isso vira sua própria documentação.

---

# Cheat Sheet mental

Quando precisar criar algo, pense:

```text
É algo no mundo?
→ Node2D

É um personagem controlado?
→ CharacterBody2D

Só precisa detectar?
→ Area2D

É imóvel e colide?
→ StaticBody2D

É dado/configuração?
→ Resource

Aconteceu alguma coisa?
→ Signal

Preciso esperar tempo?
→ Timer

Preciso criar várias cópias?
→ PackedScene

Preciso marcar vários objetos?
→ Group

Preciso existir entre scenes?
→ talvez Autoload

Preciso mover IA por obstáculos?
→ NavigationAgent2D

Preciso organizar comportamento complexo?
→ State Machine
```

---

# Meta final

Você concluiu esta trilha quando conseguir abrir um projeto vazio e, sem tutorial, construir aproximadamente isto:

```text
Main Menu
   ↓
Game
├── World
│   ├── TileMap
│   ├── Player
│   ├── Garden
│   ├── Towers
│   ├── Enemies
│   └── SpawnPoints
│
├── Systems
│   ├── WaveManager
│   ├── BuildingSystem
│   └── EconomyManager
│
└── UI
    ├── Health
    ├── GardenHealth
    ├── Sun
    ├── Wave
    └── TowerBar
```

E conseguir explicar:

> quem cria quem, quem conhece quem, quem envia signals para quem e onde cada estado do jogo é armazenado.

Nesse ponto você já não está apenas "seguindo Godot".

Você está **desenvolvendo um jogo**.

---

# Próxima evolução depois do mini game

Só depois de fechar esse projeto, comece a estudar sistemas maiores:

```text
advanced enemy AI
behavior trees
procedural generation
advanced shader effects
custom resources
editor plugins
multithreading
ECS concepts
advanced save migration
localization
accessibility
controller support
advanced optimization
```

Para o seu jogo completo, a evolução natural seria:

```text
Mini Garden Defense
        ↓
Top-down exploration
        ↓
Garden construction
        ↓
Wave defense
        ↓
Multiple gardens
        ↓
Hero plants
        ↓
Garden progression
        ↓
Bosses
        ↓
World progression
        ↓
Story / campaign
```

Não tente construir a última etapa enquanto ainda está aprendendo a primeira.

Fechar pequenos jogos é uma das formas mais rápidas de aprender a terminar jogos grandes.
