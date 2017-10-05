---
title: "Kullanıcılar ve gruplar için bir uygulama atama | Microsoft Docs"
description: "Kullanıcılara erişim vermek için uygulamaya atayın"
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
ms.openlocfilehash: 61536612e0dd5102b8f5e911c350826846f5ed77
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-assign-users-and-groups-to-an-application"></a><span data-ttu-id="80b3c-103">Kullanıcılar ve gruplar için bir uygulama atama</span><span class="sxs-lookup"><span data-stu-id="80b3c-103">How to assign users and groups to an application</span></span>

<span data-ttu-id="80b3c-104">Kullanıcılarınızın herhangi birini yapmak için önce aşağıdaki belirli bir uygulama için ilk için gereksinim duyduğunuz **uygulamaya atamak** erişim vermek için:</span><span class="sxs-lookup"><span data-stu-id="80b3c-104">Before your users can do any of the below for a specific application, you need to first **assign them to the application** to grant them access:</span></span>

-   <span data-ttu-id="80b3c-105">Bir uygulama tarafından erişim **doğrudan uygulamanın URL'ye geçerken** (olarak da bilinen SP tarafından başlatılan oturum açma).</span><span class="sxs-lookup"><span data-stu-id="80b3c-105">Access an application by **navigating to the application’s URL directly** (also known as SP-initiated sign-on).</span></span>

-   <span data-ttu-id="80b3c-106">Kullanarak bir uygulamaya erişim **kullanıcı erişim URL'si** bir uygulamanın üzerinde **özellikleri** sayfa (olarak da bilinen IDP başlatılan oturum açma).</span><span class="sxs-lookup"><span data-stu-id="80b3c-106">Access an application by using the **User Access URL** on an application’s **Properties** page (also known as IDP-initiated sign on).</span></span>

