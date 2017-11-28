---
title: "aaaHow uygulamaları hello erişim panelinde görüntülenir | Microsoft Docs"
description: "Bir uygulama hello erişim paneli görünen neden sorun giderme"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.reviewr: japere
ms.openlocfilehash: 14ee732c4ed5260cba878e949cf9d90877aee67e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-applications-appear-on-hello-access-panel"></a><span data-ttu-id="c6975-103">Uygulamaları hello erişim panelinde görüntülenme</span><span class="sxs-lookup"><span data-stu-id="c6975-103">How applications appear on hello access panel</span></span>

<span data-ttu-id="c6975-104">Merhaba erişim paneli bir kullanıcı bir iş sağlayan bir web tabanlı portal ya da Okul hesabı Azure Active Directory (Azure AD) tooview ve başlangıç bulut tabanlı uygulamalarda bu hello Azure AD Yöneticisi bunları erişim izni.</span><span class="sxs-lookup"><span data-stu-id="c6975-104">hello Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) tooview and start cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="c6975-105">Bu uygulamalar hello Azure AD portalında hello kullanıcı adına yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="c6975-105">These applications are configured on behalf of hello user in hello Azure AD portal.</span></span> <span data-ttu-id="c6975-106">Hello Yöneticisi hello uygulama toohello kullanıcı doğrudan veya bir kullanıcı hello kullanıcının erişim Panoda görünmesini hello uygulamada kaynaklanan bir parçası olan tooa Grup sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c6975-106">hello admin can provision hello application toohello user directly or tooa group a user is part of resulting in hello application appearing on hello user’s Access Panel.</span></span>

## <a name="general-issues-toocheck-first"></a><span data-ttu-id="c6975-107">Genel toocheck ilk sorunları</span><span class="sxs-lookup"><span data-stu-id="c6975-107">General issues toocheck first</span></span>

-   <span data-ttu-id="c6975-108">Merhaba uygulaması kaldırılırsa bir uygulamayı yalnızca bir kullanıcıdan kaldırıldı veya grup hello kullanıcının üyesi olduğu, toosign giriş ve çıkış yeniden hello kullanıcının erişim paneline sonra birkaç dakika toosee deneyin.</span><span class="sxs-lookup"><span data-stu-id="c6975-108">If an application was just removed from a user or group hello user is a member of, try toosign in and out again into hello user’s Access Panel after a few minutes toosee if hello application is removed.</span></span>

-   <span data-ttu-id="c6975-109">Bir lisans yalnızca bir kullanıcı veya grup hello kullanıcı kaldırıldıysa bu üyesi hello boyutu ve karmaşıklığı yapılan değişiklikleri toobe hello grubunun bağlı olarak uzun bir süre devam edebilir ' dir.</span><span class="sxs-lookup"><span data-stu-id="c6975-109">If a license was just removed from a user or group hello user is a member of this may take a long time, depending on hello size and complexity of hello group for changes toobe made.</span></span> <span data-ttu-id="c6975-110">Erişim paneli hello oturum açmadan önce ek süresi için izin verin.</span><span class="sxs-lookup"><span data-stu-id="c6975-110">Allow for extra time before signing into hello Access Panel.</span></span>

## <a name="problems-related-tooassigning-applications-toousers"></a><span data-ttu-id="c6975-111">Sorunları ilgili tooassigning uygulamaları toousers</span><span class="sxs-lookup"><span data-stu-id="c6975-111">Problems related tooassigning applications toousers</span></span>

<span data-ttu-id="c6975-112">Bunlar daha önce tooit atanmış çünkü bir kullanıcı bir uygulama kullanıcıların erişim panelinde görüyor olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c6975-112">A user may be seeing an application on their Access Panel because they had been previously assigned tooit.</span></span> <span data-ttu-id="c6975-113">Bazı yolları toocheck aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="c6975-113">Below are some ways toocheck:</span></span>

