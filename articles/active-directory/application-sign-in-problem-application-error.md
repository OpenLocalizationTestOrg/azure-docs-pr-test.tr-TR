---
title: "Oturum açtıktan sonra bir uygulamanın sayfada hata | Microsoft Docs"
description: "Uygulama bir hata olduğunda yayar Azure AD oturum ile ilgili sorunları gidermek nasıl"
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
ms.openlocfilehash: a8cd93256f79ece268ec3411dfbdf590f4b24447
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="error-on-an-applications-page-after-signing-in"></a><span data-ttu-id="7f250-103">Oturum açtıktan sonra bir uygulamanın sayfada hata</span><span class="sxs-lookup"><span data-stu-id="7f250-103">Error on an application's page after signing in</span></span>

<span data-ttu-id="7f250-104">Bu senaryoda, Azure AD kullanıcı oturumu, ancak uygulama başarıyla oturum açma akışını son kullanıcıya izin hata görüntüleme.</span><span class="sxs-lookup"><span data-stu-id="7f250-104">In this scenario, Azure AD has signed the user in, but the application is displaying an error not allowing the user to successfully finish the sign in flow.</span></span> <span data-ttu-id="7f250-105">Bu senaryoda, uygulamanın yanıt sorunu Azure AD tarafından kabul etmiyor.</span><span class="sxs-lookup"><span data-stu-id="7f250-105">In this scenario, the application is not accepting the response issue by Azure AD.</span></span>

<span data-ttu-id="7f250-106">Uygulama Azure AD'den yanıt neden kabul etmediğiniz bazı olası nedenleri vardır.</span><span class="sxs-lookup"><span data-stu-id="7f250-106">There are some possible reasons why the application didn’t accept the response from Azure AD.</span></span> <span data-ttu-id="7f250-107">Uygulamada hata ne sonra yanıtta eksik olduğunu bilmeniz açık değilse:</span><span class="sxs-lookup"><span data-stu-id="7f250-107">If the error in the application is not clear enough to know what is missing in the response, then:</span></span>

