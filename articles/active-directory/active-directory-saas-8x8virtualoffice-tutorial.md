---
title: "Öğretici: Azure Active Directory Tümleştirme 8 x 8 sanal Office ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve 8 x 8 sanal Office arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b34a6edf-e745-4aec-b0b2-7337473d64c5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: df5c5de77285cd3912b68cc3b1e3eee274aa951c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-8x8-virtual-office"></a><span data-ttu-id="cce28-103">Öğretici: Azure Active Directory Tümleştirme 8 x 8 sanal Office ile</span><span class="sxs-lookup"><span data-stu-id="cce28-103">Tutorial: Azure Active Directory integration with 8x8 Virtual Office</span></span>

<span data-ttu-id="cce28-104">Bu öğreticide, bilgi nasıl toointegrate 8 x 8 sanal Office Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cce28-104">In this tutorial, you learn how toointegrate 8x8 Virtual Office with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cce28-105">8 x 8 tümleştirme Azure AD ile sanal Office ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="cce28-105">Integrating 8x8 Virtual Office with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="cce28-106">Sanal Office erişim too8x8 sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="cce28-106">You can control in Azure AD who has access too8x8 Virtual Office</span></span>
- <span data-ttu-id="cce28-107">Etkinleştirebilirsiniz tooautomatically almak, kullanıcılarınızın too8x8 sanal Office (çoklu oturum açma) ile Azure AD hesaplarına açan</span><span class="sxs-lookup"><span data-stu-id="cce28-107">You can enable your users tooautomatically get signed-on too8x8 Virtual Office (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cce28-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="cce28-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="cce28-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cce28-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cce28-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="cce28-110">Prerequisites</span></span>

<span data-ttu-id="cce28-111">tooconfigure 8 x 8 sanal Office ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="cce28-111">tooconfigure Azure AD integration with 8x8 Virtual Office, you need hello following items:</span></span>

- <span data-ttu-id="cce28-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="cce28-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cce28-113">Bir 8 x 8 sanal Office çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="cce28-113">A 8x8 Virtual Office single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cce28-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="cce28-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cce28-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="cce28-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cce28-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="cce28-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cce28-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cce28-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cce28-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="cce28-118">Scenario description</span></span>
<span data-ttu-id="cce28-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="cce28-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cce28-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="cce28-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cce28-121">8 x 8 sanal Office hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="cce28-121">Adding 8x8 Virtual Office from hello gallery</span></span>
2. <span data-ttu-id="cce28-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="cce28-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-8x8-virtual-office-from-hello-gallery"></a><span data-ttu-id="cce28-123">8 x 8 sanal Office hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="cce28-123">Adding 8x8 Virtual Office from hello gallery</span></span>
<span data-ttu-id="cce28-124">Azure AD'ye tooconfigure hello tümleştirme 8 x 8 sanal Office ihtiyacınız tooadd 8 x 8 sanal Office hello galeri tooyour listesinden yönetilen SaaS uygulamaları.</span><span class="sxs-lookup"><span data-stu-id="cce28-124">tooconfigure hello integration of 8x8 Virtual Office into Azure AD, you need tooadd 8x8 Virtual Office from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="cce28-125">**Merhaba Galeriden sanal Office tooadd 8 x 8 gerçekleştirmek hello adımları izleyin:**</span><span class="sxs-lookup"><span data-stu-id="cce28-125">**tooadd 8x8 Virtual Office from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="cce28-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="cce28-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cce28-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="cce28-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="cce28-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="cce28-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="cce28-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="cce28-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="cce28-133">Merhaba arama kutusuna yazın **8 x 8 sanal Office**.</span><span class="sxs-lookup"><span data-stu-id="cce28-133">In hello search box, type **8x8 Virtual Office**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_search.png)

5. <span data-ttu-id="cce28-135">Merhaba Sonuçlar panelinde seçin **8 x 8 sanal Office**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="cce28-135">In hello results panel, select **8x8 Virtual Office**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cce28-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="cce28-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cce28-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma 8 x 8 sanal Office "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı ile test etme</span><span class="sxs-lookup"><span data-stu-id="cce28-138">In this section, you configure and test Azure AD single sign-on with 8x8 Virtual Office based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="cce28-139">Tek toowork'ın oturum açma hangi hello karşılık gelen 8 x 8 sanal Office tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="cce28-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in 8x8 Virtual Office is tooa user in Azure AD.</span></span> <span data-ttu-id="cce28-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve hello ilgili kullanıcı 8 x 8 arasında bir bağlantı ilişkisi sanal Office kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="cce28-140">In other words, a link relationship between an Azure AD user and hello related user in 8x8 Virtual Office needs toobe established.</span></span>

<span data-ttu-id="cce28-141">8 x 8 sanal ofisinde hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="cce28-141">In 8x8 Virtual Office, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="cce28-142">tooconfigure ve 8 x 8 sanal Office ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="cce28-142">tooconfigure and test Azure AD single sign-on with 8x8 Virtual Office, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="cce28-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="cce28-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="cce28-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="cce28-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cce28-145">**[8 x 8 sanal Office test kullanıcısı oluşturma](#creating-a-8x8-virtual-office-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir 8 x 8 sanal Office, karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="cce28-145">**[Creating a 8x8 Virtual Office test user](#creating-a-8x8-virtual-office-test-user)** - toohave a counterpart of Britta Simon in 8x8 Virtual Office that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="cce28-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="cce28-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cce28-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="cce28-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cce28-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="cce28-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cce28-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma 8 x 8 sanal Office uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="cce28-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your 8x8 Virtual Office application.</span></span>

<span data-ttu-id="cce28-150">**Azure AD çoklu oturum açma tooconfigure 8 x 8 sanal Office ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="cce28-150">**tooconfigure Azure AD single sign-on with 8x8 Virtual Office, perform hello following steps:**</span></span>

1. <span data-ttu-id="cce28-151">Hello hello üzerinde Azure portal'ın **8 x 8 sanal Office** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="cce28-151">In hello Azure portal, on hello **8x8 Virtual Office** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="cce28-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="cce28-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_samlbase.png)

3. <span data-ttu-id="cce28-155">Merhaba üzerinde **8 x 8 sanal Office etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="cce28-155">On hello **8x8 Virtual Office Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_url.png)

    <span data-ttu-id="cce28-157">a.</span><span class="sxs-lookup"><span data-stu-id="cce28-157">a.</span></span> <span data-ttu-id="cce28-158">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:</span><span class="sxs-lookup"><span data-stu-id="cce28-158">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>

    <span data-ttu-id="cce28-159">| `https://sso.8x8.com/<companyname>` |
    | `https://www.8x8.com/<companyname>` |
    | `https://sso.8x8pilot.com/<companyname>` |</span><span class="sxs-lookup"><span data-stu-id="cce28-159">| `https://sso.8x8.com/<companyname>` |
 | `https://www.8x8.com/<companyname>` |
 | `https://sso.8x8pilot.com/<companyname>` |</span></span>

    <span data-ttu-id="cce28-160">b.</span><span class="sxs-lookup"><span data-stu-id="cce28-160">b.</span></span> <span data-ttu-id="cce28-161">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:</span><span class="sxs-lookup"><span data-stu-id="cce28-161">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>

    <span data-ttu-id="cce28-162">| `https://<subdomain>.8x8.com/saml2` |
    | `https://<subdomain>.8x8pilot.com/saml2`|</span><span class="sxs-lookup"><span data-stu-id="cce28-162">| `https://<subdomain>.8x8.com/saml2` |
 | `https://<subdomain>.8x8pilot.com/saml2`|</span></span>

    > [!NOTE] 
    > <span data-ttu-id="cce28-163">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="cce28-163">These values are not real.</span></span> <span data-ttu-id="cce28-164">Bu değerleri hello gerçek tanımlayıcısı ve yanıt URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="cce28-164">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="cce28-165">Kişi [8 x 8 sanal Office destek ekibi](https://www.8x8.com/about-us/contact-us) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="cce28-165">Contact [8x8 Virtual Office support team](https://www.8x8.com/about-us/contact-us) tooget these values.</span></span>
 


4. <span data-ttu-id="cce28-166">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (ham)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="cce28-166">On hello **SAML Signing Certificate** section, click **Certificate (Raw)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_certificate.png) 

