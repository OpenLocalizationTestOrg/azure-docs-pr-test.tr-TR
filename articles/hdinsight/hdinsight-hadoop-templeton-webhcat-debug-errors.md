---
title: "Anlama ve Hdınsight - Azure WebHCat hatalarını | Microsoft Docs"
description: "Nasıl üzere ortak tarafından WebHCat Hdınsight'ta döndürülen hataları ve bunların nasıl çözüleceği öğrenin."
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
ms.openlocfilehash: 6d8162e0d64ec9fc42690392b7c822593c0c2767
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="understand-and-resolve-errors-received-from-webhcat-on-hdinsight"></a><span data-ttu-id="566f4-103">Anlama ve hdınsight'ta WebHCat gelen karşılaşılan hataları çözme</span><span class="sxs-lookup"><span data-stu-id="566f4-103">Understand and resolve errors received from WebHCat on HDInsight</span></span>

<span data-ttu-id="566f4-104">WebHCat Hdınsight ve bunların nasıl çözüleceği ile kullanırken karşılaşılan hataları hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="566f4-104">Learn about errors received when using WebHCat with HDInsight, and how to resolve them.</span></span> <span data-ttu-id="566f4-105">WebHCat dahili olarak Visual Studio için Azure PowerShell gibi istemci tarafı araçları ve Data Lake araçları tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="566f4-105">WebHCat is used internally by client-side tools such as Azure PowerShell and the Data Lake Tools for Visual Studio.</span></span>

## <a name="what-is-webhcat"></a><span data-ttu-id="566f4-106">WebHCat nedir</span><span class="sxs-lookup"><span data-stu-id="566f4-106">What is WebHCat</span></span>

<span data-ttu-id="566f4-107">[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) bir REST API için [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), tablo ve Hadoop için Depolama Yönetimi katmanı.</span><span class="sxs-lookup"><span data-stu-id="566f4-107">[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) is a REST API for [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), a table, and storage management layer for Hadoop.</span></span> <span data-ttu-id="566f4-108">WebHCat Hdınsight kümelerinde varsayılan olarak etkindir ve çeşitli araçları tarafından kullanılan iş göndermek için küme oturum açma olmadan iş durumu, vb. alın.</span><span class="sxs-lookup"><span data-stu-id="566f4-108">WebHCat is enabled by default on HDInsight clusters, and is used by various tools to submit jobs, get job status, etc. without logging in to the cluster.</span></span>

## <a name="modifying-configuration"></a><span data-ttu-id="566f4-109">Yapılandırmasını değiştirme</span><span class="sxs-lookup"><span data-stu-id="566f4-109">Modifying configuration</span></span>

> [!IMPORTANT]
> <span data-ttu-id="566f4-110">Yapılandırılan en aştığından bu belgede listelenen hataların bazıları oluşur.</span><span class="sxs-lookup"><span data-stu-id="566f4-110">Several of the errors listed in this document occur because a configured maximum has been exceeded.</span></span> <span data-ttu-id="566f4-111">Bir değer değiştirebileceğiniz çözümleme adım değinmektedir, aşağıdakilerden birini değişiklik yapmak için kullanmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="566f4-111">When the resolution step mentions that you can change a value, you must use one of the following to perform the change:</span></span>

