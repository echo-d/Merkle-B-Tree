Merkle B Tree
==============

An implementation of Merkle B Tree, which is a combination of B+ Tree and Merkle Hash Tree.
Merkle B Tree
==============

An implementation of Merkle B Tree, which is a combination of B+ Tree and Merkle Hash Tree.


1、环境：在windows上使用wsl，ubuntu22.04，vscode，
    vscode需要安装 Remote - SSH，Dev Containers，C/C++ Extension Pack

2、Merkle B Tree/Crypto.h 报错，找不到文件openssl/rsa.h
需要安装openssl： 
sudo apt-get install openssl
sudo apt-get update
查看是否安装成功：/usr/bin/openssl version

3、在c_cpp_properties.json includePath中添加：
            "includePath": [
                "${workspaceFolder}/**",
                "/usr/include",
                "/usr/include/openssl"
            ],

4、踩坑：原文件中使用“\”, 需要更改为“/”
#include <openssl/rsa.h>
#include <openssl/evp.h>
有多处斜杠需要注意更改

5、测试数据：
/Dataset/CAL.cnode: graph的node，第一列:id(编号), 第二列和第三列可能表示经纬度
/Dataset/CAL.cedge：graph的edge，第一列到第四列应该是 源节点ID、目标节点ID，length， 第四列是poi（我理解是权重）

6、编译命令，程序入口是Driver.cpp，有一个测试生成MB tree时长的例子，代码中被注释掉的部分是使用测试生成VO并验证VO的案例
g++ -o Driver Driver.cpp Graph.cpp MerkleBTree.cpp Tools.cpp NodeHeap.cpp Crypto.cpp AuthenticationTree.cpp -lcrypto

7、使用测试数据运行命令：
./Driver Dataset/CAL.cnode Dataset/CAL.cedge test.txt 3 
//分别是nodeFilename edgeFilename outputFilename fanout（MBtree的阶，默认11）


