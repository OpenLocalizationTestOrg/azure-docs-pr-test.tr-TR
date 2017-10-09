---
title: "Azure Güvenlik Merkezi'nde saydam veri şifreleme aaaEnable | Microsoft Docs"
description: "Bu belge size nasıl tooimplement hello Azure Güvenlik Merkezi öneri gösterir. ** etkinleştirmek saydam veri şifreleme **."
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
ms.openlocfilehash: 94c6e9a1feddaa48faac6c835d416c4d131cd5c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-transparent-data-encryption-in-azure-security-center"></a><span data-ttu-id="0f63e-103">Azure Güvenlik Merkezi'nde saydam veri şifreleme etkinleştir</span><span class="sxs-lookup"><span data-stu-id="0f63e-103">Enable Transparent Data Encryption in Azure Security Center</span></span>
<span data-ttu-id="0f63e-104">Azure Güvenlik Merkezi TDE zaten etkin değilse SQL veritabanlarını saydam veri şifreleme (TDE) etkinleştirmek önerir.</span><span class="sxs-lookup"><span data-stu-id="0f63e-104">Azure Security Center will recommend that you enable Transparent Data Encryption (TDE) on SQL databases if TDE is not already enabled.</span></span> <span data-ttu-id="0f63e-105">TDE, verilerinizi korur ve veritabanınızı, ilişkili yedeklemelerinizi ve geri kalan, işlem günlüğü dosyalarını değişiklikleri tooyour uygulama gerek kalmadan şifreleyerek uyumluluk gereksinimlerinin karşılanmasına yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="0f63e-105">TDE protects your data and helps you meet compliance requirements by encrypting your database, associated backups, and transaction log files at rest, without requiring changes tooyour application.</span></span> <span data-ttu-id="0f63e-106">toolearn daha fazla [saydam veri şifrelemesi ile Azure SQL veritabanı](https://msdn.microsoft.com/library/dn948096).</span><span class="sxs-lookup"><span data-stu-id="0f63e-106">toolearn more see [Transparent Data Encryption with Azure SQL Database](https://msdn.microsoft.com/library/dn948096).</span></span>

<span data-ttu-id="0f63e-107">Bu öneri toohello yalnızca Azure SQL Hizmeti uygulanır; sanal makinelerde çalışan SQL içermez.</span><span class="sxs-lookup"><span data-stu-id="0f63e-107">This recommendation applies toohello Azure SQL service only; doesn't include SQL running on your virtual machines.</span></span>

> [!NOTE]
> <span data-ttu-id="0f63e-108">Bu belge, örnek bir dağıtım kullanarak hello hizmeti sunar.</span><span class="sxs-lookup"><span data-stu-id="0f63e-108">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="0f63e-109">Bu, adım adım ilerleyen bir kılavuz değildir.</span><span class="sxs-lookup"><span data-stu-id="0f63e-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="0f63e-110">Merhaba öneriyi uygulamayı</span><span class="sxs-lookup"><span data-stu-id="0f63e-110">Implement hello recommendation</span></span>
1. <span data-ttu-id="0f63e-111">Merhaba, **önerileri** dikey penceresinde, select **etkinleştirmek saydam veri şifreleme**.</span><span class="sxs-lookup"><span data-stu-id="0f63e-111">In hello **Recommendations** blade, select **Enable Transparent Data Encryption**.</span></span>
   <span data-ttu-id="0f63e-112">![Saydam Veri Şifrelemesini Etkinleştirme][1]</span><span class="sxs-lookup"><span data-stu-id="0f63e-112">![Enable Transparent Data Encryption][1]</span></span>
2. <span data-ttu-id="0f63e-113">Merhaba açılır **etkinleştirmek saydam veri şifreleme SQL veritabanlarında** dikey.</span><span class="sxs-lookup"><span data-stu-id="0f63e-113">This opens hello **Enable Transparent Data Encryption on SQL databases** blade.</span></span> <span data-ttu-id="0f63e-114">Bir SQL veritabanı tooenable TDE seçin.</span><span class="sxs-lookup"><span data-stu-id="0f63e-114">Select a SQL database tooenable TDE on.</span></span>
   <span data-ttu-id="0f63e-115">![SQL DB tooenable TDE seçin][2]</span><span class="sxs-lookup"><span data-stu-id="0f63e-115">![Select SQL DB tooenable TDE on][2]</span></span>
3. <span data-ttu-id="0f63e-116">Merhaba üzerinde **saydam veri şifreleme** dikey penceresinde, select **ON** veri şifreleme ve select altında **kaydetmek** hello dikey pencerenin üst hello Şeritte.</span><span class="sxs-lookup"><span data-stu-id="0f63e-116">On hello **Transparent data encryption** blade, select **ON** under Data encryption and select **Save** in hello top ribbon of hello blade.</span></span>
   <span data-ttu-id="0f63e-117">![TDE üzerinde Aç][3]</span><span class="sxs-lookup"><span data-stu-id="0f63e-117">![Turn on TDE][3]</span></span>

   <span data-ttu-id="0f63e-118">TDE etkinleştirildiğinde hello SQL veritabanı hello seçili **şifreleme durumu** çok değiştirecek**şifreli**.</span><span class="sxs-lookup"><span data-stu-id="0f63e-118">Once TDE is enabled on hello selected SQL database, hello **Encryption status** will change too**Encrypted**.</span></span>    

   ![Şifreleme durumu][4]

## <a name="see-also"></a><span data-ttu-id="0f63e-120">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="0f63e-120">See also</span></span>
<span data-ttu-id="0f63e-121">Bu makalede, nasıl tooimplement hello Güvenlik Merkezi öneri "Etkinleştirme saydam veri şifreleme." gösterdi.</span><span class="sxs-lookup"><span data-stu-id="0f63e-121">This article showed you how tooimplement hello Security Center recommendation "Enable Transparent Data Encryption."</span></span> <span data-ttu-id="0f63e-122">SQL TDE'nin hakkında daha fazla toolearn hello aşağıdaki bakın:</span><span class="sxs-lookup"><span data-stu-id="0f63e-122">toolearn more about SQL TDE, see hello following:</span></span>

* [<span data-ttu-id="0f63e-123">Saydam veri şifrelemesi ile Azure SQL veritabanı</span><span class="sxs-lookup"><span data-stu-id="0f63e-123">Transparent Data Encryption with Azure SQL Database</span></span>](https://msdn.microsoft.com/library/dn948096)
* [<span data-ttu-id="0f63e-124">Saydam veri şifreleme (TDE) ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="0f63e-124">Get started with Transparent Data Encryption (TDE)</span></span>](../sql-data-warehouse/sql-data-warehouse-encryption-tde.md)

<span data-ttu-id="0f63e-125">Güvenlik Merkezi hakkında daha fazla toolearn hello aşağıdaki bakın:</span><span class="sxs-lookup"><span data-stu-id="0f63e-125">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="0f63e-126">[Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md) --öğrenin nasıl tooconfigure Azure Abonelikleriniz ve kaynak grupları için güvenlik ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="0f63e-126">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="0f63e-127">[Azure Güvenlik Merkezi'nde güvenlik önerilerini yönetme](security-center-recommendations.md) --nasıl önerilerin Azure kaynaklarınızı korumanıza yardımcı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="0f63e-127">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="0f63e-128">[Azure Güvenlik Merkezi'nde güvenlik durumunu izleme](security-center-monitoring.md) --nasıl toomonitor hello Azure kaynaklarınızın sistem durumunu öğrenin.</span><span class="sxs-lookup"><span data-stu-id="0f63e-128">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="0f63e-129">[Azure Güvenlik Merkezi'nde Uyarıları yönetme ve yanıt toosecurity](security-center-managing-and-responding-alerts.md) --öğrenin nasıl toomanage ve yanıt toosecurity uyarıları.</span><span class="sxs-lookup"><span data-stu-id="0f63e-129">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="0f63e-130">[Azure Güvenlik Merkezi ile iş ortağı çözümlerini izleme](security-center-partner-solutions.md) --nasıl toomonitor hello iş ortağı çözümlerinizin sistem durumunu öğrenin.</span><span class="sxs-lookup"><span data-stu-id="0f63e-130">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="0f63e-131">[Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) --hello hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0f63e-131">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="0f63e-132">[Azure güvenlik blogu](http://blogs.msdn.com/b/azuresecurity/) --hello en son Azure güvenlik haberlerini ve bilgilerini alın.</span><span class="sxs-lookup"><span data-stu-id="0f63e-132">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-tde-on-sql-databases/enable-tde.png
[2]:./media/security-center-enable-tde-on-sql-databases/transparent-data-encryption-blade.png
[3]: ./media/security-center-enable-tde-on-sql-databases/turn-on-tde.png
[4]: ./media/security-center-enable-tde-on-sql-databases/encrypted.png
