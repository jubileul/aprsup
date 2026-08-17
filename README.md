# aprsup

Firmware publicado da estação Multi-APRS. Este repositório guarda **apenas
artefatos** — o código-fonte fica em outro lugar e é privado.

As placas em campo leem o `latest.json` daqui sozinhas e se atualizam quando
sai versão nova.

## O que tem aqui

| Arquivo | O que é |
| --- | --- |
| `latest.json` | Manifesto: versão atual, endereço, tamanho, SHA-256 e assinatura |
| `firmware-X.Y.Z.bin` | A imagem em si |

## Por que isto é público, se o código não é

Porque não há nada a esconder aqui. O binário **já está** gravado na placa de
cada usuário, e sai de lá com o mesmo cabo USB que o gravou — publicá-lo não
revela nada que quem tem uma placa já não tenha.

A alternativa seria a placa autenticar num repositório privado, o que exigiria
um token embutido no firmware. Um token embutido é um token público, pela mesma
razão: a memória do ESP32 se lê com o cabo que a grava. E esse token daria acesso
de leitura ao código-fonte inteiro. Separar os dois repositórios troca uma
exposição que não custa nada por uma que custaria tudo.

## Nada aqui é confiável por estar aqui

Cada imagem é assinada com ECDSA P-256, e a chave pública correspondente vem
gravada dentro do firmware de cada placa. A placa **recalcula o SHA-256 da
imagem enquanto grava** e confere a assinatura antes de dar a versão nova como
boa. Uma imagem trocada, adulterada ou publicada por outra pessoa é recusada, e
a estação segue funcionando na versão que já tinha.

É por isso que este repositório poder ser público não é um risco: ele não
precisa ser confiável para o mecanismo ser seguro.

## Se você chegou aqui procurando o programa para gravar

Não é este arquivo. Existe um instalador que faz tudo pelo cabo USB, e um manual
com o passo a passo.

## Interessado?

Se você tem interesse na estação Multi-APRS, entre em contato:

**pp5eal.dev@gmail.com**
