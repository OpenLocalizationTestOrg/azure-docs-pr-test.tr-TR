---
title: "Öğretici: Azure Active Directory Tümleştirme ile Boomi | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Boomi arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8e05afa9-2eda-4975-a0cc-6d408065860f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: ce64a4561697d311a8c7b1b244315bb552c5cfb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-boomi"></a><span data-ttu-id="b29d1-103">Öğretici: Azure Active Directory Tümleştirme Boomi ile</span><span class="sxs-lookup"><span data-stu-id="b29d1-103">Tutorial: Azure Active Directory integration with Boomi</span></span>

<span data-ttu-id="b29d1-104">Bu öğreticide, bilgi nasıl toointegrate Boomi Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b29d1-104">In this tutorial, you learn how toointegrate Boomi with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b29d1-105">Boomi Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="b29d1-105">Integrating Boomi with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b29d1-106">Erişim tooBoomi sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="b29d1-106">You can control in Azure AD who has access tooBoomi</span></span>
- <span data-ttu-id="b29d1-107">Kullanıcıların tooautomatically get açan tooBoomi (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="b29d1-107">You can enable your users tooautomatically get signed-on tooBoomi (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b29d1-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="b29d1-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b29d1-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b29d1-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b29d1-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="b29d1-110">Prerequisites</span></span>

<span data-ttu-id="b29d1-111">tooconfigure Boomi ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="b29d1-111">tooconfigure Azure AD integration with Boomi, you need hello following items:</span></span>

- <span data-ttu-id="b29d1-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="b29d1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b29d1-113">Bir Boomi çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="b29d1-113">A Boomi single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b29d1-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="b29d1-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b29d1-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="b29d1-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b29d1-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="b29d1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b29d1-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b29d1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b29d1-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="b29d1-118">Scenario description</span></span>
<span data-ttu-id="b29d1-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="b29d1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b29d1-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="b29d1-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b29d1-121">Merhaba Galerisi'nden Boomi ekleme</span><span class="sxs-lookup"><span data-stu-id="b29d1-121">Adding Boomi from hello gallery</span></span>
2. <span data-ttu-id="b29d1-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="b29d1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-boomi-from-hello-gallery"></a><span data-ttu-id="b29d1-123">Merhaba Galerisi'nden Boomi ekleme</span><span class="sxs-lookup"><span data-stu-id="b29d1-123">Adding Boomi from hello gallery</span></span>
<span data-ttu-id="b29d1-124">Azure AD'ye tooconfigure hello tümleştirme Boomi, tooadd Boomi hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="b29d1-124">tooconfigure hello integration of Boomi into Azure AD, you need tooadd Boomi from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b29d1-125">**tooadd Boomi hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="b29d1-125">**tooadd Boomi from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b29d1-126">Merhaba, ** [Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="b29d1-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b29d1-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="b29d1-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b29d1-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="b29d1-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="b29d1-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="b29d1-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="b29d1-133">Merhaba arama kutusuna yazın **Boomi**.</span><span class="sxs-lookup"><span data-stu-id="b29d1-133">In hello search box, type **Boomi**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_search.png)

5. <span data-ttu-id="b29d1-135">Merhaba Sonuçlar panelinde seçin **Boomi**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="b29d1-135">In hello results panel, select **Boomi**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b29d1-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="b29d1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b29d1-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Boomi sınayın.</span><span class="sxs-lookup"><span data-stu-id="b29d1-138">In this section, you configure and test Azure AD single sign-on with Boomi based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b29d1-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Boomi içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="b29d1-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Boomi is tooa user in Azure AD.</span></span> <span data-ttu-id="b29d1-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Boomi hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="b29d1-140">In other words, a link relationship between an Azure AD user and hello related user in Boomi needs toobe established.</span></span>

<span data-ttu-id="b29d1-141">Merhaba hello değeri Boomi içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="b29d1-141">In Boomi, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="b29d1-142">tooconfigure ve Boomi ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="b29d1-142">tooconfigure and test Azure AD single sign-on with Boomi, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b29d1-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on) ** -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="b29d1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b29d1-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user) ** -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="b29d1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b29d1-145">**[Boomi test kullanıcısı oluşturma](#creating-a-boomi-test-user) ** -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Boomi içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="b29d1-145">**[Creating a Boomi test user](#creating-a-boomi-test-user)** - toohave a counterpart of Britta Simon in Boomi that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b29d1-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="b29d1-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b29d1-147">**[Çoklu oturum açmayı test](#testing-single-sign-on) ** -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="b29d1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b29d1-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b29d1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b29d1-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Boomi uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="b29d1-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Boomi application.</span></span>

<span data-ttu-id="b29d1-150">**tooconfigure Azure AD çoklu oturum açma ile Boomi, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="b29d1-150">**tooconfigure Azure AD single sign-on with Boomi, perform hello following steps:**</span></span>

1. <span data-ttu-id="b29d1-151">Hello hello üzerinde Azure portal'ın **Boomi** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="b29d1-151">In hello Azure portal, on hello **Boomi** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="b29d1-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="b29d1-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_samlbase.png)

3. <span data-ttu-id="b29d1-155">Merhaba üzerinde **Boomi etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="b29d1-155">On hello **Boomi Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_url.png)

    <span data-ttu-id="b29d1-157">a.</span><span class="sxs-lookup"><span data-stu-id="b29d1-157">a.</span></span> <span data-ttu-id="b29d1-158">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://platform.boomi.com/sso/<accountname>/saml`</span><span class="sxs-lookup"><span data-stu-id="b29d1-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://platform.boomi.com/sso/<accountname>/saml`</span></span>

    <span data-ttu-id="b29d1-159">b.</span><span class="sxs-lookup"><span data-stu-id="b29d1-159">b.</span></span> <span data-ttu-id="b29d1-160">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://platform.boomi.com/sso/<accountname>/saml`</span><span class="sxs-lookup"><span data-stu-id="b29d1-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://platform.boomi.com/sso/<accountname>/saml`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b29d1-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="b29d1-161">These values are not real.</span></span> <span data-ttu-id="b29d1-162">Bu değerleri hello gerçek tanımlayıcısı ve yanıt URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="b29d1-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="b29d1-163">Kişi [Boomi destek ekibi](https://boomi.com/company/contact/) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="b29d1-163">Contact [Boomi support team](https://boomi.com/company/contact/) tooget these values.</span></span>