-   [<span data-ttu-id="c6975-114">Bir kullanıcı toohello uygulama atandığından emin olun</span><span class="sxs-lookup"><span data-stu-id="c6975-114">Check if a user is assigned toohello application</span></span>](#check-if-a-user-is-assigned-to-the-application)

-   [<span data-ttu-id="c6975-115">Bir kullanıcının bir lisansı altında olup olmadığını denetleyin ilgili toohello uygulama</span><span class="sxs-lookup"><span data-stu-id="c6975-115">Check if a user is under a license related toohello application</span></span>](#check-if-a-user-is-under-a-license-related-to-the-application)


### <a name="check-if-a-user-is-assigned-toohello-application"></a><span data-ttu-id="c6975-116">Bir kullanıcı toohello uygulama atandığından emin olun</span><span class="sxs-lookup"><span data-stu-id="c6975-116">Check if a user is assigned toohello application</span></span>

<span data-ttu-id="c6975-117">toocheck toohello uygulama atanmış bir kullanıcı yoksa, hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="c6975-117">toocheck if a user is assigned toohello application, follow hello steps below:</span></span>

1.  <span data-ttu-id="c6975-118">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="c6975-118">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="c6975-119">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="c6975-119">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="c6975-120">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="c6975-120">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c6975-121">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="c6975-121">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="c6975-122">Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.</span><span class="sxs-lookup"><span data-stu-id="c6975-122">click **All Applications** tooview a list of all your applications.</span></span>

6.  <span data-ttu-id="c6975-123">**Arama** için söz konusu hello uygulamasının hello adı.</span><span class="sxs-lookup"><span data-stu-id="c6975-123">**Search** for hello name of hello application in question.</span></span>

7.  <span data-ttu-id="c6975-124">tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="c6975-124">click **Users and groups**.</span></span>

8.  <span data-ttu-id="c6975-125">Kullanıcı toohello uygulama atanmışsa toosee denetleyin.</span><span class="sxs-lookup"><span data-stu-id="c6975-125">Check toosee if your user is assigned toohello application.</span></span>

  * <span data-ttu-id="c6975-126">Merhaba uygulamasından tooremove hello kullanıcının istiyorsanız **hello satıra tıklayın** hello kullanıcı seçin ve **silmek**.</span><span class="sxs-lookup"><span data-stu-id="c6975-126">If you want tooremove hello user from hello application, **click hello row** of hello user and select **delete**.</span></span>

### <a name="check-if-a-user-is-under-a-license-related-toohello-application"></a><span data-ttu-id="c6975-127">Bir kullanıcının bir lisansı altında olup olmadığını denetleyin ilgili toohello uygulama</span><span class="sxs-lookup"><span data-stu-id="c6975-127">Check if a user is under a license related toohello application</span></span>

<span data-ttu-id="c6975-128">toocheck bir kullanıcıya ait atanmış lisansların, aşağıdaki hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="c6975-128">toocheck a user’s assigned licenses, follow hello steps below:</span></span>

1.  <span data-ttu-id="c6975-129">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="c6975-129">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="c6975-130">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="c6975-130">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="c6975-131">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="c6975-131">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c6975-132">Tıklatın **kullanıcılar ve gruplar** hello Gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="c6975-132">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="c6975-133">tıklatın **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="c6975-133">click **All users**.</span></span>

6.  <span data-ttu-id="c6975-134">**Arama** ilgilendiğiniz hello kullanıcı için ve **hello satıra tıklayın** tooselect.</span><span class="sxs-lookup"><span data-stu-id="c6975-134">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="c6975-135">tıklatın **lisansları** toosee lisansları hello kullanıcı şu anda atanmış.</span><span class="sxs-lookup"><span data-stu-id="c6975-135">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

   * <span data-ttu-id="c6975-136">Merhaba kullanıcı atanan tooan Office lisansı ise bu etkinleştirin birinci taraf Office uygulamaları tooappear hello kullanıcının erişim panelinde.</span><span class="sxs-lookup"><span data-stu-id="c6975-136">If hello user is assigned tooan Office license this enable First Party Office applications tooappear on hello user’s Access Panel.</span></span>

## <a name="problems-related-tooassigning-applications-toogroups"></a><span data-ttu-id="c6975-137">Sorunları ilgili tooassigning uygulamaları toogroups</span><span class="sxs-lookup"><span data-stu-id="c6975-137">Problems related tooassigning applications toogroups</span></span>

<span data-ttu-id="c6975-138">Merhaba uygulaması atanmış bir grubun parçası olmadığından bir kullanıcı bir uygulama kullanıcıların erişim panelinde görüyor olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c6975-138">A user may be seeing an application on their Access Panel because they are part of a group that has been assigned hello application.</span></span> <span data-ttu-id="c6975-139">Bazı yolları toocheck aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="c6975-139">Below are some ways toocheck:</span></span>

-   [<span data-ttu-id="c6975-140">Bir kullanıcı grup üyeliklerini denetleyin</span><span class="sxs-lookup"><span data-stu-id="c6975-140">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="c6975-141">Bir kullanıcı tooa lisans atanmış bir grup üyesi olup olmadığını denetleyin</span><span class="sxs-lookup"><span data-stu-id="c6975-141">Check if a user is a member of a group assigned tooa license</span></span>](#check-if-a-user-is-a-member-of-a-group-assigned-to-a-license)

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="c6975-142">Bir kullanıcı grup üyeliklerini denetleyin</span><span class="sxs-lookup"><span data-stu-id="c6975-142">Check a user’s group memberships</span></span>

<span data-ttu-id="c6975-143">toocheck bir grubun üyeliğini, aşağıdaki hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="c6975-143">toocheck a group’s membership, follow hello steps below:</span></span>

1.  <span data-ttu-id="c6975-144">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="c6975-144">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="c6975-145">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="c6975-145">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="c6975-146">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="c6975-146">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c6975-147">Tıklatın **kullanıcılar ve gruplar** hello Gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="c6975-147">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="c6975-148">tıklatın **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="c6975-148">click **All users**.</span></span>

6.  <span data-ttu-id="c6975-149">**Arama** ilgilendiğiniz hello kullanıcı için ve **hello satıra tıklayın** tooselect.</span><span class="sxs-lookup"><span data-stu-id="c6975-149">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="c6975-150">tıklatın **gruplar.**</span><span class="sxs-lookup"><span data-stu-id="c6975-150">click **Groups.**</span></span>

8.  <span data-ttu-id="c6975-151">Kullanıcı grubunun bir parçası ise onay toosee toohello uygulama atanır.</span><span class="sxs-lookup"><span data-stu-id="c6975-151">Check toosee if your user is part of a Group assigned toohello application.</span></span>

   * <span data-ttu-id="c6975-152">Merhaba grubundan tooremove hello kullanıcının istiyorsanız **hello satıra tıklayın** hello grubu ve select silin.</span><span class="sxs-lookup"><span data-stu-id="c6975-152">If you want tooremove hello user from hello group, **click hello row** of hello group and select delete.</span></span>

### <a name="check-if-a-user-is-a-member-of-a-group-assigned-tooa-license"></a><span data-ttu-id="c6975-153">Bir kullanıcı tooa lisans atanmış bir grup üyesi olup olmadığını denetleyin</span><span class="sxs-lookup"><span data-stu-id="c6975-153">Check if a user is a member of a group assigned tooa license</span></span>

1.  <span data-ttu-id="c6975-154">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="c6975-154">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="c6975-155">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="c6975-155">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="c6975-156">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="c6975-156">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c6975-157">Tıklatın **kullanıcılar ve gruplar** hello Gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="c6975-157">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="c6975-158">tıklatın **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="c6975-158">click **All users**.</span></span>

6.  <span data-ttu-id="c6975-159">**Arama** ilgilendiğiniz hello kullanıcı için ve **hello satıra tıklayın** tooselect.</span><span class="sxs-lookup"><span data-stu-id="c6975-159">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="c6975-160">tıklatın **gruplar.**</span><span class="sxs-lookup"><span data-stu-id="c6975-160">click **Groups.**</span></span>

8.  <span data-ttu-id="c6975-161">belirli bir grup Hello satırının'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="c6975-161">click hello row of a specific group.</span></span>

9.  <span data-ttu-id="c6975-162">tıklatın **lisansları** toosee hangi lisansları hello Grup tooit atanan.</span><span class="sxs-lookup"><span data-stu-id="c6975-162">click **Licenses** toosee which licenses hello group has assigned tooit.</span></span>

  * <span data-ttu-id="c6975-163">Merhaba grubu atanan tooan Office lisansı ise bu belirli birinci taraf Office uygulamaları tooappear hello kullanıcının erişim panelinde sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="c6975-163">If hello group is assigned tooan Office license this may enable certain First Party Office applications tooappear on hello user’s Access Panel.</span></span>


## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a><span data-ttu-id="c6975-164">Sorun giderme adımları değil hello varsa hello sorunu çözün</span><span class="sxs-lookup"><span data-stu-id="c6975-164">If these troubleshooting steps do not hello resolve hello issue</span></span>

<span data-ttu-id="c6975-165">bir destek bileti varsa aşağıdaki bilgilerle hello ile açın:</span><span class="sxs-lookup"><span data-stu-id="c6975-165">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="c6975-166">Bağıntı hata kimliği</span><span class="sxs-lookup"><span data-stu-id="c6975-166">Correlation error ID</span></span>

-   <span data-ttu-id="c6975-167">UPN (kullanıcı e-posta adresi)</span><span class="sxs-lookup"><span data-stu-id="c6975-167">UPN (user email address)</span></span>

-   <span data-ttu-id="c6975-168">Kiracı Kimliği</span><span class="sxs-lookup"><span data-stu-id="c6975-168">Tenant ID</span></span>

-   <span data-ttu-id="c6975-169">Tarayıcı türü</span><span class="sxs-lookup"><span data-stu-id="c6975-169">Browser type</span></span>

-   <span data-ttu-id="c6975-170">Saat dilimi ve saat/zaman çerçevesine hata oluşuyor</span><span class="sxs-lookup"><span data-stu-id="c6975-170">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="c6975-171">Fiddler izlemeleri</span><span class="sxs-lookup"><span data-stu-id="c6975-171">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="c6975-172">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c6975-172">Next steps</span></span>
[<span data-ttu-id="c6975-173">Azure Active Directory ile uygulamaları yönetme</span><span class="sxs-lookup"><span data-stu-id="c6975-173">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
