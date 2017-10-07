---
title: "aaaUnderstand Azure dış hizmet ücretlerinizi | Microsoft Docs"
description: "Önceden Market bilinen dış hizmetler, Azure ücretlere faturalama hakkında bilgi edinin."
services: 
documentationcenter: 
author: adpick
manager: tonguyen
editor: 
tags: billing
ms.assetid: 5e0e2a3c-d111-4054-8508-0c111c1b749b
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: adpick
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1d2cb28319e2ab4eff753177220993cbf94c96ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-your-azure-billing-for-external-service-charges"></a><span data-ttu-id="5b793-103">Azure fatura dış servis ücretleri anlamak</span><span class="sxs-lookup"><span data-stu-id="5b793-103">Understand your Azure billing for external service charges</span></span>
<span data-ttu-id="5b793-104">Dış hizmetler Azure Marketi adlı toobe kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5b793-104">External services used toobe called Azure Marketplace.</span></span> <span data-ttu-id="5b793-105">Genellikle, Azure için üçüncü taraflar tarafından kullanılabilen yayımlanan hizmetleri olduğunuz ancak Azure içinde tamamen tümleşiktir.</span><span class="sxs-lookup"><span data-stu-id="5b793-105">Generally, they're services published by third-parties available for Azure but are integrated completely within Azure.</span></span> <span data-ttu-id="5b793-106">Örneğin, ClearDB ve SendGrid Azure'da satın alabilir, ancak Microsoft tarafından yayımlanmayan dış hizmetleridir.</span><span class="sxs-lookup"><span data-stu-id="5b793-106">For example, ClearDB and SendGrid are external services that you can purchase in Azure, but are not published by Microsoft.</span></span>

<span data-ttu-id="5b793-107">Yeni bir dış hizmet veya kaynak sağladığınızda, bir uyarı gösterilir:</span><span class="sxs-lookup"><span data-stu-id="5b793-107">When you provision a new external service or resource, a warning is shown:</span></span>

![Market satın uyarı](./media/billing-understand-your-azure-marketplace-charges/marketplace-warning.PNG)

> [!NOTE]
> <span data-ttu-id="5b793-109">Dış Hizmetler Microsoft olmayan şirketler tarafından yayımlanır, ancak bazen Microsoft ürünleri dış hizmetler de ayrılır.</span><span class="sxs-lookup"><span data-stu-id="5b793-109">External services are published by companies that are not Microsoft, but sometimes Microsoft products are also categorized as external services.</span></span>
> 
> 

## <a name="how-external-services-are-billed"></a><span data-ttu-id="5b793-110">Dış hizmetler faturalandırılır nasıl</span><span class="sxs-lookup"><span data-stu-id="5b793-110">How external services are billed</span></span>
- <span data-ttu-id="5b793-111">Dış hizmetler ayrı ayrı faturalandırılır.</span><span class="sxs-lookup"><span data-stu-id="5b793-111">External services are billed separately.</span></span> <span data-ttu-id="5b793-112">Bunlar, Azure aboneliğinizin içinde tek tek siparişleri olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="5b793-112">They are treated as individual orders within your Azure subscription.</span></span> <span data-ttu-id="5b793-113">Merhaba hizmeti satın aldığınız her hizmet için fatura döneminde hello ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="5b793-113">hello billing period for each service is set when you purchase hello service.</span></span> <span data-ttu-id="5b793-114">Değil toobe hello fatura hello abonelik altında aldığınız noktayla kafası.</span><span class="sxs-lookup"><span data-stu-id="5b793-114">Not toobe confused with hello billing period of hello subscription under which you purchased it.</span></span> <span data-ttu-id="5b793-115">Ayrıca ayrı faturaları aldığınız ve kredi kartınızdan ayrı olarak ücretlendirilir.</span><span class="sxs-lookup"><span data-stu-id="5b793-115">You also receive separate bills and your credit card is charged separately.</span></span>
- <span data-ttu-id="5b793-116">Dış her hizmetin farklı bir fatura modeli vardır.</span><span class="sxs-lookup"><span data-stu-id="5b793-116">Each external service has a different billing model.</span></span> <span data-ttu-id="5b793-117">Diğer bir aylık tabanlı ödeme modeli kullanırken bazı hizmetler Kullandıkça Öde biçimde faturalandırılır.</span><span class="sxs-lookup"><span data-stu-id="5b793-117">Some services are billed in a pay-as-you-go fashion while others use a monthly based payment model.</span></span> <span data-ttu-id="5b793-118">Azure dış hizmetler için bir kredi kartı gerekir, fatura ödeme ile dış hizmetler satın alın.</span><span class="sxs-lookup"><span data-stu-id="5b793-118">You need a credit card for Azure external services, you can't buy external services with invoice pay.</span></span>
- <span data-ttu-id="5b793-119">Dış Hizmetleri için aylık ücretsiz krediler kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="5b793-119">You can't use monthly free credits for external services.</span></span> <span data-ttu-id="5b793-120">İçeren bir Azure aboneliği kullanıyorsanız [ücretsiz krediler](https://azure.microsoft.com/pricing/spending-limits/), uygulanan tooexternal hizmet faturaları olamaz.</span><span class="sxs-lookup"><span data-stu-id="5b793-120">If you are using an Azure subscription that includes [free credits](https://azure.microsoft.com/pricing/spending-limits/), they can't be applied tooexternal service bills.</span></span> <span data-ttu-id="5b793-121">Bir kredi kartı toopurchase dış hizmetler kullanın.</span><span class="sxs-lookup"><span data-stu-id="5b793-121">Use a credit card toopurchase external services.</span></span>


