📘 HUD Generator — Documentação
🖥️ Gerador de HUD por /title
O HUD Generator é uma ferramenta para criar HUDs visuais personalizados para Minecraft Bedrock Edition, utilizando o sistema de HUD JSON e o texto enviado através do comando /title.
A ideia principal é permitir que você associe imagens a determinados textos enviados pelo /title.
Por exemplo:
/title @s title 0
pode fazer uma imagem configurada com o Trigger 0 aparecer na tela.
Outro exemplo:
/title @s title 1
pode trocar para outra imagem.
O gerador cria automaticamente a estrutura JSON necessária para fazer essa ligação entre o texto do /title e a imagem.
🧩 1. Como o sistema funciona
O funcionamento básico é:
Comando /title
      ↓
Texto enviado
      ↓
HUD detecta o texto
      ↓
Binding verifica o valor
      ↓
Imagem correspondente fica visível
Cada imagem adicionada ao gerador possui um Trigger.
Exemplo:
Imagem
Trigger
tutorial.png
0
espada.png
1
mapa.png
2
Quando o HUD recebe:
/title @s title 0
a imagem associada ao Trigger 0 é exibida.
🖼️ 2. Adicionando uma imagem
Na seção Adicionar Imagem, existem alguns campos principais.
📁 Arquivo da imagem
Primeiro selecione a imagem que deseja utilizar.
O gerador aceita:
.png
.jpg
.jpeg
.webp
O arquivo selecionado é carregado no navegador para ser utilizado no Preview.
O nome do arquivo também é utilizado posteriormente para montar o caminho da textura no JSON.
Exemplo
Se você selecionar:
tutorial.png
o JSON será configurado para utilizar:
textures/ui/tutorial
Portanto, a textura deverá estar em:
textures/
└── ui/
    └── tutorial.png
🔑 3. Trigger
O Trigger é o texto que será utilizado para identificar qual imagem deve aparecer.
Exemplo:
Trigger: 0
A imagem será associada ao valor:
0
Então:
/title @s title 0
ativa essa imagem.
🔢 Exemplos de Triggers
Você pode utilizar:
0
1
2
3
tutorial
menu
mapa
boss
aviso
Também podem ser utilizados caracteres especiais.
O campo atualmente possui limite de 50 caracteres.
⚠️ Não repita Triggers
Cada imagem precisa possuir um Trigger diferente.
Por exemplo:
Imagem 1 → 0
Imagem 2 → 1
Imagem 3 → 2
Não faça:
Imagem 1 → menu
Imagem 2 → menu
O gerador impede a criação de dois itens com o mesmo Trigger.
📍 4. Posição X e Y
Os campos:
X
Y
controlam a posição da imagem.
X
Controla a posição horizontal.
X positivo → direita
X negativo → esquerda
Y
Controla a posição vertical.
Y positivo → baixo
Y negativo → cima
Exemplo:
X = 100
Y = 50
A imagem será posicionada com:
"offset": [100, 50]
No JSON gerado, esses valores são utilizados como o offset da imagem.
📐 5. Largura e altura
Os campos:
Largura
Altura
definem o tamanho da imagem.
Exemplo:
Largura: 500
Altura: 300
gera:
"size": [500, 300]
Esses valores são definidos individualmente para cada imagem.
➕ 6. Adicionar Imagem
Depois de configurar:
Arquivo
Trigger
X
Y
Largura
Altura
clique:
➕ Adicionar Imagem
A imagem será adicionada à lista do projeto.
O gerador atualmente permite até:
2000 imagens
O contador mostra algo como:
Imagens Adicionadas: 3/2000
👁️ 7. Preview
O botão:
👁️ Atualizar Preview
atualiza a visualização das imagens adicionadas.
O Preview possui uma área proporcional a:
16:9
e posiciona as imagens de acordo com os valores X, Y, largura e altura configurados.
Isso permite verificar aproximadamente como a composição ficará antes de gerar o JSON.
📋 8. Lista de imagens
A seção:
Imagens Adicionadas
mostra todas as imagens configuradas.
Cada item apresenta:
Trigger
Posição
Tamanho
Arquivo
Por exemplo:
Trigger: 0
Posição: 100, 50
Tamanho: 500x300
Arquivo: tutorial.png
Também existe o botão:
🗑️ Remover
para excluir uma imagem da configuração.
🗺️ 9. Trigger Map
O Trigger Map mostra todos os Triggers utilizados no projeto.
Exemplo:
0, 1, 2, tutorial, menu
Isso facilita verificar rapidamente quais valores já estão sendo utilizados.
🧱 10. Estrutura do JSON gerado
Ao clicar em:
📝 Gerar Arquivo Completo
o gerador cria um JSON contendo a estrutura do HUD.
A estrutura possui:
namespace
hud_title_text/title
root_panel
imagens
factories
animações
bindings
O namespace utilizado atualmente é:
"namespace": "hud"
🔗 11. Binding
O sistema utiliza bindings para decidir quando cada imagem deve ficar visível.
Um exemplo gerado é:
"bindings": [
    {
        "binding_name": "#hud_title_text_string"
    },
    {
        "binding_type": "view",
        "source_property_name": "(#hud_title_text_string = '0')",
        "target_property_name": "#visible"
    }
]
A parte mais importante é:
source_property_name
Ela verifica o texto atual do HUD.
Neste exemplo:
#hud_title_text_string = '0'
significa:
Mostre esta imagem quando o texto do /title for 0.
🎮 12. Usando com /title
Depois de colocar o HUD no seu Resource Pack, você pode utilizar comandos como:
/title @s title 0
ou:
/title @s title 1
ou:
/title @s title tutorial
dependendo dos Triggers configurados.
🔄 13. Exemplo completo
Imagine que você adicionou três imagens:
menu.png
espada.png
boss.png
Configuradas assim:
menu.png
Trigger: menu

