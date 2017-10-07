---
title: "Öğretici: Azure Active Directory Tümleştirme ile Workstars | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Workstars arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 51a4a4e4-ff60-4971-b3f8-a0367b70d220
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: 86250d7538f058d2a821ded7dda0b2fc185d80df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workstars"></a><span data-ttu-id="bdc99-103">Öğretici: Azure Active Directory Tümleştirme Workstars ile</span><span class="sxs-lookup"><span data-stu-id="bdc99-103">Tutorial: Azure Active Directory integration with Workstars</span></span>

<span data-ttu-id="bdc99-104">Bu öğreticide, bilgi nasıl toointegrate Workstars Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bdc99-104">In this tutorial, you learn how toointegrate Workstars with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bdc99-105">Workstars Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="bdc99-105">Integrating Workstars with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="bdc99-106">Erişim tooWorkstars sahip Azure AD'de kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bdc99-106">You can control in Azure AD who has access tooWorkstars.</span></span>
- <span data-ttu-id="bdc99-107">Kullanıcıların tooautomatically get açan tooWorkstars (çoklu oturum açma) Azure AD hesaplarına ile etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bdc99-107">You can enable your users tooautomatically get signed-on tooWorkstars (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="bdc99-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="bdc99-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="bdc99-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bdc99-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bdc99-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="bdc99-110">Prerequisites</span></span>

<span data-ttu-id="bdc99-111">tooconfigure Workstars ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="bdc99-111">tooconfigure Azure AD integration with Workstars, you need hello following items:</span></span>

- <span data-ttu-id="bdc99-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="bdc99-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bdc99-113">Bir Workstars çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="bdc99-113">A Workstars single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bdc99-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="bdc99-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bdc99-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="bdc99-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bdc99-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="bdc99-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bdc99-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bdc99-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bdc99-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="bdc99-118">Scenario description</span></span>
<span data-ttu-id="bdc99-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="bdc99-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bdc99-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="bdc99-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bdc99-121">Merhaba Galerisi'nden Workstars ekleme</span><span class="sxs-lookup"><span data-stu-id="bdc99-121">Adding Workstars from hello gallery</span></span>
2. <span data-ttu-id="bdc99-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="bdc99-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workstars-from-hello-gallery"></a><span data-ttu-id="bdc99-123">Merhaba Galerisi'nden Workstars ekleme</span><span class="sxs-lookup"><span data-stu-id="bdc99-123">Adding Workstars from hello gallery</span></span>
<span data-ttu-id="bdc99-124">Azure AD'ye tooconfigure hello tümleştirme Workstars, tooadd Workstars hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="bdc99-124">tooconfigure hello integration of Workstars into Azure AD, you need tooadd Workstars from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="bdc99-125">**tooadd Workstars hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="bdc99-125">**tooadd Workstars from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="bdc99-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="bdc99-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory düğmesi][1]

2. <span data-ttu-id="bdc99-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="bdc99-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="bdc99-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="bdc99-129">Then go too**All applications**.</span></span>

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="bdc99-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="bdc99-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Merhaba yeni uygulama düğmesi][3]

4. <span data-ttu-id="bdc99-133">Merhaba arama kutusuna yazın **Workstars**seçin **Workstars** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="bdc99-133">In hello search box, type **Workstars**, select **Workstars** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Merhaba sonuçları listesinde Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="bdc99-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="bdc99-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="bdc99-136">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Workstars sınayın.</span><span class="sxs-lookup"><span data-stu-id="bdc99-136">In this section, you configure and test Azure AD single sign-on with Workstars based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="bdc99-137">Tek toowork'ın oturum açma hangi hello karşılık gelen Workstars içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="bdc99-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Workstars is tooa user in Azure AD.</span></span> <span data-ttu-id="bdc99-138">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Workstars hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="bdc99-138">In other words, a link relationship between an Azure AD user and hello related user in Workstars needs toobe established.</span></span>

