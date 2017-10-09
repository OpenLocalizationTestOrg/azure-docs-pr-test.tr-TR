---
title: "Azure Güvenlik Merkezi'nde depolama hesabı için aaaEnable şifreleme | Microsoft Docs"
description: "Bu belge size nasıl tooimplement hello Azure Güvenlik Merkezi önerilerini gösterir. ** şifreleme için Azure depolama hesabı ** etkinleştirin."
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
ms.openlocfilehash: c5cbafbf3a8be86f213dcf1c0c0ddcc0222b3d95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-encryption-for-azure-storage-account-in-azure-security-center"></a><span data-ttu-id="bae36-103">Azure Güvenlik Merkezi'nde Azure depolama hesabı için şifrelemeyi etkinleştir</span><span class="sxs-lookup"><span data-stu-id="bae36-103">Enable encryption for Azure storage account in Azure Security Center</span></span>
<span data-ttu-id="bae36-104">Azure Güvenlik Merkezi, Azure depolama hizmeti şifrelemesi bekleyen veri için etkinleştirmenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="bae36-104">Azure Security Center may recommend that you enable Azure Storage Service Encryption for data at rest.</span></span>

<span data-ttu-id="bae36-105">Depolama hizmeti şifreleme (SSE) tooAzure depolama yazıldığında hello verileri şifrelemek ve alma önce hello verilerin şifresini çözmek çalışır.</span><span class="sxs-lookup"><span data-stu-id="bae36-105">Storage Service Encryption (SSE) works by encrypting hello data when it is written tooAzure storage and decrypting hello data before retrieval.</span></span>  <span data-ttu-id="bae36-106">SSE yalnızca hello Azure Blob hizmeti şu anda kullanılabilir değil ve blok blobları, sayfa bloblarını kullanılabilir ve ekleme blobları.</span><span class="sxs-lookup"><span data-stu-id="bae36-106">SSE is currently available only for hello Azure Blob service and can be used for block blobs, page blobs, and append blobs.</span></span>  <span data-ttu-id="bae36-107">toolearn daha, fazla [bekleyen veri için depolama hizmeti şifrelemesi](../storage/common/storage-service-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="bae36-107">toolearn more, see [Storage Service Encryption for data at rest](../storage/common/storage-service-encryption.md).</span></span>


> [!Note]
> <span data-ttu-id="bae36-108">Şifreleme etkinleştirdikten sonra yalnızca yeni veri şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="bae36-108">After enabling encryption, only new data is encrypted.</span></span> <span data-ttu-id="bae36-109">Varolan BLOB storage hesabınızdaki şifrelenmemiş kalır.</span><span class="sxs-lookup"><span data-stu-id="bae36-109">Any existing blobs in your storage account remain unencrypted.</span></span> <span data-ttu-id="bae36-110">tooencrypt varolan BLOB'lar, bkz: Merhaba [depolama hizmeti şifrelemesi SSS](../storage/common/storage-service-encryption.md#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest).</span><span class="sxs-lookup"><span data-stu-id="bae36-110">tooencrypt existing blobs, see hello [Storage Service Encryption FAQ](../storage/common/storage-service-encryption.md#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest).</span></span>
>
>

<span data-ttu-id="bae36-111">Depolama hizmeti şifreleme yalnızca Resource Manager depolama hesaplarında desteklenir.</span><span class="sxs-lookup"><span data-stu-id="bae36-111">Storage Service Encryption is only supported on Resource Manager storage accounts.</span></span> <span data-ttu-id="bae36-112">Klasik depolama hesapları şu anda desteklenmemektedir.</span><span class="sxs-lookup"><span data-stu-id="bae36-112">Classic storage accounts are not currently supported.</span></span> <span data-ttu-id="bae36-113">toounderstand hello Klasik ve Resource Manager dağıtım modellerinde bkz [Azure dağıtım modelleri](../azure-classic-rm.md).</span><span class="sxs-lookup"><span data-stu-id="bae36-113">toounderstand hello classic and Resource Manager deployment models, see [Azure deployment models](../azure-classic-rm.md).</span></span>

> [!NOTE]
> <span data-ttu-id="bae36-114">Bu belge, örnek bir dağıtım kullanarak hello hizmeti sunar.</span><span class="sxs-lookup"><span data-stu-id="bae36-114">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="bae36-115">Bu belge hakkında adım adım kılavuz değildir.</span><span class="sxs-lookup"><span data-stu-id="bae36-115">This document is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="bae36-116">Merhaba öneriyi uygulamayı</span><span class="sxs-lookup"><span data-stu-id="bae36-116">Implement hello recommendation</span></span>
1. <span data-ttu-id="bae36-117">Merhaba, **önerileri** dikey penceresinde, select **etkinleştirmek Azure depolama hesabı için şifreleme**.</span><span class="sxs-lookup"><span data-stu-id="bae36-117">In hello **Recommendations** blade, select **Enable encryption for Azure Storage Account**.</span></span>
   <span data-ttu-id="bae36-118">![Depolama hesabı için şifrelemeyi etkinleştirme][1]</span><span class="sxs-lookup"><span data-stu-id="bae36-118">![Enable encryption for storage account][1]</span></span>
2. <span data-ttu-id="bae36-119">Merhaba **etkinleştirmek depolama şifreleme** dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="bae36-119">hello **Enable storage encryption** blade opens.</span></span> <span data-ttu-id="bae36-120">Bu dikey burada depolama şifreleme devre dışı hello Azure depolama hesaplarını listeler.</span><span class="sxs-lookup"><span data-stu-id="bae36-120">This blade lists hello Azure storage accounts where storage encryption is disabled.</span></span> <span data-ttu-id="bae36-121">Bu örnekte, şimdi seçin **storageacct1**.</span><span class="sxs-lookup"><span data-stu-id="bae36-121">In this example, let's select **storageacct1**.</span></span>
   <span data-ttu-id="bae36-122">![Depolama şifrelemeyi etkinleştir][2]</span><span class="sxs-lookup"><span data-stu-id="bae36-122">![Enable storage encryption][2]</span></span>
3. <span data-ttu-id="bae36-123">Merhaba **şifreleme** dikey **storageacct1** açar.</span><span class="sxs-lookup"><span data-stu-id="bae36-123">hello **Encryption** blade for **storageacct1** opens.</span></span> <span data-ttu-id="bae36-124">Seçin **etkin**.</span><span class="sxs-lookup"><span data-stu-id="bae36-124">Select **Enabled**.</span></span>
   <span data-ttu-id="bae36-125">![Şifreleme dikey penceresi][3]</span><span class="sxs-lookup"><span data-stu-id="bae36-125">![Encryption blade][3]</span></span>
4. <span data-ttu-id="bae36-126">**Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="bae36-126">Select **Save**.</span></span>

<span data-ttu-id="bae36-127">Depolama şifrelemesi için şimdi etkinleştirdiğiniz **storageacct1**.</span><span class="sxs-lookup"><span data-stu-id="bae36-127">You have now enabled storage encryption for **storageacct1**.</span></span>


## <a name="see-also"></a><span data-ttu-id="bae36-128">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="bae36-128">See also</span></span>
<span data-ttu-id="bae36-129">Bu belge size nasıl tooimplement hello Güvenlik Merkezi öneri "etkinleştirmek için şifreleme Azure depolama hesabı." gösterdi.</span><span class="sxs-lookup"><span data-stu-id="bae36-129">This document showed you how tooimplement hello Security Center recommendation "Enable encryption for Azure Storage Account."</span></span> <span data-ttu-id="bae36-130">Azure depolama hizmeti şifrelemesi hakkında daha fazla toolearn hello aşağıdaki bakın:</span><span class="sxs-lookup"><span data-stu-id="bae36-130">toolearn more about Azure Storage Service Encryption, see hello following:</span></span>

* [<span data-ttu-id="bae36-131">Rest verileri için Azure Storage hizmeti şifreleme</span><span class="sxs-lookup"><span data-stu-id="bae36-131">Azure Storage Service Encryption for Data at Rest</span></span>](../storage/common/storage-service-encryption.md)

<span data-ttu-id="bae36-132">Güvenlik Merkezi hakkında daha fazla toolearn hello aşağıdaki bakın:</span><span class="sxs-lookup"><span data-stu-id="bae36-132">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="bae36-133">[Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md) -öğrenin nasıl tooconfigure Azure Abonelikleriniz ve kaynak grupları için güvenlik ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="bae36-133">[Setting security policies in Azure Security Center](security-center-policies.md) - Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="bae36-134">[Azure Güvenlik Merkezi'nde güvenlik durumunu izleme](security-center-monitoring.md) -nasıl toomonitor hello Azure kaynaklarınızın sistem durumunu öğrenin.</span><span class="sxs-lookup"><span data-stu-id="bae36-134">[Security health monitoring in Azure Security Center](security-center-monitoring.md) - Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="bae36-135">[Azure Güvenlik Merkezi'nde Uyarıları yönetme ve yanıt toosecurity](security-center-managing-and-responding-alerts.md) -öğrenin nasıl toomanage ve yanıt toosecurity uyarıları.</span><span class="sxs-lookup"><span data-stu-id="bae36-135">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) - Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="bae36-136">[Azure Güvenlik Merkezi'nde güvenlik önerilerini yönetme](security-center-recommendations.md) -önerilerin Azure kaynaklarınızı korumanıza nasıl yardımcı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="bae36-136">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) - Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="bae36-137">[Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) -hello hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bae36-137">[Azure Security Center FAQ](security-center-faq.md) - Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="bae36-138">[Azure güvenlik blogu](http://blogs.msdn.com/b/azuresecurity/) -Azure güvenliği ve uyumluluğu ile ilgili blog yazılarını bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bae36-138">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) - Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-encryption-for-storage-account/enable-encryption-for-storage-account.png
[2]: ./media/security-center-enable-encryption-for-storage-account/enable-storage-encryption.png
[3]: ./media/security-center-enable-encryption-for-storage-account/encryption-blade.png