-   <span data-ttu-id="7f250-108">Azure AD galeri uygulamasıysa, makaledeki tüm adımları doğrulayın [SAML tabanlı çoklu oturum açma Azure Active Directory'de uygulamalar için hata ayıklama](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging).</span><span class="sxs-lookup"><span data-stu-id="7f250-108">If the application is the Azure AD Gallery, verify you have followed all the steps in the article [How to debug SAML-based single sign-on to applications in Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging).</span></span>

-   <span data-ttu-id="7f250-109">Gibi bir araç kullanın [Fiddler](http://www.telerik.com/fiddler) SAML isteği SAML yanıtını ve SAML belirteci yakalamak için.</span><span class="sxs-lookup"><span data-stu-id="7f250-109">Use a tool like [Fiddler](http://www.telerik.com/fiddler) to capture SAML request, SAML response and SAML token.</span></span>

-   <span data-ttu-id="7f250-110">SAML yanıtını eksik biliyor için uygulama satıcısına ile paylaşır.</span><span class="sxs-lookup"><span data-stu-id="7f250-110">Share the SAML response with the application vendor to know what is missing.</span></span>

## <a name="missing-attributes-in-the-saml-response"></a><span data-ttu-id="7f250-111">SAML yanıtını eksik öznitelikleri</span><span class="sxs-lookup"><span data-stu-id="7f250-111">Missing attributes in the SAML response</span></span>

<span data-ttu-id="7f250-112">Azure AD yanıtta gönderilecek Azure AD yapılandırmasında bir öznitelik eklemek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="7f250-112">To add an attribute in the Azure AD configuration to be sent in the Azure AD response, follow the steps below:</span></span>

1.  <span data-ttu-id="7f250-113">Açık [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="7f250-113">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="7f250-114">Açık **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** ana sol taraftaki gezinti menüsünde sonundaki.</span><span class="sxs-lookup"><span data-stu-id="7f250-114">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="7f250-115">Yazın **"Azure Active Directory**" Filtre Arama kutusuna seçip **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="7f250-115">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="7f250-116">tıklatın **kurumsal uygulamalar** Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="7f250-116">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="7f250-117">tıklatın **tüm uygulamaları** tüm uygulamaların bir listesini görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="7f250-117">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="7f250-118">Burada gösterisini istediğiniz uygulama görmüyorsanız kullanın **filtre** üst kısmındaki denetim **tüm uygulamalar listesini** ve **Göster** için seçenek **tüm uygulamaları.**</span><span class="sxs-lookup"><span data-stu-id="7f250-118">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="7f250-119">Çoklu oturum açma yapılandırmak istediğiniz uygulamayı seçin.</span><span class="sxs-lookup"><span data-stu-id="7f250-119">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="7f250-120">Uygulamanın yüklediği sonra tıklayın **çoklu oturum açma** uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="7f250-120">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="7f250-121">tıklatın **görüntüleme ve düzenleme diğer tüm kullanıcı özniteliklerini altında** **kullanıcı öznitelikleri** kullanıcı oturum açtığında SAML belirteci uygulamada gönderilmesini öznitelikleri düzenlemek için bölüm.</span><span class="sxs-lookup"><span data-stu-id="7f250-121">click **View and edit all other user attributes under** the **User Attributes** section to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="7f250-122">Bir öznitelik eklemek için:</span><span class="sxs-lookup"><span data-stu-id="7f250-122">To add an attribute:</span></span>

   * <span data-ttu-id="7f250-123">tıklatın **Ekle özniteliği**.</span><span class="sxs-lookup"><span data-stu-id="7f250-123">click **Add attribute**.</span></span> <span data-ttu-id="7f250-124">Girin **adı** seçip **değeri** gelen açılır.</span><span class="sxs-lookup"><span data-stu-id="7f250-124">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   * <span data-ttu-id="7f250-125">Tıklatın **kaydedin.**</span><span class="sxs-lookup"><span data-stu-id="7f250-125">Click **Save.**</span></span> <span data-ttu-id="7f250-126">Yeni öznitelik tablosundaki bakın.</span><span class="sxs-lookup"><span data-stu-id="7f250-126">You see the new attribute in the table.</span></span>

9.  <span data-ttu-id="7f250-127">Yapılandırmayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="7f250-127">Save the configuration.</span></span>

<span data-ttu-id="7f250-128">Uygulama için kullanıcı oturum açtığında sonraki zaman Azure AD yeni öznitelik SAML yanıt olarak gönderin.</span><span class="sxs-lookup"><span data-stu-id="7f250-128">Next time the user signs in to the application, Azure AD send the new attribute in the SAML response.</span></span>

## <a name="the-application-expects-a-different-user-identifier-value-or-format"></a><span data-ttu-id="7f250-129">Farklı kullanıcı tanımlayıcısı value veya format uygulama bekliyor</span><span class="sxs-lookup"><span data-stu-id="7f250-129">The application expects a different User Identifier value or format</span></span>

<span data-ttu-id="7f250-130">Oturum açma uygulamaya SAML yanıtını rolleri gibi öznitelikleri eksik veya uygulama Entityıd özniteliği için farklı bir biçim bekleniyordu nedeniyle başarısız oluyor.</span><span class="sxs-lookup"><span data-stu-id="7f250-130">The sign-in to the application is failing because the SAML response is missing attributes such as roles or because the application is expecting a different format for the EntityID attribute.</span></span>

## <a name="add-an-attribute-in-the-azure-ad-application-configuration"></a><span data-ttu-id="7f250-131">Azure AD uygulama yapılandırmasında bir özniteliği ekleyin:</span><span class="sxs-lookup"><span data-stu-id="7f250-131">Add an attribute in the Azure AD application configuration:</span></span>

<span data-ttu-id="7f250-132">Kullanıcı tanımlayıcısı değeri değiştirmek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="7f250-132">To change the User Identifier value, follow the steps below:</span></span>

1.  <span data-ttu-id="7f250-133">Açık [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="7f250-133">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="7f250-134">Açık **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** ana sol taraftaki gezinti menüsünde sonundaki.</span><span class="sxs-lookup"><span data-stu-id="7f250-134">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="7f250-135">Yazın **"Azure Active Directory**" Filtre Arama kutusuna seçip **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="7f250-135">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="7f250-136">tıklatın **kurumsal uygulamalar** Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="7f250-136">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="7f250-137">tıklatın **tüm uygulamaları** tüm uygulamaların bir listesini görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="7f250-137">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="7f250-138">Burada gösterisini istediğiniz uygulama görmüyorsanız kullanın **filtre** üst kısmındaki denetim **tüm uygulamalar listesini** ve **Göster** için seçenek **tüm uygulamaları.**</span><span class="sxs-lookup"><span data-stu-id="7f250-138">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="7f250-139">Çoklu oturum açma yapılandırmak istediğiniz uygulamayı seçin.</span><span class="sxs-lookup"><span data-stu-id="7f250-139">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="7f250-140">Uygulamanın yüklediği sonra tıklayın **çoklu oturum açma** uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="7f250-140">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="7f250-141">Altında **kullanıcı öznitelikleri**, kullanıcılarınız için benzersiz tanımlayıcı seçin **kullanıcı tanımlayıcısı** açılır.</span><span class="sxs-lookup"><span data-stu-id="7f250-141">Under the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

## <a name="change-entityid-user-identifier-format"></a><span data-ttu-id="7f250-142">Entityıd (kullanıcı tanımlayıcısı) biçimini değiştirme</span><span class="sxs-lookup"><span data-stu-id="7f250-142">Change EntityID (User Identifier) format</span></span>

<span data-ttu-id="7f250-143">Uygulama Entityıd özniteliği için başka bir biçime görüyorsa.</span><span class="sxs-lookup"><span data-stu-id="7f250-143">If the application expects another format for the EntityID attribute.</span></span> <span data-ttu-id="7f250-144">Ardından, Azure AD kullanıcı kimlik doğrulamasının ardından yanıt uygulamaya gönderir Entityıd (kullanıcı tanımlayıcısı) biçimi seçin mümkün olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="7f250-144">Then, you won’t be able to select the EntityID (User Identifier) format that Azure AD sends to the application in the response after user authentication.</span></span>

<span data-ttu-id="7f250-145">Azure AD seçin (kullanıcı tanımlayıcısı) NameID özniteliğin biçimini değere göre seçilen veya biçimi SAML AuthRequest uygulama tarafından istenen.</span><span class="sxs-lookup"><span data-stu-id="7f250-145">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="7f250-146">Daha fazla bilgi için makaleyi ziyaret [tek oturum açma SAML Protokolü](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) NameIDPolicy bölümünde.</span><span class="sxs-lookup"><span data-stu-id="7f250-146">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>

## <a name="the-application-expects-a-different-signature-method-for-the-saml-response"></a><span data-ttu-id="7f250-147">SAML yanıtını için farklı imza yöntemi uygulama bekliyor</span><span class="sxs-lookup"><span data-stu-id="7f250-147">The application expects a different signature method for the SAML response</span></span>

<span data-ttu-id="7f250-148">SAML belirteci hangi kısımlarının Azure Active Directory tarafından dijital olarak imzalanmış değiştirmek için.</span><span class="sxs-lookup"><span data-stu-id="7f250-148">To change what parts of the SAML token are digitally signed by Azure Active Directory.</span></span> <span data-ttu-id="7f250-149">Aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="7f250-149">Follow the steps below:</span></span>

1.  <span data-ttu-id="7f250-150">Açık [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="7f250-150">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="7f250-151">Açık **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** ana sol taraftaki gezinti menüsünde sonundaki.</span><span class="sxs-lookup"><span data-stu-id="7f250-151">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="7f250-152">Yazın **"Azure Active Directory**" Filtre Arama kutusuna seçip **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="7f250-152">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="7f250-153">tıklatın **kurumsal uygulamalar** Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="7f250-153">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="7f250-154">tıklatın **tüm uygulamaları** tüm uygulamaların bir listesini görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="7f250-154">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="7f250-155">Burada gösterisini istediğiniz uygulama görmüyorsanız kullanın **filtre** üst kısmındaki denetim **tüm uygulamalar listesini** ve **Göster** için seçenek **tüm uygulamaları.**</span><span class="sxs-lookup"><span data-stu-id="7f250-155">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="7f250-156">Çoklu oturum açma yapılandırmak istediğiniz uygulamayı seçin.</span><span class="sxs-lookup"><span data-stu-id="7f250-156">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="7f250-157">Uygulamanın yüklediği sonra tıklayın **çoklu oturum açma** uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="7f250-157">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="7f250-158">tıklatın **Göster gelişmiş sertifika imzalama ayarları** altında **SAML imzalama sertifikası** bölümü.</span><span class="sxs-lookup"><span data-stu-id="7f250-158">click **Show advanced certificate signing settings** under the **SAML Signing Certificate** section.</span></span>

9.  <span data-ttu-id="7f250-159">Uygun seçin **imzalama seçeneği** uygulama tarafından beklenen:</span><span class="sxs-lookup"><span data-stu-id="7f250-159">Select the appropriate **Signing Option** expected by the application:</span></span>

  * <span data-ttu-id="7f250-160">Oturum SAML yanıtını</span><span class="sxs-lookup"><span data-stu-id="7f250-160">Sign SAML response</span></span>

  * <span data-ttu-id="7f250-161">Oturum açma SAML yanıtını ve onaylama</span><span class="sxs-lookup"><span data-stu-id="7f250-161">Sign SAML response and assertion</span></span>

  * <span data-ttu-id="7f250-162">Oturum SAML onayı</span><span class="sxs-lookup"><span data-stu-id="7f250-162">Sign SAML assertion</span></span>

<span data-ttu-id="7f250-163">Uygulama için kullanıcı oturum açtığında sonraki zaman Azure AD oturum seçili SAML yanıtını parçası.</span><span class="sxs-lookup"><span data-stu-id="7f250-163">Next time the user signs in to the application, Azure AD sign the part of the SAML response selected.</span></span>

## <a name="the-application-expects-the-signing-algorithm-to-be-sha-1"></a><span data-ttu-id="7f250-164">SHA-1 olması için imzalama algoritmasını uygulama bekliyor</span><span class="sxs-lookup"><span data-stu-id="7f250-164">The application expects the signing algorithm to be SHA-1</span></span>

<span data-ttu-id="7f250-165">Varsayılan olarak, Azure AD çoğu güvenlik algoritmasını kullanarak SAML belirteci imzalar.</span><span class="sxs-lookup"><span data-stu-id="7f250-165">By default, Azure AD signs the SAML token using the most security algorithm.</span></span> <span data-ttu-id="7f250-166">Oturum algoritması SHA-1'den değiştirilmesi uygulama tarafından gerekli kılınmadıkça hiçbir önerilmez.</span><span class="sxs-lookup"><span data-stu-id="7f250-166">Changing the sign algorithm to SHA-1 is not recommended unless required by the application.</span></span>

<span data-ttu-id="7f250-167">İmza algoritmasını değiştirmek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="7f250-167">To change the signing algorithm, follow the steps below:</span></span>

1.  <span data-ttu-id="7f250-168">Açık [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="7f250-168">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="7f250-169">Açık **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** ana sol taraftaki gezinti menüsünde sonundaki.</span><span class="sxs-lookup"><span data-stu-id="7f250-169">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="7f250-170">Yazın **"Azure Active Directory**" Filtre Arama kutusuna seçip **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="7f250-170">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="7f250-171">tıklatın **kurumsal uygulamalar** Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="7f250-171">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="7f250-172">tıklatın **tüm uygulamaları** tüm uygulamaların bir listesini görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="7f250-172">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="7f250-173">Burada gösterisini istediğiniz uygulama görmüyorsanız kullanın **filtre** üst kısmındaki denetim **tüm uygulamalar listesini** ve **Göster** için seçenek **tüm uygulamaları.**</span><span class="sxs-lookup"><span data-stu-id="7f250-173">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="7f250-174">Çoklu oturum açma yapılandırmak istediğiniz uygulamayı seçin.</span><span class="sxs-lookup"><span data-stu-id="7f250-174">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="7f250-175">Uygulamanın yüklediği sonra tıklayın **çoklu oturum açma** uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="7f250-175">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="7f250-176">tıklatın **Göster gelişmiş sertifika imzalama ayarları** altında **SAML imzalama sertifikası** bölümü.</span><span class="sxs-lookup"><span data-stu-id="7f250-176">click **Show advanced certificate signing settings** under the **SAML Signing Certificate** section.</span></span>

9.  <span data-ttu-id="7f250-177">SHA-1, seçin **imza algoritması**.</span><span class="sxs-lookup"><span data-stu-id="7f250-177">Select SHA-1, in the **Signing Algorithm**.</span></span>

<span data-ttu-id="7f250-178">Sonraki sefer uygulama için kullanıcı oturum açtığında, Azure AD'sha-1 algoritmasını kullanarak SAML belirteci oturum açın.</span><span class="sxs-lookup"><span data-stu-id="7f250-178">Next time the user signs in to the application, Azure AD sign the SAML token using SHA-1 algorithm.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7f250-179">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7f250-179">Next steps</span></span>
[<span data-ttu-id="7f250-180">SAML tabanlı çoklu oturum açma Azure Active Directory uygulamalarında hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="7f250-180">How to debug SAML-based single sign-on to applications in Azure Active Directory</span></span>](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging)