4. <span data-ttu-id="b29d1-164">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="b29d1-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_certificate.png)

4. <span data-ttu-id="b29d1-166">Boomi uygulama hello SAML onaylar belirli bir biçimde bekler.</span><span class="sxs-lookup"><span data-stu-id="b29d1-166">Boomi application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="b29d1-167">Lütfen bu uygulama için talep aşağıdaki hello yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="b29d1-167">Please configure hello following claims for this application.</span></span> <span data-ttu-id="b29d1-168">Hello başlangıç değerleri bu özniteliklerin yönetebilirsiniz "**kullanıcı öznitelikleri**" uygulama tümleştirmesi sayfasında bölüm.</span><span class="sxs-lookup"><span data-stu-id="b29d1-168">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="b29d1-169">Ekran aşağıdaki hello bunun bir örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="b29d1-169">hello following screenshot shows an example for this.</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-boomi-tutorial/tutorial_attribute.png)

5. <span data-ttu-id="b29d1-171">Merhaba, **kullanıcı öznitelikleri** hello bölüm **çoklu oturum açma** iletişim kutusunda, hello aşağıdaki tabloda, gösterilen her satır için gerçekleştirme adımları izleyerek hello:</span><span class="sxs-lookup"><span data-stu-id="b29d1-171">In hello **User Attributes** section on hello **Single sign-on** dialog, for each row shown in hello table below, perform hello following steps:</span></span>

    | <span data-ttu-id="b29d1-172">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="b29d1-172">Attribute Name</span></span> | <span data-ttu-id="b29d1-173">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="b29d1-173">Attribute Value</span></span> |
    | -------------- | --------------- |
    | <span data-ttu-id="b29d1-174">FEDERATION_ID</span><span class="sxs-lookup"><span data-stu-id="b29d1-174">FEDERATION_ID</span></span> | <span data-ttu-id="b29d1-175">User.Mail</span><span class="sxs-lookup"><span data-stu-id="b29d1-175">user.mail</span></span> |
    
    <span data-ttu-id="b29d1-176">a.</span><span class="sxs-lookup"><span data-stu-id="b29d1-176">a.</span></span> <span data-ttu-id="b29d1-177">Tıklatın **Ekle özniteliği** tooopen hello **özniteliği eklemek** iletişim.</span><span class="sxs-lookup"><span data-stu-id="b29d1-177">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-boomi-tutorial/tutorial_attribute_04.png)
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-boomi-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="b29d1-180">b.</span><span class="sxs-lookup"><span data-stu-id="b29d1-180">b.</span></span> <span data-ttu-id="b29d1-181">Merhaba, **adı** metin kutusuna, ilgili satır için gösterilen türü hello öznitelik adı.</span><span class="sxs-lookup"><span data-stu-id="b29d1-181">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="b29d1-182">c.</span><span class="sxs-lookup"><span data-stu-id="b29d1-182">c.</span></span> <span data-ttu-id="b29d1-183">Merhaba gelen **değeri** listesinde, ilgili satır için gösterilen türü hello öznitelik değeri.</span><span class="sxs-lookup"><span data-stu-id="b29d1-183">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="b29d1-184">d.</span><span class="sxs-lookup"><span data-stu-id="b29d1-184">d.</span></span> <span data-ttu-id="b29d1-185">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b29d1-185">Click **Ok**.</span></span>

