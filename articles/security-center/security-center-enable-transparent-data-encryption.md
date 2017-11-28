---
title: "Azure Güvenlik Merkezi'nde saydam veri şifreleme etkinleştirme | Microsoft Docs"
description: "Bu belgede Azure Güvenlik Merkezi öneriyi uygulamayı gösterilmiştir ** etkinleştirmek saydam veri şifreleme **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: e4be8a0e-2118-4ee9-a266-69e52d9f7f8e
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 2a2963affdbff3710ad08f86c6ed4e6304335559
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-transparent-data-encryption-in-azure-security-center"></a><span data-ttu-id="7af44-103">Azure Güvenlik Merkezi'nde saydam veri şifreleme etkinleştir</span><span class="sxs-lookup"><span data-stu-id="7af44-103">Enable Transparent Data Encryption in Azure Security Center</span></span>
<span data-ttu-id="7af44-104">Azure Güvenlik Merkezi TDE zaten etkin değilse SQL veritabanlarını saydam veri şifreleme (TDE) etkinleştirmek önerir.</span><span class="sxs-lookup"><span data-stu-id="7af44-104">Azure Security Center will recommend that you enable Transparent Data Encryption (TDE) on SQL databases if TDE is not already enabled.</span></span> <span data-ttu-id="7af44-105">TDE, verilerinizi korur ve veritabanınızı, ilişkili yedeklemelerinizi ve geri kalan, işlem günlüğü dosyalarını uygulamanızda değişiklik yapılması gerekmeksizin şifreleyerek uyumluluk gereksinimlerinin karşılanmasına yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="7af44-105">TDE protects your data and helps you meet compliance requirements by encrypting your database, associated backups, and transaction log files at rest, without requiring changes to your application.</span></span> <span data-ttu-id="7af44-106">Daha fazla bilgi edinmek için [saydam veri şifrelemesi ile Azure SQL veritabanı](https://msdn.microsoft.com/library/dn948096).</span><span class="sxs-lookup"><span data-stu-id="7af44-106">To learn more see [Transparent Data Encryption with Azure SQL Database](https://msdn.microsoft.com/library/dn948096).</span></span>

<span data-ttu-id="7af44-107">Bu öneri, yalnızca Azure SQL Hizmeti için geçerlidir; sanal makinelerde çalışan SQL içermez.</span><span class="sxs-lookup"><span data-stu-id="7af44-107">This recommendation applies to the Azure SQL service only; doesn't include SQL running on your virtual machines.</span></span>

> [!NOTE]
> <span data-ttu-id="7af44-108">Bu belge, örnek bir dağıtım kullanarak hizmeti tanıtır.</span><span class="sxs-lookup"><span data-stu-id="7af44-108">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="7af44-109">Bu, adım adım ilerleyen bir kılavuz değildir.</span><span class="sxs-lookup"><span data-stu-id="7af44-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="7af44-110">Öneriyi uygulamayı</span><span class="sxs-lookup"><span data-stu-id="7af44-110">Implement the recommendation</span></span>
1. <span data-ttu-id="7af44-111">İçinde **önerileri** dikey penceresinde, select **etkinleştirmek saydam veri şifreleme**.</span><span class="sxs-lookup"><span data-stu-id="7af44-111">In the **Recommendations** blade, select **Enable Transparent Data Encryption**.</span></span>
   <span data-ttu-id="7af44-112">![Saydam Veri Şifrelemesini Etkinleştirme][1]</span><span class="sxs-lookup"><span data-stu-id="7af44-112">![Enable Transparent Data Encryption][1]</span></span>
2. <span data-ttu-id="7af44-113">Bu açılır **etkinleştirmek saydam veri şifreleme SQL veritabanlarında** dikey.</span><span class="sxs-lookup"><span data-stu-id="7af44-113">This opens the **Enable Transparent Data Encryption on SQL databases** blade.</span></span> <span data-ttu-id="7af44-114">TDE etkinleştirmek için bir SQL veritabanı seçin.</span><span class="sxs-lookup"><span data-stu-id="7af44-114">Select a SQL database to enable TDE on.</span></span>
   <span data-ttu-id="7af44-115">![SQL TDE'nin etkinleştirmek için DB seçin][2]</span><span class="sxs-lookup"><span data-stu-id="7af44-115">![Select SQL DB to enable TDE on][2]</span></span>
3. <span data-ttu-id="7af44-116">Üzerinde **saydam veri şifreleme** dikey penceresinde, select **ON** veri şifreleme ve select altında **kaydetmek** dikey pencerenin üst Şeritte.</span><span class="sxs-lookup"><span data-stu-id="7af44-116">On the **Transparent data encryption** blade, select **ON** under Data encryption and select **Save** in the top ribbon of the blade.</span></span>
   <span data-ttu-id="7af44-117">![TDE üzerinde Aç][3]</span><span class="sxs-lookup"><span data-stu-id="7af44-117">![Turn on TDE][3]</span></span>

   <span data-ttu-id="7af44-118">TDE seçili SQL veritabanını etkinleştirildikten sonra **şifreleme durumu** değiştirir **şifreli**.</span><span class="sxs-lookup"><span data-stu-id="7af44-118">Once TDE is enabled on the selected SQL database, the **Encryption status** will change to **Encrypted**.</span></span>    

   ![Şifreleme durumu][4]

## <a name="see-also"></a><span data-ttu-id="7af44-120">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="7af44-120">See also</span></span>
<span data-ttu-id="7af44-121">Bu makalede "Saydam veri şifrelemeyi etkinleştirir." Güvenlik Merkezi öneriyi uygulamayı nasıl oluşturulacağını gösterir</span><span class="sxs-lookup"><span data-stu-id="7af44-121">This article showed you how to implement the Security Center recommendation "Enable Transparent Data Encryption."</span></span> <span data-ttu-id="7af44-122">SQL TDE'nin hakkında daha fazla bilgi için aşağıdakilere bakın:</span><span class="sxs-lookup"><span data-stu-id="7af44-122">To learn more about SQL TDE, see the following:</span></span>

* [<span data-ttu-id="7af44-123">Saydam veri şifrelemesi ile Azure SQL veritabanı</span><span class="sxs-lookup"><span data-stu-id="7af44-123">Transparent Data Encryption with Azure SQL Database</span></span>](https://msdn.microsoft.com/library/dn948096)
* [<span data-ttu-id="7af44-124">Saydam veri şifreleme (TDE) ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="7af44-124">Get started with Transparent Data Encryption (TDE)</span></span>](../sql-data-warehouse/sql-data-warehouse-encryption-tde.md)

<span data-ttu-id="7af44-125">Güvenlik Merkezi hakkında daha fazla bilgi edinmek için şunlara bakın:</span><span class="sxs-lookup"><span data-stu-id="7af44-125">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="7af44-126">[Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md) -- Azure abonelikleriniz ve kaynak gruplarınız için güvenlik ilkelerini yapılandırma hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="7af44-126">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="7af44-127">[Azure Güvenlik Merkezi'nde güvenlik önerilerini yönetme](security-center-recommendations.md) --nasıl önerilerin Azure kaynaklarınızı korumanıza yardımcı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="7af44-127">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="7af44-128">[Azure Güvenlik Merkezi'nde güvenlik durumunu izleme](security-center-monitoring.md) --Azure kaynaklarınızı sağlığını izlemek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="7af44-128">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="7af44-129">[Azure Güvenlik Merkezi'nde güvenlik uyarılarını yönetme ve yanıtlama](security-center-managing-and-responding-alerts.md) -- Güvenlik uyarılarını yönetme ve yanıtlama hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="7af44-129">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="7af44-130">[Azure Güvenlik Merkezi ile iş ortağı çözümlerini izleme](security-center-partner-solutions.md) - İş ortağı çözümlerinizin sistem durumunu nasıl izleyeceğiniz hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="7af44-130">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="7af44-131">[Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) -- Hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7af44-131">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="7af44-132">[Azure güvenlik blogu](http://blogs.msdn.com/b/azuresecurity/) --en son Azure güvenlik haberlerini ve bilgilerini edinin.</span><span class="sxs-lookup"><span data-stu-id="7af44-132">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-tde-on-sql-databases/enable-tde.png
[2]:./media/security-center-enable-tde-on-sql-databases/transparent-data-encryption-blade.png
[3]: ./media/security-center-enable-tde-on-sql-databases/turn-on-tde.png
[4]: ./media/security-center-enable-tde-on-sql-databases/encrypted.png
