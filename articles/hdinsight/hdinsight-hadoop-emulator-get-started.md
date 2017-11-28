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
# <a name="get-started-with-a-hadoop-sandbox-an-emulator-on-a-virtual-machine"></a><span data-ttu-id="1ae32-104">Bir Hadoop korumalı bir sanal makinede bir öykünücü kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="1ae32-104">Get started with a Hadoop sandbox, an emulator on a virtual machine</span></span>

<span data-ttu-id="1ae32-105">Nasıl tooinstall hello korumalı alan Hortonworks gelen Hadoop üzerinde bir sanal makine toolearn hello Hadoop ekosistemi hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="1ae32-105">Learn how tooinstall hello Hadoop sandbox from Hortonworks on a virtual machine toolearn about hello Hadoop ecosystem.</span></span> <span data-ttu-id="1ae32-106">Merhaba sandbox Hadoop, Hadoop dağıtılmış dosya sistemi (HDFS) ve iş gönderme ilgili yerel geliştirme ortamı toolearn sağlar.</span><span class="sxs-lookup"><span data-stu-id="1ae32-106">hello sandbox provides a local development environment toolearn about Hadoop, Hadoop Distributed File System (HDFS), and job submission.</span></span> <span data-ttu-id="1ae32-107">Hadoop ile hakkında bilgi sahibi olduktan sonra Hdınsight kümesi oluşturarak Azure üzerinde Hadoop kullanmaya başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1ae32-107">Once you are familiar with Hadoop, you can start using Hadoop on Azure by creating an HDInsight cluster.</span></span> <span data-ttu-id="1ae32-108">Tooget çalışmaya nasıl daha fazla bilgi için bkz: [hdınsight'ta Hadoop kullanmaya başlama](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="1ae32-108">For more information on how tooget started, see [Get started with Hadoop on HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1ae32-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="1ae32-109">Prerequisites</span></span>
* <span data-ttu-id="1ae32-110">[Oracle VirtualBox](https://www.virtualbox.org/).</span><span class="sxs-lookup"><span data-stu-id="1ae32-110">[Oracle VirtualBox](https://www.virtualbox.org/).</span></span> <span data-ttu-id="1ae32-111">Buradan yükleyip [burada](https://www.virtualbox.org/wiki/Downloads).</span><span class="sxs-lookup"><span data-stu-id="1ae32-111">Download and install it from [here](https://www.virtualbox.org/wiki/Downloads).</span></span>



## <a name="download-and-install-hello-virtual-machine"></a><span data-ttu-id="1ae32-112">Merhaba sanal makineye yükleyip</span><span class="sxs-lookup"><span data-stu-id="1ae32-112">Download and install hello virtual machine</span></span>
1. <span data-ttu-id="1ae32-113">Toohello Gözat [Hortonworks indirmeleri](http://hortonworks.com/downloads/#sandbox).</span><span class="sxs-lookup"><span data-stu-id="1ae32-113">Browse toohello [Hortonworks downloads](http://hortonworks.com/downloads/#sandbox).</span></span>

2. <span data-ttu-id="1ae32-114">Tıklatın **İNDİRMEK için VIRTUALBOX** toodownload hello son Hortonworks korumalı alan bir VM üzerinde.</span><span class="sxs-lookup"><span data-stu-id="1ae32-114">Click **DOWNLOAD FOR VIRTUALBOX** toodownload hello latest Hortonworks Sandbox on a VM.</span></span> <span data-ttu-id="1ae32-115">Merhaba yükleme başlamadan önce istendiğinde tooregister Hortonworks ile demektir.</span><span class="sxs-lookup"><span data-stu-id="1ae32-115">You are prompted tooregister with Hortonworks before hello download begins.</span></span> <span data-ttu-id="1ae32-116">Ağ hızınıza bağlı olarak bir tootwo saatleri toodownload alır.</span><span class="sxs-lookup"><span data-stu-id="1ae32-116">It takes one tootwo hours toodownload depending on your network speed.</span></span>
   
    ![İçin bağlantı görüntüsünü karşıdan yüklemek için VirtualBox Hortonworks korumalı alan](./media/hdinsight-hadoop-emulator-get-started/download-sandbox.png)
3. <span data-ttu-id="1ae32-118">Gelen Merhaba aynı web sayfasında, hello tıklatın **sanal kutusundaki içeri aktarma** hello sanal makine için yükleme yönergeleri içeren bir PDF toodownload bağlantı.</span><span class="sxs-lookup"><span data-stu-id="1ae32-118">From hello same web page, click hello **Import on Virtual Box** link toodownload a PDF containing installation instructions for hello virtual machine.</span></span>

<span data-ttu-id="1ae32-119">toodownload daha eski bir HDP sürüm sandbox hello arşiv genişletin:</span><span class="sxs-lookup"><span data-stu-id="1ae32-119">toodownload an older HDP version sandbox, expand hello archive:</span></span>

![Hortonworks Sandbox arşiv](./media/hdinsight-hadoop-emulator-get-started/hortonworks-sandbox-archive.png)


## <a name="start-hello-virtual-machine"></a><span data-ttu-id="1ae32-121">Merhaba sanal makineyi Başlat</span><span class="sxs-lookup"><span data-stu-id="1ae32-121">Start hello virtual machine</span></span>

1. <span data-ttu-id="1ae32-122">Oracle VM VirtualBox açın.</span><span class="sxs-lookup"><span data-stu-id="1ae32-122">Open Oracle VM VirtualBox.</span></span>
2. <span data-ttu-id="1ae32-123">Hello gelen **dosya** menüsünde tıklatın **alma Gereci**ve ardından hello Hortonworks Sandbox görüntüsü belirtin.</span><span class="sxs-lookup"><span data-stu-id="1ae32-123">From hello **File** menu, click **Import Appliance**, and then specify hello Hortonworks Sandbox image.</span></span>
1. <span data-ttu-id="1ae32-124">Select hello Hortonworks Sandbox tıklatın **Başlat**ve ardından **Normal başlangıç**.</span><span class="sxs-lookup"><span data-stu-id="1ae32-124">Select hello Hortonworks Sandbox, click **Start**, and then **Normal Start**.</span></span> <span data-ttu-id="1ae32-125">Merhaba sanal makine hello önyükleme işlemi tamamlandıktan sonra oturum açma yönergeleri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="1ae32-125">Once hello virtual machine has finished hello boot process, it displays login instructions.</span></span>
   
    ![Normal Başlat](./media/hdinsight-hadoop-emulator-get-started/normal-start.png)
2. <span data-ttu-id="1ae32-127">Bir web tarayıcısı açın ve görüntülenen toohello URL (genellikle http://127.0.0.1:8888) gidin.</span><span class="sxs-lookup"><span data-stu-id="1ae32-127">Open a web browser and navigate toohello URL displayed (usually http://127.0.0.1:8888).</span></span>

## <a name="set-sandbox-passwords"></a><span data-ttu-id="1ae32-128">Korumalı alan parola ayarlama</span><span class="sxs-lookup"><span data-stu-id="1ae32-128">Set Sandbox passwords</span></span>

1. <span data-ttu-id="1ae32-129">Merhaba gelen **başlama** hello Hortonworks Sandbox sayfasında, adım **görünüm Gelişmiş Seçenekler**.</span><span class="sxs-lookup"><span data-stu-id="1ae32-129">From hello **get started** step of hello Hortonworks Sandbox page, select **View Advanced Options**.</span></span> <span data-ttu-id="1ae32-130">Bu sayfa toolog SSH kullanarak toohello korumalı alanı içinde üzerinde Hello bilgileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="1ae32-130">Use hello information on this page toolog in toohello sandbox using SSH.</span></span> <span data-ttu-id="1ae32-131">Sağlanan Hello adını ve parolayı kullanın.</span><span class="sxs-lookup"><span data-stu-id="1ae32-131">Use hello name and password provided.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="1ae32-132">Bir SSH istemcisi yüklü değil, web tabanlı SSH sağlayan en hello sanal makinenin hello kullanabilirsiniz **http://localhost:4200 /**.</span><span class="sxs-lookup"><span data-stu-id="1ae32-132">If you do not have an SSH client installed, you can use hello web-based SSH provided at by hello virtual machine at **http://localhost:4200/**.</span></span>
   > 
   
    <span data-ttu-id="1ae32-133">Merhaba SSH, bağlanırken ilk kez istendiğinde toochange hello hello kök hesabının parolasını olduğunuz.</span><span class="sxs-lookup"><span data-stu-id="1ae32-133">hello first time you connect using SSH, you are prompted toochange hello password for hello root account.</span></span> <span data-ttu-id="1ae32-134">SSH kullanarak oturum açışınızda kullanacağınız yeni bir parola girin.</span><span class="sxs-lookup"><span data-stu-id="1ae32-134">Enter a new password, which you use when you log in using SSH.</span></span>

2. <span data-ttu-id="1ae32-135">Oturum açtıktan sonra komutu aşağıdaki hello girin:</span><span class="sxs-lookup"><span data-stu-id="1ae32-135">Once logged in, enter hello following command:</span></span>
   
        ambari-admin-password-reset
   
    <span data-ttu-id="1ae32-136">İstendiğinde, hello Ambari yönetici hesabı için bir parola sağlayın.</span><span class="sxs-lookup"><span data-stu-id="1ae32-136">When prompted, provide a password for hello Ambari admin account.</span></span> <span data-ttu-id="1ae32-137">Merhaba Ambari Web kullanıcı arabirimini eriştiğinizde bu kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1ae32-137">This is used when you access hello Ambari Web UI.</span></span>

## <a name="use-hive-commands"></a><span data-ttu-id="1ae32-138">Hive komutları kullanın</span><span class="sxs-lookup"><span data-stu-id="1ae32-138">Use Hive commands</span></span>

1. <span data-ttu-id="1ae32-139">Bir SSH bağlantısı toohello sandbox komut toostart hello Hive kabuğunu aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="1ae32-139">From an SSH connection toohello sandbox, use hello following command toostart hello Hive shell:</span></span>
   
        hive
2. <span data-ttu-id="1ae32-140">Merhaba Kabuk başladıktan sonra hello sandbox ile sağlanan tooview hello tabloları aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="1ae32-140">Once hello shell has started, use hello following tooview hello tables that are provided with hello sandbox:</span></span>
   
        show tables;
3. <span data-ttu-id="1ae32-141">Hello tooretrieve 10 satır aşağıdaki kullanım hello `sample_07` tablosu:</span><span class="sxs-lookup"><span data-stu-id="1ae32-141">Use hello following tooretrieve 10 rows from hello `sample_07` table:</span></span>
   
        select * from sample_07 limit 10;

## <a name="next-steps"></a><span data-ttu-id="1ae32-142">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1ae32-142">Next steps</span></span>
* [<span data-ttu-id="1ae32-143">Bilgi nasıl toouse Visual Studio ile Merhaba Hortonworks korumalı alan</span><span class="sxs-lookup"><span data-stu-id="1ae32-143">Learn how toouse Visual Studio with hello Hortonworks Sandbox</span></span>](hdinsight-hadoop-emulator-visual-studio.md)
* [<span data-ttu-id="1ae32-144">Merhaba ipleri hello Hortonworks korumalı alan, öğrenme</span><span class="sxs-lookup"><span data-stu-id="1ae32-144">Learning hello ropes of hello Hortonworks Sandbox</span></span>](http://hortonworks.com/hadoop-tutorial/learning-the-ropes-of-the-hortonworks-sandbox/)
* [<span data-ttu-id="1ae32-145">Hadoop Öğreticisi - HDP ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="1ae32-145">Hadoop tutorial - Getting started with HDP</span></span>](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/)

