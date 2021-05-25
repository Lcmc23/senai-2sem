# Comandos Linux

Esse são os comandos utilizados em sala de aula, USE como consulta caso esteja em dúvida em alguma configuração.

## Informações da linha de comando
```
[usuário]@[nome da máquina]: ~$ **(usuário)**
[usuário]@[nome da máquina]: ~# **(root)**
```

## Simbolos utilizados no Linux
```
^ = Ctrl
EXEMPLO: ^G = Ctrl + G

M = Alt
```

## Quem está logado?
```
whoami
```

## Arquivos e diretórios no ls
```
Arquivos começam com (-) e diretórios com (d)
```

## Informações de processamento
```
who -u
```

## Permissões root 
```
sudo su
```

## Mudar o diretório
```
cd
```

## Verificar qual diretório estou
```
pwd
```

## Limpar a tela
```
clear ou ctrl + l
```

## Criar pastas
```
mkdir
```

## Apagar arquivos 
```
rm
```

## Apagar pastas
```
rm -r
```

## Visualizar o que está contido dentro de um arquivo 
```
cat
```

## Parâmetro de busca "find"
```
find [ONDE-PESQUISAR] -name [NOME-DO-ARQUIVO-OU-PASTA]
```

## Copiar arquivos
```
cp [ORIGEM] [DESTINO]
```

## Copiar pastas
```
cp -r [ORIGEM] [DESTINO]
```

## Mover arquivos e pastas
```
mv [ORIGEM] [DESTINO]
```

## Adicionar usuário
```
adduser
UID - Identificação numérica única do Usuário
```

## Deletar usuário
```
deluser
```

## Adicionae grupo
```
addgroup
GID - Identificação numérica única do Grupo
``` 

## Deletar grupo
```
delgroup 
```

## Trocar a senha de um usuário
```
passwd
``` 

## Relção entre usuário e grupo
```
adduser [usuario] [grupo] - Adiciona um usuário a um grupo
deluser [usuario] [grupo] - Retirar um usuário de um grupo
```

## Arquivo que armazena o nome de computador
```
/etc/hostname
```

## Arquivo que contém os usuários do Linux
```
/etc/passwd 
```

## Arquivo que contém os grupos do Linux
```
/etc/group
```

## Arquivo que contém as senhas dos usuários
```
/etc/shadow 
```

## Arquivo de armazenamento dos Logs do Sistema
```
/var/log/syslog 
```

## Arquivo de armazenamento de Autenticação dos Usuários
```
/var/log/auth.log
```

## Exibir as últimas 10 linhas de um Arquivo
```
tail
``` 

## Exibe as últimas linhas de um arquivo em tempo real
```
tail -f 
```

## Filtrar informações específicas de um arquivo (quando usado com o |)
```
grep 
```

## Trocar o usuário dono da pasta/arquivo
```
chown 
chown [usuario] [pasta/arquivo]

OBS: Para trocar o usuário dono da pasta e o grupo do da pasta de uma vez use **chown usuario:grupo [pasta/arquivo]**
```

## Trocar o grupo dono da pasta/arquivo
```
chgrp
chgrp [grupo] [pasta/arquivo]

OBS: Para trocar os grupos das subpastas de uma vez use **chgrp -R**
``` 

## Trocar as permissões de pasta/arquivo
```
chmod 
chmod [permissao] [pasta/arquivo]

OBS: Para trocar as permissões das subpastas de uma vez use **chmod -R**
``` 

Permissões

    d     rwx        rwx      rwx
       U[suario]   G[rupo]   O[utros]
    r - read
    w - write
    x - execute

    desenvolvimento - d rwx r-x r-x [Permissão antiga]
                        111 101 101
                         7   5   5
    desenvolvimento - d rwx rwx r-x [Permissão nova]
                        111 111 101
                         7   7   5

    Permissão para as pastas do Exercício -   7   0   0
                                             rwx --- ---

	       ---------------------------------------
	        número    binário equiv.   permissões
	       ---------------------------------------
                0           000            ---
                1           001            --x
                2           010            -w-
                3           011            -wx
                4           100            r--
                5           101            r-x
                6           110            rw-
                7           111            rwx
	       ---------------------------------------

