# Linux_do_Zero_Guia_de_Comandos
DIO Linux do Zero: guia de comandos. Aqui estão, resumidamente, todos os comandos do curso e suas utilidades
---

- Comandos essenciais
    - `comando --help` informa o que faz o comando e informa todos os argumentos utilizáveis, junto com suas funções
    x: `ls --help` 
    x: `help cd`
    - `man instrução` retorna o manual de instruções da instrução desejada
    x: `man clear`
    - `hystory` mostra o histórico de comandos (até 1000 comandos)
    - `!!` executa o último comando utilizado
- Navegação
    - `pwd` descubra o diretório em que você está
    - `cd` (change directory) muda o diretório
        - `cd ..` retrocede uma pasta
        - `cd ../pasta` retrocede uma pasta e abre outra desejada
        - `cd /` vai para a raiz principal
        - `cd "expressão"`+ tab (teclado) 
        x: `cd up` +tab. Saída: `cd upstream`
        - `cd "expressão`" + tab x2 (teclado) mostra os diretórios que começam com a expressão citada
        x: `cd up` + tab x2 (teclado). Saída de pastas `/upstream /upword`
    - `ls` lista os arquivos deste diretório
        - `ls “expressão”*` lista os diretórios e seus arquivos que iniciem com a expressão citada 
        x: `ls p*` saída: `pam.d: atd chfn / perl: net`
        Ou seja: traga todos os arquivos e diretório que se iniciem com p e tenham qualquer coisa depois dele.
            
        - `ls “expressão”?”expressão”` lista os diretórios e seus arquivos que iniciem com a expressão citada, que possuem uma outra letra ou número após a expressão, e contenham outra expressão na sequência. 
        x: `ls p*m` saída: `pam.d: atd chfn`
        Ou seja: traga todos os arquivos que se iniciem com p, tenham qualquer número ou letra no segundo index/elemento e tenham m na sequência
- Gerenciar arquivos e pastas
    - CRUD (create, read, update e delete)
        - `touch nomeDoArquivo.formato` cria um arquivo no diretório local 
        x: `touch arquivo.txt`
            - `touch nomeDoArquivo1.formato e nomeDoArquivo2.formato` cria dois arquivos no diretório local, de uma vez
        - `rm nomeDoArquivo.formato` exclui o arquivo desejado
        x: `rm texto.txt`
            - `rm *.txt` exclui todos os arquivos no formato `.txt`
        - `mkdir nomeDaPasta` cria uma pasta no diretório atual
        x: `mkdir pastaExemplo`
            - `mkdir nomeDaPasta1 nomeDaPasta2` cria duas pastas no diretório atual, de uma vez
        - `rmdir nomeDaPasta` excluí a pasta desejada (se estiver vazia)
        x: `rmdir contatos`
            - `rmdir nomeDaPasta1 nomeDaPasta2` excluiu duas pastas de uma vez
            x: `rmdir contatos documentos` (é necessário estar na pasta superior, ou informar o caminho completo das pastas)
        - `rm -rf nomeDodiretório/nomeDaPasta` (recursive forced) exclui todas as subpastas e subarquivos do diretório/pasta informado
        x: `rm -rf documentos` (é necessário estar na pasta superior, ou informar o caminho completo da pasta/diretório)
    - Copiar/Mover/Renomear/Procurar
        - `find -name expressão` procura, a partir do diretório atual, pelo nome do arquivo especificado
        x: `find -name arquivo.txt` ou `find -name arq*`
        - Copiar 1 arquivo:
            - `cp /diretorioArquivo/arquivo.extensão /diretorioDestino`  (cp - copy)
            x: `cp /home/denilson/bancodedados.mdf /disk2/`
        - Copiar vários arquivos que contenham a extensão .txt
            - `cp /diretorioArquivos/*.txt /diretorioDestino`
            x: `cp /home/denilson/*.txt /disk2`
        - Copiar arquivos a partir do diretório em que você está
            - `cp ./arquivo.extensão /diretorioDestino`
        - OBS: Caso você tentar copiar arquivos com o mesmo nome que já estiverem no diretório destino, ele fará a sobreposição. Para evitar isso, utilize a instrução `-i`
        - `-i` instrução indicada para evitar sobreposição, questionando antecipadamente se sobrepõe ou não.
        - `-r` instrução indicada para fazer a cópia recursiva, ou seja, copia-se todas as pastas, arquivos, subpastas e subarquivos presentes no diretório especificado (essencial para backup)
        - `-v` instrução indicada para trazer feedback visual ao usuário, informando os arquivos/pastas que ele está copiando no momento (essencial para caso houver arquivos pesados)
        - Mover 1 arquivo
            - `mv /diretorioArquivo/arquivo.extensão /diretorioDestino`
            x: `mv /home/denilson/planilhas.xlsx /disk2/`
        - OBS: não é possível mover recursivamente, deve-se mover manualmente subpastas e subarquivos
        - Renomear um arquivo
            - `mv nomeDoArquivo.extensão nomeDesejado.extensão`
            x: `mv planilhas.xlsx planilha_investimento.xlsx`
