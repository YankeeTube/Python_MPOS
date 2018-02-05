================================
SimpleCrypto, Sigwo, mathframer
================================

작성한 내용을 기반으로 에러 및 한글버전으로 수정한 내용입니다.
--------------------------------------------------------------

마지막 수정일자 : 2018.02.02



파이썬 및 다른 프로그램 설치
----------------------------
.. code-block:: bash
    
    sudo apt-get install python python-pip -y 
    sudo apt-get install git curl vim -y


파이썬 패키지 업그레이드 및 가상환경 설치
-----------------------------------------
.. code-block:: bash

    sudo pip install --upgrade pip
    sudo pip install virtualenv virtualenvwrapper
    mkdir ~/.virtualenvs
    sudo vim .bashrc


.bashrc 내용 수정(맨 아래 추가)
-------------------------------
.. code-block:: bash

    export WORKON_HOME=~/.virtualenvs
    source /usr/local/bin/virtualenvwrapper.sh


재부팅
------
.. code-block:: bash

    sudo reboot now


rabbitmq-server 설치를 위한 erlang 설치
---------------------------------------
.. code-block:: bash

    wget https://packages.erlang-solutions.com/erlang-solutions_1.0_all.deb
    sudo dpkg -i erlang-solutions_1.0_all.deb
    sudo apt-get update
    sudo apt-get install erlang erlang-nox


rabbitmq deb 및 Public 키 생성
------------------------------
.. code-block:: bash

    echo 'deb http://www.rabbitmq.com/debian/ testing main' | sudo tee /etc/apt/sources.list.d/rabbitmq.list
    wget -O- https://www.rabbitmq.com/rabbitmq-release-signing-key.asc | sudo apt-key add -
    sudo apt-get update


update 오류 시 | Ubuntu 16.04
-----------------------------
.. code-block:: bash

    echo "deb https://dl.bintray.com/rabbitmq/debian xenial main" | sudo tee /etc/apt/sources.list.d/bintray.rabbitmq.list
    wget -O- https://www.rabbitmq.com/rabbitmq-release-signing-key.asc | sudo apt-key add -
    sudo apt-get update


update 오류 시 | Ubuntu 17.10
-----------------------------
.. code-block:: bash

    echo "deb https://dl.bintray.com/rabbitmq/debian artful main" | sudo tee /etc/apt/sources.list.d/bintray.rabbitmq.list
    wget -O- https://www.rabbitmq.com/rabbitmq-release-signing-key.asc | sudo apt-key add -
    sudo apt-get update


rabbitmq-server 설치
--------------------
.. code-block:: bash

    sudo apt-get install rabbitmq-server
    sudo vim /etc/default/rabbitmq-server


rabbitmq-server 설정
--------------------
.. code-block:: bash

    unlimit -n 1024 # 주석 해제


rabbitmq-server 계정 생성 설정 및 GUI 활성화
--------------------------------------------
.. code-block:: bash

    sudo rabbitmq-plugins enable rabbitmq_management # Browser GUI Enabled
    sudo rabbitmqctl add_user radmin radmin # add_user [username] [password]
    sudo rabbitmqctl set_user_tags radmin administrator # [username] [permission]
    sudo rabbitmqctl set_permissions ?p / radmin “.*” “.*” “.*” # [owner] [group] [other]


rabbitmq-server GUI로 보기
--------------------------
    http://localhost:15672
    username : radmin
    password : radmin


