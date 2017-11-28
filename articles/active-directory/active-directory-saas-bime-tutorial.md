---
title: "Öğretici: Azure Active Directory Tümleştirme ile Bime | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Bime arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bdcf0729-c880-4c95-b739-0f6345b17dd8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: 1213725028dd8ce90f22fa6e9c50ffabebc8f3fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bime"></a><span data-ttu-id="26c44-103">Öğretici: Azure Active Directory Tümleştirme Bime ile</span><span class="sxs-lookup"><span data-stu-id="26c44-103">Tutorial: Azure Active Directory integration with Bime</span></span>

<span data-ttu-id="26c44-104">Bu öğreticide, bilgi nasıl toointegrate Bime Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="26c44-104">In this tutorial, you learn how toointegrate Bime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="26c44-105">Bime Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="26c44-105">Integrating Bime with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="26c44-106">Erişim tooBime sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="26c44-106">You can control in Azure AD who has access tooBime</span></span>
- <span data-ttu-id="26c44-107">Kullanıcıların tooautomatically get açan tooBime (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="26c44-107">You can enable your users tooautomatically get signed-on tooBime (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="26c44-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="26c44-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="26c44-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="26c44-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="26c44-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="26c44-110">Prerequisites</span></span>

<span data-ttu-id="26c44-111">tooconfigure Bime ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="26c44-111">tooconfigure Azure AD integration with Bime, you need hello following items:</span></span>

- <span data-ttu-id="26c44-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="26c44-112">An Azure AD subscription</span></span>
- <span data-ttu-id="26c44-113">Bir Bime çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="26c44-113">A Bime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="26c44-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="26c44-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="26c44-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="26c44-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="26c44-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="26c44-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="26c44-117">Bir Azure AD deneme ortam yoksa, burada bir aylık deneme elde edebilirsiniz: [deneme teklifi](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="26c44-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="26c44-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="26c44-118">Scenario description</span></span>
<span data-ttu-id="26c44-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="26c44-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="26c44-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="26c44-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="26c44-121">Merhaba Galerisi'nden Bime ekleme</span><span class="sxs-lookup"><span data-stu-id="26c44-121">Adding Bime from hello gallery</span></span>
2. <span data-ttu-id="26c44-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="26c44-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bime-from-hello-gallery"></a><span data-ttu-id="26c44-123">Merhaba Galerisi'nden Bime ekleme</span><span class="sxs-lookup"><span data-stu-id="26c44-123">Adding Bime from hello gallery</span></span>
<span data-ttu-id="26c44-124">Azure AD'ye tooconfigure hello tümleştirme Bime, tooadd Bime hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="26c44-124">tooconfigure hello integration of Bime into Azure AD, you need tooadd Bime from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="26c44-125">**tooadd Bime hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="26c44-125">**tooadd Bime from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="26c44-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="26c44-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="26c44-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="26c44-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="26c44-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="26c44-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="26c44-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="26c44-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="26c44-133">Merhaba arama kutusuna yazın **Bime**.</span><span class="sxs-lookup"><span data-stu-id="26c44-133">In hello search box, type **Bime**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bime-tutorial/tutorial_bime_search.png)

5. <span data-ttu-id="26c44-135">Merhaba Sonuçlar panelinde seçin **Bime**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="26c44-135">In hello results panel, select **Bime**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bime-tutorial/tutorial_bime_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="26c44-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="26c44-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="26c44-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Bime sınayın.</span><span class="sxs-lookup"><span data-stu-id="26c44-138">In this section, you configure and test Azure AD single sign-on with Bime based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="26c44-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Bime içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="26c44-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Bime is tooa user in Azure AD.</span></span> <span data-ttu-id="26c44-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Bime hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="26c44-140">In other words, a link relationship between an Azure AD user and hello related user in Bime needs toobe established.</span></span>

<span data-ttu-id="26c44-141">Merhaba hello değeri Bime içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="26c44-141">In Bime, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="26c44-142">tooconfigure ve Bime ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="26c44-142">tooconfigure and test Azure AD single sign-on with Bime, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="26c44-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="26c44-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="26c44-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="26c44-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="26c44-145">**[Bime test kullanıcısı oluşturma](#creating-a-bime-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Bime içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="26c44-145">**[Creating a Bime test user](#creating-a-bime-test-user)** - toohave a counterpart of Britta Simon in Bime that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="26c44-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="26c44-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="26c44-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="26c44-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="26c44-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="26c44-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="26c44-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Bime uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="26c44-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Bime application.</span></span>

<span data-ttu-id="26c44-150">**tooconfigure Azure AD çoklu oturum açma ile Bime, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="26c44-150">**tooconfigure Azure AD single sign-on with Bime, perform hello following steps:**</span></span>

1. <span data-ttu-id="26c44-151">Hello hello üzerinde Azure portal'ın **Bime** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="26c44-151">In hello Azure portal, on hello **Bime** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="26c44-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="26c44-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bime-tutorial/tutorial_bime_samlbase.png)

3. <span data-ttu-id="26c44-155">Merhaba üzerinde **Bime etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="26c44-155">On hello **Bime Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bime-tutorial/tutorial_bime_url.png)

    <span data-ttu-id="26c44-157">a.</span><span class="sxs-lookup"><span data-stu-id="26c44-157">a.</span></span> <span data-ttu-id="26c44-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<tenant-name>.Bimeapp.com`</span><span class="sxs-lookup"><span data-stu-id="26c44-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.Bimeapp.com`</span></span>

    <span data-ttu-id="26c44-159">b.</span><span class="sxs-lookup"><span data-stu-id="26c44-159">b.</span></span> <span data-ttu-id="26c44-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<tenant-name>.Bimeapp.com`</span><span class="sxs-lookup"><span data-stu-id="26c44-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenant-name>.Bimeapp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="26c44-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="26c44-161">These values are not real.</span></span> <span data-ttu-id="26c44-162">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="26c44-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="26c44-163">Kişi [Bime istemci destek ekibi](https://bime.zendesk.com/hc/categories/202604307-Support-tech-notes-and-tips-) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="26c44-163">Contact [Bime Client support team](https://bime.zendesk.com/hc/categories/202604307-Support-tech-notes-and-tips-) tooget these values.</span></span> 
 
4. <span data-ttu-id="26c44-164">Merhaba üzerinde **SAML imzalama sertifikası** bölümü, kopyalama hello **parmak İZİ** hello sertifikasından değeri.</span><span class="sxs-lookup"><span data-stu-id="26c44-164">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value from hello certificate.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bime-tutorial/tutorial_bime_certificate.png) 

5. <span data-ttu-id="26c44-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="26c44-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bime-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="26c44-168">Merhaba üzerinde **Bime yapılandırma** 'yi tıklatın **yapılandırma Bime** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="26c44-168">On hello **Bime Configuration** section, click **Configure Bime** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="26c44-169">Kopya hello **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="26c44-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bime-tutorial/tutorial_bime_configure.png) 

7. <span data-ttu-id="26c44-171">Farklı web tarayıcısı penceresinde Bime şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="26c44-171">In a different web browser window, log into your Bime company site as an administrator.</span></span>

8. <span data-ttu-id="26c44-172">Merhaba araç çubuğunda **yönetici**ve ardından **hesap**.</span><span class="sxs-lookup"><span data-stu-id="26c44-172">In hello toolbar, click **Admin**, and then **Account**.</span></span>
   
    <span data-ttu-id="26c44-173">![Yönetici](./media/active-directory-saas-bime-tutorial/ic775558.png "yönetici")</span><span class="sxs-lookup"><span data-stu-id="26c44-173">![Admin](./media/active-directory-saas-bime-tutorial/ic775558.png "Admin")</span></span>

9. <span data-ttu-id="26c44-174">Merhaba hesap yapılandırma sayfasında hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="26c44-174">On hello account configuration page, perform hello following steps:</span></span>
   
    <span data-ttu-id="26c44-175">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-bime-tutorial/ic775559.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="26c44-175">![Configure Single Sign-On](./media/active-directory-saas-bime-tutorial/ic775559.png "Configure Single Sign-On")</span></span>
   
    <span data-ttu-id="26c44-176">a.</span><span class="sxs-lookup"><span data-stu-id="26c44-176">a.</span></span> <span data-ttu-id="26c44-177">Seçin **etkinleştirmek SAML kimlik doğrulaması**.</span><span class="sxs-lookup"><span data-stu-id="26c44-177">Select **Enable SAML authentication**.</span></span>

    <span data-ttu-id="26c44-178">b.</span><span class="sxs-lookup"><span data-stu-id="26c44-178">b.</span></span> <span data-ttu-id="26c44-179">Merhaba, **uzaktan oturum açma URL'si** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="26c44-179">In hello **Remote Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="26c44-180">c.</span><span class="sxs-lookup"><span data-stu-id="26c44-180">c.</span></span>  <span data-ttu-id="26c44-181">Yapıştır hello **parmak izi** hello Azure portalına değerinden **sertifika parmak izi** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="26c44-181">Paste hello **Thumbprint** value from Azure portal into hello **Certificate Fingerprint** textbox.</span></span>       
   
    <span data-ttu-id="26c44-182">d.</span><span class="sxs-lookup"><span data-stu-id="26c44-182">d.</span></span> <span data-ttu-id="26c44-183">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="26c44-183">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="26c44-184">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="26c44-184">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="26c44-185">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="26c44-185">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="26c44-186">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="26c44-186">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="26c44-187">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="26c44-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="26c44-188">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="26c44-188">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="26c44-190">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="26c44-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="26c44-191">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="26c44-191">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bime-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="26c44-193">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="26c44-193">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bime-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="26c44-195">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="26c44-195">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bime-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="26c44-197">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="26c44-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bime-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="26c44-199">a.</span><span class="sxs-lookup"><span data-stu-id="26c44-199">a.</span></span> <span data-ttu-id="26c44-200">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="26c44-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="26c44-201">b.</span><span class="sxs-lookup"><span data-stu-id="26c44-201">b.</span></span> <span data-ttu-id="26c44-202">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="26c44-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="26c44-203">c.</span><span class="sxs-lookup"><span data-stu-id="26c44-203">c.</span></span> <span data-ttu-id="26c44-204">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="26c44-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="26c44-205">d.</span><span class="sxs-lookup"><span data-stu-id="26c44-205">d.</span></span> <span data-ttu-id="26c44-206">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="26c44-206">Click **Create**.</span></span>
 
### <a name="creating-a-bime-test-user"></a><span data-ttu-id="26c44-207">Bime test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="26c44-207">Creating a Bime test user</span></span>

<span data-ttu-id="26c44-208">TooBime içinde sipariş tooenable Azure AD kullanıcıların toolog bunların Bime sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="26c44-208">In order tooenable Azure AD users toolog in tooBime, they must be provisioned into Bime.</span></span> <span data-ttu-id="26c44-209">Bime Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="26c44-209">In hello case of Bime, provisioning is a manual task.</span></span>

<span data-ttu-id="26c44-210">**tooconfigure kullanıcı hazırlama, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="26c44-210">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="26c44-211">İçinde tooyour oturum **Bime** Kiracı.</span><span class="sxs-lookup"><span data-stu-id="26c44-211">Log in tooyour **Bime** tenant.</span></span>

2. <span data-ttu-id="26c44-212">Merhaba araç çubuğunda **yönetici**ve ardından **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="26c44-212">In hello toolbar, click **Admin**, and then **Users**.</span></span>
   
    <span data-ttu-id="26c44-213">![Yönetici](./media/active-directory-saas-bime-tutorial/ic775561.png "yönetici")</span><span class="sxs-lookup"><span data-stu-id="26c44-213">![Admin](./media/active-directory-saas-bime-tutorial/ic775561.png "Admin")</span></span>

3. <span data-ttu-id="26c44-214">Merhaba, **kullanıcılar listesi**, tıklatın **yeni kullanıcı Ekle** ("+").</span><span class="sxs-lookup"><span data-stu-id="26c44-214">In hello **Users List**, click **Add New User** (“+”).</span></span>
   
    <span data-ttu-id="26c44-215">![Kullanıcıların](./media/active-directory-saas-bime-tutorial/ic775562.png "kullanıcılar")</span><span class="sxs-lookup"><span data-stu-id="26c44-215">![Users](./media/active-directory-saas-bime-tutorial/ic775562.png "Users")</span></span>

4. <span data-ttu-id="26c44-216">Merhaba üzerinde **kullanıcı ayrıntıları** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="26c44-216">On hello **User Details** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="26c44-217">![Kullanıcı ayrıntılarını](./media/active-directory-saas-bime-tutorial/ic775563.png "kullanıcı ayrıntıları")</span><span class="sxs-lookup"><span data-stu-id="26c44-217">![User Details](./media/active-directory-saas-bime-tutorial/ic775563.png "User Details")</span></span>
   
    <span data-ttu-id="26c44-218">a.</span><span class="sxs-lookup"><span data-stu-id="26c44-218">a.</span></span> <span data-ttu-id="26c44-219">Merhaba, **ad** metin kutusuna, hello ilk gibi kullanıcı adını girin **Britta**.</span><span class="sxs-lookup"><span data-stu-id="26c44-219">In hello **First name** textbox, enter hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="26c44-220">b.</span><span class="sxs-lookup"><span data-stu-id="26c44-220">b.</span></span> <span data-ttu-id="26c44-221">Merhaba, **Soyadı** metin kutusuna, hello son gibi kullanıcı adını girin **Simon**.</span><span class="sxs-lookup"><span data-stu-id="26c44-221">In hello **Last name** textbox, enter hello last name of user like **Simon**.</span></span>
 
    <span data-ttu-id="26c44-222">c.</span><span class="sxs-lookup"><span data-stu-id="26c44-222">c.</span></span> <span data-ttu-id="26c44-223">Merhaba, **e-posta** metin kutusuna, bir kullanıcı gibi hello e-posta girin  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="26c44-223">In hello **Email** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="26c44-224">d.</span><span class="sxs-lookup"><span data-stu-id="26c44-224">d.</span></span> <span data-ttu-id="26c44-225">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="26c44-225">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="26c44-226">API AAD kullanıcı hesaplarının Bime tooprovision tarafından sağlanan veya herhangi diğer Bime kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="26c44-226">You can use any other Bime user account creation tools or APIs provided by Bime tooprovision AAD user accounts.</span></span>
>  

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="26c44-227">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="26c44-227">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="26c44-228">Bu bölümde, erişim tooBime vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="26c44-228">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBime.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="26c44-230">**tooassign Britta Simon tooBime hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="26c44-230">**tooassign Britta Simon tooBime, perform hello following steps:**</span></span>

1. <span data-ttu-id="26c44-231">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="26c44-231">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="26c44-233">Merhaba uygulamalar listesinde **Bime**.</span><span class="sxs-lookup"><span data-stu-id="26c44-233">In hello applications list, select **Bime**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bime-tutorial/tutorial_bime_app.png) 

3. <span data-ttu-id="26c44-235">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="26c44-235">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="26c44-237">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="26c44-237">Click **Add** button.</span></span> <span data-ttu-id="26c44-238">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="26c44-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="26c44-240">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="26c44-240">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="26c44-241">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="26c44-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="26c44-242">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="26c44-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="26c44-243">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="26c44-243">Testing single sign-on</span></span>

<span data-ttu-id="26c44-244">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="26c44-244">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="26c44-245">Merhaba Bime hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Bime uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="26c44-245">When you click hello Bime tile in hello Access Panel, you should get automatically signed-on tooyour Bime application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="26c44-246">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="26c44-246">Additional resources</span></span>

* [<span data-ttu-id="26c44-247">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="26c44-247">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="26c44-248">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="26c44-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bime-tutorial/tutorial_general_203.png