## <a name="view-external-service-spending-and-history-in-hello-azure-portal"></a><span data-ttu-id="5b793-122">Görünüm dış hizmet harcama ve hello Azure portal geçmişi</span><span class="sxs-lookup"><span data-stu-id="5b793-122">View external service spending and history in hello Azure portal</span></span>
<span data-ttu-id="5b793-123">Her abonelik hello içinde bulunan hello dış hizmetlerin bir listesini görüntüleyebileceğiniz [Azure portal](https://portal.azure.com/):</span><span class="sxs-lookup"><span data-stu-id="5b793-123">You can view a list of hello external services that are on each subscription within hello [Azure portal](https://portal.azure.com/):</span></span> 

1. <span data-ttu-id="5b793-124">İçinde toohello oturum [Azure portal](https://portal.azure.com/) hello hesabı yönetici olarak.</span><span class="sxs-lookup"><span data-stu-id="5b793-124">Sign in toohello [Azure portal](https://portal.azure.com/) as hello account administrator.</span></span>
2. <span data-ttu-id="5b793-125">Merhaba Hub menüsünde seçin **abonelikleri**.</span><span class="sxs-lookup"><span data-stu-id="5b793-125">In hello Hub menu, select **Subscriptions**.</span></span>
   
    ![Merhaba Hub menüsünde aboneliklerini seçin](./media/billing-understand-your-azure-marketplace-charges/sub-button.png) 
3. <span data-ttu-id="5b793-127">Merhaba, **abonelikleri** dikey penceresinde, tooview istediğiniz ve ardından select hello abonelik **dış Hizmetler**.</span><span class="sxs-lookup"><span data-stu-id="5b793-127">In hello **Subscriptions** blade, select hello subscription that you want tooview, and then select **External services**.</span></span>
   
    ![Merhaba faturalama dikey penceresinde bir abonelik seçin](./media/billing-understand-your-azure-marketplace-charges/select-sub-external-services.png)
4. <span data-ttu-id="5b793-129">Her bir dış hizmet siparişleri, hello Yayımcı adı, satın aldığınız hizmet katmanı, hello kaynak ve hello geçerli sıra durumu verdiği ad görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="5b793-129">You should see each of your external service orders, hello publisher name, service tier you bought, name you gave hello resource, and hello current order status.</span></span> <span data-ttu-id="5b793-130">toosee bir dış hizmet faturaları ' i seçin.</span><span class="sxs-lookup"><span data-stu-id="5b793-130">toosee past bills, select an external service.</span></span>
   
    ![Bir dış hizmet seçin](./media/billing-understand-your-azure-marketplace-charges/external-service-blade2.png)
5. <span data-ttu-id="5b793-132">Buradan, hello vergi dökümünü dahil olmak üzere fatura miktarda görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5b793-132">From here, you can view past bill amounts including hello tax breakdown.</span></span>
   
    ![Dış Hizmetleri fatura geçmişini görüntüle](./media/billing-understand-your-azure-marketplace-charges/billing-overview-blade.png)

## <a name="view-external-service-spending-for-enterprise-agreement-ea-customers"></a><span data-ttu-id="5b793-134">Kurumsal Anlaşma (Kurumsal Sözleşme) müşteriler için harcama dış Service'i Görüntüle</span><span class="sxs-lookup"><span data-stu-id="5b793-134">View external service spending for Enterprise Agreement (EA) customers</span></span>
<span data-ttu-id="5b793-135">EA müşteriler dış hizmet harcama bakın ve hello EA portalında raporları indirin.</span><span class="sxs-lookup"><span data-stu-id="5b793-135">EA customers can see external service spending and download reports in hello EA portal.</span></span> <span data-ttu-id="5b793-136">Bkz: [EA müşteriler için Azure Marketi](https://ea.azure.com/helpdocs/azureMarketplace) tooget başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="5b793-136">See [Azure Marketplace for EA Customers](https://ea.azure.com/helpdocs/azureMarketplace) tooget started.</span></span>

## <a name="manage-payment-methods-for-external-service-orders"></a><span data-ttu-id="5b793-137">Dış servis siparişleri için ödeme yöntemleri yönetme</span><span class="sxs-lookup"><span data-stu-id="5b793-137">Manage payment methods for external service orders</span></span>
<span data-ttu-id="5b793-138">Merhaba dış servis siparişleri için Ödeme yöntemleriniz güncelleştirme [hesap Merkezi'nde](https://account.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="5b793-138">Update your payment methods for external service orders from hello [Account Center](https://account.windowsazure.com/).</span></span>

> [!NOTE]
> <span data-ttu-id="5b793-139">Bir iş veya Okul hesabı aboneliğinizle satın aldıysanız [desteğine başvurun](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) toomake tooyour ödeme yöntemini değiştirir.</span><span class="sxs-lookup"><span data-stu-id="5b793-139">If you purchased your subscription with a Work or School account, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) toomake changes tooyour payment method.</span></span>
> 
> 

1. <span data-ttu-id="5b793-140">İçinde toohello oturum [hesap Merkezi'nde](https://account.windowsazure.com/) ve [toohello gidin **Market** sekmesi](https://account.windowsazure.com/Store)</span><span class="sxs-lookup"><span data-stu-id="5b793-140">Sign in toohello [Account Center](https://account.windowsazure.com/) and [navigate toohello **marketplace** tab](https://account.windowsazure.com/Store)</span></span>
   
    ![Market hello hesap Merkezi'nde seçin](./media/billing-understand-your-azure-marketplace-charges/select-marketplace.png)
2. <span data-ttu-id="5b793-142">Toomanage istediğiniz hello dış hizmeti seçin</span><span class="sxs-lookup"><span data-stu-id="5b793-142">Select hello external service you want toomanage</span></span>
   
    ![Toomanage istediğiniz hello dış hizmeti seçin](./media/billing-understand-your-azure-marketplace-charges/select-ext-service.png)
3. <span data-ttu-id="5b793-144">Tıklatın **ödeme yöntemini değiştirme** hello hello sayfasının sağ tarafında.</span><span class="sxs-lookup"><span data-stu-id="5b793-144">Click **Change payment method** on hello right side of hello page.</span></span> <span data-ttu-id="5b793-145">Bu bağlantı, tooa farklı portal toomanage ödeme yönteminizi getirir.</span><span class="sxs-lookup"><span data-stu-id="5b793-145">This link brings you tooa different portal toomanage your payment method.</span></span>
   
    ![Sipariş Özeti](./media/billing-understand-your-azure-marketplace-charges/change-payment.PNG)
4. <span data-ttu-id="5b793-147">Tıklatın **Düzenle bilgisi** ve ödeme bilgilerinizin tooupdate yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="5b793-147">Click **Edit info** and follow instructions tooupdate your payment information.</span></span>
   
    ![Bilgi Düzenle](./media/billing-understand-your-azure-marketplace-charges/edit-info.png)

## <a name="cancel-an-external-service-order"></a><span data-ttu-id="5b793-149">Bir dış hizmet siparişi iptal etme</span><span class="sxs-lookup"><span data-stu-id="5b793-149">Cancel an external service order</span></span>
<span data-ttu-id="5b793-150">Dış hizmet siparişinizi toocancel istiyorsanız, hello hello kaynağında silin [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5b793-150">If you want toocancel your external service order, delete hello resource in hello [Azure portal](https://portal.azure.com).</span></span>

![Kaynağı silme](./media/billing-understand-your-azure-marketplace-charges/deleteMarketplaceOrder.PNG)

## <a name="need-help-contact-support"></a><span data-ttu-id="5b793-152">Yardım mı gerekiyor?</span><span class="sxs-lookup"><span data-stu-id="5b793-152">Need help?</span></span> <span data-ttu-id="5b793-153">Desteğe başvurun.</span><span class="sxs-lookup"><span data-stu-id="5b793-153">Contact support.</span></span>
<span data-ttu-id="5b793-154">Hala sorularınız varsa [desteğine başvurun](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) sorunu Çözümlendi hızla tooget.</span><span class="sxs-lookup"><span data-stu-id="5b793-154">If you still have questions, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your issue resolved quickly.</span></span>

