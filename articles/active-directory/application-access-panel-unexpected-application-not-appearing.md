---
title: "Merhaba erişim panelinde atanan aaaAn uygulama görünmesini değil | Microsoft Docs"
description: "Bir uygulama hello erişim paneli görünmeyen neden sorun giderme"
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
ms.reviwer: japere
ms.openlocfilehash: 089883f406267df4552c7fc991883f335ad49fd5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="an-assigned-application-is-not-appearing-on-hello-access-panel"></a><span data-ttu-id="4d454-103">Atanmış bir uygulama hello erişim panelinde görünmüyor</span><span class="sxs-lookup"><span data-stu-id="4d454-103">An assigned application is not appearing on hello access panel</span></span>

<span data-ttu-id="4d454-104">Merhaba erişim paneli bir kullanıcı bir iş sağlayan bir web tabanlı portal ya da Okul hesabı Azure Active Directory (Azure AD) tooview ve başlangıç bulut tabanlı uygulamalarda bu hello Azure AD Yöneticisi bunları erişim izni.</span><span class="sxs-lookup"><span data-stu-id="4d454-104">hello Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) tooview and start cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="4d454-105">Bu uygulamalar hello Azure AD portalında hello kullanıcı adına yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="4d454-105">These applications are configured on behalf of hello user in hello Azure AD portal.</span></span> <span data-ttu-id="4d454-106">Merhaba uygulaması düzgün şekilde yapılandırılmalıdır ve atanan toohello kullanıcı veya grup hello kullanıcı toosee hello hello erişim paneli uygulamada üyesidir.</span><span class="sxs-lookup"><span data-stu-id="4d454-106">hello application must be configured properly and assigned toohello user or a group hello user is a member of toosee hello application in hello Access Panel.</span></span>

<span data-ttu-id="4d454-107">bir kullanıcı için görüyor olabilirsiniz uygulamalarının Hello türü kategorileri aşağıdaki hello ayrılır:</span><span class="sxs-lookup"><span data-stu-id="4d454-107">hello type of apps a user may be seeing fall in hello following categories:</span></span>

-   <span data-ttu-id="4d454-108">Office 365 uygulamaları</span><span class="sxs-lookup"><span data-stu-id="4d454-108">Office 365 Applications</span></span>

-   <span data-ttu-id="4d454-109">Federasyon tabanlı SSO ile yapılandırılan Microsoft ve üçüncü taraf uygulamalar</span><span class="sxs-lookup"><span data-stu-id="4d454-109">Microsoft and third-party applications configured with federation-based SSO</span></span>

-   <span data-ttu-id="4d454-110">Parola tabanlı SSO uygulamaları</span><span class="sxs-lookup"><span data-stu-id="4d454-110">Password-based SSO applications</span></span>

-   <span data-ttu-id="4d454-111">Varolan SSO çözümleriyle uygulamaları</span><span class="sxs-lookup"><span data-stu-id="4d454-111">Applications with existing SSO solutions</span></span>

## <a name="general-issues-toocheck-first"></a><span data-ttu-id="4d454-112">Genel toocheck ilk sorunları</span><span class="sxs-lookup"><span data-stu-id="4d454-112">General issues toocheck first</span></span>

-   <span data-ttu-id="4d454-113">Bir uygulamayı yalnızca tooa kullanıcı eklendiyse, hello uygulama eklediyseniz toosign içeri ve dışarı yeniden hello kullanıcının erişim paneline sonra birkaç dakika toosee deneyin.</span><span class="sxs-lookup"><span data-stu-id="4d454-113">If an application was just added tooa user, try toosign in and out again into hello user’s Access Panel after a few minutes toosee if hello application is added.</span></span>

-   <span data-ttu-id="4d454-114">Bir lisans yalnızca bir kullanıcı veya grup hello kullanıcı kaldırıldıysa bu üyesi hello boyutu ve karmaşıklığı yapılan değişiklikleri toobe hello grubunun bağlı olarak uzun bir süre devam edebilir ' dir.</span><span class="sxs-lookup"><span data-stu-id="4d454-114">If a license was just removed from a user or group hello user is a member of this may take a long time, depending on hello size and complexity of hello group for changes toobe made.</span></span> <span data-ttu-id="4d454-115">Erişim paneli hello oturum açmadan önce ek süresi için izin verin.</span><span class="sxs-lookup"><span data-stu-id="4d454-115">Allow for extra time before signing into hello Access Panel.</span></span>

## <a name="problems-related-tooapplication-configuration"></a><span data-ttu-id="4d454-116">Sorunları ilgili tooapplication yapılandırma</span><span class="sxs-lookup"><span data-stu-id="4d454-116">Problems related tooapplication configuration</span></span>

<span data-ttu-id="4d454-117">Düzgün yapılandırılmadığından, bir uygulama kullanıcının erişim panelinde görünüyor değil.</span><span class="sxs-lookup"><span data-stu-id="4d454-117">An application may not be appearing in a user’s Access Panel because it is not configured properly.</span></span> <span data-ttu-id="4d454-118">Aşağıda ilgili tooapplication yapılandırma sorunlarını gidermek için kullanabileceğiniz bazı yöntemler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="4d454-118">Below are some ways you can troubleshoot issues related tooapplication configuration:</span></span>

