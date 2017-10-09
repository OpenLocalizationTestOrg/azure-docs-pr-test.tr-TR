---
title: "Öğretici: Azure Active Directory Tümleştirme Amazon Web Hizmetleri (AWS) ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve Amazon Web Hizmetleri (AWS) arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7561c20b-2325-4d97-887f-693aa383c7be
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 1b79572ace63f6174ce4fa014c49bf44bd728228
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-amazon-web-services-aws"></a><span data-ttu-id="09a50-103">Öğretici: Azure Active Directory Tümleştirme Amazon Web Hizmetleri (AWS)</span><span class="sxs-lookup"><span data-stu-id="09a50-103">Tutorial: Azure Active Directory integration with Amazon Web Services (AWS)</span></span>

<span data-ttu-id="09a50-104">Bu öğreticide, bilgi nasıl toointegrate Azure Active Directory (Azure AD) ile Amazon Web Hizmetleri (AWS).</span><span class="sxs-lookup"><span data-stu-id="09a50-104">In this tutorial, you learn how toointegrate Amazon Web Services (AWS) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="09a50-105">Amazon Web Hizmetleri (AWS) Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="09a50-105">Integrating Amazon Web Services (AWS) with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="09a50-106">Erişim tooAmazon Web Hizmetleri (AWS) sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="09a50-106">You can control in Azure AD who has access tooAmazon Web Services (AWS)</span></span>
- <span data-ttu-id="09a50-107">Azure AD hesaplarına ile kullanıcılar tooautomatically get açan tooAmazon (çoklu oturum açma) Web Hizmetleri (AWS) etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="09a50-107">You can enable your users tooautomatically get signed-on tooAmazon Web Services (AWS) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="09a50-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="09a50-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="09a50-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="09a50-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

tooenable single sign-on with Amazon Web Services (AWS), it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Amazon Web Services (AWS).

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="09a50-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="09a50-110">Prerequisites</span></span>

<span data-ttu-id="09a50-111">Azure AD tümleştirme Amazon Web Hizmetleri (AWS) ile tooconfigure, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="09a50-111">tooconfigure Azure AD integration with Amazon Web Services (AWS), you need hello following items:</span></span>