-   <span data-ttu-id="80b3c-107">Görünür bir uygulama bkz kendi [uygulama erişim Paneli'ne](https://myapps.microsoft.com/) ya da mobil uygulama.</span><span class="sxs-lookup"><span data-stu-id="80b3c-107">See an application appear on their [Application Access Panel](https://myapps.microsoft.com/) or mobile application.</span></span>

-   <span data-ttu-id="80b3c-108">Görünür bir uygulama bkz kendi [Office 365 uygulama Başlatıcı](https://support.office.com/article/Meet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a).</span><span class="sxs-lookup"><span data-stu-id="80b3c-108">See an application appear on their [Office 365 Application Launcher](https://support.office.com/article/Meet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a).</span></span>

## <a name="methods-to-assign-applications-with-azure-active-directory"></a><span data-ttu-id="80b3c-109">Azure Active Directory ile uygulamaları atamak için yöntemleri</span><span class="sxs-lookup"><span data-stu-id="80b3c-109">Methods to assign applications with Azure Active Directory</span></span> 

<span data-ttu-id="80b3c-110">Azure Active Directory ile uygulamaları atayabilirsiniz 3 yolu vardır:</span><span class="sxs-lookup"><span data-stu-id="80b3c-110">There are 3 ways you can assign applications with Azure Active Directory:</span></span>

-   [<span data-ttu-id="80b3c-111">Yönetici olarak bir uygulamaya doğrudan kullanıcı atama</span><span class="sxs-lookup"><span data-stu-id="80b3c-111">Assign a user directly to an application as an administrator</span></span>](#assign-a-user-directly-as-an-administrator)

-   [<span data-ttu-id="80b3c-112">Yönetici olarak bir uygulamaya doğrudan bir gruba atamak</span><span class="sxs-lookup"><span data-stu-id="80b3c-112">Assign a group directly to an application as an administrator</span></span>](#assign-a-group-directly-to-an-application-as-an-administrator)

-   [<span data-ttu-id="80b3c-113">Kullanıcıların kendi uygulamalarını bulmak izin vermek Self Servis uygulama erişimini etkinleştir</span><span class="sxs-lookup"><span data-stu-id="80b3c-113">Enable self-service application access to allow users to find their own applications</span></span>](#enable-self-service-application-access-to-allow-users-to-find-their-own-applications)

## <a name="assign-a-user-directly-as-an-administrator"></a><span data-ttu-id="80b3c-114">Yönetici doğrudan kullanıcı atama</span><span class="sxs-lookup"><span data-stu-id="80b3c-114">Assign a user directly as an administrator</span></span>

<span data-ttu-id="80b3c-115">Bir veya daha fazla kullanıcının uygulamaya doğrudan atamak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="80b3c-115">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="80b3c-116">Açık [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="80b3c-116">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="80b3c-117">Açık **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** ana sol taraftaki gezinti menüsünde sonundaki.</span><span class="sxs-lookup"><span data-stu-id="80b3c-117">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="80b3c-118">Yazın **"Azure Active Directory**" Filtre Arama kutusuna seçip **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="80b3c-118">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="80b3c-119">tıklatın **kurumsal uygulamalar** Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="80b3c-119">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="80b3c-120">tıklatın **tüm uygulamaları** tüm uygulamaların bir listesini görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="80b3c-120">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="80b3c-121">Burada gösterisini istediğiniz uygulama görmüyorsanız kullanın **filtre** üst kısmındaki denetim **tüm uygulamalar listesini** ve **Göster** için seçenek **tüm uygulamaları.**</span><span class="sxs-lookup"><span data-stu-id="80b3c-121">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="80b3c-122">Listeden bir kullanıcıya atamak istediğiniz uygulamayı seçin.</span><span class="sxs-lookup"><span data-stu-id="80b3c-122">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="80b3c-123">Uygulamanın yüklediği sonra tıklayın **kullanıcılar ve gruplar** uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="80b3c-123">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="80b3c-124">Tıklatın **Ekle** üstünde düğmesini **kullanıcılar ve gruplar** açmak için liste **eklemek atama** dikey.</span><span class="sxs-lookup"><span data-stu-id="80b3c-124">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="80b3c-125">tıklatın **kullanıcılar ve gruplar** seçicisini **eklemek atama** dikey.</span><span class="sxs-lookup"><span data-stu-id="80b3c-125">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="80b3c-126">Yazın **tam adı** veya **e-posta adresi** içine atama ilgilenen kullanıcının **ad veya e-posta adresine göre arama** arama kutusu.</span><span class="sxs-lookup"><span data-stu-id="80b3c-126">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="80b3c-127">Üzerine gelerek **kullanıcı** ortaya çıkarmak için listedeki bir **onay kutusunu**.</span><span class="sxs-lookup"><span data-stu-id="80b3c-127">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="80b3c-128">Kullanıcının profil fotoğrafınız veya logosu, kullanıcı eklemek için yanındaki onay kutusuna tıklayın **seçili** listesi.</span><span class="sxs-lookup"><span data-stu-id="80b3c-128">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="80b3c-129">**İsteğe bağlı:** başlamayı tercih ederseniz **birden fazla kullanıcı ekleme**, başka bir tür **tam adı** veya **e-posta adresi** içine **ad veya e-posta adresine göre arama** arama kutusu ve bu kullanıcıyı eklemek için onay kutusunu işaretleyin **seçili** listesi.</span><span class="sxs-lookup"><span data-stu-id="80b3c-129">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="80b3c-130">Kullanıcıların seçerek bittiğinde tıklatın **seçin** düğmesi uygulamaya atanan kullanıcılar ve gruplar listesi eklemek için.</span><span class="sxs-lookup"><span data-stu-id="80b3c-130">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="80b3c-131">**İsteğe bağlı:** tıklatın **rolü Seç** seçicide **eklemek atama** seçtiğiniz kullanıcılara atamak için bir rol seçin dikey.</span><span class="sxs-lookup"><span data-stu-id="80b3c-131">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="80b3c-132">Tıklatın **atamak** uygulamayı Seçilen kullanıcılara atamak için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="80b3c-132">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="80b3c-133">Bir kısa süre sonra seçtiğiniz kullanıcıların çözüm Açıklama bölümünde açıklanan yöntemleri kullanarak bu uygulamaları başlatabilir.</span><span class="sxs-lookup"><span data-stu-id="80b3c-133">After a short period of time, the users you have selected be able to launch these applications using the methods described in the solution description section.</span></span>

## <a name="assign-a-group-directly-to-an-application-as-an-administrator"></a><span data-ttu-id="80b3c-134">Yönetici olarak bir uygulamaya doğrudan bir gruba atamak</span><span class="sxs-lookup"><span data-stu-id="80b3c-134">Assign a group directly to an application as an administrator</span></span>

<span data-ttu-id="80b3c-135">Bir veya daha fazla grupları doğrudan bir uygulamaya atamak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="80b3c-135">To assign one or more groups to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="80b3c-136">Açık [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="80b3c-136">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="80b3c-137">Açık **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** ana sol taraftaki gezinti menüsünde sonundaki.</span><span class="sxs-lookup"><span data-stu-id="80b3c-137">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="80b3c-138">Yazın **"Azure Active Directory**" Filtre Arama kutusuna seçip **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="80b3c-138">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="80b3c-139">tıklatın **kurumsal uygulamalar** Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="80b3c-139">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="80b3c-140">tıklatın **tüm uygulamaları** tüm uygulamaların bir listesini görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="80b3c-140">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="80b3c-141">Burada gösterisini istediğiniz uygulama görmüyorsanız kullanın **filtre** üst kısmındaki denetim **tüm uygulamalar listesini** ve **Göster** için seçenek **tüm uygulamaları.**</span><span class="sxs-lookup"><span data-stu-id="80b3c-141">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="80b3c-142">Listeden bir kullanıcıya atamak istediğiniz uygulamayı seçin.</span><span class="sxs-lookup"><span data-stu-id="80b3c-142">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="80b3c-143">Uygulamanın yüklediği sonra tıklayın **kullanıcılar ve gruplar** uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="80b3c-143">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="80b3c-144">Tıklatın **Ekle** üstünde düğmesini **kullanıcılar ve gruplar** açmak için liste **eklemek atama** dikey.</span><span class="sxs-lookup"><span data-stu-id="80b3c-144">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="80b3c-145">tıklatın **kullanıcılar ve gruplar** seçicisini **eklemek atama** dikey.</span><span class="sxs-lookup"><span data-stu-id="80b3c-145">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="80b3c-146">Yazın **tam grup adı** içine atama ilgilenen grubunun **ad veya e-posta adresine göre arama** arama kutusu.</span><span class="sxs-lookup"><span data-stu-id="80b3c-146">Type in the **full group name** of the group you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="80b3c-147">Üzerine gelerek **grup** ortaya çıkarmak için listedeki bir **onay kutusunu**.</span><span class="sxs-lookup"><span data-stu-id="80b3c-147">Hover over the **group** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="80b3c-148">Grubun profil fotoğrafınız veya logosu, kullanıcı eklemek için yanındaki onay kutusuna tıklayın **seçili** listesi.</span><span class="sxs-lookup"><span data-stu-id="80b3c-148">Click the checkbox next to the group’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="80b3c-149">**İsteğe bağlı:** başlamayı tercih ederseniz **birden fazla grubu Ekle**, başka bir tür **tam grup adı** içine **ad veya e-posta adresine göre arama** arama kutusu ve bu gruba eklemek için onay kutusunu işaretleyin **seçili** listesi.</span><span class="sxs-lookup"><span data-stu-id="80b3c-149">**Optional:** If you would like to **add more than one group**, type in another **full group name** into the **Search by name or email address** search box, and click the checkbox to add this group to the **Selected** list.</span></span>

13. <span data-ttu-id="80b3c-150">Grupları seçmek bittiğinde tıklatın **seçin** düğmesi uygulamaya atanan kullanıcılar ve gruplar listesi eklemek için.</span><span class="sxs-lookup"><span data-stu-id="80b3c-150">When you are finished selecting groups, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="80b3c-151">**İsteğe bağlı:** tıklatın **rolü Seç** seçicide **eklemek atama** seçtiğiniz gruplarına atamak için bir rol seçin dikey.</span><span class="sxs-lookup"><span data-stu-id="80b3c-151">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the groups you have selected.</span></span>

15. <span data-ttu-id="80b3c-152">Tıklatın **atamak** seçilen grupları uygulamaya atamak için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="80b3c-152">Click the **Assign** button to assign the application to the selected groups.</span></span>

<span data-ttu-id="80b3c-153">Bir kısa süre sonra kullanıcılar seçtiğiniz grupları içindeki çözüm Açıklama bölümünde açıklanan yöntemleri kullanarak bu uygulamaları başlatabilir.</span><span class="sxs-lookup"><span data-stu-id="80b3c-153">After a short period of time, the users within the groups you have selected be able to launch these applications using the methods described in the solution description section.</span></span> <span data-ttu-id="80b3c-154">Bu dinamik grupların varsa, bazı ek işleme gecikme olabilir bu grupları atanan içindeki kullanıcılar için görünen bu atamaları içinde.</span><span class="sxs-lookup"><span data-stu-id="80b3c-154">If these are dynamic groups, there may be some additional processing delay in these assignments appearing for users within these assigned groups.</span></span>

## <a name="enable-self-service-application-access-to-allow-users-to-find-their-own-applications"></a><span data-ttu-id="80b3c-155">Kullanıcıların kendi uygulamalarını bulmak izin vermek Self Servis uygulama erişimini etkinleştir</span><span class="sxs-lookup"><span data-stu-id="80b3c-155">Enable self-service application access to allow users to find their own applications</span></span>

<span data-ttu-id="80b3c-156">Self Servis uygulamaya erişim uygulamaları, kendi kendine Bul yapmalarına izin vermek için mükemmel bir yoldur bu uygulamalara erişimi onaylamak için iş grubuna isteğe bağlı olarak sağlar.</span><span class="sxs-lookup"><span data-stu-id="80b3c-156">Self-service application access is a great way to allow users to self-discover applications, optionally allow the business group to approve access to those applications.</span></span> <span data-ttu-id="80b3c-157">Bu kullanıcılar için parola çoklu oturum uygulamalar üzerinde sağ bunların erişim paneller atanan kimlik bilgilerini yönetmek iş grubuna izin verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="80b3c-157">You can allow the business group to manage the credentials assigned to those users for Password Single-Sign On Applications right from their access panels.</span></span>

<span data-ttu-id="80b3c-158">Bir uygulama Self Servis uygulama erişimi etkinleştirmek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="80b3c-158">To enable self-service application access to an application, follow the steps below:</span></span>

1.  <span data-ttu-id="80b3c-159">Açık [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="80b3c-159">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="80b3c-160">Açık **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** ana sol taraftaki gezinti menüsünde sonundaki.</span><span class="sxs-lookup"><span data-stu-id="80b3c-160">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="80b3c-161">Yazın **"Azure Active Directory**" Filtre Arama kutusuna seçip **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="80b3c-161">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="80b3c-162">tıklatın **kurumsal uygulamalar** Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="80b3c-162">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="80b3c-163">tıklatın **tüm uygulamaları** tüm uygulamaların bir listesini görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="80b3c-163">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="80b3c-164">Burada gösterisini istediğiniz uygulama görmüyorsanız kullanın **filtre** üst kısmındaki denetim **tüm uygulamalar listesini** ve **Göster** için seçenek **tüm uygulamaları.**</span><span class="sxs-lookup"><span data-stu-id="80b3c-164">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="80b3c-165">Self Servis etkinleştirmek istediğiniz uygulamayı seçin listeden erişmek için.</span><span class="sxs-lookup"><span data-stu-id="80b3c-165">Select the application you want to enable Self-service access to from the list.</span></span>

7.  <span data-ttu-id="80b3c-166">Uygulamanın yüklediği sonra tıklayın **Self Servis** uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="80b3c-166">Once the application loads, click **Self-service** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="80b3c-167">Bu uygulama için Self Servis uygulama erişimini etkinleştirmek için Aç **bu uygulamaya erişmek kullanıcıların?** geç **Evet.**</span><span class="sxs-lookup"><span data-stu-id="80b3c-167">To enable Self-service application access for this application, turn the **Allow users to request access to this application?** toggle to **Yes.**</span></span>

9.  <span data-ttu-id="80b3c-168">Ardından, isteyen hangi kullanıcıların bu uygulamaya erişim eklenecek grubu seçmek için etiketi yanındaki seçiciyi **hangi grubuna atanan kullanıcıların eklenmesi?** ve bir grubu seçin.</span><span class="sxs-lookup"><span data-stu-id="80b3c-168">Next, to select the group to which users who request access to this application should be added, click the selector next to the label **To which group should assigned users be added?** and select a group.</span></span>

10. <span data-ttu-id="80b3c-169">**İsteğe bağlı:** önce iş onayı iste isterseniz, kullanıcılara erişim verilir, Ayarla **bu uygulamaya erişim vermeden önce onay gerektirir?** geç **Evet**.</span><span class="sxs-lookup"><span data-stu-id="80b3c-169">**Optional:** If you wish to require a business approval before users are allowed access, set the **Require approval before granting access to this application?** toggle to **Yes**.</span></span>

11. <span data-ttu-id="80b3c-170">**İsteğe bağlı: yalnızca parola çoklu oturum üzerinde kullanan uygulamalar için** onaylanan kullanıcılar için bu uygulamaya gönderilen parolalar belirtmek bu iş onaylayanlar izin vermek istiyorsanız, Ayarla **bu uygulama için kullanıcının parola ayarlamak onaylayanlar izin?** geç **Evet**.</span><span class="sxs-lookup"><span data-stu-id="80b3c-170">**Optional: For applications using password single-sign on only,** if you wish to allow those business approvers to specify the passwords that are sent to this application for approved users, set the **Allow approvers to set user’s passwords for this application?** toggle to **Yes**.</span></span>

12. <span data-ttu-id="80b3c-171">**İsteğe bağlı:** bu uygulamaya erişimi onaylamak için izin verilen iş onaylayanlar belirtmek için etiketi yanındaki seçiciyi **kimin bu uygulamaya erişimi onaylamak için verilir?** en fazla 10 ayrı ayrı iş onaylayanlar seçin.</span><span class="sxs-lookup"><span data-stu-id="80b3c-171">**Optional:** To specify the business approvers who are allowed to approve access to this application, click the selector next to the label **Who is allowed to approve access to this application?** to select up to 10 individual business approvers.</span></span>

  >[!NOTE]
  ><span data-ttu-id="80b3c-172">Grupları desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="80b3c-172">Groups are not supported.</span></span>
  >
  >

13. <span data-ttu-id="80b3c-173">**İsteğe bağlı:** **rolleri kullanıma uygulamalar için**, Self Servis onaylanan kullanıcılar role atamak istiyorsanız Seçici tıklayın **hangi rolü için kullanıcıları bu uygulamada atanmalıdır?** , bu kullanıcılar atanabilir rol seçin.</span><span class="sxs-lookup"><span data-stu-id="80b3c-173">**Optional:** **For applications which expose roles**, if you wish to assign self-service approved users to a role, click the selector next to the **To which role should users be assigned in this application?** to select the role to which these users should be assigned.</span></span>

14. <span data-ttu-id="80b3c-174">Tıklatın **kaydetmek** tamamlamak için dikey pencerenin üstündeki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="80b3c-174">Click the **Save** button at the top of the blade to finish.</span></span>

<span data-ttu-id="80b3c-175">Self Servis uygulama yapılandırması tamamlandığında, kullanıcılar için gezinebilir kendi [uygulama erişim Paneli'ne](https://myapps.microsoft.com/) tıklatıp **+ Ekle** Self Servis erişim etkin uygulamalar Bul düğmesi.</span><span class="sxs-lookup"><span data-stu-id="80b3c-175">Once you complete Self-service application configuration, users can navigate to their [Application Access Panel](https://myapps.microsoft.com/) and click the **+Add** button to find the apps to which you have enabled Self-service access.</span></span> <span data-ttu-id="80b3c-176">İş onaylayanlar Ayrıca bkz. bir bildirim kendi [uygulama erişim Paneli'ne](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="80b3c-176">Business approvers also see a notification in their [Application Access Panel](https://myapps.microsoft.com/).</span></span> <span data-ttu-id="80b3c-177">Bir kullanıcı kendi onay gerektiren bir uygulamaya erişim istendiğinde bildiren bir e-posta etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="80b3c-177">You can enable an email notifying them when a user has requested access to an application that requires their approval.</span></span> 

<span data-ttu-id="80b3c-178">Bu onaylar, birden çok onaylayanlar belirtirseniz, tek bir onaylayan uygulamaya onaylayan erişim olabilir yani yalnızca tek onay iş akışları destekler.</span><span class="sxs-lookup"><span data-stu-id="80b3c-178">These approvals support single approval workflows only, meaning that if you specify multiple approvers, any single approver may approver access to the application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="80b3c-179">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="80b3c-179">Next steps</span></span>
[<span data-ttu-id="80b3c-180">Çoklu oturum açma uygulamalarınızı uygulama proxy'si ile sağlayın.</span><span class="sxs-lookup"><span data-stu-id="80b3c-180">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
