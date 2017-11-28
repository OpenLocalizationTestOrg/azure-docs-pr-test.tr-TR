---
title: "aaaHow tooconfigure parola tek oturum açma için Galeri olmayan applicationn | Microsoft Docs"
description: "Tooconfigure için özel bir galeri olmayan uygulama güvenliğini nasıl parola tabanlı çoklu oturum açma hello Azure AD uygulama galerisinde listelenmeyen olduğunda"
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
ms.openlocfilehash: e3d0e658f792a0a63110a198811edc66acd6ccf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="d2624-103">Tooconfigure parola nasıl tek bir galeri olmayan uygulaması için oturum açma</span><span class="sxs-lookup"><span data-stu-id="d2624-103">How tooconfigure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="d2624-104">Ayrıca toohello seçenekleri bulunan hello Azure AD uygulama galerisinde içinde hello seçeneği tooadd de sahip bir **galeri olmayan uygulama** zaman hello uygulamasıyla listelenmemiş vardır.</span><span class="sxs-lookup"><span data-stu-id="d2624-104">In addition toohello choices found within hello Azure AD Application Gallery, you also have hello option tooadd a **non-gallery application** when hello application you want is not listed there.</span></span> <span data-ttu-id="d2624-105">Bu özelliği kullanarak, kuruluşunuzda zaten herhangi bir uygulama ya da kullanıyor olabileceğiniz herhangi bir üçüncü taraf uygulama zaten hello parçası olmayan bir satıcıdan ekleyebileceğiniz [Azure AD uygulama galerisinde](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span><span class="sxs-lookup"><span data-stu-id="d2624-105">Using this capability, you can add any application that already exists in your organization, or any third-party application that you might use from a vendor who is not already part of hello [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span></span>

<span data-ttu-id="d2624-106">Bir galeri olmayan uygulama ekledikten sonra daha sonra bu uygulamanın kullandığı hello seçerek hello tek oturum açma yöntemi yapılandırabilirsiniz **çoklu oturum açma** hello kuruluş uygulamasında Gezinti öğede [Azure portalı ](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d2624-106">Once you add a non-gallery application, you can then configure hello Single sign-on method this application uses by selecting hello **Single Sign-on** navigation item on an Enterprise Application in hello [Azure Portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="d2624-107">Merhaba çoklu oturum açma yöntemleri kullanılabilir tooyou biri hello [parola tabanlı çoklu oturum açma](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) seçeneği.</span><span class="sxs-lookup"><span data-stu-id="d2624-107">One of hello Single Sign-on methods available tooyou is hello [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) option.</span></span> <span data-ttu-id="d2624-108">Merhaba ile **bir galeri olmayan uygulama eklemek** deneyimi, bir HTML tabanlı kullanıcıadı işleyen herhangi bir uygulama tümleştirebilir ve parola giriş alanı, önceden tümleştirilmiş uygulamaların bizim kümesinde olmasa bile.</span><span class="sxs-lookup"><span data-stu-id="d2624-108">With hello **add a non-gallery application** experience, you can integrate any application that renders an HTML-based username and password input field, even if it is not in our set of pre-integrated applications.</span></span>

<span data-ttu-id="d2624-109">Bu çalışır hello yoludur hello parçası olan teknoloji değiştirilene sayfası tarafından bize tooauto sağlayan erişim paneli uzantısı-kullanıcı adı ve parola giriş alanlarının algılamak, belirli bir uygulama Örneğiniz için bunları güvenli bir şekilde saklayın.</span><span class="sxs-lookup"><span data-stu-id="d2624-109">hello way this works is by a page scraping technology that is part of hello Access Panel extension that allows us tooauto-detect username and password input fields, store them securely for your specific application instance.</span></span> <span data-ttu-id="d2624-110">Kullanıcı adlarını güvenli bir şekilde yeniden yürütme ve parolaları toothose alanları bir kullanıcı hello uygulama erişim Paneli'ne toothat uygulamaya gider.</span><span class="sxs-lookup"><span data-stu-id="d2624-110">Then securely replay usernames and passwords toothose fields when a user navigates toothat application on hello application access panel.</span></span>

<span data-ttu-id="d2624-111">Bu tooget her türlü uygulama hızlı bir şekilde Azure AD ile tümleştirme kullanmaya ve böylece kullanışlı bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="d2624-111">This is a great way tooget started integrating any kind of application into Azure AD quickly, and allows you to:</span></span>

-   <span data-ttu-id="d2624-112">Tümleştirme **Merhaba Dünya herhangi bir uygulamada** ile Azure AD kiracınız, HTML kullanıcı adı ve parola giriş alanını işleyen kadar uzun süre</span><span class="sxs-lookup"><span data-stu-id="d2624-112">Integrate **any application in hello world** with your Azure AD tenant, so long as it renders an HTML username and password input field</span></span>

-   <span data-ttu-id="d2624-113">Etkinleştirme **kullanıcılarınız için çoklu oturum açmayı** güvenli bir şekilde depolamak ve kullanıcı adları ve parolalar Merhaba uygulaması için yeniden oynatmak tarafından Azure AD ile tümleşik</span><span class="sxs-lookup"><span data-stu-id="d2624-113">Enable **Single Sign-on for your users** by securely storing and replaying usernames and passwords for hello application you’ve integrated with Azure AD</span></span>

-   <span data-ttu-id="d2624-114">**Giriş otomatik algıla** alanlar için herhangi bir uygulama ve izin toomanually algılamak hello erişim paneli tarayıcı uzantısı kullanarak bu alanlar otomatik algılamayı bulmaz durumda</span><span class="sxs-lookup"><span data-stu-id="d2624-114">**Auto-detect input** fields for any application and allow you toomanually detect those fields using hello Access Panel Browser Extension, in case auto-detection does not find them</span></span>

-   <span data-ttu-id="d2624-115">**Destek oturum açma birden çok alan gerektiren uygulamalar** içinde birden fazla yalnızca kullanıcı adı ve parola alanları toosign gerektiren uygulamalar için</span><span class="sxs-lookup"><span data-stu-id="d2624-115">**Support applications that require multiple sign-in fields** for applications that require more than just username and password fields toosign in</span></span>

-   <span data-ttu-id="d2624-116">**Başlangıç etiketleri özelleştirme** hello kullanıcı adı ve parola giriş alanları kullanıcılarınızın üzerinde hello görmek [uygulama erişim Paneli'ne](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) kimlik bilgilerini girmeleri zaman</span><span class="sxs-lookup"><span data-stu-id="d2624-116">**Customize hello labels** of hello username and password input fields your users see on hello [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) when they enter their credentials</span></span>

-   <span data-ttu-id="d2624-117">İzin ver, **kullanıcılar** tooprovide kendi kullanıcı adları ve bunlar yazarak el ile Merhaba üzerinde var olan tüm uygulama hesaplar için parolaları [uygulama erişim paneli](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span><span class="sxs-lookup"><span data-stu-id="d2624-117">Allow your **users** tooprovide their own usernames and passwords for any existing application accounts they are typing in manually on hello [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span></span>

-   <span data-ttu-id="d2624-118">İzin bir **hello iş grubunun üyesi** toospecify hello kullanıcı adları ve parolalar atanan tooa kullanıcı hello kullanarak [Self Servis uygulamaya erişim](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) özelliği</span><span class="sxs-lookup"><span data-stu-id="d2624-118">Allow a **member of hello business group** toospecify hello usernames and passwords assigned tooa user by using hello [Self-Service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) feature</span></span>

-   <span data-ttu-id="d2624-119">İzin bir **yönetici** toospecify hello kullanıcı adları ve parolalar hello güncelleştirme kimlik bilgileri kullanılarak tooa kullanıcı atanan özellik ne zaman [kullanıcı tooan uygulama atama](#_How_to_configure_1)</span><span class="sxs-lookup"><span data-stu-id="d2624-119">Allow an **administrator** toospecify hello usernames and passwords assigned tooa user by using hello Update Credentials feature when [assigning a user tooan application](#_How_to_configure_1)</span></span>

-   <span data-ttu-id="d2624-120">İzin bir **yönetici** toospecify paylaşılan hello kullanıcı adı veya parola hello güncelleştirme kimlik bilgilerini kullanarak bir grup kişi tarafından kullanılan özellik ne zaman [grubu tooan uygulama atama](#assign-an-application-to-a-group-directly)</span><span class="sxs-lookup"><span data-stu-id="d2624-120">Allow an **administrator** toospecify hello shared username or password used by a group of people by using hello Update Credentials feature when [assigning a group tooan application](#assign-an-application-to-a-group-directly)</span></span>

<span data-ttu-id="d2624-121">Aşağıda nasıl etkinleştirebilirsiniz açıklar [parola tabanlı çoklu oturum açma](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) tooany uygulama hello kullanarak Ekle **bir galeri olmayan uygulama eklemek** karşılaşırsınız.</span><span class="sxs-lookup"><span data-stu-id="d2624-121">Below describes how you can enable [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) tooany application that you add using hello **add a non-gallery application** experience.</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="d2624-122">Gerekli adımlara genel bakış</span><span class="sxs-lookup"><span data-stu-id="d2624-122">Overview of steps required</span></span>

<span data-ttu-id="d2624-123">tooconfigure hello Azure AD Galeriden bir uygulama şunları yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="d2624-123">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="d2624-124">Bir galeri olmayan uygulama ekleme</span><span class="sxs-lookup"><span data-stu-id="d2624-124">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="d2624-125">Merhaba uygulaması parola çoklu oturum açma için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d2624-125">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

-   [<span data-ttu-id="d2624-126">Merhaba uygulama tooa kullanıcısı veya grubu atayın</span><span class="sxs-lookup"><span data-stu-id="d2624-126">Assign hello application tooa user or a group</span></span>](#assign-the-application-to-a-user-or-a-group)

    -   [<span data-ttu-id="d2624-127">Bir kullanıcı tooan uygulama doğrudan atama</span><span class="sxs-lookup"><span data-stu-id="d2624-127">Assign a user tooan application directly</span></span>](#assign-a-user-to-an-application-directly)

    -   [<span data-ttu-id="d2624-128">Uygulama tooa grubu doğrudan atama</span><span class="sxs-lookup"><span data-stu-id="d2624-128">Assign an application tooa group directly</span></span>](#assign-an-application-to-a-group-directly)

## <a name="add-a-non-gallery-application"></a><span data-ttu-id="d2624-129">Bir galeri olmayan uygulama ekleme</span><span class="sxs-lookup"><span data-stu-id="d2624-129">Add a non-gallery application</span></span>

<span data-ttu-id="d2624-130">tooadd hello Azure AD galeri, bir uygulamadan hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="d2624-130">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="d2624-131">Açık hello [Azure Portal](https://portal.azure.com) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="d2624-131">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="d2624-132">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="d2624-132">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d2624-133">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="d2624-133">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d2624-134">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="d2624-134">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d2624-135">Merhaba tıklatın **Ekle** hello sağ üst köşesindeki hello düğmesi **kurumsal uygulamalar** dikey</span><span class="sxs-lookup"><span data-stu-id="d2624-135">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="d2624-136">tıklatın **olmayan galeri uygulaması.**</span><span class="sxs-lookup"><span data-stu-id="d2624-136">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="d2624-137">Merhaba, uygulamanızın hello adını **adı** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="d2624-137">Enter hello name of your application in hello **Name** textbox.</span></span> <span data-ttu-id="d2624-138">Seçin **ekleyin.**</span><span class="sxs-lookup"><span data-stu-id="d2624-138">Select **Add.**</span></span>

<span data-ttu-id="d2624-139">Kısa bir süre sonra mümkün toosee hello uygulamanın yapılandırma dikey olabilir.</span><span class="sxs-lookup"><span data-stu-id="d2624-139">After a short period, you be able toosee hello application’s configuration blade.</span></span>

## <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="d2624-140">Merhaba uygulaması parola çoklu oturum açma için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d2624-140">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="d2624-141">tooconfigure çoklu oturum açma bir uygulama için başlangıç adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="d2624-141">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="d2624-142">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="d2624-142">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="d2624-143">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="d2624-143">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d2624-144">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="d2624-144">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d2624-145">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="d2624-145">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d2624-146">Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.</span><span class="sxs-lookup"><span data-stu-id="d2624-146">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="d2624-147">Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**</span><span class="sxs-lookup"><span data-stu-id="d2624-147">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="d2624-148">Tooconfigure çoklu oturum açma hello uygulamasını seçin.</span><span class="sxs-lookup"><span data-stu-id="d2624-148">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="d2624-149">Merhaba uygulamanın yüklediği sonra hello tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="d2624-149">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="d2624-150">Select hello modu **parola tabanlı oturum açma.**</span><span class="sxs-lookup"><span data-stu-id="d2624-150">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="d2624-151">Merhaba girin **oturum açma URL'si**.</span><span class="sxs-lookup"><span data-stu-id="d2624-151">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="d2624-152">Bu kullanıcılar kendi kullanıcı adı ve parola toosign içinde için girdiğiniz yere hello URL'dir.</span><span class="sxs-lookup"><span data-stu-id="d2624-152">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="d2624-153">Merhaba oturum alanları hello URL'de göründüğünden emin olun.</span><span class="sxs-lookup"><span data-stu-id="d2624-153">Ensure hello sign in fields are visible at hello URL.</span></span>

10. <span data-ttu-id="d2624-154">Kullanıcıların toohello uygulama atayın.</span><span class="sxs-lookup"><span data-stu-id="d2624-154">Assign users toohello application.</span></span>

11. <span data-ttu-id="d2624-155">Ayrıca, ayrıca hello kullanıcı adına kimlik bilgilerini hello satırları hello kullanıcıların seçerek ve tıklayarak sağlayabilirsiniz **güncelleştirme kimlik bilgileri** ve hello kullanıcılar adına hello kullanıcı adı ve parola girme.</span><span class="sxs-lookup"><span data-stu-id="d2624-155">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="d2624-156">Aksi takdirde, kullanıcılar istendiğinde tooenter hello kimlik bilgilerinin kendilerini başlatma bağlı olması.</span><span class="sxs-lookup"><span data-stu-id="d2624-156">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="assign-a-user-tooan-application-directly"></a><span data-ttu-id="d2624-157">Bir kullanıcı tooan uygulama doğrudan atama</span><span class="sxs-lookup"><span data-stu-id="d2624-157">Assign a user tooan application directly</span></span>

<span data-ttu-id="d2624-158">tooassign bir veya daha fazla kullanıcı tooan uygulama, doğrudan başlangıç adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="d2624-158">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="d2624-159">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="d2624-159">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="d2624-160">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="d2624-160">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d2624-161">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="d2624-161">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d2624-162">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="d2624-162">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d2624-163">Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.</span><span class="sxs-lookup"><span data-stu-id="d2624-163">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="d2624-164">Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**</span><span class="sxs-lookup"><span data-stu-id="d2624-164">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="d2624-165">Tooassign kullanıcı toofrom hello listesini hello uygulamasını seçin.</span><span class="sxs-lookup"><span data-stu-id="d2624-165">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="d2624-166">Merhaba uygulamanın yüklediği sonra tıklayın **kullanıcılar ve gruplar** hello uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="d2624-166">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="d2624-167">Hello tıklatın **Ekle** hello üstünde düğmesi **kullanıcılar ve gruplar** listesi tooopen hello **eklemek atama** dikey.</span><span class="sxs-lookup"><span data-stu-id="d2624-167">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="d2624-168">Merhaba tıklatın **kullanıcılar ve gruplar** hello seçicisini **eklemek atama** dikey.</span><span class="sxs-lookup"><span data-stu-id="d2624-168">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="d2624-169">Merhaba türü **tam adı** veya **e-posta adresi** hello atama ilgilenen hello kullanıcının **ad veya e-posta adresine göre arama** arama kutusu.</span><span class="sxs-lookup"><span data-stu-id="d2624-169">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="d2624-170">Merhaba getirin **kullanıcı** hello listesi tooreveal içinde bir **onay kutusunu**.</span><span class="sxs-lookup"><span data-stu-id="d2624-170">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="d2624-171">Kullanıcı toohello Hello onay kutusu sonraki toohello kullanıcının profili fotoğraf veya logosu tooadd tıklatın **seçili** listesi.</span><span class="sxs-lookup"><span data-stu-id="d2624-171">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="d2624-172">**İsteğe bağlı:** çok isterseniz**birden fazla kullanıcı ekleme**, başka bir tür **tam adı** veya **e-posta adresi** hello içine **ada göre ara veya e-posta adresi** arama kutusu ve bu kullanıcı toohello hello onay kutusunu tooadd tıklatın **seçili** listesi.</span><span class="sxs-lookup"><span data-stu-id="d2624-172">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="d2624-173">Kullanıcıların seçerek bittiğinde hello tıklatın **seçin** düğmesini tooadd bunları kullanıcılar ve gruplar toobe toohello listesi atanan toohello uygulama.</span><span class="sxs-lookup"><span data-stu-id="d2624-173">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="d2624-174">**İsteğe bağlı:** hello tıklatın **rolü Seç** hello seçicide **eklemek atama** dikey tooselect rol seçtiğiniz tooassign toohello kullanıcılar.</span><span class="sxs-lookup"><span data-stu-id="d2624-174">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="d2624-175">Merhaba tıklatın **atamak** düğmesini tooassign hello uygulama toohello seçilen kullanıcılar.</span><span class="sxs-lookup"><span data-stu-id="d2624-175">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

## <a name="assign-an-application-tooa-group-directly"></a><span data-ttu-id="d2624-176">Uygulama tooa grubu doğrudan atama</span><span class="sxs-lookup"><span data-stu-id="d2624-176">Assign an application tooa group directly</span></span>

<span data-ttu-id="d2624-177">bir veya daha fazla tooassign doğrudan tooan uygulama hello adımları aşağıdaki grupları:</span><span class="sxs-lookup"><span data-stu-id="d2624-177">tooassign one or more groups tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="d2624-178">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="d2624-178">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="d2624-179">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="d2624-179">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d2624-180">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="d2624-180">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d2624-181">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="d2624-181">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d2624-182">Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.</span><span class="sxs-lookup"><span data-stu-id="d2624-182">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="d2624-183">Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**</span><span class="sxs-lookup"><span data-stu-id="d2624-183">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="d2624-184">Tooassign kullanıcı toofrom hello listesini hello uygulamasını seçin.</span><span class="sxs-lookup"><span data-stu-id="d2624-184">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="d2624-185">Merhaba uygulamanın yüklediği sonra tıklayın **kullanıcılar ve gruplar** hello uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="d2624-185">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="d2624-186">Hello tıklatın **Ekle** hello üstünde düğmesi **kullanıcılar ve gruplar** listesi tooopen hello **eklemek atama** dikey.</span><span class="sxs-lookup"><span data-stu-id="d2624-186">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="d2624-187">Merhaba tıklatın **kullanıcılar ve gruplar** hello seçicisini **eklemek atama** dikey.</span><span class="sxs-lookup"><span data-stu-id="d2624-187">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="d2624-188">Merhaba türü **tam grup adı** hello atama ilgilenen hello grubunun **ad veya e-posta adresine göre arama** arama kutusu.</span><span class="sxs-lookup"><span data-stu-id="d2624-188">Type in hello **full group name** of hello group you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="d2624-189">Merhaba getirin **grup** hello listesi tooreveal içinde bir **onay kutusunu**.</span><span class="sxs-lookup"><span data-stu-id="d2624-189">Hover over hello **group** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="d2624-190">Kullanıcı toohello Hello onay kutusu sonraki toohello grubun profili fotoğraf veya logosu tooadd tıklatın **seçili** listesi.</span><span class="sxs-lookup"><span data-stu-id="d2624-190">Click hello checkbox next toohello group’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="d2624-191">**İsteğe bağlı:** çok isterseniz**birden fazla grubu Ekle**, başka bir tür **tam grup adı** hello içine **ad veya e-posta adresine göre arama** arama kutusu tıklatıp hello onay kutusunu tooadd bu Grup toohello **seçili** listesi.</span><span class="sxs-lookup"><span data-stu-id="d2624-191">**Optional:** If you would like too**add more than one group**, type in another **full group name** into hello **Search by name or email address** search box, and click hello checkbox tooadd this group toohello **Selected** list.</span></span>

13. <span data-ttu-id="d2624-192">Grupları seçmek bittiğinde hello tıklatın **seçin** düğmesini tooadd bunları kullanıcılar ve gruplar toobe toohello listesi atanan toohello uygulama.</span><span class="sxs-lookup"><span data-stu-id="d2624-192">When you are finished selecting groups, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="d2624-193">**İsteğe bağlı:** hello tıklatın **rolü Seç** hello seçicide **eklemek atama** dikey tooselect rol tooassign toohello gruplar seçtiniz.</span><span class="sxs-lookup"><span data-stu-id="d2624-193">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello groups you have selected.</span></span>

15. <span data-ttu-id="d2624-194">Merhaba tıklatın **atamak** düğmesini tooassign hello uygulama toohello seçilen grupları.</span><span class="sxs-lookup"><span data-stu-id="d2624-194">Click hello **Assign** button tooassign hello application toohello selected groups.</span></span>

<span data-ttu-id="d2624-195">Seçtiğiniz hello kullanıcılar kısa bir süre mümkün toolaunch bu uygulamalarında değiştirdikten sonra erişim Paneli'ne hello.</span><span class="sxs-lookup"><span data-stu-id="d2624-195">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d2624-196">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d2624-196">Next steps</span></span>
[<span data-ttu-id="d2624-197">Uygulama proxy'si ile çoklu oturum açma tooyour uygulamaları sağlayın</span><span class="sxs-lookup"><span data-stu-id="d2624-197">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
