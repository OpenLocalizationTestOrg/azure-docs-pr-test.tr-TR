---
title: "Öğretici: Azure Active Directory Tümleştirme ile Kudos | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Kudos arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 39c47ce6-4944-47ba-8f53-3afa95398034
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: c1b481463574461f9948db2b83843fefa5d74e99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kudos"></a><span data-ttu-id="77b50-103">Öğretici: Azure Active Directory Tümleştirme Kudos ile</span><span class="sxs-lookup"><span data-stu-id="77b50-103">Tutorial: Azure Active Directory integration with Kudos</span></span>

<span data-ttu-id="77b50-104">Bu öğreticide, bilgi nasıl toointegrate Kudos Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="77b50-104">In this tutorial, you learn how toointegrate Kudos with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="77b50-105">Kudos Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="77b50-105">Integrating Kudos with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="77b50-106">Erişim tooKudos sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="77b50-106">You can control in Azure AD who has access tooKudos</span></span>
- <span data-ttu-id="77b50-107">Kullanıcıların tooautomatically get açan tooKudos (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="77b50-107">You can enable your users tooautomatically get signed-on tooKudos (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="77b50-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="77b50-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="77b50-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="77b50-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="77b50-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="77b50-110">Prerequisites</span></span>

<span data-ttu-id="77b50-111">tooconfigure Kudos ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="77b50-111">tooconfigure Azure AD integration with Kudos, you need hello following items:</span></span>

- <span data-ttu-id="77b50-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="77b50-112">An Azure AD subscription</span></span>
- <span data-ttu-id="77b50-113">Bir Kudos çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="77b50-113">A Kudos single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="77b50-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="77b50-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="77b50-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="77b50-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="77b50-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="77b50-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="77b50-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="77b50-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="77b50-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="77b50-118">Scenario description</span></span>
<span data-ttu-id="77b50-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="77b50-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="77b50-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="77b50-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="77b50-121">Merhaba Galerisi'nden Kudos ekleme</span><span class="sxs-lookup"><span data-stu-id="77b50-121">Adding Kudos from hello gallery</span></span>
2. <span data-ttu-id="77b50-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="77b50-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kudos-from-hello-gallery"></a><span data-ttu-id="77b50-123">Merhaba Galerisi'nden Kudos ekleme</span><span class="sxs-lookup"><span data-stu-id="77b50-123">Adding Kudos from hello gallery</span></span>
<span data-ttu-id="77b50-124">Azure AD'ye tooconfigure hello tümleştirme Kudos, tooadd Kudos hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="77b50-124">tooconfigure hello integration of Kudos into Azure AD, you need tooadd Kudos from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="77b50-125">**tooadd Kudos hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="77b50-125">**tooadd Kudos from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="77b50-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="77b50-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="77b50-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="77b50-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="77b50-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="77b50-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="77b50-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="77b50-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="77b50-133">Merhaba arama kutusuna yazın **Kudos**.</span><span class="sxs-lookup"><span data-stu-id="77b50-133">In hello search box, type **Kudos**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_search.png)

5. <span data-ttu-id="77b50-135">Merhaba Sonuçlar panelinde seçin **Kudos**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="77b50-135">In hello results panel, select **Kudos**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="77b50-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="77b50-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="77b50-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Kudos sınayın.</span><span class="sxs-lookup"><span data-stu-id="77b50-138">In this section, you configure and test Azure AD single sign-on with Kudos based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="77b50-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Kudos içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="77b50-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kudos is tooa user in Azure AD.</span></span> <span data-ttu-id="77b50-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Kudos hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="77b50-140">In other words, a link relationship between an Azure AD user and hello related user in Kudos needs toobe established.</span></span>

<span data-ttu-id="77b50-141">Merhaba hello değeri Kudos içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="77b50-141">In Kudos, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="77b50-142">tooconfigure ve Kudos ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="77b50-142">tooconfigure and test Azure AD single sign-on with Kudos, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="77b50-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="77b50-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="77b50-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="77b50-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="77b50-145">**[Kudos test kullanıcısı oluşturma](#creating-a-kudos-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Kudos içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="77b50-145">**[Creating a Kudos test user](#creating-a-kudos-test-user)** - toohave a counterpart of Britta Simon in Kudos that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="77b50-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="77b50-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="77b50-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="77b50-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="77b50-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="77b50-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="77b50-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Kudos uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="77b50-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kudos application.</span></span>

<span data-ttu-id="77b50-150">**tooconfigure Azure AD çoklu oturum açma ile Kudos, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="77b50-150">**tooconfigure Azure AD single sign-on with Kudos, perform hello following steps:**</span></span>

1. <span data-ttu-id="77b50-151">Hello hello üzerinde Azure portal'ın **Kudos** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="77b50-151">In hello Azure portal, on hello **Kudos** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="77b50-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="77b50-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_samlbase.png)

3. <span data-ttu-id="77b50-155">Merhaba üzerinde **Kudos etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="77b50-155">On hello **Kudos Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_url.png)

    <span data-ttu-id="77b50-157">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<company>.kudosnow.com`</span><span class="sxs-lookup"><span data-stu-id="77b50-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company>.kudosnow.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="77b50-158">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="77b50-158">This value is not real.</span></span> <span data-ttu-id="77b50-159">Bu değer ile Merhaba güncelleştirme gerçek oturum açma URL'si.</span><span class="sxs-lookup"><span data-stu-id="77b50-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="77b50-160">Kişi [Kudos istemci destek ekibi](http://success.kudosnow.com/home) tooget bu değer.</span><span class="sxs-lookup"><span data-stu-id="77b50-160">Contact [Kudos Client support team](http://success.kudosnow.com/home) tooget this value.</span></span> 
 
4. <span data-ttu-id="77b50-161">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="77b50-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_certificate.png) 

5. <span data-ttu-id="77b50-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="77b50-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kudos-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="77b50-165">Merhaba üzerinde **Kudos yapılandırma** 'yi tıklatın **yapılandırma Kudos** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="77b50-165">On hello **Kudos Configuration** section, click **Configure Kudos** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="77b50-166">Kopya hello **Sign-Out URL ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="77b50-166">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_configure.png) 

7. <span data-ttu-id="77b50-168">Farklı web tarayıcısı penceresinde Kudos şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="77b50-168">In a different web browser window, log into your Kudos company site as an administrator.</span></span>

8. <span data-ttu-id="77b50-169">Hello içinde hello üst menüsünde **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="77b50-169">In hello menu on hello top, click **Settings**.</span></span>
   
    <span data-ttu-id="77b50-170">![Ayarları](./media/active-directory-saas-kudos-tutorial/ic787806.png "ayarları")</span><span class="sxs-lookup"><span data-stu-id="77b50-170">![Settings](./media/active-directory-saas-kudos-tutorial/ic787806.png "Settings")</span></span>

9. <span data-ttu-id="77b50-171">Tıklatın **tümleştirmeler \> SSO**.</span><span class="sxs-lookup"><span data-stu-id="77b50-171">Click **Integrations \> SSO**.</span></span>

10. <span data-ttu-id="77b50-172">Merhaba, **SSO** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="77b50-172">In hello **SSO** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="77b50-173">![SSO](./media/active-directory-saas-kudos-tutorial/ic787807.png "SSO")</span><span class="sxs-lookup"><span data-stu-id="77b50-173">![SSO](./media/active-directory-saas-kudos-tutorial/ic787807.png "SSO")</span></span>
   
    <span data-ttu-id="77b50-174">a.</span><span class="sxs-lookup"><span data-stu-id="77b50-174">a.</span></span> <span data-ttu-id="77b50-175">İçinde **URL üzerinde oturum** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="77b50-175">In **Sign on URL** textbox, paste hello value of  **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="77b50-176">b.</span><span class="sxs-lookup"><span data-stu-id="77b50-176">b.</span></span> <span data-ttu-id="77b50-177">Base-64 kodlanmış sertifikanızı kopyalama hello panonuza bunu içerik Not Defteri'nde açın ve toohello yapıştırın **X.509 sertifikası** metin kutusu</span><span class="sxs-lookup"><span data-stu-id="77b50-177">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **X.509 certificate** textbox</span></span>
   
    <span data-ttu-id="77b50-178">c.</span><span class="sxs-lookup"><span data-stu-id="77b50-178">c.</span></span> <span data-ttu-id="77b50-179">İçinde **oturum kapatma tooURL**, hello değerini yapıştırın **Sign-Out URL** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="77b50-179">In **Logout tooURL**, paste hello value of  **Sign-Out URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="77b50-180">d.</span><span class="sxs-lookup"><span data-stu-id="77b50-180">d.</span></span> <span data-ttu-id="77b50-181">Merhaba, **Kudos URL'niz** metin kutusuna, şirketinizin adını yazın.</span><span class="sxs-lookup"><span data-stu-id="77b50-181">In hello **Your Kudos URL** textbox, type your company name.</span></span>
   
    <span data-ttu-id="77b50-182">e.</span><span class="sxs-lookup"><span data-stu-id="77b50-182">e.</span></span> <span data-ttu-id="77b50-183">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="77b50-183">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="77b50-184">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="77b50-184">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="77b50-185">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="77b50-185">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="77b50-186">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="77b50-186">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="77b50-187">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="77b50-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="77b50-188">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="77b50-188">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="77b50-190">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="77b50-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="77b50-191">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="77b50-191">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kudos-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="77b50-193">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="77b50-193">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kudos-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="77b50-195">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="77b50-195">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kudos-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="77b50-197">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="77b50-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kudos-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="77b50-199">a.</span><span class="sxs-lookup"><span data-stu-id="77b50-199">a.</span></span> <span data-ttu-id="77b50-200">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="77b50-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="77b50-201">b.</span><span class="sxs-lookup"><span data-stu-id="77b50-201">b.</span></span> <span data-ttu-id="77b50-202">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="77b50-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="77b50-203">c.</span><span class="sxs-lookup"><span data-stu-id="77b50-203">c.</span></span> <span data-ttu-id="77b50-204">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="77b50-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="77b50-205">d.</span><span class="sxs-lookup"><span data-stu-id="77b50-205">d.</span></span> <span data-ttu-id="77b50-206">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="77b50-206">Click **Create**.</span></span>
 
### <a name="creating-a-kudos-test-user"></a><span data-ttu-id="77b50-207">Kudos test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="77b50-207">Creating a Kudos test user</span></span>

<span data-ttu-id="77b50-208">Kudos içine sipariş tooenable Azure AD kullanıcıların toolog bunların Kudos sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="77b50-208">In order tooenable Azure AD users toolog into Kudos, they must be provisioned into Kudos.</span></span> 

<span data-ttu-id="77b50-209">Kudos Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="77b50-209">In hello case of Kudos, provisioning is a manual task.</span></span>

<span data-ttu-id="77b50-210">**bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="77b50-210">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="77b50-211">İçinde tooyour oturum **Kudos** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="77b50-211">Log in tooyour **Kudos** company site as administrator.</span></span>

2. <span data-ttu-id="77b50-212">Hello içinde hello üst menüsünde **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="77b50-212">In hello menu on hello top, click **Settings**.</span></span>
   
   <span data-ttu-id="77b50-213">![Ayarları](./media/active-directory-saas-kudos-tutorial/ic787806.png "ayarları")</span><span class="sxs-lookup"><span data-stu-id="77b50-213">![Settings](./media/active-directory-saas-kudos-tutorial/ic787806.png "Settings")</span></span>

3. <span data-ttu-id="77b50-214">Tıklatın **kullanıcı yönetici**.</span><span class="sxs-lookup"><span data-stu-id="77b50-214">Click **User Admin**.</span></span>

4. <span data-ttu-id="77b50-215">Merhaba tıklatın **kullanıcılar** sekmesini ve ardından **kullanıcı ekleme**.</span><span class="sxs-lookup"><span data-stu-id="77b50-215">Click hello **Users** tab, and then click **Add a User**.</span></span>
   
   <span data-ttu-id="77b50-216">![Kullanıcı Yönetim](./media/active-directory-saas-kudos-tutorial/ic787809.png "kullanıcı yönetici")</span><span class="sxs-lookup"><span data-stu-id="77b50-216">![User Admin](./media/active-directory-saas-kudos-tutorial/ic787809.png "User Admin")</span></span>

5. <span data-ttu-id="77b50-217">Merhaba, **kullanıcı ekleme** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="77b50-217">In hello **Add a User** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="77b50-218">![Kullanıcı ekleme](./media/active-directory-saas-kudos-tutorial/ic787810.png "kullanıcı ekleme")</span><span class="sxs-lookup"><span data-stu-id="77b50-218">![Add a User](./media/active-directory-saas-kudos-tutorial/ic787810.png "Add a User")</span></span>
   
    <span data-ttu-id="77b50-219">a.</span><span class="sxs-lookup"><span data-stu-id="77b50-219">a.</span></span> <span data-ttu-id="77b50-220">Türü hello **ad**, **Soyadı**, **e-posta** ve ilgili diğer ayrıntıları hello tooprovision istediğiniz geçerli bir Azure Active Directory hesabının metin kutuları.</span><span class="sxs-lookup"><span data-stu-id="77b50-220">Type hello **First Name**, **Last Name**, **Email** and other details of a valid Azure Active Directory account you want tooprovision into hello related textboxes.</span></span>
   
    <span data-ttu-id="77b50-221">b.</span><span class="sxs-lookup"><span data-stu-id="77b50-221">b.</span></span> <span data-ttu-id="77b50-222">Tıklatın **kullanıcı oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="77b50-222">Click **Create User**.</span></span>

>[!NOTE]
><span data-ttu-id="77b50-223">API AAD kullanıcı hesaplarının Kudos tooprovision tarafından sağlanan veya herhangi diğer Kudos kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="77b50-223">You can use any other Kudos user account creation tools or APIs provided by Kudos tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="77b50-224">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="77b50-224">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="77b50-225">Bu bölümde, erişim tooKudos vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="77b50-225">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKudos.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="77b50-227">**tooassign Britta Simon tooKudos hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="77b50-227">**tooassign Britta Simon tooKudos, perform hello following steps:**</span></span>

1. <span data-ttu-id="77b50-228">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="77b50-228">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="77b50-230">Merhaba uygulamalar listesinde **Kudos**.</span><span class="sxs-lookup"><span data-stu-id="77b50-230">In hello applications list, select **Kudos**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_app.png) 

3. <span data-ttu-id="77b50-232">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="77b50-232">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="77b50-234">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="77b50-234">Click **Add** button.</span></span> <span data-ttu-id="77b50-235">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="77b50-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="77b50-237">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="77b50-237">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="77b50-238">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="77b50-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="77b50-239">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="77b50-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="77b50-240">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="77b50-240">Testing single sign-on</span></span>

<span data-ttu-id="77b50-241">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="77b50-241">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="77b50-242">Merhaba Kudos hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Kudos uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="77b50-242">When you click hello Kudos tile in hello Access Panel, you should get automatically signed-on tooyour Kudos application.</span></span> <span data-ttu-id="77b50-243">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="77b50-243">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="77b50-244">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="77b50-244">Additional resources</span></span>

* [<span data-ttu-id="77b50-245">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="77b50-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="77b50-246">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="77b50-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_203.png

