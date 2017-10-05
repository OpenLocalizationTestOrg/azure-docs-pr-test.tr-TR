---
title: "Azure Güvenlik Merkezi'nde depolama hesabı için şifrelemeyi etkinleştirme | Microsoft Docs"
description: "Bu belgede Azure Güvenlik Merkezi önerileri uygulamak gösterilmiştir ** şifreleme için Azure depolama hesabı ** etkinleştirin."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/20/2016
ms.author: terrylan
ms.openlocfilehash: b7b2e8a12cbab68da9c8fcc348e8e3c543607007
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="enable-encryption-for-azure-storage-account-in-azure-security-center"></a><span data-ttu-id="a5b4e-103">Azure Güvenlik Merkezi'nde Azure depolama hesabı için şifrelemeyi etkinleştir</span><span class="sxs-lookup"><span data-stu-id="a5b4e-103">Enable encryption for Azure storage account in Azure Security Center</span></span>
<span data-ttu-id="a5b4e-104">Azure Güvenlik Merkezi, Azure depolama hizmeti şifrelemesi bekleyen veri için etkinleştirmenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-104">Azure Security Center may recommend that you enable Azure Storage Service Encryption for data at rest.</span></span>

<span data-ttu-id="a5b4e-105">Azure depolama birimine yazıldığında verileri şifrelemek ve alma önce verilerin şifresini çözmek depolama hizmeti şifreleme (SSE) çalışır.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-105">Storage Service Encryption (SSE) works by encrypting the data when it is written to Azure storage and decrypting the data before retrieval.</span></span>  <span data-ttu-id="a5b4e-106">SSE yalnızca Azure Blob hizmeti için şu anda kullanılabilir değil ve blok blobları, sayfa bloblarını kullanılabilir ve ekleme blobları.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-106">SSE is currently available only for the Azure Blob service and can be used for block blobs, page blobs, and append blobs.</span></span>  <span data-ttu-id="a5b4e-107">Daha fazla bilgi için bkz: [bekleyen veri için depolama hizmeti şifrelemesi](../storage/common/storage-service-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="a5b4e-107">To learn more, see [Storage Service Encryption for data at rest](../storage/common/storage-service-encryption.md).</span></span>


> [!Note]
> <span data-ttu-id="a5b4e-108">Şifreleme etkinleştirdikten sonra yalnızca yeni veri şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-108">After enabling encryption, only new data is encrypted.</span></span> <span data-ttu-id="a5b4e-109">Varolan BLOB storage hesabınızdaki şifrelenmemiş kalır.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-109">Any existing blobs in your storage account remain unencrypted.</span></span> <span data-ttu-id="a5b4e-110">Mevcut BLOB'ları şifrelemek için bkz: [depolama hizmeti şifrelemesi SSS](../storage/common/storage-service-encryption.md#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest).</span><span class="sxs-lookup"><span data-stu-id="a5b4e-110">To encrypt existing blobs, see the [Storage Service Encryption FAQ](../storage/common/storage-service-encryption.md#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest).</span></span>
>
>

<span data-ttu-id="a5b4e-111">Depolama hizmeti şifreleme yalnızca Resource Manager depolama hesaplarında desteklenir.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-111">Storage Service Encryption is only supported on Resource Manager storage accounts.</span></span> <span data-ttu-id="a5b4e-112">Klasik depolama hesapları şu anda desteklenmemektedir.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-112">Classic storage accounts are not currently supported.</span></span> <span data-ttu-id="a5b4e-113">Klasik ve Resource Manager dağıtım modellerinde anlamak için bkz: [Azure dağıtım modelleri](../azure-classic-rm.md).</span><span class="sxs-lookup"><span data-stu-id="a5b4e-113">To understand the classic and Resource Manager deployment models, see [Azure deployment models](../azure-classic-rm.md).</span></span>

> [!NOTE]
> <span data-ttu-id="a5b4e-114">Bu belge, örnek bir dağıtım kullanarak hizmeti tanıtır.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-114">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="a5b4e-115">Bu belge hakkında adım adım kılavuz değildir.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-115">This document is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="a5b4e-116">Öneriyi uygulamayı</span><span class="sxs-lookup"><span data-stu-id="a5b4e-116">Implement the recommendation</span></span>
1. <span data-ttu-id="a5b4e-117">İçinde **önerileri** dikey penceresinde, select **etkinleştirmek Azure depolama hesabı için şifreleme**.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-117">In the **Recommendations** blade, select **Enable encryption for Azure Storage Account**.</span></span>
   <span data-ttu-id="a5b4e-118">![Depolama hesabı için şifrelemeyi etkinleştirme][1]</span><span class="sxs-lookup"><span data-stu-id="a5b4e-118">![Enable encryption for storage account][1]</span></span>
2. <span data-ttu-id="a5b4e-119">**Etkinleştirmek depolama şifreleme** dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-119">The **Enable storage encryption** blade opens.</span></span> <span data-ttu-id="a5b4e-120">Bu dikey burada depolama şifreleme devre dışı Azure depolama hesaplarını listeler.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-120">This blade lists the Azure storage accounts where storage encryption is disabled.</span></span> <span data-ttu-id="a5b4e-121">Bu örnekte, şimdi seçin **storageacct1**.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-121">In this example, let's select **storageacct1**.</span></span>
   <span data-ttu-id="a5b4e-122">![Depolama şifrelemeyi etkinleştir][2]</span><span class="sxs-lookup"><span data-stu-id="a5b4e-122">![Enable storage encryption][2]</span></span>
3. <span data-ttu-id="a5b4e-123">**Şifreleme** dikey **storageacct1** açar.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-123">The **Encryption** blade for **storageacct1** opens.</span></span> <span data-ttu-id="a5b4e-124">Seçin **etkin**.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-124">Select **Enabled**.</span></span>
   <span data-ttu-id="a5b4e-125">![Şifreleme dikey penceresi][3]</span><span class="sxs-lookup"><span data-stu-id="a5b4e-125">![Encryption blade][3]</span></span>
4. <span data-ttu-id="a5b4e-126">**Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-126">Select **Save**.</span></span>

<span data-ttu-id="a5b4e-127">Depolama şifrelemesi için şimdi etkinleştirdiğiniz **storageacct1**.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-127">You have now enabled storage encryption for **storageacct1**.</span></span>


## <a name="see-also"></a><span data-ttu-id="a5b4e-128">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-128">See also</span></span>
<span data-ttu-id="a5b4e-129">Bu belgede "Azure depolama hesabı için şifrelemeyi etkinleştirir." Güvenlik Merkezi öneriyi uygulamayı nasıl oluşturulacağını gösterir</span><span class="sxs-lookup"><span data-stu-id="a5b4e-129">This document showed you how to implement the Security Center recommendation "Enable encryption for Azure Storage Account."</span></span> <span data-ttu-id="a5b4e-130">Azure depolama hizmeti şifrelemesi hakkında daha fazla bilgi için aşağıdakilere bakın:</span><span class="sxs-lookup"><span data-stu-id="a5b4e-130">To learn more about Azure Storage Service Encryption, see the following:</span></span>

* [<span data-ttu-id="a5b4e-131">Rest verileri için Azure Storage hizmeti şifreleme</span><span class="sxs-lookup"><span data-stu-id="a5b4e-131">Azure Storage Service Encryption for Data at Rest</span></span>](../storage/common/storage-service-encryption.md)

<span data-ttu-id="a5b4e-132">Güvenlik Merkezi hakkında daha fazla bilgi edinmek için şunlara bakın:</span><span class="sxs-lookup"><span data-stu-id="a5b4e-132">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="a5b4e-133">[Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md) -Azure Abonelikleriniz ve kaynak grupları için güvenlik ilkeleri yapılandırmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-133">[Setting security policies in Azure Security Center](security-center-policies.md) - Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="a5b4e-134">[Azure Güvenlik Merkezi'nde güvenlik durumunu izleme](security-center-monitoring.md) -Azure kaynaklarınızın sistem durumunu izlemek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-134">[Security health monitoring in Azure Security Center](security-center-monitoring.md) - Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="a5b4e-135">[Yönetme ve Azure Güvenlik Merkezi'nde güvenlik uyarılarını yanıtlama](security-center-managing-and-responding-alerts.md) -yönetme ve güvenlik uyarılarını yanıtlama hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-135">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) - Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="a5b4e-136">[Azure Güvenlik Merkezi'nde güvenlik önerilerini yönetme](security-center-recommendations.md) -önerilerin Azure kaynaklarınızı korumanıza nasıl yardımcı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-136">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) - Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="a5b4e-137">[Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) -hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-137">[Azure Security Center FAQ](security-center-faq.md) - Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="a5b4e-138">[Azure güvenlik blogu](http://blogs.msdn.com/b/azuresecurity/) -Azure güvenliği ve uyumluluğu ile ilgili blog yazılarını bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a5b4e-138">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) - Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-encryption-for-storage-account/enable-encryption-for-storage-account.png
[2]: ./media/security-center-enable-encryption-for-storage-account/enable-storage-encryption.png
[3]: ./media/security-center-enable-encryption-for-storage-account/encryption-blade.png