espada.png
Trigger: espada

boss.png
Trigger: boss
Você poderá chamar:
/title @s title menu
Para mostrar:
menu.png
Depois:
/title @s title espada
Para mostrar:
espada.png
E:
/title @s title boss
Para mostrar:
boss.png
🗂️ 14. Onde colocar as imagens
As imagens utilizadas pelo HUD precisam estar disponíveis no Resource Pack na pasta:
textures/ui/
Exemplo:
MeuResourcePack/
│
├── manifest.json
│
├── hud_screen.json
│
└── textures/
    └── ui/
        ├── menu.png
        ├── espada.png
        └── boss.png
O JSON gerado utiliza automaticamente:
textures/ui/NOME_DA_IMAGEM
⚙️ 15. Como o gerador cria cada imagem
Cada imagem recebe uma configuração semelhante a:
{
    "type": "image",
    "texture": "textures/ui/tutorial",
    "anchor_from": "top_left",
    "anchor_to": "top_left",
    "size": [500, 300],
    "offset": [100, 50],
    "fill": true,
    "layer": 999999
}
type
Define que o controle é uma imagem:
"type": "image"
texture
Define a textura:
"texture": "textures/ui/tutorial"
anchor_from
Define a origem do posicionamento:
"anchor_from": "top_left"
anchor_to
Define o ponto de destino:
"anchor_to": "top_left"
size
Define o tamanho:
"size": [500, 300]
offset
Define o deslocamento:
"offset": [100, 50]
fill
Define o preenchimento da imagem:
"fill": true
layer
Define uma camada extremamente alta:
"layer": 999999
Essas propriedades são geradas automaticamente pela ferramenta.
🏭 16. Factories
O gerador também cria automaticamente uma factory para cada imagem.
Por exemplo:
v1_factory
v2_factory
v3_factory
Cada factory referencia a imagem correspondente.
Exemplo:
"v1_factory": {
    "type": "panel",
    "factory": {
        "name": "hud_title_text_factory",
        "control_ids": {
            "hud_title_text": "0@hud.0"
        }
    }
}
Isso permite inserir os controles criados dentro do root_panel.
🎬 17. Animação
O HUD também possui uma sequência de animação.
A configuração criada pelo gerador inclui:
"wait3": {
    "anim_type": "wait",
    "duration": 3,
    "next": "@hud.fade"
}
Depois:
"fade": {
    "anim_type": "alpha",
    "duration": 0.2,
    "from": 1,
    "to": 0
}
Isso cria uma espera de 3 segundos e depois uma transição de transparência para desaparecer.
📤 18. Gerar o JSON
Depois de configurar tudo, clique:
📝 Gerar Arquivo Completo
O JSON será colocado no campo:
JSON Gerado
O gerador não permite gerar o arquivo caso nenhuma imagem tenha sido adicionada.
📋 19. Copiar JSON
O botão:
📋 Copiar JSON
copia o conteúdo do JSON gerado para a área de transferência.
Se ainda não houver JSON, o gerador tenta criá-lo primeiro.
💾 20. Download JSON
O botão:
⬇️ Download JSON
salva o JSON como:
hud_screen.json
Esse arquivo pode então ser colocado no local apropriado do seu Resource Pack.
🖼️ 21. Imagens
É importante entender que o JSON não contém automaticamente os arquivos PNG/JPG/WebP.
O JSON apenas referencia as texturas:
textures/ui/nome_da_imagem
Por isso, as imagens precisam estar presentes no Resource Pack.
O botão:
⬇️ Download Todas as Imagens
na versão atual não cria um pacote ZIP das imagens. Ele apenas apresenta uma lista com os nomes dos arquivos e orienta que sejam colocados em:
textures/ui/
🚨 22. Erros comuns
❌ A imagem não aparece
Verifique:
A imagem está em:
textures/ui/
O nome do arquivo está correto.
O Trigger usado no /title é exatamente igual ao configurado.
Por exemplo:
Trigger:
tutorial
deve ser chamado como:
/title @s title tutorial
e não:
/title @s title Tutorial
❌ Duas imagens possuem o mesmo Trigger
Isso não é permitido.
Use valores diferentes:
0
1
2
3
ou:
menu
config
tutorial
boss
❌ A imagem está fora do lugar
Ajuste:
X
Y
Por exemplo:
X = 100
Y = -50
Move a imagem:
100 pixels para a direita
50 pixels para cima
❌ A imagem está muito grande
Diminua:
Largura
Altura
Por exemplo:
1920 × 1080
pode ser reduzido para:
960 × 540
💡 23. Exemplo de projeto
Um projeto simples pode utilizar:
Imagem              Trigger
─────────────────────────────
tutorial.png        tutorial
menu.png            menu
warning.png         warning
boss.png            boss
Comandos:
/title @s title tutorial
/title @s title menu
/title @s title warning
/title @s title boss
Cada comando fará o sistema verificar o texto recebido e mostrar a imagem correspondente.
🧠 24. Resumo rápido
1. Escolha uma imagem
        ↓
