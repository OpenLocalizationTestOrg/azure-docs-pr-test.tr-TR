---
title: "Öğretici: Azure Active Directory Tümleştirme ile Netsuite | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Netsuite arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dafa0864-aef2-4f5e-9eac-770504688ef4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 7cf205d5bda5333872fb589e57f4779a8670b595
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-netsuite"></a><span data-ttu-id="e1700-103">Öğretici: Azure Active Directory Tümleştirme Netsuite ile</span><span class="sxs-lookup"><span data-stu-id="e1700-103">Tutorial: Azure Active Directory integration with Netsuite</span></span>

<span data-ttu-id="e1700-104">Bu öğreticide, bilgi nasıl toointegrate Netsuite Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e1700-104">In this tutorial, you learn how toointegrate Netsuite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e1700-105">Netsuite Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="e1700-105">Integrating Netsuite with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e1700-106">Erişim tooNetsuite sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="e1700-106">You can control in Azure AD who has access tooNetsuite</span></span>
- <span data-ttu-id="e1700-107">Kullanıcıların tooautomatically get açan tooNetsuite (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="e1700-107">You can enable your users tooautomatically get signed-on tooNetsuite (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e1700-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="e1700-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e1700-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e1700-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e1700-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e1700-110">Prerequisites</span></span>

<span data-ttu-id="e1700-111">tooconfigure Netsuite ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="e1700-111">tooconfigure Azure AD integration with Netsuite, you need hello following items:</span></span>

- <span data-ttu-id="e1700-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="e1700-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e1700-113">Bir Netsuite çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="e1700-113">A Netsuite single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e1700-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="e1700-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e1700-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="e1700-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e1700-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="e1700-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e1700-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e1700-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e1700-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="e1700-118">Scenario description</span></span>
<span data-ttu-id="e1700-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="e1700-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e1700-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="e1700-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e1700-121">Merhaba Galerisi'nden Netsuite ekleme</span><span class="sxs-lookup"><span data-stu-id="e1700-121">Adding Netsuite from hello gallery</span></span>
2. <span data-ttu-id="e1700-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="e1700-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-netsuite-from-hello-gallery"></a><span data-ttu-id="e1700-123">Merhaba Galerisi'nden Netsuite ekleme</span><span class="sxs-lookup"><span data-stu-id="e1700-123">Adding Netsuite from hello gallery</span></span>
<span data-ttu-id="e1700-124">Azure AD'ye tooconfigure hello tümleştirme Netsuite, tooadd Netsuite hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="e1700-124">tooconfigure hello integration of Netsuite into Azure AD, you need tooadd Netsuite from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e1700-125">**tooadd Netsuite hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e1700-125">**tooadd Netsuite from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e1700-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="e1700-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e1700-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="e1700-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e1700-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="e1700-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="e1700-131">Tıklatın **yeni uygulama** hello iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e1700-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="e1700-133">Merhaba arama kutusuna yazın **Netsuite**.</span><span class="sxs-lookup"><span data-stu-id="e1700-133">In hello search box, type **Netsuite**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_search.png)

5. <span data-ttu-id="e1700-135">Merhaba Sonuçlar panelinde seçin **Netsuite**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="e1700-135">In hello results panel, select **Netsuite**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e1700-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="e1700-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e1700-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Netsuite ile test etme</span><span class="sxs-lookup"><span data-stu-id="e1700-138">In this section, you configure and test Azure AD single sign-on with Netsuite based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e1700-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Netsuite içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="e1700-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Netsuite is tooa user in Azure AD.</span></span> <span data-ttu-id="e1700-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Netsuite hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="e1700-140">In other words, a link relationship between an Azure AD user and hello related user in Netsuite needs toobe established.</span></span>

<span data-ttu-id="e1700-141">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** Netsuite içinde.</span><span class="sxs-lookup"><span data-stu-id="e1700-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Netsuite.</span></span>

<span data-ttu-id="e1700-142">tooconfigure ve Netsuite ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="e1700-142">tooconfigure and test Azure AD single sign-on with Netsuite, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e1700-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="e1700-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e1700-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="e1700-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e1700-145">**[Netsuite test kullanıcısı oluşturma](#creating-a-netsuite-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Netsuite içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="e1700-145">**[Creating a Netsuite test user](#creating-a-netsuite-test-user)** - toohave a counterpart of Britta Simon in Netsuite that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e1700-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="e1700-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e1700-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="e1700-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e1700-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e1700-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e1700-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Netsuite uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="e1700-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Netsuite application.</span></span>

<span data-ttu-id="e1700-150">**tooconfigure Azure AD çoklu oturum açma ile Netsuite, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e1700-150">**tooconfigure Azure AD single sign-on with Netsuite, perform hello following steps:**</span></span>

1. <span data-ttu-id="e1700-151">Hello hello üzerinde Azure portal'ın **Netsuite** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="e1700-151">In hello Azure portal, on hello **Netsuite** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="e1700-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="e1700-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_samlbase.png)

3. <span data-ttu-id="e1700-155">Merhaba üzerinde **Netsuite etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e1700-155">On hello **Netsuite Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_url.png)

    <span data-ttu-id="e1700-157">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın: `https://<tenant-name>.netsuite.com/saml2/acs` `https://<tenant-name>.na1.netsuite.com/saml2/acs` `https://<tenant-name>.na2.netsuite.com/saml2/acs` `https://<tenant-name>.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na1.sandbox.netsuite.com/saml2/acs``https://<tenant-name>.na2.sandbox.netsuite.com/saml2/acs`</span><span class="sxs-lookup"><span data-stu-id="e1700-157">In hello **Reply URL** textbox, type a URL using hello following pattern:   `https://<tenant-name>.netsuite.com/saml2/acs` `https://<tenant-name>.na1.netsuite.com/saml2/acs` `https://<tenant-name>.na2.netsuite.com/saml2/acs` `https://<tenant-name>.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na1.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na2.sandbox.netsuite.com/saml2/acs`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e1700-158">Bu değer gerçek değeri değil.</span><span class="sxs-lookup"><span data-stu-id="e1700-158">This value is not real value.</span></span> <span data-ttu-id="e1700-159">Güncelleştirme hello değerle hello gerçek yanıt URL'si.</span><span class="sxs-lookup"><span data-stu-id="e1700-159">Update hello value with hello actual Reply URL.</span></span> <span data-ttu-id="e1700-160">Kişi [Netsuite destek ekibi](http://www.netsuite.com/portal/services/support.shtml) tooget bu değer.</span><span class="sxs-lookup"><span data-stu-id="e1700-160">Contact [Netsuite support team](http://www.netsuite.com/portal/services/support.shtml) tooget this value.</span></span>
 
4. <span data-ttu-id="e1700-161">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello XML dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e1700-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_certificate.png) 

5. <span data-ttu-id="e1700-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e1700-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-netsuite-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e1700-165">Merhaba üzerinde **Netsuite yapılandırma** 'yi tıklatın **yapılandırma Netsuite** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="e1700-165">On hello **Netsuite Configuration** section, click **Configure Netsuite** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="e1700-166">Kopya hello **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="e1700-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_configure.png) 

7. <span data-ttu-id="e1700-168">Tarayıcınızda yeni bir sekme açın ve Netsuite şirket sitenizin yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="e1700-168">Open a new tab in your browser, and sign into your Netsuite company site as an administrator.</span></span>

8. <span data-ttu-id="e1700-169">Merhaba sayfanın üst kısmındaki hello Hello araç çubuğunda **Kurulum**, ardından **Kurulum Yöneticisi**.</span><span class="sxs-lookup"><span data-stu-id="e1700-169">In hello toolbar at hello top of hello page, click **Setup**, then click **Setup Manager**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

9. <span data-ttu-id="e1700-171">Merhaba gelen **kurulum görevlerini** listesinde **tümleştirme**.</span><span class="sxs-lookup"><span data-stu-id="e1700-171">From hello **Setup Tasks** list, select **Integration**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-Netsuite-tutorial/ns-integration.png)

