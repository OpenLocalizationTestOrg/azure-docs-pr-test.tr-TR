---
title: "Oluştur, bağlantı, silmek veya bir tümleştirme hesap Azure logic apps içinde taşımak | Microsoft Docs"
description: "Bir tümleştirme hesap oluşturma ve mantıksal uygulamalarınızı Bağla"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: d3ad9e99-a9ee-477b-81bf-0881e11e632f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: LADocs; mandia
ms.openlocfilehash: 716e7b5bab8725dea0fd2b760d0e46e8e892c5b4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-an-integration-account"></a><span data-ttu-id="1597d-103">Bir tümleştirme hesabı nedir?</span><span class="sxs-lookup"><span data-stu-id="1597d-103">What is an integration account?</span></span>

<span data-ttu-id="1597d-104">Bir tümleştirme hesabı kuruluş şemaları, haritalar, sertifikalar, iş ortakları ve anlaşmaları dahil olmak üzere yapıları yönetmek tümleştirme uygulamalarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="1597d-104">An integration account allows enterprise integration apps to manage artifacts, including schemas, maps, certificates, partners and agreements.</span></span> <span data-ttu-id="1597d-105">Oluşturduğunuz herhangi bir tümleştirme uygulama tümleştirmesi hesabınız bu şemaları, haritalar, sertifikalar ve benzeri erişmek için kullanır.</span><span class="sxs-lookup"><span data-stu-id="1597d-105">Any integration app you create uses an integration account to access these schemas, maps, certificates, and so on.</span></span>

## <a name="create-an-integration-account"></a><span data-ttu-id="1597d-106">Bir tümleştirme hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="1597d-106">Create an integration account</span></span>

