---
title: "Yönetim Paketi güvenlik ve denetim çözüm Web temel aaaOperations | Microsoft Docs"
description: "Bu belge açıklar nasıl toouse OMS güvenlik ve denetim çözüm tooperform web temeli değerlendirme uyumluluk ve güvenlik amaçla tüm izlenen web sunucuları."
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
ms.openlocfilehash: 8aa87fa404ff97ab549dda3f9bebb75766055963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="web-baseline-assessment-in-operations-management-suite-security-and-audit-solution"></a><span data-ttu-id="e2bdd-103">Operations Management Suite Güvenlik ve Denetim Çözümünde Web Temeli Değerlendirmesi</span><span class="sxs-lookup"><span data-stu-id="e2bdd-103">Web Baseline Assessment in Operations Management Suite Security and Audit Solution</span></span>
<span data-ttu-id="e2bdd-104">Bu belge toouse yardımcı olur [Operations Management Suite (OMS) güvenlik ve denetim çözümü](operations-management-suite-overview.md) web özellikleri tooaccess hello izlenen kaynaklarınızın güvenli durumunu temel değerlendirmesi.</span><span class="sxs-lookup"><span data-stu-id="e2bdd-104">This document helps you toouse [Operations Management Suite (OMS) Security and Audit Solution](operations-management-suite-overview.md) web baseline assessment capabilities tooaccess hello secure state of your monitored resources.</span></span>

## <a name="what-is-web-baseline-assessment"></a><span data-ttu-id="e2bdd-105">Web Temeli Değerlendirmesi nedir?</span><span class="sxs-lookup"><span data-stu-id="e2bdd-105">What is Web Baseline Assessment?</span></span>
<span data-ttu-id="e2bdd-106">OMS Güvenliği şu anda işletim sistemleri için güvenlik temeli değerlendirmesi sağlamaktadır.</span><span class="sxs-lookup"><span data-stu-id="e2bdd-106">Currently OMS Security provides security baseline assessment for operating systems.</span></span> <span data-ttu-id="e2bdd-107">Hello işletim sistemi ayarlarını, sunucularınızın her 24 saatte tarar ve savunmasız olabilecek ayarları içine bir görünümünü sağlar.</span><span class="sxs-lookup"><span data-stu-id="e2bdd-107">It scans hello operating system settings of your servers every 24 hours and provides a view into potentially vulnerable settings.</span></span> <span data-ttu-id="e2bdd-108">Bu seçenek hakkında daha fazla bilgi için [Operations Management Suite Güvenlik ve Denetim Çözümünde Temel Değerlendirmesi](oms-security-baseline.md) makalesini okuyun.</span><span class="sxs-lookup"><span data-stu-id="e2bdd-108">Read [Baseline Assessment in Operations Management Suite Security and Audit Solution](oms-security-baseline.md) for more information on this.</span></span>

<span data-ttu-id="e2bdd-109">Merhaba hello web temeli değerlendirme toofind savunmasız olabilecek web sunucusu ayarları hedefidir.</span><span class="sxs-lookup"><span data-stu-id="e2bdd-109">hello goal of hello web baseline assessment is toofind potentially vulnerable web server settings.</span></span> <span data-ttu-id="e2bdd-110">Merhaba web temel yapılandırmalar için üç birincil kaynağı hello: .NET, ASP.NET ve IIS yapılandırması.</span><span class="sxs-lookup"><span data-stu-id="e2bdd-110">hello three primary sources for hello web baseline configurations are: .NET, ASP.NET, and IIS configuration.</span></span>  <span data-ttu-id="e2bdd-111">Yalnızca işletim sistemi temel değerlendirme hello gibi OMS güvenlik tooscan geçiyor, her 24hrs web sunucuları ve bunları güvenlik durumunu görünüme sağlayın.</span><span class="sxs-lookup"><span data-stu-id="e2bdd-111">Just like hello operating system baseline assessment, OMS Security is going tooscan your web servers every 24hrs and provide a view into security state of them.</span></span>  <span data-ttu-id="e2bdd-112">Internet Information Service (IIS), çeşitli site ve uygulama düzeyleri toobe ilgili geçersiz kılınmış sağlayan, yapılandırmaları büyük ölçüde özelleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="e2bdd-112">In Internet Information Service (IIS), configurations are highly customizable, which allows various site and application levels toobe overridden.</span></span> <span data-ttu-id="e2bdd-113">Merhaba tarayıcı toplama toohello varsayılan kök düzeyinde her uygulama/site düzeyinde hello ayarlarını denetler.</span><span class="sxs-lookup"><span data-stu-id="e2bdd-113">hello scanner checks hello settings at each application/site level in addition toohello default root level.</span></span> <span data-ttu-id="e2bdd-114">Bu tooidentify olası güvenlik açığı ayarları konumları yardımcı olur ve hızlı bir şekilde düzeltin.</span><span class="sxs-lookup"><span data-stu-id="e2bdd-114">This helps you tooidentify potential vulnerability settings locations and quickly remediate.</span></span>