<span data-ttu-id="bdc99-139">Merhaba hello değeri Workstars içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="bdc99-139">In Workstars, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="bdc99-140">tooconfigure ve Workstars ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="bdc99-140">tooconfigure and test Azure AD single sign-on with Workstars, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="bdc99-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="bdc99-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="bdc99-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="bdc99-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bdc99-143">**[Workstars test kullanıcısı oluşturma](#create-a-workstars-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Workstars içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="bdc99-143">**[Create a Workstars test user](#create-a-workstars-test-user)** - toohave a counterpart of Britta Simon in Workstars that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="bdc99-144">**[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="bdc99-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bdc99-145">**[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="bdc99-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="bdc99-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="bdc99-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="bdc99-147">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Workstars uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="bdc99-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Workstars application.</span></span>

<span data-ttu-id="bdc99-148">**tooconfigure Azure AD çoklu oturum açma ile Workstars, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="bdc99-148">**tooconfigure Azure AD single sign-on with Workstars, perform hello following steps:**</span></span>

1. <span data-ttu-id="bdc99-149">Hello hello üzerinde Azure portal'ın **Workstars** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="bdc99-149">In hello Azure portal, on hello **Workstars** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. <span data-ttu-id="bdc99-151">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="bdc99-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_samlbase.png)

3. <span data-ttu-id="bdc99-153">Merhaba üzerinde **Workstars etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="bdc99-153">On hello **Workstars Domain and URLs** section, perform hello following steps:</span></span>

    ![Workstars etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_url.png)

    <span data-ttu-id="bdc99-155">a.</span><span class="sxs-lookup"><span data-stu-id="bdc99-155">a.</span></span> <span data-ttu-id="bdc99-156">Merhaba, **tanımlayıcısı** metin kutusuna, türü hello URL'si:`https://workstars.com`</span><span class="sxs-lookup"><span data-stu-id="bdc99-156">In hello **Identifier** textbox, type hello URL: `https://workstars.com`</span></span>

    <span data-ttu-id="bdc99-157">b.</span><span class="sxs-lookup"><span data-stu-id="bdc99-157">b.</span></span> <span data-ttu-id="bdc99-158">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.workstars.com/saml/login_check`</span><span class="sxs-lookup"><span data-stu-id="bdc99-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.workstars.com/saml/login_check`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="bdc99-159">Merhaba değeri gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="bdc99-159">hello value is not real.</span></span> <span data-ttu-id="bdc99-160">Güncelleştirme hello değerle hello gerçek yanıt URL'si.</span><span class="sxs-lookup"><span data-stu-id="bdc99-160">Update hello value with hello actual Reply URL.</span></span> <span data-ttu-id="bdc99-161">Kişi [Workstars destek ekibi](https://support.workstars.com) tooget hello değeri.</span><span class="sxs-lookup"><span data-stu-id="bdc99-161">Contact [Workstars support team](https://support.workstars.com) tooget hello value.</span></span>
 
4. <span data-ttu-id="bdc99-162">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="bdc99-162">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_certificate.png) 

5. <span data-ttu-id="bdc99-164">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="bdc99-164">Click **Save** button.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-workstars-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="bdc99-166">Merhaba üzerinde **Workstars yapılandırma** 'yi tıklatın **yapılandırma Workstars** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="bdc99-166">On hello **Workstars Configuration** section, click **Configure Workstars** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="bdc99-167">Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="bdc99-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Workstars yapılandırma](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_configure.png) 

7. <span data-ttu-id="bdc99-169">Başka bir tarayıcı penceresinde tooyour Workstars şirket sitesinde yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="bdc99-169">In another browser window, sign on tooyour Workstars company site as an administrator.</span></span>

8. <span data-ttu-id="bdc99-170">Merhaba ana araç çubuğunda **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="bdc99-170">In hello main toolbar, click **Settings**.</span></span>

    ![Workstars ayarları](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_sett.png)

