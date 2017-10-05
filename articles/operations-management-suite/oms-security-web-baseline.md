---
title: "Operations Management Suite Güvenlik ve Denetim Çözümü Web Temeli | Microsoft Docs"
description: "Bu belgede; uyumluluk ve güvenlik amaçlarıyla, izlenen tüm web sunucularında bir web temeli değerlendirmesinin gerçekleştirilmesi için OMS Güvenlik ve Denetim çözümünün nasıl kullanılacağı açıklanmaktadır."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ROBOTS: NOINDEX
redirect_url: https://www.microsoft.com/cloud-platform/security-and-compliance
ms.assetid: 17837c8b-3e79-47c0-9b83-a51c6ca44ca6
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: yurid
ms.openlocfilehash: 0d4707dc0c0ffbf40d0d10a6d12b9709a9655258
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="web-baseline-assessment-in-operations-management-suite-security-and-audit-solution"></a><span data-ttu-id="b7eb0-103">Operations Management Suite Güvenlik ve Denetim Çözümünde Web Temeli Değerlendirmesi</span><span class="sxs-lookup"><span data-stu-id="b7eb0-103">Web Baseline Assessment in Operations Management Suite Security and Audit Solution</span></span>
<span data-ttu-id="b7eb0-104">Bu belge, izlenen kaynaklarınızın güvenlik durumuna erişmek için [Operations Management Suite (OMS) Güvenlik ve Denetim Çözümü](operations-management-suite-overview.md) web temeli değerlendirmesi özelliklerini kullanmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="b7eb0-104">This document helps you to use [Operations Management Suite (OMS) Security and Audit Solution](operations-management-suite-overview.md) web baseline assessment capabilities to access the secure state of your monitored resources.</span></span>

## <a name="what-is-web-baseline-assessment"></a><span data-ttu-id="b7eb0-105">Web Temeli Değerlendirmesi nedir?</span><span class="sxs-lookup"><span data-stu-id="b7eb0-105">What is Web Baseline Assessment?</span></span>
<span data-ttu-id="b7eb0-106">OMS Güvenliği şu anda işletim sistemleri için güvenlik temeli değerlendirmesi sağlamaktadır.</span><span class="sxs-lookup"><span data-stu-id="b7eb0-106">Currently OMS Security provides security baseline assessment for operating systems.</span></span> <span data-ttu-id="b7eb0-107">Sunucularınızın işletim sistemi ayarlarını 24 saatte bir taramakta ve savunmasız olabilecek ayarları görüntülemeyi sağlamaktadır.</span><span class="sxs-lookup"><span data-stu-id="b7eb0-107">It scans the operating system settings of your servers every 24 hours and provides a view into potentially vulnerable settings.</span></span> <span data-ttu-id="b7eb0-108">Bu seçenek hakkında daha fazla bilgi için [Operations Management Suite Güvenlik ve Denetim Çözümünde Temel Değerlendirmesi](oms-security-baseline.md) makalesini okuyun.</span><span class="sxs-lookup"><span data-stu-id="b7eb0-108">Read [Baseline Assessment in Operations Management Suite Security and Audit Solution](oms-security-baseline.md) for more information on this.</span></span>

<span data-ttu-id="b7eb0-109">Web temeli değerlendirmesinin amacı, savunmasız olabilecek web sunucusu ayarlarını bulmaktır.</span><span class="sxs-lookup"><span data-stu-id="b7eb0-109">The goal of the web baseline assessment is to find potentially vulnerable web server settings.</span></span> <span data-ttu-id="b7eb0-110">Web temeli yapılandırmaları için üç birincil kaynak şunlardır: .NET, ASP.NET ve IIS yapılandırması.</span><span class="sxs-lookup"><span data-stu-id="b7eb0-110">The three primary sources for the web baseline configurations are: .NET, ASP.NET, and IIS configuration.</span></span>  <span data-ttu-id="b7eb0-111">İşletim sistemi temel değerlendirmesinde olduğu gibi, OMS Güvenliği web sunucularınızı 24 saatte bir tarar ve güvenlik durumlarını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="b7eb0-111">Just like the operating system baseline assessment, OMS Security is going to scan your web servers every 24hrs and provide a view into security state of them.</span></span>  <span data-ttu-id="b7eb0-112">Internet Information Service (IIS) hizmetinde yapılandırmalar yüksek oranda özelleştirilebilir durumdadır, sonuç olarak çeşitli site ve uygulama düzeyleri geçersiz kılınabilir.</span><span class="sxs-lookup"><span data-stu-id="b7eb0-112">In Internet Information Service (IIS), configurations are highly customizable, which allows various site and application levels to be overridden.</span></span> <span data-ttu-id="b7eb0-113">Tarayıcı varsayılan kök düzeye ek olarak her bir uygulama/site düzeyindeki ayarları denetler.</span><span class="sxs-lookup"><span data-stu-id="b7eb0-113">The scanner checks the settings at each application/site level in addition to the default root level.</span></span> <span data-ttu-id="b7eb0-114">Bunun yapılması, savunmasız olabilecek ayarların konumlarını belirlemenize ve hızlıca düzeltmenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="b7eb0-114">This helps you to identify potential vulnerability settings locations and quickly remediate.</span></span>