## <a name="web-security-baseline-assessment"></a><span data-ttu-id="e2bdd-115">Web Güvenlik Temeli Değerlendirmesi</span><span class="sxs-lookup"><span data-stu-id="e2bdd-115">Web Security Baseline Assessment</span></span>
<span data-ttu-id="e2bdd-116">Bu önizleme için bu özelliği hello OMS arama seçeneği kullanılarak erişilir toobe geçiyor.</span><span class="sxs-lookup"><span data-stu-id="e2bdd-116">For this preview this feature is going toobe accessed using hello OMS Search option.</span></span> <span data-ttu-id="e2bdd-117">Tooperform tahsis hello sorgu Hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="e2bdd-117">Follow hello steps below tooperform hello appropriated query:</span></span>

1. <span data-ttu-id="e2bdd-118">Merhaba, **Microsoft Operations Management Suite** ana Pano tıklatın **güvenlik ve Denetim** döşeme.</span><span class="sxs-lookup"><span data-stu-id="e2bdd-118">In hello **Microsoft Operations Management Suite** main dashboard click **Security and Audit** tile.</span></span>
2. <span data-ttu-id="e2bdd-119">Merhaba, **güvenlik ve Denetim** panoyu tıklatın **günlük arama** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e2bdd-119">In hello **Security and Audit** dashboard, click **Log Search** button.</span></span>
3. <span data-ttu-id="e2bdd-120">kullanabileceğiniz hello ilk sorgudur hello **Web temeli değerlendirme özeti**.</span><span class="sxs-lookup"><span data-stu-id="e2bdd-120">hello first query that you can use is hello **Web Baseline Assessment Summary**.</span></span> <span data-ttu-id="e2bdd-121">Merhaba, **burada başlangıç arama** alanına, bu sorgu yazın: türü*SecurityBaselineSummary BaselineType = web =*.</span><span class="sxs-lookup"><span data-stu-id="e2bdd-121">In hello **Begin search here** field, type this query: Type*=SecurityBaselineSummary BaselineType=web*.</span></span> <span data-ttu-id="e2bdd-122">Merhaba ekranında aşağıdaki çıktı örneği vardır:</span><span class="sxs-lookup"><span data-stu-id="e2bdd-122">hello following screen has an output sample:</span></span>

![Web temeli değerlendirme özeti](./media/oms-security-web-baseline/oms-security-web-baseline-fig1-new.png)

> [!NOTE]
> <span data-ttu-id="e2bdd-124">Bu sorguda her kayıt, tek bir sunucu üzerindeki değerlendirme özetini gösterir.</span><span class="sxs-lookup"><span data-stu-id="e2bdd-124">In this query, each record indicates assessment summary on a single server.</span></span>

<span data-ttu-id="e2bdd-125">Hello olduğunuzda **günlük arama**, farklı sorgular tooobtain hello web temeli değerlendirme hakkında daha fazla bilgi yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e2bdd-125">Once you are in hello **Log Search**, you can type different queries tooobtain more information about hello web baseline assessment.</span></span> <span data-ttu-id="e2bdd-126">Ayrıca toohello önceki sorgu olanları bu Önizleme'de aşağıdaki hello de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e2bdd-126">In addition toohello previous query, you can also use hello following ones in this preview.</span></span>

<span data-ttu-id="e2bdd-127">**Web Temeli Kural Değerlendirmesi**: Her kayıt, tek bir sunucudaki tek bir web temeli kural değerlendirmesini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="e2bdd-127">**Web Baseline Rule Assessment**: Each record represents a single web baseline rule evaluation on a single server.</span></span> <span data-ttu-id="e2bdd-128">Merhaba kuralı, konumu, beklenen hello sonuç ve hello gerçek sonucu için tüm verileri içerir.</span><span class="sxs-lookup"><span data-stu-id="e2bdd-128">It includes all data for hello rule, location, hello expected result, and hello actual result.</span></span>

<span data-ttu-id="e2bdd-129">**Sorgu**: Type*=SecurityBaseline BaselineType=web*</span><span class="sxs-lookup"><span data-stu-id="e2bdd-129">**Query**: Type*=SecurityBaseline BaselineType=web*</span></span>

