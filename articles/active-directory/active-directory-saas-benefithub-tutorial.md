---
title: "Öğretici: Azure Active Directory Tümleştirme ile BenefitHub | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile BenefitHub arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4069fe32-a452-463f-973e-7aa0baa4c2fa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: c07d6e44e8cbc79afd79c900664011b059206b56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benefithub"></a><span data-ttu-id="ff5e3-103">Öğretici: Azure Active Directory Tümleştirme BenefitHub ile</span><span class="sxs-lookup"><span data-stu-id="ff5e3-103">Tutorial: Azure Active Directory integration with BenefitHub</span></span>

<span data-ttu-id="ff5e3-104">Bu öğreticide, bilgi nasıl toointegrate BenefitHub Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ff5e3-104">In this tutorial, you learn how toointegrate BenefitHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ff5e3-105">BenefitHub Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="ff5e3-105">Integrating BenefitHub with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ff5e3-106">Erişim tooBenefitHub sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="ff5e3-106">You can control in Azure AD who has access tooBenefitHub</span></span>
- <span data-ttu-id="ff5e3-107">Kullanıcıların tooautomatically get açan tooBenefitHub (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="ff5e3-107">You can enable your users tooautomatically get signed-on tooBenefitHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ff5e3-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="ff5e3-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ff5e3-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ff5e3-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ff5e3-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ff5e3-110">Prerequisites</span></span>

<span data-ttu-id="ff5e3-111">tooconfigure BenefitHub ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="ff5e3-111">tooconfigure Azure AD integration with BenefitHub, you need hello following items:</span></span>

- <span data-ttu-id="ff5e3-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="ff5e3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ff5e3-113">Bir BenefitHub çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="ff5e3-113">A BenefitHub single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ff5e3-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ff5e3-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="ff5e3-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ff5e3-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ff5e3-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ff5e3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ff5e3-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="ff5e3-118">Scenario description</span></span>
<span data-ttu-id="ff5e3-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ff5e3-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="ff5e3-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ff5e3-121">Merhaba Galerisi'nden BenefitHub ekleme</span><span class="sxs-lookup"><span data-stu-id="ff5e3-121">Adding BenefitHub from hello gallery</span></span>
2. <span data-ttu-id="ff5e3-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="ff5e3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-benefithub-from-hello-gallery"></a><span data-ttu-id="ff5e3-123">Merhaba Galerisi'nden BenefitHub ekleme</span><span class="sxs-lookup"><span data-stu-id="ff5e3-123">Adding BenefitHub from hello gallery</span></span>
<span data-ttu-id="ff5e3-124">Azure AD'ye tooconfigure hello tümleştirme BenefitHub, tooadd BenefitHub hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-124">tooconfigure hello integration of BenefitHub into Azure AD, you need tooadd BenefitHub from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ff5e3-125">**tooadd BenefitHub hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ff5e3-125">**tooadd BenefitHub from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ff5e3-126">Merhaba, ** [Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ff5e3-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ff5e3-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="ff5e3-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="ff5e3-133">Merhaba arama kutusuna yazın **BenefitHub**.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-133">In hello search box, type **BenefitHub**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_search.png)

5. <span data-ttu-id="ff5e3-135">Merhaba Sonuçlar panelinde seçin **BenefitHub**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-135">In hello results panel, select **BenefitHub**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ff5e3-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="ff5e3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ff5e3-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı BenefitHub ile test etme</span><span class="sxs-lookup"><span data-stu-id="ff5e3-138">In this section, you configure and test Azure AD single sign-on with BenefitHub based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ff5e3-139">Tek toowork'ın oturum açma hangi hello karşılık gelen BenefitHub içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BenefitHub is tooa user in Azure AD.</span></span> <span data-ttu-id="ff5e3-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı BenefitHub hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-140">In other words, a link relationship between an Azure AD user and hello related user in BenefitHub needs toobe established.</span></span>

<span data-ttu-id="ff5e3-141">Merhaba hello değeri BenefitHub içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-141">In BenefitHub, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ff5e3-142">tooconfigure ve BenefitHub ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="ff5e3-142">tooconfigure and test Azure AD single sign-on with BenefitHub, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ff5e3-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on) ** -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ff5e3-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user) ** -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ff5e3-145">**[BenefitHub test kullanıcısı oluşturma](#creating-a-benefithub-test-user) ** -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir BenefitHub içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-145">**[Creating a BenefitHub test user](#creating-a-benefithub-test-user)** - toohave a counterpart of Britta Simon in BenefitHub that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ff5e3-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ff5e3-147">**[Çoklu oturum açmayı test](#testing-single-sign-on) ** -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ff5e3-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ff5e3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ff5e3-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma BenefitHub uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BenefitHub application.</span></span>

<span data-ttu-id="ff5e3-150">**tooconfigure Azure AD çoklu oturum açma ile BenefitHub, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ff5e3-150">**tooconfigure Azure AD single sign-on with BenefitHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="ff5e3-151">Hello hello üzerinde Azure portal'ın **BenefitHub** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-151">In hello Azure portal, on hello **BenefitHub** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="ff5e3-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_samlbase.png)

3. <span data-ttu-id="ff5e3-155">Merhaba üzerinde **BenefitHub etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="ff5e3-155">On hello **BenefitHub Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_url1.png)
  
    <span data-ttu-id="ff5e3-157">a.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-157">a.</span></span> <span data-ttu-id="ff5e3-158">Merhaba, **tanımlayıcısı** metin kutusuna, türü:`urn:benefithub:passport`</span><span class="sxs-lookup"><span data-stu-id="ff5e3-158">In hello **Identifier** textbox, type: `urn:benefithub:passport`</span></span>
    
    <span data-ttu-id="ff5e3-159">b.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-159">b.</span></span> <span data-ttu-id="ff5e3-160">Merhaba, **yanıt URL'si** metin kutusuna, türü:`https://passport.benefithub.info/saml/post/ac`</span><span class="sxs-lookup"><span data-stu-id="ff5e3-160">In hello **Reply URL** textbox, type: `https://passport.benefithub.info/saml/post/ac`</span></span>

