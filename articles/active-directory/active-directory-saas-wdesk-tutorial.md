---
title: "Öğretici: Azure Active Directory Tümleştirme ile Wdesk | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Wdesk arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 06900a91-a326-4663-8ba6-69ae741a536e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 2c278a5e4f50cc362663efc0f826ff0c0fcf6e7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wdesk"></a><span data-ttu-id="2b9b4-103">Öğretici: Azure Active Directory Tümleştirme Wdesk ile</span><span class="sxs-lookup"><span data-stu-id="2b9b4-103">Tutorial: Azure Active Directory integration with Wdesk</span></span>

<span data-ttu-id="2b9b4-104">Bu öğreticide, bilgi nasıl toointegrate Wdesk Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2b9b4-104">In this tutorial, you learn how toointegrate Wdesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2b9b4-105">Wdesk Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="2b9b4-105">Integrating Wdesk with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2b9b4-106">Erişim tooWdesk sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="2b9b4-106">You can control in Azure AD who has access tooWdesk</span></span>
- <span data-ttu-id="2b9b4-107">Kullanıcıların tooautomatically get açan tooWdesk (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="2b9b4-107">You can enable your users tooautomatically get signed-on tooWdesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2b9b4-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="2b9b4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="2b9b4-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="2b9b4-110">[Uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2b9b4-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2b9b4-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="2b9b4-111">Prerequisites</span></span>

<span data-ttu-id="2b9b4-112">tooconfigure Wdesk ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="2b9b4-112">tooconfigure Azure AD integration with Wdesk, you need hello following items:</span></span>

- <span data-ttu-id="2b9b4-113">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="2b9b4-113">An Azure AD subscription</span></span>
- <span data-ttu-id="2b9b4-114">Bir Wdesk çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="2b9b4-114">A Wdesk single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2b9b4-115">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2b9b4-116">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="2b9b4-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2b9b4-117">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2b9b4-118">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2b9b4-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2b9b4-119">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="2b9b4-119">Scenario description</span></span>
<span data-ttu-id="2b9b4-120">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2b9b4-121">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="2b9b4-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2b9b4-122">Merhaba Galerisi'nden Wdesk ekleme</span><span class="sxs-lookup"><span data-stu-id="2b9b4-122">Adding Wdesk from hello gallery</span></span>
2. <span data-ttu-id="2b9b4-123">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="2b9b4-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-wdesk-from-hello-gallery"></a><span data-ttu-id="2b9b4-124">Merhaba Galerisi'nden Wdesk ekleme</span><span class="sxs-lookup"><span data-stu-id="2b9b4-124">Adding Wdesk from hello gallery</span></span>
<span data-ttu-id="2b9b4-125">Azure AD'ye tooconfigure hello tümleştirme Wdesk, tooadd Wdesk hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-125">tooconfigure hello integration of Wdesk into Azure AD, you need tooadd Wdesk from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2b9b4-126">**tooadd Wdesk hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2b9b4-126">**tooadd Wdesk from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2b9b4-127">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2b9b4-129">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2b9b4-130">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-130">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="2b9b4-132">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="2b9b4-134">Merhaba arama kutusuna yazın **Wdesk**.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-134">In hello search box, type **Wdesk**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_search.png)

5. <span data-ttu-id="2b9b4-136">Merhaba Sonuçlar panelinde seçin **Wdesk**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-136">In hello results panel, select **Wdesk**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2b9b4-138">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="2b9b4-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2b9b4-139">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Wdesk ile test etme</span><span class="sxs-lookup"><span data-stu-id="2b9b4-139">In this section, you configure and test Azure AD single sign-on with Wdesk based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="2b9b4-140">Tek toowork'ın oturum açma hangi hello karşılık gelen Wdesk içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Wdesk is tooa user in Azure AD.</span></span> <span data-ttu-id="2b9b4-141">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Wdesk hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-141">In other words, a link relationship between an Azure AD user and hello related user in Wdesk needs toobe established.</span></span>

<span data-ttu-id="2b9b4-142">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** Wdesk içinde.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Wdesk.</span></span>

<span data-ttu-id="2b9b4-143">tooconfigure ve Wdesk ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="2b9b4-143">tooconfigure and test Azure AD single sign-on with Wdesk, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2b9b4-144">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2b9b4-145">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2b9b4-146">**[Wdesk test kullanıcısı oluşturma](#creating-a-wdesk-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Wdesk içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-146">**[Creating a Wdesk test user](#creating-a-wdesk-test-user)** - toohave a counterpart of Britta Simon in Wdesk that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="2b9b4-147">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2b9b4-148">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2b9b4-149">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="2b9b4-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2b9b4-150">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Wdesk uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Wdesk application.</span></span>

<span data-ttu-id="2b9b4-151">**tooconfigure Azure AD çoklu oturum açma ile Wdesk, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2b9b4-151">**tooconfigure Azure AD single sign-on with Wdesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="2b9b4-152">Hello hello üzerinde Azure portal'ın **Wdesk** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-152">In hello Azure portal, on hello **Wdesk** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="2b9b4-154">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_samlbase.png)

3. <span data-ttu-id="2b9b4-156">Merhaba üzerinde **Wdesk etki alanı ve URL'leri** tooconfigure hello uygulamada isterseniz, bölümü **IDP** başlatılan modu hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2b9b4-156">On hello **Wdesk Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_url.png)

    <span data-ttu-id="2b9b4-158">a.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-158">a.</span></span> <span data-ttu-id="2b9b4-159">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.wdesk.com/auth/saml/sp/metadata/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="2b9b4-159">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.wdesk.com/auth/saml/sp/metadata/<instancename>`</span></span>

    <span data-ttu-id="2b9b4-160">b.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-160">b.</span></span> <span data-ttu-id="2b9b4-161">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.wdesk.com/auth/saml/sp/consumer/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="2b9b4-161">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.wdesk.com/auth/saml/sp/consumer/<instancename>`</span></span>

4. <span data-ttu-id="2b9b4-162">Denetleme **Göster Gelişmiş URL ayarları**.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-162">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="2b9b4-163">Tooconfigure hello uygulamada istiyorsanız **SP** modunda başlatılan adım aşağıdaki hello gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2b9b4-163">If you wish tooconfigure hello application in **SP** initiated mode, perform hello following step:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_url1.png)

    <span data-ttu-id="2b9b4-165">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.wdesk.com/auth/login/saml/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="2b9b4-165">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.wdesk.com/auth/login/saml/<instancename>`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="2b9b4-166">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-166">These values are not real.</span></span> <span data-ttu-id="2b9b4-167">Bu güncelleştirme tanımlayıcısı, yanıt URL'si ve oturum açma URL'si ile Merhaba gerçek değerler.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-167">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="2b9b4-168">Merhaba SSO yapılandırdığınızda WDesk Portalı'ndan bu değerleri alır.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-168">You get these values from WDesk portal when you configure hello SSO.</span></span> 
  
5. <span data-ttu-id="2b9b4-169">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-169">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_certificate.png) 

6. <span data-ttu-id="2b9b4-171">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-171">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-wdesk-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="2b9b4-173">Bir farklı web tarayıcısı penceresinde, bir güvenlik yöneticisi olarak oturum açma tooWdesk.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-173">In a different web browser window, login tooWdesk as a Security Administrator.</span></span>

8. <span data-ttu-id="2b9b4-174">Merhaba alt sol tıklayın **yönetici** ve **Hesap Yöneticisi**:</span><span class="sxs-lookup"><span data-stu-id="2b9b4-174">In hello bottom left, click **Admin** and choose **Account Admin**:</span></span>
 
     ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig1.png)

9. <span data-ttu-id="2b9b4-176">Wdesk Yöneticisi çok gidin**güvenlik**, ardından **SAML** > **SAML ayarları**:</span><span class="sxs-lookup"><span data-stu-id="2b9b4-176">In Wdesk Admin, navigate too**Security**, then **SAML** > **SAML Settings**:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig2.png)

10. <span data-ttu-id="2b9b4-178">Altında **genel ayarları**, hello denetleyin **SAML çoklu oturum açmayı etkinleştir**:</span><span class="sxs-lookup"><span data-stu-id="2b9b4-178">Under **General Settings**, check hello **Enable SAML Single Sign On**:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig3.png)

11. <span data-ttu-id="2b9b4-180">Altında **hizmet sağlayıcı ayrıntıları**, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2b9b4-180">Under **Service Provider Details**, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig4.png)

      <span data-ttu-id="2b9b4-182">a.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-182">a.</span></span> <span data-ttu-id="2b9b4-183">Kopya hello **oturum açma URL'si** ve yapıştırın **oturum açma URL'si** Azure Portal'daki metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-183">Copy hello **Login URL** and paste it in **Sign-on Url** textbox on Azure portal.</span></span>
   
      <span data-ttu-id="2b9b4-184">b.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-184">b.</span></span> <span data-ttu-id="2b9b4-185">Kopya hello **meta veri URL'sini** ve yapıştırın **tanımlayıcısı** Azure Portal'daki metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-185">Copy hello **Metadata Url** and paste it in **Identifier** textbox on Azure portal.</span></span>
       
      <span data-ttu-id="2b9b4-186">c.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-186">c.</span></span> <span data-ttu-id="2b9b4-187">Kopya hello **tüketici url** ve yapıştırın **yanıt URL'si** Azure Portal'daki metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-187">Copy hello **Consumer url** and paste it in **Reply Url** textbox on Azure portal.</span></span>
   
      <span data-ttu-id="2b9b4-188">d.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-188">d.</span></span> <span data-ttu-id="2b9b4-189">Tıklatın **kaydetmek** Azure portal toosave hello değişir.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-189">Click **Save** on Azure portal toosave hello changes.</span></span>      

12. <span data-ttu-id="2b9b4-190">Tıklatın **IDP ayarlarını yapılandır** tooopen **IDP ayarlarını Düzenle** iletişim.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-190">Click **Configure IdP Settings** tooopen **Edit IdP Settings** dialog.</span></span> <span data-ttu-id="2b9b4-191">Tıklatın **Dosya Seç** toolocate hello **Metadata.xml** Azure portalından, kaydettiğiniz dosyayı karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-191">Click **Choose File** toolocate hello **Metadata.xml** file you saved from Azure portal, then upload it.</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig5.png)
  
13. <span data-ttu-id="2b9b4-193">Tıklatın **değişiklikleri kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-193">Click **Save changes**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfigsavebutton.png)

> [!TIP]
> <span data-ttu-id="2b9b4-195">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="2b9b4-195">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2b9b4-196">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-196">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2b9b4-197">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2b9b4-197">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2b9b4-198">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="2b9b4-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="2b9b4-199">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-199">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="2b9b4-201">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2b9b4-201">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2b9b4-202">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-202">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-wdesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2b9b4-204">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-204">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-wdesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2b9b4-206">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-206">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-wdesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2b9b4-208">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2b9b4-208">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-wdesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2b9b4-210">a.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-210">a.</span></span> <span data-ttu-id="2b9b4-211">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-211">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2b9b4-212">b.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-212">b.</span></span> <span data-ttu-id="2b9b4-213">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-213">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2b9b4-214">c.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-214">c.</span></span> <span data-ttu-id="2b9b4-215">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-215">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="2b9b4-216">d.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-216">d.</span></span> <span data-ttu-id="2b9b4-217">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-217">Click **Create**.</span></span>
 
### <a name="creating-a-wdesk-test-user"></a><span data-ttu-id="2b9b4-218">Wdesk test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="2b9b4-218">Creating a Wdesk test user</span></span>

<span data-ttu-id="2b9b4-219">tooenable Azure AD kullanıcıların toolog tooWdesk bunların Wdesk sağlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-219">tooenable Azure AD users toolog in tooWdesk, they must be provisioned into Wdesk.</span></span> <span data-ttu-id="2b9b4-220">Wdesk içinde sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-220">In Wdesk, provisioning is a manual task.</span></span>

<span data-ttu-id="2b9b4-221">**bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2b9b4-221">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="2b9b4-222">İçinde tooWdesk güvenlik yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-222">Log in tooWdesk as a Security Administrator.</span></span>
2. <span data-ttu-id="2b9b4-223">Çok gidin**yönetici** > **Hesap Yöneticisi**.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-223">Navigate too**Admin** > **Account Admin**.</span></span>

     ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig1.png)

3. <span data-ttu-id="2b9b4-225">Tıklatın **üyeleri** altında **kişiler**.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-225">Click **Members** under **People**.</span></span>

4. <span data-ttu-id="2b9b4-226">Şimdi **Üye Ekle** tooopen **Üye Ekle** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-226">Now click **Add Member** tooopen **Add Member** dialog box.</span></span> 
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-wdesk-tutorial/createuser1.png)  

5. <span data-ttu-id="2b9b4-228">İçinde **kullanıcı** metin kutusuna, kullanıcının gibi hello kullanıcı adı girin  **brittasimon@contoso.com**  tıklatıp **devam** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-228">In **User** text box, enter hello username of user like **brittasimon@contoso.com** and click **Continue** button.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-wdesk-tutorial/createuser3.png)

6.  <span data-ttu-id="2b9b4-230">Aşağıda gösterildiği gibi Hello ayrıntılarını girin:</span><span class="sxs-lookup"><span data-stu-id="2b9b4-230">Enter hello details as shown below:</span></span>
  
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-wdesk-tutorial/createuser4.png)
 
    <span data-ttu-id="2b9b4-232">a.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-232">a.</span></span> <span data-ttu-id="2b9b4-233">İçinde **e-posta** metin kutusunda, bir kullanıcı gibi hello e-posta girin  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="2b9b4-233">In **E-mail** text box, enter hello email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="2b9b4-234">b.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-234">b.</span></span> <span data-ttu-id="2b9b4-235">İçinde **ad** metin kutusuna, hello ilk gibi kullanıcı adını girin **Britta**.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-235">In **First Name** text box, enter hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="2b9b4-236">c.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-236">c.</span></span> <span data-ttu-id="2b9b4-237">İçinde **Soyadı** metin kutusuna, hello kullanıcının soyadını gibi girin **Simon**.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-237">In **Last Name** text box, enter hello last name of user like **Simon**.</span></span>

7. <span data-ttu-id="2b9b4-238">Tıklatın **Save Member** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-238">Click **Save Member** button.</span></span>  

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-wdesk-tutorial/createuser5.png)

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="2b9b4-240">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="2b9b4-240">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="2b9b4-241">Bu bölümde, erişim tooWdesk vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-241">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWdesk.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="2b9b4-243">**tooassign Britta Simon tooWdesk hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2b9b4-243">**tooassign Britta Simon tooWdesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="2b9b4-244">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-244">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="2b9b4-246">Merhaba uygulamalar listesinde **Wdesk**.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-246">In hello applications list, select **Wdesk**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_app.png) 

3. <span data-ttu-id="2b9b4-248">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-248">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="2b9b4-250">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-250">Click **Add** button.</span></span> <span data-ttu-id="2b9b4-251">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-251">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="2b9b4-253">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-253">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2b9b4-254">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-254">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2b9b4-255">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-255">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2b9b4-256">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="2b9b4-256">Testing single sign-on</span></span>

<span data-ttu-id="2b9b4-257">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-257">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="2b9b4-258">Merhaba Wdesk hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Wdesk uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2b9b4-258">When you click hello Wdesk tile in hello Access Panel, you should get automatically signed-on tooyour Wdesk application.</span></span>
<span data-ttu-id="2b9b4-259">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2b9b4-259">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="2b9b4-260">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="2b9b4-260">Additional resources</span></span>

* [<span data-ttu-id="2b9b4-261">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="2b9b4-261">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2b9b4-262">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="2b9b4-262">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_203.png

