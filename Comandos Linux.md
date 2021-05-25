# Comandos Linux

Esse são os comandos utilizados em sala de aula, USE como consulta caso esteja em dúvida em alguma configuração.~

## Informações da linha de comando
```
[usuário]@[nome da máquina]: ~$ **(usuário)**
[usuário]@[nome da máquina]: ~# **(root)**
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

## Criar arquivos (vazio)
```
touch 
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