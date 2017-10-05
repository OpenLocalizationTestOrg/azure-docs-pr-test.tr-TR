---
title: "Erişim paneli uygulamaları nasıl göründüğünü | Microsoft Docs"
description: "Bir uygulama erişim panelinde görünen neden sorun giderme"
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
ms.openlocfilehash: f8ccf2cf66b49940bc7f2b9f4764020efc04838e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="how-applications-appear-on-the-access-panel"></a><span data-ttu-id="92e98-103">Erişim paneli uygulamaları nasıl göründüğünü</span><span class="sxs-lookup"><span data-stu-id="92e98-103">How applications appear on the access panel</span></span>

<span data-ttu-id="92e98-104">Erişim için bir iş veya Okul hesabı Azure Active Directory'de (görüntülemek ve Azure AD Yöneticisi bunları erişim izni bulut tabanlı uygulamalar başlatmak için Azure AD) olan bir kullanıcı sağlayan bir web tabanlı portal panosudur.</span><span class="sxs-lookup"><span data-stu-id="92e98-104">The Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) to view and start cloud-based applications that the Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="92e98-105">Bu uygulamalar, Azure AD portalında kullanıcı adına yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="92e98-105">These applications are configured on behalf of the user in the Azure AD portal.</span></span> <span data-ttu-id="92e98-106">Yönetici kullanıcının uygulamaya doğrudan sağlayabilir veya bir gruba bir kullanıcı kullanıcının erişim panelinde görünen uygulama sonuçta parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="92e98-106">The admin can provision the application to the user directly or to a group a user is part of resulting in the application appearing on the user’s Access Panel.</span></span>

## <a name="general-issues-to-check-first"></a><span data-ttu-id="92e98-107">İlk denetlemek için genel sorunlar</span><span class="sxs-lookup"><span data-stu-id="92e98-107">General issues to check first</span></span>

-   <span data-ttu-id="92e98-108">Bir uygulamayı yalnızca bir kullanıcı veya kullanıcının üyesi olduğu Grup kaldırıldıysa, içeri ve dışarı kullanıcının erişim paneline birkaç dakika sonra uygulama kaldırılırsa, görmek için oturum yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="92e98-108">If an application was just removed from a user or group the user is a member of, try to sign in and out again into the user’s Access Panel after a few minutes to see if the application is removed.</span></span>

-   <span data-ttu-id="92e98-109">Bir lisans yalnızca bir kullanıcı veya grup kaldırıldıysa bu üyesi boyutu ve karmaşıklığı grubunun yapılacak değişiklikler için bağlı olarak uzun bir süre devam edebilir kullanıcıdır.</span><span class="sxs-lookup"><span data-stu-id="92e98-109">If a license was just removed from a user or group the user is a member of this may take a long time, depending on the size and complexity of the group for changes to be made.</span></span> <span data-ttu-id="92e98-110">Erişim paneline oturum açmadan önce ek süresi için izin verin.</span><span class="sxs-lookup"><span data-stu-id="92e98-110">Allow for extra time before signing into the Access Panel.</span></span>

## <a name="problems-related-to-assigning-applications-to-users"></a><span data-ttu-id="92e98-111">Uygulamaları kullanıcılara atamak için ilgili sorunlar</span><span class="sxs-lookup"><span data-stu-id="92e98-111">Problems related to assigning applications to users</span></span>

<span data-ttu-id="92e98-112">Bunlar daha önce kendisine atanmış çünkü bir kullanıcı bir uygulama kullanıcıların erişim panelinde görüyor olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="92e98-112">A user may be seeing an application on their Access Panel because they had been previously assigned to it.</span></span> <span data-ttu-id="92e98-113">Aşağıda denetlemek için bazı yöntemler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="92e98-113">Below are some ways to check:</span></span>

