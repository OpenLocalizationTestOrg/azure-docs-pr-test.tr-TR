---
title: "hdınsight'ta - Azure aaaUnderstand ve çözümleme WebHCat hatalarını | Microsoft Docs"
description: "Hdınsight üzerinde WebHCat tarafından döndürülen tooabout ortak hataları nasıl ve ne öğrenin tooresolve bunları."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 1b3d94b1-207d-4550-aece-21dc45485549
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 0071a1e9ed448ae146b93c8f4f518e31b95d27c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-resolve-errors-received-from-webhcat-on-hdinsight"></a><span data-ttu-id="50798-103">Anlama ve hdınsight'ta WebHCat gelen karşılaşılan hataları çözme</span><span class="sxs-lookup"><span data-stu-id="50798-103">Understand and resolve errors received from WebHCat on HDInsight</span></span>

<span data-ttu-id="50798-104">Tooresolve WebHCat Hdınsight ile kullanırken ve nasıl alınan hataları hakkında bilgi edinin bunları.</span><span class="sxs-lookup"><span data-stu-id="50798-104">Learn about errors received when using WebHCat with HDInsight, and how tooresolve them.</span></span> <span data-ttu-id="50798-105">WebHCat dahili olarak Azure PowerShell ve hello Data Lake araçları gibi istemci tarafı araçları Visual Studio için kullanılıyor.</span><span class="sxs-lookup"><span data-stu-id="50798-105">WebHCat is used internally by client-side tools such as Azure PowerShell and hello Data Lake Tools for Visual Studio.</span></span>

## <a name="what-is-webhcat"></a><span data-ttu-id="50798-106">WebHCat nedir</span><span class="sxs-lookup"><span data-stu-id="50798-106">What is WebHCat</span></span>

<span data-ttu-id="50798-107">[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) bir REST API için [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), tablo ve Hadoop için Depolama Yönetimi katmanı.</span><span class="sxs-lookup"><span data-stu-id="50798-107">[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) is a REST API for [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), a table, and storage management layer for Hadoop.</span></span> <span data-ttu-id="50798-108">WebHCat Hdınsight kümelerinde varsayılan olarak etkindir ve çeşitli araçlar toosubmit işleri tarafından kullanılır, iş durumu, vb. toohello kümede günlüğe kaydetmeden Al.</span><span class="sxs-lookup"><span data-stu-id="50798-108">WebHCat is enabled by default on HDInsight clusters, and is used by various tools toosubmit jobs, get job status, etc. without logging in toohello cluster.</span></span>

## <a name="modifying-configuration"></a><span data-ttu-id="50798-109">Yapılandırmasını değiştirme</span><span class="sxs-lookup"><span data-stu-id="50798-109">Modifying configuration</span></span>

> [!IMPORTANT]
> <span data-ttu-id="50798-110">Yapılandırılan en aştığından birkaç bu belgede listelenen hello hataları oluşur.</span><span class="sxs-lookup"><span data-stu-id="50798-110">Several of hello errors listed in this document occur because a configured maximum has been exceeded.</span></span> <span data-ttu-id="50798-111">Bir değer değiştirebileceğiniz Hello çözümleme adım değinmektedir kullanırken, tooperform hello değişikliğinden sonra hello birini kullanmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="50798-111">When hello resolution step mentions that you can change a value, you must use one of hello following tooperform hello change:</span></span>

