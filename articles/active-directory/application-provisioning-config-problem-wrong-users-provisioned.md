---
title: "Kullanıcı yanlış kümesi, bir Azure AD galeri uygulamaya sağlanan | Microsoft Docs"
description: "Neden farklı bir kullanıcı kümesini sağlanan bir uygulamaya beklediğiniz olandan öğrenmek öğrenin"
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
ms.openlocfilehash: 85b533584c8ec15a23be32e20db7de583fced6a0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="wrong-set-of-users-are-being-provisioned-to-an-azure-ad-gallery-application"></a><span data-ttu-id="e765f-103">Kullanıcı yanlış kümesi, bir Azure AD galeri uygulamaya sağlanan</span><span class="sxs-lookup"><span data-stu-id="e765f-103">Wrong set of users are being provisioned to an Azure AD Gallery application</span></span>

<span data-ttu-id="e765f-104">Hangi kullanıcıların uygulama için sağlanan öncelikle hangi kullanıcıların ve grupların silinmiş tarafından yönetilir **atanan** uygulama.</span><span class="sxs-lookup"><span data-stu-id="e765f-104">Which users are provisioned to the app is primarily driven by which users and groups have been **assigned** to the application.</span></span>

<span data-ttu-id="e765f-105">Hangi kullanıcıların ve grupların Azure Active Directory içinde bir uygulama atanmış denetlemek öğrenmek için aşağıdaki kaynakları kullanın.</span><span class="sxs-lookup"><span data-stu-id="e765f-105">Use the resources below to learn how to check which users and groups have been assigned to an application within Azure Active Directory.</span></span>

## <a name="assign-a-user-directly-as-an-administrator"></a><span data-ttu-id="e765f-106">Yönetici doğrudan kullanıcı atama</span><span class="sxs-lookup"><span data-stu-id="e765f-106">Assign a user directly as an administrator</span></span>