10. <span data-ttu-id="e1700-173">Merhaba, **yönetmek kimlik doğrulama** 'yi tıklatın **SAML çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="e1700-173">In hello **Manage Authentication** section, click **SAML Single Sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-Netsuite-tutorial/ns-saml.png)

11. <span data-ttu-id="e1700-175">Merhaba üzerinde **SAML Kurulumu** sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e1700-175">On hello **SAML Setup** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="e1700-176">a.</span><span class="sxs-lookup"><span data-stu-id="e1700-176">a.</span></span> <span data-ttu-id="e1700-177">Kopya hello **SAML çoklu oturum açma hizmet URL'si** değeri **hızlı başvuru** bölümünü **yapılandırma oturum açma** ve hello yapıştırma **kimlik sağlayıcısı Oturum açma sayfasına** Netsuite alanındaki.</span><span class="sxs-lookup"><span data-stu-id="e1700-177">Copy hello **SAML Single Sign-On Service URL** value from **Quick Reference** section of **Configure sign-on** and paste it into hello **Identity Provider Login Page** field in Netsuite.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-netsuite-tutorial/ns-saml-setup.png)
  
    <span data-ttu-id="e1700-179">b.</span><span class="sxs-lookup"><span data-stu-id="e1700-179">b.</span></span> <span data-ttu-id="e1700-180">Netsuite içinde seçin **birincil kimlik doğrulama yöntemini**.</span><span class="sxs-lookup"><span data-stu-id="e1700-180">In Netsuite, select **Primary Authentication Method**.</span></span>

    <span data-ttu-id="e1700-181">c.</span><span class="sxs-lookup"><span data-stu-id="e1700-181">c.</span></span> <span data-ttu-id="e1700-182">Etiketli hello alan için **SAMLV2 kimlik sağlayıcısı meta verileri**seçin **IDP meta veri dosyasını karşıya yükle**.</span><span class="sxs-lookup"><span data-stu-id="e1700-182">For hello field labeled **SAMLV2 Identity Provider Metadata**, select **Upload IDP Metadata File**.</span></span> <span data-ttu-id="e1700-183">Ardından **Gözat** Azure portalından indirdiğiniz tooupload hello meta veri dosyası.</span><span class="sxs-lookup"><span data-stu-id="e1700-183">Then click **Browse** tooupload hello metadata file that you downloaded from Azure portal.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-netsuite-tutorial/ns-sso-setup.png)

    <span data-ttu-id="e1700-185">d.</span><span class="sxs-lookup"><span data-stu-id="e1700-185">d.</span></span> <span data-ttu-id="e1700-186">Tıklatın **gönderme**.</span><span class="sxs-lookup"><span data-stu-id="e1700-186">Click **Submit**.</span></span>

