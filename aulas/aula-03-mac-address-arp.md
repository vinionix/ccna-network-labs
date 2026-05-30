# Aula 03 — MAC Address, ARP e tabela MAC do switch

## Objetivo

Entender como a comunicação acontece dentro da rede local.

Nas aulas anteriores:

```text
Aula 01: mesma rede conversa pelo switch; redes diferentes precisam de roteador/gateway.
Aula 02: a máscara define se dois IPs estão na mesma rede.
```

Agora a pergunta é:

> Se dois PCs estão na mesma rede, como o switch sabe para qual porta mandar os dados?

A resposta envolve:

```text
MAC Address
ARP
Tabela MAC do switch
```

## IP e MAC não são a mesma coisa

O IP é o endereço lógico da máquina na rede.

Exemplo:

```text
192.168.1.10
```

O MAC Address é o endereço físico da interface de rede.

Exemplo:

```text
00:1A:2B:3C:4D:5E
```

Resumo:

```text
IP  = endereço lógico
MAC = endereço físico da interface de rede
```

O IP pode mudar. O MAC normalmente vem gravado na placa de rede.

## O switch trabalha com MAC

Dentro de uma LAN, o switch encaminha tráfego usando MAC Address.

Exemplo:

```text
PC0 ---- Switch ---- PC1
```

Se o PC0 está conectado na porta `Fa0/1`, o switch aprende:

```text
O MAC do PC0 está na porta Fa0/1
```

Se o PC1 está conectado na porta `Fa0/2`, o switch aprende:

```text
O MAC do PC1 está na porta Fa0/2
```

Com isso, ele monta a tabela MAC.

## O que é a tabela MAC?

É a tabela que o switch usa para saber onde cada dispositivo está conectado.

| MAC Address | Porta |
|---|---|
| MAC do PC0 | Fa0/1 |
| MAC do PC1 | Fa0/2 |
| MAC do PC2 | Fa0/3 |

Quando o switch recebe um quadro destinado ao MAC do PC1, ele pensa:

> Eu sei onde esse MAC está. Está na Fa0/2.

Então ele envia somente para aquela porta.

## Como o switch aprende os MACs?

Ele aprende olhando o MAC de origem dos quadros que chegam.

Exemplo:

```text
Quadro chegou pela porta Fa0/1
MAC de origem: MAC do PC0
```

O switch grava:

```text
MAC do PC0 -> Fa0/1
```

Depois, quando o PC1 envia tráfego:

```text
Quadro chegou pela porta Fa0/2
MAC de origem: MAC do PC1
```

O switch grava:

```text
MAC do PC1 -> Fa0/2
```

O switch aprende observando o tráfego. Não precisa cadastrar manualmente em um lab comum.

## E se o switch não souber onde está o MAC?

Ele faz flood.

Flood significa:

> Enviar o quadro para todas as portas, exceto a porta por onde ele entrou.

Isso acontece quando o switch ainda não conhece o MAC de destino.

Quando o destino responde, o switch aprende o MAC e a porta correta.

## O que é ARP?

ARP significa:

```text
Address Resolution Protocol
```

Ele serve para descobrir:

> Qual MAC Address pertence a determinado IP?

Exemplo:

```text
PC0: 192.168.1.10
PC1: 192.168.1.20
```

PC0 sabe o IP do PC1, mas para enviar dentro da LAN precisa saber o MAC do PC1.

Então PC0 pergunta:

```text
Quem tem o IP 192.168.1.20?
Me diga seu MAC.
```

PC1 responde:

```text
Eu tenho 192.168.1.20.
Meu MAC é AA:BB:CC:DD:EE:FF.
```

Depois disso, PC0 consegue enviar o quadro corretamente.

## Fluxo completo de um ping na mesma rede

Topologia:

```text
PC0 ---- Switch ---- PC1
```

Configuração:

```text
PC0: 192.168.1.10/24
PC1: 192.168.1.20/24
```

Quando PC0 pinga PC1:

```text
1. PC0 verifica a máscara.
2. PC0 percebe que PC1 está na mesma rede.
3. PC0 precisa descobrir o MAC do PC1.
4. PC0 envia uma requisição ARP em broadcast.
5. O switch espalha esse broadcast pela LAN.
6. PC1 responde com seu MAC.
7. PC0 salva essa informação na tabela ARP.
8. PC0 envia o ping para o MAC do PC1.
9. O switch usa a tabela MAC para entregar pela porta correta.
10. PC1 responde.
```

## Broadcast do ARP

A requisição ARP é enviada em broadcast.

MAC de broadcast:

```text
FF:FF:FF:FF:FF:FF
```

Isso significa:

> Todo mundo na LAN recebe.

Mas só o dono daquele IP responde.

## Tabela ARP vs Tabela MAC

Tabela ARP fica no host e mapeia:

```text
IP -> MAC
```

Exemplo:

```text
192.168.1.20 -> AA:BB:CC:DD:EE:FF
```

Tabela MAC fica no switch e mapeia:

```text
MAC -> porta
```

Exemplo:

```text
AA:BB:CC:DD:EE:FF -> Fa0/2
```

Resumo:

```text
ARP Table: IP para MAC
MAC Table: MAC para porta
```

## Laboratório 3A — Ver ARP funcionando

Use a topologia:

```text
PC0 ---- Switch ---- PC1
```

Configure:

```text
PC0: 192.168.1.10/24
PC1: 192.168.1.20/24
```

No PC0:

```text
Desktop -> Command Prompt
```

Antes do ping:

```text
arp -a
```

Agora pingue o PC1:

```text
ping 192.168.1.20
```

Depois rode de novo:

```text
arp -a
```

Resultado esperado:

```text
PC0 agora conhece o MAC do IP 192.168.1.20.
```

## Laboratório 3B — Ver tabela MAC do switch

No switch:

```text
CLI
```

Entre no modo privilegiado:

```text
enable
```

Veja a tabela MAC:

```text
show mac address-table
```

Resultado esperado:

```text
O switch aprendeu os MACs dos PCs e as portas onde eles estão conectados.
```

Exemplo:

```text
Vlan    Mac Address       Type        Ports
----    -----------       --------    -----
1       xxxx.xxxx.xxxx    DYNAMIC     Fa0/1
1       yyyy.yyyy.yyyy    DYNAMIC     Fa0/2
```

## Laboratório 3C — Limpar a tabela MAC

No switch:

```text
enable
clear mac address-table dynamic
show mac address-table
```

Agora faça um ping novamente entre os PCs.

Depois rode:

```text
show mac address-table
```

O switch deve aprender os MACs novamente.

## Erro proposital

Mude o PC1 para outra rede:

```text
PC1: 192.168.2.20/24
```

PC0 continua:

```text
PC0: 192.168.1.10/24
```

Teste:

```text
ping 192.168.2.20
```

Vai falhar.

Motivo:

```text
PC0 percebe que 192.168.2.20 não está na mesma rede.
Sem gateway, ele não tem para onde enviar o tráfego remoto.
```

Moral:

```text
IP/máscara decide se é local ou remoto.
ARP resolve MAC para comunicação local.
Switch entrega usando tabela MAC.
```

## Exemplo real de suporte/NOC

Usuário diz:

> Meu computador está com IP, mas não comunica na rede.

Checklist:

```text
1. O cabo está conectado?
2. A interface está ativa?
3. O IP está correto?
4. A máscara está correta?
5. Está na mesma rede do destino?
6. O PC aprende ARP?
7. O switch aprende o MAC desse PC?
8. A porta está na VLAN correta?
9. O firewall local está bloqueando?
```

Se o switch não aprende o MAC do PC, pode ser:

```text
cabo ruim
porta errada
placa de rede desativada
interface desligada
VLAN errada
problema físico
```

Se o PC não aprende ARP, pode ser:

```text
destino fora da rede
máscara errada
firewall bloqueando
VLAN errada
host desligado
```

## Importante para cibersegurança

ARP é importante para segurança porque existe um ataque chamado ARP spoofing.

A ideia do ataque é enganar a rede local com uma associação falsa de IP e MAC.

Exemplo conceitual:

```text
Atacante diz:
"Eu sou o gateway. Mande o tráfego para meu MAC."
```

Isso pode permitir Man-in-the-Middle, captura de tráfego inseguro, redirecionamento e indisponibilidade.

## Perguntas estilo CCNA

### 1. O switch encaminha frames usando qual endereço?

```text
MAC Address
```

### 2. O ARP serve para quê?

```text
Descobrir o MAC Address associado a um endereço IP.
```

### 3. A tabela ARP fica onde?

```text
Nos hosts, como PCs, servidores e roteadores.
```

### 4. A tabela MAC fica onde?

```text
No switch.
```

### 5. O que acontece quando o switch não conhece o MAC de destino?

```text
Ele faz flood para todas as portas, exceto a porta de origem.
```

### 6. Qual é o MAC de broadcast?

```text
FF:FF:FF:FF:FF:FF
```

### 7. Se dois PCs estão em redes diferentes, o ARP resolve diretamente o MAC do destino final?

```text
Não.
```

Se o destino está em outra rede, o host envia o tráfego para o gateway. Nesse caso, ele usa ARP para descobrir o MAC do gateway, não do destino final.

## Tarefa da Aula 3

Monte no Packet Tracer:

```text
PC0 ---- Switch ---- PC1
```

Configure:

```text
PC0: 192.168.1.10/24
PC1: 192.168.1.20/24
```

Faça:

```text
1. No PC0, rode arp -a antes do ping.
2. Pingue o PC1.
3. Rode arp -a depois do ping.
4. No switch, rode show mac address-table.
5. Limpe a tabela MAC.
6. Pingue novamente.
7. Veja a tabela MAC de novo.
```

Depois responda:

```text
1. O que apareceu na tabela ARP do PC0?
2. O que apareceu na tabela MAC do switch?
3. Qual porta estava associada ao PC0?
4. Qual porta estava associada ao PC1?
5. O primeiro ping falhou ou demorou mais? Por quê?
```

## Resumo

```text
IP identifica logicamente um host.
MAC identifica a interface de rede.
ARP descobre o MAC associado a um IP.
Switch encaminha usando MAC.
Switch aprende MAC observando o tráfego.
Tabela ARP fica nos hosts.
Tabela MAC fica no switch.
Se o switch não conhece o MAC, ele faz flood.
```

Frase para guardar:

> O host decide com IP e máscara. O ARP descobre o MAC. O switch entrega usando a tabela MAC.
