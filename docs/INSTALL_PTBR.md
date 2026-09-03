# Instalação — PS3 HEN

> Exemplo documentado com GameSir T4 Nova Lite.

## 1. Estrutura do plugin

No PS3:

```text
/dev_hdd0/plugins/ps3xpad/
├── xpad_vsh.sprx
├── xpad_game.sprx
├── xpad_devices.txt
├── xpad_settings.txt
└── xpad_remap.txt
```

## 2. xpad_devices.txt

Para o GameSir T4 Nova Lite em XInput verde:

```text
0x3537, 0x1040, GameSir T4 Nova Lite, XTYPE_XBOX360
```

## 3. boot_plugins.txt

Edite:

```text
/dev_hdd0/boot_plugins.txt
```

Não apague as outras linhas existentes.

Exemplo com webMAN:

```text
/dev_hdd0/plugins/webftp_server.sprx
/dev_hdd0/plugins/ps3xpad/xpad_vsh.sprx
```

Se uma versão anterior do PS3xPAD estiver carregada:

```text
/dev_hdd0/plugins/xpad.sprx
```

remova essa linha para evitar carregar dois plugins XPAD ao mesmo tempo.

## 4. Reinicie

1. Desligue completamente o PS3.
2. Ligue novamente.
3. Ative o HEN.
4. Espere o XMB carregar.
5. Conecte o controle.
6. Use o modo XInput correto.

## GameSir T4 Nova Lite

Use:

```text
LED verde
VID:PID = 3537:1040
```

Evite, para este teste:

```text
LED amarelo
VID:PID = 3537:1041
```

Esse segundo modo é HID/DInput e possui outro formato de entrada.

## 5. Dentro do jogo

Se o VSH funcionar mas o jogo não enxergar corretamente o controle, espere o jogo carregar completamente e teste:

```text
START + SELECT + R3
```

Algumas versões do PS3xPAD usam essa combinação para anexar o módulo ao processo do jogo.

## Recuperação

Faça backup de `boot_plugins.txt` antes de alterar plugins de boot.

Se um SPRX impedir o HEN de ativar, restaure a configuração anterior antes de continuar.

Nunca carregue simultaneamente duas versões diferentes do plugin XPAD.
