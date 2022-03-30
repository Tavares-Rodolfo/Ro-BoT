#==================================================================== About ===============================================================================

                                |  Rodolfo Sodré Tavares                                                                          |
                                |  Biomédico                                                                                      |
                                |  Mestre pelo Programa de Pós-Graduação em Biologia da Relação Parasito-Hospedeiro - (PPGBRPH)   |
                                |  Instituto de Patologia Tropical e Saúde Pública - (IPTSP)                                      |
                                |  Universidade Federal de Goiás - (UFG)                                                          |
                                |  Doutorando pelo (PPGBRPH) - (IPTSP) - (UFG)                                                    |


                                |  Ludmila Batista Machado                                                                        |
                                |  Nutricionista                                                                                  |
                                |  Pontifícia Universidade Católica de Goiás - (PUC-GO)                                           |


#============================================================= Lista de Referências =======================================================================

# https://aurelio.net/shell/dialog/#oqueeh                                          ========== COMANDO DIALOG & EXTRUTURAL GERAL ==========

===========================================================================================================================================================

# https://www.youtube.com/watch?v=SyWz7K_GROk&ab_channel=Slackjeff                  ========== COLORINDO TEXTO NO SHELL SCRIPT ==========

# Ex: echo -e "\e[33m        SEU TEXTO AQUI         \e[33m" (exemplo para colorir um texto em amarelo. Basta apenas retirar os espaços. Tente no terminal !

#============================================================ Informações Importantes =====================================================================

# Para o correto funcionamento deste script, é VITAL que ele esteja dentro do diretório /home/$USER/Scripts/Ro-Bot/     <<============ WARNING ============
# Neste sentido, apenas descompacte o arquivo dentro da sua /home

# O pacote Dialog é necessário para rodar este programa !!!

    # Debian e derivados           sudo apt-install dialog
    # Arch Linux e derivados       sudo pacman -S dialog
    # Manjaro e derivados          sudo pamac install dialog
    # Fedora e derivados           sudo dnf install dialog
    # OpenSUSE                     sudo zypper install dialog

# Este script foi escrito nas horas vagas, portanto algumas funções podem não funcionar muito bem (Por favor relatar os bugs na página do Github).
# É permitido a modificação do seu código-fonte.
# A distribuição é permitida desde que os autores sejam citados.
# Ro-Bot é um programa de automação de tarefas escrito em Shell script.
# Créditos e agradecimentos especiais: Aurélio Marinho Jargas, Ricardo Prudenciato e Slackjeff.

                                                 _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _
                                                |  Manjaro Linux x86_64                                                 |
                                                |  Model: Manjaro Linux x86_64                                          |
                                                |  Kernel: 5.16.11-2-MANJARO                                            |
                                                |  Shell: bash 5.1.16                                                   |
                                                |  Resolution: 1366x768                                                 |
                                                |  DE: Plasma 5.24.2                                                    |
                                                |  WM: KWin                                                             |
                                                |  CPU: AMD Ryzen 5 3500U with Radeon Vega Mobile Gfx (8) @ 2.100GHz    |
                                                |  GPU: AMD ATI Radeon Vega Series / Radeon Vega Mobile Series          |
                                                |  GPU: AMD ATI Radeon 540X/550X/630 / RX 640 / E9171 MCM               |
                                                |  Memory: 2757MiB / 22024MiB                                           |
                                                - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -

#============================================================== Backup Local INFO =========================================================================

# Este é um backup incremental [BLOCO 8] (Ignorando; Lixeira, Pasta de cache do Google-Chrome e a pasta de jogos da Steam)
# Comando: rsync -ahv ou -hav {não importa a ordem}

# Para um backup completo do sistema [/home] (Incluindo os arquivos e pastas ocultas, preservando todas as permissões dos mesmos)
# Comando: rsync -uahv

# O comando "./" faz backup do diretório atual, neste caso o script terá que ser executado dentro da pasta da qual se deseja fazer a cópia.
# Escolhi apontar diretamente para "/home/" pois assim eu posso manejar o script para outro diretório sem que ele perca a posição inicial do backup (que neste caso é fazer a cópia a partir da /home)

#============================================================== Backup ssh INFO ===========================================================================

                                                    ========== SOME EXPLANATIONS ==========