![Web temeli kural değerlendirmesi](./media/oms-security-web-baseline/oms-security-web-baseline-fig2.png)

<span data-ttu-id="e2bdd-131">**Belirli bir sunucu için tüm sonuçları göster**: Bu sorgu nasıl toosee sonuçlarını gösterir belirli bir sunucunun.</span><span class="sxs-lookup"><span data-stu-id="e2bdd-131">**Show all results for a specific server**: This query shows how toosee results of a specific server.</span></span>

<span data-ttu-id="e2bdd-132">**Sorgu**: *Type=SecurityBaseline BaselineType=web Computer=BaselineTestVM1*</span><span class="sxs-lookup"><span data-stu-id="e2bdd-132">**Query**: *Type=SecurityBaseline BaselineType=web Computer=BaselineTestVM1*</span></span>

![Tüm sonuçlar](./media/oms-security-web-baseline/oms-security-web-baseline-fig3.png)

<span data-ttu-id="e2bdd-134">Bu kayıtları/sorguları toocreate kendi panolar, raporlar ve uyarılar de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e2bdd-134">You can also use these records/queries toocreate your own dashboards, reports, or alerts.</span></span> <span data-ttu-id="e2bdd-135">Merhaba ekranında aşağıdaki tooyour Pano ekleyebileceğiniz örnek UI denetimi vardır.</span><span class="sxs-lookup"><span data-stu-id="e2bdd-135">hello screen below has a sample UI control that you can add tooyour dashboard.</span></span> <span data-ttu-id="e2bdd-136">Bilgi edinebilirsiniz nasıl toovisualize OMS Görünüm Tasarımcısı kullanarak verilerinizi [burada](https://blogs.technet.microsoft.com/msoms/2016/06/30/oms-view-designer-visualize-your-data-your-way/).</span><span class="sxs-lookup"><span data-stu-id="e2bdd-136">You can learn how toovisualize your data using OMS View Designer [here](https://blogs.technet.microsoft.com/msoms/2016/06/30/oms-view-designer-visualize-your-data-your-way/).</span></span> <span data-ttu-id="e2bdd-137">Merhaba ekranında aşağıdaki bu özelleştirme yaptıktan sonra hello döşemenin nasıl örneği nasıl görüneceği gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="e2bdd-137">hello screen below is an example of how hello tile will look like once you make this customization.</span></span>

![Örnek Kullanıcı Arabirimi](./media/oms-security-web-baseline/oms-security-web-baseline-fig4.png)

> [!NOTE]
> <span data-ttu-id="e2bdd-139">Merhaba temel değerlendirmesi için işaretlenmiş olan tooknow hello ayarlar isterseniz indirebilirsiniz [bu Excel elektronik tablosu](https://gallery.technet.microsoft.com/OMS-Web-Baseline-1e811690) bu ayarları içerir.</span><span class="sxs-lookup"><span data-stu-id="e2bdd-139">If you would like tooknow hello settings that are checked for hello baseline assessment, you can download [this Excel spreadsheet](https://gallery.technet.microsoft.com/OMS-Web-Baseline-1e811690) that contains these settings.</span></span>

## <a name="see-also"></a><span data-ttu-id="e2bdd-140">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="e2bdd-140">See also</span></span>
<span data-ttu-id="e2bdd-141">Bu belgede OMS Güvenlik ve Denetim web temeli değerlendirmesi hakkında bilgi edindiniz.</span><span class="sxs-lookup"><span data-stu-id="e2bdd-141">In this document, you learned about OMS Security and Audit web baseline assessment.</span></span> <span data-ttu-id="e2bdd-142">toolearn OMS güvenlik hakkında daha fazla bilgi makaleleri aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="e2bdd-142">toolearn more about OMS Security, see hello following articles:</span></span>

* [<span data-ttu-id="e2bdd-143">Operations Management Suite'e (OMS) genel bakış</span><span class="sxs-lookup"><span data-stu-id="e2bdd-143">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="e2bdd-144">İzleme ve yanıt tooSecurity uyarıları Operations Management Suite güvenlik ve denetim çözümü</span><span class="sxs-lookup"><span data-stu-id="e2bdd-144">Monitoring and Responding tooSecurity Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)
* [<span data-ttu-id="e2bdd-145">Operations Management Suite Güvenlik ve Denetim Çözümünde Kaynakları İzleme</span><span class="sxs-lookup"><span data-stu-id="e2bdd-145">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)