1.  <span data-ttu-id="1597d-107">[Azure portalı](http://portal.azure.com "Azure portalı") oturumunu açın.</span><span class="sxs-lookup"><span data-stu-id="1597d-107">Sign in to the [Azure portal](http://portal.azure.com "Azure portal").</span></span> <span data-ttu-id="1597d-108">Sol menüden seçin **daha fazla hizmet**.</span><span class="sxs-lookup"><span data-stu-id="1597d-108">From the left menu, select **More services**.</span></span>

    !["Daha fazla Hizmetleri" seçin](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. <span data-ttu-id="1597d-110">Arama kutusuna filtreniz için "tümleştirme" yazın.</span><span class="sxs-lookup"><span data-stu-id="1597d-110">In the search box, type "integration" for your filter.</span></span> <span data-ttu-id="1597d-111">Sonuçlar listesinde **tümleştirme hesapları**.</span><span class="sxs-lookup"><span data-stu-id="1597d-111">In the results list, select **Integration Accounts**.</span></span>

    ![Filtre "tümleştirme üzerinde", "Tümleştirme hesapları" seçin](./media/logic-apps-enterprise-integration-accounts/account-2.png)  

3. <span data-ttu-id="1597d-113">Sayfanın en üstünde seçin **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="1597d-113">At the top of the page, choose **Add**.</span></span>

    ![Seçin ekleme](./media/logic-apps-enterprise-integration-accounts/account-3.png)

4. <span data-ttu-id="1597d-115">Tümleştirme hesabınızın adını ve kullanmak istediğiniz Azure aboneliğini seçin.</span><span class="sxs-lookup"><span data-stu-id="1597d-115">Name your integration account and select the Azure subscription that you want to use.</span></span> <span data-ttu-id="1597d-116">Oluşturabilir ya da yeni bir **kaynak grubu** veya varolan bir kaynak grubu seçin.</span><span class="sxs-lookup"><span data-stu-id="1597d-116">You can either create a new **Resource group** or select an existing resource group.</span></span> <span data-ttu-id="1597d-117">Ardından bir **konumu** tümleştirme hesabınızı barındırmak için ve bir **fiyatlandırma katmanı**.</span><span class="sxs-lookup"><span data-stu-id="1597d-117">Then select a **Location** for hosting your integration account and a **Pricing Tier**.</span></span> 

    <span data-ttu-id="1597d-118">Hazır olduğunuzda, seçin **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="1597d-118">When you're ready, choose **Create**.</span></span>

    ![Tümleştirme hesabının ayrıntılarını verin](./media/logic-apps-enterprise-integration-accounts/account-4.png)

    <span data-ttu-id="1597d-120">Azure tümleştirme hesabınızda 1 dakika içinde tamamlanmalıdır seçilen konum sağlar.</span><span class="sxs-lookup"><span data-stu-id="1597d-120">Azure provisions your integration account  in the selected location, which should complete within 1 minute.</span></span>

5. <span data-ttu-id="1597d-121">Sayfayı yenileyin.</span><span class="sxs-lookup"><span data-stu-id="1597d-121">Refresh the page.</span></span> <span data-ttu-id="1597d-122">Yeni tümleştirme hesabınızı bakın.</span><span class="sxs-lookup"><span data-stu-id="1597d-122">You see your new integration account listed.</span></span>

    ![Yeni tümleştirme hesabınız görüntülenir](./media/logic-apps-enterprise-integration-accounts/account-5.png) 

<span data-ttu-id="1597d-124">Ardından, mantıksal uygulamanızı oluşturduğunuz tümleştirme hesabı bağlayın.</span><span class="sxs-lookup"><span data-stu-id="1597d-124">Next, link the integration account that you created to your logic app.</span></span> 

## <a name="link-an-integration-account-to-a-logic-app"></a><span data-ttu-id="1597d-125">Bir mantıksal uygulama için bir tümleştirme hesap bağlantı</span><span class="sxs-lookup"><span data-stu-id="1597d-125">Link an integration account to a logic app</span></span>

<span data-ttu-id="1597d-126">Maps, şemalar, sözleşmeleri ve diğer yapıları tümleştirme hesabınızda logic apps erişim vermek için mantıksal uygulamanızı tümleştirme hesabı bağlayın.</span><span class="sxs-lookup"><span data-stu-id="1597d-126">To give your logic apps access to maps, schemas, agreements, and other artifacts in your integration account, link the integration account to your logic app.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="1597d-127">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="1597d-127">Prerequisites</span></span>

* <span data-ttu-id="1597d-128">Bir tümleştirme hesabı</span><span class="sxs-lookup"><span data-stu-id="1597d-128">An integration account</span></span>
* <span data-ttu-id="1597d-129">Bir mantıksal uygulama</span><span class="sxs-lookup"><span data-stu-id="1597d-129">A logic app</span></span>

> [!NOTE] 
> <span data-ttu-id="1597d-130">Tümleştirme hesabı ve mantıksal uygulamanızı emin olun olan *aynı Azure konumuna* başlamadan önce.</span><span class="sxs-lookup"><span data-stu-id="1597d-130">Make sure your integration account and logic app are in the *same Azure location* before you begin.</span></span>


1. <span data-ttu-id="1597d-131">Azure portalında mantıksal uygulamanızı seçin ve mantığı uygulamanızın konumunu denetleyin.</span><span class="sxs-lookup"><span data-stu-id="1597d-131">In the Azure portal, select your logic app, and check your logic app's location.</span></span>

    ![Mantıksal uygulamanızı seçin, konumunu denetleyin](./media/logic-apps-enterprise-integration-accounts/linkaccount-1.png)

2. <span data-ttu-id="1597d-133">Altında **ayarları**seçin **tümleştirme hesabını**.</span><span class="sxs-lookup"><span data-stu-id="1597d-133">Under **Settings**, select **Integration Account**.</span></span>

    !["Tümleştirme hesabı" seçin](./media/logic-apps-enterprise-integration-accounts/linkaccount-2.png)

3. <span data-ttu-id="1597d-135">Gelen **tümleştirme hesabı seçme** listesinde, mantıksal uygulamanızı bağlamak istediğiniz tümleştirme hesabını seçin.</span><span class="sxs-lookup"><span data-stu-id="1597d-135">From the **Select an Integration account** list, select the integration account you want to link to your logic app.</span></span> <span data-ttu-id="1597d-136">Bağlama işlemini tamamlamak için seçin **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="1597d-136">To finish linking, choose **Save**.</span></span>

    ![Tümleştirme hesabınızı seçin](./media/logic-apps-enterprise-integration-accounts/linkaccount-3.png)

    <span data-ttu-id="1597d-138">Tümleştirmenize hesabına mantıksal uygulamanızı bağlanır ve tümleştirme hesabınızdaki tüm yapıları mantıksal uygulamanızı kullanılabilir olduğunu gösteren bir bildirim alır.</span><span class="sxs-lookup"><span data-stu-id="1597d-138">You get a notification that shows your integration account is linked to your logic app,  and that all artifacts in your integration account are now available to your logic app.</span></span>

    ![Mantıksal uygulamanızı tümleştirme hesabınıza bağlı](./media/logic-apps-enterprise-integration-accounts/linkaccount-5.png)

<span data-ttu-id="1597d-140">Mantıksal uygulamanızı tümleştirme hesabınıza bağlı, logic apps içinde B2B bağlayıcılar kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1597d-140">Now that your integration account is linked to your logic app, you can use the B2B connectors in your logic apps.</span></span> <span data-ttu-id="1597d-141">XML doğrulaması ve düz dosya kodlama/kod çözme bazı ortak B2B bağlayıcıları içerir.</span><span class="sxs-lookup"><span data-stu-id="1597d-141">Some common B2B connectors include XML validation and flat file encode/decode.</span></span>  

## <a name="delete-your-integration-account"></a><span data-ttu-id="1597d-142">Tümleştirme hesabınızı silme</span><span class="sxs-lookup"><span data-stu-id="1597d-142">Delete your integration account</span></span>

1. <span data-ttu-id="1597d-143">Seçin **daha fazla hizmet**.</span><span class="sxs-lookup"><span data-stu-id="1597d-143">Select **More services**.</span></span>

    !["Daha fazla Hizmetleri" seçin](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. <span data-ttu-id="1597d-145">Arama kutusuna filtreniz için "tümleştirme" yazın.</span><span class="sxs-lookup"><span data-stu-id="1597d-145">In the search box, type "integration" for your filter.</span></span> <span data-ttu-id="1597d-146">Sonuçlar listesinde **tümleştirme hesapları**.</span><span class="sxs-lookup"><span data-stu-id="1597d-146">In the results list, select **Integration Accounts**.</span></span>

    ![Filtre "tümleştirme üzerinde", "Tümleştirme hesapları" seçin](./media/logic-apps-enterprise-integration-accounts/account-2.png)  

3. <span data-ttu-id="1597d-148">Silmek istediğiniz tümleştirme hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="1597d-148">Select the integration account that you want to delete.</span></span>

    ![Silmek için tümleştirme hesabı seçin](./media/logic-apps-enterprise-integration-accounts/account-5.png)

4. <span data-ttu-id="1597d-150">Menüsünde, **silmek**.</span><span class="sxs-lookup"><span data-stu-id="1597d-150">On the menu, choose **Delete**.</span></span>

    !["Sil"'i seçin](./media/logic-apps-enterprise-integration-accounts/delete.png)

5. <span data-ttu-id="1597d-152">Tümleştirme hesabını silmek için seçiminizi onaylayın.</span><span class="sxs-lookup"><span data-stu-id="1597d-152">Confirm your choice to delete the integration account.</span></span>

## <a name="move-your-integration-account"></a><span data-ttu-id="1597d-153">Tümleştirme hesabınızı taşıma</span><span class="sxs-lookup"><span data-stu-id="1597d-153">Move your integration account</span></span>

<span data-ttu-id="1597d-154">Bir tümleştirme hesabı başka bir Azure abonelik veya kaynak grubuna taşımak için şu adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="1597d-154">To move an integration account to another Azure subscription or resource group, follow these steps.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1597d-155">Bir tümleştirme hesap taşıdıktan sonra yeni kaynak kimlikleri kullanmak için tüm betikler güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1597d-155">You must update all scripts to use the new resource IDs after you move an integration account.</span></span>

1. <span data-ttu-id="1597d-156">Seçin **daha fazla hizmet**.</span><span class="sxs-lookup"><span data-stu-id="1597d-156">Select **More services**.</span></span>

    !["Daha fazla Hizmetleri" seçin](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. <span data-ttu-id="1597d-158">Arama kutusuna filtreniz için "tümleştirme" yazın.</span><span class="sxs-lookup"><span data-stu-id="1597d-158">In the search box, type "integration" for your filter.</span></span> <span data-ttu-id="1597d-159">Sonuçlar listesinde **tümleştirme hesapları**.</span><span class="sxs-lookup"><span data-stu-id="1597d-159">In the results list, select **Integration Accounts**.</span></span>

    ![Filtre "tümleştirme üzerinde", "Tümleştirme hesapları" seçin](./media/logic-apps-enterprise-integration-accounts/account-2.png)

3. <span data-ttu-id="1597d-161">Taşımak istediğiniz tümleştirme hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="1597d-161">Select the integration account that you want to move.</span></span> <span data-ttu-id="1597d-162">Altında **ayarları**, seçin **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="1597d-162">Under **Settings**, choose **Properties**.</span></span>

    ![Taşımak için tümleştirme hesabı seçin.](./media/logic-apps-enterprise-integration-accounts/move.png)

5. <span data-ttu-id="1597d-165">Kaynak grubu veya tümleştirme hesabınızla ilişkili Azure abonelik değiştirin.</span><span class="sxs-lookup"><span data-stu-id="1597d-165">Change the resource group or Azure subscription that's associated with your integration account.</span></span>

    ![Kaynak grubu Değiştir veya değişiklik abonelik seçin](./media/logic-apps-enterprise-integration-accounts/move-2.png)

## <a name="next-steps"></a><span data-ttu-id="1597d-167">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="1597d-167">Next Steps</span></span>
* [<span data-ttu-id="1597d-168">Anlaşmaları hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="1597d-168">Learn more about agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Kurumsal tümleştirme anlaşmaları hakkında bilgi edinin")  

