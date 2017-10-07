---
title: "aaaHow tooconfigure federe bir galeri olmayan uygulama için çoklu oturum açmayı | Microsoft Docs"
description: "Azure AD ile toointegrate istediğiniz özel bir galeri olmayan uygulama için çoklu oturum açmayı tooconfigure nasıl Federasyon"
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
ms.openlocfilehash: f4a37cb500c075d0ce917ad8f13411f2ce208c56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="2807e-103">Nasıl bir galeri olmayan uygulama için çoklu oturum açmayı tooconfigure Federasyon</span><span class="sxs-lookup"><span data-stu-id="2807e-103">How tooconfigure federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="2807e-104">Galeri olmayan uygulama tooconfigure toohave Azure AD premium gerekir ve Merhaba uygulaması SAML 2.0 destekler.</span><span class="sxs-lookup"><span data-stu-id="2807e-104">tooconfigure a non-gallery application, you need toohave Azure AD premium and hello application supports SAML 2.0.</span></span> <span data-ttu-id="2807e-105">Azure AD sürümleri hakkında daha fazla bilgi için ziyaret [Azure AD fiyatlandırma](https://azure.microsoft.com/pricing/details/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="2807e-105">For more information about Azure AD versions, visit [Azure AD pricing](https://azure.microsoft.com/pricing/details/active-directory/).</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="2807e-106">Gerekli adımlara genel bakış</span><span class="sxs-lookup"><span data-stu-id="2807e-106">Overview of steps required</span></span>
<span data-ttu-id="2807e-107">Bir yüksek düzeyde genel bakış hello adımları federe gerekli tooconfigure tek oturum açma için Galeri olmayan aşağıdadır (örneğin, özel) uygulama.</span><span class="sxs-lookup"><span data-stu-id="2807e-107">Below is a high level overview of hello steps required tooconfigure federated single sign-on for a non-gallery (e.g., custom) application.</span></span>

-   [<span data-ttu-id="2807e-108">Azure AD (oturum açma URL'si, tanımlayıcı, yanıt URL'si) Hello uygulamanın meta veri değerlerini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="2807e-108">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#_Configuring_single_sign-on)

-   [<span data-ttu-id="2807e-109">Kullanıcı tanımlayıcısı seçin ve kullanıcı öznitelikleri gönderilen toobe toohello uygulaması ekleyin</span><span class="sxs-lookup"><span data-stu-id="2807e-109">Select User Identifier and add user attributes toobe sent toohello application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="2807e-110">Azure AD meta verileri ve sertifika alma</span><span class="sxs-lookup"><span data-stu-id="2807e-110">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="2807e-111">Merhaba uygulaması (oturum açma URL'si, veren, oturum kapatma URL'si ve sertifika) Azure AD meta veri değerlerini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="2807e-111">Configure Azure AD metadata values in hello application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#_Configuring_single_sign-on)

-   [<span data-ttu-id="2807e-112">Kullanıcıların toohello uygulama atama</span><span class="sxs-lookup"><span data-stu-id="2807e-112">Assign users toohello application</span></span>](#_Assign_users_to_the_application)

## <a name="configuring-single-sign-on-toonon-gallery-applications"></a><span data-ttu-id="2807e-113">Çoklu oturum açma toonon-galeri uygulamaları yapılandırma</span><span class="sxs-lookup"><span data-stu-id="2807e-113">Configuring single sign-on toonon-gallery applications</span></span>

<span data-ttu-id="2807e-114">tooconfigure çoklu oturum açma hello Azure AD Galerisi'nde olmayan bir uygulama için başlangıç adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="2807e-114">tooconfigure single sign-on for an application that is not in hello Azure AD gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="2807e-115">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="2807e-115">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="2807e-116">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="2807e-116">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2807e-117">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="2807e-117">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2807e-118">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="2807e-118">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="2807e-119">Merhaba tıklatın **Ekle** hello sağ üst köşesindeki hello düğmesi **kurumsal uygulamalar** dikey.</span><span class="sxs-lookup"><span data-stu-id="2807e-119">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="2807e-120">tıklatın **olmayan galeri uygulama** hello içinde **kendi uygulama Ekle** bölümü</span><span class="sxs-lookup"><span data-stu-id="2807e-120">click **Non-gallery application** in hello **Add your own app** section</span></span>

7.  <span data-ttu-id="2807e-121">Merhaba Merhaba uygulaması hello adını **adı** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="2807e-121">Enter hello name of hello application in hello **Name** textbox.</span></span>

8.  <span data-ttu-id="2807e-122">Tıklatın **Ekle** button, tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="2807e-122">Click **Add** button, tooadd hello application.</span></span>

9.  <span data-ttu-id="2807e-123">Merhaba uygulamanın yüklediği sonra hello tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="2807e-123">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

10. <span data-ttu-id="2807e-124">Seçin **SAML tabanlı oturum açma** hello içinde **modu** açılır.</span><span class="sxs-lookup"><span data-stu-id="2807e-124">Select **SAML-based Sign-on** in hello **Mode** dropdown.</span></span>

11. <span data-ttu-id="2807e-125">Merhaba gerekli değerleri girin **etki alanı ve URL'ler.**</span><span class="sxs-lookup"><span data-stu-id="2807e-125">Enter hello required values in **Domain and URLs.**</span></span> <span data-ttu-id="2807e-126">Bu değerleri hello uygulama satıcısından almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2807e-126">You should get these values from hello application vendor.</span></span>

   1. <span data-ttu-id="2807e-127">IDP tarafından başlatılan SSO'yu olarak tooconfigure hello uygulama hello yanıt URL'si ve hello tanımlayıcısı girin.</span><span class="sxs-lookup"><span data-stu-id="2807e-127">tooconfigure hello application as IdP-initiated SSO, enter hello Reply URL and hello Identifier.</span></span>

   2. <span data-ttu-id="2807e-128">**İsteğe bağlı:** tooconfigure hello uygulama SP tarafından başlatılan SSO'yu olarak hello oturum URL'yi, gerekli bir değerdir.</span><span class="sxs-lookup"><span data-stu-id="2807e-128">**Optional:** tooconfigure hello application as SP-initiated SSO, hello Sign on URL it’s a required value.</span></span>

12. <span data-ttu-id="2807e-129">Merhaba, **kullanıcı öznitelikleri**, select hello hello kullanıcılarınız için benzersiz tanımlayıcı **kullanıcı tanımlayıcısı** açılır.</span><span class="sxs-lookup"><span data-stu-id="2807e-129">In hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

13. <span data-ttu-id="2807e-130">**İsteğe bağlı:** tıklatın **Görünüm ve diğer tüm kullanıcı özniteliklerini düzenleme** tooedit Merhaba, kullanıcı oturum açtığında gönderilen toobe toohello hello SAML belirteci uygulamada öznitelikleri.</span><span class="sxs-lookup"><span data-stu-id="2807e-130">**Optional:** click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="2807e-131">bir öznitelik tooadd:</span><span class="sxs-lookup"><span data-stu-id="2807e-131">tooadd an attribute:</span></span>

   1. <span data-ttu-id="2807e-132">tıklatın **Ekle özniteliği**.</span><span class="sxs-lookup"><span data-stu-id="2807e-132">click **Add attribute**.</span></span> <span data-ttu-id="2807e-133">Merhaba girin **adı** ve hello select hello **değeri** gelen hello açılır.</span><span class="sxs-lookup"><span data-stu-id="2807e-133">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="2807e-134">Tıklatın **kaydedin.**</span><span class="sxs-lookup"><span data-stu-id="2807e-134">Click **Save.**</span></span> <span data-ttu-id="2807e-135">Yeni bir öznitelik hello hello tablosundaki bakın.</span><span class="sxs-lookup"><span data-stu-id="2807e-135">You see hello new attribute in hello table.</span></span>

14. <span data-ttu-id="2807e-136">tıklatın **yapılandırma &lt;uygulama adı&gt;**  tooaccess belgelerine nasıl tooconfigure çoklu oturum açma hello uygulamada.</span><span class="sxs-lookup"><span data-stu-id="2807e-136">click **Configure &lt;application name&gt;** tooaccess documentation on how tooconfigure single sign-on in hello application.</span></span> <span data-ttu-id="2807e-137">Ayrıca, Azure AD URL'leri ve hello uygulama için gerekli sertifika sahiptir.</span><span class="sxs-lookup"><span data-stu-id="2807e-137">Also, you has Azure AD URLs and certificate required for hello application.</span></span>

15. [<span data-ttu-id="2807e-138">Kullanıcıların toohello uygulama atayın.</span><span class="sxs-lookup"><span data-stu-id="2807e-138">Assign users toohello application.</span></span>](#assign-users-to-the-application)

## <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a><span data-ttu-id="2807e-139">Kullanıcı tanımlayıcısı seçin ve kullanıcı öznitelikleri gönderilen toobe toohello uygulaması ekleyin</span><span class="sxs-lookup"><span data-stu-id="2807e-139">Select User Identifier and add user attributes toobe sent toohello application</span></span>

<span data-ttu-id="2807e-140">tooselect kullanıcı tanımlayıcısı Merhaba veya kullanıcı öznitelikleri ekleme, hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="2807e-140">tooselect hello User Identifier or add user attributes, follow hello steps below:</span></span>

1.  <span data-ttu-id="2807e-141">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="2807e-141">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="2807e-142">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="2807e-142">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2807e-143">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="2807e-143">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2807e-144">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="2807e-144">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="2807e-145">Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.</span><span class="sxs-lookup"><span data-stu-id="2807e-145">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="2807e-146">Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**</span><span class="sxs-lookup"><span data-stu-id="2807e-146">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="2807e-147">Çoklu oturum açma yapılandırdığınız hello uygulaması'nı seçin.</span><span class="sxs-lookup"><span data-stu-id="2807e-147">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="2807e-148">Merhaba uygulamanın yüklediği sonra hello tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="2807e-148">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="2807e-149">Merhaba altında **kullanıcı öznitelikleri** bölümünde, select hello hello kullanıcılarınız için benzersiz tanımlayıcı **kullanıcı tanımlayıcısı** açılır.</span><span class="sxs-lookup"><span data-stu-id="2807e-149">Under hello **User attributes** section, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span> <span data-ttu-id="2807e-150">Merhaba seçeneği hello uygulama tooauthenticate hello kullanıcı toomatch hello beklenen değer gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="2807e-150">hello selected option needs toomatch hello expected value in hello application tooauthenticate hello user.</span></span>

 ><span data-ttu-id="2807e-151">[! Azure AD seçili hello değere göre hello NameID özniteliği (kullanıcı tanımlayıcısı) için hello biçimini seçin veya hello SAML AuthRequest hello uygulama tarafından istenen biçim hello unutmayın}.</span><span class="sxs-lookup"><span data-stu-id="2807e-151">[!NOTE} Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="2807e-152">Daha fazla bilgi için hello makalesine bakın [tek oturum açma SAML Protokolü](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) NameIDPolicy altında hello bölüm.</span><span class="sxs-lookup"><span data-stu-id="2807e-152">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>
 >
 >

9.  <span data-ttu-id="2807e-153">tooadd kullanıcı öznitelikleri, tıklatın **Görünüm ve diğer tüm kullanıcı özniteliklerini düzenleme** tooedit Merhaba, kullanıcı oturum açtığında gönderilen toobe toohello hello SAML belirteci uygulamada öznitelikleri.</span><span class="sxs-lookup"><span data-stu-id="2807e-153">tooadd user attributes, click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="2807e-154">bir öznitelik tooadd:</span><span class="sxs-lookup"><span data-stu-id="2807e-154">tooadd an attribute:</span></span>

   1. <span data-ttu-id="2807e-155">tıklatın **Ekle özniteliği**.</span><span class="sxs-lookup"><span data-stu-id="2807e-155">click **Add attribute**.</span></span> <span data-ttu-id="2807e-156">Merhaba girin **adı** ve hello select hello **değeri** gelen hello açılır.</span><span class="sxs-lookup"><span data-stu-id="2807e-156">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="2807e-157">Tıklatın **kaydedin.**</span><span class="sxs-lookup"><span data-stu-id="2807e-157">Click **Save.**</span></span> <span data-ttu-id="2807e-158">Yeni bir öznitelik hello hello tablosundaki bakın.</span><span class="sxs-lookup"><span data-stu-id="2807e-158">You see hello new attribute in hello table.</span></span>

## <a name="download-hello-azure-ad-metadata-or-certificate"></a><span data-ttu-id="2807e-159">Hello Azure AD meta verileri veya sertifika yükleme</span><span class="sxs-lookup"><span data-stu-id="2807e-159">Download hello Azure AD metadata or certificate</span></span>

<span data-ttu-id="2807e-160">toodownload hello uygulama meta verileri veya sertifika Azure AD'den hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="2807e-160">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="2807e-161">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="2807e-161">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="2807e-162">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="2807e-162">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2807e-163">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="2807e-163">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2807e-164">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="2807e-164">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="2807e-165">Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.</span><span class="sxs-lookup"><span data-stu-id="2807e-165">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="2807e-166">Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**</span><span class="sxs-lookup"><span data-stu-id="2807e-166">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="2807e-167">Çoklu oturum açma yapılandırdığınız hello uygulaması'nı seçin.</span><span class="sxs-lookup"><span data-stu-id="2807e-167">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="2807e-168">Merhaba uygulamanın yüklediği sonra hello tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="2807e-168">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="2807e-169">Çok Git**SAML imzalama sertifikası** bölümünde ve ardından **karşıdan** sütun değeri.</span><span class="sxs-lookup"><span data-stu-id="2807e-169">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="2807e-170">Çoklu oturum açma yapılandırma hangi hello uygulama gerektirir bağlı olarak, meta veri XML hello veya sertifika hello ya da hello seçeneği toodownload bakın.</span><span class="sxs-lookup"><span data-stu-id="2807e-170">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

<span data-ttu-id="2807e-171">Azure AD, URL tooget hello meta verilerinin sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="2807e-171">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="2807e-172">Merhaba meta veriler yalnızca bir XML dosyası olarak alınabilir.</span><span class="sxs-lookup"><span data-stu-id="2807e-172">hello metadata can only be retrieved as a XML file.</span></span>

## <a name="assign-users-toohello-application"></a><span data-ttu-id="2807e-173">Kullanıcıların toohello uygulama atama</span><span class="sxs-lookup"><span data-stu-id="2807e-173">Assign users toohello application</span></span>

<span data-ttu-id="2807e-174">tooassign bir veya daha fazla kullanıcı tooan uygulama, doğrudan başlangıç adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="2807e-174">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="2807e-175">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici.**</span><span class="sxs-lookup"><span data-stu-id="2807e-175">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="2807e-176">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="2807e-176">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2807e-177">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="2807e-177">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2807e-178">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="2807e-178">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="2807e-179">Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.</span><span class="sxs-lookup"><span data-stu-id="2807e-179">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="2807e-180">Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**</span><span class="sxs-lookup"><span data-stu-id="2807e-180">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="2807e-181">Tooassign kullanıcı toofrom hello listesini hello uygulamasını seçin.</span><span class="sxs-lookup"><span data-stu-id="2807e-181">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="2807e-182">Merhaba uygulamanın yüklediği sonra tıklayın **kullanıcılar ve gruplar** hello uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="2807e-182">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="2807e-183">Hello tıklatın **Ekle** hello üstünde düğmesi **kullanıcılar ve gruplar** listesi tooopen hello **eklemek atama** dikey.</span><span class="sxs-lookup"><span data-stu-id="2807e-183">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="2807e-184">Merhaba tıklatın **kullanıcılar ve gruplar** hello seçicisini **eklemek atama** dikey.</span><span class="sxs-lookup"><span data-stu-id="2807e-184">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="2807e-185">Merhaba türü **tam adı** veya **e-posta adresi** hello atama ilgilenen hello kullanıcının **ad veya e-posta adresine göre arama** arama kutusu.</span><span class="sxs-lookup"><span data-stu-id="2807e-185">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="2807e-186">Merhaba getirin **kullanıcı** hello listesi tooreveal içinde bir **onay kutusunu**.</span><span class="sxs-lookup"><span data-stu-id="2807e-186">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="2807e-187">Kullanıcı toohello Hello onay kutusu sonraki toohello kullanıcının profili fotoğraf veya logosu tooadd tıklatın **seçili** listesi.</span><span class="sxs-lookup"><span data-stu-id="2807e-187">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="2807e-188">**İsteğe bağlı:** çok isterseniz**birden fazla kullanıcı ekleme**, başka bir tür **tam adı** veya **e-posta adresi** hello içine **ada göre ara veya e-posta adresi** arama kutusu ve bu kullanıcı toohello hello onay kutusunu tooadd tıklatın **seçili** listesi.</span><span class="sxs-lookup"><span data-stu-id="2807e-188">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="2807e-189">Kullanıcıların seçerek bittiğinde hello tıklatın **seçin** düğmesini tooadd bunları kullanıcılar ve gruplar toobe toohello listesi atanan toohello uygulama.</span><span class="sxs-lookup"><span data-stu-id="2807e-189">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="2807e-190">**İsteğe bağlı:** hello tıklatın **rolü Seç** hello seçicide **eklemek atama** dikey tooselect rol seçtiğiniz tooassign toohello kullanıcılar.</span><span class="sxs-lookup"><span data-stu-id="2807e-190">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="2807e-191">Merhaba tıklatın **atamak** düğmesini tooassign hello uygulama toohello seçilen kullanıcılar.</span><span class="sxs-lookup"><span data-stu-id="2807e-191">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="2807e-192">Bir kısa süre sonra seçtiğiniz hello kullanıcıların hello çözüm Açıklama bölümünde açıklanan yöntemleri kullanarak bu uygulamaları hello mümkün toolaunch olması.</span><span class="sxs-lookup"><span data-stu-id="2807e-192">After a short period of time, hello users you have selected be able toolaunch these applications using hello methods described in hello solution description section.</span></span>

## <a name="customizing-hello-saml-claims-sent-tooan-application"></a><span data-ttu-id="2807e-193">Gönderilen tooan uygulama Hello SAML talepler özelleştiriliyor</span><span class="sxs-lookup"><span data-stu-id="2807e-193">Customizing hello SAML claims sent tooan application</span></span>

<span data-ttu-id="2807e-194">toolearn tooyour uygulama toocustomize hello SAML öznitelik taleplerini gönderilen nasıl bkz [talep eşleme Azure Active Directory'de](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="2807e-194">toolearn how toocustomize hello SAML attribute claims sent tooyour application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2807e-195">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2807e-195">Next steps</span></span>
[<span data-ttu-id="2807e-196">Uygulama proxy'si ile çoklu oturum açma tooyour uygulamaları sağlayın</span><span class="sxs-lookup"><span data-stu-id="2807e-196">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
