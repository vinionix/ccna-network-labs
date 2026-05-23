# Troubleshooting de rede

## Checklist inicial

Quando alguém disser "não conecta", pensar:

```text
1. O cabo/link está ativo?
2. O dispositivo tem IP?
3. A máscara está correta?
4. O gateway está correto?
5. O destino está na mesma rede?
6. Se o destino está em outra rede, existe roteador?
7. Existe rota até o destino?
8. O DNS resolve nomes?
9. Existe bloqueio de firewall?
10. O problema é local, de rede ou de serviço?
```

## Sintomas comuns

### Pinga IP, mas não abre site por nome

Possível causa:

```text
DNS
```

### Não pinga nem o gateway

Possíveis causas:

```text
IP errado
Máscara errada
Gateway errado
Cabo/link
VLAN errada
Interface desligada
```

### Dispositivos no mesmo switch não se comunicam

Verificar:

```text
Máscara
IP
VLAN
Firewall local
Cabo/link
```

### Dispositivos em redes diferentes não se comunicam

Verificar:

```text
Gateway
Roteador
Tabela de rotas
Firewall/ACL
Rota de retorno
```

## Registro técnico de incidente

Modelo:

```text
Incidente:
Horário:
Sintoma:
Impacto:
Testes realizados:
Resultado dos testes:
Causa provável:
Ação tomada:
Escalonamento:
```
