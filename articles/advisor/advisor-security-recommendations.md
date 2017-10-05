---
title: "Azure Danışmanı güvenlik önerileri | Microsoft Docs"
description: "Azure dağıtımlarınızın güvenliğini artırmanıza yardımcı olmak için Azure Danışmanı'nı kullanın."
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
ms.openlocfilehash: 53be05593c3733ccb27979a3a026414013125779
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="advisor-security-recommendations"></a><span data-ttu-id="a1ef6-103">Advisor güvenlik önerileri</span><span class="sxs-lookup"><span data-stu-id="a1ef6-103">Advisor Security recommendations</span></span>

<span data-ttu-id="a1ef6-104">Azure Danışmanı önerileri için tüm Azure kaynaklarına tutarlı, birleştirilmiş bir görünümünü sağlar.</span><span class="sxs-lookup"><span data-stu-id="a1ef6-104">Azure Advisor provides you with a consistent, consolidated view of recommendations for all your Azure resources.</span></span> <span data-ttu-id="a1ef6-105">Güvenlik önerileri getirmek için Azure Güvenlik Merkezi ile tümleşir.</span><span class="sxs-lookup"><span data-stu-id="a1ef6-105">It integrates with Azure Security Center to bring you security recommendations.</span></span> <span data-ttu-id="a1ef6-106">Güvenlik önerilerini alabilirsiniz **güvenlik** Danışmanı Pano sekmesinde.</span><span class="sxs-lookup"><span data-stu-id="a1ef6-106">You can get security recommendations from the **Security** tab on the Advisor dashboard.</span></span>

![Advisor güvenliği düğmesi](./media/advisor-security-recommendations/advisor-security-tab.png)

<span data-ttu-id="a1ef6-108">Güvenlik Merkezi, artırılmış görünürlük aracılığıyla tehditleri engellemenize, algılamanıza ve yanıtlamanıza, ayrıca Azure kaynaklarınızın güvenliğini denetlemenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="a1ef6-108">Security Center helps you prevent, detect, and respond to threats with increased visibility into and control over the security of your Azure resources.</span></span> <span data-ttu-id="a1ef6-109">Düzenli aralıklarla Azure kaynaklarınızın güvenlik durumunu analiz eder.</span><span class="sxs-lookup"><span data-stu-id="a1ef6-109">It periodically analyzes the security state of your Azure resources.</span></span> <span data-ttu-id="a1ef6-110">Güvenlik Merkezi olası güvenlik açıklarını belirlediğinde öneriler oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a1ef6-110">When Security Center identifies potential security vulnerabilities, it creates recommendations.</span></span> <span data-ttu-id="a1ef6-111">Öneriler gereksinim denetimlerini yapılandırma işleminde size kılavuzluk.</span><span class="sxs-lookup"><span data-stu-id="a1ef6-111">The recommendations guide you through the process of configuring the controls you need.</span></span> 

![Advisor Güvenlik sekmesi](./media/advisor-security-recommendations/advisor-security-recommendations.png)

<span data-ttu-id="a1ef6-113">Güvenlik önerileri hakkında daha fazla bilgi için bkz: [Azure Güvenlik Merkezi'nde güvenlik önerilerini yönetme](https://azure.microsoft.com/en-us/documentation/articles/security-center-recommendations/).</span><span class="sxs-lookup"><span data-stu-id="a1ef6-113">For more information about security recommendations, see [Managing security recommendations in Azure Security Center](https://azure.microsoft.com/en-us/documentation/articles/security-center-recommendations/).</span></span>

## <a name="how-to-access-security-recommendations-in-azure-advisor"></a><span data-ttu-id="a1ef6-114">Güvenlik önerileri Azure Danışmanı erişme</span><span class="sxs-lookup"><span data-stu-id="a1ef6-114">How to access Security recommendations in Azure Advisor</span></span>

1. <span data-ttu-id="a1ef6-115">[Azure Portal](https://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="a1ef6-115">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="a1ef6-116">Sol bölmede **daha fazla hizmet**.</span><span class="sxs-lookup"><span data-stu-id="a1ef6-116">In the left pane, click **More services**.</span></span>

3. <span data-ttu-id="a1ef6-117">Hizmet menü bölmesinde altında **izleme ve Yönetim**, tıklatın **Azure Danışmanı**.</span><span class="sxs-lookup"><span data-stu-id="a1ef6-117">In the service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="a1ef6-118">Advisor Panosu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="a1ef6-118">The Advisor dashboard is displayed.</span></span>

4. <span data-ttu-id="a1ef6-119">Advisor Panoda tıklatın **güvenlik** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="a1ef6-119">On the Advisor dashboard, click the **Security** tab.</span></span>

5. <span data-ttu-id="a1ef6-120">Önerileri almak ve ardından istediğiniz aboneliği seçin **alma önerileri**.</span><span class="sxs-lookup"><span data-stu-id="a1ef6-120">Select the subscription for which you want to receive recommendations, and then click **Get recommendations**.</span></span>

> [!NOTE]
> <span data-ttu-id="a1ef6-121">Advisor önerileri erişmek için öncelikle *aboneliğinizi kaydetmek* Danışmanı ile.</span><span class="sxs-lookup"><span data-stu-id="a1ef6-121">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="a1ef6-122">Bir abonelik kayıtlı olduğunda bir *abonelik sahibi* Danışmanı Pano başlatır ve tıkladığında **alma önerileri** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a1ef6-122">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span></span> <span data-ttu-id="a1ef6-123">Bu bir *tek seferlik işlem*.</span><span class="sxs-lookup"><span data-stu-id="a1ef6-123">This is a *one-time operation*.</span></span> <span data-ttu-id="a1ef6-124">Abonelik kaydedildikten sonra Advisor önerileri olarak erişebilir *sahibi*, *katkıda bulunan*, veya *okuyucu* bir abonelik, bir kaynak grubu ya da belirli bir kaynak için.</span><span class="sxs-lookup"><span data-stu-id="a1ef6-124">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a1ef6-125">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a1ef6-125">Next steps</span></span>

<span data-ttu-id="a1ef6-126">Advisor önerileri hakkında daha fazla bilgi için bkz:</span><span class="sxs-lookup"><span data-stu-id="a1ef6-126">To learn more about Advisor recommendations, see:</span></span>
* [<span data-ttu-id="a1ef6-127">Advisor giriş</span><span class="sxs-lookup"><span data-stu-id="a1ef6-127">Introduction to Advisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="a1ef6-128">Danışman’ı kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="a1ef6-128">Get started with Advisor</span></span>](advisor-get-started.md)
* [<span data-ttu-id="a1ef6-129">Advisor maliyet önerileri</span><span class="sxs-lookup"><span data-stu-id="a1ef6-129">Advisor Cost recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="a1ef6-130">Advisor performans önerileri</span><span class="sxs-lookup"><span data-stu-id="a1ef6-130">Advisor Performance recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="a1ef6-131">Advisor yüksek kullanılabilirlik önerileri</span><span class="sxs-lookup"><span data-stu-id="a1ef6-131">Advisor High Availability recommendations</span></span>](advisor-high-availability-recommendations.md)


 
