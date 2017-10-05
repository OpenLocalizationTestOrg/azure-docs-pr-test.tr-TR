---
title: "Azure, dış hizmet ücretlerini anlama | Microsoft Docs"
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
ms.openlocfilehash: 11701ce0162113ef6c8e056d3a30fe1d8f702f92
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="understand-your-azure-billing-for-external-service-charges"></a><span data-ttu-id="fe59b-103">Azure fatura dış servis ücretleri anlamak</span><span class="sxs-lookup"><span data-stu-id="fe59b-103">Understand your Azure billing for external service charges</span></span>
<span data-ttu-id="fe59b-104">Dış hizmetler Azure Marketi çağrılması için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="fe59b-104">External services used to be called Azure Marketplace.</span></span> <span data-ttu-id="fe59b-105">Genellikle, Azure için üçüncü taraflar tarafından kullanılabilen yayımlanan hizmetleri olduğunuz ancak Azure içinde tamamen tümleşiktir.</span><span class="sxs-lookup"><span data-stu-id="fe59b-105">Generally, they're services published by third-parties available for Azure but are integrated completely within Azure.</span></span> <span data-ttu-id="fe59b-106">Örneğin, ClearDB ve SendGrid Azure'da satın alabilir, ancak Microsoft tarafından yayımlanmayan dış hizmetleridir.</span><span class="sxs-lookup"><span data-stu-id="fe59b-106">For example, ClearDB and SendGrid are external services that you can purchase in Azure, but are not published by Microsoft.</span></span>

<span data-ttu-id="fe59b-107">Yeni bir dış hizmet veya kaynak sağladığınızda, bir uyarı gösterilir:</span><span class="sxs-lookup"><span data-stu-id="fe59b-107">When you provision a new external service or resource, a warning is shown:</span></span>

![Market satın uyarı](./media/billing-understand-your-azure-marketplace-charges/marketplace-warning.PNG)

> [!NOTE]
> <span data-ttu-id="fe59b-109">Dış Hizmetler Microsoft olmayan şirketler tarafından yayımlanır, ancak bazen Microsoft ürünleri dış hizmetler de ayrılır.</span><span class="sxs-lookup"><span data-stu-id="fe59b-109">External services are published by companies that are not Microsoft, but sometimes Microsoft products are also categorized as external services.</span></span>
> 
> 

## <a name="how-external-services-are-billed"></a><span data-ttu-id="fe59b-110">Dış hizmetler faturalandırılır nasıl</span><span class="sxs-lookup"><span data-stu-id="fe59b-110">How external services are billed</span></span>
- <span data-ttu-id="fe59b-111">Dış hizmetler ayrı ayrı faturalandırılır.</span><span class="sxs-lookup"><span data-stu-id="fe59b-111">External services are billed separately.</span></span> <span data-ttu-id="fe59b-112">Bunlar, Azure aboneliğinizin içinde tek tek siparişleri olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="fe59b-112">They are treated as individual orders within your Azure subscription.</span></span> <span data-ttu-id="fe59b-113">Hizmeti satın aldığınız her hizmet için fatura döneminde ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="fe59b-113">The billing period for each service is set when you purchase the service.</span></span> <span data-ttu-id="fe59b-114">Altında aldığınız abonelik faturalama dönemi ile karıştırılmamalıdır için.</span><span class="sxs-lookup"><span data-stu-id="fe59b-114">Not to be confused with the billing period of the subscription under which you purchased it.</span></span> <span data-ttu-id="fe59b-115">Ayrıca ayrı faturaları aldığınız ve kredi kartınızdan ayrı olarak ücretlendirilir.</span><span class="sxs-lookup"><span data-stu-id="fe59b-115">You also receive separate bills and your credit card is charged separately.</span></span>
- <span data-ttu-id="fe59b-116">Dış her hizmetin farklı bir fatura modeli vardır.</span><span class="sxs-lookup"><span data-stu-id="fe59b-116">Each external service has a different billing model.</span></span> <span data-ttu-id="fe59b-117">Diğer bir aylık tabanlı ödeme modeli kullanırken bazı hizmetler Kullandıkça Öde biçimde faturalandırılır.</span><span class="sxs-lookup"><span data-stu-id="fe59b-117">Some services are billed in a pay-as-you-go fashion while others use a monthly based payment model.</span></span> <span data-ttu-id="fe59b-118">Azure dış hizmetler için bir kredi kartı gerekir, fatura ödeme ile dış hizmetler satın alın.</span><span class="sxs-lookup"><span data-stu-id="fe59b-118">You need a credit card for Azure external services, you can't buy external services with invoice pay.</span></span>
- <span data-ttu-id="fe59b-119">Dış Hizmetleri için aylık ücretsiz krediler kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="fe59b-119">You can't use monthly free credits for external services.</span></span> <span data-ttu-id="fe59b-120">İçeren bir Azure aboneliği kullanıyorsanız [ücretsiz krediler](https://azure.microsoft.com/pricing/spending-limits/), dış hizmet faturaları uygulanamaz.</span><span class="sxs-lookup"><span data-stu-id="fe59b-120">If you are using an Azure subscription that includes [free credits](https://azure.microsoft.com/pricing/spending-limits/), they can't be applied to external service bills.</span></span> <span data-ttu-id="fe59b-121">Dış hizmetler satın almak için bir kredi kartı kullanın.</span><span class="sxs-lookup"><span data-stu-id="fe59b-121">Use a credit card to purchase external services.</span></span>


