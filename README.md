# CCNA Network Labs

Repositório de estudos práticos de redes, suporte, NOC e preparação para CCNA.

A proposta é aprender redes fazendo: montar topologias, testar comunicação, provocar falhas, diagnosticar problemas e documentar o raciocínio técnico.

## Objetivo

Construir uma base sólida em redes de computadores com foco em:

- suporte técnico;
- troubleshooting;
- fundamentos de NOC;
- Cisco Packet Tracer;
- TCP/IP;
- subnetting;
- switching;
- routing;
- serviços IP;
- segurança básica;
- base para cloud networking e cloud security.

## Método de estudo

Cada aula segue um formato prático:

1. conceito direto;
2. exemplo aplicado a suporte/NOC;
3. laboratório ou topologia sugerida;
4. erro proposital;
5. troubleshooting;
6. perguntas de revisão;
7. tarefa prática.

A regra do repositório é:

```text
montar -> testar -> quebrar -> diagnosticar -> corrigir -> documentar
```

## Trilha estimada

A trilha inicial foi pensada para aproximadamente 50 aulas práticas.

| Fase | Aulas | Tema |
| --- | ---: | --- |
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
- [Aula 03 — MAC Address, ARP e tabela MAC do switch](aulas/aula-03-mac-address-arp.md)

## Anotações

- [Comandos úteis](anotacoes/comandos.md)
- [Troubleshooting de rede](anotacoes/troubleshooting.md)
- [Glossário](anotacoes/glossario.md)
- [Tabela de subnetting](anotacoes/tabela-subnetting.md)

## Laboratórios Packet Tracer

Os arquivos `.pkt` devem ser adicionados conforme os laboratórios forem criados.

Sugestão de organização:

```text
labs/lab-01-switch-mesma-rede.pkt
labs/lab-02-dois-switches-mesma-lan.pkt
labs/lab-03-subnetting-24-25-26.pkt
labs/lab-04-arp-mac-table.pkt
```

## Status atual

Repositório em andamento.

Até o momento, há três aulas documentadas e anotações auxiliares para comandos, troubleshooting, glossário e subnetting. Os laboratórios Packet Tracer ainda dependem da inclusão manual dos arquivos `.pkt`.

## Evolução do projeto

- Definição da trilha prática para estudos de redes/CCNA.
- Criação das primeiras aulas documentadas.
- Inclusão de anotações auxiliares para consulta rápida.
- Fase atual: expansão gradual das aulas e futura inclusão dos laboratórios `.pkt`.

## Próximos passos

- Adicionar os arquivos Packet Tracer dos laboratórios já descritos.
- Continuar a sequência de aulas a partir dos fundamentos.
- Registrar erros comuns e troubleshooting real de suporte/NOC.
- Criar revisões periódicas com perguntas no estilo CCNA.

## Autor

Desenvolvido por [Vinícius Fidelis](https://github.com/vinionix).
