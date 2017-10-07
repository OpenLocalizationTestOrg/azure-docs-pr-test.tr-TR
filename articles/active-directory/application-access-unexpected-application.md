---
title: "uygulamaları listem aaaUnexpected uygulamada | Microsoft Docs"
description: "Nasıl toosee kiracınızda tüm uygulamaları ve uygulamaların kurumsal uygulamalar altındaki tüm uygulamalar listenizde görüntülenme anlama"
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
ms.openlocfilehash: 2f974046b655bc36a05f002c56511a8a988cd01c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="unexpected-application-in-my-applications-list"></a><span data-ttu-id="e4f06-103">My uygulamalar listesinde beklenmeyen uygulama</span><span class="sxs-lookup"><span data-stu-id="e4f06-103">Unexpected application in my applications list</span></span>

<span data-ttu-id="e4f06-104">Bu makale uygulamaları görüntülenme toounderstand yardımcı, **tüm uygulamaları** altında listesinde **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="e4f06-104">This article help you toounderstand how applications appear in your **All Applications** list under **Enterprise Applications**.</span></span> 

## <a name="how-toosee-all-applications-in-your-tenant"></a><span data-ttu-id="e4f06-105">Nasıl toosee kiracınızda bulunan tüm uygulamalar</span><span class="sxs-lookup"><span data-stu-id="e4f06-105">How toosee all applications in your tenant</span></span>

<span data-ttu-id="e4f06-106">toosee tüm Kiracı uygulamalarda Merhaba, toouse hello gereksinim **filtre** tooshow kontrol **tüm uygulamaları** hello altında **tüm uygulamaları** listesi.</span><span class="sxs-lookup"><span data-stu-id="e4f06-106">toosee all hello applications in your tenant, you need toouse hello **Filter** control tooshow **All Applications** under hello **All Applications** list.</span></span> <span data-ttu-id="e4f06-107">toodo Bu, başlangıç adımları aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="e4f06-107">toodo this, follow hello steps below:</span></span>

1.  <span data-ttu-id="e4f06-108">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="e4f06-108">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="e4f06-109">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="e4f06-109">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e4f06-110">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="e4f06-110">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e4f06-111">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="e4f06-111">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="e4f06-112">Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.</span><span class="sxs-lookup"><span data-stu-id="e4f06-112">click **All Applications** tooview a list of all your applications.</span></span>

6.  <span data-ttu-id="e4f06-113">Hello kullan hello tıklatın **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini**.</span><span class="sxs-lookup"><span data-stu-id="e4f06-113">click hello use hello **Filter** control at hello top of hello **All Applications List**.</span></span>

7.  <span data-ttu-id="e4f06-114">Merhaba üzerinde **filtre** dikey penceresinde, kümesi hello **Göster** çok seçenek**tüm uygulamaları.**</span><span class="sxs-lookup"><span data-stu-id="e4f06-114">On hello **Filter** blade, set hello **Show** option too**All Applications.**</span></span>

## <a name="why-does-a-specific-application-appear-in-my-all-applications-list"></a><span data-ttu-id="e4f06-115">Belirli bir uygulama my tüm uygulamalar listesinde neden görünüyor?</span><span class="sxs-lookup"><span data-stu-id="e4f06-115">Why does a specific application appear in my all applications list?</span></span>

<span data-ttu-id="e4f06-116">Çok filtre zaman**tüm uygulamaları**, hello **tüm uygulamaları** **listesi** her hizmet sorumlusu nesnesi kiracınızda gösterir.</span><span class="sxs-lookup"><span data-stu-id="e4f06-116">When filtered too**All Applications**, hello **All Applications** **List** shows every Service Principal object in your tenant.</span></span> <span data-ttu-id="e4f06-117">Hizmet sorumlusu nesneleri, çeşitli yollarla bu listede görünebilir:</span><span class="sxs-lookup"><span data-stu-id="e4f06-117">Service Principal objects can appear in this list in a various ways:</span></span>