12. <span data-ttu-id="e1700-187">Azure AD'de tıklayın **Görünüm ve diğer tüm kullanıcı özniteliklerini düzenleme** onay kutusunu ve özniteliğini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e1700-187">In Azure AD, Click on **View and edit all other user attributes** check-box and add attribute.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-Netsuite-tutorial/ns-attributes.png)

13. <span data-ttu-id="e1700-189">Hello için **öznitelik adı** alan, yazın `account`.</span><span class="sxs-lookup"><span data-stu-id="e1700-189">For hello **Attribute Name** field, type in `account`.</span></span> <span data-ttu-id="e1700-190">Hello için **öznitelik değeri** alanında, Netsuite hesabı kimliğinizi yazın Bu, sabit ve hesap değişiklikle değerdir.</span><span class="sxs-lookup"><span data-stu-id="e1700-190">For hello **Attribute Value** field, type in your Netsuite account ID.This value is constant and change with account.</span></span> <span data-ttu-id="e1700-191">Yönergeler toofind hesabı Kimliğiniz aşağıda bulunmaktadır:</span><span class="sxs-lookup"><span data-stu-id="e1700-191">Instructions on how toofind your account ID are included below:</span></span>

      ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-Netsuite-tutorial/ns-add-attribute.png)

    <span data-ttu-id="e1700-193">a.</span><span class="sxs-lookup"><span data-stu-id="e1700-193">a.</span></span> <span data-ttu-id="e1700-194">Netsuite içinde tıklatın **Kurulum** hello üst gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="e1700-194">In Netsuite, click **Setup** from hello top navigation menu.</span></span>

    <span data-ttu-id="e1700-195">b.</span><span class="sxs-lookup"><span data-stu-id="e1700-195">b.</span></span> <span data-ttu-id="e1700-196">Hello altında ardından **kurulum görevlerini** hello sol gezinti menüsünde, select hello bölümünü **tümleştirme** bölüm ve'ı tıklatın **Web Hizmetleri tercihleri**.</span><span class="sxs-lookup"><span data-stu-id="e1700-196">Then click under hello **Setup Tasks** section of hello left navigation menu, select hello **Integration** section, and click **Web Services Preferences**.</span></span>

    <span data-ttu-id="e1700-197">c.</span><span class="sxs-lookup"><span data-stu-id="e1700-197">c.</span></span> <span data-ttu-id="e1700-198">Netsuite hesabı Kimliğinizi kopyalayın ve hello yapıştırın **öznitelik değeri** Azure AD alanındaki.</span><span class="sxs-lookup"><span data-stu-id="e1700-198">Copy your Netsuite Account ID and paste it into hello **Attribute Value** field in Azure AD.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-Netsuite-tutorial/ns-account-id.png)