2. Defina o Trigger
        ↓
3. Defina X e Y
        ↓
4. Defina largura e altura
        ↓
5. Clique em "Adicionar Imagem"
        ↓
6. Confira o Preview
        ↓
7. Repita para outras imagens
        ↓
8. Clique em "Gerar Arquivo Completo"
        ↓
9. Copie ou baixe o JSON
        ↓
10. Coloque as imagens em textures/ui/
        ↓
11. Coloque o JSON no Resource Pack
        ↓
12. Use /title para ativar os Triggers
📚 Estrutura mental do HUD Generator
Pense no sistema desta forma:
HUD GENERATOR
                         │
                         ▼
                  IMAGEM CONFIGURADA
                         │
          ┌──────────────┼──────────────┐
          ▼              ▼              ▼
       Trigger        Posição         Tamanho
          │              │              │
          ▼              ▼              ▼
       "menu"       X / Y pixels     W / H pixels
          │
          ▼
       Binding
          │
          ▼
#hud_title_text_string
          │
          ▼
    /title @s title menu
          │
          ▼
     IMAGEM VISÍVEL
🛠️ 25. Recursos atualmente disponíveis
O HUD Generator possui atualmente:
🖼️ Adição de imagens
🔑 Triggers personalizados
📍 Posição X/Y
📐 Largura e altura
👁️ Preview
🗺️ Trigger Map
🗑️ Remoção de imagens
📊 Contador de imagens
📝 Geração automática de JSON
📋 Cópia do JSON
💾 Download do JSON
🎬 Animação de espera e fade
🔗 Bindings automáticos
🏭 Factories automáticas
📱 Estrutura de HUD baseada em hud_title_text
O limite configurado atualmente é de 2000 imagens por projeto.
⚠️ Observação importante
O HUD Generator não funciona como um sistema de comandos independente.
Ele gera a interface e configura os bindings necessários para reagir ao texto do HUD. Quem dispara a mudança é o comando /title.
Portanto:
Gerador
= cria o HUD

/title
= envia o texto

Binding
= verifica o texto

Imagem
= aparece quando o valor corresponde
Essa é a base do funcionamento do projeto.
