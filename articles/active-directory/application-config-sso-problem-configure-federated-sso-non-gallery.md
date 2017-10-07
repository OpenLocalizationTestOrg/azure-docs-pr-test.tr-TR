---
title: "Federasyon tek oturum açma için Galeri olmayan uygulama yapılandırma aaaProblem | Microsoft Docs"
description: "Bazı listelenmeyen Federasyon tek oturum açma tooyour özel SAML uygulama hello Azure AD uygulama galerisinde yapılandırırken karşılaşabileceğiniz hello yaygın sorunları ele"
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
ms.openlocfilehash: 8c80f0001de01cbc9930ef0441cd804082ee8578
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="252a1-103">Federasyon tek oturum açma için Galeri olmayan uygulama yapılandırma sorunu</span><span class="sxs-lookup"><span data-stu-id="252a1-103">Problem configuring federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="252a1-104">Bir uygulama yapılandırırken bir sorunla karşılaşırsanız.</span><span class="sxs-lookup"><span data-stu-id="252a1-104">If you encounter a problem when configuring an application.</span></span> <span data-ttu-id="252a1-105">Merhaba makaledeki tüm hello adımları takip doğrulayın [hello Azure Active Directory Uygulama galerisinde olmayan tek oturum açma tooapplications yapılandırma.](https://docs.microsoft.com/azure/active-directory/active-directory-saas-custom-apps)</span><span class="sxs-lookup"><span data-stu-id="252a1-105">Verify you have followed all hello steps in hello article [Configuring single sign-on tooapplications that are not in hello Azure Active Directory application gallery.](https://docs.microsoft.com/azure/active-directory/active-directory-saas-custom-apps)</span></span>

## <a name="cant-add-another-instance-of-hello-application"></a><span data-ttu-id="252a1-106">Merhaba uygulaması başka bir örneği eklenemiyor</span><span class="sxs-lookup"><span data-stu-id="252a1-106">Can’t add another instance of hello application</span></span>

<span data-ttu-id="252a1-107">bir uygulamanın ikinci bir örneğini tooadd, toobe yapabileceksiniz da gerekir:</span><span class="sxs-lookup"><span data-stu-id="252a1-107">tooadd a second instance of an application, you need toobe able to:</span></span>

-   <span data-ttu-id="252a1-108">Merhaba ikinci örneği için benzersiz bir tanımlayıcı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="252a1-108">Configure a unique identifier for hello second instance.</span></span> <span data-ttu-id="252a1-109">Merhaba ilk örnek için kullanılan aynı tanımlayıcısı mümkün tooconfigure hello olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="252a1-109">You won’t be able tooconfigure hello same identifier used for hello first instance.</span></span>

-   <span data-ttu-id="252a1-110">Merhaba hello ilk örnek için kullanılan daha farklı bir sertifika yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="252a1-110">Configure a different certificate than hello one used for hello first instance.</span></span>

<span data-ttu-id="252a1-111">Merhaba, uygulama hello yukarıdaki hiçbirini desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="252a1-111">If hello application doesn’t support any of hello above.</span></span> <span data-ttu-id="252a1-112">Ardından, mümkün tooconfigure ikinci bir örneğini olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="252a1-112">Then, you won’t be able tooconfigure a second instance.</span></span>

## <a name="where-do-i-set-hello-entityid-user-identifier-format"></a><span data-ttu-id="252a1-113">Merhaba Entityıd (kullanıcı tanımlayıcısı) biçimi belirlendiği</span><span class="sxs-lookup"><span data-stu-id="252a1-113">Where do I set hello EntityID (User Identifier) format</span></span>

<span data-ttu-id="252a1-114">Azure AD hello yanıtta toohello uygulama kullanıcı kimlik doğrulamasından sonra gönderir mümkün tooselect hello Entityıd (kullanıcı tanımlayıcısı) biçimi olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="252a1-114">You won’t be able tooselect hello EntityID (User Identifier) format that Azure AD sends toohello application in hello response after user authentication.</span></span>

<span data-ttu-id="252a1-115">Merhaba NameID özniteliği (kullanıcı tanımlayıcısı) için Azure AD select hello biçimi seçili hello değere göre veya hello SAML AuthRequest hello uygulama tarafından istenen biçim hello.</span><span class="sxs-lookup"><span data-stu-id="252a1-115">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="252a1-116">Daha fazla bilgi için hello makale ziyaret [tek oturum açma SAML Protokolü](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) NameIDPolicy, hello bölümünde</span><span class="sxs-lookup"><span data-stu-id="252a1-116">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy,</span></span>

## <a name="where-do-i-get-hello-application-metadata-or-certificate-from-azure-ad"></a><span data-ttu-id="252a1-117">Merhaba uygulama meta verileri veya sertifika Azure AD'den nereden bulabilirim</span><span class="sxs-lookup"><span data-stu-id="252a1-117">Where do I get hello application metadata or certificate from Azure AD</span></span>

<span data-ttu-id="252a1-118">toodownload hello uygulama meta verileri veya sertifika Azure AD'den hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="252a1-118">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="252a1-119">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="252a1-119">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="252a1-120">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="252a1-120">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="252a1-121">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="252a1-121">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="252a1-122">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="252a1-122">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="252a1-123">Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.</span><span class="sxs-lookup"><span data-stu-id="252a1-123">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="252a1-124">Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**</span><span class="sxs-lookup"><span data-stu-id="252a1-124">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="252a1-125">Çoklu oturum açma yapılandırdığınız hello uygulaması'nı seçin.</span><span class="sxs-lookup"><span data-stu-id="252a1-125">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="252a1-126">Merhaba uygulamanın yüklediği sonra hello tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="252a1-126">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="252a1-127">Çok Git**SAML imzalama sertifikası** bölümünde ve ardından **karşıdan** sütun değeri.</span><span class="sxs-lookup"><span data-stu-id="252a1-127">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="252a1-128">Çoklu oturum açma yapılandırma hangi hello uygulama gerektirir bağlı olarak, meta veri XML hello veya sertifika hello ya da hello seçeneği toodownload bakın.</span><span class="sxs-lookup"><span data-stu-id="252a1-128">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

<span data-ttu-id="252a1-129">Azure AD, URL tooget hello meta verilerinin sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="252a1-129">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="252a1-130">Merhaba meta veriler yalnızca bir XML dosyası olarak alınabilir.</span><span class="sxs-lookup"><span data-stu-id="252a1-130">hello metadata can only be retrieved as a XML file.</span></span>

## <a name="dont-know-how-toocustomize-saml-claims-sent-tooan-application"></a><span data-ttu-id="252a1-131">Toocustomize SAML talep tooan uygulama nasıl gönderileceğini bilmiyorsanız</span><span class="sxs-lookup"><span data-stu-id="252a1-131">Don't know how toocustomize SAML claims sent tooan application</span></span>

<span data-ttu-id="252a1-132">toolearn tooyour uygulama toocustomize hello SAML öznitelik taleplerini gönderilen nasıl bkz [talep eşleme Azure Active Directory'de](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="252a1-132">toolearn how toocustomize hello SAML attribute claims sent tooyour application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="252a1-133">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="252a1-133">Next steps</span></span>
[<span data-ttu-id="252a1-134">Azure Active Directory ile uygulamaları yönetme</span><span class="sxs-lookup"><span data-stu-id="252a1-134">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
