---
title: "aaaAzure Danışmanı güvenlik önerileri | Microsoft Docs"
description: "Kullanım Azure Danışmanı toohelp Azure dağıtımlarınızı hello güvenliğini artırır."
services: advisor
documentationcenter: NA
author: kumudd
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: kumud
ms.openlocfilehash: e01ac29eb6e02bff0b1e846e320e7c36f85c7343
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="advisor-security-recommendations"></a><span data-ttu-id="c4ab6-103">Advisor güvenlik önerileri</span><span class="sxs-lookup"><span data-stu-id="c4ab6-103">Advisor Security recommendations</span></span>

<span data-ttu-id="c4ab6-104">Azure Danışmanı önerileri için tüm Azure kaynaklarına tutarlı, birleştirilmiş bir görünümünü sağlar.</span><span class="sxs-lookup"><span data-stu-id="c4ab6-104">Azure Advisor provides you with a consistent, consolidated view of recommendations for all your Azure resources.</span></span> <span data-ttu-id="c4ab6-105">Bunu Azure Güvenlik Merkezi toobring ile güvenlik önerileri tümleştirir.</span><span class="sxs-lookup"><span data-stu-id="c4ab6-105">It integrates with Azure Security Center toobring you security recommendations.</span></span> <span data-ttu-id="c4ab6-106">Merhaba güvenlik önerilerini alabilirsiniz **güvenlik** hello Danışmanı Pano sekmesinde.</span><span class="sxs-lookup"><span data-stu-id="c4ab6-106">You can get security recommendations from hello **Security** tab on hello Advisor dashboard.</span></span>

![Merhaba Danışmanı güvenliği düğmesi](./media/advisor-security-recommendations/advisor-security-tab.png)

<span data-ttu-id="c4ab6-108">Güvenlik Merkezi engellemek, algılamanıza ve Artırılmış görünürlük aracılığıyla toothreats hello Azure kaynaklarınızın güvenliğini denetlemenize yanıtlamanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="c4ab6-108">Security Center helps you prevent, detect, and respond toothreats with increased visibility into and control over hello security of your Azure resources.</span></span> <span data-ttu-id="c4ab6-109">Düzenli aralıklarla Azure kaynaklarınızın güvenlik durumunu hello analiz eder.</span><span class="sxs-lookup"><span data-stu-id="c4ab6-109">It periodically analyzes hello security state of your Azure resources.</span></span> <span data-ttu-id="c4ab6-110">Güvenlik Merkezi olası güvenlik açıklarını belirlediğinde öneriler oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c4ab6-110">When Security Center identifies potential security vulnerabilities, it creates recommendations.</span></span> <span data-ttu-id="c4ab6-111">Merhaba önerileri ihtiyacınız hello denetimlerini yapılandırma hello işleminde size kılavuzluk.</span><span class="sxs-lookup"><span data-stu-id="c4ab6-111">hello recommendations guide you through hello process of configuring hello controls you need.</span></span> 

![Merhaba Danışmanı Güvenlik sekmesi](./media/advisor-security-recommendations/advisor-security-recommendations.png)

<span data-ttu-id="c4ab6-113">Güvenlik önerileri hakkında daha fazla bilgi için bkz: [Azure Güvenlik Merkezi'nde güvenlik önerilerini yönetme](https://azure.microsoft.com/en-us/documentation/articles/security-center-recommendations/).</span><span class="sxs-lookup"><span data-stu-id="c4ab6-113">For more information about security recommendations, see [Managing security recommendations in Azure Security Center](https://azure.microsoft.com/en-us/documentation/articles/security-center-recommendations/).</span></span>

## <a name="how-tooaccess-security-recommendations-in-azure-advisor"></a><span data-ttu-id="c4ab6-114">Nasıl tooaccess Azure Danışmanı güvenlik önerileri</span><span class="sxs-lookup"><span data-stu-id="c4ab6-114">How tooaccess Security recommendations in Azure Advisor</span></span>

1. <span data-ttu-id="c4ab6-115">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c4ab6-115">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="c4ab6-116">Merhaba sol bölmede **daha fazla hizmet**.</span><span class="sxs-lookup"><span data-stu-id="c4ab6-116">In hello left pane, click **More services**.</span></span>

3. <span data-ttu-id="c4ab6-117">Hello menü bölmesi altında hizmet **izleme ve Yönetim**, tıklatın **Azure Danışmanı**.</span><span class="sxs-lookup"><span data-stu-id="c4ab6-117">In hello service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="c4ab6-118">Merhaba Danışmanı Panosu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="c4ab6-118">hello Advisor dashboard is displayed.</span></span>

4. <span data-ttu-id="c4ab6-119">Hello Danışmanı Panoda hello tıklatın **güvenlik** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="c4ab6-119">On hello Advisor dashboard, click hello **Security** tab.</span></span>

5. <span data-ttu-id="c4ab6-120">Kendisi için tooreceive önerileri istediğiniz ve ardından hello aboneliği seçin **alma önerileri**.</span><span class="sxs-lookup"><span data-stu-id="c4ab6-120">Select hello subscription for which you want tooreceive recommendations, and then click **Get recommendations**.</span></span>

> [!NOTE]
> <span data-ttu-id="c4ab6-121">tooaccess Advisor önerileri, şunları yapmalısınız ilk *aboneliğinizi kaydetmek* Danışmanı ile.</span><span class="sxs-lookup"><span data-stu-id="c4ab6-121">tooaccess Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="c4ab6-122">Bir abonelik kayıtlı olduğunda bir *abonelik sahibi* başlatır hello Danışmanı Pano ve tıklama hello **alma önerileri** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c4ab6-122">A subscription is registered when a *subscription Owner* launches hello Advisor dashboard and clicks hello **Get recommendations** button.</span></span> <span data-ttu-id="c4ab6-123">Bu bir *tek seferlik işlem*.</span><span class="sxs-lookup"><span data-stu-id="c4ab6-123">This is a *one-time operation*.</span></span> <span data-ttu-id="c4ab6-124">Merhaba abonelik kaydedildikten sonra Advisor önerileri olarak erişebilir *sahibi*, *katkıda bulunan*, veya *okuyucu* abonelik, bir kaynak grubu için veya bir belirli kaynak.</span><span class="sxs-lookup"><span data-stu-id="c4ab6-124">After hello subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c4ab6-125">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c4ab6-125">Next steps</span></span>

<span data-ttu-id="c4ab6-126">Advisor önerileri hakkında daha fazla toolearn bakın:</span><span class="sxs-lookup"><span data-stu-id="c4ab6-126">toolearn more about Advisor recommendations, see:</span></span>
* [<span data-ttu-id="c4ab6-127">Giriş tooAdvisor</span><span class="sxs-lookup"><span data-stu-id="c4ab6-127">Introduction tooAdvisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="c4ab6-128">Danışman’ı kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="c4ab6-128">Get started with Advisor</span></span>](advisor-get-started.md)
* [<span data-ttu-id="c4ab6-129">Advisor maliyet önerileri</span><span class="sxs-lookup"><span data-stu-id="c4ab6-129">Advisor Cost recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="c4ab6-130">Advisor performans önerileri</span><span class="sxs-lookup"><span data-stu-id="c4ab6-130">Advisor Performance recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="c4ab6-131">Advisor yüksek kullanılabilirlik önerileri</span><span class="sxs-lookup"><span data-stu-id="c4ab6-131">Advisor High Availability recommendations</span></span>](advisor-high-availability-recommendations.md)


 