- <span data-ttu-id="09a50-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="09a50-112">An Azure AD subscription</span></span>
- <span data-ttu-id="09a50-113">Amazon Web Hizmetleri (AWS) çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="09a50-113">Amazon Web Services (AWS) single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="09a50-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="09a50-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="09a50-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="09a50-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="09a50-116">Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="09a50-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="09a50-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="09a50-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="09a50-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="09a50-118">Scenario description</span></span>
<span data-ttu-id="09a50-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="09a50-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="09a50-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="09a50-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="09a50-121">Amazon Web Hizmetleri (AWS) hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="09a50-121">Adding Amazon Web Services (AWS) from hello gallery</span></span>
2. <span data-ttu-id="09a50-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="09a50-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-amazon-web-services-aws-from-hello-gallery"></a><span data-ttu-id="09a50-123">Amazon Web Hizmetleri (AWS) hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="09a50-123">Adding Amazon Web Services (AWS) from hello gallery</span></span>
<span data-ttu-id="09a50-124">tooconfigure hello tümleştirmeye Amazon Web Hizmetleri (AWS) Azure AD, hello galeri tooyour yönetilen SaaS uygulamaları listesinden tooadd Amazon Web Hizmetleri (AWS) gerekir.</span><span class="sxs-lookup"><span data-stu-id="09a50-124">tooconfigure hello integration of Amazon Web Services (AWS) into Azure AD, you need tooadd Amazon Web Services (AWS) from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="09a50-125">**tooadd hello galerisinden Amazon Web Hizmetleri (AWS) hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="09a50-125">**tooadd Amazon Web Services (AWS) from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="09a50-126">Merhaba,  **[Azure Portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="09a50-126">In hello **[Azure Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="09a50-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="09a50-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="09a50-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="09a50-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="09a50-131">Tıklatın **Ekle** hello iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="09a50-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="09a50-133">Merhaba arama kutusuna yazın **Amazon Web Hizmetleri (AWS)**.</span><span class="sxs-lookup"><span data-stu-id="09a50-133">In hello search box, type **Amazon Web Services (AWS)**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_search.png)

5. <span data-ttu-id="09a50-135">Merhaba Sonuçlar panelinde seçin **Amazon Web Hizmetleri (AWS)**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="09a50-135">In hello results panel, select **Amazon Web Services (AWS)**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="09a50-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="09a50-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="09a50-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma ile Amazon Web Hizmetleri ("Britta Simon" adlı bir test kullanıcı tabanlı AWS) test etme.</span><span class="sxs-lookup"><span data-stu-id="09a50-138">In this section, you configure and test Azure AD single sign-on with Amazon Web Services (AWS) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="09a50-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Amazon Web Hizmetleri (AWS) tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="09a50-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Amazon Web Services (AWS) is tooa user in Azure AD.</span></span> <span data-ttu-id="09a50-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve hello ilgili kullanıcı Amazon Web Hizmetleri (AWS) arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="09a50-140">In other words, a link relationship between an Azure AD user and hello related user in Amazon Web Services (AWS) needs toobe established.</span></span>

<span data-ttu-id="09a50-141">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** Amazon Web Hizmetleri (AWS).</span><span class="sxs-lookup"><span data-stu-id="09a50-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Amazon Web Services (AWS).</span></span>

<span data-ttu-id="09a50-142">tooconfigure ve test Amazon Web Hizmetleri (AWS) ile Azure AD çoklu oturum açma, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="09a50-142">tooconfigure and test Azure AD single sign-on with Amazon Web Services (AWS), you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="09a50-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="09a50-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="09a50-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="09a50-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="09a50-145">**[Amazon Web Hizmetleri test kullanıcısı oluşturma](#creating-an-amazon-web-services-test-user)**  -toohave karşılık gelen, Britta Simon Amazon Web Hizmetleri (AWS) her bağlantılı toohello Azure AD gösterimidir.</span><span class="sxs-lookup"><span data-stu-id="09a50-145">**[Creating an Amazon Web Services test user](#creating-an-amazon-web-services-test-user)** - toohave a counterpart of Britta Simon in Amazon Web Services (AWS) that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="09a50-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="09a50-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="09a50-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="09a50-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="09a50-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="09a50-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="09a50-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma, Amazon Web Hizmetleri (AWS) uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="09a50-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Amazon Web Services (AWS) application.</span></span>

<span data-ttu-id="09a50-150">**Amazon Web Hizmetleri (AWS) ile tooconfigure Azure AD çoklu oturum açma hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="09a50-150">**tooconfigure Azure AD single sign-on with Amazon Web Services (AWS), perform hello following steps:**</span></span>

1. <span data-ttu-id="09a50-151">Hello üzerinde hello Azure Portal'ın **Amazon Web Hizmetleri (AWS)** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="09a50-151">In hello Azure Portal, on hello **Amazon Web Services (AWS)** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="09a50-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda, olarak **modu** seçin **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="09a50-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_samlbase.png)

3. <span data-ttu-id="09a50-155">Merhaba üzerinde **Amazon Web Hizmetleri (AWS) etki alanı ve URL'leri** bölümünde, hello uygulama zaten Azure ile önceden tümleştirilmiş gibi hello kullanıcının tooperform herhangi bir adımı yok.</span><span class="sxs-lookup"><span data-stu-id="09a50-155">On hello **Amazon Web Services (AWS) Domain and URLs** section, hello user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_url.png)

4. <span data-ttu-id="09a50-157">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello XML dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="09a50-157">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_certificate.png)

5. <span data-ttu-id="09a50-159">Merhaba Amazon Web Hizmetleri (AWS) yazılım uygulaması hello SAML onaylar belirli bir biçimde bekliyor.</span><span class="sxs-lookup"><span data-stu-id="09a50-159">hello Amazon Web Services (AWS) Software application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="09a50-160">Lütfen bu uygulama için talep aşağıdaki hello yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="09a50-160">Please configure hello following claims for this application.</span></span> <span data-ttu-id="09a50-161">Hello başlangıç değerleri bu özniteliklerin yönetebilirsiniz "**kullanıcı öznitelikleri**" uygulama tümleştirmesi sayfasında bölüm.</span><span class="sxs-lookup"><span data-stu-id="09a50-161">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="09a50-162">Ekran aşağıdaki hello bunun bir örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="09a50-162">hello following screenshot shows an example for this.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_attribute.png)

6. <span data-ttu-id="09a50-164">Merhaba, **kullanıcı öznitelikleri** hello bölüm **çoklu oturum açma** iletişim kutusunda, SAML belirteci özniteliği yukarıdaki hello resimde gösterildiği gibi yapılandırmak ve hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="09a50-164">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="09a50-165">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="09a50-165">Attribute Name</span></span>  | <span data-ttu-id="09a50-166">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="09a50-166">Attribute Value</span></span> | <span data-ttu-id="09a50-167">Namespace</span><span class="sxs-lookup"><span data-stu-id="09a50-167">Namespace</span></span> |
    | --------------- | --------------- | --------------- |
    | <span data-ttu-id="09a50-168">RoleSessionName</span><span class="sxs-lookup"><span data-stu-id="09a50-168">RoleSessionName</span></span> | <span data-ttu-id="09a50-169">User.userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="09a50-169">user.userprincipalname</span></span> | <span data-ttu-id="09a50-170">https://aws.Amazon.com/SAML/Attributes</span><span class="sxs-lookup"><span data-stu-id="09a50-170">https://aws.amazon.com/SAML/Attributes</span></span> |
    | <span data-ttu-id="09a50-171">Rol</span><span class="sxs-lookup"><span data-stu-id="09a50-171">Role</span></span>            | <span data-ttu-id="09a50-172">User.assignedroles</span><span class="sxs-lookup"><span data-stu-id="09a50-172">user.assignedroles</span></span> |  <span data-ttu-id="09a50-173">https://aws.Amazon.com/SAML/Attributes</span><span class="sxs-lookup"><span data-stu-id="09a50-173">https://aws.amazon.com/SAML/Attributes</span></span> |
    
    >[!TIP]
    ><span data-ttu-id="09a50-174">Azure AD toofetch AWS Konsolu tüm hello rollerden sağlama tooconfigure hello kullanıcı gerekir.</span><span class="sxs-lookup"><span data-stu-id="09a50-174">You need tooconfigure hello user provisioning in Azure AD toofetch all hello roles from AWS Console.</span></span> <span data-ttu-id="09a50-175">Lütfen aşağıdaki adımları sağlama hello bakın.</span><span class="sxs-lookup"><span data-stu-id="09a50-175">Please refer hello provisioning steps below.</span></span>

    <span data-ttu-id="09a50-176">a.</span><span class="sxs-lookup"><span data-stu-id="09a50-176">a.</span></span> <span data-ttu-id="09a50-177">Tıklatın **Ekle özniteliği** tooopen hello **özniteliği eklemek** iletişim.</span><span class="sxs-lookup"><span data-stu-id="09a50-177">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="09a50-179">b.</span><span class="sxs-lookup"><span data-stu-id="09a50-179">b.</span></span> <span data-ttu-id="09a50-180">Merhaba, **adı** metin kutusuna, ilgili satır için gösterilen türü hello öznitelik adı.</span><span class="sxs-lookup"><span data-stu-id="09a50-180">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="09a50-182">c.</span><span class="sxs-lookup"><span data-stu-id="09a50-182">c.</span></span> <span data-ttu-id="09a50-183">Merhaba gelen **değeri** listesinde, ilgili satır için gösterilen türü hello öznitelik değeri.</span><span class="sxs-lookup"><span data-stu-id="09a50-183">From hello **Value** list, type hello attribute value shown for that row.</span></span> <span data-ttu-id="09a50-184">Yukarıda verilen Hello Namespace değerini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="09a50-184">Add hello Namespace value as given above.</span></span>
    
    <span data-ttu-id="09a50-185">d.</span><span class="sxs-lookup"><span data-stu-id="09a50-185">d.</span></span> <span data-ttu-id="09a50-186">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="09a50-186">Click **Ok**.</span></span>

7. <span data-ttu-id="09a50-187">Tıklatın **kaydetmek** düğmesini Azure toosave hello ayarları.</span><span class="sxs-lookup"><span data-stu-id="09a50-187">Click **Save** button toosave hello settings on Azure.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="09a50-189">Farklı bir tarayıcı penceresinde yönetici olarak oturum açma tooyour Amazon Web Hizmetleri (AWS) şirket site.</span><span class="sxs-lookup"><span data-stu-id="09a50-189">In a different browser window, sign-on tooyour Amazon Web Services (AWS) company site as administrator.</span></span>

9. <span data-ttu-id="09a50-190">Tıklatın **konsol giriş**.</span><span class="sxs-lookup"><span data-stu-id="09a50-190">Click **Console Home**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın][11]

