# Comandos Cisco IOS

Esse são os comandos utilizados no 1° e 2° Semestre do Curso Técnico de Redes de Computadores - SENAI Informática 

## Configurações Iniciais (Switch e Router)

**Entrar no modo Exec Privilegiado**
```
>enable
```

**Mostrar as configurações que estão ativas no equipamentos**
```
#show running-config
```

**Mostrar as configurações que estão salvas no equipamentos**
```
#show startup-config
```

**Salvas as configurações que estão do equipamentos**
```
#copy running-config startup-config
ou
#write memory
ou
#wr
```

**Reiniciar o equipamento**
```
#reload
```

**Apagar todas as configurações salvas**
```
#write erase
```

**Destravar o terminal**
```
Ctrl+Shift+6
```

**Ir para a tela de configuração do equipamento**
```
#configure terminal
ou
#conf t
```

**Mudar nome do equipamentos**
```
(config)#hostname [nome]
```

**Inserir um banner de entrada**
```
(config)#banner motd "[mensagem]"
```

**Inserir senha de Enable**
```
(config)#enable secret [senha] (Criptografada)
(config)#enable password [senha] (Sem criptografia)
```

**Definir o tempo na troca de informações entre os equipamentos**
```
(config-if)# clock rate [tempo]
``` 

**Inserir senha na console**
```
(config)#line console [número-da-console]
(config-line)#password [senha]
(config-line)#login
```

**Encriptar todas as senhas que estão em texto plano**
```
(config)#service password-encryption
```

**Anular qualquer commando no CISCO IOS**
```
'no' na frente do comando
Exemplo: no hostname SW-01 --> (Apagar o nome configurado no Switch)
```

**Voltar para a tela de EXEC-Privilegiado**
```
Atalho no Teclado: Ctrl+Z
ou
Comando: end
```

**Voltar para a tela anterior**
```
Comando: exit
```

**Mostrar a tabela MAC do Switch**
```
#show mac-address-table (IOS 12.2)
#show mac address-table dynamic (IOS 15.0)
```

**Ver MAC de todas as interfaces (interfaces conectadas e não ativas)** 
```
#show interfaces | in line protocol | address
```

**Ver apenas interfaces do tipo FastEthernet**
```
#show interfaces | in FastEthernet
```

**Ver arquivos na memória Flash**
```
#dir flash
```

**Ver arquivos na memória NVRAM**
```
#dir nvram
```

**Desativar a paginação (--MORE--)**
```
#terminal length 0
```

**Desativar as mensagens de erro na tela**
```
(config)#no logging console
```

**Configurar várias Interfaces ao mesmo tempo**
**Exemplo**: Configurar todas as interfaces entre a f0/1 e a f0/5
```
(config)#interface range f0/1-5
```

**Mostrar resumo das interfaces do Equipamento**
```
#show ip interface brief
```

**Inserir uma descrição em uma Interface**
```
(config-if)#description [texto-da-descrição]
```

**Desativar uma interface**
```
(config-if)#shutdown
```

**Ativar uma Interface**
```
(config-if)#no shutdown
```

**Definir nome do domínio no dispositivo**
```
(config)#ip domain-name [nome-do-domínio]
```

**Gerar chave de criptografia**
```
(config)#crypto key generate rsa general-key modulus [tamanho-da-chave-em-bits]
```

**Criar usuário local**
```
(config)#username [nome-do-usuário] privilege [nível-de-privilégio] secret [senha-do-usuário]
```

**Configurar acesso via SSH em todas as linhas VTY**
```
(config)line vty 0 15
(config-line)transport input ssh
```

**Ativar o login com usuário e senha local (funciona para as linhas de Console e VTY)**
```
(config-line)#login local
```

**Desativar tradução de nome**
```
(config)#no ip domain-lookup
ou
(config-line)#logging synchronous
```

**Interface Loopback**

Uma interface de loopback é uma interface de rede virtual que permite que um cliente e um servidor no **mesmo host** se comuniquem entre si usando a pilha de protocolos TCP/IP

```
(config)#int loopback [id-da-interface]
```

**Atrelar um endereço IP no Loopback**
```
(config-if)#ip add [endereço-ip] [máscara(em decimal)]
```

## Configurações do Switch

**Configurar endereço IP em um Switch**
```
(config)#interface vlan [id-da-vlan-de-gerenciamento]
(config-if)#ip address [endereço-ip] [máscara (em decimal)]
(config-if)#no shutdown
Lembrando que você deve criar a VLAN de Gerenciamento, do contrário o Switch não vai ativar o endereço IP
```

**Configurar o Gateway Padrão no Switch**
```
(config)#ip default-gateway [ip-do-gateway]
```

## Configurações de VLAN

**Criar e definir um nome para uma VLAN**
```
(config)#vlan [id-da-vlan]
(config-vlan)#name [nome-da-vlan]
```