5. <span data-ttu-id="cce28-168">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="cce28-168">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="cce28-170">Merhaba üzerinde **8 x 8 sanal Office yapılandırma** 'yi tıklatın **yapılandırma 8 x 8 sanal Office** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="cce28-170">On hello **8x8 Virtual Office Configuration** section, click **Configure 8x8 Virtual Office** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="cce28-171">Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="cce28-171">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_configure.png) 

7. <span data-ttu-id="cce28-173">Yönetici olarak oturum açma tooyour 8 x 8 sanal Office Kiracı.</span><span class="sxs-lookup"><span data-stu-id="cce28-173">Sign-on tooyour 8x8 Virtual Office tenant as an administrator.</span></span>

8. <span data-ttu-id="cce28-174">Seçin **sanal Office hesap Mgr** uygulama panelindeki.</span><span class="sxs-lookup"><span data-stu-id="cce28-174">Select **Virtual Office Account Mgr** on Application Panel.</span></span>
   
    ![Uygulama tarafında yapılandırma](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_001.png)

9. <span data-ttu-id="cce28-176">Seçin **iş** toomanage hesap ve tıklatın **oturum** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="cce28-176">Select **Business** account toomanage and click **Sign In** button.</span></span>
   
    ![Uygulama tarafında yapılandırma](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_002.png)