## Lista os diretórios e Subdiretórios
```
ls -lR
```

## Como encontrar uma pasta oculta?
```
ls -la
```

## Editores de texto para terminal

```
    **nano**
        Pesquisar: Ctrl+W
        Copiar = Alt+6
        Recortar = Ctrl+K
        Colar = Ctrl+U

        Salvar = Ctrl+O
        Sair = Ctrl+X

        Desfazer = Alt+U

    **vim** (Versão melhorada do 'vi')
        vim.tiny - Versão menor do vim, onde alguns recursos não estão disponíveis

        : = Inserir comando no Vim
        i = Entrar no modo de Inserção
        :w = Salvar o arquivo
        :q = Sair do arquivo
        :q! = salvar de maneira "forçada"
        :wq = salvar e sair
        v = Entrar no modo visual
        y = Copiar
        p = Colar
        u = Desfazer
```

## Nome das Interfaces
```
lo - Loopback
enp0s3 - Interface de Rede [Padrão antigo era eth0]
```

## Comandos para visualizar informações de Rede
```
ip add
ifconfig (necessário instalar o 'net-tools')
```

## Limpar e solicitar um endereço IP novo para o DHCP
```
ip add flush dev [nome-da-interface] -----> Mesma função do ipconfig /release no Windows
Exemplo: ip add flush dev enp0s3

dhclient -----> Mesma função do ipconfig /renew no Windows
``` 

## Arquivo que contém as configurações das Interfaces de Rede
```
/etc/network/interfaces


    Configurar IP Estático

        auto [nome-da-interface]
        iface [nome-da-interface] inet static
            address [endereco-ip]/[máscara]

        Pode-se utilizar também os parêmetros gateway, broadcast, nameserver e etc. 

         auto [nome-da-interface]
         iface [nome-da-interface] inet static
            address [endereco-ip]/[máscara]
            gateway [endereco-ip-do-gateway]
            nameserver [endereco-ip-do-dns]
```

## Reiniciar todas interfaces de Rede
```
systemctl restart networking
```

## Ligar e Desligar uma Interface Específica
```
Desligar uma interface de rede
ifdown [nome-da-interface]

Ligar uma interface de rede
ifup [nome-da-interface]
```

## Log de erros nos serviços do Linux
```
journalctl -xe
```

## Habilitação de Apache - BootStraping (automatização)

```
#!/bin/bash
yum -y install httpd
systemctl enable httpd
systemctl start httpd
echo '<html><h1>Senai Informática e AWS a parceria do futuro! </h1></html>' > /var/www/html/index.html
```
    
## Editar o apache 
```
vim ou nano /var/www/html/index.html
```  

## Reiniciar / carregar a alteração 
```
systemctl restart httpd
```

## Adicionar novas chaves SSH
```
vim ou nano /home/ec2-user/.ssh/authorized_keys
```

## Reiniciar o ssh
```
sudo systemctl restart sshd
```

## Visualizar os discos existentes
```
fdisk -l
```

## Visualizar os discos em execução
```
df -h
```

## Criar uma partição no disco
```
fdisk /dev/xvdf

    n
    p
    enter
    enter
    enter 
    w
```

## Formatação de partição 
```
mkfs -t ext3 /dev/xvdf1
```

## Criar um diretório para a nova partição
```
mkdir /mnt/novo-disco
```

## Finalização
```
mount /dev/xvdf1 /mnt/novo-disco
```

## Criar um arquivo para vermos se o backup deu certo
```
nano /mnt/novo-disco/arquivo.txt
```

## Criar um ponto de montagem 
```
mkdir /mnt/disco2G
```

## Montar a partição nesse diretório que criei 
```
mount /dev/xvdf1 /mnt/disco2G
```

## Criar arquivos vazios
```
touch /mnt/disco2G/arquivo2.txt (exemplo)
```

## Restaurar backup
```
cp -a /mnt/disco2G/* /mnt/novo-disco30G/

OBS: o "-a" mantém as informações do arquivo original
OBS: o "*" significa tudo o que possui no /mnt/disco2G/*
```