**Atrelar uma VLAN a uma interface**
```
(config)#interface [id-da-interface]
(config-if)#switchport mode access
(config-if)#switchport access vlan [id-da-vlan]
```

**Configurar o Trunk em uma interface**
```
(config)#interface [id-da-interface]
(config-if)#switchport mode trunk
(config-if)#switchport trunk native vlan [id-da-vlan_nativa]
(config-if)#switchport trunk allowed vlan [id-das-vlans (separado por vírgula)]
```

**Exibir um resumo das VLANs presentes no dispositivo e as interfaces atreladas as VLANs**
```
#show vlan brief
```

**Exibir informações do modo trunk**
```
#show interface trunk
```

**Exibir informações sobre uma VLAN específica**
```
#show vlan id [id-da-vlan]
ou
#show vlan name [nome-da-vlan]
```
**Exibir informações relacionadas a VLAN em um interface específica**
```
#show interface [id-da-interface] switchport
```
**Deletar arquivo vlan.dat**
```
#delete vlan.dat
```
**Criação de Subinterface e atrelamento dela a uma VLAN**
Para configurar uma Subinterface, basta colocar um **ponto** no final do nome da Interface onde você quer criar a **Subinterface**, após o ponto digite o **ID da Subinterface**, lembrando que o **ID da Subinterface** normalmente é o **ID da VLAN** a qual essa Subinterface será atrelada.
No exemplo abaixo vamos criar a **Subinterface .10** na **Interface g0/0** e atrelar ela a **VLAN 10**
```
(config)#interface g0/0.10
(config-if)#encapsulation dot1q 10
```

## VTP

**Modo de distribuição dos pacotes**
**AUTO** - Torna a interface capaz de converter o link em um link de trunk.
**DESIRABLE** - Faz com que a interface tente ativamente converter o link em um link de trunk.

```
(config)#int [id-da-interface]
(config-if)#switchport mode dynamic [desirable-ou-auto]
```

**Configurações VTP - CLIENTE (client), SERVIDOR (server) e TRANSPARENTE (transparent)**
```
(config)#vtp mode [modo]
(config)#vtp domain [nome-do-domínio]
(config)#vtp password [senha]

VTP Operating Mode: Server - distribui os pacotes
VTP Operating Mode: Client - recebe os pacotes
VTP Operating Mode: Transparent - passa os pacotes (VLANs) sem absorver as configurações
```

**Exibir informações sobre o VTP**
```
#show vtp status
```

**Exibir senha do domínio cadastrado**
```
#show vtp password
```

## Configurações do Roteador

**Configurar IP em uma Interface ou Subinterface**
```
(config-if)#ip address [endereço-ip] [máscara (em decimal)]
```

**Exibir a tabela de roteamento**
```
#show ip route
```

**Definir um tamanho mínimo de senha para os usuários locais**
```
(config)#security password min-length [tamanho-mínimo]
```

**Bloquear acesso de um usuário, após muitas tentativas de acesso**
```
Exemplo: Bloquear um usuário por 30 Segundos, caso ele erre a senha 3 vezes, em um período de 60 segundos
(config)#login block-for 30 attempts 3 within 60 
```

**Criar Rota Estática**
```
(config)#ip route [rede-de-destino] [máscara-da-rede-de-destino] [interface-de-saída]
ou
(config)#ip route [rede-de-destino] [máscara-da-rede-de-destino] [ip-do-roteador-que-conhece-a-rede]
```

**Configurar Rota Padrão**
```
(config)#ip route 0.0.0.0 0.0.0.0 [ip-de-último-recurso]
```

## Configurações Rota Dinâmica (RIPv2) 

**Ativar o RIPv2**
```
(config)#router rip
```

**Desativar o RIPv2**
```
(config)#no router rip
```

**Versão do RIP**
```
(config-router)#version 2
```

**Definir as Rotas conhecidas pelo Roteador**
```
(config-router)#network [rede-conhecida-pelo-roteador]
```

**Resumir a Tabela de Roteamento**
```
(config-router)#no auto-summary
```

**Exibir as Rotas do RIP**
```
#show ip route rip
``` 

**Exibir as configurações do protocolo IPv4**
```
#show ip protocols
```

**Propagar a rota padrão**
```
(config-router)#default-information originate
``` 

**Uma forma de economizar processamento no Router**
```
(config-router)#passive-interface [interface-que-normalmente-não-está-conectada-em-outro-roteador]
``` 

**Definir uma rota RIP utlizando IPv6**
```
(config-if)#ipv6 rip [nome-da-rota] enable
``` 

## Configurações STP

**Ver todas as interfaces conectadas do Spanning-tree**
```
#show spanning-tree detail
ou
#show spanning-tree
ou
#show span
```

**Ativar o STP em uma Vlan específica**
```
(config)#spanning-tree vlan [id-da-vlan]
OBS: Para desativar o STP, basta adicionar o comando "no" antes do conteúdo.  
``` 

**Ver as informações do protocolo STP em uma VLAN específica**
```
#show spanning-tree vlan [id-da-vlan]
``` 

