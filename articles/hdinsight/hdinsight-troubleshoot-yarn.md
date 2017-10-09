---
title: "Azure Hdınsight kullanarak YARN aaaTroubleshoot | Microsoft Docs"
description: "Apache Hadoop YARN ve Azure Hdınsight ile çalışma hakkında toocommon soruların yanıtlarını alın."
keywords: "Azure Hdınsight, YARN, SSS, sorun giderme kılavuzu, sık sorulan sorular"
services: Azure HDInsight
documentationcenter: na
author: arijitt
manager: 
editor: 
ms.assetid: F76786A9-99AB-4B85-9B15-CA03528FC4CD
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: arijitt
ms.openlocfilehash: 800d9738cb27e05a64db470ee58565af3b85aa99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-yarn-by-using-azure-hdinsight"></a><span data-ttu-id="3f42f-104">YARN Azure Hdınsight kullanarak sorun giderme</span><span class="sxs-lookup"><span data-stu-id="3f42f-104">Troubleshoot YARN by using Azure HDInsight</span></span>

<span data-ttu-id="3f42f-105">Apache Ambari, Apache Hadoop YARN yükü ile çalışırken Hello üst sorunları ve bunların çözümleri hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="3f42f-105">Learn about hello top issues and their resolutions when working with Apache Hadoop YARN payloads in Apache Ambari.</span></span>

## <a name="how-do-i-create-a-new-yarn-queue-on-a-cluster"></a><span data-ttu-id="3f42f-106">Bir kümede nasıl yeni bir YARN sıra oluşturulsun mu</span><span class="sxs-lookup"><span data-stu-id="3f42f-106">How do I create a new YARN queue on a cluster</span></span>


### <a name="resolution-steps"></a><span data-ttu-id="3f42f-107">Çözüm adımları</span><span class="sxs-lookup"><span data-stu-id="3f42f-107">Resolution steps</span></span> 

<span data-ttu-id="3f42f-108">Kullanım hello aşağıdaki Ambari toocreate yeni bir YARN sırası adımları ve hello kapasite ayırma tüm hello sıraları arasında dengeleyin.</span><span class="sxs-lookup"><span data-stu-id="3f42f-108">Use hello following steps in Ambari toocreate a new YARN queue, and then balance hello capacity allocation among all hello queues.</span></span> 

<span data-ttu-id="3f42f-109">Bu örnekte, iki mevcut sıraları (**varsayılan** ve **thriftsvr**) hem de hello yeni sıra (spark) % 50 kapasitesini sunan % 50 kapasite too25% kapasiteden, değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="3f42f-109">In this example, two existing queues (**default** and **thriftsvr**) both are changed from 50% capacity too25% capacity, which gives hello new queue (spark) 50% capacity.</span></span>
| <span data-ttu-id="3f42f-110">Kuyruk</span><span class="sxs-lookup"><span data-stu-id="3f42f-110">Queue</span></span> | <span data-ttu-id="3f42f-111">Kapasite</span><span class="sxs-lookup"><span data-stu-id="3f42f-111">Capacity</span></span> | <span data-ttu-id="3f42f-112">Maksimum kapasite</span><span class="sxs-lookup"><span data-stu-id="3f42f-112">Maximum capacity</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3f42f-113">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="3f42f-113">default</span></span> | <span data-ttu-id="3f42f-114">%25</span><span class="sxs-lookup"><span data-stu-id="3f42f-114">25%</span></span> | <span data-ttu-id="3f42f-115">50%</span><span class="sxs-lookup"><span data-stu-id="3f42f-115">50%</span></span> |
| <span data-ttu-id="3f42f-116">thrftsvr</span><span class="sxs-lookup"><span data-stu-id="3f42f-116">thrftsvr</span></span> | <span data-ttu-id="3f42f-117">%25</span><span class="sxs-lookup"><span data-stu-id="3f42f-117">25%</span></span> | <span data-ttu-id="3f42f-118">50%</span><span class="sxs-lookup"><span data-stu-id="3f42f-118">50%</span></span> |
| <span data-ttu-id="3f42f-119">Spark</span><span class="sxs-lookup"><span data-stu-id="3f42f-119">spark</span></span> | <span data-ttu-id="3f42f-120">50%</span><span class="sxs-lookup"><span data-stu-id="3f42f-120">50%</span></span> | <span data-ttu-id="3f42f-121">50%</span><span class="sxs-lookup"><span data-stu-id="3f42f-121">50%</span></span> |

1. <span data-ttu-id="3f42f-122">Select hello **Ambari görünümleri** simgesine ve ardından hello Kılavuz düzeni.</span><span class="sxs-lookup"><span data-stu-id="3f42f-122">Select hello **Ambari Views** icon, and then select hello grid pattern.</span></span> <span data-ttu-id="3f42f-123">Ardından, **YARN sıra yöneticisi**.</span><span class="sxs-lookup"><span data-stu-id="3f42f-123">Next, select **YARN Queue Manager**.</span></span>

    ![Merhaba Ambari görünümleri simgesini seçin](media/hdinsight-troubleshoot-yarn/create-queue-1.png)
