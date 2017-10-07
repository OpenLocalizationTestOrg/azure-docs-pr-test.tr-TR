---
title: "Öğretici: TINFOIL SECURITY Azure Active Directory Tümleştirme | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile TINFOIL SECURITY arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: da02da92-e3b0-4c09-ad6c-180882b0f9f8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 1a3fa9880d9e026c2d6d6548188df2269ff69139
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tinfoil-security"></a><span data-ttu-id="eaac1-103">Öğretici: TINFOIL SECURITY Azure Active Directory Tümleştirme</span><span class="sxs-lookup"><span data-stu-id="eaac1-103">Tutorial: Azure Active Directory integration with TINFOIL SECURITY</span></span>

<span data-ttu-id="eaac1-104">Bu öğreticide, bilgi nasıl toointegrate TINFOIL SECURITY Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="eaac1-104">In this tutorial, you learn how toointegrate TINFOIL SECURITY with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="eaac1-105">TINFOIL SECURITY Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="eaac1-105">Integrating TINFOIL SECURITY with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="eaac1-106">Erişim tooTINFOIL güvenlik sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="eaac1-106">You can control in Azure AD who has access tooTINFOIL SECURITY</span></span>
- <span data-ttu-id="eaac1-107">Kullanıcıların tooautomatically get açan tooTINFOIL güvenlik (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="eaac1-107">You can enable your users tooautomatically get signed-on tooTINFOIL SECURITY (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="eaac1-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="eaac1-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="eaac1-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="eaac1-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eaac1-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="eaac1-110">Prerequisites</span></span>

<span data-ttu-id="eaac1-111">TINFOIL SECURITY ile Azure AD tümleştirme tooconfigure, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="eaac1-111">tooconfigure Azure AD integration with TINFOIL SECURITY, you need hello following items:</span></span>

- <span data-ttu-id="eaac1-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="eaac1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="eaac1-113">Bir TINFOIL SECURITY çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="eaac1-113">A TINFOIL SECURITY single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="eaac1-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="eaac1-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="eaac1-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="eaac1-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="eaac1-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="eaac1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="eaac1-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="eaac1-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="eaac1-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="eaac1-118">Scenario description</span></span>
<span data-ttu-id="eaac1-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="eaac1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="eaac1-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="eaac1-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="eaac1-121">TINFOIL SECURITY hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="eaac1-121">Add TINFOIL SECURITY from hello gallery</span></span>
2. <span data-ttu-id="eaac1-122">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="eaac1-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-tinfoil-security-from-hello-gallery"></a><span data-ttu-id="eaac1-123">TINFOIL SECURITY hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="eaac1-123">Add TINFOIL SECURITY from hello gallery</span></span>
<span data-ttu-id="eaac1-124">Azure AD'ye tooconfigure hello tümleştirme TINFOIL güvenlik tooadd TINFOIL SECURITY hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="eaac1-124">tooconfigure hello integration of TINFOIL SECURITY into Azure AD, you need tooadd TINFOIL SECURITY from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="eaac1-125">**TINFOIL SECURITY hello galerisinden tooadd hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="eaac1-125">**tooadd TINFOIL SECURITY from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="eaac1-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="eaac1-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="eaac1-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="eaac1-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="eaac1-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="eaac1-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="eaac1-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="eaac1-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="eaac1-133">Merhaba arama kutusuna yazın **TINFOIL SECURITY**seçin **TINFOIL SECURITY** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="eaac1-133">In hello search box, type **TINFOIL SECURITY**, select  **TINFOIL SECURITY** from result panel then click **Add** button tooadd hello application.</span></span>

    ![TINFOIL SECURITY Galeriden](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="eaac1-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="eaac1-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="eaac1-136">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma TINFOIL "Britta Simon" adlı bir test kullanıcı tabanlı güvenliği ile test etme.</span><span class="sxs-lookup"><span data-stu-id="eaac1-136">In this section, you configure and test Azure AD single sign-on with TINFOIL SECURITY based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="eaac1-137">Tek toowork'ın oturum açma hangi hello karşılık gelen TINFOIL Security tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="eaac1-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TINFOIL SECURITY is tooa user in Azure AD.</span></span> <span data-ttu-id="eaac1-138">Diğer bir deyişle, bir Azure AD kullanıcısının ve TINFOIL Security hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="eaac1-138">In other words, a link relationship between an Azure AD user and hello related user in TINFOIL SECURITY needs toobe established.</span></span>

<span data-ttu-id="eaac1-139">TINFOIL güvenlik hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="eaac1-139">In TINFOIL SECURITY, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="eaac1-140">tooconfigure ve TINFOIL SECURITY ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="eaac1-140">tooconfigure and test Azure AD single sign-on with TINFOIL SECURITY, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="eaac1-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="eaac1-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="eaac1-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="eaac1-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="eaac1-143">**[TINFOIL SECURITY test kullanıcısı oluşturma](#create-a-tinfoil-security-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir TINFOIL Security, karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="eaac1-143">**[Create a TINFOIL SECURITY test user](#create-a-tinfoil-security-test-user)** - toohave a counterpart of Britta Simon in TINFOIL SECURITY that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="eaac1-144">**[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="eaac1-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="eaac1-145">**[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="eaac1-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="eaac1-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="eaac1-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="eaac1-147">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma TINFOIL SECURITY uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="eaac1-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TINFOIL SECURITY application.</span></span>

<span data-ttu-id="eaac1-148">**tooconfigure Azure AD çoklu oturum açma TINFOIL güvenlik, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="eaac1-148">**tooconfigure Azure AD single sign-on with TINFOIL SECURITY, perform hello following steps:**</span></span>

1. <span data-ttu-id="eaac1-149">Merhaba hello üzerinde Azure portal'ın **TINFOIL SECURITY** uygulama tümleştirmesi sayfasında, tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="eaac1-149">In hello Azure portal, on hello **TINFOIL SECURITY** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="eaac1-151">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="eaac1-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![SAML oturum açma tabanlı](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_samlbase.png)

3. <span data-ttu-id="eaac1-153">Merhaba üzerinde **TINFOIL güvenlik etki alanı ve URL'leri** bölümünde, hello uygulama zaten Azure ile önceden tümleştirilmiş gibi hello kullanıcının tooperform herhangi bir adımı yok.</span><span class="sxs-lookup"><span data-stu-id="eaac1-153">On hello **TINFOIL SECURITY Domain and URLs** section, hello user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_url.png)


4. <span data-ttu-id="eaac1-155">Merhaba üzerinde **SAML imzalama sertifikası** bölümü, kopyalama hello **parmak İZİ** değeri.</span><span class="sxs-lookup"><span data-stu-id="eaac1-155">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value.</span></span>

    ![SAML imzalama sertifikası bölümü](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_certificate.png) 

5. <span data-ttu-id="eaac1-157">tooadd hello gerekli öznitelik eşlemelerini hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="eaac1-157">tooadd hello required attribute mappings, perform hello following steps:</span></span>
    
    <span data-ttu-id="eaac1-158">![Öznitelikleri](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute1.png "öznitelikleri")</span><span class="sxs-lookup"><span data-stu-id="eaac1-158">![Attributes](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute1.png "Attributes")</span></span>
    
    | <span data-ttu-id="eaac1-159">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="eaac1-159">Attribute Name</span></span>    |   <span data-ttu-id="eaac1-160">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="eaac1-160">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="eaac1-161">Hesap Kimliği</span><span class="sxs-lookup"><span data-stu-id="eaac1-161">accountid</span></span> | <span data-ttu-id="eaac1-162">UXXXXXXXXXXXXX</span><span class="sxs-lookup"><span data-stu-id="eaac1-162">UXXXXXXXXXXXXX</span></span> |
    
    <span data-ttu-id="eaac1-163">a.</span><span class="sxs-lookup"><span data-stu-id="eaac1-163">a.</span></span> <span data-ttu-id="eaac1-164">Tıklatın **kullanıcı özniteliği eklemek**.</span><span class="sxs-lookup"><span data-stu-id="eaac1-164">Click **add user attribute**.</span></span>
    
    <span data-ttu-id="eaac1-165">![Ekle özniteliği](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute.png "öznitelikleri")</span><span class="sxs-lookup"><span data-stu-id="eaac1-165">![ADD Attribute](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute.png "Attributes")</span></span>
    
    <span data-ttu-id="eaac1-166">![Ekle özniteliği](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addatt.png "öznitelikleri")</span><span class="sxs-lookup"><span data-stu-id="eaac1-166">![ADD Attribute](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addatt.png "Attributes")</span></span>
    
    <span data-ttu-id="eaac1-167">b.</span><span class="sxs-lookup"><span data-stu-id="eaac1-167">b.</span></span> <span data-ttu-id="eaac1-168">Merhaba, **öznitelik adı** metin kutusuna, türü **AccountID**.</span><span class="sxs-lookup"><span data-stu-id="eaac1-168">In hello **Attribute Name** textbox, type **accountid**.</span></span>
    
    <span data-ttu-id="eaac1-169">c.</span><span class="sxs-lookup"><span data-stu-id="eaac1-169">c.</span></span> <span data-ttu-id="eaac1-170">Merhaba, **öznitelik değeri** metin kutusuna, daha sonra hello öğretici alacak Yapıştır hello hesabı kimliği değeri.</span><span class="sxs-lookup"><span data-stu-id="eaac1-170">In hello **Attribute Value** textbox, paste hello account ID value which you will get later on hello tutorial.</span></span>
    
    <span data-ttu-id="eaac1-171">d.</span><span class="sxs-lookup"><span data-stu-id="eaac1-171">d.</span></span> <span data-ttu-id="eaac1-172">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="eaac1-172">Click **Ok**.</span></span>    

6. <span data-ttu-id="eaac1-173">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="eaac1-173">Click **Save** button.</span></span>

    ![Kaydet düğmesi](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="eaac1-175">Merhaba üzerinde **TINFOIL Güvenlik Yapılandırması** 'yi tıklatın **TINFOIL Güvenlik Yapılandırması** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="eaac1-175">On hello **TINFOIL SECURITY Configuration** section, click **Configure TINFOIL SECURITY** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="eaac1-176">Kopya hello **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="eaac1-176">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![TINFOIL güvenlik yapılandırması](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_configure.png) 

8. <span data-ttu-id="eaac1-178">Farklı web tarayıcısı penceresinde TINFOIL SECURITY şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="eaac1-178">In a different web browser window, log into your TINFOIL SECURITY company site as an administrator.</span></span>

9. <span data-ttu-id="eaac1-179">Merhaba üstte Hello araç çubuğunda **hesabım**.</span><span class="sxs-lookup"><span data-stu-id="eaac1-179">In hello toolbar on hello top, click **My Account**.</span></span>
   
    <span data-ttu-id="eaac1-180">![Pano](./media/active-directory-saas-tinfoil-security-tutorial/ic798971.png "Panosu")</span><span class="sxs-lookup"><span data-stu-id="eaac1-180">![Dashboard](./media/active-directory-saas-tinfoil-security-tutorial/ic798971.png "Dashboard")</span></span>

10. <span data-ttu-id="eaac1-181">Tıklatın **güvenlik**.</span><span class="sxs-lookup"><span data-stu-id="eaac1-181">Click **Security**.</span></span>
   
    <span data-ttu-id="eaac1-182">![Güvenlik](./media/active-directory-saas-tinfoil-security-tutorial/ic798972.png "güvenlik")</span><span class="sxs-lookup"><span data-stu-id="eaac1-182">![Security](./media/active-directory-saas-tinfoil-security-tutorial/ic798972.png "Security")</span></span>

11. <span data-ttu-id="eaac1-183">Merhaba üzerinde **çoklu oturum açma** yapılandırma sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="eaac1-183">On hello **Single Sign-On** configuration page, perform hello following steps:</span></span>
   
    <span data-ttu-id="eaac1-184">![Çoklu oturum açma](./media/active-directory-saas-tinfoil-security-tutorial/ic798973.png "çoklu oturum açma")</span><span class="sxs-lookup"><span data-stu-id="eaac1-184">![Single Sign-On](./media/active-directory-saas-tinfoil-security-tutorial/ic798973.png "Single Sign-On")</span></span>
   
    <span data-ttu-id="eaac1-185">a.</span><span class="sxs-lookup"><span data-stu-id="eaac1-185">a.</span></span> <span data-ttu-id="eaac1-186">Seçin **etkinleştirmek SAML**.</span><span class="sxs-lookup"><span data-stu-id="eaac1-186">Select **Enable SAML**.</span></span>
   
    <span data-ttu-id="eaac1-187">b.</span><span class="sxs-lookup"><span data-stu-id="eaac1-187">b.</span></span> <span data-ttu-id="eaac1-188">Tıklatın **el ile yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="eaac1-188">Click **Manual Configuration**.</span></span>
   
    <span data-ttu-id="eaac1-189">c.</span><span class="sxs-lookup"><span data-stu-id="eaac1-189">c.</span></span> <span data-ttu-id="eaac1-190">İçinde **SAML gönderme URL'sini** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan</span><span class="sxs-lookup"><span data-stu-id="eaac1-190">In **SAML Post URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal</span></span>
   
    <span data-ttu-id="eaac1-191">d.</span><span class="sxs-lookup"><span data-stu-id="eaac1-191">d.</span></span> <span data-ttu-id="eaac1-192">İçinde **SAML sertifika parmak izi** metin kutusuna, Yapıştır hello değerini **parmak izi** kopyalanan **SAML imzalama sertifikası** bölümü.</span><span class="sxs-lookup"><span data-stu-id="eaac1-192">In **SAML Certificate Fingerprint** textbox, paste hello value of **Thumbprint** which you have copied from **SAML Signing Certificate** section.</span></span>
  
    <span data-ttu-id="eaac1-193">e.</span><span class="sxs-lookup"><span data-stu-id="eaac1-193">e.</span></span> <span data-ttu-id="eaac1-194">Kopya **bilgisayarınızı hesap kimliği** değer ve hello değerinde yapıştırma **öznitelik değeri** metin kutusu altında **özniteliği eklemek** Azure portalı bölümünde.</span><span class="sxs-lookup"><span data-stu-id="eaac1-194">Copy **Your Account ID** value and paste hello value in **Attribute Value** textbox under **Add Attribute** section in Azure portal.</span></span>
   
    <span data-ttu-id="eaac1-195">f.</span><span class="sxs-lookup"><span data-stu-id="eaac1-195">f.</span></span> <span data-ttu-id="eaac1-196">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="eaac1-196">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="eaac1-197">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="eaac1-197">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="eaac1-198">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="eaac1-198">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="eaac1-199">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="eaac1-199">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="eaac1-200">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="eaac1-200">Create an Azure AD test user</span></span>
<span data-ttu-id="eaac1-201">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="eaac1-201">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="eaac1-203">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="eaac1-203">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="eaac1-204">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="eaac1-204">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="eaac1-206">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="eaac1-206">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![<span data-ttu-id="eaac1-207">Kullanıcıların ve grupların tüm kullanıcılar -></span><span class="sxs-lookup"><span data-stu-id="eaac1-207">Users and groups -> All users</span></span> ](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="eaac1-208">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="eaac1-208">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Kullanıcı](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="eaac1-210">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="eaac1-210">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="eaac1-212">a.</span><span class="sxs-lookup"><span data-stu-id="eaac1-212">a.</span></span> <span data-ttu-id="eaac1-213">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="eaac1-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="eaac1-214">b.</span><span class="sxs-lookup"><span data-stu-id="eaac1-214">b.</span></span> <span data-ttu-id="eaac1-215">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="eaac1-215">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="eaac1-216">c.</span><span class="sxs-lookup"><span data-stu-id="eaac1-216">c.</span></span> <span data-ttu-id="eaac1-217">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="eaac1-217">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="eaac1-218">d.</span><span class="sxs-lookup"><span data-stu-id="eaac1-218">d.</span></span> <span data-ttu-id="eaac1-219">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="eaac1-219">Click **Create**.</span></span>
 
### <a name="create-a-tinfoil-security-test-user"></a><span data-ttu-id="eaac1-220">TINFOIL SECURITY test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="eaac1-220">Create a TINFOIL SECURITY test user</span></span>

<span data-ttu-id="eaac1-221">TINFOIL SECURITY içine sipariş tooenable Azure AD kullanıcıların toolog bunların TINFOIL SECURITY sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="eaac1-221">In order tooenable Azure AD users toolog into TINFOIL SECURITY, they must be provisioned into TINFOIL SECURITY.</span></span> <span data-ttu-id="eaac1-222">TINFOIL SECURITY Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="eaac1-222">In hello case of TINFOIL SECURITY, provisioning is a manual task.</span></span>

<span data-ttu-id="eaac1-223">**tooget sağlanan, bir kullanıcı hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="eaac1-223">**tooget a user provisioned, perform hello following steps:**</span></span>

1. <span data-ttu-id="eaac1-224">Merhaba kullanıcı bir kurumsal hesap parçasıysa çok ihtiyacınız[hello TINFOIL SECURITY Destek ekibine başvurun](https://www.tinfoilsecurity.com/contact) tooget hello kullanıcı hesabı oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="eaac1-224">If hello user is a part of an Enterprise account, you need too[contact hello TINFOIL SECURITY support team](https://www.tinfoilsecurity.com/contact) tooget hello user account created.</span></span>

2. <span data-ttu-id="eaac1-225">Merhaba kullanıcı normal bir TINFOIL güvenlik SaaS kullanıcı ise, hello kullanıcı hello kullanıcının sitelerin ortak çalışanı tooany ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eaac1-225">If hello user is a regular TINFOIL SECURITY SaaS user, then hello user can add a collaborator tooany of hello user’s sites.</span></span> <span data-ttu-id="eaac1-226">Bu tetikleyicileri bir davet toohello belirtilen işlem toosend e-posta toocreate yeni TINFOIL SECURITY kullanıcı hesabı.</span><span class="sxs-lookup"><span data-stu-id="eaac1-226">This triggers a process toosend an invitation toohello specified email toocreate a new TINFOIL SECURITY user account.</span></span>

> [!NOTE]
> <span data-ttu-id="eaac1-227">API'leri, Azure AD kullanıcı hesapları TINFOIL SECURITY tooprovision tarafından sağlanan veya herhangi diğer TINFOIL SECURITY kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eaac1-227">You can use any other TINFOIL SECURITY user account creation tools or APIs provided by TINFOIL SECURITY tooprovision Azure AD user accounts.</span></span>
> 
> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="eaac1-228">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="eaac1-228">Assign hello Azure AD test user</span></span>

<span data-ttu-id="eaac1-229">Bu bölümde, erişim tooTINFOIL güvenlik vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="eaac1-229">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTINFOIL SECURITY.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="eaac1-231">**tooassign Britta Simon tooTINFOIL güvenlik hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="eaac1-231">**tooassign Britta Simon tooTINFOIL SECURITY, perform hello following steps:**</span></span>

1. <span data-ttu-id="eaac1-232">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="eaac1-232">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="eaac1-234">Merhaba uygulamalar listesinde **TINFOIL SECURITY**.</span><span class="sxs-lookup"><span data-stu-id="eaac1-234">In hello applications list, select **TINFOIL SECURITY**.</span></span>

    ![TINFOIL SECURITY seçin](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_app.png) 

3. <span data-ttu-id="eaac1-236">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="eaac1-236">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="eaac1-238">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="eaac1-238">Click **Add** button.</span></span> <span data-ttu-id="eaac1-239">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="eaac1-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="eaac1-241">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="eaac1-241">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="eaac1-242">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="eaac1-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="eaac1-243">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="eaac1-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="eaac1-244">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="eaac1-244">Test single sign-on</span></span>

<span data-ttu-id="eaac1-245">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="eaac1-245">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="eaac1-246">Merhaba TINFOIL SECURITY hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour TINFOIL SECURITY uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="eaac1-246">When you click hello TINFOIL SECURITY tile in hello Access Panel, you should get automatically signed-on tooyour TINFOIL SECURITY application.</span></span> <span data-ttu-id="eaac1-247">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="eaac1-247">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="eaac1-248">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="eaac1-248">Additional resources</span></span>

* [<span data-ttu-id="eaac1-249">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="eaac1-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="eaac1-250">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="eaac1-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_203.png

