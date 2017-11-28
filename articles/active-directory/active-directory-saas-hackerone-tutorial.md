---
title: "Öğretici: Azure Active Directory Tümleştirme ile Hackerone | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Hackerone arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 229d1efb-b6a5-4df8-9839-5d551487db4e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: c9dc033e26e79a7233dcfb3899c62684d4a19652
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hackerone"></a><span data-ttu-id="46353-103">Öğretici: Azure Active Directory Tümleştirme HackerOne ile</span><span class="sxs-lookup"><span data-stu-id="46353-103">Tutorial: Azure Active Directory integration with HackerOne</span></span>

<span data-ttu-id="46353-104">Bu öğreticide, bilgi nasıl toointegrate HackerOne Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="46353-104">In this tutorial, you learn how toointegrate HackerOne with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="46353-105">HackerOne Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="46353-105">Integrating HackerOne with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="46353-106">Erişim tooHackerOne sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="46353-106">You can control in Azure AD who has access tooHackerOne</span></span>
- <span data-ttu-id="46353-107">Kullanıcıların tooautomatically get açan tooHackerOne (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="46353-107">You can enable your users tooautomatically get signed-on tooHackerOne (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="46353-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="46353-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="46353-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="46353-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="46353-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="46353-110">Prerequisites</span></span>

<span data-ttu-id="46353-111">tooconfigure HackerOne ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="46353-111">tooconfigure Azure AD integration with HackerOne, you need hello following items:</span></span>

- <span data-ttu-id="46353-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="46353-112">An Azure AD subscription</span></span>
- <span data-ttu-id="46353-113">Bir HackerOne çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="46353-113">A HackerOne single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="46353-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="46353-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="46353-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="46353-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="46353-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="46353-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="46353-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="46353-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="46353-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="46353-118">Scenario description</span></span>
<span data-ttu-id="46353-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="46353-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="46353-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="46353-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="46353-121">Merhaba Galerisi'nden HackerOne ekleme</span><span class="sxs-lookup"><span data-stu-id="46353-121">Adding HackerOne from hello gallery</span></span>
2. <span data-ttu-id="46353-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="46353-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hackerone-from-hello-gallery"></a><span data-ttu-id="46353-123">Merhaba Galerisi'nden HackerOne ekleme</span><span class="sxs-lookup"><span data-stu-id="46353-123">Adding HackerOne from hello gallery</span></span>
<span data-ttu-id="46353-124">Azure AD'ye tooconfigure hello tümleştirme HackerOne, tooadd HackerOne hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="46353-124">tooconfigure hello integration of HackerOne into Azure AD, you need tooadd HackerOne from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="46353-125">**tooadd HackerOne hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="46353-125">**tooadd HackerOne from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="46353-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="46353-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="46353-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="46353-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="46353-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="46353-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="46353-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="46353-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="46353-133">Merhaba arama kutusuna yazın **HackerOne**.</span><span class="sxs-lookup"><span data-stu-id="46353-133">In hello search box, type **HackerOne**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_search.png)

5. <span data-ttu-id="46353-135">Merhaba Sonuçlar panelinde seçin **HackerOne**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="46353-135">In hello results panel, select **HackerOne**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="46353-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="46353-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="46353-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı HackerOne ile test etme</span><span class="sxs-lookup"><span data-stu-id="46353-138">In this section, you configure and test Azure AD single sign-on with HackerOne based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="46353-139">Tek toowork'ın oturum açma hangi hello karşılık gelen HackerOne içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="46353-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in HackerOne is tooa user in Azure AD.</span></span> <span data-ttu-id="46353-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı HackerOne hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="46353-140">In other words, a link relationship between an Azure AD user and hello related user in HackerOne needs toobe established.</span></span>

<span data-ttu-id="46353-141">Merhaba hello değeri HackerOne içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="46353-141">In HackerOne, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="46353-142">tooconfigure ve HackerOne ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="46353-142">tooconfigure and test Azure AD single sign-on with HackerOne, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="46353-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="46353-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="46353-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="46353-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="46353-145">**[HackerOne test kullanıcısı oluşturma](#creating-a-hackerone-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir HackerOne içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="46353-145">**[Creating a HackerOne test user](#creating-a-hackerone-test-user)** - toohave a counterpart of Britta Simon in HackerOne that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="46353-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="46353-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="46353-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="46353-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="46353-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="46353-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="46353-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma HackerOne uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="46353-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your HackerOne application.</span></span>

<span data-ttu-id="46353-150">**tooconfigure Azure AD çoklu oturum açma ile HackerOne, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="46353-150">**tooconfigure Azure AD single sign-on with HackerOne, perform hello following steps:**</span></span>

1. <span data-ttu-id="46353-151">Hello hello üzerinde Azure portal'ın **HackerOne** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="46353-151">In hello Azure portal, on hello **HackerOne** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="46353-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="46353-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_samlbase.png)

3. <span data-ttu-id="46353-155">Merhaba üzerinde **HackerOne tek oturum açma URL'si ve tanımlayıcı** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="46353-155">On hello **HackerOne Single sign-on URL and Identifier** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_url.png)

    <span data-ttu-id="46353-157">a.</span><span class="sxs-lookup"><span data-stu-id="46353-157">a.</span></span> <span data-ttu-id="46353-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://hackerone.com/<company name>/authentication`</span><span class="sxs-lookup"><span data-stu-id="46353-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://hackerone.com/<company name>/authentication`</span></span>

    <span data-ttu-id="46353-159">b.</span><span class="sxs-lookup"><span data-stu-id="46353-159">b.</span></span> <span data-ttu-id="46353-160">Merhaba, **tanımlayıcısı** metin kutusuna, URL'yi yazın:`https://hackerone.com/users/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="46353-160">In hello **Identifier** textbox, type a URL as:  `https://hackerone.com/users/saml/metadata`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="46353-161">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="46353-161">This value is not real.</span></span> <span data-ttu-id="46353-162">Bu değer ile Merhaba güncelleştirme gerçek oturum açma URL'si.</span><span class="sxs-lookup"><span data-stu-id="46353-162">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="46353-163">Kişi [HackerOne destek ekibi](mailto:support@hackerone.com) tooget bu değer.</span><span class="sxs-lookup"><span data-stu-id="46353-163">Contact [HackerOne support team](mailto:support@hackerone.com) tooget this value.</span></span> 
 
4. <span data-ttu-id="46353-164">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="46353-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_certificate.png) 

5. <span data-ttu-id="46353-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="46353-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hackerone-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="46353-168">Merhaba üzerinde **HackerOne yapılandırma** 'yi tıklatın **yapılandırma HackerOne** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="46353-168">On hello **HackerOne Configuration** section, click **Configure HackerOne** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="46353-169">Kopya hello **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="46353-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_configure.png) 

7. <span data-ttu-id="46353-171">Oturum açma tooyour HackerOne Kiracı yönetici olarak.</span><span class="sxs-lookup"><span data-stu-id="46353-171">Sign On tooyour HackerOne tenant as an administrator.</span></span>

8. <span data-ttu-id="46353-172">Hello'nde hello üstte, hello menüsünü "**ayarları**."</span><span class="sxs-lookup"><span data-stu-id="46353-172">In hello menu on hello top, click hello "**Settings**."</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_001.png) 

9. <span data-ttu-id="46353-174">Çok gidin"**kimlik doğrulaması**"tıklatıp"**SAML ayarları ekleme**."</span><span class="sxs-lookup"><span data-stu-id="46353-174">Navigate too"**Authentication**" and click "**Add SAML settings**."</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_003.png) 

10. <span data-ttu-id="46353-176">Merhaba üzerinde **SAML ayarları** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="46353-176">On hello **SAML Settings** dialog, perform hello following steps:</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_004.png) 

    <span data-ttu-id="46353-178">a.</span><span class="sxs-lookup"><span data-stu-id="46353-178">a.</span></span> <span data-ttu-id="46353-179">Merhaba, **e-posta etki alanı** metin kutusuna, kayıtlı bir etki alanı yazın.</span><span class="sxs-lookup"><span data-stu-id="46353-179">In hello **Email Domain** textbox, type a registered domain.</span></span>

    <span data-ttu-id="46353-180">b.</span><span class="sxs-lookup"><span data-stu-id="46353-180">b.</span></span> <span data-ttu-id="46353-181">İçinde **üzerinde tek oturum URL'si** metin kutuları, hello değerini yapıştırın **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="46353-181">In  **Single Sign On URL** textboxes, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="46353-182">c.</span><span class="sxs-lookup"><span data-stu-id="46353-182">c.</span></span> <span data-ttu-id="46353-183">Açık, **sertifika dosyası** Azure portalından indirdiğiniz Defteri'nde Merhaba içeriğine, panoya kopyalayın ve toohello Yapıştır **X509 sertifika** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="46353-183">Open your **Certificate file** in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **X509 Certificate**  textbox.</span></span>
    
    <span data-ttu-id="46353-184">d.</span><span class="sxs-lookup"><span data-stu-id="46353-184">d.</span></span> <span data-ttu-id="46353-185">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="46353-185">Click **Save**.</span></span>

11. <span data-ttu-id="46353-186">Merhaba kimlik doğrulama ayarları iletişim kutusunda hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="46353-186">On hello Authentication Settings dialog, perform hello following steps:</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_005.png) 

    <span data-ttu-id="46353-188">a.</span><span class="sxs-lookup"><span data-stu-id="46353-188">a.</span></span> <span data-ttu-id="46353-189">Tıklatın **testi**.</span><span class="sxs-lookup"><span data-stu-id="46353-189">Click **Run test**.</span></span>

    <span data-ttu-id="46353-190">b.</span><span class="sxs-lookup"><span data-stu-id="46353-190">b.</span></span> <span data-ttu-id="46353-191">Varsa hello hello değerini **durum** alan eşittir **durumu'son test: oluşturulan**, kişi, [HackerOne destek ekibi](mailto:support@hackerone.com) toorequest yapılandırmanızı gözden.</span><span class="sxs-lookup"><span data-stu-id="46353-191">If hello value of hello **Status** field equals **Last test status: created**, contact your [HackerOne support team](mailto:support@hackerone.com) toorequest a review of your configuration.</span></span>

