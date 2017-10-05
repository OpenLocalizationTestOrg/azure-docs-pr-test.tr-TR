---
title: "Federasyon tek oturum açma için Azure AD galeri uygulamanın yapılandırma sorunu | Microsoft Docs"
description: "Bazı yapılandırma tek federe olduğunda karşılaşabilir yaygın sorunları ele Azure AD uygulama galerisinde listelenen uygulamalar için SAML kullanarak oturum"
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
ms.openlocfilehash: 290ca66048281de5e031b0404919bed84ab19ffa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="problem-configuring-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="8ec51-103">Federasyon tek oturum açma için Azure AD galeri uygulamanın yapılandırma sorunu</span><span class="sxs-lookup"><span data-stu-id="8ec51-103">Problem configuring federated single sign-on for an Azure AD Gallery application</span></span>

<span data-ttu-id="8ec51-104">Bir uygulama yapılandırırken bir sorunla karşılaşırsanız.</span><span class="sxs-lookup"><span data-stu-id="8ec51-104">If you encounter a problem when configuring an application.</span></span> <span data-ttu-id="8ec51-105">Uygulama için öğreticideki tüm adımları izlediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="8ec51-105">Verify you have followed all the steps in the tutorial for the application.</span></span> <span data-ttu-id="8ec51-106">Uygulamanın yapılandırma dosyasındaki satır içi belgeleri uygulama yapılandırma konusunda sahip.</span><span class="sxs-lookup"><span data-stu-id="8ec51-106">In the application’s configuration, you have inline documentation on how to configure the application.</span></span> <span data-ttu-id="8ec51-107">Ayrıca, erişim [SaaS uygulamaları Azure Active Directory ile tümleştirme hakkında öğreticiler listesi](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) ayrıntılı adım adım yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="8ec51-107">Also, you can access the [List of tutorials on how to integrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for a detail step-by-step guidance.</span></span>

## <a name="cant-add-another-instance-of-the-application"></a><span data-ttu-id="8ec51-108">Uygulama başka bir örneği eklenemiyor</span><span class="sxs-lookup"><span data-stu-id="8ec51-108">Can’t add another instance of the application</span></span>

<span data-ttu-id="8ec51-109">Uygulamanın ikinci bir örneğini eklemek için şunları yapması gerekir:</span><span class="sxs-lookup"><span data-stu-id="8ec51-109">To add a second instance of an application, you need to be able to:</span></span>

-   <span data-ttu-id="8ec51-110">İkinci örneği için benzersiz bir tanımlayıcı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="8ec51-110">Configure a unique identifier for the second instance.</span></span> <span data-ttu-id="8ec51-111">İlk örnek için kullanılan aynı tanımlayıcısı yapılandırmanız mümkün olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="8ec51-111">You won’t be able to configure the same identifier used for the first instance.</span></span>

-   <span data-ttu-id="8ec51-112">İlk örnek için kullanılan olandan farklı bir sertifika yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="8ec51-112">Configure a different certificate than the one used for the first instance.</span></span>

<span data-ttu-id="8ec51-113">Yukarıdakilerin tümü uygulamayı desteklemiyorsa.</span><span class="sxs-lookup"><span data-stu-id="8ec51-113">If the application doesn’t support any of the above.</span></span> <span data-ttu-id="8ec51-114">Ardından, ikinci bir örneğini yapılandırmanız mümkün olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="8ec51-114">Then, you won’t be able to configure a second instance.</span></span>

## <a name="cant-add-the-identifier-or-the-reply-url"></a><span data-ttu-id="8ec51-115">Tanımlayıcı veya yanıt URL'si eklenemiyor</span><span class="sxs-lookup"><span data-stu-id="8ec51-115">Can’t add the Identifier or the Reply URL</span></span>

<span data-ttu-id="8ec51-116">Tanımlayıcı veya yanıt URL'si yapılandırmadı değilseniz, uygulama için önceden yapılandırılmış desenleri tanımlayıcısı ve yanıt URL'si değerleri eşleşen onaylayın.</span><span class="sxs-lookup"><span data-stu-id="8ec51-116">If you’re not able to configure the Identifier or the Reply URL, confirm the Identifier and Reply URL values match the patterns pre-configured for the application.</span></span>

<span data-ttu-id="8ec51-117">Uygulama için önceden yapılandırılmış desenleri öğrenmek için:</span><span class="sxs-lookup"><span data-stu-id="8ec51-117">To know the patterns pre-configured for the application:</span></span>

1.  <span data-ttu-id="8ec51-118">Açık [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="8ec51-118">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span> <span data-ttu-id="8ec51-119">7. adıma gidin.</span><span class="sxs-lookup"><span data-stu-id="8ec51-119">Go to step 7.</span></span> <span data-ttu-id="8ec51-120">Üzerinde Azure AD uygulama yapılandırma dikey penceresinde zaten varsa.</span><span class="sxs-lookup"><span data-stu-id="8ec51-120">If you are already in the application configuration blade on Azure AD.</span></span>

2.  <span data-ttu-id="8ec51-121">Açık **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** ana sol taraftaki gezinti menüsünde sonundaki.</span><span class="sxs-lookup"><span data-stu-id="8ec51-121">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="8ec51-122">Yazın **"Azure Active Directory**" Filtre Arama kutusuna seçip **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="8ec51-122">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="8ec51-123">tıklatın **kurumsal uygulamalar** Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="8ec51-123">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="8ec51-124">tıklatın **tüm uygulamaları** tüm uygulamaların bir listesini görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="8ec51-124">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="8ec51-125">Burada gösterisini istediğiniz uygulama görmüyorsanız kullanın **filtre** üst kısmındaki denetim **tüm uygulamalar listesini** ve **Göster** için seçenek **tüm uygulamaları.**</span><span class="sxs-lookup"><span data-stu-id="8ec51-125">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="8ec51-126">Çoklu oturum açma yapılandırmak istediğiniz uygulamayı seçin.</span><span class="sxs-lookup"><span data-stu-id="8ec51-126">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="8ec51-127">Uygulamanın yüklediği sonra tıklayın **çoklu oturum açma** uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="8ec51-127">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="8ec51-128">Seçin **SAML tabanlı oturum açma** gelen **modu** açılır.</span><span class="sxs-lookup"><span data-stu-id="8ec51-128">Select **SAML-based Sign-on** from the **Mode** dropdown.</span></span>

9.  <span data-ttu-id="8ec51-129">Git **tanımlayıcısı** veya **yanıt URL'si** metin kutusu altında **etki alanı ve URL'ler bölümü.**</span><span class="sxs-lookup"><span data-stu-id="8ec51-129">Go to the **Identifier** or **Reply URL** textbox, under the **Domain and URLs section.**</span></span>

10. <span data-ttu-id="8ec51-130">Uygulama için desteklenen desenleri bilmeniz üç yolu vardır:</span><span class="sxs-lookup"><span data-stu-id="8ec51-130">There are three ways to know the supported patterns for the application:</span></span>

   * <span data-ttu-id="8ec51-131">Metin kutusuna bir yer tutucu olarak desteklenen desenler bkz *örnek:* <https://contoso.com>.</span><span class="sxs-lookup"><span data-stu-id="8ec51-131">In the textbox, you see the supported pattern(s) as a placeholder *Example:* <https://contoso.com>.</span></span>

   * <span data-ttu-id="8ec51-132">Desen desteklenmiyorsa, metin kutusuna bir değer girmenizi çalıştığınızda, kırmızı bir ünlem işareti görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="8ec51-132">if the pattern is not supported, you see a red exclamation mark when you try to enter the value in the textbox.</span></span> <span data-ttu-id="8ec51-133">Farenizi kırmızı bir ünlem işareti getirirseniz, desteklenen desenleri bakın.</span><span class="sxs-lookup"><span data-stu-id="8ec51-133">If you hover your mouse over the red exclamation mark, you see the supported patterns.</span></span>

   * <span data-ttu-id="8ec51-134">Uygulama için öğreticide desteklenen desenleri hakkında bilgi alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8ec51-134">In the tutorial for the application, you can also get information about the supported patterns.</span></span> <span data-ttu-id="8ec51-135">Altında **yapılandırma Azure AD çoklu oturum açma** bölümü.</span><span class="sxs-lookup"><span data-stu-id="8ec51-135">Under the **Configure Azure AD single sign-on** section.</span></span> <span data-ttu-id="8ec51-136">Altındaki değerleri yapılandırılmış adıma Git **etki alanı ve URL'leri** bölümü.</span><span class="sxs-lookup"><span data-stu-id="8ec51-136">Go to the step for configured the values under the **Domain and URLs** section.</span></span>

<span data-ttu-id="8ec51-137">Değerler üzerinde Azure AD önceden yapılandırılmış desenlerle eşleşmiyorsa.</span><span class="sxs-lookup"><span data-stu-id="8ec51-137">If the values don’t match with the patterns pre-configured on Azure AD.</span></span> <span data-ttu-id="8ec51-138">Şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="8ec51-138">You can:</span></span>

-   <span data-ttu-id="8ec51-139">Üzerinde Azure AD önceden yapılandırılmış bir desenle eşleşen değerleri almak için uygulama satıcısına ile çalışma</span><span class="sxs-lookup"><span data-stu-id="8ec51-139">Work with the application vendor to get values that match the pattern pre-configured on Azure AD</span></span>

-   <span data-ttu-id="8ec51-140">Veya, Azure AD ekibi sizinle < aadapprequest@microsoft.com > veya uygulama için desteklenen desenleri güncelleştirmesi istemek için öğreticide bir yorum yazın</span><span class="sxs-lookup"><span data-stu-id="8ec51-140">Or, you can contact Azure AD team at <aadapprequest@microsoft.com> or leave a comment in the tutorial to request the update of the supported patterns for the application</span></span>

## <a name="where-do-i-set-the-entityid-user-identifier-format"></a><span data-ttu-id="8ec51-141">Entityıd (kullanıcı tanımlayıcısı) biçimi belirlendiği</span><span class="sxs-lookup"><span data-stu-id="8ec51-141">Where do I set the EntityID (User Identifier) format</span></span>

<span data-ttu-id="8ec51-142">Azure AD kullanıcı kimlik doğrulamasının ardından yanıt uygulamaya gönderir Entityıd (kullanıcı tanımlayıcısı) biçimi seçin mümkün olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="8ec51-142">You won’t be able to select the EntityID (User Identifier) format that Azure AD sends to the application in the response after user authentication.</span></span>

<span data-ttu-id="8ec51-143">Azure AD seçin (kullanıcı tanımlayıcısı) NameID özniteliğin biçimini değere göre seçilen veya biçimi SAML AuthRequest uygulama tarafından istenen.</span><span class="sxs-lookup"><span data-stu-id="8ec51-143">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="8ec51-144">Daha fazla bilgi için makaleyi ziyaret [tek oturum açma SAML Protokolü](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) NameIDPolicy, bölümünde</span><span class="sxs-lookup"><span data-stu-id="8ec51-144">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy,</span></span>

## <a name="cant-find-the-azure-ad-metadata-to-complete-the-configuration-with-the-application"></a><span data-ttu-id="8ec51-145">Uygulama ile yapılandırmayı tamamlamak için Azure AD meta verileri bulamıyor</span><span class="sxs-lookup"><span data-stu-id="8ec51-145">Can’t find the Azure AD metadata to complete the configuration with the application</span></span>

<span data-ttu-id="8ec51-146">Uygulama meta verileri veya sertifika Azure AD'den karşıdan yüklemek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="8ec51-146">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="8ec51-147">Açık [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="8ec51-147">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="8ec51-148">Açık **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** ana sol taraftaki gezinti menüsünde sonundaki.</span><span class="sxs-lookup"><span data-stu-id="8ec51-148">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="8ec51-149">Yazın **"Azure Active Directory**" Filtre Arama kutusuna seçip **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="8ec51-149">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="8ec51-150">tıklatın **kurumsal uygulamalar** Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="8ec51-150">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="8ec51-151">tıklatın **tüm uygulamaları** tüm uygulamaların bir listesini görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="8ec51-151">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="8ec51-152">Burada gösterisini istediğiniz uygulama görmüyorsanız kullanın **filtre** üst kısmındaki denetim **tüm uygulamalar listesini** ve **Göster** için seçenek **tüm uygulamaları.**</span><span class="sxs-lookup"><span data-stu-id="8ec51-152">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="8ec51-153">Çoklu oturum açma yapılandırdığınız uygulaması'nı seçin.</span><span class="sxs-lookup"><span data-stu-id="8ec51-153">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="8ec51-154">Uygulamanın yüklediği sonra tıklayın **çoklu oturum açma** uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="8ec51-154">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="8ec51-155">Git **SAML imzalama sertifikası** bölümünde ve ardından **karşıdan** sütun değeri.</span><span class="sxs-lookup"><span data-stu-id="8ec51-155">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="8ec51-156">Çoklu oturum açma yapılandırma hangi uygulama gerektiriyor bağlı olarak, meta veri XML yükleme seçeneği ya da sertifika bakın.</span><span class="sxs-lookup"><span data-stu-id="8ec51-156">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

<span data-ttu-id="8ec51-157">Azure AD meta verilerini almak için bir URL sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="8ec51-157">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="8ec51-158">Meta veriler yalnızca bir XML dosyası olarak alınabilir.</span><span class="sxs-lookup"><span data-stu-id="8ec51-158">The metadata can only be retrieved as a XML file.</span></span>

## <a name="dont-know-how-to-customize-saml-claims-sent-to-an-application"></a><span data-ttu-id="8ec51-159">Uygulamaya gönderilen SAML talep özelleştirmek nasıl bilinmiyor</span><span class="sxs-lookup"><span data-stu-id="8ec51-159">Don't know how to customize SAML claims sent to an application</span></span>

<span data-ttu-id="8ec51-160">Uygulamanıza gönderilen SAML öznitelik taleplerini özelleştirmek öğrenmek için bkz: [talep eşleme Azure Active Directory'de](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="8ec51-160">To learn how to customize the SAML attribute claims sent to your application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8ec51-161">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8ec51-161">Next steps</span></span>
[<span data-ttu-id="8ec51-162">Azure Active Directory ile uygulamaları yönetme</span><span class="sxs-lookup"><span data-stu-id="8ec51-162">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
