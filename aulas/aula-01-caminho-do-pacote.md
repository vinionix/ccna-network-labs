# Aula 01 — O caminho do pacote

## Objetivo

Entender a primeira regra forte de redes:

> Dispositivos na mesma rede conversam pelo switch.  
> Dispositivos em redes diferentes precisam de roteador/gateway.

Essa ideia é base para CCNA, NOC, suporte, cloud e segurança.

## Topologia inicial

```text
PC1 ---- Switch ---- PC2
```

O switch conecta dispositivos dentro da mesma rede local, chamada de LAN.

## Exemplo funcionando

```text
PC1: 192.168.1.10/24
PC2: 192.168.1.20/24
Máscara: 255.255.255.0
```

Os dois estão na rede:

```text
192.168.1.0/24
```

Então eles conseguem se comunicar.

## Regra principal

```text
Mesma rede = switch resolve.
Rede diferente = precisa de roteador.
```

## Exemplo que não funciona só com switch

```text
PC1: 192.168.1.10/24
PC2: 192.168.2.20/24
```

Eles estão em redes diferentes:

```text
PC1 -> 192.168.1.0/24
PC2 -> 192.168.2.0/24
```

Mesmo que estejam no mesmo switch, não vão se comunicar sem roteador/gateway.

## Onde entra o gateway?

O gateway é a saída da rede. Normalmente é o roteador.

Exemplo:

```text
PC1
IP:       192.168.1.10
Máscara: 255.255.255.0
Gateway: 192.168.1.1
```

Quando o PC quer falar com algo fora da própria rede, ele envia o tráfego para o gateway.

## Laboratório 1A — Dois PCs na mesma rede

### Montagem

```text
PC0 ---- Switch ---- PC1
```

### PC0

```text
IP Address: 192.168.1.10
Subnet Mask: 255.255.255.0
Default Gateway: 0.0.0.0
```

### PC1

```text
IP Address: 192.168.1.20
Subnet Mask: 255.255.255.0
Default Gateway: 0.0.0.0
```

### Teste

No PC0:

```text
ping 192.168.1.20
```

Resultado esperado:

```text
Reply from 192.168.1.20
```

## Laboratório 1B — Quebrando a rede

Mude o PC1 para:

```text
IP Address: 192.168.2.20
Subnet Mask: 255.255.255.0
```

No PC0:

```text
ping 192.168.2.20
```

Resultado esperado:

```text
Falha
```

Motivo:

```text
PC0 está na rede 192.168.1.0/24
PC1 está na rede 192.168.2.0/24
```

Sem roteador, redes diferentes não se comunicam.

## Laboratório 1C — Dois switches na mesma LAN

Topologia feita no Packet Tracer:

```text
PC1
 |
Switch0 ---- Switch1 ---- PC2
 |
PC0
```

Sem VLAN configurada, todos estão na VLAN 1, a VLAN padrão.

Configuração sugerida:

```text
PC0: 192.168.1.10/24
PC1: 192.168.1.20/24
PC2: 192.168.1.30/24
```

Resultado esperado:

```text
PC0 pinga PC1: sim
PC0 pinga PC2: sim
PC1 pinga PC2: sim
```

Conclusão:

```text
Dois switches podem formar a mesma LAN.
Switch não separa rede por si só.
Sem VLAN, todos ficam na VLAN padrão.
```

## Checklist de diagnóstico

Quando dois dispositivos não se comunicarem:

```text
1. O cabo está conectado?
2. A interface está ligada?
3. Os dois têm IP?
4. A máscara está correta?
5. Eles estão na mesma rede?
6. Se estão em redes diferentes, existe gateway?
7. O gateway está configurado corretamente?
8. Existe roteador entre as redes?
```

## Perguntas estilo CCNA

### 1. Dois PCs no mesmo switch conseguem se comunicar?

```text
PC1: 192.168.1.10/24
PC2: 192.168.1.20/24
```

Resposta: sim. Estão na mesma rede.

### 2. Dois PCs no mesmo switch conseguem se comunicar sem roteador?

```text
PC1: 192.168.1.10/24
PC2: 192.168.2.20/24
```

Resposta: não. Estão em redes diferentes.

### 3. Qual equipamento conecta dispositivos dentro da mesma rede?

Resposta: switch.

### 4. Qual equipamento conecta redes diferentes?

Resposta: roteador ou switch camada 3.

### 5. Para que serve o gateway padrão?

Resposta: para encaminhar tráfego destinado a outras redes.

## Resumo

```text
Switch conecta dispositivos na mesma rede.
Roteador conecta redes diferentes.
Gateway é a saída da rede.
Mesma rede conversa direto.
Rede diferente precisa de roteamento.
```
