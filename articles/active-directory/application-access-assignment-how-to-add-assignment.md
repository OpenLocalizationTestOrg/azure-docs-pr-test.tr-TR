---
title: "aaaHow tooassign kullanıcılar ve gruplar tooan uygulama | Microsoft Docs"
description: "Kullanıcıların toohello uygulama toogrant erişimi atayın"
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
ms.openlocfilehash: e039a26e4b8f88ad747354859f1071b8f74b6789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooassign-users-and-groups-tooan-application"></a><span data-ttu-id="4314f-103">Nasıl tooassign kullanıcılar ve gruplar tooan uygulama</span><span class="sxs-lookup"><span data-stu-id="4314f-103">How tooassign users and groups tooan application</span></span>

<span data-ttu-id="4314f-104">Kullanıcılarınızın herhangi belirli bir uygulama için hello yapabilmeniz için önce toofirst gerek **toohello uygulama atama** erişmesine toogrant:</span><span class="sxs-lookup"><span data-stu-id="4314f-104">Before your users can do any of hello below for a specific application, you need toofirst **assign them toohello application** toogrant them access:</span></span>

-   <span data-ttu-id="4314f-105">Bir uygulama tarafından erişim **toohello uygulamanın URL doğrudan gezinme** (olarak da bilinen SP tarafından başlatılan oturum açma).</span><span class="sxs-lookup"><span data-stu-id="4314f-105">Access an application by **navigating toohello application’s URL directly** (also known as SP-initiated sign-on).</span></span>

-   <span data-ttu-id="4314f-106">Hello kullanarak bir uygulamaya erişim **kullanıcı erişim URL'si** bir uygulamanın üzerinde **özellikleri** sayfa (olarak da bilinen IDP başlatılan oturum açma).</span><span class="sxs-lookup"><span data-stu-id="4314f-106">Access an application by using hello **User Access URL** on an application’s **Properties** page (also known as IDP-initiated sign on).</span></span>