**Alterar as configurações STP (BALANCEAMENTO DE CARGA)**
```
(config)#spanning-tree mode pvst
(config)#spanning-tree vlan [id-das-vlans] root [primary ou secondary]
``` 

**Interromper a troca de BPDUs**

**PortFast:** faz com que uma porta entre no estado forwarding quase imediatamente, reduzindo drasticamente o tempo dos estados listening e learning. O PortFast minimiza o tempo necessário para o servidor ou estação de trabalho entrar on-line. Configure o PortFast nas interfaces de switch que estão conectadas aos computadores.

O aprimoramento do **STP PortFast BPDU Guard** permite que os programadores de redes reforcem as fronteiras do domínio STP e mantenham a topologia ativa previsível. Os dispositivo atrás das portas com PortFast do STP habilitado não conseguem influenciar a topologia de STP. No recebimento das BPDUs, a operação da BPDU Guard desativa a porta com PortFast configurado. O BPDU Guard faz a transição da porta para o estado err-disable e uma mensagem aparece na console. Configure o BPDU Guard nas interfaces de switch que são conectadas aos PCs.

```
(config)#int [id-da-interface]
(config-if)#spanning-tree portfast
(config-if)#spanning-tree bpduguard enable
```

## HSRP

**Ativar a interface que está atrelada como **gateway** em **standby**** 
```
(config)#int [id-da-interface-do-gateway]
(config-if)#standby version 2
```

**Atrelar endereço IP a interface bem como seu grupo**

OBS: Os roteadores da Cisco suportam **até 4095** grupos 

```
(config-if)#standby [número-do-grupo] ip [endereço-ip]
```

**Definir a prioridade do roteador sobre os outros**

OBS: Os roteadores da Cisco possuem limite máximo de prioridade de **até 255**

```
(config-if)#standby [número-do-grupo] priority [número-de-prioridade]
```

**Tornar o roteador ativo imediatamente**

```
(config-if)#standby [número-do-grupo] preempt
```

**Exibir as informações do HSRP**
```
#show standby
```

## ETHERCHENNEL - LACP e PAGP

**Configurando a **range** de interfaces que será utilizada no Etherchannel** 
```
(config)#Interface range [id´s-das-interfaces]
```

**Definir o protocolo LACP**

**On** - Membros de canal sem negociação (nenhum protocolo) 

**Active** – A porta envia pacotes LACP para iniciar negociações com outras interfaces

**Passive** – A porta negocia passivamente o estado, mas não inicia a negociação LACP

```
(config-if-range)# channel-group 1 mode active
ou
(config-if-range)# channel-group 1 mode passive
```

**Definir o protocolo PAGP**

**On** - Membros de canal sem negociação (nenhum protocolo) 

**Desirable** – Inicia negociações do PAgP

**Auto** – Negocia passivamente, mas não inicia

```
(config-if-range)# channel-group 1 mode desirable
ou
(config-if-range)# channel-group 1 mode auto
```

OBS: Os modos de operação devem ser **compatíveis** de cada lado. 

**Exibir um resumo dos etherchannel´s configurados**
```
#show etherchannel summary
```

**Detalhar os etherchannel´s configurados**
```
#show etherchannel port-channel
```

## ACL - ACCESS CONTROL LISTS - PADRÃO (STANDARD)

**Atribuir as configurações de Controle de Acesso**
```
(config)#access-list [1-99] [deny or permit] [endereço-ip] [wildcard]
ou
(config)#access-list [1-99] [deny or permit] host [endereço-ip]
```

**Parâmtro 'Any' (restante)**
```
(config)#access-list [1-99] [deny or permit] any
```

**Atrelar as configurações ACL à interface mais próxima do destino**

**OBS:** As ACLs de **entrada** são mais usadas para filtrar pacotes quando a rede conectada a uma interface de entrada é a única origem dos pacotes que precisa ser examinada.

As ACLs de **saída** são mais usadas quando o mesmo filtro é aplicado aos pacotes que vêm de
várias interfaces de entrada antes de saírem da mesma interface de saída.

```
(config)#int [id-da-interface]
(config-if)#ip access-group [1-99] [out or in]
```

**ACL padrão nomeada**
```
(config)# ip access-list standard [name]
```

**Permissões em uma ACL (padrão) nomeada**
```
(config-std-nacl)#[permit or deny] host [endereço-ip-do-host]
ou
(config-std-nacl)#[permit or deny] [endereço-ip-da-rede] [wildcard]
```

**Parâmetro 'any', nestas situações**
```
(config-std-nacl)#[permit or deny] any
```

**Aplicar ACL (padrão) nomeada em uma interface**
```
(config-if)#ip access-group [name] [out or in]
```

## ACL - ACCESS CONTROL LISTS - ESTENDIDA (EXTENDED)

**Atribuir as configurações ACL estendidas**
```
(config)#ip access-list extended [nome-da-lista-estendida]
```