- Gerenciar usuários e grupos
    - Usuário
        - `cat /etc/passwd` mostra a listagem de serviços e usuários
        - `useradd nomeDoUsuario` adiciona um usuário
        `useradd nomeDoUsuario -m` adiciona um usuário e cria seu diretório particular dentro de `/home`
        - `userdel nomeDoUsuario` deleta um usuário
        `userdel nomeDoUsuario -r` deleta um usuário e remove o seu diretório padrão (use -f para forçar)
        - `passwd nomeDoUsuario` define ou redefine a senha para o usuário
        - `usermod nomeDoUsuario -parametro` modifica algum atributo do usuário
        `usermod nomeDoUsuario -s` adiciona cores ao prompt de comando
        `usermod nomeDoUsuario -c "mensagem"` adiciona um comentário específico ao usuário, como sobrenome ou função
        x: `usermod convidado -c "Convidado Especial"`
        - `su nomeDoUsuario` altera o usuário atual para o usuário desejado
        `su maria`
        - `w` como root, lista os usuários, juntamente com IP, horário de login, tempo em espera (idle)
        - `who -a` lista os usuários e seus PIDs (processo de logon)
        - `kill pidUsuario` “derruba” a sessão de um usuário
    - Grupo
        - `cat /etc/group` lista os grupos
        - `usermod -G grupo1, grupo2 nomeDoUsuario` adiciona o usuário aos 2 grupos mencionados, removendo-o de outros grupos anteriores (-G groups, para adicionar apenas a um grupo, use -g e o grupo desejado)
        x: `usermod -G adm, sudo mariana` adiciona a mariana ao grupo adm e sudo, removendo-a aos grupos anteriores
        - `gpasswd -d nomeDoUsuario nomeDoGrupo` remove o usuário do grupo citado (-d delete)
        x: `gpasswd -d mariana adm` remove a mariana do grupo “adm”
- Gerenciar scripts
    - Crie um arquivo executável `nano criar_user.sh`
    - Crie 4 usuários `useradd guest10`
        - Com o comentário “Usuário convidado” `-c “Usuário convidado”`
        - Com o terminal colorido `-s /bin/bash`
        - Com seu diretório particular `-m`
        - Com uma senha padrão `-p $(openss1 passwd -crypt Senha123)`
        - E com expiração de senha no primeiro login `passwd guest10 -e`
    
    ```jsx
    #!/bin/bash
    echo "Criando usuários do sistema...."
    useradd guest10 -c "Usuário convidado" -s /bin/bash -m -p $ (openssl passwd -crypt Senha123)
    passwd guest10 -e
    
    useradd guest11 -c "Usuário convidado" -s /bin/bash -m -p $ (openssl passwd -crypt Senha123)
    passwd guest11 -e
    
    useradd guest12 -c "Usuário convidado" -s /bin/bash -m -p $ (openssl passwd -crypt Senha123)
    passwd guest12 -e
    
    useradd guest13 -c "Usuário convidado" -s /bin/bash -m -p $ (openssl passwd -crypt Senha123)
    passwd guest13 -e
    
    echo "Finalizado!!"
    ```
    
    - `chmod +x  nomeDoArquivo.extensão` concede a permissão de execução do arquivo para o dono
    x: `chmod +x criar_user.sh`
    - `./nomeDoArquivo.extensão` executa o arquivo desejado
    x: `./criar_user.sh`