2. <span data-ttu-id="3f42f-125">Select hello **varsayılan** sırası.</span><span class="sxs-lookup"><span data-stu-id="3f42f-125">Select hello **default** queue.</span></span>

    ![Merhaba varsayılan sıra seçin](media/hdinsight-troubleshoot-yarn/create-queue-2.png)
3. <span data-ttu-id="3f42f-127">Hello için **varsayılan** kuyruk, hello değiştirme **kapasite** % 50 too25%.</span><span class="sxs-lookup"><span data-stu-id="3f42f-127">For hello **default** queue, change hello **capacity** from 50% too25%.</span></span> <span data-ttu-id="3f42f-128">Hello için **thriftsvr** kuyruk, hello değiştirme **kapasite** too25%.</span><span class="sxs-lookup"><span data-stu-id="3f42f-128">For hello **thriftsvr** queue, change hello **capacity** too25%.</span></span>

    ![Merhaba kapasite too25% hello sıralar için varsayılan ve thriftsvr değiştirin](media/hdinsight-troubleshoot-yarn/create-queue-3.png)
4. <span data-ttu-id="3f42f-130">toocreate yeni bir sıra seçin **ekleme sırası**.</span><span class="sxs-lookup"><span data-stu-id="3f42f-130">toocreate a new queue, select **Add Queue**.</span></span>

    ![Select kuyruk Ekle](media/hdinsight-troubleshoot-yarn/create-queue-4.png)

5. <span data-ttu-id="3f42f-132">Merhaba yeni kuyruk adı.</span><span class="sxs-lookup"><span data-stu-id="3f42f-132">Name hello new queue.</span></span>

    ![Merhaba sıra Spark adı](media/hdinsight-troubleshoot-yarn/create-queue-5.png)  

6. <span data-ttu-id="3f42f-134">Merhaba bırakın **kapasite** % 50 ve ardından hello değerlerinde **Eylemler** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="3f42f-134">Leave hello **capacity** values at 50%, and then select hello **Actions** button.</span></span>

    ![Merhaba Eylemler düğmesini seçin](media/hdinsight-troubleshoot-yarn/create-queue-6.png)  
