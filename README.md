# HUD Generator

Gerador visual de HUDs para Minecraft Bedrock Edition. Crie interfaces customizadas com efeitos de horror, glitchs e animações usando a UI Definition format.

## 🎮 Características

- **Preview em Tempo Real** - Visualize suas HUDs enquanto configura
- **Suporte a Múltiplas Imagens** - Adicione até 2000 imagens diferentes
- **Sistema de Triggers** - Mapear teclas e caracteres para ativar elementos
- **Geração Automática de JSON** - Crie arquivos prontos para usar no addon
- **Editor de UI Defs** - Configure `_ui_defs.json` diretamente no navegador
- **Download em Lote** - Baixe todas as imagens de uma vez

## 🚀 Como Usar

### 1. Adicionar Imagens

1. Clique em "Selecionar Arquivo" para escolher uma imagem (PNG, JPG ou WebP)
2. Configure o **Trigger** (a tecla/caractere que ativa a imagem)
3. Defina a **Posição** (X e Y em pixels)
4. Defina o **Tamanho** (largura e altura em pixels)
5. Clique em "➕ Adicionar Imagem"

### 2. Preview

Todas as suas imagens aparecem em tempo real no preview 16:9. Use "👁️ Atualizar Preview" se necessário.

### 3. Gerar JSON

Após adicionar suas imagens:
1. Clique em "📝 Gerar Arquivo Completo"
2. Copie com "📋 Copiar JSON" ou baixe com "⬇️ Download JSON"
3. Renomeie o arquivo para `hud_screen.json`
4. Coloque na pasta do seu addon

### 4. Adicionar ao Addon

**Estrutura de pastas do addon:**
```
meu_addon/
├── ui/
│   └── hud_screen.json
├── textures/
│   └── ui/
│       ├── imagem1.png
│       ├── imagem2.png
│       └── ...
└── manifest.json
```

### 5. Configurar _ui_defs.json

Use a aba **"Editor de UI Defs"** para configurar suas definições personalizadas:

```json
{
  "namespace": "custom",
  "images": [
    {
      "name": "my_hud",
      "texture": "textures/ui/my_image",
      "trigger": "0"
    }
  ]
}
```

## 📋 Estrutura do JSON Gerado

O gerador cria um arquivo com:

- **Namespace** - Espaço de nomes do addon (padrão: `hud`)
- **Controls** - Lista de elementos da HUD
- **Bindings** - Propriedades vinculadas (visibilidade baseada em triggers)
- **Animations** - Efeitos de fade e wait
- **Factories** - Controladores de elementos

Exemplo:
```json
{
  "namespace": "hud",
  "root_panel": {
    "modifications": [
      {
        "array_name": "controls",
        "operation": "insert_front",
        "value": [...]
      }
    ]
  },
  "0": {
    "type": "image",
    "texture": "textures/ui/minha_imagem",
    "size": [1920, 1080],
    "offset": [0, 0],
    "bindings": [...]
  }
}
```

## 🎨 Triggers Suportados

Use qualquer caractere como trigger:
- **Números**: `0-9`
- **Letras**: `a-z`, `A-Z`
- **Especiais**: `!@#$%^&*()` etc

Cada trigger ativa uma imagem específica. Use múltiplas imagens com o mesmo trigger para criar efeitos em sequência.

## 🔧 Configurações Avançadas

### Posição (Offset)
- **X**: Distância horizontal em pixels (0 = esquerda)
- **Y**: Distância vertical em pixels (0 = topo)

### Tamanho
- **Largura**: Em pixels (padrão: 1920)
- **Altura**: Em pixels (padrão: 1080)

### Animações
O gerador adiciona automaticamente:
- **wait3** - Espera 3 segundos
- **fade** - Desvanece em 0.2 segundos

Para modificar, edite o JSON gerado ou use a aba de Editor de UI Defs.

## 📝 Exemplo de Uso Completo

1. Crie 3 imagens de horror
2. Defina triggers: `H`, `O`, `R`
3. Gere o JSON
4. Adicione as imagens na pasta `textures/ui/`
5. Inclua o arquivo no seu addon
6. Quando o jogador digitar H, O ou R, a imagem correspondente aparece

## 🛠️ Requisitos

- Navegador moderno (Chrome, Firefox, Edge, Safari)
- Imagens em formato PNG, JPG ou WebP
- Minecraft Bedrock Edition (para usar o addon gerado)

## 📱 Compatibilidade

- ✅ Desktop
- ✅ Tablet
- ⚠️ Mobile (interface pequena, não recomendado)

## 🐛 Dúvidas Comuns

**P: Como adicionar sons junto com as imagens?**
R: Use a aba "Editor de UI Defs" para adicionar propriedades de som ao JSON.

**P: Quantas imagens posso adicionar?**
R: Até 2000 imagens. Quanto mais, mais pesado o addon.

**P: As imagens aparecem distorcidas?**
R: Defina o tamanho correto. O generator normaliza automaticamente o aspect ratio.

**P: Como fazer animações com fade?**
R: O JSON gerado já inclui animações de fade. Você pode customizar durações na aba de Editor.

## 📄 Licença

MIT - Use livremente em seus projetos

## 🤝 Contribuições

Pull requests são bem-vindos! Sinta-se à vontade para sugerir melhorias.

## 📞 Suporte

Dúvidas? Abra uma issue no repositório do GitHub.

---

**Versão**: 1.0.0  
**Última atualização**: 2026

