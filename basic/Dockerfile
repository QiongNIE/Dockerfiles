FROM nvidia/cuda:10.1-cudnn7-devel
#update source list
RUN sed -i 's#http://archive.ubuntu.com/ubuntu#http://mirrors.163.com/ubuntu/#' /etc/apt/sources.list && \ 
    apt-get update --fix-missing && \
    apt-get upgrade -y && \
    # aptitude
    apt-get install aptitude -y && \
    aptitude update && \
    # curl
    aptitude install -y curl && \
    # vim
    aptitude install -y vim && \
    # git
    aptitude install -y git && \
    # wget
    aptitude install -y wget && \
    # cmake
    aptitude install -y cmake && \
    aptitude install -y cmake-gui && \
    # htop
    aptitude install -y htop &&\
    # screen
    aptitude install -y screen &&\
    # clean
    aptitude clean

# zsh
RUN aptitude install -y zsh  powerline fonts-powerline && \
    chsh -s /bin/zsh && zsh

RUN    git clone https://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh && \
    cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc && \
    git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ~/.oh-my-zsh/custom/plugins/zsh-syntax-highlighting && \
    git clone git://github.com/zsh-users/zsh-autosuggestions ~/.oh-my-zsh/custom/plugins/zsh-autosuggestions && \
    aptitude install -y autojump && \
    sed -i "s/plugins=(git)/plugins=(git zsh-syntax-highlighting zsh-autosuggestions autojump)/" ~/.zshrc


# conda
RUN wget --quiet https://repo.anaconda.com/archive/Anaconda3-2019.07-Linux-x86_64.sh -O /home/anaconda.sh && \
    /bin/bash /home/anaconda.sh -b -p /opt/conda && \
    ln -s /opt/conda/etc/profile.d/conda.sh /etc/profile.d/conda.sh && \
    rm /home/anaconda.sh && \
    echo "export PATH=/opt/conda/bin:$PATH" >> ~/.zshrc

RUN /opt/conda/bin/conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main && \
    /opt/conda/bin/conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/menpo && \
    /opt/conda/bin/conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge && \
    /opt/conda/bin/conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/pytorch

#SSH
RUN aptitude update && aptitude install -y openssh-server && \
    mkdir /var/run/sshd && \
    echo 'root:`' | chpasswd && \
    sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config && \
    sed -i 's/#X11DisplayOffset 10/X11DisplayOffset 10/' /etc/ssh/sshd_config && \
    sed -i 's/#X11UseLocalhost yes/X11UseLocalhost no/' /etc/ssh/sshd_config && \
    sed -i 's/#AllowTcpForwarding yes/AllowTcpForwarding yes/' /etc/ssh/sshd_config && \
    sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd && \
    echo "export VISIBLE=now" >> /etc/profile && \
    aptitude clean

RUN aptitude update && aptitude install -y locales && \
    locale-gen en_US en_US.UTF-8 zh_CN.UTF-8 && update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]