4. <span data-ttu-id="ff5e3-161">Merhaba BenefitHub uygulama hello SAML onaylar, tooadd özel öznitelik eşlemelerini tooyour SAML belirteci öznitelikleri yapılandırma gerektiren belirli bir biçimde, bekliyor.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-161">hello BenefitHub application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="ff5e3-162">Bu uygulama için talep aşağıdaki hello yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-162">Configure hello following claims for this application.</span></span> <span data-ttu-id="ff5e3-163">Hello başlangıç değerleri bu özniteliklerin yönetebilirsiniz "**kullanıcı öznitelikleri**" uygulama tümleştirmesi sayfasında bölüm.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-163">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_attribute.png)

5. <span data-ttu-id="ff5e3-165">Merhaba, **kullanıcı öznitelikleri** hello bölüm **çoklu oturum açma** iletişim kutusunda, SAML belirteci özniteliği görüntü önceki hello gösterildiği gibi yapılandırmak ve hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="ff5e3-165">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello preceding image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="ff5e3-166">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="ff5e3-166">Attribute Name</span></span> | <span data-ttu-id="ff5e3-167">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="ff5e3-167">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="ff5e3-168">organizationid</span><span class="sxs-lookup"><span data-stu-id="ff5e3-168">organizationid</span></span> | <span data-ttu-id="ff5e3-169">< organizationid ></span><span class="sxs-lookup"><span data-stu-id="ff5e3-169">< organizationid ></span></span> |

    > [!NOTE]
    > <span data-ttu-id="ff5e3-170">Bu öznitelik değerini gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-170">This attribute value is not real.</span></span> <span data-ttu-id="ff5e3-171">Bu değer ile gerçek organizationid güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-171">Update this value with actual organizationid.</span></span> <span data-ttu-id="ff5e3-172">Kişi [BenefitHub destek ekibi](https://www.benefithub.com/Home/ContactUs) tooget hello gerçek organizationid.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-172">Contact [BenefitHub support team](https://www.benefithub.com/Home/ContactUs) tooget hello actual organizationid.</span></span>
    
    <span data-ttu-id="ff5e3-173">a.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-173">a.</span></span> <span data-ttu-id="ff5e3-174">Tıklatın **Ekle özniteliği** tooopen hello **özniteliği eklemek** iletişim.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-174">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-benefithub-tutorial/tutorial_attribute_04.png)

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-benefithub-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="ff5e3-177">b.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-177">b.</span></span> <span data-ttu-id="ff5e3-178">Merhaba, **adı** metin kutusuna, ilgili satır için gösterilen türü hello öznitelik adı.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-178">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="ff5e3-179">c.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-179">c.</span></span> <span data-ttu-id="ff5e3-180">Merhaba gelen **değeri** listesinde, ilgili satır için gösterilen türü hello öznitelik değeri.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-180">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="ff5e3-181">d.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-181">d.</span></span> <span data-ttu-id="ff5e3-182">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-182">Click **Ok**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ff5e3-183">Merhaba SAML onayı yapılandırmadan önce toocontact gerekir, [BenefitHub Destek](https://www.benefithub.com/Home/ContactUs) ve kiracınız için hello benzersiz tanımlayıcı özniteliği hello değerini isteyin.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-183">Before you can configure hello SAML assertion, you need toocontact your [BenefitHub support](https://www.benefithub.com/Home/ContactUs) and request hello value of hello unique identifier attribute for your tenant.</span></span> <span data-ttu-id="ff5e3-184">Değer bu tooconfigure hello özel talep uygulamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-184">You need this value tooconfigure hello custom claim for your application.</span></span>

6. <span data-ttu-id="ff5e3-185">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-185">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_certificate.png) 

7. <span data-ttu-id="ff5e3-187">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-187">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-benefithub-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="ff5e3-189">tooconfigure çoklu oturum açma üzerinde **BenefitHub** yan, indirilen toosend hello ihtiyacınız **meta veri XML** çok[BenefitHub destek ekibi](https://www.benefithub.com/Home/ContactUs).</span><span class="sxs-lookup"><span data-stu-id="ff5e3-189">tooconfigure single sign-on on **BenefitHub** side, you need toosend hello downloaded **Metadata XML** too[BenefitHub support team](https://www.benefithub.com/Home/ContactUs).</span></span> <span data-ttu-id="ff5e3-190">Bunlar, bu ayar toohave hello iki tarafta da ayarlamanızı SAML SSO bağlantı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-190">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="ff5e3-191">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="ff5e3-191">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ff5e3-192">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere ** Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-192">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ff5e3-193">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ff5e3-193">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ff5e3-194">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ff5e3-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="ff5e3-195">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-195">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="ff5e3-197">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ff5e3-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ff5e3-198">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-198">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-benefithub-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ff5e3-200">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-200">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-benefithub-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ff5e3-202">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-202">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-benefithub-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ff5e3-204">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="ff5e3-204">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-benefithub-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ff5e3-206">a.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-206">a.</span></span> <span data-ttu-id="ff5e3-207">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-207">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ff5e3-208">b.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-208">b.</span></span> <span data-ttu-id="ff5e3-209">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-209">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ff5e3-210">c.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-210">c.</span></span> <span data-ttu-id="ff5e3-211">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-211">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ff5e3-212">d.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-212">d.</span></span> <span data-ttu-id="ff5e3-213">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-213">Click **Create**.</span></span>
 
### <a name="creating-a-benefithub-test-user"></a><span data-ttu-id="ff5e3-214">BenefitHub test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ff5e3-214">Creating a BenefitHub test user</span></span>

<span data-ttu-id="ff5e3-215">Bu bölümde, BenefitHub içinde Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-215">In this section, you create a user called Britta Simon in BenefitHub.</span></span> <span data-ttu-id="ff5e3-216">Çalışmak [BenefitHub destek ekibi](https://www.benefithub.com/Home/ContactUs) hello BenefitHub platform hello kullanıcıları eklemek için.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-216">Work with [BenefitHub support team](https://www.benefithub.com/Home/ContactUs) to add hello users in hello BenefitHub platform.</span></span> <span data-ttu-id="ff5e3-217">Kullanıcıların oluşturulan ve çoklu oturum açma kullanmadan önce etkinleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-217">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ff5e3-218">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="ff5e3-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ff5e3-219">Bu bölümde, erişim tooBenefitHub vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBenefitHub.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="ff5e3-221">**tooassign Britta Simon tooBenefitHub hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ff5e3-221">**tooassign Britta Simon tooBenefitHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="ff5e3-222">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="ff5e3-224">Merhaba uygulamalar listesinde **BenefitHub**.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-224">In hello applications list, select **BenefitHub**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_app.png) 

3. <span data-ttu-id="ff5e3-226">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="ff5e3-228">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-228">Click **Add** button.</span></span> <span data-ttu-id="ff5e3-229">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="ff5e3-231">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ff5e3-232">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ff5e3-233">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ff5e3-234">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="ff5e3-234">Testing single sign-on</span></span>

<span data-ttu-id="ff5e3-235">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-235">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ff5e3-236">Merhaba BenefitHub hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour BenefitHub uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ff5e3-236">When you click hello BenefitHub tile in hello Access Panel, you should get automatically signed-on tooyour BenefitHub application.</span></span>
<span data-ttu-id="ff5e3-237">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="ff5e3-237">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ff5e3-238">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="ff5e3-238">Additional resources</span></span>

* [<span data-ttu-id="ff5e3-239">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="ff5e3-239">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ff5e3-240">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="ff5e3-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_203.png