9. <span data-ttu-id="bdc99-172">Çok Git**oturum açma** > **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="bdc99-172">Go too**Sign On** > **Settings**.</span></span>

    ![Workstars oturum açma](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_signon.png)

    ![Workstars ayarları](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_settings.png)

10. <span data-ttu-id="bdc99-175">Merhaba üzerinde **tek oturum üzerinde (SAML) - ayarları** sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="bdc99-175">On hello **Single Sign On (SAML) - Settings** page, perform hello following steps:</span></span>
    
    ![Workstars saml](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_saml.png)

    <span data-ttu-id="bdc99-177">a.</span><span class="sxs-lookup"><span data-stu-id="bdc99-177">a.</span></span> <span data-ttu-id="bdc99-178">İçinde **kimlik sağlayıcı adı** metin kutusuna, türü **Office 365**.</span><span class="sxs-lookup"><span data-stu-id="bdc99-178">In **Identity Provider Name** textbox, type **Office 365**.</span></span>

    <span data-ttu-id="bdc99-179">b.</span><span class="sxs-lookup"><span data-stu-id="bdc99-179">b.</span></span> <span data-ttu-id="bdc99-180">Merhaba, **kimlik sağlayıcısı varlık kimliği** metin kutusuna, Yapıştır hello değerini **SAML varlık kimliği**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="bdc99-180">In hello **Identity Provider Entity ID** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="bdc99-181">c.</span><span class="sxs-lookup"><span data-stu-id="bdc99-181">c.</span></span> <span data-ttu-id="bdc99-182">Not Defteri'nde Hello hello indirilen sertifika dosyasının içeriğini kopyalayın ve hello yapıştırma **x509 sertifika** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="bdc99-182">Copy hello content of hello downloaded certificate file in notepad, and then paste it into hello **x509 Certificate** textbox.</span></span> 

    <span data-ttu-id="bdc99-183">d.</span><span class="sxs-lookup"><span data-stu-id="bdc99-183">d.</span></span> <span data-ttu-id="bdc99-184">Merhaba, **SAML SSO URL** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="bdc99-184">In hello **SAML SSO URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="bdc99-185">e.</span><span class="sxs-lookup"><span data-stu-id="bdc99-185">e.</span></span> <span data-ttu-id="bdc99-186">Merhaba, **uzak oturum kapatma URL'si** metin kutusuna, Yapıştır hello değerini **Sign-Out URL**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="bdc99-186">In hello **Remote Logout URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="bdc99-187">f.</span><span class="sxs-lookup"><span data-stu-id="bdc99-187">f.</span></span> <span data-ttu-id="bdc99-188">seçin **ad kimliği** olarak **e-posta (varsayılan)**.</span><span class="sxs-lookup"><span data-stu-id="bdc99-188">select **Name ID** as **Email (Default)**.</span></span>

    <span data-ttu-id="bdc99-189">g.</span><span class="sxs-lookup"><span data-stu-id="bdc99-189">g.</span></span> <span data-ttu-id="bdc99-190">Tıklatın **onaylayın**.</span><span class="sxs-lookup"><span data-stu-id="bdc99-190">Click **Confirm**.</span></span>
    
> [!TIP]
> <span data-ttu-id="bdc99-191">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="bdc99-191">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="bdc99-192">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="bdc99-192">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="bdc99-193">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bdc99-193">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="bdc99-194">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="bdc99-194">Create an Azure AD test user</span></span>

