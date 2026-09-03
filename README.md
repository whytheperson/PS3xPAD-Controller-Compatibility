# PS3xPAD Controller Compatibility for PS3 HEN

Projeto comunitário para documentar e testar controles não oficiais no PlayStation 3 usando PS3xPAD.

## Primeiro controle documentado

### GameSir T4 Nova Lite

| Item | Valor |
|---|---|
| Conexão testada | USB |
| Modo | XInput / LED verde |
| VID | `3537` |
| PID | `1040` |
| Tipo PS3xPAD | `XTYPE_XBOX360` |
| HEN inicia com plugin | ✅ Confirmado |
| Mapeamento completo em jogos | 🧪 Em validação |
| Modo amarelo/HID | `3537:1041` — não recomendado para PS3xPAD |

Entrada:

```text
0x3537, 0x1040, GameSir T4 Nova Lite, XTYPE_XBOX360
```

## Documentação

- [Instalação no PS3 HEN](docs/INSTALL_PTBR.md)
- [Compatibilidade e outros controles](docs/COMPATIBILITY.md)
- [Descobrir VID/PID no Windows](docs/VID_PID_WINDOWS.md)
- [Problema LDD table full do alpha001](docs/ALPHA001_LDD.md)
- [Como contribuir com novos controles](docs/CONTRIBUTING_CONTROLLERS.md)

## Configuração pronta

Arquivo:

```text
configs/xpad_devices_gamesir_t4_nova_lite.txt
```

Conteúdo:

```text
0x3537, 0x1040, GameSir T4 Nova Lite, XTYPE_XBOX360
```

## Aviso sobre binários

Este repositório documenta configuração e compatibilidade.

Os binários `.sprx` do PS3xPAD não são incluídos aqui por padrão. Use uma distribuição do PS3xPAD apropriada ao seu ambiente e confirme os termos de redistribuição do projeto original antes de republicar binários.

## Créditos

PS3xPAD foi desenvolvido por OsirisX e possui contribuições/manutenção comunitária.

Este repositório documenta testes de compatibilidade de controles e não reivindica autoria do PS3xPAD.