**Configurar as 'regras' dentro de uma ACL**
```
(config-ext-nacl)#[1-99] [permit or deny] ip [endereço-ip] [wildcard] host [endereço-ip]
```

**Parâmtro 'Any Any'**

**OBS:** Significa - "qualquer endereço na origem e no destino"

```
(config)#[1-99] [permit or deny] any any
```

**Atrelar as configurações ACL à interface mais próxima da origem**
```
(config)#int [id-da-interface]
(config-if)#ip access-group [nome-da-lista-estendida] [in or out]
```

**Alguns parâmetros de uma ACL estendida**

**Exemplo:** 10 permit tcp host 192.168.0.1 host 172.16.0.2 eq www

```
(config-ext-nacl)#[número-da-acl] [permit or deny] [protocolo] [host-ou-ip-da-rede] [wildcard (apenas quando for ip da rede)] [range-de-portas (não obrigatório)] host [endereço-ip] eq [porta-de-destino]
```

**Verificar as ACLs**
```
#sh access-lists
```

**Verificar uma ACL específica**
```
#sh access-list [id-da-acl]
```

**Verificar em qual porta está aplicada uma ACL**
```
#sh running-config
```

**Remover uma ACL**
```
(config-ext-nacl)# no [id-da-ACL]
ou
(config-std-nacl)# no [id-da-ACL]
```

## Configurações IPv6

**Ver resumo dos endereços IPv6 configurados no equipamento**
```
#show ipv6 interface brief
```

**Habilitar Roteamento IPv6**
```
(config)#ipv6 unicast-routing
```

**Configurar IPv6 em uma Interface ou Subinterface**
```
(config-if)#ipv6 address [endereço-ip]/[prefixo]
```

**Configurar IPv6 Link Local em uma Interface ou Subinterface**
```
(config-if)#ipv6 address [endereço-ip]/[prefixo] link-local
```

**Configurar Rota Estática IPv6**
```
(config)#ipv6 route [rede-de-destino]/[prefixo] [ip-do-roteador-que-conhece-a-rede]
ou
(config)#ipv6 route [rede-de-destino]/[prefixo] [interface-de-saída]
```

**Configurar Rota Padrão IPv6**
```
(config)#ipv6 route ::/0 [ip-de-último-recurso]
```

## NAT - ESTÁTICO

**Estabelecer a tradução estática entre um endereço local interno e um endereço global interno**

OBS: Conversões de NAT estático são usadas geralmente quando os clientes da rede externa (Internet) precisam acessar servidores da rede interna.

Exemplo:

(config)#ip nat inside source static 192.168.11.99 209.165.201.5

```
(config)#ip nat inside source static [ip-local] [ip-global]
ou
(config)#ip nat inside source [tcp or udp] [ip-local] [porta-local] [ip-global] [porta-global]
```

**Marcar a interface conectada internamente**

```
(config-if)ip nat inside
```

**Marcar a interface conectada externamente**

```
(config-if)ip nat outside
```

**Exibir as conversões ativas de NAT**

```
#show ip nat translations
```

**Exibir informações sobre o número total de conversões ativas**

OBS: Para verificar se a conversão de NAT está funcionando, é melhor limpar as estatísticas de algumas conversões do passado usando o comando clear ip nat statistics e clear ip nat translation antes de testar.

```
#show ip nat statistics
```

**Verificar a operação do recurso NAT, exibindo informações sobre cada pacote que está sendo convertido pelo roteador**

```
#debug ip nat
#debug ip nat detailed 
```

## NAT - DINÂMICO

**Definir um pool de endereços globais a serem usados para conversão**

OBS: Os endereços são definidos pela indicação do endereço IPv4 inicial e endereço IPv4 final do pool.

Exemplo: 

(config)#ip nat pool NAT-POOL1 209.165.200.226 209.165.200.240 netmask 255.255.255.224

```
(config)#ip nat pool [name] [primeiro-ip-da-rede] [ultimo-ip-da-rede] netmask [máscara]
```

**Configurar uma ACL padrão para permitir os endereços que devem ser convertidos**

Exemplo: 

(config)#access-list 1 permit 192.168.0.0 0.0.255.255

```
(config)#access-list [1-99] [deny or permit] [endereço-ip] [wildcard]
```

**Estabelecer a conversão dinâmica de origem, especificando a lista de acesso e o pool**

Exemplo: 

(config)#ip nat inside source list 1 pool NAT-POOL1

```
(config)#ip nat inside source list [número-da-acl] pool [name]
```

**Marcar a interface conectada internamente**

```
(config-if)ip nat inside
```

**Marcar a interface conectada externamente**

```
(config-if)ip nat outside
```

**Remover conversões de NAT**

```
#clear ip nat translations *
```

**Exibir as conversões ativas de NAT**

```
#show ip nat translations
```

**Exibir informações sobre o número total de conversões ativas**

```
#show ip nat statistics
```

**Eliminar as estatísticas e as entradas**