14. <span data-ttu-id="e1700-200">Kullanıcıların çoklu oturum açma Netsuite gerçekleştirmeden önce ilk hello Netsuite için uygun izinler atanmaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="e1700-200">Before users can perform single sign-on into Netsuite, they must first be assigned hello appropriate permissions in Netsuite.</span></span> <span data-ttu-id="e1700-201">Bu izinleri tooassign aşağıdaki Hello yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="e1700-201">Follow hello instructions below tooassign these permissions.</span></span>

    <span data-ttu-id="e1700-202">a.</span><span class="sxs-lookup"><span data-stu-id="e1700-202">a.</span></span> <span data-ttu-id="e1700-203">Merhaba üst gezinti menüsünde **Kurulum**, ardından **Kurulum Yöneticisi**.</span><span class="sxs-lookup"><span data-stu-id="e1700-203">On hello top navigation menu, click **Setup**, then click **Setup Manager**.</span></span>
      
      ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

    <span data-ttu-id="e1700-205">b.</span><span class="sxs-lookup"><span data-stu-id="e1700-205">b.</span></span> <span data-ttu-id="e1700-206">Merhaba sol gezinti menüsünde seçin **kullanıcıları/rolleri**, ardından **Rolleri Yönet**.</span><span class="sxs-lookup"><span data-stu-id="e1700-206">On hello left navigation menu, select **Users/Roles**, then click **Manage Roles**.</span></span>
      
      ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-Netsuite-tutorial/ns-manage-roles.png)

    <span data-ttu-id="e1700-208">c.</span><span class="sxs-lookup"><span data-stu-id="e1700-208">c.</span></span> <span data-ttu-id="e1700-209">Tıklatın **yeni rol**.</span><span class="sxs-lookup"><span data-stu-id="e1700-209">Click **New Role**.</span></span>

    <span data-ttu-id="e1700-210">d.</span><span class="sxs-lookup"><span data-stu-id="e1700-210">d.</span></span> <span data-ttu-id="e1700-211">Yazın bir **adı** yeni rol ve select hello **tek oturum açma yalnızca** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="e1700-211">Type in a **Name** for your new role, and select hello **Single Sign-On Only** checkbox.</span></span>
      
      ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-Netsuite-tutorial/ns-new-role.png)

    <span data-ttu-id="e1700-213">e.</span><span class="sxs-lookup"><span data-stu-id="e1700-213">e.</span></span> <span data-ttu-id="e1700-214">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e1700-214">Click **Save**.</span></span>

    <span data-ttu-id="e1700-215">f.</span><span class="sxs-lookup"><span data-stu-id="e1700-215">f.</span></span> <span data-ttu-id="e1700-216">Hello içinde hello üst menüsünde **izinleri**.</span><span class="sxs-lookup"><span data-stu-id="e1700-216">In hello menu on hello top, click **Permissions**.</span></span> <span data-ttu-id="e1700-217">Ardından **Kurulum**.</span><span class="sxs-lookup"><span data-stu-id="e1700-217">Then click **Setup**.</span></span>
      
       ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-Netsuite-tutorial/ns-sso.png)

    <span data-ttu-id="e1700-219">g.</span><span class="sxs-lookup"><span data-stu-id="e1700-219">g.</span></span> <span data-ttu-id="e1700-220">Seçin **ayarlamak yukarı SAM çoklu oturum açma**ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="e1700-220">Select **Set Up SAM Single Sign-on**, and then click **Add**.</span></span>

    <span data-ttu-id="e1700-221">h.</span><span class="sxs-lookup"><span data-stu-id="e1700-221">h.</span></span> <span data-ttu-id="e1700-222">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e1700-222">Click **Save**.</span></span>

    <span data-ttu-id="e1700-223">ı.</span><span class="sxs-lookup"><span data-stu-id="e1700-223">i.</span></span> <span data-ttu-id="e1700-224">Merhaba üst gezinti menüsünde **Kurulum**, ardından **Kurulum Yöneticisi**.</span><span class="sxs-lookup"><span data-stu-id="e1700-224">On hello top navigation menu, click **Setup**, then click **Setup Manager**.</span></span>
      
       ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

    <span data-ttu-id="e1700-226">j.</span><span class="sxs-lookup"><span data-stu-id="e1700-226">j.</span></span> <span data-ttu-id="e1700-227">Merhaba sol gezinti menüsünde seçin **kullanıcıları/rolleri**, ardından **kullanıcıları yönetme**.</span><span class="sxs-lookup"><span data-stu-id="e1700-227">On hello left navigation menu, select **Users/Roles**, then click **Manage Users**.</span></span>
      
       ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-Netsuite-tutorial/ns-manage-users.png)

    <span data-ttu-id="e1700-229">k.</span><span class="sxs-lookup"><span data-stu-id="e1700-229">k.</span></span> <span data-ttu-id="e1700-230">Bir test kullanıcı seçin.</span><span class="sxs-lookup"><span data-stu-id="e1700-230">Select a test user.</span></span> <span data-ttu-id="e1700-231">Ardından **Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="e1700-231">Then click **Edit**.</span></span>
      
       ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-Netsuite-tutorial/ns-edit-user.png)

    <span data-ttu-id="e1700-233">l.</span><span class="sxs-lookup"><span data-stu-id="e1700-233">l.</span></span> <span data-ttu-id="e1700-234">Hello rolleri iletişim kutusunda, oluşturduğunuz ve'ı tıklatın hello rolü seçin **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="e1700-234">On hello Roles dialog, select hello role that you have created and click **Add**.</span></span>
      
       ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-Netsuite-tutorial/ns-add-role.png)

    <span data-ttu-id="e1700-236">m.</span><span class="sxs-lookup"><span data-stu-id="e1700-236">m.</span></span> <span data-ttu-id="e1700-237">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e1700-237">Click **Save**.</span></span>
    
