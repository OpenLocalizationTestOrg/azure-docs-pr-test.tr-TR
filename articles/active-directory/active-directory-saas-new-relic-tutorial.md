---
title: "Öğretici: New Relic Azure Active Directory Tümleştirme | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve New Relic arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3186b9a8-f4d8-45e2-ad82-6275f95e7aa6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: jeedes
ms.openlocfilehash: dc8f0df3b18a32bde155e8911a581fc5f91af217
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-new-relic"></a><span data-ttu-id="22cfe-103">Öğretici: New Relic Azure Active Directory Tümleştirme</span><span class="sxs-lookup"><span data-stu-id="22cfe-103">Tutorial: Azure Active Directory integration with New Relic</span></span>

<span data-ttu-id="22cfe-104">Bu öğreticide, bilgi nasıl toointegrate New Relic Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="22cfe-104">In this tutorial, you learn how toointegrate New Relic with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="22cfe-105">New Relic Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="22cfe-105">Integrating New Relic with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="22cfe-106">Erişim tooNew Relic sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="22cfe-106">You can control in Azure AD who has access tooNew Relic</span></span>
- <span data-ttu-id="22cfe-107">Kullanıcıların tooautomatically get açan tooNew Relic (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="22cfe-107">You can enable your users tooautomatically get signed-on tooNew Relic (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="22cfe-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="22cfe-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="22cfe-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="22cfe-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="22cfe-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="22cfe-110">Prerequisites</span></span>

<span data-ttu-id="22cfe-111">New Relic ile Azure AD tümleştirme tooconfigure, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="22cfe-111">tooconfigure Azure AD integration with New Relic, you need hello following items:</span></span>

- <span data-ttu-id="22cfe-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="22cfe-112">An Azure AD subscription</span></span>
- <span data-ttu-id="22cfe-113">Bir New Relic çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="22cfe-113">A New Relic single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="22cfe-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="22cfe-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="22cfe-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="22cfe-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="22cfe-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="22cfe-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="22cfe-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="22cfe-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="22cfe-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="22cfe-118">Scenario description</span></span>
<span data-ttu-id="22cfe-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="22cfe-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="22cfe-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="22cfe-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="22cfe-121">New Relic hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="22cfe-121">Adding New Relic from hello gallery</span></span>
2. <span data-ttu-id="22cfe-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="22cfe-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-new-relic-from-hello-gallery"></a><span data-ttu-id="22cfe-123">New Relic hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="22cfe-123">Adding New Relic from hello gallery</span></span>
<span data-ttu-id="22cfe-124">Azure AD'ye tooconfigure hello tümleştirme New Relic, tooadd New Relic hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="22cfe-124">tooconfigure hello integration of New Relic into Azure AD, you need tooadd New Relic from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="22cfe-125">**tooadd hello galerisinden New Relic hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="22cfe-125">**tooadd New Relic from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="22cfe-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="22cfe-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="22cfe-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="22cfe-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="22cfe-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="22cfe-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="22cfe-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="22cfe-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="22cfe-133">Merhaba arama kutusuna yazın **New Relic**.</span><span class="sxs-lookup"><span data-stu-id="22cfe-133">In hello search box, type **New Relic**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_search.png)

5. <span data-ttu-id="22cfe-135">Merhaba Sonuçlar panelinde seçin **New Relic**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="22cfe-135">In hello results panel, select **New Relic**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="22cfe-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="22cfe-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="22cfe-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı New Relic ile test etme.</span><span class="sxs-lookup"><span data-stu-id="22cfe-138">In this section, you configure and test Azure AD single sign-on with New Relic based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="22cfe-139">Tek toowork'ın oturum açma hangi hello karşılık gelen New Relic içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="22cfe-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in New Relic is tooa user in Azure AD.</span></span> <span data-ttu-id="22cfe-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve New Relic hello ilgili kullanıcı arasındaki bağlantıyı ilişki kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="22cfe-140">In other words, a link relationship between an Azure AD user and hello related user in New Relic needs toobe established.</span></span>

<span data-ttu-id="22cfe-141">New Relic içinde hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="22cfe-141">In New Relic, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="22cfe-142">tooconfigure ve New Relic ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="22cfe-142">tooconfigure and test Azure AD single sign-on with New Relic, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="22cfe-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="22cfe-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="22cfe-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="22cfe-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="22cfe-145">**[New Relic test kullanıcısı oluşturma](#creating-a-new-relic-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir New Relic içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="22cfe-145">**[Creating a New Relic test user](#creating-a-new-relic-test-user)** - toohave a counterpart of Britta Simon in New Relic that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="22cfe-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="22cfe-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="22cfe-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="22cfe-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="22cfe-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="22cfe-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="22cfe-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma New Relic uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="22cfe-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your New Relic application.</span></span>

<span data-ttu-id="22cfe-150">**tooconfigure Azure AD çoklu oturum açma New Relic ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="22cfe-150">**tooconfigure Azure AD single sign-on with New Relic, perform hello following steps:**</span></span>

1. <span data-ttu-id="22cfe-151">Hello hello üzerinde Azure portal'ın **New Relic** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="22cfe-151">In hello Azure portal, on hello **New Relic** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="22cfe-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="22cfe-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_samlbase.png)

3. <span data-ttu-id="22cfe-155">Merhaba üzerinde **yeni Relic etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="22cfe-155">On hello **New Relic Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_url.png)

    <span data-ttu-id="22cfe-157">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.newrelic.com`</span><span class="sxs-lookup"><span data-stu-id="22cfe-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.newrelic.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="22cfe-158">Merhaba değeri gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="22cfe-158">hello value is not real.</span></span> <span data-ttu-id="22cfe-159">Güncelleştirme hello değerle hello gerçek oturum açma URL'si.</span><span class="sxs-lookup"><span data-stu-id="22cfe-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="22cfe-160">Kişi [yeni Relic istemci destek ekibi](https://support.newrelic.com/) tooget hello değeri.</span><span class="sxs-lookup"><span data-stu-id="22cfe-160">Contact [New Relic Client support team](https://support.newrelic.com/) tooget hello value.</span></span> 
 
4. <span data-ttu-id="22cfe-161">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="22cfe-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_certificate.png) 

5. <span data-ttu-id="22cfe-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="22cfe-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-new-relic-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="22cfe-165">Merhaba üzerinde **yeni Relic yapılandırma** 'yi tıklatın **yapılandırma New Relic** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="22cfe-165">On hello **New Relic Configuration** section, click **Configure New Relic** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="22cfe-166">Kopya hello **Sign-Out URL ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="22cfe-166">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_configure.png) 

7. <span data-ttu-id="22cfe-168">Farklı web tarayıcısı penceresinde tooyour üzerinde oturum **New Relic** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="22cfe-168">In a different web browser window, sign on tooyour **New Relic** company site as administrator.</span></span>

8. <span data-ttu-id="22cfe-169">Hello içinde hello üst menüsünde **hesap ayarlarını**.</span><span class="sxs-lookup"><span data-stu-id="22cfe-169">In hello menu on hello top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="22cfe-170">![Hesap ayarları](./media/active-directory-saas-new-relic-tutorial/ic797036.png "hesap ayarları")</span><span class="sxs-lookup"><span data-stu-id="22cfe-170">![Account Settings](./media/active-directory-saas-new-relic-tutorial/ic797036.png "Account Settings")</span></span>

9. <span data-ttu-id="22cfe-171">Merhaba tıklatın **güvenlik ve kimlik doğrulama** sekmesini ve sonra hello **çoklu oturum açmayı** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="22cfe-171">Click hello **Security and authentication** tab, and then click hello **Single sign on** tab.</span></span>
   
    <span data-ttu-id="22cfe-172">![Çoklu oturum açma](./media/active-directory-saas-new-relic-tutorial/ic797037.png "çoklu oturum açma")</span><span class="sxs-lookup"><span data-stu-id="22cfe-172">![Single Sign-On](./media/active-directory-saas-new-relic-tutorial/ic797037.png "Single Sign-On")</span></span>

10. <span data-ttu-id="22cfe-173">Merhaba SAML iletişim sayfasında hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="22cfe-173">On hello SAML dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="22cfe-174">![SAML](./media/active-directory-saas-new-relic-tutorial/ic797038.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="22cfe-174">![SAML](./media/active-directory-saas-new-relic-tutorial/ic797038.png "SAML")</span></span>
   
   <span data-ttu-id="22cfe-175">a.</span><span class="sxs-lookup"><span data-stu-id="22cfe-175">a.</span></span> <span data-ttu-id="22cfe-176">Tıklatın **Dosya Seç** tooupload indirilen Azure Active Directory Sertifika.</span><span class="sxs-lookup"><span data-stu-id="22cfe-176">Click **Choose File** tooupload your downloaded Azure Active Directory certificate.</span></span>

   <span data-ttu-id="22cfe-177">b.</span><span class="sxs-lookup"><span data-stu-id="22cfe-177">b.</span></span> <span data-ttu-id="22cfe-178">Merhaba, **uzaktan oturum açma URL'si** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="22cfe-178">In hello **Remote login URL** textbox,  paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="22cfe-179">c.</span><span class="sxs-lookup"><span data-stu-id="22cfe-179">c.</span></span> <span data-ttu-id="22cfe-180">Merhaba, **oturum kapatma URL'si** metin kutusuna, Yapıştır hello değerini **Sign-Out URL**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="22cfe-180">In hello **Logout landing URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

   <span data-ttu-id="22cfe-181">d.</span><span class="sxs-lookup"><span data-stu-id="22cfe-181">d.</span></span> <span data-ttu-id="22cfe-182">Tıklatın **my değişiklikleri kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="22cfe-182">Click **Save my changes**.</span></span>

> [!TIP]
> <span data-ttu-id="22cfe-183">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="22cfe-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="22cfe-184">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="22cfe-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="22cfe-185">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="22cfe-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="22cfe-186">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="22cfe-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="22cfe-187">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="22cfe-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="22cfe-189">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="22cfe-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="22cfe-190">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="22cfe-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-new-relic-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="22cfe-192">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="22cfe-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-new-relic-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="22cfe-194">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="22cfe-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-new-relic-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="22cfe-196">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="22cfe-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-new-relic-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="22cfe-198">a.</span><span class="sxs-lookup"><span data-stu-id="22cfe-198">a.</span></span> <span data-ttu-id="22cfe-199">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="22cfe-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="22cfe-200">b.</span><span class="sxs-lookup"><span data-stu-id="22cfe-200">b.</span></span> <span data-ttu-id="22cfe-201">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="22cfe-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="22cfe-202">c.</span><span class="sxs-lookup"><span data-stu-id="22cfe-202">c.</span></span> <span data-ttu-id="22cfe-203">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="22cfe-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="22cfe-204">d.</span><span class="sxs-lookup"><span data-stu-id="22cfe-204">d.</span></span> <span data-ttu-id="22cfe-205">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="22cfe-205">Click **Create**.</span></span>
 
### <a name="creating-a-new-relic-test-user"></a><span data-ttu-id="22cfe-206">New Relic test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="22cfe-206">Creating a New Relic test user</span></span>

<span data-ttu-id="22cfe-207">TooNew Relic içinde sipariş tooenable Azure Active Directory Kullanıcıları toolog bunların New Relic sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="22cfe-207">In order tooenable Azure Active Directory users toolog in tooNew Relic, they must be provisioned into New Relic.</span></span> <span data-ttu-id="22cfe-208">New Relic Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="22cfe-208">In hello case of New Relic, provisioning is a manual task.</span></span>

<span data-ttu-id="22cfe-209">**bir kullanıcı hesabı tooNew Relic, tooprovision hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="22cfe-209">**tooprovision a user account tooNew Relic, perform hello following steps:**</span></span>

1. <span data-ttu-id="22cfe-210">İçinde tooyour oturum **New Relic** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="22cfe-210">Log in tooyour **New Relic** company site as administrator.</span></span>

2. <span data-ttu-id="22cfe-211">Hello içinde hello üst menüsünde **hesap ayarlarını**.</span><span class="sxs-lookup"><span data-stu-id="22cfe-211">In hello menu on hello top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="22cfe-212">![Hesap ayarları](./media/active-directory-saas-new-relic-tutorial/ic797040.png "hesap ayarları")</span><span class="sxs-lookup"><span data-stu-id="22cfe-212">![Account Settings](./media/active-directory-saas-new-relic-tutorial/ic797040.png "Account Settings")</span></span>

3. <span data-ttu-id="22cfe-213">Merhaba, **hesap** hello bölmesi sol tarafında, tıklatın **Özet**ve ardından **Kullanıcı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="22cfe-213">In hello **Account** pane on hello left side, click **Summary**, and then click **Add user**.</span></span>
   
    <span data-ttu-id="22cfe-214">![Hesap ayarları](./media/active-directory-saas-new-relic-tutorial/ic797041.png "hesap ayarları")</span><span class="sxs-lookup"><span data-stu-id="22cfe-214">![Account Settings](./media/active-directory-saas-new-relic-tutorial/ic797041.png "Account Settings")</span></span>

4. <span data-ttu-id="22cfe-215">Merhaba üzerinde **etkin kullanıcılar** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="22cfe-215">On hello **Active users** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="22cfe-216">![Etkin kullanıcılar](./media/active-directory-saas-new-relic-tutorial/ic797042.png "etkin kullanıcılar")</span><span class="sxs-lookup"><span data-stu-id="22cfe-216">![Active Users](./media/active-directory-saas-new-relic-tutorial/ic797042.png "Active Users")</span></span>
   
    <span data-ttu-id="22cfe-217">a.</span><span class="sxs-lookup"><span data-stu-id="22cfe-217">a.</span></span> <span data-ttu-id="22cfe-218">Merhaba, **e-posta** metin kutusuna, türü hello e-posta adresini istediğiniz geçerli bir Azure Active Directory kullanıcı tooprovision.</span><span class="sxs-lookup"><span data-stu-id="22cfe-218">In hello **Email** textbox, type hello email address of a valid Azure Active Directory user you want tooprovision.</span></span>

    <span data-ttu-id="22cfe-219">b.</span><span class="sxs-lookup"><span data-stu-id="22cfe-219">b.</span></span> <span data-ttu-id="22cfe-220">Olarak **rol** seçin **kullanıcı**.</span><span class="sxs-lookup"><span data-stu-id="22cfe-220">As **Role** select **User**.</span></span>

    <span data-ttu-id="22cfe-221">c.</span><span class="sxs-lookup"><span data-stu-id="22cfe-221">c.</span></span> <span data-ttu-id="22cfe-222">Tıklatın **bu kullanıcıyı eklemek**.</span><span class="sxs-lookup"><span data-stu-id="22cfe-222">Click **Add this user**.</span></span>

>[!NOTE]
><span data-ttu-id="22cfe-223">API AAD kullanıcı hesapları New Relic tooprovision tarafından sağlanan veya herhangi diğer New Relic kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="22cfe-223">You can use any other New Relic user account creation tools or APIs provided by New Relic tooprovision AAD user accounts.</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="22cfe-224">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="22cfe-224">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="22cfe-225">Bu bölümde, erişim tooNew Relic vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="22cfe-225">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNew Relic.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="22cfe-227">**tooassign Britta Simon tooNew Relic, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="22cfe-227">**tooassign Britta Simon tooNew Relic, perform hello following steps:**</span></span>

1. <span data-ttu-id="22cfe-228">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="22cfe-228">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="22cfe-230">Merhaba uygulamalar listesinde **New Relic**.</span><span class="sxs-lookup"><span data-stu-id="22cfe-230">In hello applications list, select **New Relic**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_app.png) 

3. <span data-ttu-id="22cfe-232">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="22cfe-232">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="22cfe-234">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="22cfe-234">Click **Add** button.</span></span> <span data-ttu-id="22cfe-235">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="22cfe-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="22cfe-237">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="22cfe-237">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="22cfe-238">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="22cfe-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="22cfe-239">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="22cfe-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="22cfe-240">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="22cfe-240">Testing single sign-on</span></span>

<span data-ttu-id="22cfe-241">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="22cfe-241">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="22cfe-242">Merhaba New Relic hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour New Relic uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="22cfe-242">When you click hello New Relic tile in hello Access Panel, you should get automatically signed-on tooyour New Relic application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="22cfe-243">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="22cfe-243">Additional resources</span></span>

* [<span data-ttu-id="22cfe-244">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="22cfe-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="22cfe-245">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="22cfe-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_203.png

