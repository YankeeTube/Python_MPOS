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


PowerPool 설치 및 설정
---------------------

..code-block:: bash
    
    mkvirtualenv pp
    cd .virtualenv/pp
    git clone https://github.com/YankeeTube/Python_MPOS.git
    cd powerpool
    pip install -r requirement.stxt
    
    
SSL.py 수정
-----------

..code-block:: bash
    
    sudo vim home/username/.virtualenvs/pp/local/lib/python2.7/site-packages/gevent/ssl.py
    
    # Line 386
    # 변경 전
    def get_server_certificate(addr, ssl_version=PROTOCOL_SSLv3, ca_cert=None,
    
    # 변경 후
    def get_server_certificate(addr, ssl_version=PROTOCOL_SSLv23, ca_cert=None,
    
    
PowerPool 나머지 설치
--------------------

..code-block:: bash
    
    pip install -e .
    #pip install vtc_scrypt # scryptn Algorithm 지원
    pip install drk_hash # x11 Algorithm 지원
    #pip install ltc_scrypt # scrypt Algorithm 지원
    pip install git+https://github.com/BlueDragon747/Blakecoin_Python_POW_Module.git@e3fb2a5d4ea5486f52f9568ffda132bb69ed8772#egg=blake_hash
    cp config.exmaple.yml config.yml
    
    
redis & celery 설치
------------------

..code-block:: bash
    
    sudo apt-get install redis-server -y
    sudo pip install redis
    sudo pip install celery
    

Linux Wine 설치[선택사항]
------------------------

..code-block:: bash

    sudo add-apt-repository ppa:wine/wine-builds
    sudo apt-get update
    sudo apt-get install --install-recommends winehq-staging
    

SOOM Wallet Download
--------------------

..code-block:: bash
    
    https://github.com/YankeeTube/Shell-Script/raw/master/soomcoin-qtV1.003n.zip
    

PowerPool Monitor.py 수정
------------------------

..code-block:: bash
    
    sudo vim .virtualenvs/pp/powerpool/monitor.py
    # Line 77
    # 변경 전
    defaults = dict(address="127.0.0.1",
    
    # 변경 후
    defaults = dict(address="0.0.0.0",
    
YAML 설정
---------

..code-block:: bash
    
    sudo vim ~/.virtualenvs/pp/powerpool/config.yml
    
    
    # This is only really needed for SimpleMulti
    RR:
        type: powerpool.reporters.RedisReporter
        redis:
            db: 15
        # Configures special users which will get all the pool shares reported to
        # them
        pool_report_configs:
            - worker_format_string: "{chain}"
              user: "pool"
            - worker_format_string: "{currency}"
              user: "pool_currency"
              report_merge: True
            - worker_format_string: "{algo}"
              user: "pool_algo"

        # **** ADD THIS ****
        attrs:
            # Name to report in the pool stats graph. This can be different per stratum if desired.
            # You have to include this key (or disable redis reporting) or PowerPool will fail.
            chain: " Republic Of Korea"
    CR:
        type: powerpool.reporters.CeleryReporter
        # **** ADD THIS ****
        # Configures special users which will get all the pool shares reported to
        # them
        pool_report_configs:
            - worker_format_string: "{chain}"
              user: "pool"
            # I don't think you really need the two below for SimpleCoin, but whatever.
            - worker_format_string: "{currency}"
              user: "pool_currency"
              report_merge: True
            - worker_format_string: "{algo}"
              user: "pool_algo"
        attrs:
            chain: “Republic Of Korea"
           
        #LTC:
        #    type: powerpool.jobmanagers.MonitorNetwork
        #    merged:
        #        - SYS
        #    algo: scrypt
        #    currency: LTC
        #    pool_address: mri1PEngsRuU6aLKQJ5gGePUdEo76C6DeT
        #    coinservs:
        #        - port: 20001
        #          address: 127.0.0.1
        #          username: admin1
        #          password: 123
        #          poll_priority: 100

        SUM:
            type: powerpool.jobmanagers.MonitorNetwork
        algo: x11
            currency: SUM
            pool_address: SRHBRcJHK8TWboYAy2eSdaZpVWrkkCFtTv
            coinservs:
                - port: 13801
                  address: 127.0.0.1
                  username: soomrpcuser
                  password: x
                  poll_priority: 100

        #SYS:
        #    type: powerpool.jobmanagers.MonitorAuxNetwork
        #    algo: scrypt
        #    signal: 28
        #    currency: SYS
        #    coinservs:
        #        - port: 19001
        #          address: 127.0.0.1
        #          username: admin1
        #          password: 123
        #          poll_priority: 100

        #TEST_STRAT:
        Python_MPOS_START:
            type: powerpool.stratum_server.StratumServer
            algo: x11
            jobmanager: SUM
            reporter: DR
            start_difficulty: 0.001

        MON:
            type: powerpool.monitor.ServerMonitor

