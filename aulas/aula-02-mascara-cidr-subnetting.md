# Aula 02 — Máscara, CIDR e subnetting sem trauma

## Objetivo

Entender como o computador sabe se outro IP está na mesma rede ou em outra rede.

A resposta é: máscara de sub-rede.

## O que é máscara?

A máscara separa o IP em duas partes:

```text
parte da rede + parte do host
```

Exemplo:

```text
IP:       192.168.1.10
Máscara: 255.255.255.0
CIDR:    /24
```

Com `/24`, os três primeiros blocos identificam a rede:

```text
192.168.1
```

E o último bloco identifica o host:

```text
10
```

Então:

```text
192.168.1.10/24
```

Significa:

```text
Rede: 192.168.1.0
Host: 10
```

## O que é CIDR?

CIDR é a notação com barra:

```text
/24
/25
/26
/27
/28
```

Exemplo:

```text
192.168.1.10/24
```

O `/24` significa que os primeiros 24 bits são a parte da rede.

## Tabela inicial

| CIDR | Máscara | Bits de host | Hosts válidos | Bloco |
|---|---|---:|---:|---:|
| /23 | 255.255.254.0 | 9 | 510 | 512 |
| /24 | 255.255.255.0 | 8 | 254 | 256 |
| /25 | 255.255.255.128 | 7 | 126 | 128 |
| /26 | 255.255.255.192 | 6 | 62 | 64 |
| /27 | 255.255.255.224 | 5 | 30 | 32 |
| /28 | 255.255.255.240 | 4 | 14 | 16 |
| /29 | 255.255.255.248 | 3 | 6 | 8 |
| /30 | 255.255.255.252 | 2 | 2 | 4 |

## Fórmula de hosts

O IPv4 tem 32 bits.

```text
bits de host = 32 - CIDR
hosts válidos = 2^(bits de host) - 2
```

Exemplo `/26`:

```text
32 - 26 = 6 bits de host
2^6 - 2 = 62 hosts válidos
```

Subtrai 2 porque:

```text
1 endereço é da rede
1 endereço é de broadcast
```

## Como descobrir o bloco

Regra prática:

```text
Bloco = 256 - valor do octeto interessante da máscara
```

Exemplo `/26`:

```text
Máscara: 255.255.255.192
Bloco = 256 - 192
Bloco = 64
```

Então as redes pulam de 64 em 64:

```text
192.168.1.0
192.168.1.64
192.168.1.128
192.168.1.192
```

## Exemplo com /24

```text
Rede: 192.168.1.0/24
Máscara: 255.255.255.0
```

Faixa:

```text
Rede:      192.168.1.0
1º host:   192.168.1.1
Último:    192.168.1.254
Broadcast: 192.168.1.255
```

Hosts válidos:

```text
2^8 - 2 = 254
```

## Exemplo com /25

```text
Máscara: 255.255.255.128
Bloco: 256 - 128 = 128
```

Redes:

```text
192.168.1.0/25
192.168.1.128/25
```

Primeira rede:

```text
Rede:      192.168.1.0
1º host:   192.168.1.1
Último:    192.168.1.126
Broadcast: 192.168.1.127
```

Segunda rede:

```text
Rede:      192.168.1.128
1º host:   192.168.1.129
Último:    192.168.1.254
Broadcast: 192.168.1.255
```

## Exemplo com /26

```text
Máscara: 255.255.255.192
Bloco: 256 - 192 = 64
```

Redes:

```text
192.168.1.0/26
192.168.1.64/26
192.168.1.128/26
192.168.1.192/26
```

Faixas:

```text
Rede 1:
Rede:      192.168.1.0
Hosts:     192.168.1.1 até 192.168.1.62
Broadcast: 192.168.1.63
```

```text
Rede 2:
Rede:      192.168.1.64
Hosts:     192.168.1.65 até 192.168.1.126
Broadcast: 192.168.1.127
```

```text
Rede 3:
Rede:      192.168.1.128
Hosts:     192.168.1.129 até 192.168.1.190
Broadcast: 192.168.1.191
```

```text
Rede 4:
Rede:      192.168.1.192
Hosts:     192.168.1.193 até 192.168.1.254
Broadcast: 192.168.1.255
```

## Exemplo com /23

```text
/23 = 255.255.254.0
```

O octeto interessante é o terceiro:

```text
Bloco = 256 - 254 = 2
```

