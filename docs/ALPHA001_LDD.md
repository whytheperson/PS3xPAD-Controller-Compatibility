# alpha001 — LDD table full

Durante o teste do PS3xPAD alpha001, o plugin:

1. leu corretamente o `xpad_devices.txt`;
2. aceitou o VID/PID personalizado;
3. registrou vários dispositivos internos;
4. atingiu o limite da tabela LDD USB do PS3;
5. deixou IDs posteriores sem registro.

O log apresentou:

```text
xpad_devices.txt entry accepted ...
LDD table full
XPAD Loaded!
```

## Consequência

Um dispositivo personalizado pode ser válido e ainda assim não ser registrado porque a tabela USB ficou cheia antes de chegar à sua entrada.

## Possível melhoria de código

Priorizar:

```text
1. dispositivos personalizados
2. dispositivos internos de alta prioridade
3. IDs internos menos comuns
```

Em pseudocódigo:

```c
register_custom_devices();
register_high_priority_builtin_devices();
register_low_priority_builtin_devices();
```

Outra opção é adicionar hardware confirmado diretamente à tabela interna prioritária.

Para o GameSir T4 Nova Lite em XInput:

```c
{0x3537, 0x1040, "GameSir T4 Nova Lite"}
```