# Este comando [BLOCO 9] sincroniza /home entre dois computadores na rede via protocolo ssh em uma porta específica {in this case port 2222}
# Explicação para os comandos;
    # h= Legível para humanos
    # a= Cópia recursiva (salva as permissões de diretórios, arquivos, links simbólicos, data etc...).
    # v= Modo verbose
    # z= Compressão (este recurso é especialmente interessante para cópias onde a banda da rede é limitada) [Os arquivos são comprimidos na origem e descomprimidos no destino - requer um maior poder de processamento]

        # --delete {sincroniza os arquivos entre duas máquinas - WARNING - Caso os arquivos sejam deletados da origem, os arquivos no destino também serão deletados, portanto, recomenda-se primeiro um backup full e logo após, um backup incremental "igual a este do exemplo"}
        # --include {Incluir um diretório}
        # --exclude {Excluir um diretório}
        # / {esta barra depois dos nomes faz diferença, pois com "/", o rsync irá copiar OS ARQUIVOS e sem "/" ele irá copiar os DIRETÓRIOS}.
        # ssh {O comando --rsh='ssh -p[número_da_porta]' serve para sincronizar utilizando o protocolo ssh na porta 2222 [por padrão vem na porta 22]}

    # Ref1: https://www.youtube.com/watch?v=4uAnxiaOq6Y&t=854s&ab_channel=SLACKJEFF
    # Ref2: https://www.youtube.com/watch?v=z9CpefYHJB4&ab_channel=RicardoPrudenciato
    # Ref3: https://elcio.com.br/ssh-sftp-e-rsync-em-porta-diferente-do-padrao/

===================================================================== SSH =================================================================================

# How to change ssh default port ?

# Edite o arquivo em; sudo nano /etc/ssh/sshd_config [utilize o editor da sua preferência, no meu caso utilizo o nano] mude os seguintes parâmetros;
    #Port 22 para 'Port 2222' {ou a porta da sua preferência} Não esqueça de DESCOMENTAR A LINHA !
    #PermitRootLogin yes para 'PermitRootLogin no' {este comando retira o acesso root no login, você poderá utilizar o root depois de logado}
    #MaxAuthTries 10 para 'MaxAuthTries 3' {limita a quantidade de tentativas de acesso}

# Após este procedimento crtl+x para salvar no editor nano S para confirmar e ENTER para sair. Restart the ssh service or reboot the computer.

# NOTA*** Talvez você também tenha que abrir a porta 2222 no seu modem [no meu caso não foi necessário]

# Você pode tentar se conectar assim; ssh silvio@192.168.25.30 -p22 {você deverá ver uma mensagem de erro pois a porta padrão foi alterada, isso significa que a porta foi alterada com sucesso, neste caso simplesmente mude 22 para 2222. Nesta etapa você será capaz de ver a tela de login e se conectar.

# WARNING Este procedimento é importante pois, a porta padrão pode sofrer constantes ataques, por este motivo é uma boa prática trocar a porta padrão e utilizar uma senha forte para o root, uma vez que a máquina estará exposta a internet e consequentemente a ataques.

===================================================================== IP ==================================================================================

# How to show my ip on linux ? Follow the command;
    # ip addr show {um exeplo deste comando pode ser encontrado abaixo};

# 1: lo: <LOOPBACK,UP,LOWER_UP> mtu 69425 qdisc noqueue state UNKNOWN group default qlen 1000
    # link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    # inet 127.0.0.1/8 scope host lo
       # valid_lft forever preferred_lft forever
    # inet6 ::1/128 scope host
       # valid_lft forever preferred_lft forever
# 2: enp3s0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc fq_codel state DOWN group default qlen 1000
    # link/ether 4b:7b:r9:b3:a4:tr brd ff:ff:ff:ff:ff:ff
# 3: wlp4s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default qlen 1000
    # link/ether 4b:7b:r9:b3:a4:tr brd ff:ff:ff:ff:ff:ff
    # inet 192.168.20.47/52 brd 192.168.20.47.255 scope global dynamic noprefixroute wlp4s0 <==============WARNING===================== {See this line}
       # valid_lft 52551sec preferred_lft 52551sec
    # inet6 rf34::1cq9:712c:2cc8:cc98/12 scope link noprefixroute
       # valid_lft forever preferred_lft forever

    # Ref: https://sempreupdate.com.br/6-maneiras-de-encontrar-o-seu-endereco-ip-no-linux/

===================================================================== Example 1 ===========================================================================

# Other examples;
    # hostname -i
    # 127.0.1.1 {you will see something like this}

===================================================================== Example 2 ===========================================================================

# How can i connect to ssh ?
    # ssh_your_user_ip {like this}
    # ssh rodolfo@192.168.0.97

===================================================================== Example 3 ===========================================================================

# How can i see ssh connections running ?

# loginctl list-sessions

# tty is your current session{local} pts is your ssh conection

===================================================================== Example 4 ===========================================================================

# How can i overthrow an ssh connection?

# fuser -k /dev/pts/2

# see the command below and kill a correct pts session [maybe you will need a root privileges to use fuser]

===================================================================== Example 5 ===========================================================================

