---
title: "Azure Güvenlik Merkezi'nde doğrulama aaaAlerts | Microsoft Docs"
description: "Bu belge, Azure Güvenlik Merkezi'nde toovalidate hello güvenlik uyarılarını yardımcı olur."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: f8f17a55-e672-4d86-8ba9-6c3ce2e71a57
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2017
ms.author: yurid
ms.openlocfilehash: 030e9e74303758192eedaf517f1cb0d2e4a7852e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="alerts-validation-in-azure-security-center"></a><span data-ttu-id="14413-103">Azure Güvenlik Merkezi'nde Uyarıları Doğrulama</span><span class="sxs-lookup"><span data-stu-id="14413-103">Alerts Validation in Azure Security Center</span></span>
<span data-ttu-id="14413-104">Bu belge öğrenmenize yardımcı olur nasıl sisteminiz için Azure Güvenlik Merkezi uyarılarını düzgün şekilde yapılandırılmışsa tooverify.</span><span class="sxs-lookup"><span data-stu-id="14413-104">This document helps you learn how tooverify if your system is properly configured for Azure Security Center alerts.</span></span>

## <a name="what-are-security-alerts"></a><span data-ttu-id="14413-105">Güvenlik uyarıları nedir?</span><span class="sxs-lookup"><span data-stu-id="14413-105">What are security alerts?</span></span>
<span data-ttu-id="14413-106">Güvenlik Merkezi otomatik olarak toplar, analiz eder ve Azure kaynakları, hello ağ ve güvenlik duvarı ve endpoint protection çözümleri, toodetect ve uyarı, toothreats gibi bağlı iş ortağı çözümlerinden günlük verilerini tümleştirir.</span><span class="sxs-lookup"><span data-stu-id="14413-106">Security Center automatically collects, analyzes, and integrates log data from your Azure resources, hello network, and connected partner solutions, like firewall and endpoint protection solutions, toodetect and alert you toothreats.</span></span> <span data-ttu-id="14413-107">Okuma [yönetme ve yanıt toosecurity Azure Güvenlik Merkezi'nde uyarıları](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts) güvenlik uyarıları ve okuma hakkında daha fazla bilgi için [Azure Güvenlik Merkezi'nde güvenlik uyarıları anlama](https://docs.microsoft.com/azure/security-center/security-center-alerts-type) toolearn daha fazla Merhaba farklı türde bir uyarı hakkında.</span><span class="sxs-lookup"><span data-stu-id="14413-107">Read [Managing and responding toosecurity alerts in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts) for more information about security alerts, and read [Understanding security alerts in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-alerts-type) toolearn more about hello different types of alerts.</span></span>

## <a name="alert-validation"></a><span data-ttu-id="14413-108">Uyarı doğrulaması</span><span class="sxs-lookup"><span data-stu-id="14413-108">Alert validation</span></span>
<span data-ttu-id="14413-109">Güvenlik Merkezi Aracısı, bilgisayarınızda yüklendikten sonra toobe saldırıya hello kaynak hello uyarının istediğiniz hello bilgisayardan hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="14413-109">After Security Center agent is installed on your computer, follow hello steps below from hello computer where you want toobe hello attacked resource of hello alert:</span></span>

1. <span data-ttu-id="14413-110">Bir yürütülebilir dosya (için örnek calc.exe) toohello bilgisayarın masaüstünde veya diğer kolaylık dizininin kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="14413-110">Copy an executable (for example calc.exe) toohello computer’s desktop, or other directory of your convenience.</span></span>
2. <span data-ttu-id="14413-111">Bu dosyayı yeniden adlandırmak çok**ASC_AlertTest_662jfi039N.exe**.</span><span class="sxs-lookup"><span data-stu-id="14413-111">Rename this file too**ASC_AlertTest_662jfi039N.exe**.</span></span>
3. <span data-ttu-id="14413-112">Merhaba komut istemi açın ve bu dosyayı (yalnızca bir sahte bağımsız değişkeni adı), bağımsız değişkeni gibi yürütün: *ASC_AlertTest_662jfi039N.exe - foo*</span><span class="sxs-lookup"><span data-stu-id="14413-112">Open hello command prompt and execute this file with an argument (just a fake argument name), such as: *ASC_AlertTest_662jfi039N.exe -foo*</span></span>
4. <span data-ttu-id="14413-113">5 too10 dakika bekleyin ve Güvenlik Merkezi uyarılarını açın.</span><span class="sxs-lookup"><span data-stu-id="14413-113">Wait 5 too10 minutes and open Security Center Alerts.</span></span> <span data-ttu-id="14413-114">Var. bir uyarı benzer toofollowing bir bulmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="14413-114">There you should find an alert similar toofollowing one:</span></span>

    ![Uyarı Doğrulaması](./media/security-center-alert-validation/security-center-alert-validation-fig1.png)

<span data-ttu-id="14413-116">Bu uyarıyı gözden geçirirken hello alan bağımsız değişkenleri denetiminin etkin olarak doğru göründüğünden emin olun.</span><span class="sxs-lookup"><span data-stu-id="14413-116">When reviewing this alert, make sure hello field Arguments Auditing Enabled appears as true.</span></span> <span data-ttu-id="14413-117">False gösteriyorsa, Denetim tooenable komut satırı bağımsız değişkenleri gerekir.</span><span class="sxs-lookup"><span data-stu-id="14413-117">If it shows false, you need tooenable command-line arguments auditing.</span></span> <span data-ttu-id="14413-118">Komut satırı aşağıdaki hello kullanarak bu seçeneği etkinleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="14413-118">You can enable this option using hello following command line:</span></span>

<span data-ttu-id="14413-119">*reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\Audit" /f /v "ProcessCreationIncludeCmdLine_Enabled"*</span><span class="sxs-lookup"><span data-stu-id="14413-119">*reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\Audit" /f /v "ProcessCreationIncludeCmdLine_Enabled"*</span></span>


## <a name="see-also"></a><span data-ttu-id="14413-120">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="14413-120">See also</span></span>
<span data-ttu-id="14413-121">Bu makalede toohello uyarıları doğrulama işlemini kullanıma sunuldu.</span><span class="sxs-lookup"><span data-stu-id="14413-121">This article introduced you toohello alerts validation process.</span></span> <span data-ttu-id="14413-122">Bu doğrulama ile tanıdık, makaleler hello deneyin:</span><span class="sxs-lookup"><span data-stu-id="14413-122">Now that you're familiar with this validation, try hello following articles:</span></span>

* <span data-ttu-id="14413-123">[Azure Güvenlik Merkezi'nde Uyarıları yönetme ve yanıt toosecurity](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts).</span><span class="sxs-lookup"><span data-stu-id="14413-123">[Managing and responding toosecurity alerts in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts).</span></span> <span data-ttu-id="14413-124">Bilgi nasıl toomanage uyarıları ve Güvenlik Merkezi'nde yanıt toosecurity olaylar.</span><span class="sxs-lookup"><span data-stu-id="14413-124">Learn how toomanage alerts, and respond toosecurity incidents in Security Center.</span></span>
* <span data-ttu-id="14413-125">[Azure Güvenlik Merkezi'nde güvenlik durumunu izleme](security-center-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="14413-125">[Security health monitoring in Azure Security Center](security-center-monitoring.md).</span></span> <span data-ttu-id="14413-126">Nasıl toomonitor hello Azure kaynaklarınızın sistem durumunu öğrenin.</span><span class="sxs-lookup"><span data-stu-id="14413-126">Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="14413-127">[Azure Güvenlik Merkezi'ndeki güvenlik uyarılarını anlama](https://docs.microsoft.com/azure/security-center/security-center-alerts-type).</span><span class="sxs-lookup"><span data-stu-id="14413-127">[Understanding security alerts in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-alerts-type).</span></span> <span data-ttu-id="14413-128">Merhaba farklı türlerde güvenlik uyarıları hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="14413-128">Learn about hello different types of security alerts.</span></span>
* <span data-ttu-id="14413-129">[Azure Güvenlik Merkezi Sorun Giderme Kılavuzu](https://docs.microsoft.com/azure/security-center/security-center-troubleshooting-guide).</span><span class="sxs-lookup"><span data-stu-id="14413-129">[Azure Security Center Troubleshooting Guide](https://docs.microsoft.com/azure/security-center/security-center-troubleshooting-guide).</span></span> <span data-ttu-id="14413-130">Güvenlik Merkezi'nde nasıl tootroubleshoot ortak sorunlar hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="14413-130">Learn how tootroubleshoot common issues in Security Center.</span></span> 
* <span data-ttu-id="14413-131">[Azure Güvenlik Merkezi SSS](security-center-faq.md).</span><span class="sxs-lookup"><span data-stu-id="14413-131">[Azure Security Center FAQ](security-center-faq.md).</span></span> <span data-ttu-id="14413-132">Merhaba Hizmeti'ni kullanma hakkında sık sorulan soruları bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="14413-132">Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="14413-133">[Azure Güvenlik Blogu](http://blogs.msdn.com/b/azuresecurity/).</span><span class="sxs-lookup"><span data-stu-id="14413-133">[Azure Security Blog](http://blogs.msdn.com/b/azuresecurity/).</span></span> <span data-ttu-id="14413-134">Azure güvenliği ve uyumluluğu ile ilgili blog yazılarını bulun.</span><span class="sxs-lookup"><span data-stu-id="14413-134">Find blog posts about Azure security and compliance.</span></span>