```
#clear ip nat statistics
#clear ip nat translation *
```

**Verificar a operação do recurso NAT, exibindo informações sobre cada pacote que está sendo convertido pelo roteador**

```
#debug ip nat
#debug ip nat detailed 
```

## PAT - Pool de Endereços

**Definir um pool de endereços globais a serem usados para conversão de sobrecarga**

OBS: Os endereços são definidos pela indicação do endereço IPv4 inicial e endereço IPv4 final do pool.

Exemplo: 

(config)#ip nat pool NAT-POOL2 209.165.200.226 209.165.200.240 netmask 255.255.255.224

```
(config)#ip nat pool [name] [intervalo-de-IPs] netmask [máscara]
```

**Configurar uma ACL padrão para permitir os endereços que devem ser convertidos**

Exemplo: 

(config)#access-list 1 permit 192.168.0.0 0.0.255.255

```
(config)#access-list [1-99] [deny or permit] [endereço-ip] [wildcard]
```

**Estabelecer a conversão de sobrecarga, especificando a lista de acesso e o pool**

Exemplo: 

(config)#ip nat inside source list 1 pool NAT-POOL2 overload

```
(config)#ip nat inside source list [número-da-acl] pool [name] overload
```

**Marcar a interface conectada internamente**

```
(config-if)ip nat inside
```

**Marcar a interface conectada externamente**

```
(config-if)ip nat outside
```

**Eliminar as estatísticas e as entradas**

```
#clear ip nat statistics
#clear ip nat translation *
```

**Exibir as conversões ativas de NAT**

```
#show ip nat translations
```

**Exibir informações sobre o número total de conversões ativas**

```
#show ip nat statistics
```

## PAT - Endereço único

**Configurar uma ACL padrão para permitir os endereços que devem ser convertidos**

Exemplo: 

(config)#access-list 1 permit 192.168.0.0 0.0.255.255

```
(config)#access-list [1-99] [deny or permit] [endereço-ip] [wildcard]
```

**Estabelecer a conversão dinâmica de origem, especificando as opções de ACL, interface de saída e sobrecarga**

Exemplo:

(config)#ip nat inside source list 1 interface serial 0/1/0 overload

```
(config)#ip nat inside source list [1-99] interface [id-da-interface] overload
```

**Marcar a interface conectada internamente**

```
(config-if)ip nat inside
```

**Marcar a interface conectada externamente**

```
(config-if)ip nat outside
```

**Eliminar as estatísticas e as entradas**

```
#clear ip nat statistics
#clear ip nat translation *
```

**Exibir as conversões ativas de NAT**

```
#show ip nat translations
```

**Exibir informações sobre o número total de conversões ativas**

```
#show ip nat statistics
```

**Verificar a operação do recurso NAT, exibindo informações sobre cada pacote que está sendo convertido pelo roteador**

```
#debug ip nat
#debug ip nat detailed 
```

## OSPF

**Definir o número de processo que o OSPF irá executar**

```
(config)#router OSPF [número-do-processo]
```

**Definir o ID do roteador**

```
(config-router)#router-id [id-do-roteador]
```

**'Limpar' os processos OSPF**

```
#clear ip ospf process
```

**Redes conhecidas**

```
(config-router)#network [ip-da-rede] [wildcard] area [número-da-área]
```

**Evitar a distribuição das networks para as respectivas LAN´s**

```
(config-router)passive-interface [interface-que-está-conectada-na-LAN]
```

**Redistribuição OSPF --> BGP**

```
(config-router)#redistribute bgp [número-do-processo-bgp-que-foi-definido] metric [número-do-processo-ospf-que-foi-definido] subnets
```

**Verificar banco de dados do OSPF**

```
#sh ip ospf database
```

**Verificar Interfaces do OSPF**

```
#sh ip ospf interface
```

**Exibir vizinhos OSPF**

```
#sh ip ospf neighbor
```

**Ver redes cadastradas e áreas participantes**

```
#sh ip protocols
```

**Exibir as rotas OSPF**

```
#sh ip route ospf
```

**Verificar as áreas conhecidas**

```
#sh ip ospf interface brief
```

## BGP 

**Definir o número de processo que o BGP irá executar**

OBS: Normalmente o número do processo deve ser > ou = 65000

```
(config)#router bgp [número-do-processo]
```

**Determinar o caminho para outra rede**

```
(config-router)#neighbor [endereço-ip-da-interface-vizinha] remote-as [número-do-processo-do-roteador-vizinho]
```

**Declarar a rede na qual estou inserido**

```
(config-router)#network [endereço-ip] mask [máscara]
```

**Redistribuição BGP --> OSPF**

```
(config-router)#redistribute ospf [número-do-processo-executado-pelo-ospf]
```

**Verificar informações sobre o BGP**

```
#sh ip bgp
```

## GRE - VPN

**Definir a interface de túnel**

```
(config)int tunnel [número-do-túnel]
```

**Atrelar um endereço IP nesta interface**