10. <span data-ttu-id="09a50-192">Tıklatın **IAM** gelen **güvenlik, Identity & Uyumluluk** hizmet.</span><span class="sxs-lookup"><span data-stu-id="09a50-192">Click **IAM** from **Security, Identity & Compliance** service.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın][12]

11. <span data-ttu-id="09a50-194">Tıklatın **kimlik sağlayıcıları**ve ardından **oluşturma sağlayıcısı**.</span><span class="sxs-lookup"><span data-stu-id="09a50-194">Click **Identity Providers**, and then click **Create Provider**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın][13]

12. <span data-ttu-id="09a50-196">Merhaba üzerinde **yapılandırma sağlayıcısı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="09a50-196">On hello **Configure Provider** dialog page, perform hello following steps:</span></span>
   
    ![Çoklu oturum açmayı yapılandırın][14]
 
    <span data-ttu-id="09a50-198">a.</span><span class="sxs-lookup"><span data-stu-id="09a50-198">a.</span></span> <span data-ttu-id="09a50-199">Olarak **sağlayıcı türü**seçin **SAML**.</span><span class="sxs-lookup"><span data-stu-id="09a50-199">As **Provider Type**, select **SAML**.</span></span>

    <span data-ttu-id="09a50-200">b.</span><span class="sxs-lookup"><span data-stu-id="09a50-200">b.</span></span> <span data-ttu-id="09a50-201">Merhaba, **sağlayıcı adı** metin kutusuna, bir sağlayıcı adı yazın (örneğin: *WAAD*).</span><span class="sxs-lookup"><span data-stu-id="09a50-201">In hello **Provider Name** textbox, type a provider name (e.g.: *WAAD*).</span></span>

    <span data-ttu-id="09a50-202">c.</span><span class="sxs-lookup"><span data-stu-id="09a50-202">c.</span></span> <span data-ttu-id="09a50-203">tooupload, indirilen meta veri dosyası tıklatın **Dosya Seç**.</span><span class="sxs-lookup"><span data-stu-id="09a50-203">tooupload your downloaded metadata file, click **Choose File**.</span></span>

    <span data-ttu-id="09a50-204">d.</span><span class="sxs-lookup"><span data-stu-id="09a50-204">d.</span></span> <span data-ttu-id="09a50-205">Tıklatın **sonraki adım**.</span><span class="sxs-lookup"><span data-stu-id="09a50-205">Click **Next Step**.</span></span>