> [!TIP]
> <span data-ttu-id="e1700-238">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="e1700-238">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e1700-239">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="e1700-239">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e1700-240">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e1700-240">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e1700-241">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e1700-241">Creating an Azure AD test user</span></span>
<span data-ttu-id="e1700-242">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="e1700-242">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="e1700-244">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e1700-244">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e1700-245">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="e1700-245">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-netsuite-tutorial/create_aaduser_01.png) 

2.  <span data-ttu-id="e1700-247">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="e1700-247">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-netsuite-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e1700-249">Merhaba iletişim Hello üstünde tıklatın **Ekle** tooopen hello **kullanıcı** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e1700-249">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-netsuite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e1700-251">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e1700-251">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-netsuite-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e1700-253">a.</span><span class="sxs-lookup"><span data-stu-id="e1700-253">a.</span></span> <span data-ttu-id="e1700-254">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e1700-254">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e1700-255">b.</span><span class="sxs-lookup"><span data-stu-id="e1700-255">b.</span></span> <span data-ttu-id="e1700-256">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="e1700-256">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e1700-257">c.</span><span class="sxs-lookup"><span data-stu-id="e1700-257">c.</span></span> <span data-ttu-id="e1700-258">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="e1700-258">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e1700-259">d.</span><span class="sxs-lookup"><span data-stu-id="e1700-259">d.</span></span> <span data-ttu-id="e1700-260">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e1700-260">Click **Create**.</span></span> 