- Permissões
    - `ls -l` lista todos os arquivos e pastas do diretório atual, incluindo as permissões, tamanho e data de criação
        - Na imagem abaixo tem-se, da esquerda pra direita:
            - Permissões: `lrwxrwxrwx`
               
                ![permissao](https://i.imgur.com/5gVsstl.png)
                
                - A primeira letra informa o que é o arquivo Link `l` (redirecionamento de diretório) Diretório `d` Arquivo `-`
                - os 3 conjuntos de letra são as permissões de leitura `r` escrita `w` e execução`x`.
            - Quantidade de arquivos
            - Dono do arquivo/diretório
            - Grupo pertencente
            - Tamanho em bytes
            - Data e hora criada
            - Nome do Arquivo/Diretório/Links
        
        ![ls-l](https://i.imgur.com/EJV0ntl.png)
        
    - `chown nomeDoUsuario:nomeDoGrupo /nomeDoDiretorio` troca o dono do diretório para o usuário e grupo citados (chown = change owner. Só é possível com sudo ou root)
    x: `chown debora:GRP_ADM /adm/`
    - `chown nomeDoUsuario:nomeDoGrupo arquivo.extensão` troca o dono do grupo para o usuário e grupo citados
    x: `chown root:GRP_ADM texto-adm.txt`
    - Nível de permissões: conforme a tabela abaixo, se você quer ter privilégio de Leitura (R) e Gravação (W), terá que informar o valor 6. Se quiser ter R W e X, valor 7. Apenas X? 1. W e X? 3. Nenhuma? 0.
        
        ![tabela](https://i.imgur.com/Y4nz6ry.png)
        
    - Sigla `ndp`: nível de permissão (para ficar mais curto o código abaixo)
    - `chmod **ndpROOTndpGROUPndpOTHER** /diretorio` concede privilégios específicos para o root, grupo e outros para um diretório específico
    `chmod 775 /adm` dá permissão RWX ao root, RWX ao grupo e RX aos outros
    - `chmod **ndpROOTndpGROUPndpOTHER** /arquivo.extensão` concede privilégios específicos para o root, grupo e outros para um arquivo específico
    x: `chmod 750 texto-adm.txt`
    - `chmod +x  nomeDoArquivo.extensão` concede a permissão de execução do arquivo para o dono
    x: `chmod +x criar_user.sh`
    - `chmod -x  nomeDoArquivo.extensão` remove a permissão de execução do arquivo para o dono
    x: `chmod -x criar_user.sh`
- Gerenciar pacotes
    - `apt list installed` lista os aplicativos instalados na máquina
    - `apt list --upgradable` lista os aplicativos instalados que possuem atualização disponível
    - `apt search nomeDoAplicativo` procura aplicativos nos repositórios do ubuntu com o nome citado
    - `apt install nomeDoAplicativo` instala um aplicativo
    x: `apt install net-tools`
    - `apt-get install nomeDoAplicativo` instala um aplicativo
    - `apt-get update nomeDoAplicativo`  faz o download da atualização de um aplicativo
    - `apt-get upgrade nomeDoAplicativo` executa a atualização de um aplicativo
    - `wget link` baixa o(s) arquivo(s) deste link para o diretório atual
    x: `wget [https://github.com/BrunoThums/Web-Scraping-Practice/archive/refs/heads/main.zip](https://github.com/BrunoThums/Web-Scraping-Practice/archive/refs/heads/main.zip)` baixa para o diretório atual
    - `apt remove nomeDoPrograma` remove um aplicativo
    x: `apt remove net-tools`
    - `apt update` faz o download da atualização dos pacotes do sistema
    - `apt upgrade` faz a instalação das atualizações dos pacotes do sistema
    - 
- Gerenciar discos
    - Particionar o disco
        - Escolha o disco desejado ( ex: `/dev/sdb` )
        - `fdisk caminhoDoDisco` abre o fdisk para o disco escolhido
        x: `fdisk /dev/sdb`
        - `n` cria uma nova partição
        - `p` para primária `e` para extendida
        - `1` numero da partição (de 1 a 4, se for a primeira, escolha `1`)
        - ***************`pressiona enter`* entra com a quantidade de bytes do primeiro setor (*****enter***** para o padrão)
        - ***************`pressiona enter`* entra com a quantidade de bytes do último setor (*****enter***** para o padrão). Utiliza todo o disco para esta “partição”
        - `w` salva as alterações
        - `mkfs.formato /diretorioDoDisco` formata o disco para o formato Ext4
        x: `mkfs.ext4 /dev/sdb`
        - `y` para confirmar a formatação
    - Sistema de arquivos linux: `Ext3`, `Ext4`, `XFS`
    - No Windows temos os discos C: D: E:
    - No Linux, cada disco inicia por **sd** (disco físico)e termina com uma numeração (correspondendo às suas partições):
        - x: **sd**a1, **sd**a2, **sd**b1. (sda corresponde ao disco rígido Adata, por exemplo, e os números 1 e 2 são suas partições)
    - Adicionar um disco rígido
    - `lsblk` lista os discos disponíveis no computador, informando onde estão montados, juntamente com o local das partições.
    - `fdisk -l` lista os discos disponíveis no computador com mais detalhes (-l = list)
    - `mount /diretorioDoDisco /nomeDaPastaExistente (vazia)` monta o disco nesta pasta (significa que o conteúdo do disco passa a existir dentro desta pasta
    `mount /dev/sdb /disk2` (lembre-se de fazer o próximo comando para efetivar essas alterações, pois do contrário elas se perdem ao reiniciar a máquina, terá sempre que fazer o `mount`)
    - `nano /etc/fstab` e adicione uma linha ao final com:
    `nomeDodisco + localMontado + formatoDoSistemaDeArquivos + parâmetrosPadrões`
    x: `/dev/sdb /disk2 etx4 defaults 0 0` salve com CTRL+O Enter CTRL+X
    - Faça o reboot para confirmar as modificações
- Gerenciar processos
    - `ps` lista os processos do usuário atual
        - `-a` parâmetro indicado para mostrar os processos de todos os usuários
        - `-u` parâmetro indicado para exibir o nome do usuário e horário de início do processo
        - `-x` parâmetro indicado para exibir processos executados fora do console
    - `kill pidDoProcesso` elimina o processo com base no código PID
    x: `kill 12852`
    - `killall nomeDoAplicativo` elimina todos os processos de um determinado processo
    x: `killall chrome`
- Desafio: Infraestrutura como Código (IaC)
    
    ![Desafio](https://i.imgur.com/LW7wzVx.png)
    
    - Todo provisionamento deve ser feito em um arquivo do tipo Bash Script;
        - `nano script.sh`
    - Excluir diretórios, grupos e usuários criados anteriormente:
        - `rm -Rf /adm`
        - `groupdel GRP_ADM`
        - `userdel -r maisa`
    - Criar usuários e atribuí-los aos grupos
        - `useradd carlos -m -g GRP_ADM -p $ (openssl passwd -crypt Senha123)`
        `passwd carlos -e`
    - Os usuários de cada grupo terão permissão total dentro de seu respectivo diretório;
    - Os usuários não poderão ter permissão de leitura, escrita e execução em diretórios de departamentos que eles não pertencem;
    - Criar as pastas e definir as permissões (root 7, grupo 7, outros 0)
        - `mkdir /adm -m 770`
        - `mkdir /ven -m 770`
        - `mkdir /sec -m 770`
        - `mkdir /public -m 777`
    - Cria os grupos
        - `groupadd GRP_ADM`
        - `groupadd GRP_VEN`
        - `groupadd GRP_SEC`
    - O dono de todos os diretórios criados será o usuário root;
        - `chown root:GRP_ADM /adm`
        - `chown root:GRP_ADM /ven`
        - `chown root:GRP_ADM /sec`
    - Todos os usuários terão permissão total dentro do diretório publico;
        - `chmod 777 /publico`
    - Subir arquivo de script criado para a sua conta no GitHub.
    - `nano start_environment_pattern.sh`
    
    ```bash
    #!/bin/bash
    
    echo "Deletando pastas dos usuários..."
    
    rm -Rf /adm/
    #defina outras pastas aqui
    
    echo "Pastas deletadas!"
    
    echo "Excluindo usuários do sistema..."
    
    userdel -r maisa
    #defina outros usuários aqui
    
    echo "Usuários excluídos!"
    
    echo "Criando os diretórios com suas permissões..."
    
    mkdir /adm -m 770
    mkdir /ven -m 770
    mkdir /sec -m 770
    mkdir /publico -m 777
    
    echo "Diretórios criados!"
    
    echo "Criando os Grupos..."
    
    groupadd GRP_ADM
    groupadd GRP_VEN
    groupadd GRP_SEC
    
    echo "Grupos criados!"
    
    echo "Criando usuários do sistema e separando em seus grupos..."
    #GRUPO GRP_ADM
    #cria o usuário carlos
    useradd carlos -m -g GRP_ADM -p $ (openssl passwd -crypt Senha123)
    passwd carlos -e
    
    #cria o usuário maria
    useradd maria -m -g GRP_ADM -p $ (openssl passwd -crypt Senha123)
    passwd maria -e
    
    #cria o usuário joão
    useradd joao -m -g GRP_ADM -p $ (openssl passwd -crypt Senha123)
    passwd joao -e
    
    #GRUPO GRP_VEN
    #cria o usuário debora
    useradd debora -m -g GRP_VEN -p $ (openssl passwd -crypt Senha123)
    passwd debora -e
    
    #cria o usuário sebastiano
    useradd sebastiano -m -g GRP_VEN -p $ (openssl passwd -crypt Senha123)
    passwd sebastiano -e
    
    #cria o usuário roberto
    useradd roberto -m -g GRP_VEN -p $ (openssl passwd -crypt Senha123)
    passwd roberto -e
    
    #GRUPO GRP_SEC
    #cria o usuário josefina
    useradd josefina -m -g GRP_SEC -p $ (openssl passwd -crypt Senha123)
    passwd josefina -e
    
    #cria o usuário amanda
    useradd amanda -m -g GRP_SEC -p $ (openssl passwd -crypt Senha123)
    passwd amanda -e
    
    #cria o usuário rogerio
    useradd rogerio -m -g GRP_SEC -p $ (openssl passwd -crypt Senha123)
    passwd rogerio -e
    
    echo "Usuários criados!"
    
    echo "Definindo o root como dono dos diretórios..."
    
    chown root:GRP_ADM /adm
    chown root:GRP_ADM /ven
    chown root:GRP_ADM /sec
    
    echo "Root agora é dono dos diretórios!"
    
    echo "Script executado com sucesso!"
    ```
    
    - `chmod +x  start_environment_pattern.sh`concede a permissão de execução do arquivo
    - `./start_environment_pattern.sh` executa o arquivo desejado
    

- Servidores
    - São utilizados como: servidor de arquivos, servidor web e servidor de banco de dados.
    - Servidor de arquivos
        - É necessário instalar o samba (para manipular arquivos SMB, do Windows)
        `apt install samba -y`
        - Cria-se uma pasta publica
        `mkdir publica`
        - Com permissão total a todos
        `chmod 777 publica`
        - Abre-se o arquivo de configuração do samba
        `nano /etc/samba/smb.conf`
        - Vá até o final do arquivo e adicione as seguintes linhas
        
        ```bash
        #[nomeDaPastaPublica/PastaParaSeCompartilhar]
        [publica]
        #path = diretórioDaPasta
        path = /disk2/publica
        writable = yes
        #Definir para que qualquer pessoa tenha acesso à pasta
        guest ok = yes
        #Definir que todos que acessarem serão apenas convidados (guest)
        guest only = yes
        #CTRL+O enter CTRL+X
        ```
        
        - O `systemctl` gerencia serviços em segundo plano. Neste caso vamos reiniciar o `smb` (samba). Termina em “d” pois ele é um `daemon` (serviço em segundo plano)
        `systemctl restart` 
        `systemctl restart smbd`
        - Verifique se o processo está em execução
        `systemctl status smbd`
        - Para iniciar o processo, use
        `systemctl enable smbd`
        - Verifique o ip do samba
        `ip a`
        - Para acessar o samba pelo Windows, abra o explorador de arquivos, e onde mostra o diretório, digite o ip
        `\\10.0.0.19\publica` e enter
        - OBS: só é possível acessar a pasta as pessoas cadastradas na lista do servidor
        `cat /etc/passwd`
        - É possível acessar conectando-se a um local de rede
            
            ![mapear unidade de rede](https://i.imgur.com/Xk3opkT.png)
            
    - Servidor Web
        - Instale o apache2
        `apt install apache2 -y`
        - Verifique se ele já está em execução
        `systemctl status apache2`
        - Verifique o ip do apache
        `ip a`
        - Abra o Chrome e conecte-se ao IP
        - Altere o conteúdo do index.html ou o exclua. Ele está no diretório
        `cd /var/www/html`
        - Para remover use
        `rm index.html`
        - E crie um novo
        `nano index.html`
        - Este servidor estará apenas habilitado localmente (apenas na sua rede). Para disponibilizar mundialmente, é necessário conectar por meio de um servidor (AWS, por exemplo)

---


1. **Instale o Servidor DHCP**:
   
   Certifique-se de que o servidor DHCP esteja instalado na máquina. Você pode usar o servidor DHCP ISC (Internet Systems Consortium), que é comumente usado no Debian. Se ainda não estiver instalado, execute o seguinte comando:

   ```bash
   sudo apt-get install isc-dhcp-server
   ```

2. **Configurar o DHCP Server**:

   Edite o arquivo de configuração `/etc/dhcp/dhcpd.conf` para configurar o servidor DHCP:

   ```bash
   sudo nano /etc/dhcp/dhcpd.conf
   ```

   Dentro do arquivo de configuração, você pode adicionar a configuração para a rede interna, como abaixo:

   ```plaintext
   subnet 192.168.10.0 netmask 255.255.255.0 {
       range 192.168.10.100 192.168.10.200;
       option routers 192.168.10.1;
       option domain-name-servers 8.8.8.8, 8.8.4.4;
   }
   ```

   - `subnet 192.168.10.0 netmask 255.255.255.0` define a rede e a máscara de sub-rede.
   - `range 192.168.10.100 192.168.10.200` define a faixa de endereços IP que o servidor DHCP pode atribuir aos clientes na rede interna.
   - `option routers 192.168.10.1` define o gateway padrão.
   - `option domain-name-servers 8.8.8.8, 8.8.4.4` define os servidores DNS a serem fornecidos aos clientes.

3. **Configurar a Interface de Rede Interna**:

   Você precisa atribuir o endereço IP à interface de rede interna (por exemplo, eth1) e configurá-la para que o servidor DHCP responda a solicitações nessa interface. Edite o arquivo de configuração da interface:

   ```bash
   sudo nano /etc/network/interfaces
   ```

   Adicione as configurações para a interface de rede interna:

   ```plaintext
   auto eth1
   iface eth1 inet static
       address 192.168.10.1
       netmask 255.255.255.0
   ```

   Reinicie a interface de rede:

   ```bash
   sudo ifdown eth1
   sudo ifup eth1
   ```

4. **Iniciar e Habilitar o Servidor DHCP**:

   Inicie o servidor DHCP e configure-o para ser executado na inicialização:

   ```bash
   sudo systemctl start isc-dhcp-server
   sudo systemctl enable isc-dhcp-server
   ```

Agora, seu servidor DHCP estará configurado para atribuir endereços IP na faixa 192.168.10.0/24 à rede interna. Certifique-se de que o roteamento esteja configurado corretamente se você desejar que os dispositivos da rede interna acessem a rede NAT e a Internet. Além disso, ajuste as configurações de firewall, se necessário, para permitir o tráfego entre as redes interna e NAT.

---

**DHCP

1. **Instale o servidor SSH no Linux:**

   Certifique-se de que o servidor SSH esteja instalado no seu servidor Linux. Geralmente, o OpenSSH é a escolha mais comum. Você pode verificar se o OpenSSH está instalado e instalá-lo, se necessário, usando os seguintes comandos:

   ```bash
   sudo apt update
   sudo apt install openssh-server
   ```

2. **Configurar o servidor SSH:**

   Por padrão, o OpenSSH é configurado para permitir acesso por senha. É altamente recomendável que você configure a autenticação baseada em chave, pois isso é mais seguro. No entanto, se desejar manter a autenticação por senha, siga estas etapas para configurar o servidor SSH.

   Abra o arquivo de configuração do SSH:

   ```bash
   sudo nano /etc/ssh/sshd_config
   ```

   Certifique-se de que as seguintes linhas estejam configuradas da seguinte forma:

   ```plaintext
   PasswordAuthentication yes
   PermitRootLogin no
   ```

   - `PasswordAuthentication` deve ser definido como `yes` se você quiser permitir a autenticação por senha. Se preferir usar autenticação baseada em chave, configure esta opção como `no`.
   - `PermitRootLogin` deve ser configurado como `no` para desabilitar o acesso direto como root.

   Após fazer as alterações, salve o arquivo e saia do editor de texto.

3. **Reinicie o Serviço SSH:**

   Após fazer as alterações na configuração, reinicie o serviço SSH para que as alterações tenham efeito:

   ```bash
   sudo systemctl restart ssh
   ```

4. **Encontre o Endereço IP do Servidor Linux:**

   Anote o endereço IP do servidor Linux para poder se conectar a ele.

5. **Baixe e Instale o PuTTY:**

   Baixe o PuTTY no site oficial (https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) e instale-o no seu computador Windows.

6. **Conecte-se ao Servidor Linux usando o PuTTY:**

   Abra o PuTTY e siga estas etapas:

   - Insira o endereço IP do servidor Linux na caixa "Host Name (or IP address)".
   - Certifique-se de que a porta esteja configurada para 22 (a porta padrão para SSH).
   - Escolha "SSH" como o tipo de conexão.
   - Clique em "Open" para iniciar a conexão.

   Se você estiver usando a autenticação por senha, o PuTTY solicitará a senha do usuário. Se estiver usando a autenticação baseada em chave, certifique-se de que sua chave privada esteja configurada no PuTTY (no menu "Connection" > "SSH" > "Auth").

Pronto! Agora você está conectado ao seu servidor Linux usando o PuTTY via SSH. Certifique-se de que a configuração de autenticação e segurança esteja de acordo com as melhores práticas para manter seu servidor seguro.


---

** PROXY

**Nota:** Antes de configurar um servidor proxy, certifique-se de que você tem autorização para fazê-lo e que está ciente das políticas de segurança da sua organização.

Aqui estão os passos para configurar um servidor proxy Squid:

1. **Instale o Squid:**

   Se o Squid ainda não estiver instalado, você pode fazê-lo com o seguinte comando:

   ```bash
   sudo apt-get update
   sudo apt-get install squid
   ```

2. **Configurar o Squid:**

   O arquivo de configuração principal do Squid está localizado em `/etc/squid/squid.conf`. Você pode editar este arquivo usando um editor de texto, como o `nano` ou o `vim`. 

   ```bash
   sudo nano /etc/squid/squid.conf
   ```

3. **Configurar as Opções Básicas:**

   Você pode definir opções básicas no arquivo de configuração do Squid. Aqui está um exemplo de configuração simples:

   ```plaintext
   # Define a porta em que o Squid irá escutar as solicitações de proxy.
   http_port 3128

   # Defina o nome da máquina do servidor proxy.
   visible_hostname myproxyserver

   # Permita o acesso somente a clientes na rede local.
   acl localnet src 192.168.1.0/24
   http_access allow localnet
   ```

   Lembre-se de personalizar as configurações de acordo com suas necessidades, como a porta, o nome do servidor, a faixa de IPs da rede local, etc.

5. **Reiniciar o Squid:**

   Após fazer as alterações no arquivo de configuração, reinicie o serviço do Squid para aplicar as configurações:

   ```bash
   sudo systemctl restart squid
   ```

6. **Configurar Clientes para Usar o Proxy:**

   Agora, você precisa configurar os clientes para usar o proxy Squid. Isso geralmente é feito nas configurações do navegador ou nas configurações de rede dos clientes.

Após seguir essas etapas, você terá um servidor proxy Squid básico em funcionamento. Certifique-se de ajustar a configuração de acordo com as necessidades específicas da sua rede e de implementar medidas de segurança apropriadas.


---

- SERVIDOR FTP


**Passo 1: Instalar o vsftpd**

Abra um terminal e execute os seguintes comandos como superusuário ou com "sudo" (substitua "seu_usuario" pelo seu nome de usuário):

```bash
sudo apt update
sudo apt install vsftpd
```

Isso irá atualizar a lista de pacotes disponíveis e instalar o servidor FTP vsftpd.

**Passo 2: Configurar o vsftpd**

Após a instalação, você precisa configurar o vsftpd de acordo com suas necessidades. O arquivo de configuração do vsftpd está localizado em `/etc/vsftpd.conf`. Você pode editá-lo com um editor de texto, como o nano:

```bash
sudo nano /etc/vsftpd.conf
```

Dentro do arquivo de configuração, você pode ajustar várias opções, como as seguintes configurações comuns:

- Habilitar ou desabilitar o acesso anônimo:

  ```
  anonymous_enable=NO
  ```

- Definir o diretório raiz para os usuários:

  ```
  local_root=/home/seu_usuario
  ```

- Permitir gravação de arquivos:

  ```
  write_enable=YES
  ```

Altere essas configurações de acordo com suas necessidades. Salve o arquivo após fazer as alterações.

**Passo 3: Reiniciar o vsftpd**

Após a configuração, reinicie o serviço vsftpd para aplicar as alterações:

```bash
sudo systemctl restart vsftpd
```

**Passo 4: Abrir as portas FTP no firewall**

Se você estiver usando um firewall, certifique-se de abrir as portas FTP (geralmente 20 e 21) para permitir a comunicação com o servidor FTP. Dependendo do firewall que você está usando, os comandos podem variar. Por exemplo, para abrir as portas no iptables, você pode usar algo como:

```bash
sudo iptables -A INPUT -p tcp --dport 20 -j ACCEPT
sudo iptables -A INPUT -p tcp --dport 21 -j ACCEPT
```

**Passo 5: Criar contas de usuário FTP**

Para permitir que os usuários acessem seu servidor FTP, você precisa criar contas de usuário no sistema. Use o seguinte comando para adicionar um novo usuário (substitua "nome_do_usuario" pelo nome de usuário desejado):

```bash
sudo adduser nome_do_usuario
```

Defina uma senha forte para o usuário quando solicitado.

**Passo 6: Testar a conexão FTP**

Agora que seu servidor FTP está configurado, você pode testar a conexão de um cliente FTP. Use um cliente FTP, como o FileZilla, ou o cliente de linha de comando `ftp` para se conectar ao servidor FTP.

Certifique-se de usar o nome de usuário e a senha que você criou para acessar o servidor FTP.

Com esses passos, você deve ter um servidor FTP funcionando no seu sistema Debian Linux. Lembre-se de configurar a segurança apropriada, como o uso de FTP seguro (FTP sobre TLS/SSL), e de restringir o acesso apenas aos diretórios necessários para garantir a segurança do servidor.