-   <span data-ttu-id="4314f-107">Görünür bir uygulama bkz kendi [uygulama erişim Paneli'ne](https://myapps.microsoft.com/) ya da mobil uygulama.</span><span class="sxs-lookup"><span data-stu-id="4314f-107">See an application appear on their [Application Access Panel](https://myapps.microsoft.com/) or mobile application.</span></span>

-   <span data-ttu-id="4314f-108">Görünür bir uygulama bkz kendi [Office 365 uygulama Başlatıcı](https://support.office.com/article/Meet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a).</span><span class="sxs-lookup"><span data-stu-id="4314f-108">See an application appear on their [Office 365 Application Launcher](https://support.office.com/article/Meet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a).</span></span>

## <a name="methods-tooassign-applications-with-azure-active-directory"></a><span data-ttu-id="4314f-109">Azure Active Directory ile yöntemleri tooassign uygulamalar</span><span class="sxs-lookup"><span data-stu-id="4314f-109">Methods tooassign applications with Azure Active Directory</span></span> 

<span data-ttu-id="4314f-110">Azure Active Directory ile uygulamaları atayabilirsiniz 3 yolu vardır:</span><span class="sxs-lookup"><span data-stu-id="4314f-110">There are 3 ways you can assign applications with Azure Active Directory:</span></span>

-   [<span data-ttu-id="4314f-111">Bir kullanıcı atamak doğrudan tooan uygulama yönetici olarak</span><span class="sxs-lookup"><span data-stu-id="4314f-111">Assign a user directly tooan application as an administrator</span></span>](#assign-a-user-directly-as-an-administrator)

-   [<span data-ttu-id="4314f-112">Bir gruba atamak doğrudan tooan uygulama yönetici olarak</span><span class="sxs-lookup"><span data-stu-id="4314f-112">Assign a group directly tooan application as an administrator</span></span>](#assign-a-group-directly-to-an-application-as-an-administrator)

-   [<span data-ttu-id="4314f-113">Self Servis uygulama erişim tooallow kullanıcılar toofind kendi uygulamalarını etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="4314f-113">Enable self-service application access tooallow users toofind their own applications</span></span>](#enable-self-service-application-access-to-allow-users-to-find-their-own-applications)

## <a name="assign-a-user-directly-as-an-administrator"></a><span data-ttu-id="4314f-114">Yönetici doğrudan kullanıcı atama</span><span class="sxs-lookup"><span data-stu-id="4314f-114">Assign a user directly as an administrator</span></span>

<span data-ttu-id="4314f-115">tooassign bir veya daha fazla kullanıcı tooan uygulama, doğrudan başlangıç adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="4314f-115">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="4314f-116">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="4314f-116">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="4314f-117">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="4314f-117">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4314f-118">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="4314f-118">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4314f-119">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="4314f-119">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4314f-120">Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.</span><span class="sxs-lookup"><span data-stu-id="4314f-120">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="4314f-121">Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**</span><span class="sxs-lookup"><span data-stu-id="4314f-121">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="4314f-122">Tooassign kullanıcı toofrom hello listesini hello uygulamasını seçin.</span><span class="sxs-lookup"><span data-stu-id="4314f-122">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="4314f-123">Merhaba uygulamanın yüklediği sonra tıklayın **kullanıcılar ve gruplar** hello uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="4314f-123">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="4314f-124">Hello tıklatın **Ekle** hello üstünde düğmesi **kullanıcılar ve gruplar** listesi tooopen hello **eklemek atama** dikey.</span><span class="sxs-lookup"><span data-stu-id="4314f-124">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="4314f-125">Merhaba tıklatın **kullanıcılar ve gruplar** hello seçicisini **eklemek atama** dikey.</span><span class="sxs-lookup"><span data-stu-id="4314f-125">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="4314f-126">Merhaba türü **tam adı** veya **e-posta adresi** hello atama ilgilenen hello kullanıcının **ad veya e-posta adresine göre arama** arama kutusu.</span><span class="sxs-lookup"><span data-stu-id="4314f-126">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="4314f-127">Merhaba getirin **kullanıcı** hello listesi tooreveal içinde bir **onay kutusunu**.</span><span class="sxs-lookup"><span data-stu-id="4314f-127">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="4314f-128">Kullanıcı toohello Hello onay kutusu sonraki toohello kullanıcının profili fotoğraf veya logosu tooadd tıklatın **seçili** listesi.</span><span class="sxs-lookup"><span data-stu-id="4314f-128">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="4314f-129">**İsteğe bağlı:** çok isterseniz**birden fazla kullanıcı ekleme**, başka bir tür **tam adı** veya **e-posta adresi** hello içine **ada göre ara veya e-posta adresi** arama kutusu ve bu kullanıcı toohello hello onay kutusunu tooadd tıklatın **seçili** listesi.</span><span class="sxs-lookup"><span data-stu-id="4314f-129">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="4314f-130">Kullanıcıların seçerek bittiğinde hello tıklatın **seçin** düğmesini tooadd bunları kullanıcılar ve gruplar toobe toohello listesi atanan toohello uygulama.</span><span class="sxs-lookup"><span data-stu-id="4314f-130">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="4314f-131">**İsteğe bağlı:** hello tıklatın **rolü Seç** hello seçicide **eklemek atama** dikey tooselect rol seçtiğiniz tooassign toohello kullanıcılar.</span><span class="sxs-lookup"><span data-stu-id="4314f-131">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="4314f-132">Merhaba tıklatın **atamak** düğmesini tooassign hello uygulama toohello seçilen kullanıcılar.</span><span class="sxs-lookup"><span data-stu-id="4314f-132">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="4314f-133">Bir kısa süre sonra seçtiğiniz hello kullanıcıların hello çözüm Açıklama bölümünde açıklanan yöntemleri kullanarak bu uygulamaları hello mümkün toolaunch olması.</span><span class="sxs-lookup"><span data-stu-id="4314f-133">After a short period of time, hello users you have selected be able toolaunch these applications using hello methods described in hello solution description section.</span></span>

## <a name="assign-a-group-directly-tooan-application-as-an-administrator"></a><span data-ttu-id="4314f-134">Bir gruba atamak doğrudan tooan uygulama yönetici olarak</span><span class="sxs-lookup"><span data-stu-id="4314f-134">Assign a group directly tooan application as an administrator</span></span>

<span data-ttu-id="4314f-135">bir veya daha fazla tooassign doğrudan tooan uygulama hello adımları aşağıdaki grupları:</span><span class="sxs-lookup"><span data-stu-id="4314f-135">tooassign one or more groups tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="4314f-136">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="4314f-136">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="4314f-137">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="4314f-137">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4314f-138">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="4314f-138">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4314f-139">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="4314f-139">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4314f-140">Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.</span><span class="sxs-lookup"><span data-stu-id="4314f-140">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="4314f-141">Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**</span><span class="sxs-lookup"><span data-stu-id="4314f-141">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="4314f-142">Tooassign kullanıcı toofrom hello listesini hello uygulamasını seçin.</span><span class="sxs-lookup"><span data-stu-id="4314f-142">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="4314f-143">Merhaba uygulamanın yüklediği sonra tıklayın **kullanıcılar ve gruplar** hello uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="4314f-143">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="4314f-144">Hello tıklatın **Ekle** hello üstünde düğmesi **kullanıcılar ve gruplar** listesi tooopen hello **eklemek atama** dikey.</span><span class="sxs-lookup"><span data-stu-id="4314f-144">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="4314f-145">Merhaba tıklatın **kullanıcılar ve gruplar** hello seçicisini **eklemek atama** dikey.</span><span class="sxs-lookup"><span data-stu-id="4314f-145">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="4314f-146">Merhaba türü **tam grup adı** hello atama ilgilenen hello grubunun **ad veya e-posta adresine göre arama** arama kutusu.</span><span class="sxs-lookup"><span data-stu-id="4314f-146">Type in hello **full group name** of hello group you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="4314f-147">Merhaba getirin **grup** hello listesi tooreveal içinde bir **onay kutusunu**.</span><span class="sxs-lookup"><span data-stu-id="4314f-147">Hover over hello **group** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="4314f-148">Kullanıcı toohello Hello onay kutusu sonraki toohello grubun profili fotoğraf veya logosu tooadd tıklatın **seçili** listesi.</span><span class="sxs-lookup"><span data-stu-id="4314f-148">Click hello checkbox next toohello group’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="4314f-149">**İsteğe bağlı:** çok isterseniz**birden fazla grubu Ekle**, başka bir tür **tam grup adı** hello içine **ad veya e-posta adresine göre arama** arama kutusu tıklatıp hello onay kutusunu tooadd bu Grup toohello **seçili** listesi.</span><span class="sxs-lookup"><span data-stu-id="4314f-149">**Optional:** If you would like too**add more than one group**, type in another **full group name** into hello **Search by name or email address** search box, and click hello checkbox tooadd this group toohello **Selected** list.</span></span>

13. <span data-ttu-id="4314f-150">Grupları seçmek bittiğinde hello tıklatın **seçin** düğmesini tooadd bunları kullanıcılar ve gruplar toobe toohello listesi atanan toohello uygulama.</span><span class="sxs-lookup"><span data-stu-id="4314f-150">When you are finished selecting groups, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="4314f-151">**İsteğe bağlı:** hello tıklatın **rolü Seç** hello seçicide **eklemek atama** dikey tooselect rol tooassign toohello gruplar seçtiniz.</span><span class="sxs-lookup"><span data-stu-id="4314f-151">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello groups you have selected.</span></span>

15. <span data-ttu-id="4314f-152">Merhaba tıklatın **atamak** düğmesini tooassign hello uygulama toohello seçilen grupları.</span><span class="sxs-lookup"><span data-stu-id="4314f-152">Click hello **Assign** button tooassign hello application toohello selected groups.</span></span>

<span data-ttu-id="4314f-153">Bir kısa süre sonra seçtiğiniz hello grupları içindeki hello kullanıcıların hello çözüm Açıklama bölümünde açıklanan yöntemleri kullanarak bu uygulamaları hello mümkün toolaunch olması.</span><span class="sxs-lookup"><span data-stu-id="4314f-153">After a short period of time, hello users within hello groups you have selected be able toolaunch these applications using hello methods described in hello solution description section.</span></span> <span data-ttu-id="4314f-154">Bu dinamik grupların varsa, bazı ek işleme gecikme olabilir bu grupları atanan içindeki kullanıcılar için görünen bu atamaları içinde.</span><span class="sxs-lookup"><span data-stu-id="4314f-154">If these are dynamic groups, there may be some additional processing delay in these assignments appearing for users within these assigned groups.</span></span>

## <a name="enable-self-service-application-access-tooallow-users-toofind-their-own-applications"></a><span data-ttu-id="4314f-155">Self Servis uygulama erişim tooallow kullanıcılar toofind kendi uygulamalarını etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="4314f-155">Enable self-service application access tooallow users toofind their own applications</span></span>

<span data-ttu-id="4314f-156">Self Servis uygulama erişimi olan mükemmel şekilde tooallow kullanıcılar tooself-uygulamaları bulmak, isteğe bağlı olarak hello iş grubu tooapprove erişimi toothose uygulamaları izin verin.</span><span class="sxs-lookup"><span data-stu-id="4314f-156">Self-service application access is a great way tooallow users tooself-discover applications, optionally allow hello business group tooapprove access toothose applications.</span></span> <span data-ttu-id="4314f-157">Merhaba iş grubu toomanage hello kimlik toothose kullanıcılar kendi access panel üzerinde parola çoklu oturum uygulamaları sağdan için atanan izin verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4314f-157">You can allow hello business group toomanage hello credentials assigned toothose users for Password Single-Sign On Applications right from their access panels.</span></span>

<span data-ttu-id="4314f-158">tooenable Self Servis uygulama erişim tooan uygulaması, aşağıdaki hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="4314f-158">tooenable self-service application access tooan application, follow hello steps below:</span></span>

1.  <span data-ttu-id="4314f-159">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="4314f-159">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="4314f-160">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="4314f-160">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4314f-161">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="4314f-161">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4314f-162">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="4314f-162">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4314f-163">Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.</span><span class="sxs-lookup"><span data-stu-id="4314f-163">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="4314f-164">Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**</span><span class="sxs-lookup"><span data-stu-id="4314f-164">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="4314f-165">Tooenable Self Servis erişim toofrom hello listesi hello uygulamasını seçin.</span><span class="sxs-lookup"><span data-stu-id="4314f-165">Select hello application you want tooenable Self-service access toofrom hello list.</span></span>

7.  <span data-ttu-id="4314f-166">Merhaba uygulamanın yüklediği sonra tıklayın **Self Servis** hello uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="4314f-166">Once hello application loads, click **Self-service** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="4314f-167">tooenable bu uygulama için Self Servis uygulama erişimi etkinleştirmek hello **toorequest erişim toothis uygulama kullanıcıların?** çok geçiş**Evet.**</span><span class="sxs-lookup"><span data-stu-id="4314f-167">tooenable Self-service application access for this application, turn hello **Allow users toorequest access toothis application?** toggle too**Yes.**</span></span>

9.  <span data-ttu-id="4314f-168">Ardından, access toothis uygulaması eklenmesi, isteyen tooselect hello Grup toowhich kullanıcılar'ı tıklatın hello Seçici sonraki toohello etiket **toowhich grubuna atanan kullanıcıların eklenmesi?** ve bir grubu seçin.</span><span class="sxs-lookup"><span data-stu-id="4314f-168">Next, tooselect hello group toowhich users who request access toothis application should be added, click hello selector next toohello label **toowhich group should assigned users be added?** and select a group.</span></span>

10. <span data-ttu-id="4314f-169">**İsteğe bağlı:** kullanıcıların erişim izin verilmeden önce bir iş onay toorequire isterseniz, hello ayarlamak **erişim toothis uygulama vermeden önce onay gerektirir?** çok geçiş**Evet**.</span><span class="sxs-lookup"><span data-stu-id="4314f-169">**Optional:** If you wish toorequire a business approval before users are allowed access, set hello **Require approval before granting access toothis application?** toggle too**Yes**.</span></span>

11. <span data-ttu-id="4314f-170">**İsteğe bağlı: yalnızca parola çoklu oturum üzerinde kullanan uygulamalar için** toothis uygulama onaylanan kullanıcılar için gönderilen bu iş onaylayanlar toospecify hello parolaları tooallow isterseniz hello ayarlamak **izin onaylayanlar tooset Bu uygulama için kullanıcının parola?**  çok geçiş**Evet**.</span><span class="sxs-lookup"><span data-stu-id="4314f-170">**Optional: For applications using password single-sign on only,** if you wish tooallow those business approvers toospecify hello passwords that are sent toothis application for approved users, set hello **Allow approvers tooset user’s passwords for this application?** toggle too**Yes**.</span></span>

12. <span data-ttu-id="4314f-171">**İsteğe bağlı:** tooapprove erişim toothis uygulama, izin verilen toospecify hello iş onaylayanlar tıklatın hello Seçici sonraki toohello etiket **kimin tooapprove erişim toothis uygulama verilir?** tooselect ayarlama too10 ayrı ayrı iş onaylayanlar.</span><span class="sxs-lookup"><span data-stu-id="4314f-171">**Optional:** toospecify hello business approvers who are allowed tooapprove access toothis application, click hello selector next toohello label **Who is allowed tooapprove access toothis application?** tooselect up too10 individual business approvers.</span></span>

  >[!NOTE]
  ><span data-ttu-id="4314f-172">Grupları desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="4314f-172">Groups are not supported.</span></span>
  >
  >

13. <span data-ttu-id="4314f-173">**İsteğe bağlı:** **rolleri kullanıma uygulamalar için**, tooassign Self Servis onaylanan kullanıcılar tooa rol istiyorsanız hello Seçici sonraki toohello tıklatın **toowhich rol kullanıcılar bu atanmalıdır Uygulama?**  tooselect hello rol toowhich bu kullanıcılar atanabilir.</span><span class="sxs-lookup"><span data-stu-id="4314f-173">**Optional:** **For applications which expose roles**, if you wish tooassign self-service approved users tooa role, click hello selector next toohello **toowhich role should users be assigned in this application?** tooselect hello role toowhich these users should be assigned.</span></span>

14. <span data-ttu-id="4314f-174">Merhaba tıklatın **kaydetmek** hello dikey toofinish hello üstündeki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4314f-174">Click hello **Save** button at hello top of hello blade toofinish.</span></span>

<span data-ttu-id="4314f-175">Self Servis uygulama yapılandırması tamamlandığında, kullanıcılar tootheir gezinebilir [uygulama erişim Paneli'ne](https://myapps.microsoft.com/) hello tıklatıp **+ Ekle** düğmesini toofind hello uygulamaları toowhich etkinleştirdiğiniz Self Servis erişim.</span><span class="sxs-lookup"><span data-stu-id="4314f-175">Once you complete Self-service application configuration, users can navigate tootheir [Application Access Panel](https://myapps.microsoft.com/) and click hello **+Add** button toofind hello apps toowhich you have enabled Self-service access.</span></span> <span data-ttu-id="4314f-176">İş onaylayanlar Ayrıca bkz. bir bildirim kendi [uygulama erişim Paneli'ne](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="4314f-176">Business approvers also see a notification in their [Application Access Panel](https://myapps.microsoft.com/).</span></span> <span data-ttu-id="4314f-177">Bir kullanıcı kendi onay gerektiren erişim tooan uygulama istendiğinde bildiren bir e-posta etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4314f-177">You can enable an email notifying them when a user has requested access tooan application that requires their approval.</span></span> 

<span data-ttu-id="4314f-178">Bu onaylar, birden çok onaylayanlar belirtirseniz, tek bir onaylayan onaylayan access toohello uygulaması olabilir yani yalnızca tek onay iş akışları destekler.</span><span class="sxs-lookup"><span data-stu-id="4314f-178">These approvals support single approval workflows only, meaning that if you specify multiple approvers, any single approver may approver access toohello application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4314f-179">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4314f-179">Next steps</span></span>
[<span data-ttu-id="4314f-180">Uygulama proxy'si ile çoklu oturum açma tooyour uygulamaları sağlayın</span><span class="sxs-lookup"><span data-stu-id="4314f-180">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
