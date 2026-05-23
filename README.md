# CCNA Network Labs

Repositório de estudos práticos de redes, suporte, NOC e preparação para CCNA.

A ideia aqui é aprender redes fazendo: montar, quebrar, diagnosticar, corrigir e documentar.

## Objetivo

Construir uma base forte para:

- Suporte técnico e troubleshooting
- Monitoramento NOC
- Redes TCP/IP
- Cisco Packet Tracer
- Subnetting
- Switching e VLANs
- Routing
- Serviços IP
- Segurança básica
- Cloud networking e base para Cloud Security

## Método de estudo

Cada aula segue este formato:

1. Conceito direto
2. Exemplo real de suporte/NOC
3. Laboratório no Packet Tracer
4. Erro proposital
5. Troubleshooting
6. Perguntas estilo CCNA
7. Tarefa prática

## Trilha estimada

A trilha inicial tem cerca de 50 aulas práticas.

| Fase | Aulas | Tema |
|---|---:|---|
| Fundamentos de rede | 1-8 | IP, máscara, gateway, switch, roteador, ARP, TCP/UDP |
| Subnetting | 9-14 | CIDR, rede, broadcast, hosts e divisão de redes |
| Switching | 15-22 | MAC table, VLAN, trunk, STP e EtherChannel |
| Routing | 23-30 | Rotas, gateway, rota estática, default route e OSPF |
| Serviços IP | 31-36 | DHCP, DNS, NAT, NTP, SNMP e Syslog |
| Segurança | 37-41 | ACL, SSH, firewall e hardening básico |
| Wireless, cloud e automação | 42-46 | Wi-Fi, cloud, APIs, JSON e automação |
| Revisão e simulados | 47-50 | Labs mistos, troubleshooting e questões |

## Aulas documentadas

- [Aula 01 — O caminho do pacote](aulas/aula-01-caminho-do-pacote.md)
- [Aula 02 — Máscara, CIDR e subnetting sem trauma](aulas/aula-02-mascara-cidr-subnetting.md)

## Anotações

- [Comandos úteis](anotacoes/comandos.md)
- [Troubleshooting de rede](anotacoes/troubleshooting.md)
- [Glossário](anotacoes/glossario.md)
- [Tabela de subnetting](anotacoes/tabela-subnetting.md)

## Laboratórios Packet Tracer

Os arquivos `.pkt` serão adicionados manualmente conforme forem criados.

Sugestão de nomes:

```text
labs/lab-01-switch-mesma-rede.pkt
labs/lab-02-dois-switches-mesma-lan.pkt
labs/lab-03-subnetting-24-25-26.pkt
```

## Regra de estudo

```text
montar -> testar -> quebrar -> diagnosticar -> corrigir -> documentar
```

## Autor

Vinícius Fidelis  
GitHub: [vinionix](https://github.com/vinionix)