-   [<span data-ttu-id="4d454-119">Azure AD galeri uygulaması için çoklu oturum açmayı tooconfigure nasıl Federasyon</span><span class="sxs-lookup"><span data-stu-id="4d454-119">How tooconfigure federated single sign-on for an Azure AD gallery application</span></span>](#how-to-configure-federated-single-sign-on-for-an-azure-ad-gallery-application)

-   [<span data-ttu-id="4d454-120">Nasıl bir galeri olmayan uygulama için çoklu oturum açmayı tooconfigure Federasyon</span><span class="sxs-lookup"><span data-stu-id="4d454-120">How tooconfigure federated single sign-on for a non-gallery application</span></span>](#how-to-configure-federated-single-sign-on-for-a-non-gallery-application)

-   [<span data-ttu-id="4d454-121">Nasıl tooconfigure parola tek oturum açma uygulaması için Azure AD galeri uygulaması</span><span class="sxs-lookup"><span data-stu-id="4d454-121">How tooconfigure a password single sign-on application for an Azure AD gallery application</span></span>](#how-to-configure-password-single-sign-on-for-a-non-gallery-application)

-   [<span data-ttu-id="4d454-122">Nasıl tooconfigure parola tek oturum açma uygulaması Galerisi olmayan uygulama</span><span class="sxs-lookup"><span data-stu-id="4d454-122">How tooconfigure a password single sign-on application for a non-gallery application</span></span>](#how-to-configure-password-single-sign-on-for-a-non-gallery-application)

### <a name="how-tooconfigure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="4d454-123">Azure AD galeri uygulaması için çoklu oturum açmayı tooconfigure nasıl Federasyon</span><span class="sxs-lookup"><span data-stu-id="4d454-123">How tooconfigure federated single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="4d454-124">Kurumsal çoklu oturum açma özelliğine sahip etkin hello Azure AD galerisinde tüm uygulamaları kullanılabilir adım adım öğretici sahiptir.</span><span class="sxs-lookup"><span data-stu-id="4d454-124">All applications in hello Azure AD gallery enabled with Enterprise Single Sign-On capability has a step-by-step tutorial available.</span></span> <span data-ttu-id="4d454-125">Merhaba erişebilirsiniz [nasıl öğreticiler listesi toointegrate SaaS uygulamaları Azure Active Directory ile](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) ayrıntılı adım adım yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="4d454-125">You can access hello [List of tutorials on how toointegrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for a detail step-by-step guidance.</span></span>

<span data-ttu-id="4d454-126">tooconfigure hello Azure AD Galeriden bir uygulama şunları yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="4d454-126">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="4d454-127">Hello Azure AD Galeriden bir uygulama ekleme</span><span class="sxs-lookup"><span data-stu-id="4d454-127">Add an application from hello Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="4d454-128">Azure AD (oturum açma URL'si, tanımlayıcı, yanıt URL'si) Hello uygulamanın meta veri değerlerini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="4d454-128">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="4d454-129">Kullanıcı tanımlayıcısı seçin ve kullanıcı öznitelikleri gönderilen toobe toohello uygulaması ekleyin</span><span class="sxs-lookup"><span data-stu-id="4d454-129">Select User Identifier and add user attributes toobe sent toohello application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="4d454-130">Azure AD meta verileri ve sertifika alma</span><span class="sxs-lookup"><span data-stu-id="4d454-130">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="4d454-131">Merhaba uygulaması (oturum açma URL'si, veren, oturum kapatma URL'si ve sertifika) Azure AD meta veri değerlerini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="4d454-131">Configure Azure AD metadata values in hello application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

#### <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="4d454-132">Hello Azure AD Galeriden bir uygulama ekleme</span><span class="sxs-lookup"><span data-stu-id="4d454-132">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="4d454-133">tooadd hello Azure AD galeri, bir uygulamadan hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="4d454-133">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="4d454-134">Açık hello [Azure Portal](https://portal.azure.com) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="4d454-134">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="4d454-135">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="4d454-135">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4d454-136">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="4d454-136">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4d454-137">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="4d454-137">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4d454-138">Merhaba tıklatın **Ekle** hello sağ üst köşesindeki hello düğmesi **kurumsal uygulamalar** dikey.</span><span class="sxs-lookup"><span data-stu-id="4d454-138">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="4d454-139">Merhaba, **bir ad girin** hello metin **hello galerisinden Ekle** bölümü, hello uygulamasının türü hello adı.</span><span class="sxs-lookup"><span data-stu-id="4d454-139">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application.</span></span>

7.  <span data-ttu-id="4d454-140">Çoklu oturum açma için tooconfigure istediğiniz hello uygulaması'nı seçin.</span><span class="sxs-lookup"><span data-stu-id="4d454-140">Select hello application you want tooconfigure for single sign-on.</span></span>

8.  <span data-ttu-id="4d454-141">Merhaba uygulaması eklemeden önce hello adını değiştirebilirsiniz **adı** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="4d454-141">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="4d454-142">Tıklatın **Ekle** button, tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="4d454-142">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="4d454-143">Kısa bir süre sonra mümkün toosee hello uygulamanın yapılandırma dikey olabilir.</span><span class="sxs-lookup"><span data-stu-id="4d454-143">After a short period, you be able toosee hello application’s configuration blade.</span></span>

#### <a name="configure-single-sign-on-for-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="4d454-144">Hello Azure AD Galeriden bir uygulama için çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="4d454-144">Configure single sign-on for an application from hello Azure AD gallery</span></span>

<span data-ttu-id="4d454-145">tooconfigure çoklu oturum açma bir uygulama için başlangıç adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="4d454-145">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="4d454-146">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="4d454-146">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="4d454-147">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="4d454-147">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4d454-148">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="4d454-148">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4d454-149">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="4d454-149">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4d454-150">Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.</span><span class="sxs-lookup"><span data-stu-id="4d454-150">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="4d454-151">Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**</span><span class="sxs-lookup"><span data-stu-id="4d454-151">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="4d454-152">Tooconfigure çoklu oturum açma hello uygulamasını seçin.</span><span class="sxs-lookup"><span data-stu-id="4d454-152">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="4d454-153">Merhaba uygulamanın yüklediği sonra hello tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="4d454-153">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="4d454-154">Seçin **SAML tabanlı oturum açma** hello gelen **modu** açılır.</span><span class="sxs-lookup"><span data-stu-id="4d454-154">Select **SAML-based Sign-on** from hello **Mode** dropdown.</span></span>

9.  <span data-ttu-id="4d454-155">Merhaba gerekli değerleri girin **etki alanı ve URL'ler.**</span><span class="sxs-lookup"><span data-stu-id="4d454-155">Enter hello required values in **Domain and URLs.**</span></span> <span data-ttu-id="4d454-156">Bu değerleri hello uygulama satıcısından almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="4d454-156">You should get these values from hello application vendor.</span></span>

   1. <span data-ttu-id="4d454-157">SP tarafından başlatılan SSO'yu olarak tooconfigure Merhaba uygulaması hello oturum URL'yi, gerekli bir değerdir.</span><span class="sxs-lookup"><span data-stu-id="4d454-157">tooconfigure hello application as SP-initiated SSO, hello Sign on URL it’s a required value.</span></span> <span data-ttu-id="4d454-158">Bazı uygulamalar için hello tanımlayıcısı da gerekli bir değerdir.</span><span class="sxs-lookup"><span data-stu-id="4d454-158">For some applications, hello Identifier is also a required value.</span></span>

   2. <span data-ttu-id="4d454-159">IDP tarafından başlatılan SSO'yu olarak tooconfigure Merhaba uygulaması hello yanıt URL'si gerekli bir değerdir.</span><span class="sxs-lookup"><span data-stu-id="4d454-159">tooconfigure hello application as IdP-initiated SSO, hello Reply URL it’s a required value.</span></span> <span data-ttu-id="4d454-160">Bazı uygulamalar için hello tanımlayıcısı da gerekli bir değerdir.</span><span class="sxs-lookup"><span data-stu-id="4d454-160">For some applications, hello Identifier is also a required value.</span></span>

10. <span data-ttu-id="4d454-161">**İsteğe bağlı:** tıklatın **Göster Gelişmiş URL ayarları** toosee hello gerekli olmayan değer istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="4d454-161">**Optional:** click **Show advanced URL settings** if you want toosee hello non-required values.</span></span>

11. <span data-ttu-id="4d454-162">Merhaba, **kullanıcı öznitelikleri**, select hello hello kullanıcılarınız için benzersiz tanımlayıcı **kullanıcı tanımlayıcısı** açılır.</span><span class="sxs-lookup"><span data-stu-id="4d454-162">In hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

12. <span data-ttu-id="4d454-163">**İsteğe bağlı:** tıklatın **Görünüm ve diğer tüm kullanıcı özniteliklerini düzenleme** tooedit Merhaba, kullanıcı oturum açtığında gönderilen toobe toohello hello SAML belirteci uygulamada öznitelikleri.</span><span class="sxs-lookup"><span data-stu-id="4d454-163">**Optional:** click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="4d454-164">bir öznitelik tooadd:</span><span class="sxs-lookup"><span data-stu-id="4d454-164">tooadd an attribute:</span></span>

   1. <span data-ttu-id="4d454-165">tıklatın **Ekle özniteliği**.</span><span class="sxs-lookup"><span data-stu-id="4d454-165">click **Add attribute**.</span></span> <span data-ttu-id="4d454-166">Merhaba girin **adı** ve hello select hello **değeri** gelen hello açılır.</span><span class="sxs-lookup"><span data-stu-id="4d454-166">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="4d454-167">Tıklatın **kaydedin.**</span><span class="sxs-lookup"><span data-stu-id="4d454-167">click **Save.**</span></span> <span data-ttu-id="4d454-168">Yeni bir öznitelik hello hello tablosundaki bakın.</span><span class="sxs-lookup"><span data-stu-id="4d454-168">You see hello new attribute in hello table.</span></span>

13. <span data-ttu-id="4d454-169">tıklatın **yapılandırma &lt;uygulama adı&gt;**  tooaccess belgelerine nasıl tooconfigure çoklu oturum açma hello uygulamada.</span><span class="sxs-lookup"><span data-stu-id="4d454-169">click **Configure &lt;application name&gt;** tooaccess documentation on how tooconfigure single sign-on in hello application.</span></span> <span data-ttu-id="4d454-170">Ayrıca, hello meta verileri URL'leri ve gerekli sertifika toosetup SSO hello uygulamayla sahiptir.</span><span class="sxs-lookup"><span data-stu-id="4d454-170">Also, you has hello metadata URLs and certificate required toosetup SSO with hello application.</span></span>

14. <span data-ttu-id="4d454-171">tıklatın **kaydetmek** toosave hello yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="4d454-171">click **Save** toosave hello configuration.</span></span>

15. <span data-ttu-id="4d454-172">Kullanıcıların toohello uygulama atayın.</span><span class="sxs-lookup"><span data-stu-id="4d454-172">Assign users toohello application.</span></span>

#### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a><span data-ttu-id="4d454-173">Kullanıcı tanımlayıcısı seçin ve kullanıcı öznitelikleri gönderilen toobe toohello uygulaması ekleyin</span><span class="sxs-lookup"><span data-stu-id="4d454-173">Select User Identifier and add user attributes toobe sent toohello application</span></span>

<span data-ttu-id="4d454-174">tooselect kullanıcı tanımlayıcısı Merhaba veya kullanıcı öznitelikleri ekleme, hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="4d454-174">tooselect hello User Identifier or add user attributes, follow hello steps below:</span></span>

1.  <span data-ttu-id="4d454-175">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="4d454-175">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="4d454-176">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="4d454-176">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4d454-177">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="4d454-177">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4d454-178">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="4d454-178">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4d454-179">Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.</span><span class="sxs-lookup"><span data-stu-id="4d454-179">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="4d454-180">Merhaba uygulaması tooshow burada yedeklemek istediğiniz görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**</span><span class="sxs-lookup"><span data-stu-id="4d454-180">If you do not see hello application you want tooshow up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="4d454-181">Çoklu oturum açma yapılandırdığınız hello uygulaması'nı seçin.</span><span class="sxs-lookup"><span data-stu-id="4d454-181">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="4d454-182">Merhaba uygulamanın yüklediği sonra hello tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="4d454-182">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="4d454-183">Merhaba altında **kullanıcı öznitelikleri** bölümünde, select hello hello kullanıcılarınız için benzersiz tanımlayıcı **kullanıcı tanımlayıcısı** açılır.</span><span class="sxs-lookup"><span data-stu-id="4d454-183">Under hello **User attributes** section, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span> <span data-ttu-id="4d454-184">Merhaba seçeneği hello uygulama tooauthenticate hello kullanıcı toomatch hello beklenen değer gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="4d454-184">hello selected option needs toomatch hello expected value in hello application tooauthenticate hello user.</span></span>

   >[!NOTE] 
   ><span data-ttu-id="4d454-185">Merhaba NameID özniteliği (kullanıcı tanımlayıcısı) için Azure AD select hello biçimi seçili hello değere göre veya hello SAML AuthRequest hello uygulama tarafından istenen biçim hello.</span><span class="sxs-lookup"><span data-stu-id="4d454-185">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="4d454-186">Daha fazla bilgi için hello makalesine bakın [tek oturum açma SAML Protokolü](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) NameIDPolicy altında hello bölüm.</span><span class="sxs-lookup"><span data-stu-id="4d454-186">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>
   >
   >

9.  <span data-ttu-id="4d454-187">tooadd kullanıcı öznitelikleri, tıklatın **Görünüm ve diğer tüm kullanıcı özniteliklerini düzenleme** tooedit Merhaba, kullanıcı oturum açtığında gönderilen toobe toohello hello SAML belirteci uygulamada öznitelikleri.</span><span class="sxs-lookup"><span data-stu-id="4d454-187">tooadd user attributes, click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="4d454-188">bir öznitelik tooadd:</span><span class="sxs-lookup"><span data-stu-id="4d454-188">tooadd an attribute:</span></span>

   1. <span data-ttu-id="4d454-189">tıklatın **Ekle özniteliği**.</span><span class="sxs-lookup"><span data-stu-id="4d454-189">click **Add attribute**.</span></span> <span data-ttu-id="4d454-190">Merhaba girin **adı** ve hello select hello **değeri** gelen hello açılır.</span><span class="sxs-lookup"><span data-stu-id="4d454-190">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="4d454-191">Tıklatın **kaydedin.**</span><span class="sxs-lookup"><span data-stu-id="4d454-191">click **Save.**</span></span> <span data-ttu-id="4d454-192">Yeni bir öznitelik hello hello tablosundaki görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="4d454-192">You will see hello new attribute in hello table.</span></span>

#### <a name="download-hello-azure-ad-metadata-or-certificate"></a><span data-ttu-id="4d454-193">Hello Azure AD meta verileri veya sertifika yükleme</span><span class="sxs-lookup"><span data-stu-id="4d454-193">Download hello Azure AD metadata or certificate</span></span>

<span data-ttu-id="4d454-194">toodownload hello uygulama meta verileri veya sertifika Azure AD'den hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="4d454-194">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="4d454-195">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="4d454-195">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="4d454-196">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="4d454-196">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4d454-197">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="4d454-197">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4d454-198">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="4d454-198">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4d454-199">Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.</span><span class="sxs-lookup"><span data-stu-id="4d454-199">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="4d454-200">Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**</span><span class="sxs-lookup"><span data-stu-id="4d454-200">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="4d454-201">Çoklu oturum açma yapılandırdığınız hello uygulaması'nı seçin.</span><span class="sxs-lookup"><span data-stu-id="4d454-201">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="4d454-202">Merhaba uygulamanın yüklediği sonra hello tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="4d454-202">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="4d454-203">Çok Git**SAML imzalama sertifikası** bölümünde ve ardından **karşıdan** sütun değeri.</span><span class="sxs-lookup"><span data-stu-id="4d454-203">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="4d454-204">Çoklu oturum açma yapılandırma hangi hello uygulama gerektirir bağlı olarak, meta veri XML hello veya sertifika hello ya da hello seçeneği toodownload bakın.</span><span class="sxs-lookup"><span data-stu-id="4d454-204">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

    <span data-ttu-id="4d454-205">Azure AD, URL tooget hello meta verilerinin sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="4d454-205">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="4d454-206">Merhaba meta veriler yalnızca bir XML dosyası olarak alınabilir.</span><span class="sxs-lookup"><span data-stu-id="4d454-206">hello metadata can only be retrieved as a XML file.</span></span>

### <a name="how-tooconfigure-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="4d454-207">Nasıl bir galeri olmayan uygulama için çoklu oturum açmayı tooconfigure Federasyon</span><span class="sxs-lookup"><span data-stu-id="4d454-207">How tooconfigure federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="4d454-208">Galeri olmayan uygulama tooconfigure toohave Azure AD premium gerekir ve Merhaba uygulaması SAML 2.0 destekler.</span><span class="sxs-lookup"><span data-stu-id="4d454-208">tooconfigure a non-gallery application, you need toohave Azure AD premium and hello application supports SAML 2.0.</span></span> <span data-ttu-id="4d454-209">Azure AD sürümleri hakkında daha fazla bilgi için ziyaret [Azure AD fiyatlandırma](https://azure.microsoft.com/pricing/details/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="4d454-209">For more information about Azure AD versions, visit [Azure AD pricing](https://azure.microsoft.com/pricing/details/active-directory/).</span></span>

-   [<span data-ttu-id="4d454-210">Azure AD (oturum açma URL'si, tanımlayıcı, yanıt URL'si) Hello uygulamanın meta veri değerlerini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="4d454-210">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configuring-single-sign-on)

-   [<span data-ttu-id="4d454-211">Kullanıcı tanımlayıcısı seçin ve kullanıcı öznitelikleri gönderilen toobe toohello uygulaması ekleyin</span><span class="sxs-lookup"><span data-stu-id="4d454-211">Select User Identifier and add user attributes toobe sent toohello application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="4d454-212">Azure AD meta verileri ve sertifika alma</span><span class="sxs-lookup"><span data-stu-id="4d454-212">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="4d454-213">Merhaba uygulaması (oturum açma URL'si, veren, oturum kapatma URL'si ve sertifika) Azure AD meta veri değerlerini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="4d454-213">Configure Azure AD metadata values in hello application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configuring-single-sign-on)

#### <a name="configure-hello-applications-metadata-values-in-azure-ad-sign-on-url-identifier-reply-url"></a><span data-ttu-id="4d454-214">Azure AD (oturum açma URL'si, tanımlayıcı, yanıt URL'si) Hello uygulamanın meta veri değerlerini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="4d454-214">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>

<span data-ttu-id="4d454-215">tooconfigure çoklu oturum açma hello Azure AD Galerisi'nde olmayan bir uygulama için başlangıç adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="4d454-215">tooconfigure single sign-on for an application that is not in hello Azure AD gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="4d454-216">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="4d454-216">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="4d454-217">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="4d454-217">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4d454-218">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="4d454-218">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4d454-219">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="4d454-219">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4d454-220">Merhaba tıklatın **Ekle** hello sağ üst köşesindeki hello düğmesi **kurumsal uygulamalar** dikey.</span><span class="sxs-lookup"><span data-stu-id="4d454-220">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="4d454-221">tıklatın **olmayan galeri uygulama** hello içinde **kendi uygulama Ekle** bölümü.</span><span class="sxs-lookup"><span data-stu-id="4d454-221">click **Non-gallery application** in hello **Add your own app** section.</span></span>

7.  <span data-ttu-id="4d454-222">Merhaba Merhaba uygulaması hello adını **adı** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="4d454-222">Enter hello name of hello application in hello **Name** textbox.</span></span>

8.  <span data-ttu-id="4d454-223">Tıklatın **Ekle** button, tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="4d454-223">Click **Add** button, tooadd hello application.</span></span>

9.  <span data-ttu-id="4d454-224">Merhaba uygulamanın yüklediği sonra hello tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="4d454-224">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

10. <span data-ttu-id="4d454-225">Seçin **SAML tabanlı oturum açma** hello içinde **modu** açılır.</span><span class="sxs-lookup"><span data-stu-id="4d454-225">Select **SAML-based Sign-on** in hello **Mode** dropdown.</span></span>

11. <span data-ttu-id="4d454-226">Merhaba gerekli değerleri girin **etki alanı ve URL'ler.**</span><span class="sxs-lookup"><span data-stu-id="4d454-226">Enter hello required values in **Domain and URLs.**</span></span> <span data-ttu-id="4d454-227">Bu değerleri hello uygulama satıcısından almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="4d454-227">You should get these values from hello application vendor.</span></span>

   1. <span data-ttu-id="4d454-228">IDP tarafından başlatılan SSO'yu olarak tooconfigure hello uygulama hello yanıt URL'si ve hello tanımlayıcısı girin.</span><span class="sxs-lookup"><span data-stu-id="4d454-228">tooconfigure hello application as IdP-initiated SSO, enter hello Reply URL and hello Identifier.</span></span>

   2.  <span data-ttu-id="4d454-229">**İsteğe bağlı:** tooconfigure hello uygulama SP tarafından başlatılan SSO'yu olarak hello oturum URL'yi, gerekli bir değerdir.</span><span class="sxs-lookup"><span data-stu-id="4d454-229">**Optional:** tooconfigure hello application as SP-initiated SSO, hello Sign on URL it’s a required value.</span></span>

12. <span data-ttu-id="4d454-230">Merhaba, **kullanıcı öznitelikleri**, select hello hello kullanıcılarınız için benzersiz tanımlayıcı **kullanıcı tanımlayıcısı** açılır.</span><span class="sxs-lookup"><span data-stu-id="4d454-230">In hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

13. <span data-ttu-id="4d454-231">**İsteğe bağlı:** tıklatın **Görünüm ve diğer tüm kullanıcı özniteliklerini düzenleme** tooedit Merhaba, kullanıcı oturum açtığında gönderilen toobe toohello hello SAML belirteci uygulamada öznitelikleri.</span><span class="sxs-lookup"><span data-stu-id="4d454-231">**Optional:** click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="4d454-232">bir öznitelik tooadd:</span><span class="sxs-lookup"><span data-stu-id="4d454-232">tooadd an attribute:</span></span>

   1. <span data-ttu-id="4d454-233">tıklatın **Ekle özniteliği**.</span><span class="sxs-lookup"><span data-stu-id="4d454-233">click **Add attribute**.</span></span> <span data-ttu-id="4d454-234">Merhaba girin **adı** ve hello select hello **değeri** gelen hello açılır.</span><span class="sxs-lookup"><span data-stu-id="4d454-234">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="4d454-235">Tıklatın **kaydedin.**</span><span class="sxs-lookup"><span data-stu-id="4d454-235">Click **Save.**</span></span> <span data-ttu-id="4d454-236">Yeni bir öznitelik hello hello tablosundaki bakın.</span><span class="sxs-lookup"><span data-stu-id="4d454-236">You see hello new attribute in hello table.</span></span>

14. <span data-ttu-id="4d454-237">tıklatın **yapılandırma &lt;uygulama adı&gt;**  tooaccess belgelerine nasıl tooconfigure çoklu oturum açma hello uygulamada.</span><span class="sxs-lookup"><span data-stu-id="4d454-237">click **Configure &lt;application name&gt;** tooaccess documentation on how tooconfigure single sign-on in hello application.</span></span> <span data-ttu-id="4d454-238">Ayrıca, Azure AD URL'leri ve hello uygulama için gerekli sertifika sahiptir.</span><span class="sxs-lookup"><span data-stu-id="4d454-238">Also, you has Azure AD URLs and certificate required for hello application.</span></span>

#### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a><span data-ttu-id="4d454-239">Kullanıcı tanımlayıcısı seçin ve kullanıcı öznitelikleri gönderilen toobe toohello uygulaması ekleyin</span><span class="sxs-lookup"><span data-stu-id="4d454-239">Select User Identifier and add user attributes toobe sent toohello application</span></span>

<span data-ttu-id="4d454-240">tooselect kullanıcı tanımlayıcısı Merhaba veya kullanıcı öznitelikleri ekleme, hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="4d454-240">tooselect hello User Identifier or add user attributes, follow hello steps below:</span></span>

1.  <span data-ttu-id="4d454-241">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="4d454-241">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="4d454-242">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="4d454-242">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4d454-243">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="4d454-243">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4d454-244">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="4d454-244">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4d454-245">Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.</span><span class="sxs-lookup"><span data-stu-id="4d454-245">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="4d454-246">Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**</span><span class="sxs-lookup"><span data-stu-id="4d454-246">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="4d454-247">Çoklu oturum açma yapılandırdığınız hello uygulaması'nı seçin.</span><span class="sxs-lookup"><span data-stu-id="4d454-247">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="4d454-248">Merhaba uygulamanın yüklediği sonra hello tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="4d454-248">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="4d454-249">Merhaba altında **kullanıcı öznitelikleri** bölümünde, select hello hello kullanıcılarınız için benzersiz tanımlayıcı **kullanıcı tanımlayıcısı** açılır.</span><span class="sxs-lookup"><span data-stu-id="4d454-249">Under hello **User attributes** section, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span> <span data-ttu-id="4d454-250">Merhaba seçeneği hello uygulama tooauthenticate hello kullanıcı toomatch hello beklenen değer gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="4d454-250">hello selected option needs toomatch hello expected value in hello application tooauthenticate hello user.</span></span>

   >[!NOTE] 
   ><span data-ttu-id="4d454-251">Merhaba NameID özniteliği (kullanıcı tanımlayıcısı) için Azure AD select hello biçimi seçili hello değere göre veya hello SAML AuthRequest hello uygulama tarafından istenen biçim hello.</span><span class="sxs-lookup"><span data-stu-id="4d454-251">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="4d454-252">Daha fazla bilgi için hello makalesine bakın [tek oturum açma SAML Protokolü](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) NameIDPolicy altında hello bölüm.</span><span class="sxs-lookup"><span data-stu-id="4d454-252">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>
   >
   >

9.  <span data-ttu-id="4d454-253">tooadd kullanıcı öznitelikleri, tıklatın **Görünüm ve diğer tüm kullanıcı özniteliklerini düzenleme** tooedit Merhaba, kullanıcı oturum açtığında gönderilen toobe toohello hello SAML belirteci uygulamada öznitelikleri.</span><span class="sxs-lookup"><span data-stu-id="4d454-253">tooadd user attributes, click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="4d454-254">bir öznitelik tooadd:</span><span class="sxs-lookup"><span data-stu-id="4d454-254">tooadd an attribute:</span></span>

   1. <span data-ttu-id="4d454-255">tıklatın **Ekle özniteliği**.</span><span class="sxs-lookup"><span data-stu-id="4d454-255">click **Add attribute**.</span></span> <span data-ttu-id="4d454-256">Merhaba girin **adı** ve hello select hello **değeri** gelen hello açılır.</span><span class="sxs-lookup"><span data-stu-id="4d454-256">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="4d454-257">Tıklatın **kaydedin.**</span><span class="sxs-lookup"><span data-stu-id="4d454-257">Click **Save.**</span></span> <span data-ttu-id="4d454-258">Yeni bir öznitelik hello hello tablosundaki bakın.</span><span class="sxs-lookup"><span data-stu-id="4d454-258">You see hello new attribute in hello table.</span></span>

#### <a name="download-hello-azure-ad-metadata-or-certificate"></a><span data-ttu-id="4d454-259">Hello Azure AD meta verileri veya sertifika yükleme</span><span class="sxs-lookup"><span data-stu-id="4d454-259">Download hello Azure AD metadata or certificate</span></span>

<span data-ttu-id="4d454-260">toodownload hello uygulama meta verileri veya sertifika Azure AD'den hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="4d454-260">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="4d454-261">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="4d454-261">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="4d454-262">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="4d454-262">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4d454-263">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="4d454-263">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4d454-264">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="4d454-264">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4d454-265">Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.</span><span class="sxs-lookup"><span data-stu-id="4d454-265">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="4d454-266">Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**</span><span class="sxs-lookup"><span data-stu-id="4d454-266">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="4d454-267">Çoklu oturum açma yapılandırdığınız hello uygulaması'nı seçin.</span><span class="sxs-lookup"><span data-stu-id="4d454-267">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="4d454-268">Merhaba uygulamanın yüklediği sonra hello tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="4d454-268">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="4d454-269">Çok Git**SAML imzalama sertifikası** bölümünde ve ardından **karşıdan** sütun değeri.</span><span class="sxs-lookup"><span data-stu-id="4d454-269">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="4d454-270">Çoklu oturum açma yapılandırma hangi hello uygulama gerektirir bağlı olarak, meta veri XML hello veya sertifika hello ya da hello seçeneği toodownload bakın.</span><span class="sxs-lookup"><span data-stu-id="4d454-270">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

<span data-ttu-id="4d454-271">Azure AD, URL tooget hello meta verilerinin sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="4d454-271">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="4d454-272">Merhaba meta veriler yalnızca bir XML dosyası olarak alınabilir.</span><span class="sxs-lookup"><span data-stu-id="4d454-272">hello metadata can only be retrieved as a XML file.</span></span>

### <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="4d454-273">Tooconfigure parola nasıl çoklu oturum açma için Azure AD galeri uygulaması</span><span class="sxs-lookup"><span data-stu-id="4d454-273">How tooconfigure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="4d454-274">tooconfigure hello Azure AD Galeriden bir uygulama şunları yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="4d454-274">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="4d454-275">Hello Azure AD Galeriden bir uygulama ekleme</span><span class="sxs-lookup"><span data-stu-id="4d454-275">Add an application from hello Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="4d454-276">Merhaba uygulaması parola çoklu oturum açma için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="4d454-276">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

#### <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="4d454-277">Hello Azure AD Galeriden bir uygulama ekleme</span><span class="sxs-lookup"><span data-stu-id="4d454-277">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="4d454-278">tooadd hello Azure AD galeri, bir uygulamadan hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="4d454-278">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="4d454-279">Açık hello [Azure Portal](https://portal.azure.com) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="4d454-279">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="4d454-280">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="4d454-280">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4d454-281">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="4d454-281">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4d454-282">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="4d454-282">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4d454-283">Merhaba tıklatın **Ekle** hello sağ üst köşesindeki hello düğmesi **kurumsal uygulamalar** dikey.</span><span class="sxs-lookup"><span data-stu-id="4d454-283">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="4d454-284">Merhaba, **bir ad girin** hello metin **hello galerisinden Ekle** bölümü, hello uygulamasının türü hello adı.</span><span class="sxs-lookup"><span data-stu-id="4d454-284">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application.</span></span>

7.  <span data-ttu-id="4d454-285">Çoklu oturum açma için tooconfigure istediğiniz hello uygulaması'nı seçin.</span><span class="sxs-lookup"><span data-stu-id="4d454-285">Select hello application you want tooconfigure for single sign-on.</span></span>

8.  <span data-ttu-id="4d454-286">Merhaba uygulaması eklemeden önce hello adını değiştirebilirsiniz **adı** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="4d454-286">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="4d454-287">Tıklatın **Ekle** button, tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="4d454-287">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="4d454-288">Kısa bir süre sonra mümkün toosee hello uygulamanın yapılandırma dikey olabilir.</span><span class="sxs-lookup"><span data-stu-id="4d454-288">After a short period, you be able toosee hello application’s configuration blade.</span></span>

#### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="4d454-289">Merhaba uygulaması parola çoklu oturum açma için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="4d454-289">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="4d454-290">tooconfigure çoklu oturum açma bir uygulama için başlangıç adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="4d454-290">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="4d454-291">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="4d454-291">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="4d454-292">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="4d454-292">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4d454-293">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="4d454-293">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4d454-294">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="4d454-294">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4d454-295">Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.</span><span class="sxs-lookup"><span data-stu-id="4d454-295">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="4d454-296">Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**</span><span class="sxs-lookup"><span data-stu-id="4d454-296">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="4d454-297">Tooconfigure çoklu oturum açma hello uygulamasını seçin.</span><span class="sxs-lookup"><span data-stu-id="4d454-297">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="4d454-298">Merhaba uygulamanın yüklediği sonra hello tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="4d454-298">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="4d454-299">Select hello modu **parola tabanlı oturum açma.**</span><span class="sxs-lookup"><span data-stu-id="4d454-299">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="4d454-300">[Kullanıcıların toohello uygulama atama](#how-to-assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="4d454-300">[Assign users toohello application](#how-to-assign-a-user-to-an-application-directly).</span></span>

10. <span data-ttu-id="4d454-301">Ayrıca, ayrıca hello kullanıcı adına kimlik bilgilerini hello satırları hello kullanıcıların seçerek ve tıklayarak sağlayabilirsiniz **güncelleştirme kimlik bilgileri** ve hello kullanıcılar adına hello kullanıcı adı ve parola girme.</span><span class="sxs-lookup"><span data-stu-id="4d454-301">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="4d454-302">Aksi takdirde, kullanıcılar istendiğinde tooenter hello kimlik bilgilerinin kendilerini başlatma bağlı olması.</span><span class="sxs-lookup"><span data-stu-id="4d454-302">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

### <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="4d454-303">Tooconfigure parola nasıl tek bir galeri olmayan uygulaması için oturum açma</span><span class="sxs-lookup"><span data-stu-id="4d454-303">How tooconfigure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="4d454-304">tooconfigure hello Azure AD Galeriden bir uygulama şunları yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="4d454-304">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="4d454-305">Bir galeri olmayan uygulama ekleme</span><span class="sxs-lookup"><span data-stu-id="4d454-305">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="4d454-306">Merhaba uygulaması parola çoklu oturum açma için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="4d454-306">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

#### <a name="add-a-non-gallery-application"></a><span data-ttu-id="4d454-307">Bir galeri olmayan uygulama ekleme</span><span class="sxs-lookup"><span data-stu-id="4d454-307">Add a non-gallery application</span></span>

<span data-ttu-id="4d454-308">tooadd hello Azure AD galeri, bir uygulamadan hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="4d454-308">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="4d454-309">Açık hello [Azure Portal](https://portal.azure.com) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**.</span><span class="sxs-lookup"><span data-stu-id="4d454-309">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="4d454-310">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="4d454-310">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4d454-311">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="4d454-311">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4d454-312">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="4d454-312">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4d454-313">Merhaba tıklatın **Ekle** hello sağ üst köşesindeki hello düğmesi **kurumsal uygulamalar** dikey.</span><span class="sxs-lookup"><span data-stu-id="4d454-313">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="4d454-314">tıklatın **olmayan galeri uygulaması.**</span><span class="sxs-lookup"><span data-stu-id="4d454-314">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="4d454-315">Merhaba, uygulamanızın hello adını **adı** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="4d454-315">Enter hello name of your application in hello **Name** textbox.</span></span> <span data-ttu-id="4d454-316">Seçin **ekleyin.**</span><span class="sxs-lookup"><span data-stu-id="4d454-316">Select **Add.**</span></span>

<span data-ttu-id="4d454-317">Kısa bir süre sonra mümkün toosee hello uygulamanın yapılandırma dikey olabilir.</span><span class="sxs-lookup"><span data-stu-id="4d454-317">After a short period, you be able toosee hello application’s configuration blade.</span></span>

#### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="4d454-318">Merhaba uygulaması parola çoklu oturum açma için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="4d454-318">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="4d454-319">tooconfigure çoklu oturum açma bir uygulama için başlangıç adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="4d454-319">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="4d454-320">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="4d454-320">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="4d454-321">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="4d454-321">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4d454-322">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="4d454-322">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4d454-323">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="4d454-323">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4d454-324">Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.</span><span class="sxs-lookup"><span data-stu-id="4d454-324">click **All Applications** tooview a list of all your applications.</span></span>

    1.  <span data-ttu-id="4d454-325">Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**</span><span class="sxs-lookup"><span data-stu-id="4d454-325">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="4d454-326">Tooconfigure çoklu oturum açma hello uygulamasını seçin.</span><span class="sxs-lookup"><span data-stu-id="4d454-326">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="4d454-327">Merhaba uygulamanın yüklediği sonra hello tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="4d454-327">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="4d454-328">Select hello modu **parola tabanlı oturum açma.**</span><span class="sxs-lookup"><span data-stu-id="4d454-328">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="4d454-329">Merhaba girin **oturum açma URL'si**.</span><span class="sxs-lookup"><span data-stu-id="4d454-329">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="4d454-330">Bu kullanıcılar kendi kullanıcı adı ve parola toosign içinde için girdiğiniz yere hello URL'dir.</span><span class="sxs-lookup"><span data-stu-id="4d454-330">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="4d454-331">Merhaba oturum alanları hello URL'de göründüğünden emin olun.</span><span class="sxs-lookup"><span data-stu-id="4d454-331">Ensure hello sign in fields are visible at hello URL.</span></span>

10. <span data-ttu-id="4d454-332">[Kullanıcıların toohello uygulama atama](#how-to-assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="4d454-332">[Assign users toohello application](#how-to-assign-a-user-to-an-application-directly).</span></span>

11. <span data-ttu-id="4d454-333">Ayrıca, ayrıca hello kullanıcı adına kimlik bilgilerini hello satırları hello kullanıcıların seçerek ve tıklayarak sağlayabilirsiniz **güncelleştirme kimlik bilgileri** ve hello kullanıcılar adına hello kullanıcı adı ve parola girme.</span><span class="sxs-lookup"><span data-stu-id="4d454-333">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="4d454-334">Aksi takdirde, kullanıcılar istendiğinde tooenter hello kimlik bilgilerinin kendilerini başlatma bağlı olması.</span><span class="sxs-lookup"><span data-stu-id="4d454-334">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="problems-related-tooassigning-applications-toousers"></a><span data-ttu-id="4d454-335">Sorunları ilgili tooassigning uygulamaları toousers</span><span class="sxs-lookup"><span data-stu-id="4d454-335">Problems related tooassigning applications toousers</span></span>

<span data-ttu-id="4d454-336">Toohello uygulama atanmadıkları bir kullanıcı bir uygulama kullanıcıların erişim panelinde görüyor olabilirsiniz değil.</span><span class="sxs-lookup"><span data-stu-id="4d454-336">A user may not be seeing an application on their Access Panel because they are not assigned toohello application.</span></span> <span data-ttu-id="4d454-337">Bazı yolları toocheck aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="4d454-337">Below are some ways toocheck:</span></span>

-   [<span data-ttu-id="4d454-338">Bir kullanıcı toohello uygulama atandığından emin olun</span><span class="sxs-lookup"><span data-stu-id="4d454-338">Check if a user is assigned toohello application</span></span>](#check-if-a-user-is-assigned-to-the-application)

-   [<span data-ttu-id="4d454-339">Nasıl tooassign bir kullanıcı tooan uygulaması doğrudan</span><span class="sxs-lookup"><span data-stu-id="4d454-339">How tooassign a user tooan application directly</span></span>](#how-to-assign-a-user-to-an-application-directly)

-   [<span data-ttu-id="4d454-340">Bir kullanıcı tooa lisans atanmışsa onay toohello uygulama ilgili</span><span class="sxs-lookup"><span data-stu-id="4d454-340">Check if a user is assigned tooa license related toohello application</span></span>](#check-if-a-user-is-under-a-license-related-to-the-application)

-   [<span data-ttu-id="4d454-341">Nasıl tooassign lisans tooa kullanıcı</span><span class="sxs-lookup"><span data-stu-id="4d454-341">How tooassign a license tooa user</span></span>](#how-to-assign-a-user-a-license)

### <a name="check-if-a-user-is-assigned-toohello-application"></a><span data-ttu-id="4d454-342">Bir kullanıcı toohello uygulama atandığından emin olun</span><span class="sxs-lookup"><span data-stu-id="4d454-342">Check if a user is assigned toohello application</span></span>

<span data-ttu-id="4d454-343">toocheck toohello uygulama atanmış bir kullanıcı yoksa, hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="4d454-343">toocheck if a user is assigned toohello application, follow hello steps below:</span></span>

1.  <span data-ttu-id="4d454-344">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="4d454-344">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="4d454-345">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="4d454-345">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4d454-346">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="4d454-346">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4d454-347">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="4d454-347">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4d454-348">Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.</span><span class="sxs-lookup"><span data-stu-id="4d454-348">click **All Applications** tooview a list of all your applications.</span></span>

6.  <span data-ttu-id="4d454-349">**Arama** için söz konusu hello uygulamasının hello adı.</span><span class="sxs-lookup"><span data-stu-id="4d454-349">**Search** for hello name of hello application in question.</span></span>

7.  <span data-ttu-id="4d454-350">tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="4d454-350">click **Users and groups**.</span></span>

8.  <span data-ttu-id="4d454-351">Kullanıcı toohello uygulama atanmışsa toosee denetleyin.</span><span class="sxs-lookup"><span data-stu-id="4d454-351">Check toosee if your user is assigned toohello application.</span></span>

   * <span data-ttu-id="4d454-352">Aksi halde hello adımları "nasıl tooassign bir kullanıcı tooan uygulaması doğrudan" toodo şekilde.</span><span class="sxs-lookup"><span data-stu-id="4d454-352">If not follow hello steps in “How tooassign a user tooan application directly” toodo so.</span></span>

### <a name="how-tooassign-a-user-tooan-application-directly"></a><span data-ttu-id="4d454-353">Nasıl tooassign bir kullanıcı tooan uygulaması doğrudan</span><span class="sxs-lookup"><span data-stu-id="4d454-353">How tooassign a user tooan application directly</span></span>

<span data-ttu-id="4d454-354">tooassign bir veya daha fazla kullanıcı tooan uygulama, doğrudan başlangıç adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="4d454-354">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="4d454-355">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici**.</span><span class="sxs-lookup"><span data-stu-id="4d454-355">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator**.</span></span>

2.  <span data-ttu-id="4d454-356">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="4d454-356">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4d454-357">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="4d454-357">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4d454-358">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="4d454-358">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4d454-359">Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.</span><span class="sxs-lookup"><span data-stu-id="4d454-359">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="4d454-360">Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**</span><span class="sxs-lookup"><span data-stu-id="4d454-360">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="4d454-361">Tooassign kullanıcı toofrom hello listesini hello uygulamasını seçin.</span><span class="sxs-lookup"><span data-stu-id="4d454-361">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="4d454-362">Merhaba uygulamanın yüklediği sonra tıklayın **kullanıcılar ve gruplar** hello uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="4d454-362">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="4d454-363">Hello tıklatın **Ekle** hello üstünde düğmesi **kullanıcılar ve gruplar** listesi tooopen hello **eklemek atama** dikey.</span><span class="sxs-lookup"><span data-stu-id="4d454-363">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="4d454-364">Merhaba tıklatın **kullanıcılar ve gruplar** hello seçicisini **eklemek atama** dikey.</span><span class="sxs-lookup"><span data-stu-id="4d454-364">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="4d454-365">Merhaba türü **tam adı** veya **e-posta adresi** hello atama ilgilenen hello kullanıcının **ad veya e-posta adresine göre arama** arama kutusu.</span><span class="sxs-lookup"><span data-stu-id="4d454-365">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="4d454-366">Merhaba getirin **kullanıcı** hello listesi tooreveal içinde bir **onay kutusunu**.</span><span class="sxs-lookup"><span data-stu-id="4d454-366">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="4d454-367">Kullanıcı toohello Hello onay kutusu sonraki toohello kullanıcının profili fotoğraf veya logosu tooadd tıklatın **seçili** listesi.</span><span class="sxs-lookup"><span data-stu-id="4d454-367">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="4d454-368">**İsteğe bağlı:** çok isterseniz**birden fazla kullanıcı ekleme**, başka bir tür **tam adı** veya **e-posta adresi** hello içine **ada göre ara veya e-posta adresi** arama kutusu ve bu kullanıcı toohello hello onay kutusunu tooadd tıklatın **seçili** listesi.</span><span class="sxs-lookup"><span data-stu-id="4d454-368">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="4d454-369">Kullanıcıların seçerek bittiğinde hello tıklatın **seçin** düğmesini tooadd bunları kullanıcılar ve gruplar toobe toohello listesi atanan toohello uygulama.</span><span class="sxs-lookup"><span data-stu-id="4d454-369">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="4d454-370">**İsteğe bağlı:** hello tıklatın **rolü Seç** hello seçicide **eklemek atama** dikey tooselect rol seçtiğiniz tooassign toohello kullanıcılar.</span><span class="sxs-lookup"><span data-stu-id="4d454-370">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="4d454-371">Merhaba tıklatın **atamak** düğmesini tooassign hello uygulama toohello seçilen kullanıcılar.</span><span class="sxs-lookup"><span data-stu-id="4d454-371">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="4d454-372">Seçtiğiniz hello kullanıcılar kısa bir süre mümkün toolaunch bu uygulamalarında değiştirdikten sonra erişim Paneli'ne hello.</span><span class="sxs-lookup"><span data-stu-id="4d454-372">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

### <a name="check-if-a-user-is-under-a-license-related-toohello-application"></a><span data-ttu-id="4d454-373">Bir kullanıcının bir lisansı altında olup olmadığını denetleyin ilgili toohello uygulama</span><span class="sxs-lookup"><span data-stu-id="4d454-373">Check if a user is under a license related toohello application</span></span>

<span data-ttu-id="4d454-374">toocheck bir kullanıcıya ait atanmış lisansların, aşağıdaki hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="4d454-374">toocheck a user’s assigned licenses, follow hello steps below:</span></span>

1.  <span data-ttu-id="4d454-375">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="4d454-375">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="4d454-376">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="4d454-376">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4d454-377">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="4d454-377">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4d454-378">Tıklatın **kullanıcılar ve gruplar** hello Gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="4d454-378">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="4d454-379">tıklatın **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="4d454-379">click **All users**.</span></span>

6.  <span data-ttu-id="4d454-380">**Arama** ilgilendiğiniz hello kullanıcı için ve **hello satıra tıklayın** tooselect.</span><span class="sxs-lookup"><span data-stu-id="4d454-380">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="4d454-381">tıklatın **lisansları** toosee lisansları hello kullanıcı şu anda atanmış.</span><span class="sxs-lookup"><span data-stu-id="4d454-381">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

  * <span data-ttu-id="4d454-382">Merhaba kullanıcı atanan tooan Office lisansı ise bu etkinleştirin birinci taraf Office uygulamaları tooappear hello kullanıcının erişim panelinde.</span><span class="sxs-lookup"><span data-stu-id="4d454-382">If hello user is assigned tooan Office license this enable First Party Office applications tooappear on hello user’s Access Panel.</span></span>

### <a name="how-tooassign-a-user-a-license"></a><span data-ttu-id="4d454-383">Nasıl tooassign bir kullanıcı bir lisans</span><span class="sxs-lookup"><span data-stu-id="4d454-383">How tooassign a user a license</span></span> 

<span data-ttu-id="4d454-384">tooassign lisans tooa kullanıcı hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="4d454-384">tooassign a license tooa user, follow hello steps below:</span></span>

1.  <span data-ttu-id="4d454-385">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="4d454-385">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="4d454-386">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="4d454-386">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4d454-387">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="4d454-387">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4d454-388">Tıklatın **kullanıcılar ve gruplar** hello Gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="4d454-388">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="4d454-389">tıklatın **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="4d454-389">click **All users**.</span></span>

6.  <span data-ttu-id="4d454-390">**Arama** ilgilendiğiniz hello kullanıcı için ve **hello satıra tıklayın** tooselect.</span><span class="sxs-lookup"><span data-stu-id="4d454-390">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="4d454-391">tıklatın **lisansları** toosee lisansları hello kullanıcı şu anda atanmış.</span><span class="sxs-lookup"><span data-stu-id="4d454-391">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

8.  <span data-ttu-id="4d454-392">Merhaba tıklatın **atamak** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4d454-392">click hello **Assign** button.</span></span>

9.  <span data-ttu-id="4d454-393">Seçin **bir veya daha fazla ürün** mevcut ürünler hello listesinden.</span><span class="sxs-lookup"><span data-stu-id="4d454-393">Select **one or more products** from hello list of available products.</span></span>

10. <span data-ttu-id="4d454-394">**İsteğe bağlı** hello tıklatın **atama seçenekleri** öğesi toogranularly ürünleri atayın.</span><span class="sxs-lookup"><span data-stu-id="4d454-394">**Optional** click hello **assignment options** item toogranularly assign products.</span></span> <span data-ttu-id="4d454-395">Tıklatın **Tamam** ne zaman bu tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="4d454-395">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="4d454-396">Merhaba tıklatın **atamak** tooassign bu lisansları toothis kullanıcı düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4d454-396">Click hello **Assign** button tooassign these licenses toothis user.</span></span>

## <a name="problems-related-tooassigning-applications-toogroups"></a><span data-ttu-id="4d454-397">Sorunları ilgili tooassigning uygulamaları toogroups</span><span class="sxs-lookup"><span data-stu-id="4d454-397">Problems related tooassigning applications toogroups</span></span>

<span data-ttu-id="4d454-398">Merhaba uygulaması atanmış bir grubun parçası olmadığından bir kullanıcı bir uygulama kullanıcıların erişim panelinde görüyor olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4d454-398">A user may be seeing an application on their Access Panel because they are part of a group that has been assigned hello application.</span></span> <span data-ttu-id="4d454-399">Bazı yolları toocheck aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="4d454-399">Below are some ways toocheck:</span></span>

-   [<span data-ttu-id="4d454-400">Bir kullanıcı grup üyeliklerini denetleyin</span><span class="sxs-lookup"><span data-stu-id="4d454-400">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="4d454-401">Tooassign bir uygulama tooa Grup nasıl doğrudan</span><span class="sxs-lookup"><span data-stu-id="4d454-401">How tooassign an application tooa group directly</span></span>](#how-to-assign-an-application-to-a-group-directly)

-   [<span data-ttu-id="4d454-402">Bir kullanıcı grubu tooa lisans atanmış bir parçası olup olmadığını denetleyin</span><span class="sxs-lookup"><span data-stu-id="4d454-402">Check if a user is part of group assigned tooa license</span></span>](#check-if-a-user-is-part-of-group-assigned-to-a-license)

-   [<span data-ttu-id="4d454-403">Nasıl tooassign lisans tooa grubu</span><span class="sxs-lookup"><span data-stu-id="4d454-403">How tooassign a license tooa group</span></span>](#how-to-assign-a-license-to-a-group)

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="4d454-404">Bir kullanıcı grup üyeliklerini denetleyin</span><span class="sxs-lookup"><span data-stu-id="4d454-404">Check a user’s group memberships</span></span>

<span data-ttu-id="4d454-405">toocheck bir grubun üyeliğini, aşağıdaki hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="4d454-405">toocheck a group’s membership, follow hello steps below:</span></span>

1.  <span data-ttu-id="4d454-406">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="4d454-406">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="4d454-407">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="4d454-407">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4d454-408">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="4d454-408">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4d454-409">Tıklatın **kullanıcılar ve gruplar** hello Gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="4d454-409">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="4d454-410">tıklatın **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="4d454-410">click **All users**.</span></span>

6.  <span data-ttu-id="4d454-411">**Arama** ilgilendiğiniz hello kullanıcı için ve **hello satıra tıklayın** tooselect.</span><span class="sxs-lookup"><span data-stu-id="4d454-411">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="4d454-412">tıklatın **grupları**.</span><span class="sxs-lookup"><span data-stu-id="4d454-412">click **Groups**.</span></span>

8.  <span data-ttu-id="4d454-413">Kullanıcı grubunun bir parçası ise onay toosee toohello uygulama atanır.</span><span class="sxs-lookup"><span data-stu-id="4d454-413">Check toosee if your user is part of a Group assigned toohello application.</span></span>

  * <span data-ttu-id="4d454-414">Merhaba grubundan tooremove hello kullanıcının istiyorsanız **hello satıra tıklayın** hello grubu ve select silin.</span><span class="sxs-lookup"><span data-stu-id="4d454-414">If you want tooremove hello user from hello group, **click hello row** of hello group and select delete.</span></span>

### <a name="how-tooassign-an-application-tooa-group-directly"></a><span data-ttu-id="4d454-415">Tooassign bir uygulama tooa Grup nasıl doğrudan</span><span class="sxs-lookup"><span data-stu-id="4d454-415">How tooassign an application tooa group directly</span></span>

<span data-ttu-id="4d454-416">bir veya daha fazla tooassign doğrudan tooan uygulama hello adımları aşağıdaki grupları:</span><span class="sxs-lookup"><span data-stu-id="4d454-416">tooassign one or more groups tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="4d454-417">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici**.</span><span class="sxs-lookup"><span data-stu-id="4d454-417">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator**.</span></span>

2.  <span data-ttu-id="4d454-418">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="4d454-418">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4d454-419">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="4d454-419">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4d454-420">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="4d454-420">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4d454-421">Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.</span><span class="sxs-lookup"><span data-stu-id="4d454-421">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="4d454-422">Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**</span><span class="sxs-lookup"><span data-stu-id="4d454-422">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="4d454-423">Tooassign kullanıcı toofrom hello listesini hello uygulamasını seçin.</span><span class="sxs-lookup"><span data-stu-id="4d454-423">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="4d454-424">Merhaba uygulamanın yüklediği sonra tıklayın **kullanıcılar ve gruplar** hello uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="4d454-424">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="4d454-425">Hello tıklatın **Ekle** hello üstünde düğmesi **kullanıcılar ve gruplar** listesi tooopen hello **eklemek atama** dikey.</span><span class="sxs-lookup"><span data-stu-id="4d454-425">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="4d454-426">Merhaba tıklatın **kullanıcılar ve gruplar** hello seçicisini **eklemek atama** dikey.</span><span class="sxs-lookup"><span data-stu-id="4d454-426">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="4d454-427">Merhaba türü **tam grup adı** hello atama ilgilenen hello grubunun **ad veya e-posta adresine göre arama** arama kutusu.</span><span class="sxs-lookup"><span data-stu-id="4d454-427">Type in hello **full group name** of hello group you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="4d454-428">Merhaba getirin **grup** hello listesi tooreveal içinde bir **onay kutusunu**.</span><span class="sxs-lookup"><span data-stu-id="4d454-428">Hover over hello **group** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="4d454-429">Kullanıcı toohello Hello onay kutusu sonraki toohello grubun profili fotoğraf veya logosu tooadd tıklatın **seçili** listesi.</span><span class="sxs-lookup"><span data-stu-id="4d454-429">Click hello checkbox next toohello group’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="4d454-430">**İsteğe bağlı:** çok isterseniz**birden fazla grubu Ekle**, başka bir tür **tam grup adı** hello içine **ad veya e-posta adresine göre arama** arama kutusu tıklatıp hello onay kutusunu tooadd bu Grup toohello **seçili** listesi.</span><span class="sxs-lookup"><span data-stu-id="4d454-430">**Optional:** If you would like too**add more than one group**, type in another **full group name** into hello **Search by name or email address** search box, and click hello checkbox tooadd this group toohello **Selected** list.</span></span>

13. <span data-ttu-id="4d454-431">Grupları seçmek bittiğinde hello tıklatın **seçin** düğmesini tooadd bunları kullanıcılar ve gruplar toobe toohello listesi atanan toohello uygulama.</span><span class="sxs-lookup"><span data-stu-id="4d454-431">When you are finished selecting groups, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="4d454-432">**İsteğe bağlı:** hello tıklatın **rolü Seç** hello seçicide **eklemek atama** dikey tooselect rol tooassign toohello gruplar seçtiniz.</span><span class="sxs-lookup"><span data-stu-id="4d454-432">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello groups you have selected.</span></span>

15. <span data-ttu-id="4d454-433">Merhaba tıklatın **atamak** düğmesini tooassign hello uygulama toohello seçilen grupları.</span><span class="sxs-lookup"><span data-stu-id="4d454-433">Click hello **Assign** button tooassign hello application toohello selected groups.</span></span>

<span data-ttu-id="4d454-434">Seçtiğiniz hello kullanıcılar kısa bir süre mümkün toolaunch bu uygulamalarında değiştirdikten sonra erişim Paneli'ne hello.</span><span class="sxs-lookup"><span data-stu-id="4d454-434">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

### <a name="check-if-a-user-is-part-of-group-assigned-tooa-license"></a><span data-ttu-id="4d454-435">Bir kullanıcı grubu tooa lisans atanmış bir parçası olup olmadığını denetleyin</span><span class="sxs-lookup"><span data-stu-id="4d454-435">Check if a user is part of group assigned tooa license</span></span>

1.  <span data-ttu-id="4d454-436">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="4d454-436">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="4d454-437">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="4d454-437">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4d454-438">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="4d454-438">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4d454-439">Tıklatın **kullanıcılar ve gruplar** hello Gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="4d454-439">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="4d454-440">tıklatın **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="4d454-440">click **All users**.</span></span>

6.  <span data-ttu-id="4d454-441">**Arama** ilgilendiğiniz hello kullanıcı için ve **hello satıra tıklayın** tooselect.</span><span class="sxs-lookup"><span data-stu-id="4d454-441">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="4d454-442">tıklatın **grupları**.</span><span class="sxs-lookup"><span data-stu-id="4d454-442">click **Groups**.</span></span>

8.  <span data-ttu-id="4d454-443">belirli bir grup Hello satırının'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="4d454-443">click hello row of a specific group.</span></span>

9.  <span data-ttu-id="4d454-444">tıklatın **lisansları** toosee hangi lisansları hello Grup tooit atanan.</span><span class="sxs-lookup"><span data-stu-id="4d454-444">click **Licenses** toosee which licenses hello group has assigned tooit.</span></span>

   * <span data-ttu-id="4d454-445">Merhaba grubu atanan tooan Office lisansı ise bu belirli birinci taraf Office uygulamaları tooappear hello kullanıcının erişim panelinde sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="4d454-445">If hello group is assigned tooan Office license this may enable certain First Party Office applications tooappear on hello user’s Access Panel.</span></span>

### <a name="how-tooassign-a-license-tooa-group"></a><span data-ttu-id="4d454-446">Nasıl tooassign lisans tooa grubu</span><span class="sxs-lookup"><span data-stu-id="4d454-446">How tooassign a license tooa group</span></span>

<span data-ttu-id="4d454-447">tooassign bir lisans tooa grubu hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="4d454-447">tooassign a license tooa group, follow hello steps below:</span></span>

1.  <span data-ttu-id="4d454-448">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="4d454-448">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="4d454-449">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="4d454-449">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4d454-450">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="4d454-450">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4d454-451">Tıklatın **kullanıcılar ve gruplar** hello Gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="4d454-451">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="4d454-452">tıklatın **tüm grupları**.</span><span class="sxs-lookup"><span data-stu-id="4d454-452">click **All groups**.</span></span>

6.  <span data-ttu-id="4d454-453">**Arama** ilgilendiğiniz hello grubu için ve **hello satıra tıklayın** tooselect.</span><span class="sxs-lookup"><span data-stu-id="4d454-453">**Search** for hello group you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="4d454-454">tıklatın **lisansları** toosee hangi lisansları hello grubuna atanmış.</span><span class="sxs-lookup"><span data-stu-id="4d454-454">click **Licenses** toosee which licenses hello group currently has assigned.</span></span>

8.  <span data-ttu-id="4d454-455">Merhaba tıklatın **atamak** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4d454-455">click hello **Assign** button.</span></span>

9.  <span data-ttu-id="4d454-456">Seçin **bir veya daha fazla ürün** mevcut ürünler hello listesinden.</span><span class="sxs-lookup"><span data-stu-id="4d454-456">Select **one or more products** from hello list of available products.</span></span>

10. <span data-ttu-id="4d454-457">**İsteğe bağlı** hello tıklatın **atama seçenekleri** öğesi toogranularly ürünleri atayın.</span><span class="sxs-lookup"><span data-stu-id="4d454-457">**Optional** click hello **assignment options** item toogranularly assign products.</span></span> <span data-ttu-id="4d454-458">Tıklatın **Tamam** ne zaman bu tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="4d454-458">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="4d454-459">Merhaba tıklatın **atamak** bu lisansları toothis Grup tooassign düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4d454-459">Click hello **Assign** button tooassign these licenses toothis group.</span></span> <span data-ttu-id="4d454-460">Bu, başlangıç boyutu ve karmaşıklığı hello grubunun bağlı olarak uzun bir süre devam edebilir.</span><span class="sxs-lookup"><span data-stu-id="4d454-460">This may take a long time, depending on hello size and complexity of hello group.</span></span>

>[!NOTE]
><span data-ttu-id="4d454-461">toodo bu daha hızlı ve göz önünde bulundurun geçici olarak bir lisans toohello kullanıcı doğrudan atama.</span><span class="sxs-lookup"><span data-stu-id="4d454-461">toodo this faster, consider temporarily assigning a license toohello user directly.</span></span> 
>
>

## <a name="next-steps"></a><span data-ttu-id="4d454-462">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4d454-462">Next steps</span></span>
[<span data-ttu-id="4d454-463">Yeni kullanıcılar tooAzure Active Directory ekleme</span><span class="sxs-lookup"><span data-stu-id="4d454-463">Add new users tooAzure Active Directory</span></span>](active-directory-users-create-azure-portal.md)