```
(config-if)#ip add [endereço-ip] [máscara]
```

**Definir a origem do túnel**

```
(config-if)#tunnel source [id-da-interface-válida-na-internet]
```

**Definir o endereço IP destino do túnel**

```
(config-if)#tunnel destination [endereço-ip-de-destino-do-túnel]
```

**Definir o modo que a VPN irá operar**

```
(config-if)#tunnel mode gre ip
```

**Definir uma rota padrão voltada para a rede local**

```
(config)ip route [endereço-ip-destino] [máscara] [endereço-ip-de-próximo-salto]
```

## PPP

**Definir a interface que se conecta ao ISP**

```
(config)#int [id-da-interface]
```

**Encapsulamento**

```
(config-if)#encapsulation ppp
```

**Modo de operação**

```
(config-if)#ppp authentication chap
```

**Autenticação**

```
(config)username [username] password [password]
```

## Configurações DHCPv4

**Excluir endereços específicos**

Exemplo:

(config)#ip dhcp excluded-address 192.168.10.1 192.168.10.9

```
(config)#ip dhcp excluded-address [intervalo-entre-os-endereços-ip]
```

**Configuração de um pool DHCPv4**

Exemplo: 

(config)#ip dhcp pool LAN-POOL-1

(dhcp-config)#

```
(config)#ip dhcp pool [pool-name]
```

**Definir o pool de endereços**

Exemplo: 

(dhcp-config)#network 192.168.10.0 255.255.255.0

```
(dhcp-config)#network [network-number]
```

**Definir o roteador ou gateway padrão**

Exemplo: 

(dhcp-config)#default-router 192.168.10.1

```
(dhcp-config)#default-router [endereço-ip]
```

**Definir um servidor DNS**

Exemplo:

(dhcp-config)#dns-server 192.168.11.5

```
(dhcp-config)#dns-server [endereço-ip-do-servidor-de-dns]
```

**Definir o nome de domímio**

Exemplo:

(dhcp-config)#domain-name example.com

```
(dhcp-config)#domain-name [nome-de-domínio]
```

**Definir a duração do aluguel do DHCP**

```
(dhcp-config)#lease [dias-horas-minutos-infinite]
```

**Definir o servidor NetBIOS WINS**

```
(dhcp-config)#netbios-name [endereço-ip-do-servidor-de-netbios]
```

**Desativar / Reativar o DHCPv4**

OBS: O serviço DHCPv4 fica ativado por padrão.

```
(config)#no service dhcp (desativar)
ou
(config)#service DHCP (reativar)
```

**Solicitação de um servidor DHCPv4 que esteja em uma outra sub-rede / RETRANSMISSÃO**

OBS: Esse comando será atrelado na interface do roteador que receberá o broadcast de solicitação de endereço IPv4 de um determinado host

Exemplo:

(config)#int g0/1

(config-if)#ip helper-address 192.168.11.6

```
(config-if)#ip helper-address [endereço-ip-do-servidor-de-DHCPv4-em-uma-outra-subrede]
```

**Configuração de um roteador como cliente DHCP**

OBS: Essa configuração será atrelada na interface de um roteador SOHO conectada à um roteador ISP

```
(config-if)#ip address dhcp
```

**Exibir os comandos DHCPv4 configurados no Router**

```
#show running-config | section dhcp
```

**Exibir uma lista de todos os endereços IPv4 para associações de endereço MAC que foram fornecidas pelo serviço DHCPv4**

```
#show ip dhcp binding
```

**Exibir informações sobre a quantidade de mensagens DHCPv4 que foram enviadas e recebidas**

```
#show ip dhcp server statistics
```

**Exibir todos os conflitos de endereço gravados pelo servidor DHCPv4**

```
#show ip dhcp conflict
```

**Reportar eventos de servidor, como atribuições de endereço e atualizações de banco de dados**

```
#debug ip dhcp server events
```

## Configurações DHCPv6

**Ativar o roteamento IPv6**

```
(config)# ipv6 unicast-routing
```

**Configurar um pool de DHCPv6**

Exemplo: 

(config)#ipv6 dhcp pool IPV6-STATELESS

```
(config)#ipv6 dhcp pool [pool-name]
(config-dhcpv6)#
```

**Configurar os parâmetros do pool**

Exemplo:

(config-dhcpv6)#address prefix 2001:db8:cafe:1::/64 lifetime infinite

(config-dhcpv6)#dns-server 2001:db8:cafe:1:aaaa:5

(config-dhcpv6)#domain-name example.com

```
(config-dhcpv6)#address prefix [endereço-ip-e-máscara] {[lifetime [valid-lifetime or preferred-lifetime | infinite]}
(config-dhcpv6)#dns-server [endereço-ip-do-servidor-de-dns]
(config-dhcpv6)#domain-name [nome-do-domínio]
```

**Configurar a interface do DHCPv6**