## <a name="web-security-baseline-assessment"></a><span data-ttu-id="b7eb0-115">Web Güvenlik Temeli Değerlendirmesi</span><span class="sxs-lookup"><span data-stu-id="b7eb0-115">Web Security Baseline Assessment</span></span>
<span data-ttu-id="b7eb0-116">Bu önizleme sürümünde bu özelliğe OMS Arama seçeneği kullanılarak erişilecektir.</span><span class="sxs-lookup"><span data-stu-id="b7eb0-116">For this preview this feature is going to be accessed using the OMS Search option.</span></span> <span data-ttu-id="b7eb0-117">Uygun sorguyu gerçekleştirmek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="b7eb0-117">Follow the steps below to perform the appropriated query:</span></span>

1. <span data-ttu-id="b7eb0-118">**Microsoft Operations Management Suite** ana panosunda, **Güvenlik ve Denetim** kutucuğuna tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b7eb0-118">In the **Microsoft Operations Management Suite** main dashboard click **Security and Audit** tile.</span></span>
2. <span data-ttu-id="b7eb0-119">**Güvenlik ve Denetim** panosunda **Günlük Araması** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b7eb0-119">In the **Security and Audit** dashboard, click **Log Search** button.</span></span>
3. <span data-ttu-id="b7eb0-120">Kullanabileceğiniz ilk sorgu **Web Temeli Değerlendirme Özeti**’dir.</span><span class="sxs-lookup"><span data-stu-id="b7eb0-120">The first query that you can use is the **Web Baseline Assessment Summary**.</span></span> <span data-ttu-id="b7eb0-121">**Aramaya buradan başlayın** alanına şu sorguyu yazın: Type*=SecurityBaselineSummary BaselineType=web*.</span><span class="sxs-lookup"><span data-stu-id="b7eb0-121">In the **Begin search here** field, type this query: Type*=SecurityBaselineSummary BaselineType=web*.</span></span> <span data-ttu-id="b7eb0-122">Aşağıdaki ekranda bir örnek çıktı gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="b7eb0-122">The following screen has an output sample:</span></span>

![Web temeli değerlendirme özeti](./media/oms-security-web-baseline/oms-security-web-baseline-fig1-new.png)

> [!NOTE]
> <span data-ttu-id="b7eb0-124">Bu sorguda her kayıt, tek bir sunucu üzerindeki değerlendirme özetini gösterir.</span><span class="sxs-lookup"><span data-stu-id="b7eb0-124">In this query, each record indicates assessment summary on a single server.</span></span>

<span data-ttu-id="b7eb0-125">**Günlük Araması** menüsüne geldikten sonra, web temeli değerlendirmesi hakkında daha fazla bilgi almak için farklı sorgular yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b7eb0-125">Once you are in the **Log Search**, you can type different queries to obtain more information about the web baseline assessment.</span></span> <span data-ttu-id="b7eb0-126">Önceki sorguya ek olarak, bu önizlemede aşağıdaki sorguyu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b7eb0-126">In addition to the previous query, you can also use the following ones in this preview.</span></span>

<span data-ttu-id="b7eb0-127">**Web Temeli Kural Değerlendirmesi**: Her kayıt, tek bir sunucudaki tek bir web temeli kural değerlendirmesini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="b7eb0-127">**Web Baseline Rule Assessment**: Each record represents a single web baseline rule evaluation on a single server.</span></span> <span data-ttu-id="b7eb0-128">Bu kayıt; kural, konum, beklenen sonuç ve gerçek sonucun tüm verilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="b7eb0-128">It includes all data for the rule, location, the expected result, and the actual result.</span></span>

