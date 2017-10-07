---
title: "Öğretici: Azure Active Directory Tümleştirme Mozy kuruluş ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Mozy kuruluş arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 489b5e62-85c2-45c9-8766-326632d48114
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: jeedes
ms.openlocfilehash: bab0df4f3621b784cd8edfda3c8e10fe5a7ced9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mozy-enterprise"></a><span data-ttu-id="f0057-103">Öğretici: Azure Active Directory Tümleştirme Mozy kuruluş ile</span><span class="sxs-lookup"><span data-stu-id="f0057-103">Tutorial: Azure Active Directory integration with Mozy Enterprise</span></span>

<span data-ttu-id="f0057-104">Bu öğreticide, bilgi nasıl toointegrate Mozy kuruluş Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f0057-104">In this tutorial, you learn how toointegrate Mozy Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f0057-105">Mozy kuruluş Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="f0057-105">Integrating Mozy Enterprise with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f0057-106">Erişim tooMozy Kurumsal sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="f0057-106">You can control in Azure AD who has access tooMozy Enterprise</span></span>
- <span data-ttu-id="f0057-107">Kullanıcıların tooautomatically get açan tooMozy Enterprise (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="f0057-107">You can enable your users tooautomatically get signed-on tooMozy Enterprise (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f0057-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="f0057-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f0057-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f0057-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f0057-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="f0057-110">Prerequisites</span></span>

<span data-ttu-id="f0057-111">tooconfigure Mozy Kurumsal ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="f0057-111">tooconfigure Azure AD integration with Mozy Enterprise, you need hello following items:</span></span>

- <span data-ttu-id="f0057-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="f0057-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f0057-113">Bir Mozy Kurumsal çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="f0057-113">A Mozy Enterprise single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f0057-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="f0057-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f0057-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="f0057-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f0057-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="f0057-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f0057-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f0057-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f0057-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="f0057-118">Scenario description</span></span>
<span data-ttu-id="f0057-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="f0057-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f0057-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="f0057-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f0057-121">Merhaba Galerisi'nden Mozy Kurumsal ekleme</span><span class="sxs-lookup"><span data-stu-id="f0057-121">Adding Mozy Enterprise from hello gallery</span></span>
2. <span data-ttu-id="f0057-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="f0057-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mozy-enterprise-from-hello-gallery"></a><span data-ttu-id="f0057-123">Merhaba Galerisi'nden Mozy Kurumsal ekleme</span><span class="sxs-lookup"><span data-stu-id="f0057-123">Adding Mozy Enterprise from hello gallery</span></span>
<span data-ttu-id="f0057-124">Azure AD'ye tooconfigure hello tümleştirme Mozy Enterprise tooadd Mozy Kurumsal hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="f0057-124">tooconfigure hello integration of Mozy Enterprise into Azure AD, you need tooadd Mozy Enterprise from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f0057-125">**tooadd Mozy Kurumsal hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f0057-125">**tooadd Mozy Enterprise from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f0057-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="f0057-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f0057-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="f0057-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f0057-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="f0057-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="f0057-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f0057-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="f0057-133">Merhaba arama kutusuna yazın **Mozy Kurumsal**.</span><span class="sxs-lookup"><span data-stu-id="f0057-133">In hello search box, type **Mozy Enterprise**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_search.png)

5. <span data-ttu-id="f0057-135">Merhaba Sonuçlar panelinde seçin **Mozy Kurumsal**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="f0057-135">In hello results panel, select **Mozy Enterprise**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f0057-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="f0057-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f0057-138">Bu bölümde, yapılandırmak ve Mozy kuruluş ile Azure AD çoklu oturum açmayı test "Britta Simon" adlı bir test kullanıcı tabanlı.</span><span class="sxs-lookup"><span data-stu-id="f0057-138">In this section, you configure and test Azure AD single sign-on with Mozy Enterprise based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f0057-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Mozy kuruluştaki tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="f0057-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Mozy Enterprise is tooa user in Azure AD.</span></span> <span data-ttu-id="f0057-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve Mozy kuruluştaki hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="f0057-140">In other words, a link relationship between an Azure AD user and hello related user in Mozy Enterprise needs toobe established.</span></span>

<span data-ttu-id="f0057-141">Merhaba hello değeri Mozy kuruluşta atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="f0057-141">In Mozy Enterprise, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f0057-142">tooconfigure ve Mozy kuruluş ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="f0057-142">tooconfigure and test Azure AD single sign-on with Mozy Enterprise, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f0057-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="f0057-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f0057-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="f0057-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f0057-145">**[Mozy Kurumsal test kullanıcısı oluşturma](#creating-a-mozy-enterprise-test-user)**  -toohave karşılık gelen, Britta Simon Mozy kuruluştaki kullanıcı bağlantılı toohello Azure AD gösterimidir.</span><span class="sxs-lookup"><span data-stu-id="f0057-145">**[Creating a Mozy Enterprise test user](#creating-a-mozy-enterprise-test-user)** - toohave a counterpart of Britta Simon in Mozy Enterprise that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f0057-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="f0057-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f0057-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="f0057-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f0057-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f0057-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f0057-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Mozy Kurumsal uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="f0057-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Mozy Enterprise application.</span></span>

<span data-ttu-id="f0057-150">**tooconfigure Azure AD çoklu oturum açma Mozy kuruluş ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f0057-150">**tooconfigure Azure AD single sign-on with Mozy Enterprise, perform hello following steps:**</span></span>

1. <span data-ttu-id="f0057-151">Merhaba hello üzerinde Azure portal'ın **Mozy Kurumsal** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="f0057-151">In hello Azure portal, on hello **Mozy Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="f0057-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="f0057-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_samlbase.png)

3. <span data-ttu-id="f0057-155">Merhaba üzerinde **Mozy kuruluş etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="f0057-155">On hello **Mozy Enterprise Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_url.png)

    <span data-ttu-id="f0057-157">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<tenantname>.Mozyenterprise.com`</span><span class="sxs-lookup"><span data-stu-id="f0057-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenantname>.Mozyenterprise.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f0057-158">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="f0057-158">This value is not real.</span></span> <span data-ttu-id="f0057-159">Bu değer ile Merhaba güncelleştirme gerçek oturum açma URL'si.</span><span class="sxs-lookup"><span data-stu-id="f0057-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="f0057-160">Kişi [Mozy Kurumsal İstemci destek ekibi](http://support.mozy.com/) tooget bu değer.</span><span class="sxs-lookup"><span data-stu-id="f0057-160">Contact [Mozy Enterprise Client support team](http://support.mozy.com/) tooget this value.</span></span>

4. <span data-ttu-id="f0057-161">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="f0057-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_certificate.png) 

5. <span data-ttu-id="f0057-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f0057-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f0057-165">Merhaba üzerinde **Mozy Kurumsal yapılandırma** 'yi tıklatın **Mozy Kurumsal yapılandırma** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="f0057-165">On hello **Mozy Enterprise Configuration** section, click **Configure Mozy Enterprise** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="f0057-166">Kopya hello **SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="f0057-166">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_configure.png) 

7. <span data-ttu-id="f0057-168">Farklı web tarayıcısı penceresinde Mozy Kurumsal şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="f0057-168">In a different web browser window, log into your Mozy Enterprise company site as an administrator.</span></span>

8. <span data-ttu-id="f0057-169">Merhaba, **yapılandırma** 'yi tıklatın **kimlik doğrulama İlkesi**.</span><span class="sxs-lookup"><span data-stu-id="f0057-169">In hello **Configuration** section, click **Authentication Policy**.</span></span>
   
   <span data-ttu-id="f0057-170">![Kimlik doğrulama İlkesi](./media/active-directory-saas-mozy-enterprise-tutorial/ic777314.png "kimlik doğrulama İlkesi")</span><span class="sxs-lookup"><span data-stu-id="f0057-170">![Authentication policy](./media/active-directory-saas-mozy-enterprise-tutorial/ic777314.png "Authentication policy")</span></span>

9. <span data-ttu-id="f0057-171">Merhaba üzerinde **kimlik doğrulama İlkesi** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="f0057-171">On hello **Authentication Policy** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="f0057-172">![Kimlik doğrulama İlkesi](./media/active-directory-saas-mozy-enterprise-tutorial/ic777315.png "kimlik doğrulama İlkesi")</span><span class="sxs-lookup"><span data-stu-id="f0057-172">![Authentication policy](./media/active-directory-saas-mozy-enterprise-tutorial/ic777315.png "Authentication policy")</span></span>
   
   <span data-ttu-id="f0057-173">a.</span><span class="sxs-lookup"><span data-stu-id="f0057-173">a.</span></span> <span data-ttu-id="f0057-174">Seçin **dizin hizmeti** olarak **sağlayıcı**.</span><span class="sxs-lookup"><span data-stu-id="f0057-174">Select **Directory Service** as **Provider**.</span></span>
   
   <span data-ttu-id="f0057-175">b.</span><span class="sxs-lookup"><span data-stu-id="f0057-175">b.</span></span> <span data-ttu-id="f0057-176">Seçin **LDAP göndermeyi kullanmak**.</span><span class="sxs-lookup"><span data-stu-id="f0057-176">Select **Use LDAP Push**.</span></span>
   
   <span data-ttu-id="f0057-177">c.</span><span class="sxs-lookup"><span data-stu-id="f0057-177">c.</span></span> <span data-ttu-id="f0057-178">Merhaba tıklatın **SAML kimlik doğrulaması** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="f0057-178">Click hello **SAML Authentication** tab.</span></span>
   
   <span data-ttu-id="f0057-179">d.</span><span class="sxs-lookup"><span data-stu-id="f0057-179">d.</span></span> <span data-ttu-id="f0057-180">Yapıştır **SAML çoklu oturum açma hizmet URL'si**, hello hello Azure portal ' Kopyalanan **kimlik doğrulaması URL'sini** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="f0057-180">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal into hello **Authentication URL** textbox.</span></span>
   
   <span data-ttu-id="f0057-181">e.</span><span class="sxs-lookup"><span data-stu-id="f0057-181">e.</span></span> <span data-ttu-id="f0057-182">Yapıştır **SAML varlık kimliği**, hello hello Azure portal ' Kopyalanan **SAML Endpoint** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="f0057-182">Paste **SAML Entity ID**, which you have copied from hello Azure portal into hello **SAML Endpoint** textbox.</span></span>
   
   <span data-ttu-id="f0057-183">f.</span><span class="sxs-lookup"><span data-stu-id="f0057-183">f.</span></span> <span data-ttu-id="f0057-184">İndirilen base-64 kodlanmış sertifika kopyalama hello panonuza bunu içerik Not Defteri'nde açın ve yapıştırın içine tüm sertifika hello **SAML sertifika** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="f0057-184">Open your downloaded base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste hello entire Certificate into **SAML Certificate** textbox.</span></span>
   
   <span data-ttu-id="f0057-185">g.</span><span class="sxs-lookup"><span data-stu-id="f0057-185">g.</span></span> <span data-ttu-id="f0057-186">Seçin **etkinleştirmek SSO Admins toolog, ağ kimlik bilgilerini oturum için**.</span><span class="sxs-lookup"><span data-stu-id="f0057-186">Select **Enable SSO for Admins toolog in with their network credentials**.</span></span>
   
   <span data-ttu-id="f0057-187">h.</span><span class="sxs-lookup"><span data-stu-id="f0057-187">h.</span></span> <span data-ttu-id="f0057-188">Tıklatın **değişiklikleri kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="f0057-188">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="f0057-189">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="f0057-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f0057-190">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="f0057-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f0057-191">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f0057-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f0057-192">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f0057-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="f0057-193">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="f0057-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="f0057-195">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f0057-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f0057-196">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="f0057-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f0057-198">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="f0057-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f0057-200">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="f0057-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f0057-202">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="f0057-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f0057-204">a.</span><span class="sxs-lookup"><span data-stu-id="f0057-204">a.</span></span> <span data-ttu-id="f0057-205">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f0057-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f0057-206">b.</span><span class="sxs-lookup"><span data-stu-id="f0057-206">b.</span></span> <span data-ttu-id="f0057-207">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="f0057-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f0057-208">c.</span><span class="sxs-lookup"><span data-stu-id="f0057-208">c.</span></span> <span data-ttu-id="f0057-209">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="f0057-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f0057-210">d.</span><span class="sxs-lookup"><span data-stu-id="f0057-210">d.</span></span> <span data-ttu-id="f0057-211">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f0057-211">Click **Create**.</span></span>
 
### <a name="creating-a-mozy-enterprise-test-user"></a><span data-ttu-id="f0057-212">Mozy Kurumsal test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f0057-212">Creating a Mozy Enterprise test user</span></span>

<span data-ttu-id="f0057-213">Mozy Kurumsal içine sipariş tooenable Azure AD kullanıcıların toolog bunlar Mozy kuruma sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f0057-213">In order tooenable Azure AD users toolog into Mozy Enterprise, they must be provisioned into Mozy Enterprise.</span></span> <span data-ttu-id="f0057-214">Mozy Kurumsal Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="f0057-214">In hello case of Mozy Enterprise, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="f0057-215">API AAD kullanıcı hesaplarının Mozy Kurumsal tooprovision tarafından sağlanan veya herhangi diğer Mozy Kurumsal kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f0057-215">You can use any other Mozy Enterprise user account creation tools or APIs provided by Mozy Enterprise tooprovision AAD user accounts.</span></span>

<span data-ttu-id="f0057-216">**bir kullanıcı hesapları tooprovision gerçekleştirmek hello adımları izleyin:**</span><span class="sxs-lookup"><span data-stu-id="f0057-216">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="f0057-217">İçinde tooyour oturum **Mozy Kurumsal** Kiracı.</span><span class="sxs-lookup"><span data-stu-id="f0057-217">Log in tooyour **Mozy Enterprise** tenant.</span></span>

2. <span data-ttu-id="f0057-218">Tıklatın **kullanıcılar**ve ardından **yeni kullanıcı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="f0057-218">Click **Users**, and then click **Add New User**.</span></span>
   
   <span data-ttu-id="f0057-219">![Kullanıcıların](./media/active-directory-saas-mozy-enterprise-tutorial/ic777317.png "kullanıcılar")</span><span class="sxs-lookup"><span data-stu-id="f0057-219">![Users](./media/active-directory-saas-mozy-enterprise-tutorial/ic777317.png "Users")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="f0057-220">Merhaba **yeni kullanıcı Ekle** seçeneği ise yalnızca görüntülenen **Mozy** altında hello sağlayıcısı olarak seçilen **kimlik doğrulama İlkesi**.</span><span class="sxs-lookup"><span data-stu-id="f0057-220">hello **Add New User** option is only displayed only if **Mozy** is selected as hello provider under **Authentication policy**.</span></span> <span data-ttu-id="f0057-221">SAML kimlik doğrulaması yapılandırılmışsa, ardından hello kullanıcılar otomatik olarak çoklu oturum açma aracılığıyla kendi ilk oturum üzerinde üzerinde eklenir.</span><span class="sxs-lookup"><span data-stu-id="f0057-221">If SAML Authentication is configured, then hello users are added automatically on their first login through Single sign on.</span></span>
    
3. <span data-ttu-id="f0057-222">Merhaba yeni kullanıcı iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="f0057-222">On hello new user dialog, perform hello following steps:</span></span>
   
   <span data-ttu-id="f0057-223">![Kullanıcıları ekleme](./media/active-directory-saas-mozy-enterprise-tutorial/ic777318.png "kullanıcı ekleme")</span><span class="sxs-lookup"><span data-stu-id="f0057-223">![Add Users](./media/active-directory-saas-mozy-enterprise-tutorial/ic777318.png "Add Users")</span></span>
   
   <span data-ttu-id="f0057-224">a.</span><span class="sxs-lookup"><span data-stu-id="f0057-224">a.</span></span> <span data-ttu-id="f0057-225">Merhaba gelen **bir grubu seçin** listesinde, bir grup seçin.</span><span class="sxs-lookup"><span data-stu-id="f0057-225">From hello **Choose a Group** list, select a group.</span></span>
   
   <span data-ttu-id="f0057-226">b.</span><span class="sxs-lookup"><span data-stu-id="f0057-226">b.</span></span> <span data-ttu-id="f0057-227">Merhaba gelen **kullanıcı türüne** listesinde, bir tür seçin.</span><span class="sxs-lookup"><span data-stu-id="f0057-227">From hello **What type of user** list, select a type.</span></span>
   
   <span data-ttu-id="f0057-228">c.</span><span class="sxs-lookup"><span data-stu-id="f0057-228">c.</span></span> <span data-ttu-id="f0057-229">Merhaba, **kullanıcıadı** metin kutusuna, tür hello hello Azure AD kullanıcı adını.</span><span class="sxs-lookup"><span data-stu-id="f0057-229">In hello **Username** textbox, type hello name of hello Azure AD user.</span></span>
   
   <span data-ttu-id="f0057-230">d.</span><span class="sxs-lookup"><span data-stu-id="f0057-230">d.</span></span> <span data-ttu-id="f0057-231">Merhaba, **e-posta** metin kutusuna, hello Azure AD kullanıcısının hello e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="f0057-231">In hello **Email** textbox, type hello email address of hello Azure AD user.</span></span>
   
   <span data-ttu-id="f0057-232">e.</span><span class="sxs-lookup"><span data-stu-id="f0057-232">e.</span></span> <span data-ttu-id="f0057-233">Seçin **kullanıcı yönerge e-posta Gönder**.</span><span class="sxs-lookup"><span data-stu-id="f0057-233">Select **Send user instruction email**.</span></span>
   
   <span data-ttu-id="f0057-234">f.</span><span class="sxs-lookup"><span data-stu-id="f0057-234">f.</span></span> <span data-ttu-id="f0057-235">Tıklatın **kullanıcıları eklemek**.</span><span class="sxs-lookup"><span data-stu-id="f0057-235">Click **Add User(s)**.</span></span>

     >[!NOTE]
     > <span data-ttu-id="f0057-236">Merhaba kullanıcı oluşturduktan sonra onu etkinleştirilmeden önce bir bağlantı tooconfirm hello hesabı içeren toohello Azure AD kullanıcı bir e-posta gönderilir.</span><span class="sxs-lookup"><span data-stu-id="f0057-236">After creating hello user, an email will be sent toohello Azure AD user that includes a link tooconfirm hello account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f0057-237">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="f0057-237">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f0057-238">Bu bölümde, erişim tooMozy Kurumsal vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="f0057-238">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMozy Enterprise.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="f0057-240">**tooassign Britta Simon tooMozy Kurumsal hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f0057-240">**tooassign Britta Simon tooMozy Enterprise, perform hello following steps:**</span></span>

1. <span data-ttu-id="f0057-241">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="f0057-241">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="f0057-243">Merhaba uygulamalar listesinde **Mozy Kurumsal**.</span><span class="sxs-lookup"><span data-stu-id="f0057-243">In hello applications list, select **Mozy Enterprise**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_app.png) 

3. <span data-ttu-id="f0057-245">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="f0057-245">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="f0057-247">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f0057-247">Click **Add** button.</span></span> <span data-ttu-id="f0057-248">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="f0057-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="f0057-250">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="f0057-250">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f0057-251">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="f0057-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f0057-252">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="f0057-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f0057-253">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="f0057-253">Testing single sign-on</span></span>

<span data-ttu-id="f0057-254">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="f0057-254">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f0057-255">Mozy Kurumsal döşeme hello erişim paneli hello tıkladığınızda, Mozy Kurumsal uygulama oturum açma sayfasında almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f0057-255">When you click hello Mozy Enterprise tile in hello Access Panel, you should get login page of Mozy Enterprise application.</span></span>
<span data-ttu-id="f0057-256">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f0057-256">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f0057-257">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="f0057-257">Additional resources</span></span>

* [<span data-ttu-id="f0057-258">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="f0057-258">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f0057-259">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="f0057-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_203.png