Então as redes pulam de 2 em 2 no terceiro octeto:

```text
192.168.0.0/23
192.168.2.0/23
192.168.4.0/23
192.168.6.0/23
```

Exemplo:

```text
Rede:      192.168.0.0/23
1º host:   192.168.0.1
Último:    192.168.1.254
Broadcast: 192.168.1.255
```

Hosts válidos:

```text
2^9 - 2 = 510
```

## Como saber em qual rede um IP está?

Exemplo:

```text
IP: 192.168.1.70/26
```

Sabemos que `/26` tem bloco 64.

As faixas são:

```text
192.168.1.0 até 192.168.1.63
192.168.1.64 até 192.168.1.127
192.168.1.128 até 192.168.1.191
192.168.1.192 até 192.168.1.255
```

O IP `192.168.1.70` cai aqui:

```text
192.168.1.64 até 192.168.1.127
```

Então:

```text
Rede:      192.168.1.64
1º host:   192.168.1.65
Último:    192.168.1.126
Broadcast: 192.168.1.127
```

## Laboratório 2A — /24

Use a topologia:

```text
PC0 ---- Switch0 ---- Switch1 ---- PC2
          |
         PC1
```

Configuração:

```text
PC0: 192.168.1.10/24
PC1: 192.168.1.20/24
PC2: 192.168.1.30/24
```

Resultado esperado:

```text
Todos pingam todos.
```

## Laboratório 2B — /25

Configuração:

```text
PC0: 192.168.1.10/25
PC1: 192.168.1.20/25
PC2: 192.168.1.130/25
```

Resultado esperado:

```text
PC0 pinga PC1.
PC0 não pinga PC2.
PC1 não pinga PC2.
```

Motivo:

```text
PC0 e PC1: 192.168.1.0/25
PC2:       192.168.1.128/25
```

## Laboratório 2C — /26

Máscara:

```text
255.255.255.192
```

Configuração:

```text
PC0: 192.168.1.10/26
PC1: 192.168.1.50/26
PC2: 192.168.1.70/26
```

Resultado esperado:

```text
PC0 pinga PC1.
PC0 não pinga PC2.
PC1 não pinga PC2.
```

Motivo:

```text
PC0: 192.168.1.10 -> rede 192.168.1.0/26
PC1: 192.168.1.50 -> rede 192.168.1.0/26
PC2: 192.168.1.70 -> rede 192.168.1.64/26
```

## Método rápido para prova

Quando aparecer:

```text
192.168.1.150/27
```

Faça:

```text
/27 = 255.255.255.224
Bloco = 256 - 224 = 32
```

Pule de 32 em 32:

```text
0
32
64
96
128
160
192
224
```

O IP 150 cai entre 128 e 159.

Então:

```text
Rede:      192.168.1.128
1º host:   192.168.1.129
Último:    192.168.1.158
Broadcast: 192.168.1.159
```

## Checklist de subnetting

```text
1. Veja o CIDR.
2. Descubra a máscara.
3. Faça 256 - valor do octeto interessante.
4. Pule de bloco em bloco.
5. Ache onde o IP cai.
6. O primeiro número do bloco é a rede.
7. O número antes do próximo bloco é o broadcast.
8. Host válido fica entre rede + 1 e broadcast - 1.
```

## Perguntas estilo CCNA

### 1. Esses hosts estão na mesma rede?

```text
PC1: 192.168.1.10/24
PC2: 192.168.1.200/24
```

Resposta: sim.

### 2. Esses hosts estão na mesma rede?

```text
PC1: 192.168.1.10/25
PC2: 192.168.1.130/25
```

Resposta: não.

### 3. Qual o broadcast da rede 192.168.1.0/25?

Resposta:

```text
192.168.1.127
```

### 4. Qual máscara corresponde a /26?

Resposta:

```text
255.255.255.192
```

### 5. /23 corresponde a qual máscara?

Resposta:

```text
255.255.254.0
```

## Resumo

```text
Máscara define o tamanho da rede.
CIDR é a notação com barra.
Mesmo switch não garante comunicação.
Mesma faixa visual também não garante comunicação.
A máscara manda no jogo.
```

## Importante para cibersegurança e cloud

Subnetting é base para entender:

- VPC
- Subnets públicas e privadas
- Firewall
- Segmentação de rede
- Exposição de serviços
- Cloud Security