6. <span data-ttu-id="b29d1-186">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="b29d1-186">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-boomi-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="b29d1-188">Merhaba üzerinde **Boomi yapılandırma** 'yi tıklatın **yapılandırma Boomi** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="b29d1-188">On hello **Boomi Configuration** section, click **Configure Boomi** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="b29d1-189">Kopya hello **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="b29d1-189">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_configure.png) 

8. <span data-ttu-id="b29d1-191">Farklı web tarayıcısı penceresinde Boomi şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="b29d1-191">In a different web browser window, log into your Boomi company site as an administrator.</span></span> 

9. <span data-ttu-id="b29d1-192">Çok gidin**şirket adı** ve çok Git**ayarlanan**.</span><span class="sxs-lookup"><span data-stu-id="b29d1-192">Navigate too**Company Name** and go too**Set up**.</span></span>

10. <span data-ttu-id="b29d1-193">Merhaba tıklatın **SSO seçenekleri** sekmesinde ve aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="b29d1-193">Click hello **SSO Options** tab and perform below steps.</span></span>

    ![Çoklu oturum açma uygulama tarafında yapılandırma](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_11.png)

    <span data-ttu-id="b29d1-195">a.</span><span class="sxs-lookup"><span data-stu-id="b29d1-195">a.</span></span> <span data-ttu-id="b29d1-196">Denetleme **etkinleştirmek SAML çoklu oturum açma** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="b29d1-196">Check **Enable SAML Single Sign-On** checkbox.</span></span>

    <span data-ttu-id="b29d1-197">b.</span><span class="sxs-lookup"><span data-stu-id="b29d1-197">b.</span></span> <span data-ttu-id="b29d1-198">Tıklatın **alma** tooupload hello sertifika çok Azure AD'den indirilen**kimlik sağlayıcısı sertifikası**.</span><span class="sxs-lookup"><span data-stu-id="b29d1-198">Click **Import** tooupload hello downloaded certificate from Azure AD too**Identity Provider Certificate**.</span></span>
    
    <span data-ttu-id="b29d1-199">c.</span><span class="sxs-lookup"><span data-stu-id="b29d1-199">c.</span></span> <span data-ttu-id="b29d1-200">Merhaba, **kimlik sağlayıcısı oturum açma URL'si** hello değerini put textbox **SAML çoklu oturum açma hizmet URL'si** Azure AD uygulama yapılandırma penceresinden.</span><span class="sxs-lookup"><span data-stu-id="b29d1-200">In hello **Identity Provider Login URL** textbox, put hello value of **SAML Single Sign-On Service URL** from Azure AD application configuration window.</span></span>

    <span data-ttu-id="b29d1-201">d.</span><span class="sxs-lookup"><span data-stu-id="b29d1-201">d.</span></span> <span data-ttu-id="b29d1-202">Olarak **Federasyon kimliği konumu**seçin **Federasyon kimliğidir FEDERATION_ID özniteliği öğesinde** radyo düğmesi.</span><span class="sxs-lookup"><span data-stu-id="b29d1-202">As **Federation Id Location**, select **Federation Id is in FEDERATION_ID Attribute element** radio button.</span></span> 

    <span data-ttu-id="b29d1-203">e.</span><span class="sxs-lookup"><span data-stu-id="b29d1-203">e.</span></span> <span data-ttu-id="b29d1-204">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="b29d1-204">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="b29d1-205">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="b29d1-205">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b29d1-206">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere ** Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="b29d1-206">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b29d1-207">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b29d1-207">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b29d1-208">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="b29d1-208">Creating an Azure AD test user</span></span>
