---
title: "Öğretici: Azure Active Directory Tümleştirme ile Panopto | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Panopto arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 89c88e23-93ce-4970-9baa-1104c4e8fe4a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 76b30e1cd2782bb5fba3d229378b8f82652b6503
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-panopto"></a><span data-ttu-id="948d5-103">Öğretici: Azure Active Directory Tümleştirme Panopto ile</span><span class="sxs-lookup"><span data-stu-id="948d5-103">Tutorial: Azure Active Directory integration with Panopto</span></span>

<span data-ttu-id="948d5-104">Bu öğreticide, bilgi nasıl toointegrate Panopto Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="948d5-104">In this tutorial, you learn how toointegrate Panopto with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="948d5-105">Panopto Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="948d5-105">Integrating Panopto with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="948d5-106">Erişim tooPanopto sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="948d5-106">You can control in Azure AD who has access tooPanopto</span></span>
- <span data-ttu-id="948d5-107">Kullanıcıların tooautomatically get açan tooPanopto (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="948d5-107">You can enable your users tooautomatically get signed-on tooPanopto (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="948d5-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="948d5-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="948d5-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="948d5-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="948d5-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="948d5-110">Prerequisites</span></span>

<span data-ttu-id="948d5-111">tooconfigure Panopto ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="948d5-111">tooconfigure Azure AD integration with Panopto, you need hello following items:</span></span>

- <span data-ttu-id="948d5-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="948d5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="948d5-113">Bir Panopto çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="948d5-113">A Panopto single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="948d5-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="948d5-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="948d5-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="948d5-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="948d5-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="948d5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="948d5-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="948d5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="948d5-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="948d5-118">Scenario description</span></span>
<span data-ttu-id="948d5-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="948d5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="948d5-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="948d5-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="948d5-121">Merhaba Galerisi'nden Panopto ekleme</span><span class="sxs-lookup"><span data-stu-id="948d5-121">Adding Panopto from hello gallery</span></span>
2. <span data-ttu-id="948d5-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="948d5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-panopto-from-hello-gallery"></a><span data-ttu-id="948d5-123">Merhaba Galerisi'nden Panopto ekleme</span><span class="sxs-lookup"><span data-stu-id="948d5-123">Adding Panopto from hello gallery</span></span>
<span data-ttu-id="948d5-124">Azure AD'ye tooconfigure hello tümleştirme Panopto, tooadd Panopto hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="948d5-124">tooconfigure hello integration of Panopto into Azure AD, you need tooadd Panopto from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="948d5-125">**tooadd Panopto hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="948d5-125">**tooadd Panopto from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="948d5-126">Merhaba, ** [Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="948d5-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="948d5-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="948d5-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="948d5-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="948d5-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="948d5-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="948d5-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="948d5-133">Merhaba arama kutusuna yazın **Panopto**.</span><span class="sxs-lookup"><span data-stu-id="948d5-133">In hello search box, type **Panopto**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_search.png)

5. <span data-ttu-id="948d5-135">Merhaba Sonuçlar panelinde seçin **Panopto**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="948d5-135">In hello results panel, select **Panopto**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="948d5-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="948d5-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="948d5-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Panopto ile test etme</span><span class="sxs-lookup"><span data-stu-id="948d5-138">In this section, you configure and test Azure AD single sign-on with Panopto based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="948d5-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Panopto içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="948d5-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Panopto is tooa user in Azure AD.</span></span> <span data-ttu-id="948d5-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Panopto hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="948d5-140">In other words, a link relationship between an Azure AD user and hello related user in Panopto needs toobe established.</span></span>

<span data-ttu-id="948d5-141">Merhaba hello değeri Panopto içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="948d5-141">In Panopto, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="948d5-142">tooconfigure ve Panopto ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="948d5-142">tooconfigure and test Azure AD single sign-on with Panopto, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="948d5-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on) ** -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="948d5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="948d5-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user) ** -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="948d5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="948d5-145">**[Panopto test kullanıcısı oluşturma](#creating-a-panopto-test-user) ** -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Panopto içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="948d5-145">**[Creating a Panopto test user](#creating-a-panopto-test-user)** - toohave a counterpart of Britta Simon in Panopto that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="948d5-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="948d5-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="948d5-147">**[Çoklu oturum açmayı test](#testing-single-sign-on) ** -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="948d5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="948d5-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="948d5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="948d5-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Panopto uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="948d5-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Panopto application.</span></span>

<span data-ttu-id="948d5-150">**tooconfigure Azure AD çoklu oturum açma ile Panopto, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="948d5-150">**tooconfigure Azure AD single sign-on with Panopto, perform hello following steps:**</span></span>

1. <span data-ttu-id="948d5-151">Hello hello üzerinde Azure portal'ın **Panopto** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="948d5-151">In hello Azure portal, on hello **Panopto** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="948d5-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="948d5-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_samlbase.png)

3. <span data-ttu-id="948d5-155">Merhaba üzerinde **Panopto etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="948d5-155">On hello **Panopto Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_url.png)

    <span data-ttu-id="948d5-157">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<tenant-name>.panopto.com`</span><span class="sxs-lookup"><span data-stu-id="948d5-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.panopto.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="948d5-158">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="948d5-158">This value is not real.</span></span> <span data-ttu-id="948d5-159">Bu değer ile Merhaba güncelleştirme gerçek oturum açma URL'si.</span><span class="sxs-lookup"><span data-stu-id="948d5-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="948d5-160">Kişi [Panopto istemci destek ekibi](mailto:support@panopto.com‎) tooget bu değer.</span><span class="sxs-lookup"><span data-stu-id="948d5-160">Contact [Panopto Client support team](mailto:support@panopto.com‎) tooget this value.</span></span> 
 
4. <span data-ttu-id="948d5-161">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="948d5-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_certificate.png) 

5. <span data-ttu-id="948d5-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="948d5-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-panopto-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="948d5-165">Merhaba üzerinde **Panopto yapılandırma** 'yi tıklatın **yapılandırma Panopto** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="948d5-165">On hello **Panopto Configuration** section, click **Configure Panopto** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="948d5-166">Kopya hello **SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="948d5-166">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_configure.png) 

7. <span data-ttu-id="948d5-168">Farklı web tarayıcısı penceresinde tooyour Panopto şirket sitede yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="948d5-168">In a different web browser window, log in tooyour Panopto company site as an administrator.</span></span>

8. <span data-ttu-id="948d5-169">Merhaba soldaki Hello araç çubuğunda **sistem**ve ardından **kimlik sağlayıcıları**.</span><span class="sxs-lookup"><span data-stu-id="948d5-169">In hello toolbar on hello left, click **System**, and then click **Identity Providers**.</span></span>
   
   <span data-ttu-id="948d5-170">![Sistem](./media/active-directory-saas-panopto-tutorial/ic777670.png "sistem")</span><span class="sxs-lookup"><span data-stu-id="948d5-170">![System](./media/active-directory-saas-panopto-tutorial/ic777670.png "System")</span></span>
9. <span data-ttu-id="948d5-171">Tıklatın **Sağlayıcı eklemek**.</span><span class="sxs-lookup"><span data-stu-id="948d5-171">Click **Add Provider**.</span></span>
   
   <span data-ttu-id="948d5-172">![Kimlik sağlayıcılar](./media/active-directory-saas-panopto-tutorial/ic777671.png "kimlik sağlayıcıları")</span><span class="sxs-lookup"><span data-stu-id="948d5-172">![Identity Providers](./media/active-directory-saas-panopto-tutorial/ic777671.png "Identity Providers")</span></span>
   
10. <span data-ttu-id="948d5-173">Hello SAML sağlayıcısı bölümü, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="948d5-173">In hello SAML provider section, perform hello following steps:</span></span>
   
    <span data-ttu-id="948d5-174">![SaaS yapılandırma](./media/active-directory-saas-panopto-tutorial/ic777672.png "SaaS yapılandırma")</span><span class="sxs-lookup"><span data-stu-id="948d5-174">![SaaS configuration](./media/active-directory-saas-panopto-tutorial/ic777672.png "SaaS configuration")</span></span>
    
    <span data-ttu-id="948d5-175">a.</span><span class="sxs-lookup"><span data-stu-id="948d5-175">a.</span></span> <span data-ttu-id="948d5-176">Merhaba gelen **sağlayıcı türü** listesinde **SAML20**.</span><span class="sxs-lookup"><span data-stu-id="948d5-176">From hello **Provider Type** list, select **SAML20**.</span></span>    
    
    <span data-ttu-id="948d5-177">b.</span><span class="sxs-lookup"><span data-stu-id="948d5-177">b.</span></span> <span data-ttu-id="948d5-178">Merhaba, **örnek adı** metin kutusuna, hello örneği için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="948d5-178">In hello **Instance Name** textbox, type a name for hello instance.</span></span>

    <span data-ttu-id="948d5-179">c.</span><span class="sxs-lookup"><span data-stu-id="948d5-179">c.</span></span> <span data-ttu-id="948d5-180">Merhaba, **anlaşılır bir açıklama** metin kutusuna, kolay bir açıklama yazın.</span><span class="sxs-lookup"><span data-stu-id="948d5-180">In hello **Friendly Description** textbox, type a friendly description.</span></span>
    
    <span data-ttu-id="948d5-181">d.</span><span class="sxs-lookup"><span data-stu-id="948d5-181">d.</span></span> <span data-ttu-id="948d5-182">İçinde **Sıçrama sayfa URL'si** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="948d5-182">In **Bounce Page Url** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="948d5-183">e.</span><span class="sxs-lookup"><span data-stu-id="948d5-183">e.</span></span> <span data-ttu-id="948d5-184">Merhaba, **veren** metin kutusuna, Yapıştır hello değerini **SAML varlık kimliği**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="948d5-184">In hello **Issuer** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="948d5-185">f.</span><span class="sxs-lookup"><span data-stu-id="948d5-185">f.</span></span> <span data-ttu-id="948d5-186">Azure portal, kopyalama hello tooyour Pano'da bunu içerik gelen yüklediğiniz, base-64 kodlanmış sertifika açın ve ardından toohello yapıştırın **ortak anahtar** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="948d5-186">Open your base-64 encoded certificate, which you have downloaded from Azure portal, copy hello content of it in tooyour clipboard, and then paste it toohello **Public Key**  textbox.</span></span>

11. <span data-ttu-id="948d5-187">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="948d5-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="948d5-188">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="948d5-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="948d5-189">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere ** Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="948d5-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="948d5-190">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="948d5-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="948d5-191">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="948d5-191">Creating an Azure AD test user</span></span>

<span data-ttu-id="948d5-192">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="948d5-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="948d5-194">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="948d5-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="948d5-195">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="948d5-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-panopto-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="948d5-197">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="948d5-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-panopto-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="948d5-199">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="948d5-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-panopto-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="948d5-201">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="948d5-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-panopto-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="948d5-203">a.</span><span class="sxs-lookup"><span data-stu-id="948d5-203">a.</span></span> <span data-ttu-id="948d5-204">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="948d5-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="948d5-205">b.</span><span class="sxs-lookup"><span data-stu-id="948d5-205">b.</span></span> <span data-ttu-id="948d5-206">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="948d5-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="948d5-207">c.</span><span class="sxs-lookup"><span data-stu-id="948d5-207">c.</span></span> <span data-ttu-id="948d5-208">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="948d5-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="948d5-209">d.</span><span class="sxs-lookup"><span data-stu-id="948d5-209">d.</span></span> <span data-ttu-id="948d5-210">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="948d5-210">Click **Create**.</span></span>
 
### <a name="creating-a-panopto-test-user"></a><span data-ttu-id="948d5-211">Panopto test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="948d5-211">Creating a Panopto test user</span></span>

<span data-ttu-id="948d5-212">TooPanopto sağlama, tooconfigure kullanıcı için eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="948d5-212">There is no action item for you tooconfigure user provisioning tooPanopto.</span></span>  
<span data-ttu-id="948d5-213">Atanmış bir kullanıcı hello erişim paneli kullanılarak tooPanopto toolog çalıştığında Panopto hello kullanıcı var olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="948d5-213">When an assigned user tries toolog in tooPanopto using hello access panel, Panopto checks whether hello user exists.</span></span>  

<span data-ttu-id="948d5-214">Hiçbir kullanıcı hesabı varsa kullanılabilir henüz, Panopto tarafından otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="948d5-214">If there is no user account available yet, it is automatically created by Panopto.</span></span>

>[!NOTE]
><span data-ttu-id="948d5-215">API'leri, Azure AD kullanıcı hesapları Panopto tooprovision tarafından sağlanan veya herhangi diğer Panopto kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="948d5-215">You can use any other Panopto user account creation tools or APIs provided by Panopto tooprovision Azure AD user accounts.</span></span>
>
>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="948d5-216">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="948d5-216">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="948d5-217">Bu bölümde, erişim tooPanopto vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="948d5-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPanopto.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="948d5-219">**tooassign Britta Simon tooPanopto hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="948d5-219">**tooassign Britta Simon tooPanopto, perform hello following steps:**</span></span>

1. <span data-ttu-id="948d5-220">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="948d5-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="948d5-222">Merhaba uygulamalar listesinde **Panopto**.</span><span class="sxs-lookup"><span data-stu-id="948d5-222">In hello applications list, select **Panopto**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_app.png) 

3. <span data-ttu-id="948d5-224">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="948d5-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="948d5-226">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="948d5-226">Click **Add** button.</span></span> <span data-ttu-id="948d5-227">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="948d5-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="948d5-229">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="948d5-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="948d5-230">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="948d5-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="948d5-231">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="948d5-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="948d5-232">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="948d5-232">Testing single sign-on</span></span>

<span data-ttu-id="948d5-233">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="948d5-233">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="948d5-234">Merhaba Panopto hello erişim paneli parçasında tıkladığınızda, oturum açma sayfasına Panopto uygulamasının otomatik olarak almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="948d5-234">When you click hello Panopto tile in hello Access Panel, you should get automatically login page of Panopto application.</span></span>
<span data-ttu-id="948d5-235">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="948d5-235">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="948d5-236">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="948d5-236">Additional resources</span></span>

* [<span data-ttu-id="948d5-237">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="948d5-237">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="948d5-238">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="948d5-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_203.png

