---
title: "Azure Güvenlik Merkezi'nde güvenlik kişi ayrıntıları aaaProvide | Microsoft Docs"
description: "Bu belgede nasıl tooprovide güvenlik iletişim ayrıntıları Azure Güvenlik Merkezi'nde gösterilir."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 26b5dcb4-ce3f-4f22-8d56-d2bf743cfc90
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 6c378c9c84c6e4fce70b2541e4cc121018700269
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="provide-security-contact-details-in-azure-security-center"></a><span data-ttu-id="dc6c7-103">Azure Güvenlik Merkezi'nde güvenlik iletişim ayrıntılarını sağlayın</span><span class="sxs-lookup"><span data-stu-id="dc6c7-103">Provide security contact details in Azure Security Center</span></span>
<span data-ttu-id="dc6c7-104">Azure Güvenlik Merkezi, henüz yapmadıysanız, Azure aboneliğiniz için güvenlik iletişim ayrıntılarını sağlayın önerir.</span><span class="sxs-lookup"><span data-stu-id="dc6c7-104">Azure Security Center will recommend that you provide security contact details for your Azure subscription if you haven’t already.</span></span> <span data-ttu-id="dc6c7-105">Bu bilgiler Microsoft toocontact tarafından kullanılır, hello Microsoft Güvenlik Yanıt Merkezi (MSRC) müşteri verilerinizi yasadışı veya yetkisiz bir şirket tarafından erişilen olduğunu belirlerse.</span><span class="sxs-lookup"><span data-stu-id="dc6c7-105">This information will be used by Microsoft toocontact you if hello Microsoft Security Response Center (MSRC) discovers that your customer data has been accessed by an unlawful or unauthorized party.</span></span> <span data-ttu-id="dc6c7-106">MSRC select güvenlik hello Azure ağ ve altyapı izleme gerçekleştirir ve Üçüncü taraflardan tehdit Intelligence ve kötüye şikayetlerinden alır.</span><span class="sxs-lookup"><span data-stu-id="dc6c7-106">MSRC performs select security monitoring of hello Azure network and infrastructure and receives threat intelligence and abuse complaints from third parties.</span></span>

<span data-ttu-id="dc6c7-107">Merhaba ilk günlük oluşması bir uyarı ve yüksek öneme sahip uyarılar için yalnızca bir e-posta bildirimi gönderilir.</span><span class="sxs-lookup"><span data-stu-id="dc6c7-107">An email notification is sent on hello first daily occurrence of an alert and only for high severity alerts.</span></span> <span data-ttu-id="dc6c7-108">E-posta tercihleri yalnızca abonelik ilkeleri için yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="dc6c7-108">Email preferences can only be configured for subscription policies.</span></span> <span data-ttu-id="dc6c7-109">Bir abonelik içindeki kaynak grupları, bu ayarları devralır.</span><span class="sxs-lookup"><span data-stu-id="dc6c7-109">Resource groups within a subscription will inherit these settings.</span></span>

> [!NOTE]
> <span data-ttu-id="dc6c7-110">Bu belge, örnek bir dağıtım kullanarak hello hizmeti sunar.</span><span class="sxs-lookup"><span data-stu-id="dc6c7-110">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="dc6c7-111">Bu, adım adım ilerleyen bir kılavuz değildir.</span><span class="sxs-lookup"><span data-stu-id="dc6c7-111">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="dc6c7-112">Merhaba öneriyi uygulamayı</span><span class="sxs-lookup"><span data-stu-id="dc6c7-112">Implement hello recommendation</span></span>
1. <span data-ttu-id="dc6c7-113">Merhaba, **önerileri** dikey penceresinde, select **güvenlik iletişim ayrıntılarını sağlamak**.</span><span class="sxs-lookup"><span data-stu-id="dc6c7-113">In hello **Recommendations** blade, select **Provide security contact details**.</span></span>
   <span data-ttu-id="dc6c7-114">![Güvenlik kişi sağlayın][1]</span><span class="sxs-lookup"><span data-stu-id="dc6c7-114">![Provide security contact][1]</span></span>
2. <span data-ttu-id="dc6c7-115">Bu hello dikey pencere açılır **güvenlik iletişim ayrıntılarını sağlamak**.</span><span class="sxs-lookup"><span data-stu-id="dc6c7-115">This opens hello blade **Provide security contact details**.</span></span> <span data-ttu-id="dc6c7-116">' Hello Azure aboneliği tooprovide kişi bilgilerini'ı seçin.</span><span class="sxs-lookup"><span data-stu-id="dc6c7-116">Select hello Azure subscription tooprovide contact information on.</span></span>
   <span data-ttu-id="dc6c7-117">![Güvenlik ilgili kişi bilgilerini belirtin][2]</span><span class="sxs-lookup"><span data-stu-id="dc6c7-117">![Provide security contact details][2]</span></span>
