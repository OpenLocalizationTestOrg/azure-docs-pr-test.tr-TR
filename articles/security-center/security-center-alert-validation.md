---
title: "Azure Güvenlik Merkezi'nde Uyarıları Doğrulama | Microsoft Docs"
description: "Bu belge, Azure Güvenlik Merkezi'nde güvenlik uyarılarını doğrulamanıza yardımcı olur."
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
ms.openlocfilehash: 121b5d8f023a9b663d0e7af26dce8f81db27672c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="alerts-validation-in-azure-security-center"></a><span data-ttu-id="ca7de-103">Azure Güvenlik Merkezi'nde Uyarıları Doğrulama</span><span class="sxs-lookup"><span data-stu-id="ca7de-103">Alerts Validation in Azure Security Center</span></span>
<span data-ttu-id="ca7de-104">Bu belge, sisteminizin Azure Güvenlik Merkezi uyarıları için doğru yapılandırılıp yapılandırılmadığını doğrulamayı öğrenmenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="ca7de-104">This document helps you learn how to verify if your system is properly configured for Azure Security Center alerts.</span></span>

## <a name="what-are-security-alerts"></a><span data-ttu-id="ca7de-105">Güvenlik uyarıları nedir?</span><span class="sxs-lookup"><span data-stu-id="ca7de-105">What are security alerts?</span></span>
<span data-ttu-id="ca7de-106">Güvenlik Merkezi, tehditleri algılamak ve tehditler konusunda sizi uyarmak için Azure kaynaklarınızdan, ağınızdan ve güvenlik duvarı ve uç nokta koruma çözümleri gibi bağlı iş ortağı çözümlerinden günlük verilerini otomatik olarak toplar, çözümler ve tümleştirir.</span><span class="sxs-lookup"><span data-stu-id="ca7de-106">Security Center automatically collects, analyzes, and integrates log data from your Azure resources, the network, and connected partner solutions, like firewall and endpoint protection solutions, to detect and alert you to threats.</span></span> <span data-ttu-id="ca7de-107">Güvenlik uyarıları hakkında daha fazla bilgi edinmek için [Azure Güvenlik Merkezi'nde güvenlik uyarılarını yönetme ve yanıtlama](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts) konusunu; farklı uyarı türleri hakkında dah fazla bilgi edinmek içinse [Azure Güvenlik Merkezi'nde güvenlik uyarılarını anlama](https://docs.microsoft.com/azure/security-center/security-center-alerts-type) konusunu okuyun.</span><span class="sxs-lookup"><span data-stu-id="ca7de-107">Read [Managing and responding to security alerts in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts) for more information about security alerts, and read [Understanding security alerts in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-alerts-type) to learn more about the different types of alerts.</span></span>

## <a name="alert-validation"></a><span data-ttu-id="ca7de-108">Uyarı doğrulaması</span><span class="sxs-lookup"><span data-stu-id="ca7de-108">Alert validation</span></span>
<span data-ttu-id="ca7de-109">Güvenlik Merkezi aracısı bilgisayarınıza yüklendikten sonra uyarının saldırı kaynağı olmasını istediğiniz bilgisayardan aşağıdaki adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="ca7de-109">After Security Center agent is installed on your computer, follow the steps below from the computer where you want to be the attacked resource of the alert:</span></span>

1. <span data-ttu-id="ca7de-110">Bilgisayarın masaüstüne veya sizin için uygun olan başka bir dizinine yürütülebilir bir dosya (örneğin, calc.exe) kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="ca7de-110">Copy an executable (for example calc.exe) to the computer’s desktop, or other directory of your convenience.</span></span>
2. <span data-ttu-id="ca7de-111">Bu dosyayı **ASC_AlertTest_662jfi039N.exe** olarak yeniden adlandırın.</span><span class="sxs-lookup"><span data-stu-id="ca7de-111">Rename this file to **ASC_AlertTest_662jfi039N.exe**.</span></span>
3. <span data-ttu-id="ca7de-112">Komut istemini açın ve bu dosyayı şunun gibi bir bağımsız değişkenle (sahte bir bağımsız değişken adı yeterlidir) yürütün: *ASC_AlertTest_662jfi039N.exe -foo*</span><span class="sxs-lookup"><span data-stu-id="ca7de-112">Open the command prompt and execute this file with an argument (just a fake argument name), such as: *ASC_AlertTest_662jfi039N.exe -foo*</span></span>
4. <span data-ttu-id="ca7de-113">5-10 dakika bekleyin ve Güvenlik Merkezi Uyarılarını açın.</span><span class="sxs-lookup"><span data-stu-id="ca7de-113">Wait 5 to 10 minutes and open Security Center Alerts.</span></span> <span data-ttu-id="ca7de-114">Burada şuna benzer bir uyarı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="ca7de-114">There you should find an alert similar to following one:</span></span>

    ![Uyarı Doğrulaması](./media/security-center-alert-validation/security-center-alert-validation-fig1.png)

<span data-ttu-id="ca7de-116">Bu uyarıyı gözden geçirirken, Bağımsız Değişken Denetimi Etkinleştirildi alanının doğru olarak göründüğünden emin olun.</span><span class="sxs-lookup"><span data-stu-id="ca7de-116">When reviewing this alert, make sure the field Arguments Auditing Enabled appears as true.</span></span> <span data-ttu-id="ca7de-117">Yanlış olarak görünüyorsa, komut satırı bağımsız değişkenleri denetimini etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ca7de-117">If it shows false, you need to enable command-line arguments auditing.</span></span> <span data-ttu-id="ca7de-118">Bu seçeneği şu komut satırını kullanarak etkinleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ca7de-118">You can enable this option using the following command line:</span></span>

<span data-ttu-id="ca7de-119">*reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\Audit" /f /v "ProcessCreationIncludeCmdLine_Enabled"*</span><span class="sxs-lookup"><span data-stu-id="ca7de-119">*reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\Audit" /f /v "ProcessCreationIncludeCmdLine_Enabled"*</span></span>


## <a name="see-also"></a><span data-ttu-id="ca7de-120">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="ca7de-120">See also</span></span>
<span data-ttu-id="ca7de-121">Bu makalede uyarıları doğrulama işlemine giriş yaptınız.</span><span class="sxs-lookup"><span data-stu-id="ca7de-121">This article introduced you to the alerts validation process.</span></span> <span data-ttu-id="ca7de-122">Artık bu doğrulama hakkında bilgi sahibi olduğunuza göre, aşağıdaki makaleleri deneyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ca7de-122">Now that you're familiar with this validation, try the following articles:</span></span>

* <span data-ttu-id="ca7de-123">[Azure Güvenlik Merkezi'nde güvenlik uyarılarını yönetme ve ele alma](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts).</span><span class="sxs-lookup"><span data-stu-id="ca7de-123">[Managing and responding to security alerts in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts).</span></span> <span data-ttu-id="ca7de-124">Güvenlik Merkezi’nde uyarıları yönetme ve güvenlik olaylarına yanıt vermeyi öğrenin.</span><span class="sxs-lookup"><span data-stu-id="ca7de-124">Learn how to manage alerts, and respond to security incidents in Security Center.</span></span>
* <span data-ttu-id="ca7de-125">[Azure Güvenlik Merkezi'nde güvenlik durumunu izleme](security-center-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="ca7de-125">[Security health monitoring in Azure Security Center](security-center-monitoring.md).</span></span> <span data-ttu-id="ca7de-126">Azure kaynaklarınızı durumunu izleme hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="ca7de-126">Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="ca7de-127">[Azure Güvenlik Merkezi'ndeki güvenlik uyarılarını anlama](https://docs.microsoft.com/azure/security-center/security-center-alerts-type).</span><span class="sxs-lookup"><span data-stu-id="ca7de-127">[Understanding security alerts in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-alerts-type).</span></span> <span data-ttu-id="ca7de-128">Farklı güvenlik uyarısı türleri hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="ca7de-128">Learn about the different types of security alerts.</span></span>
* <span data-ttu-id="ca7de-129">[Azure Güvenlik Merkezi Sorun Giderme Kılavuzu](https://docs.microsoft.com/azure/security-center/security-center-troubleshooting-guide).</span><span class="sxs-lookup"><span data-stu-id="ca7de-129">[Azure Security Center Troubleshooting Guide](https://docs.microsoft.com/azure/security-center/security-center-troubleshooting-guide).</span></span> <span data-ttu-id="ca7de-130">Güvenlik Merkezi’nde sık karşılaşılan sorunları gidermeyi öğrenin.</span><span class="sxs-lookup"><span data-stu-id="ca7de-130">Learn how to troubleshoot common issues in Security Center.</span></span> 
* <span data-ttu-id="ca7de-131">[Azure Güvenlik Merkezi SSS](security-center-faq.md).</span><span class="sxs-lookup"><span data-stu-id="ca7de-131">[Azure Security Center FAQ](security-center-faq.md).</span></span> <span data-ttu-id="ca7de-132">Hizmet kullanımı ile ilgili sık sorulan soruları bulun.</span><span class="sxs-lookup"><span data-stu-id="ca7de-132">Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="ca7de-133">[Azure Güvenlik Blogu](http://blogs.msdn.com/b/azuresecurity/).</span><span class="sxs-lookup"><span data-stu-id="ca7de-133">[Azure Security Blog](http://blogs.msdn.com/b/azuresecurity/).</span></span> <span data-ttu-id="ca7de-134">Azure güvenliği ve uyumluluğu ile ilgili blog yazılarını bulun.</span><span class="sxs-lookup"><span data-stu-id="ca7de-134">Find blog posts about Azure security and compliance.</span></span>

