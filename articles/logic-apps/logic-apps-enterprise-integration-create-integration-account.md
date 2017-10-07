---
title: "aaaCreate, bağlantı, silmek veya bir tümleştirme hesap Azure logic apps içinde taşımak | Microsoft Docs"
description: "Nasıl toocreate bir tümleştirme hesap ve tooyour logic apps Bağla"
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
ms.openlocfilehash: fda6c91723b3e3624ee176df112ba8b6c9800273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-an-integration-account"></a><span data-ttu-id="c22fd-103">Bir tümleştirme hesabı nedir?</span><span class="sxs-lookup"><span data-stu-id="c22fd-103">What is an integration account?</span></span>

<span data-ttu-id="c22fd-104">Bir tümleştirme hesabı toomanage yapıları, şemalar, haritalar, sertifikalar, iş ortakları ve anlaşmaları dahil olmak üzere Kurumsal tümleştirme uygulamalarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="c22fd-104">An integration account allows enterprise integration apps toomanage artifacts, including schemas, maps, certificates, partners and agreements.</span></span> <span data-ttu-id="c22fd-105">Oluşturduğunuz herhangi bir tümleştirme uygulama bu şemaları, haritalar, sertifikalar ve benzeri bir tümleştirme hesap tooaccess kullanır.</span><span class="sxs-lookup"><span data-stu-id="c22fd-105">Any integration app you create uses an integration account tooaccess these schemas, maps, certificates, and so on.</span></span>

## <a name="create-an-integration-account"></a><span data-ttu-id="c22fd-106">Bir tümleştirme hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c22fd-106">Create an integration account</span></span>