13. <span data-ttu-id="09a50-206">Merhaba üzerinde **sağlayıcısı bilgilerini doğrulayın** iletişim sayfasında, tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="09a50-206">On hello **Verify Provider Information** dialog page, click **Create**.</span></span> 
    
    ![Çoklu oturum açmayı yapılandırın][15]

14. <span data-ttu-id="09a50-208">Tıklatın **rolleri**ve ardından **yeni rol oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="09a50-208">Click **Roles**, and then click **Create New Role**.</span></span> 
    
    ![Çoklu oturum açmayı yapılandırın][16]

15. <span data-ttu-id="09a50-210">Merhaba üzerinde **ayarlamak rol adı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="09a50-210">On hello **Set Role Name** dialog, perform hello following steps:</span></span> 
    
    ![Çoklu oturum açmayı yapılandırın][17] 

    <span data-ttu-id="09a50-212">a.</span><span class="sxs-lookup"><span data-stu-id="09a50-212">a.</span></span> <span data-ttu-id="09a50-213">Merhaba, **rol adı** metin kutusuna, bir rol adı yazın (örneğin: *TestUser*).</span><span class="sxs-lookup"><span data-stu-id="09a50-213">In hello **Role Name** textbox, type a role name (e.g.: *TestUser*).</span></span> 

    <span data-ttu-id="09a50-214">b.</span><span class="sxs-lookup"><span data-stu-id="09a50-214">b.</span></span> <span data-ttu-id="09a50-215">Tıklatın **sonraki adım**.</span><span class="sxs-lookup"><span data-stu-id="09a50-215">Click **Next Step**.</span></span>

