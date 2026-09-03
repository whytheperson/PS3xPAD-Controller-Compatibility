# Como contribuir com novos controles

Abra uma Issue usando o template **Controller compatibility report**.

Inclua:

- Nome exato do controle
- Fabricante
- Com fio / dongle / Bluetooth
- Cor do LED ou modo selecionado
- VID
- PID
- Nome mostrado pelo Windows
- HEN ou CFW
- Versão de firmware do PS3
- Versão do PS3xPAD
- Linha usada no `xpad_devices.txt`
- Funciona no XMB?
- Funciona dentro dos jogos?
- Analógicos
- D-pad
- Triggers
- Botão PS/Home
- Rumble
- Problemas encontrados

## Exemplo

```text
Controller: GameSir T4 Nova Lite
Connection: USB wired
Mode: XInput / green LED
VID: 3537
PID: 1040
Windows: Xbox 360 Controller for Windows
PS3: HEN
Config:
0x3537, 0x1040, GameSir T4 Nova Lite, XTYPE_XBOX360
```

Depois de confirmado por pelo menos um teste real, o controle pode ser adicionado à tabela de compatibilidade.
