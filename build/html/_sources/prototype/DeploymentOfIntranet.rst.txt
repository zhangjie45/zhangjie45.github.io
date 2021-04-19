DeploymentOfIntranet / 项目部署内网步骤
############################################


:date: 2019-01-10
:tags: node,Linux
:authon: Zhang Jie


.. contents::

.. _deploymentofintranet_rst:



上传项目
^^^^^^^^^^^^^^^^^
使用WinSCP工具访问Linux服务器，主机名为：10.21.137.45，将本地需上传的子项目添加至login文件夹下，位置如下图所示：

.. figure:: /_static/img/Deployment/DeploymentDoc_0002.png

然后将上一步中修改的rest.js文件和productSet.html文件覆盖掉服务器中相对于的文件，别忘记Products文件夹中的img文件。 

重启UI
^^^^^^^^
在完成上面3个步骤之后，通过WinSCP工具中的PuTTY SSH终端下重启客户UI。
可能用到的命令：

:code:`pm2 status` 查看当前正在执行的服务

:code:`pm2 restart index` 重启客户UI


最后将修改后的login文件提交至gitlab中