1.  <span data-ttu-id="e4f06-118">Herhangi bir uygulama hello uygulama Galerisi'nden eklediğinizde dahil olmak üzere:</span><span class="sxs-lookup"><span data-stu-id="e4f06-118">When you add any application from hello application gallery, including:</span></span>

   1. <span data-ttu-id="e4f06-119">**Azure AD galeri uygulamaları** – bir tek oturum açma için Azure AD ile önceden tümleştirilmiş uygulama.</span><span class="sxs-lookup"><span data-stu-id="e4f06-119">**Azure AD Gallery Applications** – An application that has been pre-integrated for single sign-on with Azure AD.</span></span>

   2. <span data-ttu-id="e4f06-120">**Uygulama proxy'si uygulamalar** – tooprovide güvenli çoklu oturum açma tooexternally istediğiniz şirket içi ortamınızda çalışan bir uygulama.</span><span class="sxs-lookup"><span data-stu-id="e4f06-120">**Application Proxy Applications** – An application running in your on-premises environment that you want tooprovide secure single-sign on tooexternally.</span></span>

   3. <span data-ttu-id="e4f06-121">**Özel geliştirilmiş uygulamaları** – üzerinde toodevelop kuruluşunuz isteyen bir uygulama hello Azure AD uygulama geliştirme platformu, ancak var henüz.</span><span class="sxs-lookup"><span data-stu-id="e4f06-121">**Custom-developed Applications** – An application that your organization wishes toodevelop on hello Azure AD Application Development Platform, but that may not exist yet.</span></span>

   4. <span data-ttu-id="e4f06-122">**Galeri olmayan uygulamaları** – kendi uygulamalarınızı Getir!</span><span class="sxs-lookup"><span data-stu-id="e4f06-122">**Non-Gallery Applications** – Bring your own applications!</span></span> <span data-ttu-id="e4f06-123">İstediğiniz herhangi bir web bağlantıyı ya da bir kullanıcı adı ve parola alanı işleyen herhangi bir uygulama SAML veya Openıd Connect protokollerini destekler veya çoklu oturum açma için Azure AD ile toointegrate istediğiniz SCIM'yi destekler.</span><span class="sxs-lookup"><span data-stu-id="e4f06-123">Any web link you want, or any application which renders a username and password field, supports SAML or OpenID Connect protocols, or supports SCIM which you wish toointegrate for single sign-on with Azure AD.</span></span>

2.  <span data-ttu-id="e4f06-124">İçin imzalarken veya 3'e, oturum açma<sup>rd</sup> taraf uygulama Azure Active Directory ile tümleşik.</span><span class="sxs-lookup"><span data-stu-id="e4f06-124">When signing up for, or signing in to, a 3<sup>rd</sup> party application integrated with Azure Active Directory.</span></span> <span data-ttu-id="e4f06-125">Bunun bir örneği [Smartsheet](https://app.smartsheet.com/b/home) veya [DocuSign](https://www.docusign.net/member/MemberLogin.aspx).</span><span class="sxs-lookup"><span data-stu-id="e4f06-125">One example of this is [Smartsheet](https://app.smartsheet.com/b/home) or [DocuSign](https://www.docusign.net/member/MemberLogin.aspx).</span></span>

