================================
SimpleCrypto, Sigwo, mathframer
================================

�ۼ��� ������ ������� ���� �� �ѱ۹������� ������ �����Դϴ�.
--------------------------------------------------------------

������ �������� : 2018.02.02
----------------------------


���̽� �� �ٸ� ���α׷� ��ġ
----------------------------
.. code-block:: bash
    
    sudo apt-get install python python-pip -y 
    sudo apt-get install git curl vim -y


���̽� ��Ű�� ���׷��̵� �� ����ȯ�� ��ġ
-----------------------------------------
.. code-block:: bash

    sudo pip install --upgrade pip
    sudo pip install virtualenv virtualenvwrapper
    mkdir ~/.virtualenvs
    sudo vim .bashrc


.bashrc ���� ����(�� �Ʒ� �߰�)
-------------------------------
.. code-block:: bash

    export WORKON_HOME=~/.virtualenvs
    source /usr/local/bin/virtualenvwrapper.sh


�����
------
.. code-block:: bash

    sudo reboot now


rabbitmq-server ��ġ�� ���� erlang ��ġ
---------------------------------------
.. code-block:: bash

    wget https://packages.erlang-solutions.com/erlang-solutions_1.0_all.deb
    sudo dpkg -i erlang-solutions_1.0_all.deb
    sudo apt-get update
    sudo apt-get install erlang erlang-nox


rabbitmq deb �� Public Ű ����
------------------------------
.. code-block:: bash

    echo 'deb http://www.rabbitmq.com/debian/ testing main' | sudo tee /etc/apt/sources.list.d/rabbitmq.list
    wget -O- https://www.rabbitmq.com/rabbitmq-release-signing-key.asc | sudo apt-key add -
    sudo apt-get update


update ���� �� | Ubuntu 16.04
-----------------------------
.. code-block:: bash

    echo "deb https://dl.bintray.com/rabbitmq/debian xenial main" | sudo tee /etc/apt/sources.list.d/bintray.rabbitmq.list
    wget -O- https://www.rabbitmq.com/rabbitmq-release-signing-key.asc | sudo apt-key add -
    sudo apt-get update


update ���� �� | Ubuntu 17.10
-----------------------------
.. code-block:: bash
    echo "deb https://dl.bintray.com/rabbitmq/debian artful main" | sudo tee /etc/apt/sources.list.d/bintray.rabbitmq.list
    wget -O- https://www.rabbitmq.com/rabbitmq-release-signing-key.asc | sudo apt-key add -
    sudo apt-get update


rabbitmq-server ��ġ
--------------------
.. code-block:: bash

    sudo apt-get install rabbitmq-server
    sudo vim /etc/default/rabbitmq-server


rabbitmq-server ����
--------------------
.. code-block:: bash

    unlimit -n 1024 # �ּ� ����


rabbitmq-server ���� ���� ���� �� GUI Ȱ��ȭ
--------------------------------------------
.. code-block:: bash

    sudo rabbitmq-plugins enable rabbitmq_management # Browser GUI Enabled
    sudo rabbitmqctl add_user radmin radmin # add_user [username] [password]
    sudo rabbitmqctl set_user_tags radmin administrator # [username] [permission]
    sudo rabbitmqctl set_permissions ?p / radmin ��.*�� ��.*�� ��.*�� # [owner] [group] [other]


rabbitmq-server GUI�� ����
--------------------------
    http://localhost:15672
    username : radmin
    password : radmin