<span data-ttu-id="bdc99-195">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="bdc99-195">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="bdc99-197">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="bdc99-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="bdc99-198">Merhaba hello sol bölmede Azure portal hello tıklatın **Azure Active Directory** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="bdc99-198">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-workstars-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="bdc99-200">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="bdc99-200">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-workstars-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="bdc99-202">tooopen hello **kullanıcı** iletişim kutusu, tıklatın **Ekle** hello hello üstündeki **tüm kullanıcılar** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="bdc99-202">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Merhaba Ekle düğmesi](./media/active-directory-saas-workstars-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="bdc99-204">Merhaba, **kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="bdc99-204">In hello **User** dialog box, perform hello following steps:</span></span>

    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-workstars-tutorial/create_aaduser_04.png)

    <span data-ttu-id="bdc99-206">a.</span><span class="sxs-lookup"><span data-stu-id="bdc99-206">a.</span></span> <span data-ttu-id="bdc99-207">Merhaba, **adı** kutusuna **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bdc99-207">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bdc99-208">b.</span><span class="sxs-lookup"><span data-stu-id="bdc99-208">b.</span></span> <span data-ttu-id="bdc99-209">Merhaba, **kullanıcı adı** kutusuna, kullanıcının Britta Simon hello e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="bdc99-209">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="bdc99-210">c.</span><span class="sxs-lookup"><span data-stu-id="bdc99-210">c.</span></span> <span data-ttu-id="bdc99-211">Select hello **Göster parola** onay kutusunu işaretleyin ve ardından hello görüntülenen hello değerini aşağı yazma **parola** kutusu.</span><span class="sxs-lookup"><span data-stu-id="bdc99-211">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="bdc99-212">d.</span><span class="sxs-lookup"><span data-stu-id="bdc99-212">d.</span></span> <span data-ttu-id="bdc99-213">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bdc99-213">Click **Create**.</span></span>
  
### <a name="create-a-workstars-test-user"></a><span data-ttu-id="bdc99-214">Workstars test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="bdc99-214">Create a Workstars test user</span></span>

<span data-ttu-id="bdc99-215">Bu bölümde, Workstars içinde Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="bdc99-215">In this section, you create a user called Britta Simon in Workstars.</span></span> <span data-ttu-id="bdc99-216">Çalışmak [Workstars destek ekibi](https://support.workstars.com) tooadd hello kullanıcılar hello Workstars Platform.</span><span class="sxs-lookup"><span data-stu-id="bdc99-216">Work with [Workstars support team](https://support.workstars.com) tooadd hello users in hello Workstars platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="bdc99-217">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="bdc99-217">Assign hello Azure AD test user</span></span>

<span data-ttu-id="bdc99-218">Bu bölümde, erişim tooWorkstars vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="bdc99-218">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWorkstars.</span></span>

![Merhaba kullanıcı rolü atayın][200] 

<span data-ttu-id="bdc99-220">**tooassign Britta Simon tooWorkstars hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="bdc99-220">**tooassign Britta Simon tooWorkstars, perform hello following steps:**</span></span>

1. <span data-ttu-id="bdc99-221">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="bdc99-221">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="bdc99-223">Merhaba uygulamalar listesinde **Workstars**.</span><span class="sxs-lookup"><span data-stu-id="bdc99-223">In hello applications list, select **Workstars**.</span></span>

    ![Merhaba Workstars bağlantı hello uygulamalar listesinde](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_app.png)  

3. <span data-ttu-id="bdc99-225">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="bdc99-225">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202]

4. <span data-ttu-id="bdc99-227">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="bdc99-227">Click **Add** button.</span></span> <span data-ttu-id="bdc99-228">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="bdc99-228">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Merhaba eklemek atama bölmesi][203]

5. <span data-ttu-id="bdc99-230">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="bdc99-230">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="bdc99-231">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="bdc99-231">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bdc99-232">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="bdc99-232">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="bdc99-233">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="bdc99-233">Test single sign-on</span></span>

<span data-ttu-id="bdc99-234">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="bdc99-234">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="bdc99-235">Hello erişim paneli Workstars döşeme hello tıkladığınızda, otomatik olarak oturum açma Workstars uygulama tooyour almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="bdc99-235">When you click hello Workstars tile in hello Access Panel, you should get automatically signed-on tooyour Workstars application.</span></span>
<span data-ttu-id="bdc99-236">Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bdc99-236">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="bdc99-237">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="bdc99-237">Additional resources</span></span>

* [<span data-ttu-id="bdc99-238">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="bdc99-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bdc99-239">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="bdc99-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_203.png