-   [<span data-ttu-id="92e98-114">Kullanıcı uygulamaya atandığından emin olun</span><span class="sxs-lookup"><span data-stu-id="92e98-114">Check if a user is assigned to the application</span></span>](#check-if-a-user-is-assigned-to-the-application)

-   [<span data-ttu-id="92e98-115">Bir kullanıcının uygulamayla ilgili bir lisansı altında olup olmadığını denetleyin</span><span class="sxs-lookup"><span data-stu-id="92e98-115">Check if a user is under a license related to the application</span></span>](#check-if-a-user-is-under-a-license-related-to-the-application)


### <a name="check-if-a-user-is-assigned-to-the-application"></a><span data-ttu-id="92e98-116">Kullanıcı uygulamaya atandığından emin olun</span><span class="sxs-lookup"><span data-stu-id="92e98-116">Check if a user is assigned to the application</span></span>

<span data-ttu-id="92e98-117">Kullanıcı uygulamaya atanıp atanmadığını denetlemek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="92e98-117">To check if a user is assigned to the application, follow the steps below:</span></span>

1.  <span data-ttu-id="92e98-118">Açık [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="92e98-118">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="92e98-119">Açık **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** ana sol taraftaki gezinti menüsünde sonundaki.</span><span class="sxs-lookup"><span data-stu-id="92e98-119">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="92e98-120">Yazın **"Azure Active Directory**" Filtre Arama kutusuna seçip **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="92e98-120">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="92e98-121">tıklatın **kurumsal uygulamalar** Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="92e98-121">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="92e98-122">tıklatın **tüm uygulamaları** tüm uygulamaların bir listesini görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="92e98-122">click **All Applications** to view a list of all your applications.</span></span>

6.  <span data-ttu-id="92e98-123">**Arama** için söz konusu uygulamanın adı.</span><span class="sxs-lookup"><span data-stu-id="92e98-123">**Search** for the name of the application in question.</span></span>

7.  <span data-ttu-id="92e98-124">tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="92e98-124">click **Users and groups**.</span></span>

8.  <span data-ttu-id="92e98-125">Kullanıcı uygulamaya atanıp atanmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="92e98-125">Check to see if your user is assigned to the application.</span></span>

  * <span data-ttu-id="92e98-126">Uygulamasından kullanıcıyı kaldırmak istiyorsanız, **satıra tıklayın** seçin ve kullanıcı **silmek**.</span><span class="sxs-lookup"><span data-stu-id="92e98-126">If you want to remove the user from the application, **click the row** of the user and select **delete**.</span></span>

### <a name="check-if-a-user-is-under-a-license-related-to-the-application"></a><span data-ttu-id="92e98-127">Bir kullanıcının uygulamayla ilgili bir lisansı altında olup olmadığını denetleyin</span><span class="sxs-lookup"><span data-stu-id="92e98-127">Check if a user is under a license related to the application</span></span>

<span data-ttu-id="92e98-128">Bir kullanıcının atanan lisansları denetlemek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="92e98-128">To check a user’s assigned licenses, follow the steps below:</span></span>

1.  <span data-ttu-id="92e98-129">Açık [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="92e98-129">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="92e98-130">Açık **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** ana sol taraftaki gezinti menüsünde sonundaki.</span><span class="sxs-lookup"><span data-stu-id="92e98-130">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="92e98-131">Yazın **"Azure Active Directory**" Filtre Arama kutusuna seçip **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="92e98-131">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="92e98-132">tıklatın **kullanıcılar ve gruplar** Gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="92e98-132">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="92e98-133">tıklatın **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="92e98-133">click **All users**.</span></span>

6.  <span data-ttu-id="92e98-134">**Arama** ilgilendiğiniz kullanıcı için ve **satıra tıklayın** seçin.</span><span class="sxs-lookup"><span data-stu-id="92e98-134">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="92e98-135">tıklatın **lisansları** , şu anda kullanıcı lisansları görmek üzere atanır.</span><span class="sxs-lookup"><span data-stu-id="92e98-135">click **Licenses** to see which licenses the user currently has assigned.</span></span>

   * <span data-ttu-id="92e98-136">Kullanıcı bir Office atanırsa, kullanıcının erişim panelinde için bu etkinleştir birinci taraf Office uygulamalarını lisans.</span><span class="sxs-lookup"><span data-stu-id="92e98-136">If the user is assigned to an Office license this enable First Party Office applications to appear on the user’s Access Panel.</span></span>

## <a name="problems-related-to-assigning-applications-to-groups"></a><span data-ttu-id="92e98-137">Gruplarına atamayla ilgili sorunlar</span><span class="sxs-lookup"><span data-stu-id="92e98-137">Problems related to assigning applications to groups</span></span>

<span data-ttu-id="92e98-138">Uygulama atanmış bir grubun parçası olmadığından bir kullanıcı bir uygulama kullanıcıların erişim panelinde görüyor olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="92e98-138">A user may be seeing an application on their Access Panel because they are part of a group that has been assigned the application.</span></span> <span data-ttu-id="92e98-139">Aşağıda denetlemek için bazı yöntemler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="92e98-139">Below are some ways to check:</span></span>

-   [<span data-ttu-id="92e98-140">Bir kullanıcı grup üyeliklerini denetleyin</span><span class="sxs-lookup"><span data-stu-id="92e98-140">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="92e98-141">Bir kullanıcı için bir lisans atanması grubunun bir üyesi olup olmadığını denetleyin</span><span class="sxs-lookup"><span data-stu-id="92e98-141">Check if a user is a member of a group assigned to a license</span></span>](#check-if-a-user-is-a-member-of-a-group-assigned-to-a-license)

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="92e98-142">Bir kullanıcı grup üyeliklerini denetleyin</span><span class="sxs-lookup"><span data-stu-id="92e98-142">Check a user’s group memberships</span></span>

<span data-ttu-id="92e98-143">Bir grubun üyeliğini denetlemek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="92e98-143">To check a group’s membership, follow the steps below:</span></span>

1.  <span data-ttu-id="92e98-144">Açık [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="92e98-144">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="92e98-145">Açık **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** ana sol taraftaki gezinti menüsünde sonundaki.</span><span class="sxs-lookup"><span data-stu-id="92e98-145">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="92e98-146">Yazın **"Azure Active Directory**" Filtre Arama kutusuna seçip **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="92e98-146">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="92e98-147">tıklatın **kullanıcılar ve gruplar** Gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="92e98-147">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="92e98-148">tıklatın **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="92e98-148">click **All users**.</span></span>

6.  <span data-ttu-id="92e98-149">**Arama** ilgilendiğiniz kullanıcı için ve **satıra tıklayın** seçin.</span><span class="sxs-lookup"><span data-stu-id="92e98-149">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="92e98-150">tıklatın **gruplar.**</span><span class="sxs-lookup"><span data-stu-id="92e98-150">click **Groups.**</span></span>

8.  <span data-ttu-id="92e98-151">Kullanıcı uygulamaya atanan bir grubun parçası olup olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="92e98-151">Check to see if your user is part of a Group assigned to the application.</span></span>

   * <span data-ttu-id="92e98-152">Kullanıcıyı gruptan kaldırmak istiyorsanız, **satıra tıklayın** seçin ve Grup DELETE.</span><span class="sxs-lookup"><span data-stu-id="92e98-152">If you want to remove the user from the group, **click the row** of the group and select delete.</span></span>

### <a name="check-if-a-user-is-a-member-of-a-group-assigned-to-a-license"></a><span data-ttu-id="92e98-153">Bir kullanıcı için bir lisans atanması grubunun bir üyesi olup olmadığını denetleyin</span><span class="sxs-lookup"><span data-stu-id="92e98-153">Check if a user is a member of a group assigned to a license</span></span>

1.  <span data-ttu-id="92e98-154">Açık [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="92e98-154">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="92e98-155">Açık **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** ana sol taraftaki gezinti menüsünde sonundaki.</span><span class="sxs-lookup"><span data-stu-id="92e98-155">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="92e98-156">Yazın **"Azure Active Directory**" Filtre Arama kutusuna seçip **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="92e98-156">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="92e98-157">tıklatın **kullanıcılar ve gruplar** Gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="92e98-157">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="92e98-158">tıklatın **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="92e98-158">click **All users**.</span></span>

6.  <span data-ttu-id="92e98-159">**Arama** ilgilendiğiniz kullanıcı için ve **satıra tıklayın** seçin.</span><span class="sxs-lookup"><span data-stu-id="92e98-159">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="92e98-160">tıklatın **gruplar.**</span><span class="sxs-lookup"><span data-stu-id="92e98-160">click **Groups.**</span></span>

8.  <span data-ttu-id="92e98-161">belirli bir grup satıra tıklayın.</span><span class="sxs-lookup"><span data-stu-id="92e98-161">click the row of a specific group.</span></span>

9.  <span data-ttu-id="92e98-162">tıklatın **lisansları** hangi grubun lisansları görmek için atanır.</span><span class="sxs-lookup"><span data-stu-id="92e98-162">click **Licenses** to see which licenses the group has assigned to it.</span></span>

  * <span data-ttu-id="92e98-163">Bu kullanıcının erişim panelinde için belirli birinci taraf Office uygulamalarını etkinleştirebilir bir Office lisansı için Grup atanmışsa.</span><span class="sxs-lookup"><span data-stu-id="92e98-163">If the group is assigned to an Office license this may enable certain First Party Office applications to appear on the user’s Access Panel.</span></span>


## <a name="if-these-troubleshooting-steps-do-not-the-resolve-the-issue"></a><span data-ttu-id="92e98-164">Bu sorun giderme adımları sorunu çözümleme yaparsanız</span><span class="sxs-lookup"><span data-stu-id="92e98-164">If these troubleshooting steps do not the resolve the issue</span></span>

<span data-ttu-id="92e98-165">bir destek bileti aşağıdaki bilgilerle varsa açın:</span><span class="sxs-lookup"><span data-stu-id="92e98-165">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="92e98-166">Bağıntı hata kimliği</span><span class="sxs-lookup"><span data-stu-id="92e98-166">Correlation error ID</span></span>

-   <span data-ttu-id="92e98-167">UPN (kullanıcı e-posta adresi)</span><span class="sxs-lookup"><span data-stu-id="92e98-167">UPN (user email address)</span></span>

-   <span data-ttu-id="92e98-168">Kiracı Kimliği</span><span class="sxs-lookup"><span data-stu-id="92e98-168">Tenant ID</span></span>

-   <span data-ttu-id="92e98-169">Tarayıcı türü</span><span class="sxs-lookup"><span data-stu-id="92e98-169">Browser type</span></span>

-   <span data-ttu-id="92e98-170">Saat dilimi ve saat/zaman çerçevesine hata oluşuyor</span><span class="sxs-lookup"><span data-stu-id="92e98-170">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="92e98-171">Fiddler izlemeleri</span><span class="sxs-lookup"><span data-stu-id="92e98-171">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="92e98-172">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="92e98-172">Next steps</span></span>
[<span data-ttu-id="92e98-173">Azure Active Directory ile uygulamaları yönetme</span><span class="sxs-lookup"><span data-stu-id="92e98-173">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