1.  <span data-ttu-id="c22fd-107">İçinde toohello oturum [Azure portal](http://portal.azure.com "Azure portal").</span><span class="sxs-lookup"><span data-stu-id="c22fd-107">Sign in toohello [Azure portal](http://portal.azure.com "Azure portal").</span></span> <span data-ttu-id="c22fd-108">Merhaba sol menüden seçin **daha fazla hizmet**.</span><span class="sxs-lookup"><span data-stu-id="c22fd-108">From hello left menu, select **More services**.</span></span>

    !["Daha fazla Hizmetleri" seçin](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. <span data-ttu-id="c22fd-110">Filtreniz için "tümleştirme" Merhaba arama kutusuna yazın.</span><span class="sxs-lookup"><span data-stu-id="c22fd-110">In hello search box, type "integration" for your filter.</span></span> <span data-ttu-id="c22fd-111">Merhaba sonuçları listesinden seçmek **tümleştirme hesapları**.</span><span class="sxs-lookup"><span data-stu-id="c22fd-111">In hello results list, select **Integration Accounts**.</span></span>

    ![Filtre "tümleştirme üzerinde", "Tümleştirme hesapları" seçin](./media/logic-apps-enterprise-integration-accounts/account-2.png)  

3. <span data-ttu-id="c22fd-113">Merhaba hello sayfanın en üstünde, seçin **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="c22fd-113">At hello top of hello page, choose **Add**.</span></span>

    ![Seçin ekleme](./media/logic-apps-enterprise-integration-accounts/account-3.png)

4. <span data-ttu-id="c22fd-115">Ad tümleştirme hesabını ve select hello toouse istediğiniz Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="c22fd-115">Name your integration account and select hello Azure subscription that you want toouse.</span></span> <span data-ttu-id="c22fd-116">Oluşturabilir ya da yeni bir **kaynak grubu** veya varolan bir kaynak grubu seçin.</span><span class="sxs-lookup"><span data-stu-id="c22fd-116">You can either create a new **Resource group** or select an existing resource group.</span></span> <span data-ttu-id="c22fd-117">Ardından bir **konumu** tümleştirme hesabınızı barındırmak için ve bir **fiyatlandırma katmanı**.</span><span class="sxs-lookup"><span data-stu-id="c22fd-117">Then select a **Location** for hosting your integration account and a **Pricing Tier**.</span></span> 

    <span data-ttu-id="c22fd-118">Hazır olduğunuzda, seçin **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="c22fd-118">When you're ready, choose **Create**.</span></span>

    ![Tümleştirme hesabının ayrıntılarını verin](./media/logic-apps-enterprise-integration-accounts/account-4.png)

    <span data-ttu-id="c22fd-120">Azure tümleştirme hesabınızı 1 dakika içinde tamamlanmalıdır hello seçili konumda sağlar.</span><span class="sxs-lookup"><span data-stu-id="c22fd-120">Azure provisions your integration account  in hello selected location, which should complete within 1 minute.</span></span>

5. <span data-ttu-id="c22fd-121">Merhaba sayfayı yenileyin.</span><span class="sxs-lookup"><span data-stu-id="c22fd-121">Refresh hello page.</span></span> <span data-ttu-id="c22fd-122">Yeni tümleştirme hesabınızı bakın.</span><span class="sxs-lookup"><span data-stu-id="c22fd-122">You see your new integration account listed.</span></span>

    ![Yeni tümleştirme hesabınız görüntülenir](./media/logic-apps-enterprise-integration-accounts/account-5.png) 

<span data-ttu-id="c22fd-124">Ardından, bu, oluşturulan tooyour mantıksal uygulama hello tümleştirme hesabı bağlayın.</span><span class="sxs-lookup"><span data-stu-id="c22fd-124">Next, link hello integration account that you created tooyour logic app.</span></span> 

## <a name="link-an-integration-account-tooa-logic-app"></a><span data-ttu-id="c22fd-125">Bir tümleştirme hesap tooa mantıksal uygulama bağlantı</span><span class="sxs-lookup"><span data-stu-id="c22fd-125">Link an integration account tooa logic app</span></span>

<span data-ttu-id="c22fd-126">toogive mantıksal uygulamalarınızı erişim toomaps, şemalar, anlaşmalar ve diğer yapıları tümleştirme hesabınızda, bağlantı hello tümleştirme hesap tooyour mantıksal uygulama.</span><span class="sxs-lookup"><span data-stu-id="c22fd-126">toogive your logic apps access toomaps, schemas, agreements, and other artifacts in your integration account, link hello integration account tooyour logic app.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="c22fd-127">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="c22fd-127">Prerequisites</span></span>

* <span data-ttu-id="c22fd-128">Bir tümleştirme hesabı</span><span class="sxs-lookup"><span data-stu-id="c22fd-128">An integration account</span></span>
* <span data-ttu-id="c22fd-129">Bir mantıksal uygulama</span><span class="sxs-lookup"><span data-stu-id="c22fd-129">A logic app</span></span>

> [!NOTE] 
> <span data-ttu-id="c22fd-130">Tümleştirme hesabı ve mantıksal uygulamanızı hello olduğundan emin olun *aynı Azure konumuna* başlamadan önce.</span><span class="sxs-lookup"><span data-stu-id="c22fd-130">Make sure your integration account and logic app are in hello *same Azure location* before you begin.</span></span>


1. <span data-ttu-id="c22fd-131">Hello Azure portal, mantıksal uygulamanızı seçin ve mantığı uygulamanızın konumunu denetleyin.</span><span class="sxs-lookup"><span data-stu-id="c22fd-131">In hello Azure portal, select your logic app, and check your logic app's location.</span></span>

    ![Mantıksal uygulamanızı seçin, konumunu denetleyin](./media/logic-apps-enterprise-integration-accounts/linkaccount-1.png)

2. <span data-ttu-id="c22fd-133">Altında **ayarları**seçin **tümleştirme hesabını**.</span><span class="sxs-lookup"><span data-stu-id="c22fd-133">Under **Settings**, select **Integration Account**.</span></span>

    !["Tümleştirme hesabı" seçin](./media/logic-apps-enterprise-integration-accounts/linkaccount-2.png)

3. <span data-ttu-id="c22fd-135">Merhaba gelen **tümleştirme hesabı seçin** listesinde, select hello tümleştirme hesap toolink tooyour mantıksal uygulama istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="c22fd-135">From hello **Select an Integration account** list, select hello integration account you want toolink tooyour logic app.</span></span> <span data-ttu-id="c22fd-136">bağlama, toofinish seçin **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="c22fd-136">toofinish linking, choose **Save**.</span></span>

    ![Tümleştirme hesabınızı seçin](./media/logic-apps-enterprise-integration-accounts/linkaccount-3.png)

    <span data-ttu-id="c22fd-138">Tümleştirmenize bağlantılı tooyour mantıksal uygulama hesabıdır ve tümleştirme hesabınızdaki tüm yapıları artık kullanılabilir tooyour mantıksal uygulama olduğunu gösteren bir bildirim alır.</span><span class="sxs-lookup"><span data-stu-id="c22fd-138">You get a notification that shows your integration account is linked tooyour logic app,  and that all artifacts in your integration account are now available tooyour logic app.</span></span>

    ![Mantıksal uygulamanızı bağlı tooyour tümleştirme hesabı](./media/logic-apps-enterprise-integration-accounts/linkaccount-5.png)

<span data-ttu-id="c22fd-140">Tümleştirme hesabınızın bağlantılı tooyour mantıksal uygulama olduğundan, mantıksal uygulamalarınızı hello B2B bağlayıcılar kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c22fd-140">Now that your integration account is linked tooyour logic app, you can use hello B2B connectors in your logic apps.</span></span> <span data-ttu-id="c22fd-141">XML doğrulaması ve düz dosya kodlama/kod çözme bazı ortak B2B bağlayıcıları içerir.</span><span class="sxs-lookup"><span data-stu-id="c22fd-141">Some common B2B connectors include XML validation and flat file encode/decode.</span></span>  

## <a name="delete-your-integration-account"></a><span data-ttu-id="c22fd-142">Tümleştirme hesabınızı silme</span><span class="sxs-lookup"><span data-stu-id="c22fd-142">Delete your integration account</span></span>

1. <span data-ttu-id="c22fd-143">Seçin **daha fazla hizmet**.</span><span class="sxs-lookup"><span data-stu-id="c22fd-143">Select **More services**.</span></span>

    !["Daha fazla Hizmetleri" seçin](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. <span data-ttu-id="c22fd-145">Filtreniz için "tümleştirme" Merhaba arama kutusuna yazın.</span><span class="sxs-lookup"><span data-stu-id="c22fd-145">In hello search box, type "integration" for your filter.</span></span> <span data-ttu-id="c22fd-146">Merhaba sonuçları listesinden seçmek **tümleştirme hesapları**.</span><span class="sxs-lookup"><span data-stu-id="c22fd-146">In hello results list, select **Integration Accounts**.</span></span>

    ![Filtre "tümleştirme üzerinde", "Tümleştirme hesapları" seçin](./media/logic-apps-enterprise-integration-accounts/account-2.png)  

3. <span data-ttu-id="c22fd-148">Merhaba tümleştirme hesabı toodelete istediğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="c22fd-148">Select hello integration account that you want toodelete.</span></span>

    ![Tümleştirme hesap toodelete seçin](./media/logic-apps-enterprise-integration-accounts/account-5.png)

4. <span data-ttu-id="c22fd-150">Başlangıç menüsünde, **silmek**.</span><span class="sxs-lookup"><span data-stu-id="c22fd-150">On hello menu, choose **Delete**.</span></span>

    !["Sil"'i seçin](./media/logic-apps-enterprise-integration-accounts/delete.png)

5. <span data-ttu-id="c22fd-152">Seçim toodelete hello tümleştirme hesabınızı onaylayın.</span><span class="sxs-lookup"><span data-stu-id="c22fd-152">Confirm your choice toodelete hello integration account.</span></span>

## <a name="move-your-integration-account"></a><span data-ttu-id="c22fd-153">Tümleştirme hesabınızı taşıma</span><span class="sxs-lookup"><span data-stu-id="c22fd-153">Move your integration account</span></span>

<span data-ttu-id="c22fd-154">toomove tümleştirme hesap tooanother Azure abonelik veya kaynak grubu, şu adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="c22fd-154">toomove an integration account tooanother Azure subscription or resource group, follow these steps.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c22fd-155">Bir tümleştirme hesap taşıdıktan sonra tüm betikler toouse hello yeni kaynak kimlikleri güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c22fd-155">You must update all scripts toouse hello new resource IDs after you move an integration account.</span></span>

1. <span data-ttu-id="c22fd-156">Seçin **daha fazla hizmet**.</span><span class="sxs-lookup"><span data-stu-id="c22fd-156">Select **More services**.</span></span>

    !["Daha fazla Hizmetleri" seçin](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. <span data-ttu-id="c22fd-158">Filtreniz için "tümleştirme" Merhaba arama kutusuna yazın.</span><span class="sxs-lookup"><span data-stu-id="c22fd-158">In hello search box, type "integration" for your filter.</span></span> <span data-ttu-id="c22fd-159">Merhaba sonuçları listesinden seçmek **tümleştirme hesapları**.</span><span class="sxs-lookup"><span data-stu-id="c22fd-159">In hello results list, select **Integration Accounts**.</span></span>

    ![Filtre "tümleştirme üzerinde", "Tümleştirme hesapları" seçin](./media/logic-apps-enterprise-integration-accounts/account-2.png)

3. <span data-ttu-id="c22fd-161">Merhaba tümleştirme hesabı toomove istediğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="c22fd-161">Select hello integration account that you want toomove.</span></span> <span data-ttu-id="c22fd-162">Altında **ayarları**, seçin **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="c22fd-162">Under **Settings**, choose **Properties**.</span></span>

    ![Tümleştirme hesap toomove seçin.](./media/logic-apps-enterprise-integration-accounts/move.png)

5. <span data-ttu-id="c22fd-165">Merhaba kaynak grubu veya tümleştirme hesabınızla ilişkili Azure abonelik değiştirin.</span><span class="sxs-lookup"><span data-stu-id="c22fd-165">Change hello resource group or Azure subscription that's associated with your integration account.</span></span>

    ![Kaynak grubu Değiştir veya değişiklik abonelik seçin](./media/logic-apps-enterprise-integration-accounts/move-2.png)

## <a name="next-steps"></a><span data-ttu-id="c22fd-167">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="c22fd-167">Next Steps</span></span>
* [<span data-ttu-id="c22fd-168">Anlaşmaları hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="c22fd-168">Learn more about agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Kurumsal tümleştirme anlaşmaları hakkında bilgi edinin")  