<span data-ttu-id="b7eb0-129">**Sorgu**: Type*=SecurityBaseline BaselineType=web*</span><span class="sxs-lookup"><span data-stu-id="b7eb0-129">**Query**: Type*=SecurityBaseline BaselineType=web*</span></span>

![Web temeli kural değerlendirmesi](./media/oms-security-web-baseline/oms-security-web-baseline-fig2.png)

<span data-ttu-id="b7eb0-131">**Belirli bir sunucu için tüm sonuçları göster**: Bu sorgu belirli bir sunucunun sonuçlarının nasıl görüntüleneceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="b7eb0-131">**Show all results for a specific server**: This query shows how to see results of a specific server.</span></span>

<span data-ttu-id="b7eb0-132">**Sorgu**: *Type=SecurityBaseline BaselineType=web Computer=BaselineTestVM1*</span><span class="sxs-lookup"><span data-stu-id="b7eb0-132">**Query**: *Type=SecurityBaseline BaselineType=web Computer=BaselineTestVM1*</span></span>

![Tüm sonuçlar](./media/oms-security-web-baseline/oms-security-web-baseline-fig3.png)

<span data-ttu-id="b7eb0-134">Bu kayıtları/sorguları, kendi pano, rapor veya uyarılarınızı oluşturmak için de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b7eb0-134">You can also use these records/queries to create your own dashboards, reports, or alerts.</span></span> <span data-ttu-id="b7eb0-135">Aşağıdaki ekranda panonuza ekleyebileceğiniz bir örnek kullanıcı arabirimi denetimi gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="b7eb0-135">The screen below has a sample UI control that you can add to your dashboard.</span></span> <span data-ttu-id="b7eb0-136">OMS Görünüm Tasarımcısı kullanarak verilerinizi nasıl görselleştirebileceğinizi [buradan](https://blogs.technet.microsoft.com/msoms/2016/06/30/oms-view-designer-visualize-your-data-your-way/) öğrenebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b7eb0-136">You can learn how to visualize your data using OMS View Designer [here](https://blogs.technet.microsoft.com/msoms/2016/06/30/oms-view-designer-visualize-your-data-your-way/).</span></span> <span data-ttu-id="b7eb0-137">Aşağıdaki ekran, bu özelleştirme yapıldıktan sonra kutucuğun nasıl görüneceğine ilişkin bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="b7eb0-137">The screen below is an example of how the tile will look like once you make this customization.</span></span>

![Örnek Kullanıcı Arabirimi](./media/oms-security-web-baseline/oms-security-web-baseline-fig4.png)

> [!NOTE]
> <span data-ttu-id="b7eb0-139">Temel değerlendirme için işaretlenen ayarları bilmek istiyorsanız, bu ayarları içeren [Excel elektronik tablosunu](https://gallery.technet.microsoft.com/OMS-Web-Baseline-1e811690) indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b7eb0-139">If you would like to know the settings that are checked for the baseline assessment, you can download [this Excel spreadsheet](https://gallery.technet.microsoft.com/OMS-Web-Baseline-1e811690) that contains these settings.</span></span>

## <a name="see-also"></a><span data-ttu-id="b7eb0-140">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="b7eb0-140">See also</span></span>
<span data-ttu-id="b7eb0-141">Bu belgede OMS Güvenlik ve Denetim web temeli değerlendirmesi hakkında bilgi edindiniz.</span><span class="sxs-lookup"><span data-stu-id="b7eb0-141">In this document, you learned about OMS Security and Audit web baseline assessment.</span></span> <span data-ttu-id="b7eb0-142">OMS Güvenlik hakkında daha fazla bilgi edinmek için şu makalelere göz atın:</span><span class="sxs-lookup"><span data-stu-id="b7eb0-142">To learn more about OMS Security, see the following articles:</span></span>

* [<span data-ttu-id="b7eb0-143">Operations Management Suite'e (OMS) genel bakış</span><span class="sxs-lookup"><span data-stu-id="b7eb0-143">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="b7eb0-144">Operations Management Suite Güvenlik ve Denetim Çözümünde Güvenlik Uyarılarını İzleme ve Yanıtlama</span><span class="sxs-lookup"><span data-stu-id="b7eb0-144">Monitoring and Responding to Security Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)
* [<span data-ttu-id="b7eb0-145">Operations Management Suite Güvenlik ve Denetim Çözümünde Kaynakları İzleme</span><span class="sxs-lookup"><span data-stu-id="b7eb0-145">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)

