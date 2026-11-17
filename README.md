# ajukas.grokbot

Widget da barra do Omarchy para o Grok Bot (app desktop `grok-bot`).

- Clique esquerdo: abre o Grok Bot ou mostra/esconde o popup.
- O Grok Bot abre como janela flutuante de 1300x850 no canto superior direito, no
  workspace especial `special:grokbot`. Ao focar outra janela ele some, mas continua
  rodando. Toda vez que abre, volta para o tamanho e a posição padrão.
- Se a janela for arrastada para fora do popup, ela volta para ele assim que perder o foco.
- Clicar no papel de parede ou numa área vazia também esconde o popup: o widget põe uma
  camada invisível embaixo das janelas enquanto ele está aberto.

A lógica de mostrar/esconder fica em `grokbot-popup.sh`; o tamanho e a margem são
configurados no topo dele.
- Clique direito: fecha a janela.
- Clique do meio: limpa o contador.
- Cada notificação do Grok Bot aumenta o contador no ícone; ele zera ao focar a janela.

O contador observa `~/.local/state/omarchy/notifications/` e conta as notificações cujo
app contém "grok".

## Instalação

```sh
ln -s ~/project/plugins/ajukas.grokbot ~/.config/omarchy/plugins/ajukas.grokbot
omarchy-shell shell rescanPlugins
omarchy plugin enable ajukas.grokbot
```

Como o plugin é um link simbólico, edições aqui não recarregam sozinhas; rode
`omarchy restart shell` depois de alterar o código.

## Regra do Hyprland

O popup depende desta regra em `~/.config/hypr/hyprland.lua`:

```lua
o.window("^grok-bot$", {
  workspace = "special:grokbot",
  float = true,
  size = { 1300, 850 },
  move = { "(monitor_w-window_w-12)", "38" },
})
```