10. <span data-ttu-id="cce28-178">Tıklatın **hesapları** hello menü listesi sekmesindedir.</span><span class="sxs-lookup"><span data-stu-id="cce28-178">Click **Accounts** tab in hello menu list.</span></span>
   
    ![Uygulama tarafında yapılandırma](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_003.png)

11. <span data-ttu-id="cce28-180">Tıklatın **çoklu oturum açma** hesapları hello listesinde.</span><span class="sxs-lookup"><span data-stu-id="cce28-180">Click **Single Sign On** in hello list of Accounts.</span></span>
   
    ![Uygulama tarafında yapılandırma](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_004.png)

12. <span data-ttu-id="cce28-182">Seçin **çoklu oturum açma** kimlik doğrulama yöntemi ve tıklatın altında **SAML**.</span><span class="sxs-lookup"><span data-stu-id="cce28-182">Select **Single Sign On** under Authentication method and click **SAML**.</span></span>
    
    ![Uygulama tarafında yapılandırma](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_005.png)

13. <span data-ttu-id="cce28-184">Kopya **SAML SSO URL**, **tek oturum kapatma hizmeti URL'sini** ve **veren URL'si** Azure AD'den çok**oturum açma URL'si**, **oturum kapatma URL'si**  ve **veren URL'si** 8 x 8 sanal Office.</span><span class="sxs-lookup"><span data-stu-id="cce28-184">Copy **SAML SSO URL**, **Single Sing Out Service URL** and **Issuer URL** from Azure AD too**Sign In URL**, **Sign Out URL** and **Issuer URL** in 8x8 Virtual Office.</span></span> 
    
    ![Uygulama tarafında yapılandırma](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_006.png)
    