<span data-ttu-id="b29d1-209">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="b29d1-209">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="b29d1-211">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="b29d1-211">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b29d1-212">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="b29d1-212">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-boomi-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b29d1-214">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="b29d1-214">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-boomi-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b29d1-216">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="b29d1-216">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-boomi-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b29d1-218">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="b29d1-218">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-boomi-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b29d1-220">a.</span><span class="sxs-lookup"><span data-stu-id="b29d1-220">a.</span></span> <span data-ttu-id="b29d1-221">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b29d1-221">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b29d1-222">b.</span><span class="sxs-lookup"><span data-stu-id="b29d1-222">b.</span></span> <span data-ttu-id="b29d1-223">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="b29d1-223">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b29d1-224">c.</span><span class="sxs-lookup"><span data-stu-id="b29d1-224">c.</span></span> <span data-ttu-id="b29d1-225">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="b29d1-225">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b29d1-226">d.</span><span class="sxs-lookup"><span data-stu-id="b29d1-226">d.</span></span> <span data-ttu-id="b29d1-227">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b29d1-227">Click **Create**.</span></span>
 
### <a name="creating-a-boomi-test-user"></a><span data-ttu-id="b29d1-228">Boomi test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="b29d1-228">Creating a Boomi test user</span></span>

<span data-ttu-id="b29d1-229">TooBoomi içinde sipariş tooenable Azure AD kullanıcıların toolog bunların Boomi sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b29d1-229">In order tooenable Azure AD users toolog in tooBoomi, they must be provisioned into Boomi.</span></span> <span data-ttu-id="b29d1-230">Boomi Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="b29d1-230">In hello case of Boomi, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a><span data-ttu-id="b29d1-231">bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="b29d1-231">tooprovision a user account, perform hello following steps:</span></span>

1. <span data-ttu-id="b29d1-232">İçinde tooyour Boomi şirket site yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="b29d1-232">Log in tooyour Boomi company site as an administrator.</span></span>

2. <span data-ttu-id="b29d1-233">Oturum açtıktan sonra çok gidin**kullanıcı yönetimi** ve çok Git**kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="b29d1-233">After logging in, navigate too**User Management** and go too**Users**.</span></span>

    <span data-ttu-id="b29d1-234">![Kullanıcıların](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_001.png "kullanıcılar")</span><span class="sxs-lookup"><span data-stu-id="b29d1-234">![Users](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_001.png "Users")</span></span>

