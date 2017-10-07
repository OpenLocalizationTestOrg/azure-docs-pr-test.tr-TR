---
title: "bir Hadoop korumalı - öykünücüsü - Azure Hdınsight kullanarak aaaLearn | Microsoft Docs"
description: "Hadoop ekosistemi kullanma hakkında öğrenme toostart Merhaba, bir Azure sanal makinesi üzerinde Hortonworks bir Hadoop korumalı ayarlayabilirsiniz. "
keywords: "hadoop öykünücüsü, hadoop korumalı alan"
editor: cgronlun
manager: jhubbard
services: hdinsight
author: nitinme
documentationcenter: 
tags: azure-portal
ms.assetid: 6ad5bb58-8215-4e3d-a07f-07fcd8839cc6
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 91e74f0823fd02e9bb812155a7d09357a77b0736
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-a-hadoop-sandbox-an-emulator-on-a-virtual-machine"></a>Bir Hadoop korumalı bir sanal makinede bir öykünücü kullanmaya başlama

Nasıl tooinstall hello korumalı alan Hortonworks gelen Hadoop üzerinde bir sanal makine toolearn hello Hadoop ekosistemi hakkında bilgi edinin. Merhaba sandbox Hadoop, Hadoop dağıtılmış dosya sistemi (HDFS) ve iş gönderme ilgili yerel geliştirme ortamı toolearn sağlar. Hadoop ile hakkında bilgi sahibi olduktan sonra Hdınsight kümesi oluşturarak Azure üzerinde Hadoop kullanmaya başlayabilirsiniz. Tooget çalışmaya nasıl daha fazla bilgi için bkz: [hdınsight'ta Hadoop kullanmaya başlama](hdinsight-hadoop-linux-tutorial-get-started.md).

## <a name="prerequisites"></a>Ön koşullar
* [Oracle VirtualBox](https://www.virtualbox.org/). Buradan yükleyip [burada](https://www.virtualbox.org/wiki/Downloads).



## <a name="download-and-install-hello-virtual-machine"></a>Merhaba sanal makineye yükleyip
1. Toohello Gözat [Hortonworks indirmeleri](http://hortonworks.com/downloads/#sandbox).

2. Tıklatın **İNDİRMEK için VIRTUALBOX** toodownload hello son Hortonworks korumalı alan bir VM üzerinde. Merhaba yükleme başlamadan önce istendiğinde tooregister Hortonworks ile demektir. Ağ hızınıza bağlı olarak bir tootwo saatleri toodownload alır.
   
    ![İçin bağlantı görüntüsünü karşıdan yüklemek için VirtualBox Hortonworks korumalı alan](./media/hdinsight-hadoop-emulator-get-started/download-sandbox.png)
3. Gelen Merhaba aynı web sayfasında, hello tıklatın **sanal kutusundaki içeri aktarma** hello sanal makine için yükleme yönergeleri içeren bir PDF toodownload bağlantı.

toodownload daha eski bir HDP sürüm sandbox hello arşiv genişletin:

![Hortonworks Sandbox arşiv](./media/hdinsight-hadoop-emulator-get-started/hortonworks-sandbox-archive.png)


## <a name="start-hello-virtual-machine"></a>Merhaba sanal makineyi Başlat

1. Oracle VM VirtualBox açın.
2. Hello gelen **dosya** menüsünde tıklatın **alma Gereci**ve ardından hello Hortonworks Sandbox görüntüsü belirtin.
1. Select hello Hortonworks Sandbox tıklatın **Başlat**ve ardından **Normal başlangıç**. Merhaba sanal makine hello önyükleme işlemi tamamlandıktan sonra oturum açma yönergeleri görüntüler.
   
    ![Normal Başlat](./media/hdinsight-hadoop-emulator-get-started/normal-start.png)
2. Bir web tarayıcısı açın ve görüntülenen toohello URL (genellikle http://127.0.0.1:8888) gidin.

## <a name="set-sandbox-passwords"></a>Korumalı alan parola ayarlama

1. Merhaba gelen **başlama** hello Hortonworks Sandbox sayfasında, adım **görünüm Gelişmiş Seçenekler**. Bu sayfa toolog SSH kullanarak toohello korumalı alanı içinde üzerinde Hello bilgileri kullanın. Sağlanan Hello adını ve parolayı kullanın.
   
   > [!NOTE]
   > Bir SSH istemcisi yüklü değil, web tabanlı SSH sağlayan en hello sanal makinenin hello kullanabilirsiniz **http://localhost:4200 /**.
   > 
   
    Merhaba SSH, bağlanırken ilk kez istendiğinde toochange hello hello kök hesabının parolasını olduğunuz. SSH kullanarak oturum açışınızda kullanacağınız yeni bir parola girin.

2. Oturum açtıktan sonra komutu aşağıdaki hello girin:
   
        ambari-admin-password-reset
   
    İstendiğinde, hello Ambari yönetici hesabı için bir parola sağlayın. Merhaba Ambari Web kullanıcı arabirimini eriştiğinizde bu kullanılır.

## <a name="use-hive-commands"></a>Hive komutları kullanın

1. Bir SSH bağlantısı toohello sandbox komut toostart hello Hive kabuğunu aşağıdaki hello kullan:
   
        hive
2. Merhaba Kabuk başladıktan sonra hello sandbox ile sağlanan tooview hello tabloları aşağıdaki hello kullan:
   
        show tables;
3. Hello tooretrieve 10 satır aşağıdaki kullanım hello `sample_07` tablosu:
   
        select * from sample_07 limit 10;

## <a name="next-steps"></a>Sonraki adımlar
* [Bilgi nasıl toouse Visual Studio ile Merhaba Hortonworks korumalı alan](hdinsight-hadoop-emulator-visual-studio.md)
* [Merhaba ipleri hello Hortonworks korumalı alan, öğrenme](http://hortonworks.com/hadoop-tutorial/learning-the-ropes-of-the-hortonworks-sandbox/)
* [Hadoop Öğreticisi - HDP ile çalışmaya başlama](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/)