14. <span data-ttu-id="cce28-186">Tıklatın **tarayıcı** düğmesine Azure AD'den indirilen tooupload hello sertifika hello tıklayın ve **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="cce28-186">Click **Browser** button tooupload hello certificate which you downloaded from Azure AD, and click hello **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="cce28-187">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="cce28-187">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="cce28-188">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="cce28-188">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="cce28-189">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cce28-189">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cce28-190">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="cce28-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="cce28-191">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="cce28-191">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="cce28-193">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="cce28-193">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="cce28-194">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="cce28-194">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cce28-196">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="cce28-196">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cce28-198">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="cce28-198">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cce28-200">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="cce28-200">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cce28-202">a.</span><span class="sxs-lookup"><span data-stu-id="cce28-202">a.</span></span> <span data-ttu-id="cce28-203">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cce28-203">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cce28-204">b.</span><span class="sxs-lookup"><span data-stu-id="cce28-204">b.</span></span> <span data-ttu-id="cce28-205">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="cce28-205">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cce28-206">c.</span><span class="sxs-lookup"><span data-stu-id="cce28-206">c.</span></span> <span data-ttu-id="cce28-207">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="cce28-207">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="cce28-208">d.</span><span class="sxs-lookup"><span data-stu-id="cce28-208">d.</span></span> <span data-ttu-id="cce28-209">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="cce28-209">Click **Create**.</span></span>
 
### <a name="creating-a-8x8-virtual-office-test-user"></a><span data-ttu-id="cce28-210">8 x 8 sanal Office test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="cce28-210">Creating a 8x8 Virtual Office test user</span></span>

<span data-ttu-id="cce28-211">Bu bölümde Hello amacı toocreate 8 x 8 sanal ofisinde Britta Simon adlı bir kullanıcı var.</span><span class="sxs-lookup"><span data-stu-id="cce28-211">hello objective of this section is toocreate a user called Britta Simon in 8x8 Virtual Office.</span></span> <span data-ttu-id="cce28-212">8 x 8 sanal Office henüz zaman sağlama, varsayılan olarak etkin olduğu destekler.</span><span class="sxs-lookup"><span data-stu-id="cce28-212">8x8 Virtual Office supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="cce28-213">Bu bölümde, eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="cce28-213">There is no action item for you in this section.</span></span> <span data-ttu-id="cce28-214">Henüz yoksa yeni bir kullanıcı sanal Office girişimi tooaccess 8 x 8 sırasında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="cce28-214">A new user is created during an attempt tooaccess 8x8 Virtual Office if it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="cce28-215">Toocreate kullanıcı el ile gerekiyorsa, toocontact hello gereksinim [8 x 8 sanal Office destek ekibi](https://www.8x8.com/about-us/contact-us).</span><span class="sxs-lookup"><span data-stu-id="cce28-215">If you need toocreate a user manually, you need toocontact hello [8x8 Virtual Office support team](https://www.8x8.com/about-us/contact-us).</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="cce28-216">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="cce28-216">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="cce28-217">Bu bölümde, Britta Simon etkinleştirme verme tarafından toouse Azure çoklu oturum açma too8x8 sanal Office erişim.</span><span class="sxs-lookup"><span data-stu-id="cce28-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access too8x8 Virtual Office.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="cce28-219">**tooassign Britta Simon too8x8 sanal Office, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="cce28-219">**tooassign Britta Simon too8x8 Virtual Office, perform hello following steps:**</span></span>

1. <span data-ttu-id="cce28-220">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="cce28-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="cce28-222">Merhaba uygulamalar listesinde **8 x 8 sanal Office**.</span><span class="sxs-lookup"><span data-stu-id="cce28-222">In hello applications list, select **8x8 Virtual Office**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_app.png) 

3. <span data-ttu-id="cce28-224">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="cce28-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="cce28-226">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="cce28-226">Click **Add** button.</span></span> <span data-ttu-id="cce28-227">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="cce28-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="cce28-229">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="cce28-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="cce28-230">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="cce28-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cce28-231">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="cce28-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cce28-232">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="cce28-232">Testing single sign-on</span></span>

<span data-ttu-id="cce28-233">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="cce28-233">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="cce28-234">Merhaba 8 x 8 sanal Office hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour 8 x 8 sanal Office uygulaması almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="cce28-234">When you click hello 8x8 Virtual Office tile in hello Access Panel, you should get automatically signed-on tooyour 8x8 Virtual Office application.</span></span>
<span data-ttu-id="cce28-235">Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="cce28-235">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md)</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cce28-236">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="cce28-236">Additional resources</span></span>

* [<span data-ttu-id="cce28-237">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="cce28-237">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cce28-238">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="cce28-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_203.png