7. <span data-ttu-id="3f42f-136">Seçin **kaydedin ve yenileyin sıraları**.</span><span class="sxs-lookup"><span data-stu-id="3f42f-136">Select **Save and Refresh Queues**.</span></span>

    ![Kaydet'i seçin ve Kuyruklar Yenile](media/hdinsight-troubleshoot-yarn/create-queue-7.png)  

<span data-ttu-id="3f42f-138">Bu değişiklikler hemen hello YARN Zamanlayıcı UI'üzerinde görünür.</span><span class="sxs-lookup"><span data-stu-id="3f42f-138">These changes are visible immediately on hello YARN Scheduler UI.</span></span>

### <a name="additional-reading"></a><span data-ttu-id="3f42f-139">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="3f42f-139">Additional reading</span></span>

- [<span data-ttu-id="3f42f-140">YARN CapacityScheduler</span><span class="sxs-lookup"><span data-stu-id="3f42f-140">YARN CapacityScheduler</span></span>](https://hadoop.apache.org/docs/r2.7.2/hadoop-yarn/hadoop-yarn-site/CapacityScheduler.html)


## <a name="how-do-i-download-yarn-logs-from-a-cluster"></a><span data-ttu-id="3f42f-141">Bir kümeden nasıl YARN günlüklerini karşıdan</span><span class="sxs-lookup"><span data-stu-id="3f42f-141">How do I download YARN logs from a cluster</span></span>


### <a name="resolution-steps"></a><span data-ttu-id="3f42f-142">Çözüm adımları</span><span class="sxs-lookup"><span data-stu-id="3f42f-142">Resolution steps</span></span> 

1. <span data-ttu-id="3f42f-143">Bir güvenli Kabuk (SSH) istemcisi kullanarak toohello Hdınsight kümesine bağlanın.</span><span class="sxs-lookup"><span data-stu-id="3f42f-143">Connect toohello HDInsight cluster by using a Secure Shell (SSH) client.</span></span> <span data-ttu-id="3f42f-144">Daha fazla bilgi için bkz: [ek okuma](#additional-reading-2).</span><span class="sxs-lookup"><span data-stu-id="3f42f-144">For more information, see [Additional reading](#additional-reading-2).</span></span>

2. <span data-ttu-id="3f42f-145">tüm uygulama kimlikleri çalışmakta olan, hello YARN uygulamaların hello toolist hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="3f42f-145">toolist all hello application IDs of hello YARN applications that are currently running, run hello following command:</span></span>

    ```apache
    yarn top
    ```
    <span data-ttu-id="3f42f-146">Merhaba kimlikleri hello listelenen **APPLİCATİONID** sütun.</span><span class="sxs-lookup"><span data-stu-id="3f42f-146">hello IDs are listed in hello **APPLICATIONID** column.</span></span> <span data-ttu-id="3f42f-147">Hello günlükleri indirmek **APPLİCATİONID** sütun.</span><span class="sxs-lookup"><span data-stu-id="3f42f-147">You can download logs from hello **APPLICATIONID** column.</span></span>

    ```apache
    YARN top - 18:00:07, up 19d, 0:14, 0 active users, queue(s): root
    NodeManager(s): 4 total, 4 active, 0 unhealthy, 0 decommissioned, 0 lost, 0 rebooted
    Queue(s) Applications: 2 running, 10 submitted, 0 pending, 8 completed, 0 killed, 0 failed
    Queue(s) Mem(GB): 97 available, 3 allocated, 0 pending, 0 reserved
    Queue(s) VCores: 58 available, 2 allocated, 0 pending, 0 reserved
    Queue(s) Containers: 2 allocated, 0 pending, 0 reserved

                      APPLICATIONID USER             TYPE      QUEUE   #CONT  #RCONT  VCORES RVCORES     MEM    RMEM  VCORESECS    MEMSECS %PROGR       TIME NAME
     application_1490377567345_0007 hive            spark  thriftsvr       1       0       1       0      1G      0G    1628407    2442611  10.00   18:20:20 Thrift JDBC/ODBC Server
     application_1490377567345_0006 hive            spark  thriftsvr       1       0       1       0      1G      0G    1628430    2442645  10.00   18:20:20 Thrift JDBC/ODBC Server
    ```

3. <span data-ttu-id="3f42f-148">tüm uygulama yöneticileri için toodownload YARN kapsayıcı günlüklerini hello aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="3f42f-148">toodownload YARN container logs for all application masters, use hello following command:</span></span>
   
    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am ALL > amlogs.txt
    ```

    <span data-ttu-id="3f42f-149">Bu komut amlogs.txt adlı bir günlük dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3f42f-149">This command creates a log file named amlogs.txt.</span></span> 

4. <span data-ttu-id="3f42f-150">toodownload YARN kapsayıcı günlüklerini yalnızca hello en son uygulama Yöneticisi için komutu aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="3f42f-150">toodownload YARN container logs for only hello latest application master, use hello following command:</span></span>

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am -1 > latestamlogs.txt
    ```

    <span data-ttu-id="3f42f-151">Bu komut latestamlogs.txt adlı bir günlük dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3f42f-151">This command creates a log file named latestamlogs.txt.</span></span> 

4. <span data-ttu-id="3f42f-152">toodownload YARN kapsayıcı günlüklerini hello ilk iki uygulama yöneticileri için komutu aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="3f42f-152">toodownload YARN container logs for hello first two application masters, use hello following command:</span></span>

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am 1,2 > first2amlogs.txt 
    ```

    <span data-ttu-id="3f42f-153">Bu komut first2amlogs.txt adlı bir günlük dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3f42f-153">This command creates a log file named first2amlogs.txt.</span></span> 

5. <span data-ttu-id="3f42f-154">Tüm YARN kapsayıcı günlükleri, toodownload kullanmak hello komutu:</span><span class="sxs-lookup"><span data-stu-id="3f42f-154">toodownload all YARN container logs, use hello following command:</span></span>

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> > logs.txt
    ```

    <span data-ttu-id="3f42f-155">Bu komut logs.txt adlı bir günlük dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3f42f-155">This command creates a log file named logs.txt.</span></span> 

6. <span data-ttu-id="3f42f-156">belirli bir kapsayıcıya, komutu aşağıdaki kullanım hello için toodownload hello YARN kapsayıcı günlüğü:</span><span class="sxs-lookup"><span data-stu-id="3f42f-156">toodownload hello YARN container log for a specific container, use hello following command:</span></span>

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -containerId <container_id> > containerlogs.txt 
    ```

    <span data-ttu-id="3f42f-157">Bu komut containerlogs.txt adlı bir günlük dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3f42f-157">This command creates a log file named containerlogs.txt.</span></span>

### <span data-ttu-id="3f42f-158"><a name="additional-reading-2"></a>Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="3f42f-158"><a name="additional-reading-2"></a>Additional reading</span></span>

- [<span data-ttu-id="3f42f-159">SSH kullanarak tooHDInsight (Hadoop) bağlanma</span><span class="sxs-lookup"><span data-stu-id="3f42f-159">Connect tooHDInsight (Hadoop) by using SSH</span></span>](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix)
- [<span data-ttu-id="3f42f-160">Apache Hadoop YARN kavramları ve uygulamalar</span><span class="sxs-lookup"><span data-stu-id="3f42f-160">Apache Hadoop YARN concepts and applications</span></span>](https://hortonworks.com/blog/apache-hadoop-yarn-concepts-and-applications/)







