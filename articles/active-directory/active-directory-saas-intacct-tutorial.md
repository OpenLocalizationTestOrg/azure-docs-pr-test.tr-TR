---
title: "Öğretici: Azure Active Directory Tümleştirme ile Intacct | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Intacct arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 92518e02-a62c-4b1b-a8e9-2803eb2b49ac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 3500039615166c2f61fb408d85bb82dfaefba134
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intacct"></a><span data-ttu-id="de00f-103">Öğretici: Azure Active Directory Tümleştirme Intacct ile</span><span class="sxs-lookup"><span data-stu-id="de00f-103">Tutorial: Azure Active Directory integration with Intacct</span></span>

<span data-ttu-id="de00f-104">Bu öğreticide, bilgi nasıl toointegrate Intacct Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="de00f-104">In this tutorial, you learn how toointegrate Intacct with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="de00f-105">Intacct Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="de00f-105">Integrating Intacct with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="de00f-106">Erişim tooIntacct sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="de00f-106">You can control in Azure AD who has access tooIntacct</span></span>
- <span data-ttu-id="de00f-107">Kullanıcıların tooautomatically get açan tooIntacct (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="de00f-107">You can enable your users tooautomatically get signed-on tooIntacct (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="de00f-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="de00f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="de00f-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="de00f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="de00f-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="de00f-110">Prerequisites</span></span>

<span data-ttu-id="de00f-111">tooconfigure Intacct ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="de00f-111">tooconfigure Azure AD integration with Intacct, you need hello following items:</span></span>

- <span data-ttu-id="de00f-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="de00f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="de00f-113">Bir Intacct çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="de00f-113">An Intacct single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="de00f-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="de00f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="de00f-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="de00f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="de00f-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="de00f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="de00f-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="de00f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="de00f-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="de00f-118">Scenario description</span></span>
<span data-ttu-id="de00f-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="de00f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="de00f-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="de00f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="de00f-121">Merhaba Galerisi'nden Intacct ekleme</span><span class="sxs-lookup"><span data-stu-id="de00f-121">Adding Intacct from hello gallery</span></span>
2. <span data-ttu-id="de00f-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="de00f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-intacct-from-hello-gallery"></a><span data-ttu-id="de00f-123">Merhaba Galerisi'nden Intacct ekleme</span><span class="sxs-lookup"><span data-stu-id="de00f-123">Adding Intacct from hello gallery</span></span>
<span data-ttu-id="de00f-124">Azure AD'ye tooconfigure hello tümleştirme Intacct, tooadd Intacct hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="de00f-124">tooconfigure hello integration of Intacct into Azure AD, you need tooadd Intacct from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="de00f-125">**tooadd Intacct hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="de00f-125">**tooadd Intacct from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="de00f-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="de00f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="de00f-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="de00f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="de00f-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="de00f-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="de00f-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="de00f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="de00f-133">Merhaba arama kutusuna yazın **Intacct**.</span><span class="sxs-lookup"><span data-stu-id="de00f-133">In hello search box, type **Intacct**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_search.png)

5. <span data-ttu-id="de00f-135">Merhaba Sonuçlar panelinde seçin **Intacct**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="de00f-135">In hello results panel, select **Intacct**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="de00f-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="de00f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="de00f-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Intacct sınayın.</span><span class="sxs-lookup"><span data-stu-id="de00f-138">In this section, you configure and test Azure AD single sign-on with Intacct based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="de00f-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Intacct içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="de00f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Intacct is tooa user in Azure AD.</span></span> <span data-ttu-id="de00f-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Intacct hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="de00f-140">In other words, a link relationship between an Azure AD user and hello related user in Intacct needs toobe established.</span></span>

<span data-ttu-id="de00f-141">Merhaba hello değeri Intacct içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="de00f-141">In Intacct, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="de00f-142">tooconfigure ve Intacct ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="de00f-142">tooconfigure and test Azure AD single sign-on with Intacct, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="de00f-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="de00f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="de00f-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="de00f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="de00f-145">**[Bir Intacct test kullanıcısı oluşturma](#creating-an-intacct-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Intacct içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="de00f-145">**[Creating an Intacct test user](#creating-an-intacct-test-user)** - toohave a counterpart of Britta Simon in Intacct that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="de00f-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="de00f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="de00f-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="de00f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="de00f-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="de00f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="de00f-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Intacct uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="de00f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Intacct application.</span></span>

<span data-ttu-id="de00f-150">**tooconfigure Azure AD çoklu oturum açma ile Intacct, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="de00f-150">**tooconfigure Azure AD single sign-on with Intacct, perform hello following steps:**</span></span>

1. <span data-ttu-id="de00f-151">Hello hello üzerinde Azure portal'ın **Intacct** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="de00f-151">In hello Azure portal, on hello **Intacct** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="de00f-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="de00f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_samlbase.png)

3. <span data-ttu-id="de00f-155">Merhaba üzerinde **Intacct etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="de00f-155">On hello **Intacct Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_url.png)

    <span data-ttu-id="de00f-157">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:</span><span class="sxs-lookup"><span data-stu-id="de00f-157">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.intacct.com/ia/acct/sso_response.phtml`|
    | `https://www.intacct.com/ia/acct/sso_response.phtml` |

    > [!NOTE] 
    > <span data-ttu-id="de00f-158">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="de00f-158">This value is not real.</span></span> <span data-ttu-id="de00f-159">Bu değer hello gerçek yanıt URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="de00f-159">Update this value with hello actual Reply URL.</span></span> <span data-ttu-id="de00f-160">Kişi [Intacct destek ekibi](https://us.intacct.com/support) tooget bu değer.</span><span class="sxs-lookup"><span data-stu-id="de00f-160">Contact [Intacct support team](https://us.intacct.com/support) tooget this value.</span></span>

4. <span data-ttu-id="de00f-161">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="de00f-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_certificate.png) 

5. <span data-ttu-id="de00f-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="de00f-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-intacct-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="de00f-165">Merhaba üzerinde **Intacct yapılandırma** 'yi tıklatın **yapılandırma Intacct** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="de00f-165">On hello **Intacct Configuration** section, click **Configure Intacct** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="de00f-166">Kopya hello **SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="de00f-166">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_configure.png) 

7. <span data-ttu-id="de00f-168">Farklı web tarayıcısı penceresinde tooyour Intacct şirket sitede yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="de00f-168">In a different web browser window, sign in tooyour Intacct company site as an administrator.</span></span>

8. <span data-ttu-id="de00f-169">Merhaba tıklatın **şirket** sekmesini ve ardından **şirket bilgisi**.</span><span class="sxs-lookup"><span data-stu-id="de00f-169">Click hello **Company** tab, and then click **Company Info**.</span></span>

    <span data-ttu-id="de00f-170">![Şirket](./media/active-directory-saas-intacct-tutorial/ic790037.png "şirket")</span><span class="sxs-lookup"><span data-stu-id="de00f-170">![Company](./media/active-directory-saas-intacct-tutorial/ic790037.png "Company")</span></span>

9. <span data-ttu-id="de00f-171">Merhaba tıklatın **güvenlik** sekmesini ve ardından **Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="de00f-171">Click hello **Security** tab, and then click **Edit**.</span></span>

    <span data-ttu-id="de00f-172">![Güvenlik](./media/active-directory-saas-intacct-tutorial/ic790038.png "güvenlik")</span><span class="sxs-lookup"><span data-stu-id="de00f-172">![Security](./media/active-directory-saas-intacct-tutorial/ic790038.png "Security")</span></span>

10. <span data-ttu-id="de00f-173">Merhaba, **tek oturum açma (SSO)** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="de00f-173">In hello **Single sign on (SSO)** section, perform hello following steps:</span></span>

    <span data-ttu-id="de00f-174">![Çoklu oturum açmayı](./media/active-directory-saas-intacct-tutorial/ic790039.png "çoklu oturum açmayı")</span><span class="sxs-lookup"><span data-stu-id="de00f-174">![Single sign on](./media/active-directory-saas-intacct-tutorial/ic790039.png "single sign on")</span></span>

    <span data-ttu-id="de00f-175">a.</span><span class="sxs-lookup"><span data-stu-id="de00f-175">a.</span></span> <span data-ttu-id="de00f-176">Seçin **etkinleştirmek çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="de00f-176">Select **Enable single sign on**.</span></span>

    <span data-ttu-id="de00f-177">b.</span><span class="sxs-lookup"><span data-stu-id="de00f-177">b.</span></span> <span data-ttu-id="de00f-178">Olarak **kimlik sağlayıcısı türü**seçin **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="de00f-178">As **Identity provider type**, select **SAML 2.0**.</span></span>

    <span data-ttu-id="de00f-179">c.</span><span class="sxs-lookup"><span data-stu-id="de00f-179">c.</span></span> <span data-ttu-id="de00f-180">İçinde **veren URL'si** metin kutusuna, Yapıştır hello değerini **SAML varlık kimliği** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="de00f-180">In **Issuer URL** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="de00f-181">d.</span><span class="sxs-lookup"><span data-stu-id="de00f-181">d.</span></span> <span data-ttu-id="de00f-182">İçinde **oturum açma URL'si** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="de00f-182">In **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="de00f-183">e.</span><span class="sxs-lookup"><span data-stu-id="de00f-183">e.</span></span> <span data-ttu-id="de00f-184">Açık, **base-64** kodlanmış sertifika Not Defteri'nde, kopyalama hello panonuza bunu içerik ve toohello yapıştırın **sertifika** kutusu.</span><span class="sxs-lookup"><span data-stu-id="de00f-184">Open your **base-64** encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **Certificate** box.</span></span>
   
    <span data-ttu-id="de00f-185">f.</span><span class="sxs-lookup"><span data-stu-id="de00f-185">f.</span></span> <span data-ttu-id="de00f-186">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="de00f-186">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="de00f-187">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="de00f-187">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="de00f-188">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="de00f-188">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="de00f-189">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="de00f-189">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="de00f-190">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="de00f-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="de00f-191">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="de00f-191">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="de00f-193">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="de00f-193">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="de00f-194">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="de00f-194">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-intacct-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="de00f-196">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="de00f-196">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-intacct-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="de00f-198">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="de00f-198">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-intacct-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="de00f-200">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="de00f-200">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-intacct-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="de00f-202">a.</span><span class="sxs-lookup"><span data-stu-id="de00f-202">a.</span></span> <span data-ttu-id="de00f-203">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="de00f-203">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="de00f-204">b.</span><span class="sxs-lookup"><span data-stu-id="de00f-204">b.</span></span> <span data-ttu-id="de00f-205">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="de00f-205">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="de00f-206">c.</span><span class="sxs-lookup"><span data-stu-id="de00f-206">c.</span></span> <span data-ttu-id="de00f-207">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="de00f-207">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="de00f-208">d.</span><span class="sxs-lookup"><span data-stu-id="de00f-208">d.</span></span> <span data-ttu-id="de00f-209">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="de00f-209">Click **Create**.</span></span>
 
### <a name="creating-an-intacct-test-user"></a><span data-ttu-id="de00f-210">Bir Intacct test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="de00f-210">Creating an Intacct test user</span></span>

<span data-ttu-id="de00f-211">tooset tooIntacct kaydolabilirsiniz şekilde Azure AD kullanıcılarının bunların Intacct sağlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="de00f-211">tooset up Azure AD users so they can sign in tooIntacct, they must be provisioned into Intacct.</span></span> <span data-ttu-id="de00f-212">Intacct için sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="de00f-212">For Intacct, provisioning is a manual task.</span></span>

<span data-ttu-id="de00f-213">**tooprovision kullanıcı hesapları, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="de00f-213">**tooprovision user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="de00f-214">İçinde tooyour oturum **Intacct** Kiracı.</span><span class="sxs-lookup"><span data-stu-id="de00f-214">Sign in tooyour **Intacct** tenant.</span></span>

2. <span data-ttu-id="de00f-215">Merhaba tıklatın **şirket** sekmesini ve ardından **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="de00f-215">Click hello **Company** tab, and then click **Users**.</span></span>

    <span data-ttu-id="de00f-216">![Kullanıcıların](./media/active-directory-saas-intacct-tutorial/ic790041.png "kullanıcılar")</span><span class="sxs-lookup"><span data-stu-id="de00f-216">![Users](./media/active-directory-saas-intacct-tutorial/ic790041.png "Users")</span></span>
3. <span data-ttu-id="de00f-217">Merhaba tıklatın **Ekle** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="de00f-217">Click hello **Add** tab.</span></span>

    <span data-ttu-id="de00f-218">![Ekleme](./media/active-directory-saas-intacct-tutorial/ic790042.png "ekleme")</span><span class="sxs-lookup"><span data-stu-id="de00f-218">![Add](./media/active-directory-saas-intacct-tutorial/ic790042.png "Add")</span></span>
4. <span data-ttu-id="de00f-219">Merhaba, **kullanıcı bilgilerini** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="de00f-219">In hello **User Information** section, perform hello following steps:</span></span>

    <span data-ttu-id="de00f-220">![Kullanıcı bilgilerini](./media/active-directory-saas-intacct-tutorial/ic790043.png "kullanıcı bilgileri")</span><span class="sxs-lookup"><span data-stu-id="de00f-220">![User Information](./media/active-directory-saas-intacct-tutorial/ic790043.png "User Information")</span></span>

    <span data-ttu-id="de00f-221">a.</span><span class="sxs-lookup"><span data-stu-id="de00f-221">a.</span></span> <span data-ttu-id="de00f-222">Merhaba girin **kullanıcı kimliği**, hello **Soyadı**, **ad**, hello **e-posta adresi**, hello **başlık**, ve hello **telefon** hello tooprovision istediğiniz bir Azure AD hesabının **kullanıcı bilgilerini** bölümü.</span><span class="sxs-lookup"><span data-stu-id="de00f-222">Enter hello **User ID**, hello **Last name**, **First name**, hello **Email address**, hello **Title**, and hello **Phone** of an Azure AD account that you want tooprovision into hello **User Information** section.</span></span>

    <span data-ttu-id="de00f-223">b.</span><span class="sxs-lookup"><span data-stu-id="de00f-223">b.</span></span> <span data-ttu-id="de00f-224">Select hello **yönetici ayrıcalıkları** tooprovision istediğiniz bir Azure AD hesabının.</span><span class="sxs-lookup"><span data-stu-id="de00f-224">Select hello **Admin privileges** of an Azure AD account that you want tooprovision.</span></span>
   
    <span data-ttu-id="de00f-225">c.</span><span class="sxs-lookup"><span data-stu-id="de00f-225">c.</span></span> <span data-ttu-id="de00f-226">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="de00f-226">Click **Save**.</span></span> <span data-ttu-id="de00f-227">Hello Azure AD hesap sahibi bir e-posta alır ve onu etkinleştirilmeden önce bir bağlantı tooconfirm hesaplarında izler.</span><span class="sxs-lookup"><span data-stu-id="de00f-227">hello Azure AD account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

>[!NOTE]
><span data-ttu-id="de00f-228">tooprovision Azure AD kullanıcı hesapları, diğer Intacct kullanıcı hesabı oluşturma araçlarını veya Intacct tarafından sağlanan API'leri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="de00f-228">tooprovision Azure AD user accounts, you can use other Intacct user account creation tools or APIs that are provided by Intacct.</span></span>
        
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="de00f-229">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="de00f-229">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="de00f-230">Bu bölümde, erişim tooIntacct vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="de00f-230">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooIntacct.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="de00f-232">**tooassign Britta Simon tooIntacct hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="de00f-232">**tooassign Britta Simon tooIntacct, perform hello following steps:**</span></span>

1. <span data-ttu-id="de00f-233">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="de00f-233">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="de00f-235">Merhaba uygulamalar listesinde **Intacct**.</span><span class="sxs-lookup"><span data-stu-id="de00f-235">In hello applications list, select **Intacct**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_app.png) 

3. <span data-ttu-id="de00f-237">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="de00f-237">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="de00f-239">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="de00f-239">Click **Add** button.</span></span> <span data-ttu-id="de00f-240">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="de00f-240">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="de00f-242">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="de00f-242">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="de00f-243">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="de00f-243">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="de00f-244">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="de00f-244">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="de00f-245">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="de00f-245">Testing single sign-on</span></span>

<span data-ttu-id="de00f-246">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test.</span><span class="sxs-lookup"><span data-stu-id="de00f-246">In this section, you test your Azure AD single sign-on configuration by using hello Access Panel.</span></span>

<span data-ttu-id="de00f-247">Merhaba Intacct hello erişim paneli parçasında tıklattığınızda tooyour Intacct uygulama otomatik olarak imzalanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="de00f-247">When you click hello Intacct tile in hello Access Panel, you should be automatically signed in tooyour Intacct application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="de00f-248">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="de00f-248">Additional resources</span></span>

* [<span data-ttu-id="de00f-249">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="de00f-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="de00f-250">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="de00f-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_203.png