16. <span data-ttu-id="09a50-216">Merhaba üzerinde **rol türünü seç** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="09a50-216">On hello **Select Role Type** dialog, perform hello following steps:</span></span> 
    
    ![Çoklu oturum açmayı yapılandırın][18] 

    <span data-ttu-id="09a50-218">a.</span><span class="sxs-lookup"><span data-stu-id="09a50-218">a.</span></span> <span data-ttu-id="09a50-219">Seçin **kimlik sağlayıcısı erişim için rol**.</span><span class="sxs-lookup"><span data-stu-id="09a50-219">Select **Role For Identity Provider Access**.</span></span> 

    <span data-ttu-id="09a50-220">b.</span><span class="sxs-lookup"><span data-stu-id="09a50-220">b.</span></span> <span data-ttu-id="09a50-221">Merhaba, **Grant Web çoklu oturum açma (WebSSO) erişim tooSAML sağlayıcıları** 'yi tıklatın **seçin**.</span><span class="sxs-lookup"><span data-stu-id="09a50-221">In hello **Grant Web Single Sign-On (WebSSO) access tooSAML providers** section, click **Select**.</span></span>

17. <span data-ttu-id="09a50-222">Merhaba üzerinde **kurmak güven** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="09a50-222">On hello **Establish Trust** dialog, perform hello following steps:</span></span>  
    
    ![Çoklu oturum açmayı yapılandırın][19] 

    <span data-ttu-id="09a50-224">a.</span><span class="sxs-lookup"><span data-stu-id="09a50-224">a.</span></span> <span data-ttu-id="09a50-225">SAML sağlayıcısı, daha önce oluşturmuş hello SAML sağlayıcısını seçin (örneğin: *WAAD*)</span><span class="sxs-lookup"><span data-stu-id="09a50-225">As SAML provider, select hello SAML provider you have created previously (e.g.: *WAAD*)</span></span>
  
    <span data-ttu-id="09a50-226">b.</span><span class="sxs-lookup"><span data-stu-id="09a50-226">b.</span></span> <span data-ttu-id="09a50-227">Tıklatın **sonraki adım**.</span><span class="sxs-lookup"><span data-stu-id="09a50-227">Click **Next Step**.</span></span>

18. <span data-ttu-id="09a50-228">Merhaba üzerinde **doğrulayın rol güven** iletişim kutusunda, tıklatın **sonraki adım**.</span><span class="sxs-lookup"><span data-stu-id="09a50-228">On hello **Verify Role Trust** dialog, click **Next Step**.</span></span>
    
    ![Çoklu oturum açmayı yapılandırın][32]

19. <span data-ttu-id="09a50-230">Merhaba üzerinde **ekleme İlkesi** iletişim kutusunda, tıklatın **sonraki adım**.</span><span class="sxs-lookup"><span data-stu-id="09a50-230">On hello **Attach Policy** dialog, click **Next Step**.</span></span>
    
    ![Çoklu oturum açmayı yapılandırın][33]

20. <span data-ttu-id="09a50-232">Merhaba üzerinde **gözden geçirme** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="09a50-232">On hello **Review** dialog, perform hello following steps:</span></span>
    
    ![Çoklu oturum açmayı yapılandırın][34]
 
    <span data-ttu-id="09a50-234">a.</span><span class="sxs-lookup"><span data-stu-id="09a50-234">a.</span></span> <span data-ttu-id="09a50-235">Tıklatın **rolü oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="09a50-235">Click **Create Role**.</span></span>

    <span data-ttu-id="09a50-236">b.</span><span class="sxs-lookup"><span data-stu-id="09a50-236">b.</span></span> <span data-ttu-id="09a50-237">Gerektiğinde kadar rolleri oluşturun ve bunları toohello kimlik sağlayıcısı eşleyin.</span><span class="sxs-lookup"><span data-stu-id="09a50-237">Create as many roles as needed and map them toohello Identity Provider.</span></span>