3. <span data-ttu-id="dc6c7-118">İkinci bir **güvenlik iletişim ayrıntılarını sağlamak** dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="dc6c7-118">A second **Provide security contact details** blade opens.</span></span>

   * <span data-ttu-id="dc6c7-119">Merhaba güvenlik iletişim e-posta adresini veya adreslerini noktalı virgüllerle ayırarak girin.</span><span class="sxs-lookup"><span data-stu-id="dc6c7-119">Enter hello security contact email address or addresses separated by commas.</span></span> <span data-ttu-id="dc6c7-120">Bir toohello sayısı sınırı girdiğiniz e-posta adresi değil.</span><span class="sxs-lookup"><span data-stu-id="dc6c7-120">There is not a limit toohello number of email addresses that you can enter.</span></span>
   * <span data-ttu-id="dc6c7-121">Bir güvenlik kişi uluslararası telefon numarası girin.</span><span class="sxs-lookup"><span data-stu-id="dc6c7-121">Enter one security contact international phone number.</span></span>
   * <span data-ttu-id="dc6c7-122">yüksek öneme sahip uyarılar hakkında tooreceive e-postaları kapatma hello seçeneği **bana Gönder e-postalar uyarılar hakkında**.</span><span class="sxs-lookup"><span data-stu-id="dc6c7-122">tooreceive emails about high severity alerts, turn on hello option **Send me emails about alerts**.</span></span>
   * <span data-ttu-id="dc6c7-123">Hello gelecekteki, hello seçeneği toosend e-posta bildirimleri toosubscription sahipleri sahip olur.</span><span class="sxs-lookup"><span data-stu-id="dc6c7-123">In hello future, you will have hello option toosend email notifications toosubscription owners.</span></span> <span data-ttu-id="dc6c7-124">Bu seçenek, gri renkte görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="dc6c7-124">This option is currently grayed out.</span></span>
   * <span data-ttu-id="dc6c7-125">Seçin **Tamam** tooapply hello güvenlik bilgileri tooyour abonelik başvurun.</span><span class="sxs-lookup"><span data-stu-id="dc6c7-125">Select **OK** tooapply hello security contact information tooyour subscription.</span></span>

## <a name="see-also"></a><span data-ttu-id="dc6c7-126">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="dc6c7-126">See also</span></span>
<span data-ttu-id="dc6c7-127">Güvenlik Merkezi hakkında daha fazla toolearn hello aşağıdaki bakın:</span><span class="sxs-lookup"><span data-stu-id="dc6c7-127">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="dc6c7-128">[Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md) --öğrenin nasıl tooconfigure Azure Abonelikleriniz ve kaynak grupları için güvenlik ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="dc6c7-128">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="dc6c7-129">[Azure Güvenlik Merkezi'nde güvenlik önerilerini yönetme](security-center-recommendations.md) --nasıl önerilerin Azure kaynaklarınızı korumanıza yardımcı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="dc6c7-129">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="dc6c7-130">[Azure Güvenlik Merkezi'nde güvenlik durumunu izleme](security-center-monitoring.md) --nasıl toomonitor hello Azure kaynaklarınızın sistem durumunu öğrenin.</span><span class="sxs-lookup"><span data-stu-id="dc6c7-130">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="dc6c7-131">[Azure Güvenlik Merkezi'nde Uyarıları yönetme ve yanıt toosecurity](security-center-managing-and-responding-alerts.md) --öğrenin nasıl toomanage ve yanıt toosecurity uyarıları.</span><span class="sxs-lookup"><span data-stu-id="dc6c7-131">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="dc6c7-132">[Azure Güvenlik Merkezi ile iş ortağı çözümlerini izleme](security-center-partner-solutions.md) --nasıl toomonitor hello iş ortağı çözümlerinizin sistem durumunu öğrenin.</span><span class="sxs-lookup"><span data-stu-id="dc6c7-132">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="dc6c7-133">[Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) --hello hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dc6c7-133">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="dc6c7-134">[Azure güvenlik blogu](http://blogs.msdn.com/b/azuresecurity/) --hello en son Azure güvenlik haberlerini ve bilgilerini alın.</span><span class="sxs-lookup"><span data-stu-id="dc6c7-134">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-provide-security-contacts/provide-contacts.png
[2]:./media/security-center-provide-security-contacts/provide-contact-details.png