* <span data-ttu-id="50798-112">İçin **Windows** kümeleri: küme oluşturma sırasında bir betik eylemi tooconfigure hello değeri kullanın.</span><span class="sxs-lookup"><span data-stu-id="50798-112">For **Windows** clusters: Use a script action tooconfigure hello value during cluster creation.</span></span> <span data-ttu-id="50798-113">Daha fazla bilgi için bkz: [betik eylemleri geliştirmeniz](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="50798-113">For more information, see [Develop script actions](hdinsight-hadoop-script-actions.md).</span></span>

* <span data-ttu-id="50798-114">İçin **Linux** kümeleri: kullanım Ambari (web veya REST API) toomodify hello değeri.</span><span class="sxs-lookup"><span data-stu-id="50798-114">For **Linux** clusters: Use Ambari (web or REST API) toomodify hello value.</span></span> <span data-ttu-id="50798-115">Daha fazla bilgi için bkz: [Ambari kullanarak Hdınsight yönetme](hdinsight-hadoop-manage-ambari.md)</span><span class="sxs-lookup"><span data-stu-id="50798-115">For more information, see [Manage HDInsight using Ambari](hdinsight-hadoop-manage-ambari.md)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="50798-116">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="50798-116">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="50798-117">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="50798-117">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

### <a name="default-configuration"></a><span data-ttu-id="50798-118">Varsayılan yapılandırma</span><span class="sxs-lookup"><span data-stu-id="50798-118">Default configuration</span></span>

<span data-ttu-id="50798-119">Varsayılan değerleri aşağıdaki hello aşılırsa, WebHCat performansı düşebilir veya hatalara neden olabilir:</span><span class="sxs-lookup"><span data-stu-id="50798-119">If hello following default values are exceeded, it can degrade WebHCat performance or cause errors:</span></span>

| <span data-ttu-id="50798-120">Ayar</span><span class="sxs-lookup"><span data-stu-id="50798-120">Setting</span></span> | <span data-ttu-id="50798-121">Neler yapar?</span><span class="sxs-lookup"><span data-stu-id="50798-121">What it does</span></span> | <span data-ttu-id="50798-122">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="50798-122">Default value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="50798-123">[yarn.Scheduler.Capacity.Maximum-uygulamalar][maximum-applications]</span><span class="sxs-lookup"><span data-stu-id="50798-123">[yarn.scheduler.capacity.maximum-applications][maximum-applications]</span></span> |<span data-ttu-id="50798-124">Merhaba eşzamanlı olarak etkinleştirilebilir iş sayısı üst sınırını (Beklemede veya çalışan)</span><span class="sxs-lookup"><span data-stu-id="50798-124">hello maximum number of jobs that can be active concurrently (pending or running)</span></span> |<span data-ttu-id="50798-125">10,000</span><span class="sxs-lookup"><span data-stu-id="50798-125">10,000</span></span> |
| <span data-ttu-id="50798-126">[templeton.Exec.max yakalar][max-procs]</span><span class="sxs-lookup"><span data-stu-id="50798-126">[templeton.exec.max-procs][max-procs]</span></span> |<span data-ttu-id="50798-127">Merhaba en fazla eşzamanlı olarak sunulan istek sayısı</span><span class="sxs-lookup"><span data-stu-id="50798-127">hello maximum number of requests that can be served concurrently</span></span> |<span data-ttu-id="50798-128">20</span><span class="sxs-lookup"><span data-stu-id="50798-128">20</span></span> |
| <span data-ttu-id="50798-129">[mapreduce.jobhistory.max yaş ms][max-age-ms]</span><span class="sxs-lookup"><span data-stu-id="50798-129">[mapreduce.jobhistory.max-age-ms][max-age-ms]</span></span> |<span data-ttu-id="50798-130">Geçmiş işi gün sayısı Hello korunur</span><span class="sxs-lookup"><span data-stu-id="50798-130">hello number of days that job history are retained</span></span> |<span data-ttu-id="50798-131">7 gün</span><span class="sxs-lookup"><span data-stu-id="50798-131">7 days</span></span> |

## <a name="too-many-requests"></a><span data-ttu-id="50798-132">Çok fazla istek</span><span class="sxs-lookup"><span data-stu-id="50798-132">Too many requests</span></span>

<span data-ttu-id="50798-133">**HTTP durum kodu**: 429</span><span class="sxs-lookup"><span data-stu-id="50798-133">**HTTP Status code**: 429</span></span>

| <span data-ttu-id="50798-134">Nedeni</span><span class="sxs-lookup"><span data-stu-id="50798-134">Cause</span></span> | <span data-ttu-id="50798-135">Çözüm</span><span class="sxs-lookup"><span data-stu-id="50798-135">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="50798-136">(Varsayılan 20) dakika başına WebHCat tarafından sunulan hello maksimum eşzamanlı istek sınırı aşıldı</span><span class="sxs-lookup"><span data-stu-id="50798-136">You have exceeded hello maximum concurrent requests served by WebHCat per minute (default 20)</span></span> |<span data-ttu-id="50798-137">Değil gönderme birden fazla hello en fazla eş zamanlı istek sayısını veya değiştirerek hello eşzamanlı istek sınırı artırmak olduğunu, iş yükü tooensure azaltmak `templeton.exec.max-procs`.</span><span class="sxs-lookup"><span data-stu-id="50798-137">Reduce your workload tooensure that you do not submit more than hello maximum number of concurrent requests or increase hello concurrent request limit by modifying `templeton.exec.max-procs`.</span></span> <span data-ttu-id="50798-138">Daha fazla bilgi için bkz: [değiştirme yapılandırma](#modifying-configuration)</span><span class="sxs-lookup"><span data-stu-id="50798-138">For more information, see [Modifying configuration](#modifying-configuration)</span></span> |

## <a name="server-unavailable"></a><span data-ttu-id="50798-139">Sunucu kullanılamıyor</span><span class="sxs-lookup"><span data-stu-id="50798-139">Server unavailable</span></span>

<span data-ttu-id="50798-140">**HTTP durum kodu**: 503</span><span class="sxs-lookup"><span data-stu-id="50798-140">**HTTP Status code**: 503</span></span>

| <span data-ttu-id="50798-141">Nedeni</span><span class="sxs-lookup"><span data-stu-id="50798-141">Cause</span></span> | <span data-ttu-id="50798-142">Çözüm</span><span class="sxs-lookup"><span data-stu-id="50798-142">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="50798-143">Bu durum kodu genellikle hello birincil ve ikincil arasında yük devretme sırasında oluşup HeadNode hello kümesi için</span><span class="sxs-lookup"><span data-stu-id="50798-143">This status code usually occurs during failover between hello primary and secondary HeadNode for hello cluster</span></span> |<span data-ttu-id="50798-144">İki dakika bekleyin, sonra hello işlemi yeniden deneyin</span><span class="sxs-lookup"><span data-stu-id="50798-144">Wait two minutes, then retry hello operation</span></span> |

## <a name="bad-request-content-could-not-find-job"></a><span data-ttu-id="50798-145">Hatalı istek içeriği: işi bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="50798-145">Bad request Content: Could not find job</span></span>

<span data-ttu-id="50798-146">**HTTP durum kodu**: 400</span><span class="sxs-lookup"><span data-stu-id="50798-146">**HTTP Status code**: 400</span></span>

| <span data-ttu-id="50798-147">Nedeni</span><span class="sxs-lookup"><span data-stu-id="50798-147">Cause</span></span> | <span data-ttu-id="50798-148">Çözüm</span><span class="sxs-lookup"><span data-stu-id="50798-148">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="50798-149">İş ayrıntılarını hello iş geçmişi tarafından temizleyici temizlendi</span><span class="sxs-lookup"><span data-stu-id="50798-149">Job details have been cleaned up by hello job history cleaner</span></span> |<span data-ttu-id="50798-150">iş geçmişi için Hello varsayılan saklama dönemi 7 gündür.</span><span class="sxs-lookup"><span data-stu-id="50798-150">hello default retention period for job history is 7 days.</span></span> <span data-ttu-id="50798-151">Merhaba varsayılan saklama dönemi değiştirerek değiştirilebilir `mapreduce.jobhistory.max-age-ms`.</span><span class="sxs-lookup"><span data-stu-id="50798-151">hello default retention period can be changed by modifying `mapreduce.jobhistory.max-age-ms`.</span></span> <span data-ttu-id="50798-152">Daha fazla bilgi için bkz: [değiştirme yapılandırma](#modifying-configuration)</span><span class="sxs-lookup"><span data-stu-id="50798-152">For more information, see [Modifying configuration](#modifying-configuration)</span></span> |
| <span data-ttu-id="50798-153">İş tooa yük devretme sonlandırıldı</span><span class="sxs-lookup"><span data-stu-id="50798-153">Job has been killed due tooa failover</span></span> |<span data-ttu-id="50798-154">Tootwo dakika yedeklemek için iş gönderme yeniden deneyin</span><span class="sxs-lookup"><span data-stu-id="50798-154">Retry job submission for up tootwo minutes</span></span> |
| <span data-ttu-id="50798-155">Geçersiz iş kimliği kullanıldı</span><span class="sxs-lookup"><span data-stu-id="50798-155">An Invalid job id was used</span></span> |<span data-ttu-id="50798-156">Merhaba iş kimliği doğru olup olmadığını denetleyin</span><span class="sxs-lookup"><span data-stu-id="50798-156">Check if hello job id is correct</span></span> |

## <a name="bad-gateway"></a><span data-ttu-id="50798-157">Hatalı ağ geçidi</span><span class="sxs-lookup"><span data-stu-id="50798-157">Bad gateway</span></span>

<span data-ttu-id="50798-158">**HTTP durum kodu**: 502</span><span class="sxs-lookup"><span data-stu-id="50798-158">**HTTP Status code**: 502</span></span>

| <span data-ttu-id="50798-159">Nedeni</span><span class="sxs-lookup"><span data-stu-id="50798-159">Cause</span></span> | <span data-ttu-id="50798-160">Çözüm</span><span class="sxs-lookup"><span data-stu-id="50798-160">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="50798-161">İç çöp toplama hello WebHCat işlem içinde gerçekleşen</span><span class="sxs-lookup"><span data-stu-id="50798-161">Internal garbage collection is occurring within hello WebHCat process</span></span> |<span data-ttu-id="50798-162">Çöp toplama toofinish için bekleyin veya hello WebHCat hizmetini yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="50798-162">Wait for garbage collection toofinish or restart hello WebHCat service</span></span> |
| <span data-ttu-id="50798-163">Merhaba ResourceManager hizmeti bilgisayarından yanıt beklenirken zaman aşımı.</span><span class="sxs-lookup"><span data-stu-id="50798-163">Time out waiting on a response from hello ResourceManager service.</span></span> <span data-ttu-id="50798-164">Etkin uygulama Hello sayısı hello yapılandırılmış en büyük (varsayılan 10.000) olduğunda bu hata oluşabilir</span><span class="sxs-lookup"><span data-stu-id="50798-164">This error can occur when hello number of active applications goes hello configured maximum (default 10,000)</span></span> |<span data-ttu-id="50798-165">İşlerini toocomplete çalışmakta bekleyin veya değiştirerek hello eşzamanlı iş sınırını artırın `yarn.scheduler.capacity.maximum-applications`.</span><span class="sxs-lookup"><span data-stu-id="50798-165">Wait for currently running jobs toocomplete or increase hello concurrent job limit by modifying `yarn.scheduler.capacity.maximum-applications`.</span></span> <span data-ttu-id="50798-166">Daha fazla bilgi için bkz: Merhaba [değiştirme yapılandırma](#modifying-configuration) bölümü.</span><span class="sxs-lookup"><span data-stu-id="50798-166">For more information, see hello [Modifying configuration](#modifying-configuration) section.</span></span> |
| <span data-ttu-id="50798-167">Merhaba aracılığıyla tüm işleri tooretrieve çalışırken [GET /jobs](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference+Jobs) çağrısı sırasında `Fields` çok ayarlama`*`</span><span class="sxs-lookup"><span data-stu-id="50798-167">Attempting tooretrieve all jobs through hello [GET /jobs](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference+Jobs) call while `Fields` is set too`*`</span></span> |<span data-ttu-id="50798-168">Alamadı *tüm* iş ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="50798-168">Do not retrieve *all* job details.</span></span> <span data-ttu-id="50798-169">Bunun yerine kullanın `jobid` tooretrieve ayrıntılarını işler yalnızca belirli iş kimliği büyük. Ya da kullanmayın`Fields`</span><span class="sxs-lookup"><span data-stu-id="50798-169">Instead use `jobid` tooretrieve details for jobs only greater than certain job id. Or, do not use `Fields`</span></span> |
| <span data-ttu-id="50798-170">HeadNode yük devretme sırasında Hello WebHCat hizmeti çalışmıyor</span><span class="sxs-lookup"><span data-stu-id="50798-170">hello WebHCat service is down during HeadNode failover</span></span> |<span data-ttu-id="50798-171">İki dakika bekleyin ve hello işlemi yeniden deneyin</span><span class="sxs-lookup"><span data-stu-id="50798-171">Wait for two minutes and retry hello operation</span></span> |
| <span data-ttu-id="50798-172">WebHCat gönderilen 500'den fazla bekleyen iş</span><span class="sxs-lookup"><span data-stu-id="50798-172">There are more than 500 pending jobs submitted through WebHCat</span></span> |<span data-ttu-id="50798-173">Daha fazla iş göndermeden önce şu anda bekleyen işler tamamlanana kadar bekleyin</span><span class="sxs-lookup"><span data-stu-id="50798-173">Wait until currently pending jobs have completed before submitting more jobs</span></span> |

[maximum-applications]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.3/bk_system-admin-guide/content/setting_application_limits.html
[max-procs]: https://hive.apache.org/javadocs/hcat-r0.5.0/configuration.html
[max-age-ms]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.6.0/ds_Hadoop/hadoop-mapreduce-client/hadoop-mapreduce-client-core/mapred-default.xml