21. <span data-ttu-id="09a50-238">Şimdi hello kullanıcı toofetch hazırlama AWS tüm hello rollerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="09a50-238">Now configure hello user provisioning toofetch all hello roles from AWS</span></span>

    <span data-ttu-id="09a50-239">a.</span><span class="sxs-lookup"><span data-stu-id="09a50-239">a.</span></span> <span data-ttu-id="09a50-240">Kök hesabınızla Hello AWS konsol oturum açma</span><span class="sxs-lookup"><span data-stu-id="09a50-240">In hello AWS Console login with your root account</span></span>

    <span data-ttu-id="09a50-241">b.</span><span class="sxs-lookup"><span data-stu-id="09a50-241">b.</span></span> <span data-ttu-id="09a50-242">Merhaba sağ üst köşedeki adınıza tıklayın ve ardından hello tıklayın **My güvenlik kimlik bilgileri** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="09a50-242">In hello top right corner click your name and then click hello **My Security Credentials** option.</span></span> <span data-ttu-id="09a50-243">Bu ekran yukarı bir uyarı iletisi açar.</span><span class="sxs-lookup"><span data-stu-id="09a50-243">This will open up a screen as a warning message.</span></span> <span data-ttu-id="09a50-244">Merhaba düğmesini **güvenlik kimlik bilgileri** düğmesini toopass Merhaba ekranında.</span><span class="sxs-lookup"><span data-stu-id="09a50-244">Click hello button **Security Credentials** button toopass hello screen.</span></span>
        
       ![Çoklu oturum açmayı yapılandırın][36]

       ![Çoklu oturum açmayı yapılandırın][37]

    <span data-ttu-id="09a50-247">c.</span><span class="sxs-lookup"><span data-stu-id="09a50-247">c.</span></span> <span data-ttu-id="09a50-248">Merhaba erişim tuşları bölümüne tıklatın hello **yeni erişim anahtarı oluştur** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="09a50-248">In hello Access Keys section click hello **Create New Access Key** button.</span></span> <span data-ttu-id="09a50-249">Bu, hello erişim anahtarı kimliği ve bir belirteç değeri oluşturur.</span><span class="sxs-lookup"><span data-stu-id="09a50-249">This generates hello Access Key ID and a token value.</span></span>
    
       ![Çoklu oturum açmayı yapılandırın][38]

    <span data-ttu-id="09a50-251">d.</span><span class="sxs-lookup"><span data-stu-id="09a50-251">d.</span></span> <span data-ttu-id="09a50-252">Bu değerleri kopyalayın ve böylece bu kaybetmeyin Ayrıca, indirin.</span><span class="sxs-lookup"><span data-stu-id="09a50-252">Copy both these values and also download it, so that you don't lose it.</span></span>

    <span data-ttu-id="09a50-253">e.</span><span class="sxs-lookup"><span data-stu-id="09a50-253">e.</span></span> <span data-ttu-id="09a50-254">Merhaba Amazon Web Hizmetleri (AWS) uygulama tümleştirmesi sayfasında hello Azure Portal'ı tıklatın **sağlama**.</span><span class="sxs-lookup"><span data-stu-id="09a50-254">In hello Azure Portal, on hello Amazon Web Services (AWS) application integration page, click **Provisioning**.</span></span>
        
       ![Çoklu oturum açmayı yapılandırın][35]

    <span data-ttu-id="09a50-256">f.</span><span class="sxs-lookup"><span data-stu-id="09a50-256">f.</span></span> <span data-ttu-id="09a50-257">Merhaba hazırlama modunu çok ayarlamak**otomatik**</span><span class="sxs-lookup"><span data-stu-id="09a50-257">Set hello Provisioning mode too**Automatic**</span></span>
        
       ![Çoklu oturum açmayı yapılandırın][39]

    <span data-ttu-id="09a50-259">g.</span><span class="sxs-lookup"><span data-stu-id="09a50-259">g.</span></span> <span data-ttu-id="09a50-260">Merhaba, şimdi **clientsecret** ve **gizli belirteci** AWS konsolundan kopyaladığınız hello karşılık gelen değerler yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="09a50-260">Now in hello **clientsecret** and **Secret Token** paste hello corresponding values, which you have copied from AWS Console.</span></span>
    
    <span data-ttu-id="09a50-261">h.</span><span class="sxs-lookup"><span data-stu-id="09a50-261">h.</span></span> <span data-ttu-id="09a50-262">Merhaba tıklayabilirsiniz **Bağlantıyı Sına** düğmesini tootest hello bağlantısı.</span><span class="sxs-lookup"><span data-stu-id="09a50-262">You can click hello **Test Connection** button tootest hello connectivity.</span></span> <span data-ttu-id="09a50-263">Başarılı olduktan sonra Bağlayıcıyı sağlamadan hello başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="09a50-263">Once that is successful then you can start hello provisioning connector.</span></span>
       
       ![Çoklu oturum açmayı yapılandırın][40]

    <span data-ttu-id="09a50-265">ı.</span><span class="sxs-lookup"><span data-stu-id="09a50-265">i.</span></span> <span data-ttu-id="09a50-266">Şimdi hello sağlama durumu çok etkinleştirmek**üzerinde**.</span><span class="sxs-lookup"><span data-stu-id="09a50-266">Now enable hello Provisioning Status too**On**.</span></span> <span data-ttu-id="09a50-267">Bu, hello uygulamadan hello rolleri getiriliyor başlatır.</span><span class="sxs-lookup"><span data-stu-id="09a50-267">This starts fetching hello roles from hello application.</span></span>

       ![Çoklu oturum açmayı yapılandırın][41]

    > [!NOTE]
    > <span data-ttu-id="09a50-269">Azure AD sağlama hizmeti çalıştığında AWS bazı zaman toosync hello rollerden sonra her.</span><span class="sxs-lookup"><span data-stu-id="09a50-269">Azure AD Provisioning service runs every after some time toosync hello roles from AWS.</span></span> <span data-ttu-id="09a50-270">Tüm hello kimlik sağlayıcısı AWS rolleri Azure AD ile bağlı ve hello uygulama toousers ya da grupları atarken kullanabilmek için görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="09a50-270">You should see all hello Identity Provider attached AWS roles into Azure AD and you can use them while assigning hello application toousers or groups.</span></span>

