---
title: "aaaHow tooconfigure parola tek oturum açma için Azure AD galeri uygulama | Microsoft Docs"
description: "Nasıl tooconfigure bir uygulama için güvenli parola tabanlı çoklu oturum açma hello Azure AD uygulama galerisinde zaten listelendiğinde"
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
ms.openlocfilehash: 7a93bff119b477d946368686fc2d9006ca2722a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="416e4-103">Tooconfigure parola nasıl çoklu oturum açma için Azure AD galeri uygulama</span><span class="sxs-lookup"><span data-stu-id="416e4-103">How tooconfigure password single sign-on for an Azure AD Gallery application</span></span>

<span data-ttu-id="416e4-104">Uygulamanın hello eklediğinizde [Azure AD uygulama galerisinde](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery), toothat uygulamada, kullanıcıların toosign istediğiniz hello seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="416e4-104">When you add an application from hello [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery), you have hello choice of how you want your users toosign in toothat application.</span></span> <span data-ttu-id="416e4-105">Bu seçenek hello seçerek herhangi bir anda yapılandırabilirsiniz **çoklu oturum açma** hello kuruluş uygulamasında Gezinti öğede [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="416e4-105">You can configure this choice at any time by selecting hello **Single Sign-on** navigation item on an Enterprise Application in hello [Azure Portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="416e4-106">Merhaba tek oturum açma yöntemleri kullanılabilir tooyou biri hello [parola tabanlı çoklu oturum açma](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) seçeneği.</span><span class="sxs-lookup"><span data-stu-id="416e4-106">One of hello single sign-on methods available tooyou is hello [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) option.</span></span> <span data-ttu-id="416e4-107">Bu tooget uygulamaları hızlı bir şekilde Azure AD ile tümleştirme kullanmaya ve böylece kullanışlı bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="416e4-107">This is a great way tooget started integrating applications into Azure AD quickly, and allows you to:</span></span>

-   <span data-ttu-id="416e4-108">Etkinleştirme **kullanıcılarınız için çoklu oturum açmayı** güvenli bir şekilde depolamak ve kullanıcı adları ve parolalar Merhaba uygulaması için yeniden oynatmak tarafından Azure AD ile tümleşik</span><span class="sxs-lookup"><span data-stu-id="416e4-108">Enable **Single Sign-on for your users** by securely storing and replaying usernames and passwords for hello application you’ve integrated with Azure AD</span></span>

-   <span data-ttu-id="416e4-109">**Destek oturum açma birden çok alan gerektiren uygulamalar** içinde birden fazla yalnızca kullanıcı adı ve parola alanları toosign gerektiren uygulamalar için</span><span class="sxs-lookup"><span data-stu-id="416e4-109">**Support applications that require multiple sign-in fields** for applications that require more than just username and password fields toosign in</span></span>

-   <span data-ttu-id="416e4-110">**Başlangıç etiketleri özelleştirme** hello kullanıcı adı ve parola giriş alanları kullanıcılarınızın üzerinde hello görmek [uygulama erişim Paneli'ne](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) kimlik bilgilerini girmeleri zaman</span><span class="sxs-lookup"><span data-stu-id="416e4-110">**Customize hello labels** of hello username and password input fields your users see on hello [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) when they enter their credentials</span></span>

-   <span data-ttu-id="416e4-111">İzin ver, **kullanıcılar** tooprovide kendi kullanıcı adları ve bunlar yazarak el ile Merhaba üzerinde var olan tüm uygulama hesaplar için parolaları [uygulama erişim paneli](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span><span class="sxs-lookup"><span data-stu-id="416e4-111">Allow your **users** tooprovide their own usernames and passwords for any existing application accounts they are typing in manually on hello [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span></span>

-   <span data-ttu-id="416e4-112">İzin bir **hello iş grubunun üyesi** toospecify hello kullanıcı adları ve parolalar atanan tooa kullanıcı hello kullanarak [Self Servis uygulamaya erişim](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) özelliği</span><span class="sxs-lookup"><span data-stu-id="416e4-112">Allow a **member of hello business group** toospecify hello usernames and passwords assigned tooa user by using hello [Self-Service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) feature</span></span>

-   <span data-ttu-id="416e4-113">İzin bir **yönetici** toospecify hello kullanıcı adları ve parolalar hello güncelleştirme kimlik bilgileri kullanılarak tooa kullanıcı atanan özellik ne zaman [kullanıcı tooan uygulama atama](#assign-a-user-to-an-application-directly)</span><span class="sxs-lookup"><span data-stu-id="416e4-113">Allow an **administrator** toospecify hello usernames and passwords assigned tooa user by using hello Update Credentials feature when [assigning a user tooan application](#assign-a-user-to-an-application-directly)</span></span>

-   <span data-ttu-id="416e4-114">İzin bir **yönetici** toospecify paylaşılan hello kullanıcı adı veya parola hello güncelleştirme kimlik bilgilerini kullanarak bir grup kişi tarafından kullanılan özellik ne zaman [grubu tooan uygulama atama](#assign-an-application-to-a-group-directly)</span><span class="sxs-lookup"><span data-stu-id="416e4-114">Allow an **administrator** toospecify hello shared username or password used by a group of people by using hello Update Credentials feature when [assigning a group tooan application](#assign-an-application-to-a-group-directly)</span></span>

<span data-ttu-id="416e4-115">Aşağıda nasıl etkinleştirebilirsiniz açıklar [parola tabanlı çoklu oturum açma](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) hello zaten tooan uygulama [Azure AD uygulama galerisinde](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span><span class="sxs-lookup"><span data-stu-id="416e4-115">Below describes how you can enable [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) tooan application that is already in hello [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="416e4-116">Gerekli adımlara genel bakış</span><span class="sxs-lookup"><span data-stu-id="416e4-116">Overview of steps required</span></span>
<span data-ttu-id="416e4-117">tooconfigure hello Azure AD Galeriden bir uygulama şunları yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="416e4-117">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="416e4-118">Hello Azure AD Galeriden bir uygulama ekleme</span><span class="sxs-lookup"><span data-stu-id="416e4-118">Add an application from hello Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="416e4-119">Merhaba uygulaması parola çoklu oturum açma için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="416e4-119">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

-   [<span data-ttu-id="416e4-120">Merhaba uygulama tooa kullanıcısı veya grubu atayın</span><span class="sxs-lookup"><span data-stu-id="416e4-120">Assign hello application tooa user or a group</span></span>](#assign-the-application-to-a-user-or-a-group)

    -   [<span data-ttu-id="416e4-121">Bir kullanıcı tooan uygulama doğrudan atama</span><span class="sxs-lookup"><span data-stu-id="416e4-121">Assign a user tooan application directly</span></span>](#assign-a-user-to-an-application-directly)

    -   [<span data-ttu-id="416e4-122">Uygulama tooa grubu doğrudan atama</span><span class="sxs-lookup"><span data-stu-id="416e4-122">Assign an application tooa group directly</span></span>](#assign-an-application-to-a-group-directly)

## <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="416e4-123">Hello Azure AD Galeriden bir uygulama ekleme</span><span class="sxs-lookup"><span data-stu-id="416e4-123">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="416e4-124">tooadd hello Azure AD galeri, bir uygulamadan hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="416e4-124">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="416e4-125">Açık hello [Azure Portal](https://portal.azure.com) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="416e4-125">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="416e4-126">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="416e4-126">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="416e4-127">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="416e4-127">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="416e4-128">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="416e4-128">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="416e4-129">Merhaba tıklatın **Ekle** hello sağ üst köşesindeki hello düğmesi **kurumsal uygulamalar** dikey</span><span class="sxs-lookup"><span data-stu-id="416e4-129">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="416e4-130">Merhaba, **bir ad girin** hello metin **hello galerisinden Ekle** bölümü, hello uygulamasının türü hello adı</span><span class="sxs-lookup"><span data-stu-id="416e4-130">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application</span></span>

7.  <span data-ttu-id="416e4-131">Tooconfigure için çoklu oturum açmayı hello uygulamasını seçin</span><span class="sxs-lookup"><span data-stu-id="416e4-131">Select hello application you want tooconfigure for single sign-on</span></span>

8.  <span data-ttu-id="416e4-132">Merhaba uygulaması eklemeden önce hello adını değiştirebilirsiniz **adı** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="416e4-132">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="416e4-133">Tıklatın **Ekle** button, tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="416e4-133">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="416e4-134">Kısa bir süre sonra mümkün toosee hello uygulamanın yapılandırma dikey olabilir.</span><span class="sxs-lookup"><span data-stu-id="416e4-134">After a short period, you be able toosee hello application’s configuration blade.</span></span>

## <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="416e4-135">Merhaba uygulaması parola çoklu oturum açma için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="416e4-135">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="416e4-136">tooconfigure çoklu oturum açma bir uygulama için başlangıç adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="416e4-136">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="416e4-137">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="416e4-137">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="416e4-138">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="416e4-138">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="416e4-139">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="416e4-139">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="416e4-140">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="416e4-140">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="416e4-141">Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.</span><span class="sxs-lookup"><span data-stu-id="416e4-141">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="416e4-142">Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**</span><span class="sxs-lookup"><span data-stu-id="416e4-142">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="416e4-143">Tooconfigure çoklu oturum açma hello uygulamasını seçin</span><span class="sxs-lookup"><span data-stu-id="416e4-143">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="416e4-144">Merhaba uygulamanın yüklediği sonra hello tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="416e4-144">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="416e4-145">Select hello modu **parola tabanlı oturum açma.**</span><span class="sxs-lookup"><span data-stu-id="416e4-145">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="416e4-146">[Kullanıcıların toohello uygulama atama](#assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="416e4-146">[Assign users toohello application](#assign-a-user-to-an-application-directly).</span></span>

10. <span data-ttu-id="416e4-147">Ayrıca, ayrıca hello kullanıcı adına kimlik bilgilerini hello satırları hello kullanıcıların seçerek ve tıklayarak sağlayabilirsiniz **güncelleştirme kimlik bilgileri** ve hello kullanıcılar adına hello kullanıcı adı ve parola girme.</span><span class="sxs-lookup"><span data-stu-id="416e4-147">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="416e4-148">Aksi takdirde, kullanıcılar istendiğinde tooenter hello kimlik bilgilerinin kendilerini başlatma bağlı olması.</span><span class="sxs-lookup"><span data-stu-id="416e4-148">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="assign-a-user-tooan-application-directly"></a><span data-ttu-id="416e4-149">Bir kullanıcı tooan uygulama doğrudan atama</span><span class="sxs-lookup"><span data-stu-id="416e4-149">Assign a user tooan application directly</span></span>

<span data-ttu-id="416e4-150">tooassign bir veya daha fazla kullanıcı tooan uygulama, doğrudan başlangıç adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="416e4-150">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="416e4-151">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="416e4-151">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="416e4-152">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="416e4-152">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="416e4-153">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="416e4-153">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="416e4-154">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="416e4-154">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="416e4-155">Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.</span><span class="sxs-lookup"><span data-stu-id="416e4-155">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="416e4-156">Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**</span><span class="sxs-lookup"><span data-stu-id="416e4-156">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="416e4-157">Tooassign kullanıcı toofrom hello listesini hello uygulamasını seçin.</span><span class="sxs-lookup"><span data-stu-id="416e4-157">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="416e4-158">Merhaba uygulamanın yüklediği sonra tıklayın **kullanıcılar ve gruplar** hello uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="416e4-158">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="416e4-159">Hello tıklatın **Ekle** hello üstünde düğmesi **kullanıcılar ve gruplar** listesi tooopen hello **eklemek atama** dikey.</span><span class="sxs-lookup"><span data-stu-id="416e4-159">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="416e4-160">Merhaba tıklatın **kullanıcılar ve gruplar** hello seçicisini **eklemek atama** dikey.</span><span class="sxs-lookup"><span data-stu-id="416e4-160">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="416e4-161">Merhaba türü **tam adı** veya **e-posta adresi** hello atama ilgilenen hello kullanıcının **ad veya e-posta adresine göre arama** arama kutusu.</span><span class="sxs-lookup"><span data-stu-id="416e4-161">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="416e4-162">Merhaba getirin **kullanıcı** hello listesi tooreveal içinde bir **onay kutusunu**.</span><span class="sxs-lookup"><span data-stu-id="416e4-162">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="416e4-163">Kullanıcı toohello Hello onay kutusu sonraki toohello kullanıcının profili fotoğraf veya logosu tooadd tıklatın **seçili** listesi.</span><span class="sxs-lookup"><span data-stu-id="416e4-163">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="416e4-164">**İsteğe bağlı:** çok isterseniz**birden fazla kullanıcı ekleme**, başka bir tür **tam adı** veya **e-posta adresi** hello içine **ada göre ara veya e-posta adresi** arama kutusu ve bu kullanıcı toohello hello onay kutusunu tooadd tıklatın **seçili** listesi.</span><span class="sxs-lookup"><span data-stu-id="416e4-164">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="416e4-165">Kullanıcıların seçerek bittiğinde hello tıklatın **seçin** düğmesini tooadd bunları kullanıcılar ve gruplar toobe toohello listesi atanan toohello uygulama.</span><span class="sxs-lookup"><span data-stu-id="416e4-165">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="416e4-166">**İsteğe bağlı:** hello tıklatın **rolü Seç** hello seçicide **eklemek atama** dikey tooselect rol seçtiğiniz tooassign toohello kullanıcılar.</span><span class="sxs-lookup"><span data-stu-id="416e4-166">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="416e4-167">Merhaba tıklatın **atamak** düğmesini tooassign hello uygulama toohello seçilen kullanıcılar.</span><span class="sxs-lookup"><span data-stu-id="416e4-167">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

## <a name="assign-an-application-tooa-group-directly"></a><span data-ttu-id="416e4-168">Uygulama tooa grubu doğrudan atama</span><span class="sxs-lookup"><span data-stu-id="416e4-168">Assign an application tooa group directly</span></span>

<span data-ttu-id="416e4-169">bir veya daha fazla tooassign doğrudan tooan uygulama hello adımları aşağıdaki grupları:</span><span class="sxs-lookup"><span data-stu-id="416e4-169">tooassign one or more groups tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="416e4-170">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="416e4-170">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="416e4-171">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="416e4-171">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="416e4-172">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="416e4-172">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="416e4-173">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="416e4-173">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="416e4-174">Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.</span><span class="sxs-lookup"><span data-stu-id="416e4-174">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="416e4-175">Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**</span><span class="sxs-lookup"><span data-stu-id="416e4-175">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="416e4-176">Tooassign kullanıcı toofrom hello listesini hello uygulamasını seçin.</span><span class="sxs-lookup"><span data-stu-id="416e4-176">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="416e4-177">Merhaba uygulamanın yüklediği sonra tıklayın **kullanıcılar ve gruplar** hello uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="416e4-177">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="416e4-178">Hello tıklatın **Ekle** hello üstünde düğmesi **kullanıcılar ve gruplar** listesi tooopen hello **eklemek atama** dikey.</span><span class="sxs-lookup"><span data-stu-id="416e4-178">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="416e4-179">Merhaba tıklatın **kullanıcılar ve gruplar** hello seçicisini **eklemek atama** dikey.</span><span class="sxs-lookup"><span data-stu-id="416e4-179">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="416e4-180">Merhaba türü **tam grup adı** hello atama ilgilenen hello grubunun **ad veya e-posta adresine göre arama** arama kutusu.</span><span class="sxs-lookup"><span data-stu-id="416e4-180">Type in hello **full group name** of hello group you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="416e4-181">Merhaba getirin **grup** hello listesi tooreveal içinde bir **onay kutusunu**.</span><span class="sxs-lookup"><span data-stu-id="416e4-181">Hover over hello **group** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="416e4-182">Kullanıcı toohello Hello onay kutusu sonraki toohello grubun profili fotoğraf veya logosu tooadd tıklatın **seçili** listesi.</span><span class="sxs-lookup"><span data-stu-id="416e4-182">Click hello checkbox next toohello group’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="416e4-183">**İsteğe bağlı:** çok isterseniz**birden fazla grubu Ekle**, başka bir tür **tam grup adı** hello içine **ad veya e-posta adresine göre arama** arama kutusu tıklatıp hello onay kutusunu tooadd bu Grup toohello **seçili** listesi.</span><span class="sxs-lookup"><span data-stu-id="416e4-183">**Optional:** If you would like too**add more than one group**, type in another **full group name** into hello **Search by name or email address** search box, and click hello checkbox tooadd this group toohello **Selected** list.</span></span>

13. <span data-ttu-id="416e4-184">Grupları seçmek bittiğinde hello tıklatın **seçin** düğmesini tooadd bunları kullanıcılar ve gruplar toobe toohello listesi atanan toohello uygulama.</span><span class="sxs-lookup"><span data-stu-id="416e4-184">When you are finished selecting groups, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="416e4-185">**İsteğe bağlı:** hello tıklatın **rolü Seç** hello seçicide **eklemek atama** dikey tooselect rol tooassign toohello gruplar seçtiniz.</span><span class="sxs-lookup"><span data-stu-id="416e4-185">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello groups you have selected.</span></span>

15. <span data-ttu-id="416e4-186">Merhaba tıklatın **atamak** düğmesini tooassign hello uygulama toohello seçilen grupları.</span><span class="sxs-lookup"><span data-stu-id="416e4-186">Click hello **Assign** button tooassign hello application toohello selected groups.</span></span>

<span data-ttu-id="416e4-187">Seçtiğiniz hello kullanıcılar kısa bir süre mümkün toolaunch bu uygulamalarında değiştirdikten sonra erişim Paneli'ne hello.</span><span class="sxs-lookup"><span data-stu-id="416e4-187">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="416e4-188">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="416e4-188">Next steps</span></span>
[<span data-ttu-id="416e4-189">Uygulama proxy'si ile çoklu oturum açma tooyour uygulamaları sağlayın</span><span class="sxs-lookup"><span data-stu-id="416e4-189">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
