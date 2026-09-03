# Publicação no GitHub

## Repositório

Envie todo o conteúdo deste pacote para a raiz do repositório.

A estrutura deve aparecer assim:

```text
README.md
configs/
docs/
.github/
```

## Release

Recomendação:

1. Vá em `Releases`.
2. Clique em `Draft a new release`.
3. Tag sugerida: `v0.1-gamesir-t4-nova-lite`
4. Título: `GameSir T4 Nova Lite compatibility notes`
5. No corpo da release, informe:
   - `3537:1040` = XInput verde
   - `3537:1041` = HID/DInput amarelo
   - HEN boot confirmado
   - mapeamento completo ainda deve ser marcado como teste até validado.

## Binários PS3xPAD

Por segurança de redistribuição, este pacote não inclui os `.sprx` originais.

Se você tiver permissão para redistribuí-los, pode anexar um pacote separado em Releases.
Caso contrário, mantenha somente configuração/documentação e direcione o usuário à distribuição original do PS3xPAD.