### <a name="creating-a-netsuite-test-user"></a><span data-ttu-id="e1700-261">Netsuite test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e1700-261">Creating a Netsuite test user</span></span>

<span data-ttu-id="e1700-262">Bu bölümde, Britta Simon adlı bir kullanıcı Netsuite içinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="e1700-262">In this section, a user called Britta Simon is created in Netsuite.</span></span> <span data-ttu-id="e1700-263">Netsuite yalnızca zaman sağlama, varsayılan olarak etkin olduğu destekler.</span><span class="sxs-lookup"><span data-stu-id="e1700-263">Netsuite supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="e1700-264">Bu bölümde, eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="e1700-264">There is no action item for you in this section.</span></span> <span data-ttu-id="e1700-265">Bir kullanıcı Netsuite zaten yoksa, tooaccess Netsuite çalıştığında yeni bir tane oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="e1700-265">If a user doesn't already exist in Netsuite, a new one is created when you attempt tooaccess Netsuite.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e1700-266">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="e1700-266">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e1700-267">Bu bölümde, erişim tooNetsuite vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="e1700-267">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNetsuite.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="e1700-269">**tooassign Britta Simon tooNetsuite hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e1700-269">**tooassign Britta Simon tooNetsuite, perform hello following steps:**</span></span>

1. <span data-ttu-id="e1700-270">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="e1700-270">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="e1700-272">Merhaba uygulamalar listesinde **Netsuite**.</span><span class="sxs-lookup"><span data-stu-id="e1700-272">In hello applications list, select **Netsuite**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_app.png) 

3. <span data-ttu-id="e1700-274">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="e1700-274">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="e1700-276">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e1700-276">Click **Add** button.</span></span> <span data-ttu-id="e1700-277">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e1700-277">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="e1700-279">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="e1700-279">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e1700-280">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e1700-280">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e1700-281">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e1700-281">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e1700-282">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="e1700-282">Testing single sign-on</span></span>

<span data-ttu-id="e1700-283">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="e1700-283">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="e1700-284">tootest, çoklu oturum açma ayarları, açık hello adresinden erişim Paneli'nde [https://myapps.microsoft.com](https://myapps.microsoft.com/), oturum hello test dikkate ve tıklatın **Netsuite**.</span><span class="sxs-lookup"><span data-stu-id="e1700-284">tootest your single sign-on settings, open hello Access Panel at [https://myapps.microsoft.com](https://myapps.microsoft.com/), sign into hello test account, and click **Netsuite**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e1700-285">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="e1700-285">Additional resources</span></span>

* [<span data-ttu-id="e1700-286">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="e1700-286">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e1700-287">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="e1700-287">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="e1700-288">Kullanıcı sağlamayı Yapılandır</span><span class="sxs-lookup"><span data-stu-id="e1700-288">Configure User Provisioning</span></span>](active-directory-saas-netsuite-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_203.png