3.  <span data-ttu-id="e4f06-126">İçin imzalama veya bir lisans tooa kullanıcı veya grup tooa birinci taraf uygulama ekleme, ister [Microsoft Office 365](http://products.office.com/).</span><span class="sxs-lookup"><span data-stu-id="e4f06-126">When signing up for, or adding a license tooa user or a group tooa first party application, like [Microsoft Office 365](http://products.office.com/).</span></span>

4.  <span data-ttu-id="e4f06-127">Hello kullanarak özel geliştirilmiş bir uygulama oluşturarak yeni bir uygulama kaydı eklediğinizde [uygulama kayıt defteri](https://docs.microsoft.com/azure/active-directory/active-directory-app-registration).</span><span class="sxs-lookup"><span data-stu-id="e4f06-127">When you add a new application registration by creating a custom-developed application using hello [Application Registry](https://docs.microsoft.com/azure/active-directory/active-directory-app-registration).</span></span>

5.  <span data-ttu-id="e4f06-128">Hello kullanarak özel geliştirilmiş bir uygulama oluşturarak yeni bir uygulama kaydı eklediğinizde [V2.0 uygulama kayıt portalı](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-app-registration#visit-the-microsoft-app-registration-portal).</span><span class="sxs-lookup"><span data-stu-id="e4f06-128">When you add a new application registration by creating a custom-developed application using hello [V2.0 Application Registration Portal](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-app-registration#visit-the-microsoft-app-registration-portal).</span></span>

6.  <span data-ttu-id="e4f06-129">Bir uygulama eklediğinizde Visual Studio'nun kullanarak geliştirirken [ASP.net kimlik doğrulama yöntemleri](http://www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauthoptions) veya [bağlantılı Hizmetler](http://blogs.msdn.com/b/visualstudio/archive/2014/11/19/connecting-to-cloud-services.aspx).</span><span class="sxs-lookup"><span data-stu-id="e4f06-129">When you add an application you’re developing using Visual Studio’s [ASP.net Authentication Methods](http://www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauthoptions) or [Connected Services](http://blogs.msdn.com/b/visualstudio/archive/2014/11/19/connecting-to-cloud-services.aspx).</span></span>

7.  <span data-ttu-id="e4f06-130">Hello kullanarak bir hizmet sorumlusu nesnesi oluştururken [Azure AD PowerShell Modülü](/powershell/azure/install-adv2?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="e4f06-130">When you create a service principal object using hello [Azure AD PowerShell Module](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

8.  <span data-ttu-id="e4f06-131">Olduğunda, [tooan uygulama onay](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) bir kiracı yönetici toouse veri olarak.</span><span class="sxs-lookup"><span data-stu-id="e4f06-131">When you [consent tooan application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) as an administrator toouse data in your tenant.</span></span>

9.  <span data-ttu-id="e4f06-132">Zaman bir [kullanıcı izin tooan uygulama](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) kiracınızda toouse veri.</span><span class="sxs-lookup"><span data-stu-id="e4f06-132">When a [user consents tooan application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) toouse data in your tenant.</span></span>

10. <span data-ttu-id="e4f06-133">Kiracınızda verileri depolamak belirli hizmetleri etkinleştirdiğinizde.</span><span class="sxs-lookup"><span data-stu-id="e4f06-133">When you enable certain services that store data in your tenant.</span></span> <span data-ttu-id="e4f06-134">Bunun bir örneği olan parola hangi modellenir sıfırlama, güvenli bir şekilde İlkesi bir hizmet asıl toostore parolanızı sıfırlayın.</span><span class="sxs-lookup"><span data-stu-id="e4f06-134">One example of this is Password Reset, which is modeled as a service principal toostore your password reset policy securely.</span></span>

<span data-ttu-id="e4f06-135">uygulamaları tooyour dizin nasıl eklenir hakkında daha fazla ayrıntı tooget okuma [neden ve nasıl uygulamaları tooAzure AD eklenen](https://docs.microsoft.com/azure/active-directory/develop/active-directory-how-applications-are-added).</span><span class="sxs-lookup"><span data-stu-id="e4f06-135">tooget more details on how apps are added tooyour directory, read [How and why applications are added tooAzure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-how-applications-are-added).</span></span>

## <a name="i-want-tooremove-a-specific-users-or-groups-assignment-tooan-application"></a><span data-ttu-id="e4f06-136">Bu belirli kullanıcının veya grubun atama tooan uygulama tooremove istiyorum</span><span class="sxs-lookup"><span data-stu-id="e4f06-136">I want tooremove a specific user’s or group’s assignment tooan application</span></span>

<span data-ttu-id="e4f06-137">tooremove bir kullanıcı veya grup ataması tooan uygulama adımları hello listelenen hello [bir kuruluş uygulama Azure Active Directory'de bir kullanıcı veya grup atamasını kaldırmak](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) makalesi.</span><span class="sxs-lookup"><span data-stu-id="e4f06-137">tooremove a user or group assignment tooan application, follow hello steps listed in hello [Remove a user or group assignment from an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) article.</span></span>

## <a name="i-want-toodisable-all-access-tooan-application-for-every-user"></a><span data-ttu-id="e4f06-138">Her kullanıcı için tüm erişim tooan uygulama toodisable istiyorum</span><span class="sxs-lookup"><span data-stu-id="e4f06-138">I want toodisable all access tooan application for every user</span></span>

<span data-ttu-id="e4f06-139">toodisable tüm kullanıcı oturum açma işlemleri tooan uygulama hello adımları hello listelenen [kullanıcı oturum açma işlemlerine Azure Active Directory'de bir kurumsal uygulama için devre dışı bırakma](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) makalesi.</span><span class="sxs-lookup"><span data-stu-id="e4f06-139">toodisable all user sign-ins tooan application, follow hello steps listed in hello [Disable user sign-ins for an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) article.</span></span>

## <a name="i-want-toodelete-an-application-entirely"></a><span data-ttu-id="e4f06-140">Toodelete uygulamanın tamamen istiyorum</span><span class="sxs-lookup"><span data-stu-id="e4f06-140">I want toodelete an application entirely</span></span>

<span data-ttu-id="e4f06-141">çok**bir uygulamayı silmek**, aşağıdaki hello yönergeleri izleyin:</span><span class="sxs-lookup"><span data-stu-id="e4f06-141">too**delete an application**, follow hello instructions below:</span></span>

1.  <span data-ttu-id="e4f06-142">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="e4f06-142">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="e4f06-143">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="e4f06-143">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e4f06-144">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="e4f06-144">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e4f06-145">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="e4f06-145">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="e4f06-146">Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.</span><span class="sxs-lookup"><span data-stu-id="e4f06-146">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="e4f06-147">Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**</span><span class="sxs-lookup"><span data-stu-id="e4f06-147">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="e4f06-148">Toodelete hello uygulamasını seçin.</span><span class="sxs-lookup"><span data-stu-id="e4f06-148">Select hello application you want toodelete.</span></span>

7.  <span data-ttu-id="e4f06-149">Merhaba uygulamanın yüklediği sonra tıklayın **silmek** hello üst uygulamanın simgesinden **genel bakış** dikey.</span><span class="sxs-lookup"><span data-stu-id="e4f06-149">Once hello application loads, click **Delete** icon from hello top application’s **Overview** blade.</span></span>

## <a name="i-want-toodisable-all-future-user-consent-operations-tooany-application"></a><span data-ttu-id="e4f06-150">Tüm gelecekteki kullanıcı onayı işlemleri tooany uygulamasını toodisable istiyorum</span><span class="sxs-lookup"><span data-stu-id="e4f06-150">I want toodisable all future user consent operations tooany application</span></span>

<span data-ttu-id="e4f06-151">Tüm dizin önlemek için son kullanıcıların onaylıyorsunuz tooany uygulamasından kullanıcı izni devre dışı bırakılıyor.</span><span class="sxs-lookup"><span data-stu-id="e4f06-151">Disabling user consent for your entire directory prevent end users from consenting tooany application.</span></span> <span data-ttu-id="e4f06-152">Yöneticiler hala kullanıcının behalves üzerinde onay.</span><span class="sxs-lookup"><span data-stu-id="e4f06-152">Administrators can still consent on user’s behalves.</span></span> <span data-ttu-id="e4f06-153">uygulama hakkında daha fazla toolearn onay ve neden olabilir veya bu, okuma toodo istemeyen [anlama kullanıcı ve yönetici onayı](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).</span><span class="sxs-lookup"><span data-stu-id="e4f06-153">toolearn more about application consent, and why you may or may not wish toodo this, read [Understanding user and admin consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).</span></span>

<span data-ttu-id="e4f06-154">çok**tüm dizininizdeki tüm gelecekteki kullanıcı onayı işlemleri devre dışı**, aşağıdaki hello yönergeleri izleyin:</span><span class="sxs-lookup"><span data-stu-id="e4f06-154">too**disable all future user consent operations in your entire directory**, follow hello instructions below:</span></span>

1.  <span data-ttu-id="e4f06-155">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="e4f06-155">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="e4f06-156">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="e4f06-156">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e4f06-157">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="e4f06-157">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e4f06-158">Tıklatın **kullanıcılar ve gruplar** hello Gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="e4f06-158">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="e4f06-159">Tıklatın **kullanıcı ayarlarını**.</span><span class="sxs-lookup"><span data-stu-id="e4f06-159">click **User settings**.</span></span>

6.  <span data-ttu-id="e4f06-160">Tüm gelecekteki kullanıcı onayı işlemleri hello ayarı tarafından devre dışı **kullanıcıların kendi verilerini uygulamaları tooaccess izin verebilir** çok geçiş**Hayır** hello tıklatıp **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e4f06-160">Disable all future user consent operations by setting hello **Users can allow apps tooaccess their data** toggle too**No** and click hello **Save** button.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e4f06-161">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e4f06-161">Next steps</span></span>
[<span data-ttu-id="e4f06-162">Azure Active Directory ile uygulamaları yönetme</span><span class="sxs-lookup"><span data-stu-id="e4f06-162">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