<span data-ttu-id="e765f-107">Bir veya daha fazla kullanıcının uygulamaya doğrudan atamak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="e765f-107">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="e765f-108">Açık [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="e765f-108">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="e765f-109">Açık **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** ana sol taraftaki gezinti menüsünde sonundaki.</span><span class="sxs-lookup"><span data-stu-id="e765f-109">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e765f-110">Yazın **"Azure Active Directory**" Filtre Arama kutusuna seçip **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="e765f-110">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e765f-111">tıklatın **kurumsal uygulamalar** Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="e765f-111">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="e765f-112">tıklatın **tüm uygulamaları** tüm uygulamaların bir listesini görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="e765f-112">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="e765f-113">Burada gösterisini istediğiniz uygulama görmüyorsanız kullanın **filtre** üst kısmındaki denetim **tüm uygulamalar listesini** ve **Göster** için seçenek **tüm uygulamaları.**</span><span class="sxs-lookup"><span data-stu-id="e765f-113">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="e765f-114">Listeden bir kullanıcıya atamak istediğiniz uygulamayı seçin.</span><span class="sxs-lookup"><span data-stu-id="e765f-114">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="e765f-115">Uygulamanın yüklediği sonra tıklayın **kullanıcılar ve gruplar** uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="e765f-115">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="e765f-116">Tıklatın **Ekle** üstünde düğmesini **kullanıcılar ve gruplar** açmak için liste **eklemek atama** dikey.</span><span class="sxs-lookup"><span data-stu-id="e765f-116">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="e765f-117">tıklatın **kullanıcılar ve gruplar** seçicisini **eklemek atama** dikey.</span><span class="sxs-lookup"><span data-stu-id="e765f-117">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="e765f-118">Yazın **tam adı** veya **e-posta adresi** içine atama ilgilenen kullanıcının **ad veya e-posta adresine göre arama** arama kutusu.</span><span class="sxs-lookup"><span data-stu-id="e765f-118">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="e765f-119">Üzerine gelerek **kullanıcı** ortaya çıkarmak için listedeki bir **onay kutusunu**.</span><span class="sxs-lookup"><span data-stu-id="e765f-119">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="e765f-120">Kullanıcının profil fotoğrafınız veya logosu, kullanıcı eklemek için yanındaki onay kutusuna tıklayın **seçili** listesi.</span><span class="sxs-lookup"><span data-stu-id="e765f-120">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="e765f-121">**İsteğe bağlı:** başlamayı tercih ederseniz **birden fazla kullanıcı ekleme**, başka bir tür **tam adı** veya **e-posta adresi** içine **ad veya e-posta adresine göre arama** arama kutusu ve bu kullanıcıyı eklemek için onay kutusunu işaretleyin **seçili** listesi.</span><span class="sxs-lookup"><span data-stu-id="e765f-121">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="e765f-122">Kullanıcıların seçerek bittiğinde tıklatın **seçin** düğmesi uygulamaya atanan kullanıcılar ve gruplar listesi eklemek için.</span><span class="sxs-lookup"><span data-stu-id="e765f-122">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="e765f-123">**İsteğe bağlı:** tıklatın **rolü Seç** seçicide **eklemek atama** seçtiğiniz kullanıcılara atamak için bir rol seçin dikey.</span><span class="sxs-lookup"><span data-stu-id="e765f-123">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="e765f-124">Tıklatın **atamak** uygulamayı Seçilen kullanıcılara atamak için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e765f-124">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="e765f-125">Sağlama yapılandırılmış ve bir uygulama zaten çalışıyor ise, yeni kullanıcılar yaklaşık 10 dakika içinde bir uygulama için hazırlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e765f-125">If provisioning is configured and already running for an app, new users should be provisioned to an application in approximately 10 minutes.</span></span> <span data-ttu-id="e765f-126">Denetleme **denetim günlüklerini** Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="e765f-126">Check the **Audit Logs** for details.</span></span>

## <a name="assign-a-group-directly-to-an-application-as-an-administrator"></a><span data-ttu-id="e765f-127">Yönetici olarak bir uygulamaya doğrudan bir gruba atamak</span><span class="sxs-lookup"><span data-stu-id="e765f-127">Assign a group directly to an application as an administrator</span></span>

<span data-ttu-id="e765f-128">Bir veya daha fazla grupları doğrudan bir uygulamaya atamak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="e765f-128">To assign one or more groups to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="e765f-129">Açık [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="e765f-129">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="e765f-130">Açık **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** ana sol taraftaki gezinti menüsünde sonundaki.</span><span class="sxs-lookup"><span data-stu-id="e765f-130">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e765f-131">Yazın **"Azure Active Directory**" Filtre Arama kutusuna seçip **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="e765f-131">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e765f-132">tıklatın **kurumsal uygulamalar** Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="e765f-132">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="e765f-133">tıklatın **tüm uygulamaları** tüm uygulamaların bir listesini görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="e765f-133">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="e765f-134">Burada gösterisini istediğiniz uygulama görmüyorsanız kullanın **filtre** üst kısmındaki denetim **tüm uygulamalar listesini** ve **Göster** için seçenek **tüm uygulamaları.**</span><span class="sxs-lookup"><span data-stu-id="e765f-134">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="e765f-135">Listeden bir kullanıcıya atamak istediğiniz uygulamayı seçin.</span><span class="sxs-lookup"><span data-stu-id="e765f-135">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="e765f-136">Uygulamanın yüklediği sonra tıklayın **kullanıcılar ve gruplar** uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="e765f-136">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="e765f-137">Tıklatın **Ekle** üstünde düğmesini **kullanıcılar ve gruplar** açmak için liste **eklemek atama** dikey.</span><span class="sxs-lookup"><span data-stu-id="e765f-137">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="e765f-138">tıklatın **kullanıcılar ve gruplar** seçicisini **eklemek atama** dikey.</span><span class="sxs-lookup"><span data-stu-id="e765f-138">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="e765f-139">Yazın **tam grup adı** içine atama ilgilenen grubunun **ad veya e-posta adresine göre arama** arama kutusu.</span><span class="sxs-lookup"><span data-stu-id="e765f-139">Type in the **full group name** of the group you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="e765f-140">Üzerine gelerek **grup** ortaya çıkarmak için listedeki bir **onay kutusunu**.</span><span class="sxs-lookup"><span data-stu-id="e765f-140">Hover over the **group** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="e765f-141">Grubun profil fotoğrafınız veya logosu, kullanıcı eklemek için yanındaki onay kutusuna tıklayın **seçili** listesi.</span><span class="sxs-lookup"><span data-stu-id="e765f-141">Click the checkbox next to the group’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="e765f-142">**İsteğe bağlı:** başlamayı tercih ederseniz **birden fazla grubu Ekle**, başka bir tür **tam grup adı** içine **ad veya e-posta adresine göre arama** arama kutusu ve bu gruba eklemek için onay kutusunu işaretleyin **seçili** listesi.</span><span class="sxs-lookup"><span data-stu-id="e765f-142">**Optional:** If you would like to **add more than one group**, type in another **full group name** into the **Search by name or email address** search box, and click the checkbox to add this group to the **Selected** list.</span></span>

13. <span data-ttu-id="e765f-143">Grupları seçmek bittiğinde tıklatın **seçin** düğmesi uygulamaya atanan kullanıcılar ve gruplar listesi eklemek için.</span><span class="sxs-lookup"><span data-stu-id="e765f-143">When you are finished selecting groups, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="e765f-144">**İsteğe bağlı:** tıklatın **rolü Seç** seçicide **eklemek atama** seçtiğiniz gruplarına atamak için bir rol seçin dikey.</span><span class="sxs-lookup"><span data-stu-id="e765f-144">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the groups you have selected.</span></span>

15. <span data-ttu-id="e765f-145">Tıklatın **atamak** seçilen grupları uygulamaya atamak için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e765f-145">Click the **Assign** button to assign the application to the selected groups.</span></span>

<span data-ttu-id="e765f-146">Sağlama yapılandırılmış ve bir uygulama zaten çalışıyor ise, yeni kullanıcılar grubunda yer alan yaklaşık 10 dakika içinde bir uygulama için hazırlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e765f-146">If provisioning is configured and already running for an app, new users contained within the group should be provisioned to an application in approximately 10 minutes.</span></span> <span data-ttu-id="e765f-147">Denetleme **denetim günlüklerini** Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="e765f-147">Check the **Audit Logs** for details.</span></span>

>[!IMPORTANT]
><span data-ttu-id="e765f-148">Grup adı ve üyeleri yanı sıra Grup ayrıntılarını bazı uygulamalar için destekleniyorsa sağlama.</span><span class="sxs-lookup"><span data-stu-id="e765f-148">Provisioning of the group name and group details, in addition to the members, if supported for some applications.</span></span> <span data-ttu-id="e765f-149">Etkinleştirmek veya bu işlevi etkinleştirmek veya devre dışı bırakarak devre dışı **eşleme** gösterilen grubu nesnelerinin **sağlama** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="e765f-149">You can enable or disable this functionality by enabling or disabling the **Mapping** for group objects shown in the **Provisioning** tab.</span></span> 
>
>

<span data-ttu-id="e765f-150">Grupları sağlama etkinse, uygun bir alan "Eşleşen kimliği" kullanıldığından emin olmak için öznitelik eşlemelerini gözden geçirmeyi unutmayın.</span><span class="sxs-lookup"><span data-stu-id="e765f-150">If provisioning groups is enabled, be sure to review the attribute mappings to ensure an appropriate field is being used for the “matching ID”.</span></span> <span data-ttu-id="e765f-151">Bu görünen ad olabilir ve e-posta diğer adı veya eşleşen özellik boşsa, Grup ve üyelerini sağlanması değil gibi bir grup için Azure AD içinde doldurulamaz.</span><span class="sxs-lookup"><span data-stu-id="e765f-151">This can be the display name or email alias, as the group and its members not be provisioned if the matching property is empty or not populated for a group in Azure AD.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e765f-152">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e765f-152">Next steps</span></span>
[<span data-ttu-id="e765f-153">Kullanıcı sağlama ve Azure Active Directory ile SaaS uygulamalarına sağlamayı otomatikleştirme</span><span class="sxs-lookup"><span data-stu-id="e765f-153">Automate User Provisioning and Deprovisioning to SaaS Applications with Azure Active Directory</span></span>](active-directory-saas-app-provisioning.md)
