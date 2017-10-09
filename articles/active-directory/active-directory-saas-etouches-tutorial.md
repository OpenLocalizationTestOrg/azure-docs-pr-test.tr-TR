---
title: "Öğretici: Azure Active Directory Tümleştirme ile etouches | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile etouches arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 76cccaa8-859c-4c16-9d1d-8a6496fc7520
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 5f3ff7550e660b0fc52612140ca55061504b5edd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-etouches"></a><span data-ttu-id="71650-103">Öğretici: Azure Active Directory Tümleştirme etouches ile</span><span class="sxs-lookup"><span data-stu-id="71650-103">Tutorial: Azure Active Directory integration with etouches</span></span>

<span data-ttu-id="71650-104">Bu öğreticide, bilgi nasıl toointegrate etouches Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="71650-104">In this tutorial, you learn how toointegrate etouches with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="71650-105">Etouches Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="71650-105">Integrating etouches with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="71650-106">Erişim tooetouches sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="71650-106">You can control in Azure AD who has access tooetouches</span></span>
- <span data-ttu-id="71650-107">Kullanıcıların tooautomatically get açan tooetouches (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="71650-107">You can enable your users tooautomatically get signed-on tooetouches (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="71650-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="71650-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="71650-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="71650-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="71650-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="71650-110">Prerequisites</span></span>

<span data-ttu-id="71650-111">tooconfigure etouches ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="71650-111">tooconfigure Azure AD integration with etouches, you need hello following items:</span></span>

- <span data-ttu-id="71650-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="71650-112">An Azure AD subscription</span></span>
- <span data-ttu-id="71650-113">Bir etouches çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="71650-113">An etouches single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="71650-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="71650-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="71650-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="71650-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="71650-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="71650-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="71650-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="71650-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="71650-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="71650-118">Scenario description</span></span>
<span data-ttu-id="71650-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="71650-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="71650-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="71650-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="71650-121">Merhaba Galerisi'nden etouches ekleme</span><span class="sxs-lookup"><span data-stu-id="71650-121">Adding etouches from hello gallery</span></span>
2. <span data-ttu-id="71650-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="71650-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-etouches-from-hello-gallery"></a><span data-ttu-id="71650-123">Merhaba Galerisi'nden etouches ekleme</span><span class="sxs-lookup"><span data-stu-id="71650-123">Adding etouches from hello gallery</span></span>
<span data-ttu-id="71650-124">Azure AD'ye tooconfigure hello tümleştirme etouches, tooadd etouches hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="71650-124">tooconfigure hello integration of etouches into Azure AD, you need tooadd etouches from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="71650-125">**Merhaba galerisinden tooadd etouches hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="71650-125">**tooadd etouches from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="71650-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="71650-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory düğmesi][1]

2. <span data-ttu-id="71650-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="71650-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="71650-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="71650-129">Then go too**All applications**.</span></span>

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="71650-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="71650-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Merhaba yeni uygulama düğmesi][3]

4. <span data-ttu-id="71650-133">Merhaba arama kutusuna yazın **etouches**seçin **etouches** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="71650-133">In hello search box, type **etouches**, select **etouches** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Merhaba sonuçları listesinde etouches](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="71650-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="71650-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="71650-136">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı etouches sınayın.</span><span class="sxs-lookup"><span data-stu-id="71650-136">In this section, you configure and test Azure AD single sign-on with etouches based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="71650-137">Tek toowork'ın oturum açma hangi hello karşılık gelen etouches içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="71650-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in etouches is tooa user in Azure AD.</span></span> <span data-ttu-id="71650-138">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı etouches hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="71650-138">In other words, a link relationship between an Azure AD user and hello related user in etouches needs toobe established.</span></span>

<span data-ttu-id="71650-139">Merhaba hello değeri etouches içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="71650-139">In etouches, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="71650-140">tooconfigure ve etouches ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="71650-140">tooconfigure and test Azure AD single sign-on with etouches, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="71650-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="71650-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="71650-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="71650-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="71650-143">**[Bir etouches test kullanıcısı oluşturma](#create-an-etouches-test-user)**  -toohave bir Britta Simon karşılık gelen kullanıcı bağlantılı toohello Azure AD gösterimidir etouches içinde.</span><span class="sxs-lookup"><span data-stu-id="71650-143">**[Create an etouches test user](#create-an-etouches-test-user)** - toohave a counterpart of Britta Simon in etouches that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="71650-144">**[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="71650-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="71650-145">**[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="71650-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="71650-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="71650-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="71650-147">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma etouches uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="71650-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your etouches application.</span></span>

<span data-ttu-id="71650-148">**tooconfigure Azure AD çoklu oturum açma ile etouches, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="71650-148">**tooconfigure Azure AD single sign-on with etouches, perform hello following steps:**</span></span>

1. <span data-ttu-id="71650-149">Hello hello üzerinde Azure portal'ın **etouches** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="71650-149">In hello Azure portal, on hello **etouches** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="71650-151">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="71650-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_samlbase.png)

3. <span data-ttu-id="71650-153">Merhaba üzerinde **etouches etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="71650-153">On hello **etouches Domain and URLs** section, perform hello following steps:</span></span>

    ![etouches etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_url.png)

    <span data-ttu-id="71650-155">a.</span><span class="sxs-lookup"><span data-stu-id="71650-155">a.</span></span> <span data-ttu-id="71650-156">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://www.eiseverywhere.com/saml/accounts/?sso&accountid=<ACCOUNTID>`</span><span class="sxs-lookup"><span data-stu-id="71650-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://www.eiseverywhere.com/saml/accounts/?sso&accountid=<ACCOUNTID>`</span></span>

    <span data-ttu-id="71650-157">b.</span><span class="sxs-lookup"><span data-stu-id="71650-157">b.</span></span> <span data-ttu-id="71650-158">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://www.eiseverywhere.com/<instance name>`</span><span class="sxs-lookup"><span data-stu-id="71650-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://www.eiseverywhere.com/<instance name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="71650-159">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="71650-159">These values are not real.</span></span> <span data-ttu-id="71650-160">Hello ile gerçek hello değeri güncelleştirin URL ve hello öğreticinin ilerleyen bölümlerinde açıklanan tanımlayıcı oturum açın.</span><span class="sxs-lookup"><span data-stu-id="71650-160">You update hello value with hello actual Sign on URL and Identifier, which is explained later in hello tutorial.</span></span>
    > 

4. <span data-ttu-id="71650-161">etouches uygulama hello SAML onaylar belirli bir biçimde bekler.</span><span class="sxs-lookup"><span data-stu-id="71650-161">etouches application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="71650-162">Bu uygulama için talep aşağıdaki hello yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="71650-162">Configure hello following claims for this application.</span></span> <span data-ttu-id="71650-163">Hello başlangıç değerleri bu özniteliklerin yönetebilirsiniz **kullanıcı özniteliği** hello uygulamasının.</span><span class="sxs-lookup"><span data-stu-id="71650-163">You can manage hello values of these attributes from hello **User Attribute** of hello application.</span></span> <span data-ttu-id="71650-164">Ekran aşağıdaki hello bunun bir örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="71650-164">hello following screenshot shows an example for this.</span></span> 

    ![Kullanıcı özniteliği](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_attribute.png) 

5. <span data-ttu-id="71650-166">Merhaba, **kullanıcı öznitelikleri** hello bölüm **çoklu oturum açma** iletişim kutusunda, SAML belirteci özniteliği hello görüntüde gösterildiği gibi yapılandırmak ve hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="71650-166">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="71650-167">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="71650-167">Attribute Name</span></span> | <span data-ttu-id="71650-168">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="71650-168">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="71650-169">E-posta</span><span class="sxs-lookup"><span data-stu-id="71650-169">Email</span></span> | <span data-ttu-id="71650-170">User.Mail</span><span class="sxs-lookup"><span data-stu-id="71650-170">user.mail</span></span> |    
    
    <span data-ttu-id="71650-171">a.</span><span class="sxs-lookup"><span data-stu-id="71650-171">a.</span></span> <span data-ttu-id="71650-172">Tıklatın **Ekle özniteliği** tooopen hello **özniteliği eklemek** iletişim.</span><span class="sxs-lookup"><span data-stu-id="71650-172">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Öznitelik Ekle](./media/active-directory-saas-etouches-tutorial/tutorial_attribute_04.png)

    ![Öznitelik iletişim ekleyin](./media/active-directory-saas-etouches-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="71650-175">b.</span><span class="sxs-lookup"><span data-stu-id="71650-175">b.</span></span> <span data-ttu-id="71650-176">Merhaba, **adı** metin kutusuna, ilgili satır için gösterilen türü hello öznitelik adı.</span><span class="sxs-lookup"><span data-stu-id="71650-176">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="71650-177">c.</span><span class="sxs-lookup"><span data-stu-id="71650-177">c.</span></span> <span data-ttu-id="71650-178">Merhaba gelen **değeri** listesinde, ilgili satır için gösterilen türü hello öznitelik değeri.</span><span class="sxs-lookup"><span data-stu-id="71650-178">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="71650-179">d.</span><span class="sxs-lookup"><span data-stu-id="71650-179">d.</span></span> <span data-ttu-id="71650-180">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="71650-180">Click **Ok**.</span></span> 

6. <span data-ttu-id="71650-181">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="71650-181">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_certificate.png) 

7. <span data-ttu-id="71650-183">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="71650-183">Click **Save** button.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-etouches-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="71650-185">tooget uygulamanız için yapılandırılmış SSO Merhaba etouches uygulaması adımlarını izleyerek hello gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="71650-185">tooget SSO configured for your application, perform hello following steps in hello etouches application:</span></span> 

    ![etouches yapılandırma](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_06.png) 

    <span data-ttu-id="71650-187">a.</span><span class="sxs-lookup"><span data-stu-id="71650-187">a.</span></span> <span data-ttu-id="71650-188">Oturum açma çok**etouches** hello yönetici hakları kullanarak uygulama.</span><span class="sxs-lookup"><span data-stu-id="71650-188">Login too**etouches** application using hello Admin rights.</span></span>
   
    <span data-ttu-id="71650-189">b.</span><span class="sxs-lookup"><span data-stu-id="71650-189">b.</span></span> <span data-ttu-id="71650-190">Toohello Git **SAML** yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="71650-190">Go toohello **SAML** Configuration.</span></span>

    <span data-ttu-id="71650-191">c.</span><span class="sxs-lookup"><span data-stu-id="71650-191">c.</span></span> <span data-ttu-id="71650-192">Merhaba, **genel ayarları** bölümünde, Not Defteri'nde, kopyalama Merhaba içeriğine Azure Portalı'ndan indirilen sertifikanızı açın ve hello IDP meta verileri metin kutusuna yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="71650-192">In hello **General Settings** section, open your downloaded certificate from Azure portal in notepad, copy hello content, and then paste it into hello IDP metadata textbox.</span></span> 

    <span data-ttu-id="71650-193">d.</span><span class="sxs-lookup"><span data-stu-id="71650-193">d.</span></span> <span data-ttu-id="71650-194">Tıklatın hello üzerinde **kalmak & Kaydet** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="71650-194">Click on hello **Save & Stay** button.</span></span>
  
    <span data-ttu-id="71650-195">e.</span><span class="sxs-lookup"><span data-stu-id="71650-195">e.</span></span> <span data-ttu-id="71650-196">Tıklatın hello üzerinde **güncelleştirme meta verilerini** hello SAML meta veri bölümünden düğmesini.</span><span class="sxs-lookup"><span data-stu-id="71650-196">Click on hello **Update Metadata** button in hello SAML Metadata section.</span></span> 

    <span data-ttu-id="71650-197">f.</span><span class="sxs-lookup"><span data-stu-id="71650-197">f.</span></span> <span data-ttu-id="71650-198">Bu açılır sayfa hello ve SSO gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="71650-198">This opens hello page and perform SSO.</span></span> <span data-ttu-id="71650-199">Merhaba kullanıcı adına ayarlayın, sonra bir kez hello SSO çalışmaktadır.</span><span class="sxs-lookup"><span data-stu-id="71650-199">Once hello SSO is working then you can set up hello username.</span></span>

    <span data-ttu-id="71650-200">g.</span><span class="sxs-lookup"><span data-stu-id="71650-200">g.</span></span> <span data-ttu-id="71650-201">Merhaba Hello kullanıcı adı alanında seçin **emailaddress** hello resimde gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="71650-201">In hello Username field, select hello **emailaddress** as shown in hello image below.</span></span> 

    <span data-ttu-id="71650-202">h.</span><span class="sxs-lookup"><span data-stu-id="71650-202">h.</span></span> <span data-ttu-id="71650-203">Kopyalama hello **SP varlık kimliği** değer ve hello yapıştırma **tanımlayıcısı** bulunduğu textbox **etouches etki alanı ve URL'leri** Azure Portal'daki bölüm.</span><span class="sxs-lookup"><span data-stu-id="71650-203">Copy hello **SP entity ID** value and paste it into hello **Identifier**  textbox, which is in **etouches Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="71650-204">ı.</span><span class="sxs-lookup"><span data-stu-id="71650-204">i.</span></span> <span data-ttu-id="71650-205">Kopyalama hello **SSO URL / ACS** değer ve hello yapıştırma **URL üzerinde oturum** bulunduğu textbox **etouches etki alanı ve URL'leri** Azure Portal'daki bölüm.</span><span class="sxs-lookup"><span data-stu-id="71650-205">Copy hello **SSO URL / ACS** value and paste it into hello **Sign on URL** textbox, which is in **etouches Domain and URLs** section on Azure portal.</span></span>
   
> [!TIP]
> <span data-ttu-id="71650-206">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="71650-206">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="71650-207">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="71650-207">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="71650-208">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="71650-208">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="71650-209">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="71650-209">Create an Azure AD test user</span></span>
<span data-ttu-id="71650-210">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="71650-210">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="71650-212">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="71650-212">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="71650-213">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="71650-213">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-etouches-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="71650-215">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="71650-215">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-etouches-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="71650-217">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="71650-217">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Merhaba Ekle düğmesi](./media/active-directory-saas-etouches-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="71650-219">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="71650-219">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-etouches-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="71650-221">a.</span><span class="sxs-lookup"><span data-stu-id="71650-221">a.</span></span> <span data-ttu-id="71650-222">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="71650-222">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="71650-223">b.</span><span class="sxs-lookup"><span data-stu-id="71650-223">b.</span></span> <span data-ttu-id="71650-224">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="71650-224">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="71650-225">c.</span><span class="sxs-lookup"><span data-stu-id="71650-225">c.</span></span> <span data-ttu-id="71650-226">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="71650-226">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="71650-227">d.</span><span class="sxs-lookup"><span data-stu-id="71650-227">d.</span></span> <span data-ttu-id="71650-228">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="71650-228">Click **Create**.</span></span>
 
### <a name="create-an-etouches-test-user"></a><span data-ttu-id="71650-229">Bir etouches test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="71650-229">Create an etouches test user</span></span>

<span data-ttu-id="71650-230">Bu bölümde, etouches içinde Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="71650-230">In this section, you create a user called Britta Simon in etouches.</span></span> <span data-ttu-id="71650-231">Çalışmak [etouches istemci destek ekibi](https://www.etouches.com/event-software/support/customer-support/) tooadd hello kullanıcılar hello etouches Platform.</span><span class="sxs-lookup"><span data-stu-id="71650-231">Work with [etouches Client support team](https://www.etouches.com/event-software/support/customer-support/) tooadd hello users in hello etouches platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="71650-232">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="71650-232">Assign hello Azure AD test user</span></span>

<span data-ttu-id="71650-233">Bu bölümde, erişim tooetouches vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="71650-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooetouches.</span></span>

![Merhaba kullanıcı rolü atayın][200] 

<span data-ttu-id="71650-235">**tooassign Britta Simon tooetouches hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="71650-235">**tooassign Britta Simon tooetouches, perform hello following steps:**</span></span>

1. <span data-ttu-id="71650-236">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="71650-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="71650-238">Merhaba uygulamalar listesinde **etouches**.</span><span class="sxs-lookup"><span data-stu-id="71650-238">In hello applications list, select **etouches**.</span></span>

    ![Merhaba etouches bağlantı hello uygulamalar listesinde](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_app.png) 

3. <span data-ttu-id="71650-240">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="71650-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202] 

4. <span data-ttu-id="71650-242">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="71650-242">Click **Add** button.</span></span> <span data-ttu-id="71650-243">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="71650-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Merhaba eklemek atama bölmesi][203]

5. <span data-ttu-id="71650-245">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="71650-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="71650-246">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="71650-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="71650-247">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="71650-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="71650-248">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="71650-248">Test single sign-on</span></span>


<span data-ttu-id="71650-249">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="71650-249">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="71650-250">Merhaba erişim paneli etouches döşeme hello tıkladığınızda, otomatik olarak oturum açma tooyour etouches uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="71650-250">When you click hello etouches tile in hello Access Panel, you should get automatically signed-on tooyour etouches application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="71650-251">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="71650-251">Additional resources</span></span>

* [<span data-ttu-id="71650-252">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="71650-252">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="71650-253">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="71650-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_203.png

