# CCNA Network Labs

Repositório de estudos práticos de redes, suporte, NOC e preparação para CCNA.

A proposta não é estudar redes apenas por teoria ou decorar comandos. O método principal é construir topologias, prever o comportamento esperado, provocar falhas, diagnosticar a causa e documentar a correção.

## Objetivo

Construir uma base sólida em redes de computadores com foco em:

- suporte técnico;
- troubleshooting;
- fundamentos de NOC;
- Cisco Packet Tracer;
- TCP/IP;
- IPv4 e subnetting;
- switching;
- routing;
- serviços IP;
- segurança básica;
- cloud networking;
- base para cloud security e infraestrutura de sistemas de IA.

## Método de estudo

Cada aula segue, quando possível, o fluxo:

1. conceito direto;
2. caminho esperado do pacote;
3. exemplo aplicado a suporte/NOC;
4. laboratório ou topologia;
5. erro proposital;
6. troubleshooting;
7. correção;
8. verificação;
9. perguntas de revisão;
10. documentação do aprendizado.

A regra do repositório é:

```text
montar → testar → quebrar → diagnosticar → corrigir → documentar
```

## Método de troubleshooting

Antes de sair executando comandos aleatoriamente, a ideia é responder:

1. qual é exatamente o sintoma?
2. qual origem e destino deveriam se comunicar?
3. qual caminho o pacote deveria percorrer?
4. IP e máscara estão corretos?
5. ARP/tabela MAC fazem sentido?
6. gateway e rota estão corretos?
7. o problema é conectividade ou DNS?
8. existe ACL, NAT, firewall ou serviço interferindo?
9. qual teste confirma que a causa foi corrigida?

Esse processo transforma cada laboratório em prática de raciocínio operacional.

## Trilha estimada

A trilha inicial foi pensada para aproximadamente 50 aulas práticas.

| Fase | Aulas | Tema |
| --- | ---: | --- |
| Fundamentos de rede | 1-8 | IP, máscara, gateway, switch, roteador, ARP, TCP/UDP |
| Subnetting | 9-14 | CIDR, rede, broadcast, hosts e divisão de redes |
| Switching | 15-22 | MAC table, VLAN, trunk, STP e EtherChannel |
| Routing | 23-30 | rotas, gateway, rota estática, default route e OSPF |
| Serviços IP | 31-36 | DHCP, DNS, NAT, NTP, SNMP e Syslog |
| Segurança | 37-41 | ACL, SSH, firewall e hardening básico |
| Wireless, cloud e automação | 42-46 | Wi-Fi, cloud, APIs, JSON e automação |
| Revisão e simulados | 47-50 | labs mistos, troubleshooting e questões |

## Aulas documentadas

- [Aula 01 — O caminho do pacote](aulas/aula-01-caminho-do-pacote.md)
- [Aula 02 — Máscara, CIDR e subnetting sem trauma](aulas/aula-02-mascara-cidr-subnetting.md)
- [Aula 03 — MAC Address, ARP e tabela MAC do switch](aulas/aula-03-mac-address-arp.md)

## Anotações

- [Comandos úteis](anotacoes/comandos.md)
- [Troubleshooting de rede](anotacoes/troubleshooting.md)
- [Glossário](anotacoes/glossario.md)
- [Tabela de subnetting](anotacoes/tabela-subnetting.md)

## Padrão desejado para laboratórios

Cada lab deve evoluir para conter:

- objetivo;
- descrição da topologia;
- tabela de endereçamento;
- configurações relevantes;
- comportamento esperado;
- falha introduzida;
- comandos de diagnóstico;
- causa raiz;
- correção;
- teste final.

Isso deixa o repositório útil não apenas como material de estudo, mas como evidência de troubleshooting.

## Laboratórios Packet Tracer

Os arquivos `.pkt` devem ser adicionados conforme os laboratórios forem criados.

Organização sugerida:

```text
labs/lab-01-switch-mesma-rede.pkt
labs/lab-02-dois-switches-mesma-lan.pkt
labs/lab-03-subnetting-24-25-26.pkt
labs/lab-04-arp-mac-table.pkt
```

## Relação com cloud e IA

Mesmo com o foco profissional migrando para Engenharia de IA, essa trilha continua relevante. Sistemas de IA em produção dependem de conceitos como:

- DNS;
- portas e protocolos;
- roteamento;
- proxies;
- containers e redes virtuais;
- cloud networking;
- observabilidade;
- controle de acesso;
- troubleshooting entre serviços.

Entender rede reduz a dependência de tentativa e erro quando uma aplicação funciona localmente, mas falha ao ser distribuída ou implantada.

## Status

Repositório em andamento. Atualmente existem três aulas documentadas e materiais auxiliares de comandos, troubleshooting, glossário e subnetting. Os arquivos Packet Tracer ainda precisam ser incluídos conforme os labs forem executados.

## O que este projeto demonstra

- fundamentos de redes;
- raciocínio orientado ao caminho do pacote;
- troubleshooting baseado em hipóteses;
- documentação técnica;
- preparação para CCNA;
- conexão entre suporte/NOC, infraestrutura, cloud e engenharia de sistemas.

## Documentação

- [Technical Overview](docs/TECHNICAL_OVERVIEW.md) — estratégia de estudo, método de troubleshooting e padrão para documentação dos labs.

## Próximos passos

- adicionar os arquivos Packet Tracer dos laboratórios;
- continuar a sequência de aulas;
- documentar falhas reais e root cause analysis;
- criar revisões periódicas;
- incluir cenários integrando redes, Docker e serviços de aplicação.

## Autor

Desenvolvido por [Vinícius Fidelis](https://github.com/vinionix).