<!--### Next steps

tooensure users can sign-in tooAmazon Web Services (AWS) after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Amazon Web Services (AWS) prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooAmazon Web Services (AWS) in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Amazon Web Services (AWS) users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="09a50-271">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="09a50-271">Creating an Azure AD test user</span></span>
<span data-ttu-id="09a50-272">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="09a50-272">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="09a50-274">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="09a50-274">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="09a50-275">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="09a50-275">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="09a50-277">Çok Git**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar** toodisplay hello kullanıcılar listesi.</span><span class="sxs-lookup"><span data-stu-id="09a50-277">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="09a50-279">Merhaba hello iletişim üstündeki **Ekle** tooopen hello **kullanıcı** iletişim.</span><span class="sxs-lookup"><span data-stu-id="09a50-279">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="09a50-281">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="09a50-281">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="09a50-283">a.</span><span class="sxs-lookup"><span data-stu-id="09a50-283">a.</span></span> <span data-ttu-id="09a50-284">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="09a50-284">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="09a50-285">b.</span><span class="sxs-lookup"><span data-stu-id="09a50-285">b.</span></span> <span data-ttu-id="09a50-286">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="09a50-286">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="09a50-287">c.</span><span class="sxs-lookup"><span data-stu-id="09a50-287">c.</span></span> <span data-ttu-id="09a50-288">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="09a50-288">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="09a50-289">d.</span><span class="sxs-lookup"><span data-stu-id="09a50-289">d.</span></span> <span data-ttu-id="09a50-290">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="09a50-290">Click **Create**.</span></span>
 
### <a name="creating-an-amazon-web-services-test-user"></a><span data-ttu-id="09a50-291">Amazon Web Hizmetleri test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="09a50-291">Creating an Amazon Web Services test user</span></span>

<span data-ttu-id="09a50-292">TooAmazon Web Hizmetleri (AWS) içinde sipariş tooenable Azure AD kullanıcıların toolog bunlar Amazon Web Hizmetleri (AWS) içine sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="09a50-292">In order tooenable Azure AD users toolog in tooAmazon Web Services (AWS), they must be provisioned into Amazon Web Services (AWS).</span></span> <span data-ttu-id="09a50-293">Merhaba durumda Amazon Web Hizmetleri (AWS), sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="09a50-293">In hello case of Amazon Web Services (AWS), provisioning is a manual task.</span></span>

<span data-ttu-id="09a50-294">**bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="09a50-294">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="09a50-295">İçinde tooyour oturum **Amazon Web Hizmetleri (AWS)** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="09a50-295">Log in tooyour **Amazon Web Services (AWS)** company site as administrator.</span></span>

2. <span data-ttu-id="09a50-296">Merhaba tıklatın **konsol giriş** simgesi.</span><span class="sxs-lookup"><span data-stu-id="09a50-296">Click hello **Console Home** icon.</span></span> 
   
    ![Çoklu oturum açmayı yapılandırın][11]

3. <span data-ttu-id="09a50-298">Kimlik'i tıklatın ve erişim yönetimi.</span><span class="sxs-lookup"><span data-stu-id="09a50-298">Click Identity and Access Management.</span></span> 
   
    ![Çoklu oturum açmayı yapılandırın][28]

4. <span data-ttu-id="09a50-300">Hello Pano, tıklatın **kullanıcılar**ve ardından **Create New Users**.</span><span class="sxs-lookup"><span data-stu-id="09a50-300">In hello Dashboard, click **Users**, and then click **Create New Users**.</span></span> 
   
    ![Çoklu oturum açmayı yapılandırın][29]

