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
```
(config)#int [id-da-interface]
(config-if)#switchport mode dynamic [desirable-ou-auto]
AUTO - Torna a interface capaz de converter o link em um link de trunk.
DESIRABLE - Faz com que a interface tente ativamente converter o link em um link de trunk.
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

PortFast: faz com que uma porta entre no estado forwarding quase imediatamente, reduzindo drasticamente o tempo dos estados listening e learning. O PortFast minimiza o tempo necessário para o servidor ou estação de trabalho entrar on-line. Configure o PortFast nas interfaces de switch que estão conectadas aos computadores.

O aprimoramento do STP PortFast BPDU Guard permite que os programadores de redes reforcem as fronteiras do domínio STP e mantenham a topologia ativa previsível. Os dispositivo atrás das portas com PortFast do STP habilitado não conseguem influenciar a topologia de STP. No recebimento das BPDUs, a operação da BPDU Guard desativa a porta com PortFast configurado. O BPDU Guard faz a transição da porta para o estado err-disable e uma mensagem aparece na console. Configure o BPDU Guard nas interfaces de switch que são conectadas aos PCs.

```
(config)#int [id-da-interface]
(config-if)#spanning-tree portfast
(config-if)#spanning-tree bpduguard enable
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