3. <span data-ttu-id="b29d1-235">Tıklatın ** + ** simgesi ve hello **Ekle/Koru kullanıcı rolleri** iletişim kutusunu açar.</span><span class="sxs-lookup"><span data-stu-id="b29d1-235">Click **+**  icon and hello **Add/Maintain User Roles** dialog opens.</span></span>

    <span data-ttu-id="b29d1-236">![Kullanıcıların](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_002.png "kullanıcılar")</span><span class="sxs-lookup"><span data-stu-id="b29d1-236">![Users](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_002.png "Users")</span></span>

    <span data-ttu-id="b29d1-237">![Kullanıcıların](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_003.png "kullanıcılar")</span><span class="sxs-lookup"><span data-stu-id="b29d1-237">![Users](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_003.png "Users")</span></span>

    <span data-ttu-id="b29d1-238">a.</span><span class="sxs-lookup"><span data-stu-id="b29d1-238">a.</span></span> <span data-ttu-id="b29d1-239">Merhaba, **kullanıcı e-posta adresi** metin kutusuna, kullanıcının türü hello e-posta ister BrittaSimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="b29d1-239">In hello **User e-mail address** textbox, type hello email of user like BrittaSimon@contoso.com.</span></span>
    
    <span data-ttu-id="b29d1-240">b.</span><span class="sxs-lookup"><span data-stu-id="b29d1-240">b.</span></span> <span data-ttu-id="b29d1-241">Merhaba, **ad** metin kutusuna, türü hello Britta gibi kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="b29d1-241">In hello **First name** textbox, type hello First name of user like Britta.</span></span>

    <span data-ttu-id="b29d1-242">c.</span><span class="sxs-lookup"><span data-stu-id="b29d1-242">c.</span></span> <span data-ttu-id="b29d1-243">Merhaba, **Soyadı** metin kutusuna, türü hello kullanıcının soyadını Simon gibi.</span><span class="sxs-lookup"><span data-stu-id="b29d1-243">In hello **Last name** textbox, type hello Last name of user like Simon.</span></span>
    
    <span data-ttu-id="b29d1-244">d.</span><span class="sxs-lookup"><span data-stu-id="b29d1-244">d.</span></span> <span data-ttu-id="b29d1-245">Merhaba kullanıcının girin **Federasyon kimliği**.</span><span class="sxs-lookup"><span data-stu-id="b29d1-245">Enter hello user's **Federation ID**.</span></span> <span data-ttu-id="b29d1-246">Her kullanıcının hello kullanıcı hello hesabı içinde benzersiz olarak tanıtan bir Federasyon kimliği olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b29d1-246">Each user must have a Federation ID that uniquely identifies hello user within hello account.</span></span>
    
    <span data-ttu-id="b29d1-247">e.</span><span class="sxs-lookup"><span data-stu-id="b29d1-247">e.</span></span> <span data-ttu-id="b29d1-248">Merhaba atamak **standart kullanıcı** rol toohello kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="b29d1-248">Assign hello **Standard User** role toohello user.</span></span> <span data-ttu-id="b29d1-249">Hello yöneticisi rolü, kendisine normal Atmosfer erişim yanı sıra tek oturum açma erişimini vereceği için atamayın.</span><span class="sxs-lookup"><span data-stu-id="b29d1-249">Do not assign hello Administrator role because that would give him normal Atmosphere access as well as single sign-on access.</span></span>
    
    <span data-ttu-id="b29d1-250">f.</span><span class="sxs-lookup"><span data-stu-id="b29d1-250">f.</span></span> <span data-ttu-id="b29d1-251">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b29d1-251">Click **OK**.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="b29d1-252">Merhaba kullanıcı parolasını hello kimlik sağlayıcısı olarak yönetildiğinden toohello AtomSphere hesabı içinde kullanılan toolog olabilir bir parola içeren bir Hoş Geldiniz bildirim e-posta alırsınız.</span><span class="sxs-lookup"><span data-stu-id="b29d1-252">hello user will not receive a welcome notification email containing a password that can be used toolog in toohello AtomSphere account because his password is managed through hello identity provider.</span></span> <span data-ttu-id="b29d1-253">API AAD kullanıcı hesaplarının Boomi tooprovision tarafından sağlanan veya herhangi diğer Boomi kullanıcı hesabı oluşturma araçlarını kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="b29d1-253">You may use any other Boomi user account creation tools or APIs provided by Boomi tooprovision AAD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b29d1-254">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="b29d1-254">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b29d1-255">Bu bölümde, erişim tooBoomi vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="b29d1-255">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBoomi.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="b29d1-257">**tooassign Britta Simon tooBoomi hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="b29d1-257">**tooassign Britta Simon tooBoomi, perform hello following steps:**</span></span>

1. <span data-ttu-id="b29d1-258">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="b29d1-258">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="b29d1-260">Merhaba uygulamalar listesinde **Boomi**.</span><span class="sxs-lookup"><span data-stu-id="b29d1-260">In hello applications list, select **Boomi**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_app.png) 

3. <span data-ttu-id="b29d1-262">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="b29d1-262">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="b29d1-264">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="b29d1-264">Click **Add** button.</span></span> <span data-ttu-id="b29d1-265">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="b29d1-265">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="b29d1-267">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="b29d1-267">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b29d1-268">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="b29d1-268">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b29d1-269">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="b29d1-269">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b29d1-270">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="b29d1-270">Testing single sign-on</span></span>

<span data-ttu-id="b29d1-271">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="b29d1-271">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b29d1-272">Merhaba Boomi hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Boomi uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b29d1-272">When you click hello Boomi tile in hello Access Panel, you should get automatically signed-on tooyour Boomi application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b29d1-273">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="b29d1-273">Additional resources</span></span>

* [<span data-ttu-id="b29d1-274">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="b29d1-274">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b29d1-275">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="b29d1-275">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_203.png