```
(config)#int [id-da-interface]
(config-if)#ipv6 add [endereço-ip]
(config-if)#ipv6 dhcp server [pool-name]
(config-if)#[nesta-etapa-devemos-especificar-o-modo-de-operação-que-o-roteador-irá-trabalhar]
```

**Restaurar as flag M e O para seus valores iniciais de 0 - SLAAC padrão**

OBS: As mensagens de RA são configuradas em uma interface individual de um roteador.

```
(config-if)# no ipv6 nd managed-config-flag [flag-M-restaurada]
(config-if)# no ipv6 nd other-config-flag [flag-O-restaurada]
```

**Utilizar DHCPv6 Stateless**

OBS: Flag M = 0; Flag O = 1

```
(config-if)# ipv6 nd other-config-flag
```

**Utilizar DHCPv6 Stateful**

OBS: Flag M = 1; Flag O = não está envolvida

```
(config-if)#ipv6 nd managed-config-flag
```

**Configuração de um roteador como cliente de SLAAC ou DHCPv6 stateless**

OBS: Este não é um cenário típico e é usado somente para fins de demonstração.

```
(config)#int [id-da-interface]
(config-if)#ipv6 enable
(config-if)#ipv6 add autoconfig
```

**Configuração de um roteador como cliente de DHCPv6 Stateful**

OBS: Essa configuração será atrelada na interface de um roteador SOHO conectada à um roteador ISP

```
(config)#int [id-da-interface]
(config-if)#ipv6 address dhcp
```

**Configuração de um roteador como um agente de retransmissão de DHCPv6**

OBS: Esse comando é configurado na interface voltada para o cliente usando o endereço do servidor DHCPv6 como destino.

```
(config)#int [id-da-interface]
(config-if)#ipv6 dhcp relay destination [endereço-ip-do-servidor-de-IPv6]
```

**Verificação dos servidores DHCPv6 stateful**

```
#show ipv6 dhcp pool - verificar as configurações
#show ipv6 dhcp binding - verificar as vinculações
```

**Verificação do cliente DHCPv6 stateful**

```
#show ipv6 int [id-da-interface] - verificar as configurações
```

**Exibe todos os conflitos de endereço registrados por servidores DHCPv6 stateful**

```
#show ipv6 dhcp conflict
```

**Verificar a recepção e a transmissão de mensagens DHCPv6**

```
#debug ipv6 dhcp detail
```

## CDP

**Verificar o status do CDP e exibir informações sobre ele**

```
#show cdp
```

**Ativar globalmente o CDP em todas as interfaces compatíveis do dispositivo**

OBS: para desativa-lo, basta colocar o parâmetro "no" antes do comando

```
(config)#cdp run
```

**Desativar o CDP em uma interface específica (como a interface voltada para um ISP por exemplo)**

OBS: para ativar, basta retirar o "no"

```
(config-if)#no cdp enable
``` 

**Verificar o status do CDP e exibir uma lista de vizinhos**

```
#show cdp neighbors [detail]
```

**Exibir as interfaces ativadas para CDP em um dispositivo**

```
#show cdp interface
```

## LLDP

**Ativar o LLDP globalmente em um dispositivo de rede da Cisco**

OBS: para desativar o LLDP, insira o comando 'no lldp run'

```
(config)#lldp run 
```

**Transmissão e recebimento de pacotes LLDP**

```
(config-if)#lldp transmit
(config-if)#lldp receive
``` 

**Verificar LLDP**

```
#show lldp
```

**Detectar os vizinhos**

```
#show lldp neighbors [detail]
```

## NTP

**Definir o horário de maneira manual**

Exemplo: 

#clock set 20:36:00 dec 11 2015

```
#clock set [hh:mm:ss] {mmm (em-inglês | apenas as 3 primeiras letras)} [dd] [aaaa]
```

**Indicar o número de saltos de NTP com relação a uma fonte de tempo autoritativa**

```
(config)#ntp master [nível-de-stratum]
```

**Configurar NTP**

```
(config)#ntp server [endereço-ip]
```

**Atualizar o calendário periodicamente com a hora do NTP**

```
(config)#ntp update-calendar
```

**Definir o fuso do relógio**

Exemplo: Definir PDT (Horário do Pacífico, que é 8h mais tarde que o GMT)

(config)#clock timezone PST -8

```
(config)#clock timezone [fuso] [gmt]
```

**Definir para o horário verão recorrente**

```
(config)#clock summer-time PDT recurring
```

**Exibir a hora atual no relógio do software**

```
#show clock [detail]
```

**Exibir informações**

```
#show ntp associations
#show ntp status
```

## SYSLOG

**Forçar eventos registrados a exibirem a data e hora**

OBS: se você usar a palavra-chave 'datetime', o relógio do dispositivo de rede deverá ser definido manualmente ou por NTP

```
(config)#service timestamps log datetime
ou
(config)#service timestamps log datetime msec
```

**Armazenar as mensagens de log por padrão**

OBS: os comandos devem seguir essa ordem