5. <span data-ttu-id="09a50-302">Merhaba kullanıcı oluştur iletişim kutusunda hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="09a50-302">On hello Create User dialog, perform hello following steps:</span></span> 
   
    ![Çoklu oturum açmayı yapılandırın][30]   
    
    <span data-ttu-id="09a50-304">a.</span><span class="sxs-lookup"><span data-stu-id="09a50-304">a.</span></span> <span data-ttu-id="09a50-305">Merhaba, **kullanıcı adlarını girin** metin kutuları, Azure AD'de Brita Simon'ın kullanıcı adı (userprincipalname) yazın.</span><span class="sxs-lookup"><span data-stu-id="09a50-305">In hello **Enter User Names** textboxes, type Brita Simon's user name (userprincipalname) in Azure AD.</span></span>

    <span data-ttu-id="09a50-306">b.</span><span class="sxs-lookup"><span data-stu-id="09a50-306">b.</span></span> <span data-ttu-id="09a50-307">Tıklatın **oluşturun.**</span><span class="sxs-lookup"><span data-stu-id="09a50-307">Click **Create.**</span></span>
        
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="09a50-308">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="09a50-308">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="09a50-309">Bu bölümde, kendi erişim tooAmazon Web Hizmetleri (AWS) vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="09a50-309">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooAmazon Web Services (AWS).</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="09a50-311">**tooassign Britta Simon tooAmazon Web Hizmetleri (AWS), hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="09a50-311">**tooassign Britta Simon tooAmazon Web Services (AWS), perform hello following steps:**</span></span>

1. <span data-ttu-id="09a50-312">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="09a50-312">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="09a50-314">Merhaba uygulamalar listesinde **Amazon Web Hizmetleri (AWS)**.</span><span class="sxs-lookup"><span data-stu-id="09a50-314">In hello applications list, select **Amazon Web Services (AWS)**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_app.png) 

3. <span data-ttu-id="09a50-316">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="09a50-316">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="09a50-318">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="09a50-318">Click **Add** button.</span></span> <span data-ttu-id="09a50-319">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="09a50-319">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="09a50-321">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="09a50-321">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="09a50-322">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="09a50-322">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="09a50-323">Üzerinde **rolü Seç** sekmesi, hello kullanıcı için uygun rolü seçin hello.</span><span class="sxs-lookup"><span data-stu-id="09a50-323">On **Select Role** tab, select hello appropriate role for hello user.</span></span> <span data-ttu-id="09a50-324">Bu rolleri hello rol adı ve kimlik sağlayıcısı adı ile gösterilir.</span><span class="sxs-lookup"><span data-stu-id="09a50-324">All these roles are shown with hello role name and identity provider name.</span></span> <span data-ttu-id="09a50-325">Bu şekilde, AWS hello rollerden kolayca tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="09a50-325">This way you can easily identify hello roles from AWS.</span></span>

8. <span data-ttu-id="09a50-326">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="09a50-326">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="09a50-327">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="09a50-327">Testing single sign-on</span></span>

<span data-ttu-id="09a50-328">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="09a50-328">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="09a50-329">Amazon Web Hizmetleri (AWS) hello erişim paneli döşeme hello tıkladığınızda, otomatik olarak oturum açma Amazon Web Hizmetleri (AWS) uygulama tooyour almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="09a50-329">When you click hello Amazon Web Services (AWS) tile in hello Access Panel, you should get automatically signed-on tooyour Amazon Web Services (AWS) application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="09a50-330">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="09a50-330">Additional resources</span></span>

* [<span data-ttu-id="09a50-331">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="09a50-331">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="09a50-332">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="09a50-332">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_203.png
[11]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795031.png
[12]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795032.png
[13]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795033.png
[14]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795034.png
[15]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795035.png
[16]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795022.png
[17]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795023.png
[18]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795024.png
[19]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795025.png
[20]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950351.png
[21]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_80.png
[22]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950352.png
[23]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_81.png
[24]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950353.png
[25]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_15.png

[28]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950321.png
[29]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795037.png
[30]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795038.png
[32]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950251.png
[33]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950252.png
[34]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950253.png
[35]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning.png
[36]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_securitycredentials.png
[37]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_securitycredentials_continue.png
[38]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_createnewaccesskey.png
[39]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_automatic.png
[40]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_testconnection.png
[41]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_on.png