> [!TIP]
> <span data-ttu-id="46353-192">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="46353-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="46353-193">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="46353-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="46353-194">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="46353-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="46353-195">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="46353-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="46353-196">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="46353-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="46353-198">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="46353-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="46353-199">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="46353-199">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-hackerone-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="46353-201">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="46353-201">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-hackerone-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="46353-203">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="46353-203">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-hackerone-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="46353-205">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="46353-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-hackerone-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="46353-207">a.</span><span class="sxs-lookup"><span data-stu-id="46353-207">a.</span></span> <span data-ttu-id="46353-208">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="46353-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="46353-209">b.</span><span class="sxs-lookup"><span data-stu-id="46353-209">b.</span></span> <span data-ttu-id="46353-210">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="46353-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="46353-211">c.</span><span class="sxs-lookup"><span data-stu-id="46353-211">c.</span></span> <span data-ttu-id="46353-212">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="46353-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="46353-213">d.</span><span class="sxs-lookup"><span data-stu-id="46353-213">d.</span></span> <span data-ttu-id="46353-214">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="46353-214">Click **Create**.</span></span>
 
### <a name="creating-a-hackerone-test-user"></a><span data-ttu-id="46353-215">HackerOne test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="46353-215">Creating a HackerOne test user</span></span>

<span data-ttu-id="46353-216">Ardından, HackerOne içinde Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="46353-216">Next, you create a user called Britta Simon in HackerOne.</span></span> <span data-ttu-id="46353-217">HackerOne yalnızca zaman sağlama, varsayılan olarak etkin olduğu destekler.</span><span class="sxs-lookup"><span data-stu-id="46353-217">HackerOne supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="46353-218">Bu bölümde, eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="46353-218">There is no action item for you in this section.</span></span> <span data-ttu-id="46353-219">HackerOne eriştiğinizde, henüz yoksa yeni bir kullanıcı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="46353-219">When you access HackerOne, a new user is created if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="46353-220">Bir kullanıcı toocreate el ile gerekiyorsa, toocontact hello Onayla destek ekibi gerekir.</span><span class="sxs-lookup"><span data-stu-id="46353-220">If you need toocreate a user manually, you need toocontact hello Certify support team.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="46353-221">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="46353-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="46353-222">Bu bölümde, erişim tooHackerOne vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="46353-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHackerOne.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="46353-224">**tooassign Britta Simon tooHackerOne hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="46353-224">**tooassign Britta Simon tooHackerOne, perform hello following steps:**</span></span>

1. <span data-ttu-id="46353-225">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="46353-225">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="46353-227">Merhaba uygulamalar listesinde **HackerOne**.</span><span class="sxs-lookup"><span data-stu-id="46353-227">In hello applications list, select **HackerOne**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_app.png) 

3. <span data-ttu-id="46353-229">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="46353-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="46353-231">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="46353-231">Click **Add** button.</span></span> <span data-ttu-id="46353-232">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="46353-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="46353-234">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="46353-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="46353-235">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="46353-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="46353-236">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="46353-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="46353-237">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="46353-237">Testing single sign-on</span></span>

<span data-ttu-id="46353-238">Son olarak, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="46353-238">Finally, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>  

<span data-ttu-id="46353-239">Merhaba HackerOne hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour HackerOne uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="46353-239">When you click hello HackerOne tile in hello Access Panel, you should get automatically signed-on tooyour HackerOne application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="46353-240">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="46353-240">Additional resources</span></span>

* [<span data-ttu-id="46353-241">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="46353-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="46353-242">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="46353-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_203.png

