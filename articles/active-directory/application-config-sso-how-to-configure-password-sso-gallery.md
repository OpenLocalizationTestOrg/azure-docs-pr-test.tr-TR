---
title: "Parola tek oturum açma için Azure AD galeri uygulamanın yapılandırma | Microsoft Docs"
description: "Azure AD uygulama galerisinde zaten listelendiğinde güvenli parola tabanlı çoklu oturum açma için uygulama yapılandırma"
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
ms.openlocfilehash: d4dc110eb25c3e550ac4663d28e626a696b58f62
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="6d207-103">Parola tek oturum açma için Azure AD galeri uygulama yapılandırma</span><span class="sxs-lookup"><span data-stu-id="6d207-103">How to configure password single sign-on for an Azure AD Gallery application</span></span>

<span data-ttu-id="6d207-104">Bir uygulamadan eklediğinizde [Azure AD uygulama galerisinde](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery), bu uygulamada oturum açmak için kullanıcılarınızın istediğiniz seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="6d207-104">When you add an application from the [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery), you have the choice of how you want your users to sign in to that application.</span></span> <span data-ttu-id="6d207-105">Bu seçenek seçerek herhangi bir anda yapılandırabilirsiniz **çoklu oturum açma** bir kuruluş uygulamasında Gezinti öğede [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="6d207-105">You can configure this choice at any time by selecting the **Single Sign-on** navigation item on an Enterprise Application in the [Azure Portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="6d207-106">Çoklu oturum açma için kullanılabilen yöntemler biri [parola tabanlı çoklu oturum açma](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) seçeneği.</span><span class="sxs-lookup"><span data-stu-id="6d207-106">One of the single sign-on methods available to you is the [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) option.</span></span> <span data-ttu-id="6d207-107">Bu uygulamaları hızlı bir şekilde Azure AD ile tümleştirme başlamak için mükemmel bir yoldur ve olanak sağlar:</span><span class="sxs-lookup"><span data-stu-id="6d207-107">This is a great way to get started integrating applications into Azure AD quickly, and allows you to:</span></span>

-   <span data-ttu-id="6d207-108">Etkinleştirme **kullanıcılarınız için çoklu oturum açmayı** güvenli bir şekilde depolamak ve kullanıcı adları ve parolalar uygulamanın yeniden oynatmak tarafından Azure AD ile tümleşik</span><span class="sxs-lookup"><span data-stu-id="6d207-108">Enable **Single Sign-on for your users** by securely storing and replaying usernames and passwords for the application you’ve integrated with Azure AD</span></span>

-   <span data-ttu-id="6d207-109">**Destek oturum açma birden çok alan gerektiren uygulamalar** oturum açmak için daha fazlasını kullanıcı adı ve parola alanlarına gerektiren uygulamalar için</span><span class="sxs-lookup"><span data-stu-id="6d207-109">**Support applications that require multiple sign-in fields** for applications that require more than just username and password fields to sign in</span></span>

-   <span data-ttu-id="6d207-110">**Etiketleri özelleştirme** kullanıcılarınızın gördüğü kullanıcı adı ve parola giriş alanlarının [uygulama erişim Paneli'ne](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) kimlik bilgilerini girmeleri zaman</span><span class="sxs-lookup"><span data-stu-id="6d207-110">**Customize the labels** of the username and password input fields your users see on the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) when they enter their credentials</span></span>

-   <span data-ttu-id="6d207-111">İzin ver, **kullanıcılar** bunlar yazarak, el ile on tüm var olan uygulama hesaplarını için kendi kullanıcı adları ve parolalar sağlamak için [uygulama erişim paneli](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span><span class="sxs-lookup"><span data-stu-id="6d207-111">Allow your **users** to provide their own usernames and passwords for any existing application accounts they are typing in manually on the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span></span>

-   <span data-ttu-id="6d207-112">İzin bir **iş grubunun üyesi** kullanıcı adları ve parolaları kullanarak bir kullanıcıya atanmış belirtmek için [Self Servis uygulamaya erişim](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) özelliği</span><span class="sxs-lookup"><span data-stu-id="6d207-112">Allow a **member of the business group** to specify the usernames and passwords assigned to a user by using the [Self-Service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) feature</span></span>

-   <span data-ttu-id="6d207-113">İzin bir **yönetici** belirtmek için kullanıcı adları ve parolalar güncelleştirme kimlik bilgilerini kullanarak bir kullanıcıya atanmış özelliği ne zaman [bir kullanıcı için uygulama atama](#assign-a-user-to-an-application-directly)</span><span class="sxs-lookup"><span data-stu-id="6d207-113">Allow an **administrator** to specify the usernames and passwords assigned to a user by using the Update Credentials feature when [assigning a user to an application](#assign-a-user-to-an-application-directly)</span></span>

-   <span data-ttu-id="6d207-114">İzin bir **yönetici** belirtmek için paylaşılan kullanıcı adı veya parola güncelleştirme kimlik bilgilerini kullanarak bir grup kişi tarafından kullanılan özellik ne zaman [uygulama için bir grup atama](#assign-an-application-to-a-group-directly)</span><span class="sxs-lookup"><span data-stu-id="6d207-114">Allow an **administrator** to specify the shared username or password used by a group of people by using the Update Credentials feature when [assigning a group to an application](#assign-an-application-to-a-group-directly)</span></span>

<span data-ttu-id="6d207-115">Aşağıda nasıl etkinleştirebilirsiniz açıklar [parola tabanlı çoklu oturum açma](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) zaten bir uygulamaya [Azure AD uygulama galerisinde](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span><span class="sxs-lookup"><span data-stu-id="6d207-115">Below describes how you can enable [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) to an application that is already in the [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="6d207-116">Gerekli adımlara genel bakış</span><span class="sxs-lookup"><span data-stu-id="6d207-116">Overview of steps required</span></span>
<span data-ttu-id="6d207-117">Bir uygulama için gereken Azure AD galerisinden yapılandırmak için:</span><span class="sxs-lookup"><span data-stu-id="6d207-117">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="6d207-118">Azure AD Galeriden bir uygulama ekleme</span><span class="sxs-lookup"><span data-stu-id="6d207-118">Add an application from the Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="6d207-119">Uygulaması parola çoklu oturum açma için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="6d207-119">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

-   [<span data-ttu-id="6d207-120">Bir kullanıcı veya grup için uygulama atama</span><span class="sxs-lookup"><span data-stu-id="6d207-120">Assign the application to a user or a group</span></span>](#assign-the-application-to-a-user-or-a-group)

    -   [<span data-ttu-id="6d207-121">Kullanıcının uygulamaya doğrudan atayın</span><span class="sxs-lookup"><span data-stu-id="6d207-121">Assign a user to an application directly</span></span>](#assign-a-user-to-an-application-directly)

    -   [<span data-ttu-id="6d207-122">Bir gruba uygulama doğrudan atama</span><span class="sxs-lookup"><span data-stu-id="6d207-122">Assign an application to a group directly</span></span>](#assign-an-application-to-a-group-directly)

## <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="6d207-123">Azure AD Galeriden bir uygulama ekleme</span><span class="sxs-lookup"><span data-stu-id="6d207-123">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="6d207-124">Azure AD Galeriden bir uygulama eklemek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="6d207-124">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="6d207-125">Açık [Azure Portal](https://portal.azure.com) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="6d207-125">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="6d207-126">Açık **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** ana sol taraftaki gezinti menüsünde sonundaki.</span><span class="sxs-lookup"><span data-stu-id="6d207-126">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="6d207-127">Yazın **"Azure Active Directory**" Filtre Arama kutusuna seçip **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="6d207-127">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="6d207-128">tıklatın **kurumsal uygulamalar** Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="6d207-128">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="6d207-129">tıklatın **Ekle** düğmesine sağ üst köşede **kurumsal uygulamalar** dikey penceresi</span><span class="sxs-lookup"><span data-stu-id="6d207-129">click the **Add** button at the top-right corner on the **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="6d207-130">İçinde **bir ad girin** metin **galerisinden Ekle** bölümünde, uygulamanın adını yazın</span><span class="sxs-lookup"><span data-stu-id="6d207-130">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application</span></span>

7.  <span data-ttu-id="6d207-131">Çoklu oturum açma için yapılandırmak istediğiniz uygulamayı seçin</span><span class="sxs-lookup"><span data-stu-id="6d207-131">Select the application you want to configure for single sign-on</span></span>

8.  <span data-ttu-id="6d207-132">Uygulama eklemeden önce adını değiştirebilirsiniz **adı** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="6d207-132">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="6d207-133">Tıklatın **Ekle** düğmesi, bir uygulama eklemek için.</span><span class="sxs-lookup"><span data-stu-id="6d207-133">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="6d207-134">Kısa bir süre sonra uygulamanın yapılandırma dikey görüyor.</span><span class="sxs-lookup"><span data-stu-id="6d207-134">After a short period, you be able to see the application’s configuration blade.</span></span>

## <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="6d207-135">Uygulaması parola çoklu oturum açma için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="6d207-135">Configure the application for password single sign-on</span></span>

<span data-ttu-id="6d207-136">Bir uygulama için çoklu oturum açmayı yapılandırmak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="6d207-136">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="6d207-137">Açık [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="6d207-137">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="6d207-138">Açık **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** ana sol taraftaki gezinti menüsünde sonundaki.</span><span class="sxs-lookup"><span data-stu-id="6d207-138">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="6d207-139">Yazın **"Azure Active Directory**" Filtre Arama kutusuna seçip **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="6d207-139">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="6d207-140">tıklatın **kurumsal uygulamalar** Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="6d207-140">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="6d207-141">tıklatın **tüm uygulamaları** tüm uygulamaların bir listesini görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="6d207-141">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="6d207-142">Burada gösterisini istediğiniz uygulama görmüyorsanız kullanın **filtre** üst kısmındaki denetim **tüm uygulamalar listesini** ve **Göster** için seçenek **tüm uygulamaları.**</span><span class="sxs-lookup"><span data-stu-id="6d207-142">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="6d207-143">Çoklu oturum açma yapılandırmak istediğiniz uygulamayı seçin</span><span class="sxs-lookup"><span data-stu-id="6d207-143">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="6d207-144">Uygulamanın yüklediği sonra tıklayın **çoklu oturum açma** uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="6d207-144">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="6d207-145">Modunu seçin **parola tabanlı oturum açma.**</span><span class="sxs-lookup"><span data-stu-id="6d207-145">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="6d207-146">[Uygulamaya kullanıcılar atama](#assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="6d207-146">[Assign users to the application](#assign-a-user-to-an-application-directly).</span></span>

10. <span data-ttu-id="6d207-147">Ayrıca, kullanıcı adına kimlik bilgilerini kullanıcıları satırlarını seçerek ve tıklayarak sağlayabilirsiniz **güncelleştirme kimlik bilgileri** ve kullanıcılar adına kullanıcı adı ve parola girme.</span><span class="sxs-lookup"><span data-stu-id="6d207-147">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="6d207-148">Aksi takdirde, kullanıcılar başlatma sırasında kimlik kendilerini girmeniz istenir.</span><span class="sxs-lookup"><span data-stu-id="6d207-148">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="assign-a-user-to-an-application-directly"></a><span data-ttu-id="6d207-149">Kullanıcının uygulamaya doğrudan atayın</span><span class="sxs-lookup"><span data-stu-id="6d207-149">Assign a user to an application directly</span></span>

<span data-ttu-id="6d207-150">Bir veya daha fazla kullanıcının uygulamaya doğrudan atamak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="6d207-150">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="6d207-151">Açık [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="6d207-151">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="6d207-152">Açık **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** ana sol taraftaki gezinti menüsünde sonundaki.</span><span class="sxs-lookup"><span data-stu-id="6d207-152">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="6d207-153">Yazın **"Azure Active Directory**" Filtre Arama kutusuna seçip **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="6d207-153">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="6d207-154">tıklatın **kurumsal uygulamalar** Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="6d207-154">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="6d207-155">tıklatın **tüm uygulamaları** tüm uygulamaların bir listesini görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="6d207-155">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="6d207-156">Burada gösterisini istediğiniz uygulama görmüyorsanız kullanın **filtre** üst kısmındaki denetim **tüm uygulamalar listesini** ve **Göster** için seçenek **tüm uygulamaları.**</span><span class="sxs-lookup"><span data-stu-id="6d207-156">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="6d207-157">Listeden bir kullanıcıya atamak istediğiniz uygulamayı seçin.</span><span class="sxs-lookup"><span data-stu-id="6d207-157">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="6d207-158">Uygulamanın yüklediği sonra tıklayın **kullanıcılar ve gruplar** uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="6d207-158">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="6d207-159">Tıklatın **Ekle** üstünde düğmesini **kullanıcılar ve gruplar** açmak için liste **eklemek atama** dikey.</span><span class="sxs-lookup"><span data-stu-id="6d207-159">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="6d207-160">tıklatın **kullanıcılar ve gruplar** seçicisini **eklemek atama** dikey.</span><span class="sxs-lookup"><span data-stu-id="6d207-160">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="6d207-161">Yazın **tam adı** veya **e-posta adresi** içine atama ilgilenen kullanıcının **ad veya e-posta adresine göre arama** arama kutusu.</span><span class="sxs-lookup"><span data-stu-id="6d207-161">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="6d207-162">Üzerine gelerek **kullanıcı** ortaya çıkarmak için listedeki bir **onay kutusunu**.</span><span class="sxs-lookup"><span data-stu-id="6d207-162">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="6d207-163">Kullanıcının profil fotoğrafınız veya logosu, kullanıcı eklemek için yanındaki onay kutusuna tıklayın **seçili** listesi.</span><span class="sxs-lookup"><span data-stu-id="6d207-163">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="6d207-164">**İsteğe bağlı:** başlamayı tercih ederseniz **birden fazla kullanıcı ekleme**, başka bir tür **tam adı** veya **e-posta adresi** içine **ad veya e-posta adresine göre arama** arama kutusu ve bu kullanıcıyı eklemek için onay kutusunu işaretleyin **seçili** listesi.</span><span class="sxs-lookup"><span data-stu-id="6d207-164">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="6d207-165">Kullanıcıların seçerek bittiğinde tıklatın **seçin** düğmesi uygulamaya atanan kullanıcılar ve gruplar listesi eklemek için.</span><span class="sxs-lookup"><span data-stu-id="6d207-165">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="6d207-166">**İsteğe bağlı:** tıklatın **rolü Seç** seçicide **eklemek atama** seçtiğiniz kullanıcılara atamak için bir rol seçin dikey.</span><span class="sxs-lookup"><span data-stu-id="6d207-166">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="6d207-167">Tıklatın **atamak** uygulamayı Seçilen kullanıcılara atamak için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="6d207-167">Click the **Assign** button to assign the application to the selected users.</span></span>

## <a name="assign-an-application-to-a-group-directly"></a><span data-ttu-id="6d207-168">Bir gruba uygulama doğrudan atama</span><span class="sxs-lookup"><span data-stu-id="6d207-168">Assign an application to a group directly</span></span>

<span data-ttu-id="6d207-169">Bir veya daha fazla grupları doğrudan bir uygulamaya atamak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="6d207-169">To assign one or more groups to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="6d207-170">Açık [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="6d207-170">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="6d207-171">Açık **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** ana sol taraftaki gezinti menüsünde sonundaki.</span><span class="sxs-lookup"><span data-stu-id="6d207-171">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="6d207-172">Yazın **"Azure Active Directory**" Filtre Arama kutusuna seçip **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="6d207-172">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="6d207-173">tıklatın **kurumsal uygulamalar** Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="6d207-173">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="6d207-174">tıklatın **tüm uygulamaları** tüm uygulamaların bir listesini görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="6d207-174">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="6d207-175">Burada gösterisini istediğiniz uygulama görmüyorsanız kullanın **filtre** üst kısmındaki denetim **tüm uygulamalar listesini** ve **Göster** için seçenek **tüm uygulamaları.**</span><span class="sxs-lookup"><span data-stu-id="6d207-175">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="6d207-176">Listeden bir kullanıcıya atamak istediğiniz uygulamayı seçin.</span><span class="sxs-lookup"><span data-stu-id="6d207-176">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="6d207-177">Uygulamanın yüklediği sonra tıklayın **kullanıcılar ve gruplar** uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="6d207-177">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="6d207-178">Tıklatın **Ekle** üstünde düğmesini **kullanıcılar ve gruplar** açmak için liste **eklemek atama** dikey.</span><span class="sxs-lookup"><span data-stu-id="6d207-178">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="6d207-179">tıklatın **kullanıcılar ve gruplar** seçicisini **eklemek atama** dikey.</span><span class="sxs-lookup"><span data-stu-id="6d207-179">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="6d207-180">Yazın **tam grup adı** içine atama ilgilenen grubunun **ad veya e-posta adresine göre arama** arama kutusu.</span><span class="sxs-lookup"><span data-stu-id="6d207-180">Type in the **full group name** of the group you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="6d207-181">Üzerine gelerek **grup** ortaya çıkarmak için listedeki bir **onay kutusunu**.</span><span class="sxs-lookup"><span data-stu-id="6d207-181">Hover over the **group** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="6d207-182">Grubun profil fotoğrafınız veya logosu, kullanıcı eklemek için yanındaki onay kutusuna tıklayın **seçili** listesi.</span><span class="sxs-lookup"><span data-stu-id="6d207-182">Click the checkbox next to the group’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="6d207-183">**İsteğe bağlı:** başlamayı tercih ederseniz **birden fazla grubu Ekle**, başka bir tür **tam grup adı** içine **ad veya e-posta adresine göre arama** arama kutusu ve bu gruba eklemek için onay kutusunu işaretleyin **seçili** listesi.</span><span class="sxs-lookup"><span data-stu-id="6d207-183">**Optional:** If you would like to **add more than one group**, type in another **full group name** into the **Search by name or email address** search box, and click the checkbox to add this group to the **Selected** list.</span></span>

13. <span data-ttu-id="6d207-184">Grupları seçmek bittiğinde tıklatın **seçin** düğmesi uygulamaya atanan kullanıcılar ve gruplar listesi eklemek için.</span><span class="sxs-lookup"><span data-stu-id="6d207-184">When you are finished selecting groups, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="6d207-185">**İsteğe bağlı:** tıklatın **rolü Seç** seçicide **eklemek atama** seçtiğiniz gruplarına atamak için bir rol seçin dikey.</span><span class="sxs-lookup"><span data-stu-id="6d207-185">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the groups you have selected.</span></span>

15. <span data-ttu-id="6d207-186">Tıklatın **atamak** seçilen grupları uygulamaya atamak için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="6d207-186">Click the **Assign** button to assign the application to the selected groups.</span></span>

<span data-ttu-id="6d207-187">Kısa bir süre sonra seçtiğiniz kullanıcıların erişim panelinde bu uygulamaları başlatabilir.</span><span class="sxs-lookup"><span data-stu-id="6d207-187">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d207-188">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6d207-188">Next steps</span></span>
[<span data-ttu-id="6d207-189">Çoklu oturum açma uygulamalarınızı uygulama proxy'si ile sağlayın.</span><span class="sxs-lookup"><span data-stu-id="6d207-189">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