* <span data-ttu-id="566f4-112">İçin **Windows** kümeleri: küme oluşturma sırasında değerini yapılandırmak için bir betik eylemi kullanın.</span><span class="sxs-lookup"><span data-stu-id="566f4-112">For **Windows** clusters: Use a script action to configure the value during cluster creation.</span></span> <span data-ttu-id="566f4-113">Daha fazla bilgi için bkz: [betik eylemleri geliştirmeniz](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="566f4-113">For more information, see [Develop script actions](hdinsight-hadoop-script-actions.md).</span></span>

* <span data-ttu-id="566f4-114">İçin **Linux** kümeleri: kullanım Ambari (web veya REST API) değerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="566f4-114">For **Linux** clusters: Use Ambari (web or REST API) to modify the value.</span></span> <span data-ttu-id="566f4-115">Daha fazla bilgi için bkz: [Ambari kullanarak Hdınsight yönetme](hdinsight-hadoop-manage-ambari.md)</span><span class="sxs-lookup"><span data-stu-id="566f4-115">For more information, see [Manage HDInsight using Ambari](hdinsight-hadoop-manage-ambari.md)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="566f4-116">Linux, HDInsight sürüm 3.4 ve üzerinde kullanılan tek işletim sistemidir.</span><span class="sxs-lookup"><span data-stu-id="566f4-116">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="566f4-117">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="566f4-117">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

### <a name="default-configuration"></a><span data-ttu-id="566f4-118">Varsayılan yapılandırma</span><span class="sxs-lookup"><span data-stu-id="566f4-118">Default configuration</span></span>

<span data-ttu-id="566f4-119">Aşağıdaki varsayılan değerler aşılırsa, WebHCat performansı düşebilir veya hatalara neden olabilir:</span><span class="sxs-lookup"><span data-stu-id="566f4-119">If the following default values are exceeded, it can degrade WebHCat performance or cause errors:</span></span>

| <span data-ttu-id="566f4-120">Ayar</span><span class="sxs-lookup"><span data-stu-id="566f4-120">Setting</span></span> | <span data-ttu-id="566f4-121">Neler yapar?</span><span class="sxs-lookup"><span data-stu-id="566f4-121">What it does</span></span> | <span data-ttu-id="566f4-122">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="566f4-122">Default value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="566f4-123">[yarn.Scheduler.Capacity.Maximum-uygulamalar][maximum-applications]</span><span class="sxs-lookup"><span data-stu-id="566f4-123">[yarn.scheduler.capacity.maximum-applications][maximum-applications]</span></span> |<span data-ttu-id="566f4-124">Maksimum sayıda eş zamanlı olarak etkin olabilir işi (Beklemede veya çalışan)</span><span class="sxs-lookup"><span data-stu-id="566f4-124">The maximum number of jobs that can be active concurrently (pending or running)</span></span> |<span data-ttu-id="566f4-125">10,000</span><span class="sxs-lookup"><span data-stu-id="566f4-125">10,000</span></span> |
| <span data-ttu-id="566f4-126">[templeton.Exec.max yakalar][max-procs]</span><span class="sxs-lookup"><span data-stu-id="566f4-126">[templeton.exec.max-procs][max-procs]</span></span> |<span data-ttu-id="566f4-127">Eşzamanlı olarak hizmet isteklerinin sayısı</span><span class="sxs-lookup"><span data-stu-id="566f4-127">The maximum number of requests that can be served concurrently</span></span> |<span data-ttu-id="566f4-128">20</span><span class="sxs-lookup"><span data-stu-id="566f4-128">20</span></span> |
| <span data-ttu-id="566f4-129">[mapreduce.jobhistory.max yaş ms][max-age-ms]</span><span class="sxs-lookup"><span data-stu-id="566f4-129">[mapreduce.jobhistory.max-age-ms][max-age-ms]</span></span> |<span data-ttu-id="566f4-130">İş Geçmişi gün sayısını korunur</span><span class="sxs-lookup"><span data-stu-id="566f4-130">The number of days that job history are retained</span></span> |<span data-ttu-id="566f4-131">7 gün</span><span class="sxs-lookup"><span data-stu-id="566f4-131">7 days</span></span> |

## <a name="too-many-requests"></a><span data-ttu-id="566f4-132">Çok fazla istek</span><span class="sxs-lookup"><span data-stu-id="566f4-132">Too many requests</span></span>

<span data-ttu-id="566f4-133">**HTTP durum kodu**: 429</span><span class="sxs-lookup"><span data-stu-id="566f4-133">**HTTP Status code**: 429</span></span>

| <span data-ttu-id="566f4-134">Nedeni</span><span class="sxs-lookup"><span data-stu-id="566f4-134">Cause</span></span> | <span data-ttu-id="566f4-135">Çözüm</span><span class="sxs-lookup"><span data-stu-id="566f4-135">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="566f4-136">(Varsayılan 20) dakika başına WebHCat tarafından sunulan en fazla eşzamanlı istek sınırı aşıldı</span><span class="sxs-lookup"><span data-stu-id="566f4-136">You have exceeded the maximum concurrent requests served by WebHCat per minute (default 20)</span></span> |<span data-ttu-id="566f4-137">En fazla eş zamanlı istek sayısını birden değil gönderdiğiniz emin olmak için iş yükünü azaltın veya değiştirerek eşzamanlı istek sınırı artırmak `templeton.exec.max-procs`.</span><span class="sxs-lookup"><span data-stu-id="566f4-137">Reduce your workload to ensure that you do not submit more than the maximum number of concurrent requests or increase the concurrent request limit by modifying `templeton.exec.max-procs`.</span></span> <span data-ttu-id="566f4-138">Daha fazla bilgi için bkz: [değiştirme yapılandırma](#modifying-configuration)</span><span class="sxs-lookup"><span data-stu-id="566f4-138">For more information, see [Modifying configuration](#modifying-configuration)</span></span> |

## <a name="server-unavailable"></a><span data-ttu-id="566f4-139">Sunucu kullanılamıyor</span><span class="sxs-lookup"><span data-stu-id="566f4-139">Server unavailable</span></span>

<span data-ttu-id="566f4-140">**HTTP durum kodu**: 503</span><span class="sxs-lookup"><span data-stu-id="566f4-140">**HTTP Status code**: 503</span></span>

| <span data-ttu-id="566f4-141">Nedeni</span><span class="sxs-lookup"><span data-stu-id="566f4-141">Cause</span></span> | <span data-ttu-id="566f4-142">Çözüm</span><span class="sxs-lookup"><span data-stu-id="566f4-142">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="566f4-143">Bu durum kodu küme için birincil ve ikincil HeadNode arasında yük devretme sırasında genellikle oluşur.</span><span class="sxs-lookup"><span data-stu-id="566f4-143">This status code usually occurs during failover between the primary and secondary HeadNode for the cluster</span></span> |<span data-ttu-id="566f4-144">İki dakika bekleyin ve sonra işlemi yeniden deneyin</span><span class="sxs-lookup"><span data-stu-id="566f4-144">Wait two minutes, then retry the operation</span></span> |

## <a name="bad-request-content-could-not-find-job"></a><span data-ttu-id="566f4-145">Hatalı istek içeriği: işi bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="566f4-145">Bad request Content: Could not find job</span></span>

<span data-ttu-id="566f4-146">**HTTP durum kodu**: 400</span><span class="sxs-lookup"><span data-stu-id="566f4-146">**HTTP Status code**: 400</span></span>

| <span data-ttu-id="566f4-147">Nedeni</span><span class="sxs-lookup"><span data-stu-id="566f4-147">Cause</span></span> | <span data-ttu-id="566f4-148">Çözüm</span><span class="sxs-lookup"><span data-stu-id="566f4-148">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="566f4-149">İş ayrıntılarını tarafından iş geçmişi temizleyici temizlendi</span><span class="sxs-lookup"><span data-stu-id="566f4-149">Job details have been cleaned up by the job history cleaner</span></span> |<span data-ttu-id="566f4-150">İş geçmişi için varsayılan saklama dönemi 7 gündür.</span><span class="sxs-lookup"><span data-stu-id="566f4-150">The default retention period for job history is 7 days.</span></span> <span data-ttu-id="566f4-151">Varsayılan saklama dönemi değiştirerek değiştirilebilir `mapreduce.jobhistory.max-age-ms`.</span><span class="sxs-lookup"><span data-stu-id="566f4-151">The default retention period can be changed by modifying `mapreduce.jobhistory.max-age-ms`.</span></span> <span data-ttu-id="566f4-152">Daha fazla bilgi için bkz: [değiştirme yapılandırma](#modifying-configuration)</span><span class="sxs-lookup"><span data-stu-id="566f4-152">For more information, see [Modifying configuration](#modifying-configuration)</span></span> |
| <span data-ttu-id="566f4-153">İş bir yük devretmesi nedeniyle sonlandırıldı</span><span class="sxs-lookup"><span data-stu-id="566f4-153">Job has been killed due to a failover</span></span> |<span data-ttu-id="566f4-154">İş gönderme iki dakikaya kadar yeniden dene</span><span class="sxs-lookup"><span data-stu-id="566f4-154">Retry job submission for up to two minutes</span></span> |
| <span data-ttu-id="566f4-155">Geçersiz iş kimliği kullanıldı</span><span class="sxs-lookup"><span data-stu-id="566f4-155">An Invalid job id was used</span></span> |<span data-ttu-id="566f4-156">İş kimliğini doğru olup olmadığını denetleyin</span><span class="sxs-lookup"><span data-stu-id="566f4-156">Check if the job id is correct</span></span> |

## <a name="bad-gateway"></a><span data-ttu-id="566f4-157">Hatalı ağ geçidi</span><span class="sxs-lookup"><span data-stu-id="566f4-157">Bad gateway</span></span>

<span data-ttu-id="566f4-158">**HTTP durum kodu**: 502</span><span class="sxs-lookup"><span data-stu-id="566f4-158">**HTTP Status code**: 502</span></span>

| <span data-ttu-id="566f4-159">Nedeni</span><span class="sxs-lookup"><span data-stu-id="566f4-159">Cause</span></span> | <span data-ttu-id="566f4-160">Çözüm</span><span class="sxs-lookup"><span data-stu-id="566f4-160">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="566f4-161">İç çöp toplama WebHCat işlemi içinde gerçekleşen</span><span class="sxs-lookup"><span data-stu-id="566f4-161">Internal garbage collection is occurring within the WebHCat process</span></span> |<span data-ttu-id="566f4-162">Çöp toplama son veya WebHCat hizmetini yeniden başlatmak bekleyin</span><span class="sxs-lookup"><span data-stu-id="566f4-162">Wait for garbage collection to finish or restart the WebHCat service</span></span> |
| <span data-ttu-id="566f4-163">ResourceManager hizmetinden bir yanıt beklenirken zaman aşımı.</span><span class="sxs-lookup"><span data-stu-id="566f4-163">Time out waiting on a response from the ResourceManager service.</span></span> <span data-ttu-id="566f4-164">Etkin uygulama sayısı yapılandırılan en büyük (varsayılan 10.000) olduğunda bu hata oluşabilir</span><span class="sxs-lookup"><span data-stu-id="566f4-164">This error can occur when the number of active applications goes the configured maximum (default 10,000)</span></span> |<span data-ttu-id="566f4-165">Şu anda çalışan tamamlamak veya değiştirerek eşzamanlı iş sınırını artırmak için işi bekleyin `yarn.scheduler.capacity.maximum-applications`.</span><span class="sxs-lookup"><span data-stu-id="566f4-165">Wait for currently running jobs to complete or increase the concurrent job limit by modifying `yarn.scheduler.capacity.maximum-applications`.</span></span> <span data-ttu-id="566f4-166">Daha fazla bilgi için bkz: [değiştirme yapılandırma](#modifying-configuration) bölümü.</span><span class="sxs-lookup"><span data-stu-id="566f4-166">For more information, see the [Modifying configuration](#modifying-configuration) section.</span></span> |
| <span data-ttu-id="566f4-167">Tüm işleri aracılığıyla almaya [GET /jobs](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference+Jobs) çağrısı sırasında `Fields` ayarlanır`*`</span><span class="sxs-lookup"><span data-stu-id="566f4-167">Attempting to retrieve all jobs through the [GET /jobs](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference+Jobs) call while `Fields` is set to `*`</span></span> |<span data-ttu-id="566f4-168">Alamadı *tüm* iş ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="566f4-168">Do not retrieve *all* job details.</span></span> <span data-ttu-id="566f4-169">Bunun yerine kullanın `jobid` yalnızca belirli iş kimliği büyük projeler için Ayrıntılar alınamadı.</span><span class="sxs-lookup"><span data-stu-id="566f4-169">Instead use `jobid` to retrieve details for jobs only greater than certain job id.</span></span> <span data-ttu-id="566f4-170">Ya da kullanmayın`Fields`</span><span class="sxs-lookup"><span data-stu-id="566f4-170">Or, do not use `Fields`</span></span> |
| <span data-ttu-id="566f4-171">HeadNode yük devretme sırasında WebHCat hizmeti çalışmıyor</span><span class="sxs-lookup"><span data-stu-id="566f4-171">The WebHCat service is down during HeadNode failover</span></span> |<span data-ttu-id="566f4-172">İki dakika bekleyin ve işlemi yeniden deneyin</span><span class="sxs-lookup"><span data-stu-id="566f4-172">Wait for two minutes and retry the operation</span></span> |
| <span data-ttu-id="566f4-173">WebHCat gönderilen 500'den fazla bekleyen iş</span><span class="sxs-lookup"><span data-stu-id="566f4-173">There are more than 500 pending jobs submitted through WebHCat</span></span> |<span data-ttu-id="566f4-174">Daha fazla iş göndermeden önce şu anda bekleyen işler tamamlanana kadar bekleyin</span><span class="sxs-lookup"><span data-stu-id="566f4-174">Wait until currently pending jobs have completed before submitting more jobs</span></span> |

[maximum-applications]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.3/bk_system-admin-guide/content/setting_application_limits.html
[max-procs]: https://hive.apache.org/javadocs/hcat-r0.5.0/configuration.html
[max-age-ms]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.6.0/ds_Hadoop/hadoop-mapreduce-client/hadoop-mapreduce-client-core/mapred-default.xml
