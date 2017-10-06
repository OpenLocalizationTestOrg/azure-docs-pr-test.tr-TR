---
title: "Federasyon tek oturum açma için Azure AD galeri uygulamanın yapılandırma aaaProblem | Microsoft Docs"
description: "Bazı yapılandırma tek federe olduğunda karşılaşabilir hello yaygın sorunları ele hello Azure AD uygulama galerisinde listelenen uygulamalar için SAML kullanarak oturum"
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
ms.openlocfilehash: 2ae1e511bd49b19159e1ab83cf79a7db5403b9a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="326c6-103">Federasyon tek oturum açma için Azure AD galeri uygulamanın yapılandırma sorunu</span><span class="sxs-lookup"><span data-stu-id="326c6-103">Problem configuring federated single sign-on for an Azure AD Gallery application</span></span>

<span data-ttu-id="326c6-104">Bir uygulama yapılandırırken bir sorunla karşılaşırsanız.</span><span class="sxs-lookup"><span data-stu-id="326c6-104">If you encounter a problem when configuring an application.</span></span> <span data-ttu-id="326c6-105">Merhaba uygulaması için başlangıç Öğreticisi tüm hello adımları izlediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="326c6-105">Verify you have followed all hello steps in hello tutorial for hello application.</span></span> <span data-ttu-id="326c6-106">Merhaba uygulamanın yapılandırma dosyasındaki satır içi belgeleri nasıl tooconfigure hello uygulama üzerinde sahip.</span><span class="sxs-lookup"><span data-stu-id="326c6-106">In hello application’s configuration, you have inline documentation on how tooconfigure hello application.</span></span> <span data-ttu-id="326c6-107">Ayrıca, hello erişebilirsiniz [nasıl öğreticiler listesi toointegrate SaaS uygulamaları Azure Active Directory ile](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) ayrıntılı adım adım yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="326c6-107">Also, you can access hello [List of tutorials on how toointegrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for a detail step-by-step guidance.</span></span>

## <a name="cant-add-another-instance-of-hello-application"></a><span data-ttu-id="326c6-108">Merhaba uygulaması başka bir örneği eklenemiyor</span><span class="sxs-lookup"><span data-stu-id="326c6-108">Can’t add another instance of hello application</span></span>

<span data-ttu-id="326c6-109">bir uygulamanın ikinci bir örneğini tooadd, toobe yapabileceksiniz da gerekir:</span><span class="sxs-lookup"><span data-stu-id="326c6-109">tooadd a second instance of an application, you need toobe able to:</span></span>

-   <span data-ttu-id="326c6-110">Merhaba ikinci örneği için benzersiz bir tanımlayıcı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="326c6-110">Configure a unique identifier for hello second instance.</span></span> <span data-ttu-id="326c6-111">Merhaba ilk örnek için kullanılan aynı tanımlayıcısı mümkün tooconfigure hello olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="326c6-111">You won’t be able tooconfigure hello same identifier used for hello first instance.</span></span>

-   <span data-ttu-id="326c6-112">Merhaba hello ilk örnek için kullanılan daha farklı bir sertifika yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="326c6-112">Configure a different certificate than hello one used for hello first instance.</span></span>

<span data-ttu-id="326c6-113">Merhaba, uygulama hello yukarıdaki hiçbirini desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="326c6-113">If hello application doesn’t support any of hello above.</span></span> <span data-ttu-id="326c6-114">Ardından, mümkün tooconfigure ikinci bir örneğini olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="326c6-114">Then, you won’t be able tooconfigure a second instance.</span></span>

## <a name="cant-add-hello-identifier-or-hello-reply-url"></a><span data-ttu-id="326c6-115">Merhaba tanımlayıcı ekleyemez veya yanıt URL'si hello</span><span class="sxs-lookup"><span data-stu-id="326c6-115">Can’t add hello Identifier or hello Reply URL</span></span>

<span data-ttu-id="326c6-116">Mümkün tooconfigure hello tanımlayıcısı değil olduğunuz veya yanıt URL'si Merhaba, hello tanımlayıcı onaylayın ve yanıt URL'si değerleri hello uygulama için önceden yapılandırılmış hello düzenleri eşleşir.</span><span class="sxs-lookup"><span data-stu-id="326c6-116">If you’re not able tooconfigure hello Identifier or hello Reply URL, confirm hello Identifier and Reply URL values match hello patterns pre-configured for hello application.</span></span>

<span data-ttu-id="326c6-117">Merhaba uygulaması için önceden yapılandırılmış tooknow hello modelleri:</span><span class="sxs-lookup"><span data-stu-id="326c6-117">tooknow hello patterns pre-configured for hello application:</span></span>

1.  <span data-ttu-id="326c6-118">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici** Toostep 7 gidin.</span><span class="sxs-lookup"><span data-stu-id="326c6-118">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.** Go toostep 7.</span></span> <span data-ttu-id="326c6-119">Üzerinde Azure AD hello uygulama yapılandırma dikey penceresinde zaten varsa.</span><span class="sxs-lookup"><span data-stu-id="326c6-119">If you are already in hello application configuration blade on Azure AD.</span></span>

2.  <span data-ttu-id="326c6-120">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="326c6-120">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="326c6-121">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="326c6-121">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="326c6-122">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="326c6-122">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="326c6-123">Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.</span><span class="sxs-lookup"><span data-stu-id="326c6-123">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="326c6-124">Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**</span><span class="sxs-lookup"><span data-stu-id="326c6-124">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="326c6-125">Tooconfigure çoklu oturum açma hello uygulamasını seçin.</span><span class="sxs-lookup"><span data-stu-id="326c6-125">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="326c6-126">Merhaba uygulamanın yüklediği sonra hello tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="326c6-126">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="326c6-127">Seçin **SAML tabanlı oturum açma** hello gelen **modu** açılır.</span><span class="sxs-lookup"><span data-stu-id="326c6-127">Select **SAML-based Sign-on** from hello **Mode** dropdown.</span></span>

9.  <span data-ttu-id="326c6-128">Toohello Git **tanımlayıcısı** veya **yanıt URL'si** hello altındaki metin kutusuna **etki alanı ve URL'ler bölümü.**</span><span class="sxs-lookup"><span data-stu-id="326c6-128">Go toohello **Identifier** or **Reply URL** textbox, under hello **Domain and URLs section.**</span></span>

10. <span data-ttu-id="326c6-129">Merhaba uygulaması için tooknow desteklenen hello desenleri üç yolu vardır:</span><span class="sxs-lookup"><span data-stu-id="326c6-129">There are three ways tooknow hello supported patterns for hello application:</span></span>

   * <span data-ttu-id="326c6-130">Merhaba metin kutusuna bir yer tutucu olarak desteklenen hello desenler bkz *örnek:* <https://contoso.com>.</span><span class="sxs-lookup"><span data-stu-id="326c6-130">In hello textbox, you see hello supported pattern(s) as a placeholder *Example:* <https://contoso.com>.</span></span>

   * <span data-ttu-id="326c6-131">Merhaba düzeni desteklenmiyorsa tooenter hello değeri hello metin kutusuna çalıştığınızda kırmızı bir ünlem işareti bakın.</span><span class="sxs-lookup"><span data-stu-id="326c6-131">if hello pattern is not supported, you see a red exclamation mark when you try tooenter hello value in hello textbox.</span></span> <span data-ttu-id="326c6-132">Farenizi hello kırmızı bir ünlem işareti getirirseniz, desteklenen hello desenleri bakın.</span><span class="sxs-lookup"><span data-stu-id="326c6-132">If you hover your mouse over hello red exclamation mark, you see hello supported patterns.</span></span>

   * <span data-ttu-id="326c6-133">Merhaba uygulaması Hello öğreticide, desteklenen hello desenleri hakkında bilgi alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="326c6-133">In hello tutorial for hello application, you can also get information about hello supported patterns.</span></span> <span data-ttu-id="326c6-134">Merhaba altında **yapılandırma Azure AD çoklu oturum açma** bölümü.</span><span class="sxs-lookup"><span data-stu-id="326c6-134">Under hello **Configure Azure AD single sign-on** section.</span></span> <span data-ttu-id="326c6-135">Git toohello adım hello altında yapılandırılmış hello değerleri için **etki alanı ve URL'leri** bölümü.</span><span class="sxs-lookup"><span data-stu-id="326c6-135">Go toohello step for configured hello values under hello **Domain and URLs** section.</span></span>

<span data-ttu-id="326c6-136">Merhaba, değerleri üzerinde Azure AD önceden yapılandırılmış hello desen ile eşleşmiyor.</span><span class="sxs-lookup"><span data-stu-id="326c6-136">If hello values don’t match with hello patterns pre-configured on Azure AD.</span></span> <span data-ttu-id="326c6-137">Şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="326c6-137">You can:</span></span>

-   <span data-ttu-id="326c6-138">Üzerinde Azure AD önceden yapılandırılmış hello desenle eşleşen hello uygulama satıcı tooget değerleri ile çalışma</span><span class="sxs-lookup"><span data-stu-id="326c6-138">Work with hello application vendor tooget values that match hello pattern pre-configured on Azure AD</span></span>

-   <span data-ttu-id="326c6-139">Veya, Azure AD ekibi sizinle < aadapprequest@microsoft.com > veya hello öğretici toorequest hello güncelleştirmesi hello uygulama için desteklenen hello desenlerinin bir yorum yazın</span><span class="sxs-lookup"><span data-stu-id="326c6-139">Or, you can contact Azure AD team at <aadapprequest@microsoft.com> or leave a comment in hello tutorial toorequest hello update of hello supported patterns for hello application</span></span>

## <a name="where-do-i-set-hello-entityid-user-identifier-format"></a><span data-ttu-id="326c6-140">Merhaba Entityıd (kullanıcı tanımlayıcısı) biçimi belirlendiği</span><span class="sxs-lookup"><span data-stu-id="326c6-140">Where do I set hello EntityID (User Identifier) format</span></span>

<span data-ttu-id="326c6-141">Azure AD hello yanıtta toohello uygulama kullanıcı kimlik doğrulamasından sonra gönderir mümkün tooselect hello Entityıd (kullanıcı tanımlayıcısı) biçimi olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="326c6-141">You won’t be able tooselect hello EntityID (User Identifier) format that Azure AD sends toohello application in hello response after user authentication.</span></span>

<span data-ttu-id="326c6-142">Merhaba NameID özniteliği (kullanıcı tanımlayıcısı) için Azure AD select hello biçimi seçili hello değere göre veya hello SAML AuthRequest hello uygulama tarafından istenen biçim hello.</span><span class="sxs-lookup"><span data-stu-id="326c6-142">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="326c6-143">Daha fazla bilgi için hello makale ziyaret [tek oturum açma SAML Protokolü](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) NameIDPolicy, hello bölümünde</span><span class="sxs-lookup"><span data-stu-id="326c6-143">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy,</span></span>

## <a name="cant-find-hello-azure-ad-metadata-toocomplete-hello-configuration-with-hello-application"></a><span data-ttu-id="326c6-144">Hello Azure AD meta veri toocomplete hello yapılandırması hello uygulamayla bulunamıyor</span><span class="sxs-lookup"><span data-stu-id="326c6-144">Can’t find hello Azure AD metadata toocomplete hello configuration with hello application</span></span>

<span data-ttu-id="326c6-145">toodownload hello uygulama meta verileri veya sertifika Azure AD'den hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="326c6-145">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="326c6-146">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="326c6-146">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="326c6-147">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="326c6-147">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="326c6-148">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="326c6-148">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="326c6-149">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="326c6-149">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="326c6-150">Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.</span><span class="sxs-lookup"><span data-stu-id="326c6-150">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="326c6-151">Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**</span><span class="sxs-lookup"><span data-stu-id="326c6-151">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="326c6-152">Çoklu oturum açma yapılandırdığınız hello uygulaması'nı seçin.</span><span class="sxs-lookup"><span data-stu-id="326c6-152">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="326c6-153">Merhaba uygulamanın yüklediği sonra hello tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="326c6-153">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="326c6-154">Çok Git**SAML imzalama sertifikası** bölümünde ve ardından **karşıdan** sütun değeri.</span><span class="sxs-lookup"><span data-stu-id="326c6-154">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="326c6-155">Çoklu oturum açma yapılandırma hangi hello uygulama gerektirir bağlı olarak, meta veri XML hello veya sertifika hello ya da hello seçeneği toodownload bakın.</span><span class="sxs-lookup"><span data-stu-id="326c6-155">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

<span data-ttu-id="326c6-156">Azure AD, URL tooget hello meta verilerinin sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="326c6-156">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="326c6-157">Merhaba meta veriler yalnızca bir XML dosyası olarak alınabilir.</span><span class="sxs-lookup"><span data-stu-id="326c6-157">hello metadata can only be retrieved as a XML file.</span></span>

## <a name="dont-know-how-toocustomize-saml-claims-sent-tooan-application"></a><span data-ttu-id="326c6-158">Toocustomize SAML talep tooan uygulama nasıl gönderileceğini bilmiyorsanız</span><span class="sxs-lookup"><span data-stu-id="326c6-158">Don't know how toocustomize SAML claims sent tooan application</span></span>

<span data-ttu-id="326c6-159">toolearn tooyour uygulama toocustomize hello SAML öznitelik taleplerini gönderilen nasıl bkz [talep eşleme Azure Active Directory'de](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="326c6-159">toolearn how toocustomize hello SAML attribute claims sent tooyour application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="326c6-160">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="326c6-160">Next steps</span></span>
[<span data-ttu-id="326c6-161">Azure Active Directory ile uygulamaları yönetme</span><span class="sxs-lookup"><span data-stu-id="326c6-161">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