## <a name="view-external-service-spending-and-history-in-the-azure-portal"></a><span data-ttu-id="fe59b-122">Görünüm dış hizmet harcama ve Azure portalında geçmişi</span><span class="sxs-lookup"><span data-stu-id="fe59b-122">View external service spending and history in the Azure portal</span></span>
<span data-ttu-id="fe59b-123">Her abonelik içinde bulunan dış hizmetlerin bir listesini görüntüleyebileceğiniz [Azure portal](https://portal.azure.com/):</span><span class="sxs-lookup"><span data-stu-id="fe59b-123">You can view a list of the external services that are on each subscription within the [Azure portal](https://portal.azure.com/):</span></span> 

1. <span data-ttu-id="fe59b-124">Oturum [Azure portal](https://portal.azure.com/) hesabı yönetici olarak.</span><span class="sxs-lookup"><span data-stu-id="fe59b-124">Sign in to the [Azure portal](https://portal.azure.com/) as the account administrator.</span></span>
2. <span data-ttu-id="fe59b-125">Hub menüsünde seçin **abonelikleri**.</span><span class="sxs-lookup"><span data-stu-id="fe59b-125">In the Hub menu, select **Subscriptions**.</span></span>
   
    ![Hub menüsünde aboneliklerini seçin](./media/billing-understand-your-azure-marketplace-charges/sub-button.png) 
3. <span data-ttu-id="fe59b-127">İçinde **abonelikleri** dikey penceresinde, görüntülemek istediğiniz aboneliği seçin ve ardından **dış Hizmetler**.</span><span class="sxs-lookup"><span data-stu-id="fe59b-127">In the **Subscriptions** blade, select the subscription that you want to view, and then select **External services**.</span></span>
   
    ![Faturalama dikey penceresinde bir abonelik seçin](./media/billing-understand-your-azure-marketplace-charges/select-sub-external-services.png)
4. <span data-ttu-id="fe59b-129">Her bir dış hizmet siparişler, yayımcı adını, satın aldığınız hizmet katmanı, kaynak ve geçerli sıra durumu verdiğiniz adı görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="fe59b-129">You should see each of your external service orders, the publisher name, service tier you bought, name you gave the resource, and the current order status.</span></span> <span data-ttu-id="fe59b-130">Faturaları görmek için bir dış hizmet seçin.</span><span class="sxs-lookup"><span data-stu-id="fe59b-130">To see past bills, select an external service.</span></span>
   
    ![Bir dış hizmet seçin](./media/billing-understand-your-azure-marketplace-charges/external-service-blade2.png)
5. <span data-ttu-id="fe59b-132">Buradan, vergi dökümünü dahil olmak üzere fatura miktarda görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fe59b-132">From here, you can view past bill amounts including the tax breakdown.</span></span>
   
    ![Dış Hizmetleri fatura geçmişini görüntüle](./media/billing-understand-your-azure-marketplace-charges/billing-overview-blade.png)

## <a name="view-external-service-spending-for-enterprise-agreement-ea-customers"></a><span data-ttu-id="fe59b-134">Kurumsal Anlaşma (Kurumsal Sözleşme) müşteriler için harcama dış Service'i Görüntüle</span><span class="sxs-lookup"><span data-stu-id="fe59b-134">View external service spending for Enterprise Agreement (EA) customers</span></span>
<span data-ttu-id="fe59b-135">EA müşteriler dış hizmet harcama bakın ve EA portalında raporları indirin.</span><span class="sxs-lookup"><span data-stu-id="fe59b-135">EA customers can see external service spending and download reports in the EA portal.</span></span> <span data-ttu-id="fe59b-136">Bkz: [EA müşteriler için Azure Marketi](https://ea.azure.com/helpdocs/azureMarketplace) başlamak için.</span><span class="sxs-lookup"><span data-stu-id="fe59b-136">See [Azure Marketplace for EA Customers](https://ea.azure.com/helpdocs/azureMarketplace) to get started.</span></span>

## <a name="manage-payment-methods-for-external-service-orders"></a><span data-ttu-id="fe59b-137">Dış servis siparişleri için ödeme yöntemleri yönetme</span><span class="sxs-lookup"><span data-stu-id="fe59b-137">Manage payment methods for external service orders</span></span>
<span data-ttu-id="fe59b-138">Dış servis siparişleri için Ödeme yöntemleriniz güncelleştirme [hesap Merkezi'nde](https://account.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="fe59b-138">Update your payment methods for external service orders from the [Account Center](https://account.windowsazure.com/).</span></span>

> [!NOTE]
> <span data-ttu-id="fe59b-139">Bir iş veya Okul hesabı aboneliğinizle satın aldıysanız [desteğine başvurun](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) ödeme yönteminizi değişiklik yapma.</span><span class="sxs-lookup"><span data-stu-id="fe59b-139">If you purchased your subscription with a Work or School account, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to make changes to your payment method.</span></span>
> 
> 

1. <span data-ttu-id="fe59b-140">Oturum [hesap Merkezi'nde](https://account.windowsazure.com/) ve [gidin **Market** sekmesi](https://account.windowsazure.com/Store)</span><span class="sxs-lookup"><span data-stu-id="fe59b-140">Sign in to the [Account Center](https://account.windowsazure.com/) and [navigate to the **marketplace** tab](https://account.windowsazure.com/Store)</span></span>
   
    ![Market hesap Merkezi'nde seçin](./media/billing-understand-your-azure-marketplace-charges/select-marketplace.png)
2. <span data-ttu-id="fe59b-142">Yönetmek istediğiniz dış hizmeti seçin</span><span class="sxs-lookup"><span data-stu-id="fe59b-142">Select the external service you want to manage</span></span>
   
    ![Yönetmek istediğiniz dış hizmeti seçin](./media/billing-understand-your-azure-marketplace-charges/select-ext-service.png)
3. <span data-ttu-id="fe59b-144">Tıklatın **ödeme yöntemini değiştirme** sayfasının sağ tarafında.</span><span class="sxs-lookup"><span data-stu-id="fe59b-144">Click **Change payment method** on the right side of the page.</span></span> <span data-ttu-id="fe59b-145">Bu bağlantıyı ödeme yönteminizi yönetmek için farklı bir portal getirir.</span><span class="sxs-lookup"><span data-stu-id="fe59b-145">This link brings you to a different portal to manage your payment method.</span></span>
   
    ![Sipariş Özeti](./media/billing-understand-your-azure-marketplace-charges/change-payment.PNG)
4. <span data-ttu-id="fe59b-147">Tıklatın **Düzenle bilgisi** ve Ödeme bilgilerinizi güncellemek için yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="fe59b-147">Click **Edit info** and follow instructions to update your payment information.</span></span>
   
    ![Bilgi Düzenle](./media/billing-understand-your-azure-marketplace-charges/edit-info.png)

## <a name="cancel-an-external-service-order"></a><span data-ttu-id="fe59b-149">Bir dış hizmet siparişi iptal etme</span><span class="sxs-lookup"><span data-stu-id="fe59b-149">Cancel an external service order</span></span>
<span data-ttu-id="fe59b-150">Dış hizmet siparişinizi iptal etmek istiyorsanız, kaynak silin [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fe59b-150">If you want to cancel your external service order, delete the resource in the [Azure portal](https://portal.azure.com).</span></span>

![Kaynağı silme](./media/billing-understand-your-azure-marketplace-charges/deleteMarketplaceOrder.PNG)

## <a name="need-help-contact-support"></a><span data-ttu-id="fe59b-152">Yardım mı gerekiyor?</span><span class="sxs-lookup"><span data-stu-id="fe59b-152">Need help?</span></span> <span data-ttu-id="fe59b-153">Desteğe başvurun.</span><span class="sxs-lookup"><span data-stu-id="fe59b-153">Contact support.</span></span>
<span data-ttu-id="fe59b-154">Hala sorularınız varsa [desteğine başvurun](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) hızla çözümlenen sorunu almak için.</span><span class="sxs-lookup"><span data-stu-id="fe59b-154">If you still have questions, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span>