```
(config)#logging console
(config)#logging buffered
```

**Exibir as configurações de serviço de logging padrão**

```
#sh logging
```

## Comandos do roteador e do switch para clientes de Syslog

OBS: São necessários três passos para que o roteador envie mensagens do sistema a um Servidor syslog, onde elas podem ser armazenadas, 
filtradas e analisadas:

**Configurar o nome de host do destino ou o endereço IPv4 do syslog (Passo 1)**

```
(config)#logging [endereço-ipv4-do-syslog]
ou
(config)#logging host [endereço-ipv4-do-host-de-syslog]
```

**Controlar as mensagens que serão enviadas ao Servidor syslog (Passo 2)**

```
(config)#logging trap [nível]
```

**Configurar a interface de origem (Passo 3)**

```
(config-if)#logging source-interface [id-da-interface]
```

**Filtrar as saídas de syslog**

Exemplo:

#show logging | include changed state to up
#show logging | begin Jun 12 22:35

```
#sh logging | [parâmetro]
```

## BACKUP DA IMAGEM DO IOS

**Teste de conectividade no servidor TFTP**

```
#ping [endereço-ip-do-servidor]
```

**Verifique se o servidor TFTP tem espaço suficiente em disco para acomodar a imagem do software IOS Cisco**

```
#show flash0
```

**Copiar a configuração para o servidor TFTP**

```
#copy flash0: tftp:
[nome-do-arquivo]
[endereço-ip-do-servidor]
```

**Copiar o arquivo de imagem do IOS do servidor TFTP para o dispositivo**

```
#copy tftp: flash0:
[nome-do-arquivo]
[endereço-ip-do-servidor]
```

**Atualizar para a imagem do IOS copiado após ter salvo essa imagem na memória flash**

```
(config)#no boot system
(config)#boot system flash: [nome-da-imagem]
#copy running-config startup-config
#reload
```

**Verificar a imagem carregada**

```
#sh version
```

## LICENCIAMENTO DE SOFTWARE

**Exibir informações adicionais sobre licenças de software IOS Cisco**

```
#sh license
```

**Exibir as licenças do pacote de tecnologia e as licenças de recursos suportadas**

```
#show license feature
```

**Exibição do UDI**

```
#sh license udi
``` 

**instalar um arquivo de licença**

```
#license install [stored-location-url]
```

**Reinicialize o dispositivo**

```
#reload
```

**Aceitar o Contrato de Usuário Final da Licença (EULA)**

```
(config)#license accept end user agreement
```

**Instalar o pacote de tecnologia de dados da avaliação**

```
(config)#license boot module [module-name] technology-package [package-name]
```

**Backup de uma cópia das licenças em um dispositivo**

```
#license save [file-sys:lic-location]
```

**Verificar se as licenças foram salvas**

```
#sh [file-sys:]
```

**Desativar o pacote de tecnologia**

OBS: recarregue o roteador usando o comando reload. Um recarregamento é exigido para tornar o pacote de software inativo.

```
(config)#license boot module [module-name] technology-package [package-name] disable
```

**Remover a licença**

OBS: apague o comando license boot module usado para desativar a licença ativa

```
#license clear [feature-name]
```

## Manutenção do dispositivo 

**Listar todos os sistemas de arquivos disponíveis em um roteador e um switch Cisco**

```
#show file systems
```

**Listar os conteúdos da flash**

```
#dir
```

**Exibir o conteúdo da NVRAM**

```
#cd nvram:
#Pwd (verifica se estamos exibindo o diretório da NVRAM)
#dir
```

**Salvar a configuração atual ou a configuração inicial em um servidor TFTP**

OBS: deve-se configurar

- endereço IP do host onde o arquivo de configuração está armazenado;

- nome que será atribuído ao arquivo de configuração.

```
# copy running-config tftp 
ou 
#copy startup-config tftp
``` 

**Visualizar o conteúdo da unidade flash USB**

```
#dir usbflash0:
```

**Copiar o arquivo de configuração para a unidade flash USB**

OBS: A barra é opcional, mas indica o diretório raiz da unidade flash USB

dir - para ver o arquivo na unidade USB

more - para ver o conteúdo

```
#copy run usbflash0:/ 
```

**Restaurar as configurações com uma unidade USB flash**

OBS: Com o objetivo de copiar o arquivo de volta, será necessário editar o arquivo R1-Config da USB usando um editor de textos. Considere que 
o nome do arquivo é R1-Config.

```
#copy usbflash0/R1-Config running-config
```

**Recuperar a configuração inicial e alterar senhas**

```
Digitar a sequência de interrupção - Ctrl+Break (PuTTY)

rommon 1 > confreg 0x2142
rommon 2 > reset
```

**Após a conclusão do recarregamento do dispositivo**

```
#copy startup-config running-config
```

**Definir as senhas novamente**

```
(config)#enable secret [senha]
(config)#config-register 0x2102
(config)#end
#copy running-config startup-config
#reload
```