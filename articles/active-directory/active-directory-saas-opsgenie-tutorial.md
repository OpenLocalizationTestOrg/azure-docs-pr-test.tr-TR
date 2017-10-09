---
title: "Öğretici: Azure Active Directory Tümleştirme ile OpsGenie | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile OpsGenie arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 41b59b22-a61d-4fe6-ab0d-6c3991d1375f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 50d31c234fb9716d05d681b9bc4164740a3a662b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-opsgenie"></a><span data-ttu-id="96183-103">Öğretici: Azure Active Directory Tümleştirme OpsGenie ile</span><span class="sxs-lookup"><span data-stu-id="96183-103">Tutorial: Azure Active Directory integration with OpsGenie</span></span>

<span data-ttu-id="96183-104">Bu öğreticide, bilgi nasıl toointegrate OpsGenie Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="96183-104">In this tutorial, you learn how toointegrate OpsGenie with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="96183-105">OpsGenie Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="96183-105">Integrating OpsGenie with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="96183-106">Erişim tooOpsGenie sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="96183-106">You can control in Azure AD who has access tooOpsGenie</span></span>
- <span data-ttu-id="96183-107">Kullanıcıların tooautomatically get açan tooOpsGenie (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="96183-107">You can enable your users tooautomatically get signed-on tooOpsGenie (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="96183-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="96183-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="96183-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="96183-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="96183-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="96183-110">Prerequisites</span></span>

<span data-ttu-id="96183-111">tooconfigure OpsGenie ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="96183-111">tooconfigure Azure AD integration with OpsGenie, you need hello following items:</span></span>

- <span data-ttu-id="96183-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="96183-112">An Azure AD subscription</span></span>
- <span data-ttu-id="96183-113">Bir OpsGenie çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="96183-113">A OpsGenie single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="96183-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="96183-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="96183-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="96183-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="96183-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="96183-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="96183-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="96183-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="96183-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="96183-118">Scenario description</span></span>
<span data-ttu-id="96183-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="96183-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="96183-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="96183-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="96183-121">Merhaba Galerisi'nden OpsGenie ekleme</span><span class="sxs-lookup"><span data-stu-id="96183-121">Adding OpsGenie from hello gallery</span></span>
2. <span data-ttu-id="96183-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="96183-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-opsgenie-from-hello-gallery"></a><span data-ttu-id="96183-123">Merhaba Galerisi'nden OpsGenie ekleme</span><span class="sxs-lookup"><span data-stu-id="96183-123">Adding OpsGenie from hello gallery</span></span>
<span data-ttu-id="96183-124">Azure AD'ye tooconfigure hello tümleştirme OpsGenie, tooadd OpsGenie hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="96183-124">tooconfigure hello integration of OpsGenie into Azure AD, you need tooadd OpsGenie from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="96183-125">**tooadd OpsGenie hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="96183-125">**tooadd OpsGenie from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="96183-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="96183-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="96183-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="96183-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="96183-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="96183-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="96183-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="96183-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="96183-133">Merhaba arama kutusuna yazın **OpsGenie**.</span><span class="sxs-lookup"><span data-stu-id="96183-133">In hello search box, type **OpsGenie**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_search.png)

5. <span data-ttu-id="96183-135">Merhaba Sonuçlar panelinde seçin **OpsGenie**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="96183-135">In hello results panel, select **OpsGenie**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="96183-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="96183-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="96183-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı OpsGenie sınayın.</span><span class="sxs-lookup"><span data-stu-id="96183-138">In this section, you configure and test Azure AD single sign-on with OpsGenie based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="96183-139">Tek toowork'ın oturum açma hangi hello karşılık gelen OpsGenie içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="96183-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in OpsGenie is tooa user in Azure AD.</span></span> <span data-ttu-id="96183-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı OpsGenie hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="96183-140">In other words, a link relationship between an Azure AD user and hello related user in OpsGenie needs toobe established.</span></span>

<span data-ttu-id="96183-141">Merhaba hello değeri OpsGenie içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="96183-141">In OpsGenie, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="96183-142">tooconfigure ve OpsGenie ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="96183-142">tooconfigure and test Azure AD single sign-on with OpsGenie, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="96183-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="96183-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="96183-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="96183-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="96183-145">**[OpsGenie test kullanıcısı oluşturma](#creating-a-opsgenie-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir OpsGenie içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="96183-145">**[Creating a OpsGenie test user](#creating-a-opsgenie-test-user)** - toohave a counterpart of Britta Simon in OpsGenie that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="96183-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="96183-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="96183-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="96183-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="96183-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="96183-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="96183-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma OpsGenie uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="96183-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your OpsGenie application.</span></span>

<span data-ttu-id="96183-150">**tooconfigure Azure AD çoklu oturum açma ile OpsGenie, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="96183-150">**tooconfigure Azure AD single sign-on with OpsGenie, perform hello following steps:**</span></span>

1. <span data-ttu-id="96183-151">Hello hello üzerinde Azure portal'ın **OpsGenie** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="96183-151">In hello Azure portal, on hello **OpsGenie** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="96183-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="96183-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_samlbase.png)

3. <span data-ttu-id="96183-155">Merhaba üzerinde **OpsGenie etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="96183-155">On hello **OpsGenie Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_url.png)

    <span data-ttu-id="96183-157">Merhaba, **oturum açma URL'si** metin kutusuna, türü hello URL'si:`https://app.opsgenie.com/auth/login`</span><span class="sxs-lookup"><span data-stu-id="96183-157">In hello **Sign-on URL** textbox, type hello URL: `https://app.opsgenie.com/auth/login`</span></span>

4. <span data-ttu-id="96183-158">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="96183-158">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_certificate.png) 

5. <span data-ttu-id="96183-160">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="96183-160">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-opsgenie-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="96183-162">Merhaba üzerinde **OpsGenie yapılandırma** 'yi tıklatın **yapılandırma OpsGenie** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="96183-162">On hello **OpsGenie Configuration** section, click **Configure OpsGenie** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="96183-163">Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="96183-163">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_configure.png) 

7. <span data-ttu-id="96183-165">Başka bir tarayıcı örneği açın ve sonra oturum açma tooOpsGenie yönetici olarak.</span><span class="sxs-lookup"><span data-stu-id="96183-165">Open another browser instance, and then log-in tooOpsGenie as an administrator.</span></span>

8. <span data-ttu-id="96183-166">' I tıklatın **ayarları**ve ardından hello **çoklu oturum açma** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="96183-166">Click **Settings**, and then click hello **Single Sign On** tab.</span></span>
   
    ![OpsGenie çoklu oturum açma](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_06.png)

9. <span data-ttu-id="96183-168">SSO, tooenable seçin **etkin**.</span><span class="sxs-lookup"><span data-stu-id="96183-168">tooenable SSO, select **Enabled**.</span></span>
   
    ![OpsGenie ayarları](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_07.png) 

10. <span data-ttu-id="96183-170">Merhaba, **sağlayıcı** bölümünde, hello tıklatın **Azure Active Directory** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="96183-170">In hello **Provider** section, click hello **Azure Active Directory** tab.</span></span>
   
    ![OpsGenie ayarları](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_08.png) 

11. <span data-ttu-id="96183-172">Hello Azure Active Directory iletişim sayfasında hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="96183-172">On hello Azure Active Directory dialog page, perform hello following steps:</span></span>
   
    ![OpsGenie ayarları](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_09.png)
    
    <span data-ttu-id="96183-174">a.</span><span class="sxs-lookup"><span data-stu-id="96183-174">a.</span></span> <span data-ttu-id="96183-175">Yapıştır **tek oturum üzerinde hizmet URL'si**, hello hello Azure portal ' Kopyalanan **SAML 2.0 Endpoint** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="96183-175">Paste **Single Sign On Service URL**, which you have copied from hello Azure portal into hello **SAML 2.0 Endpoint** textbox.</span></span>
    
    <span data-ttu-id="96183-176">b.</span><span class="sxs-lookup"><span data-stu-id="96183-176">b.</span></span> <span data-ttu-id="96183-177">İndirilen base-64 kodlanmış sertifika kopyalama hello panonuza bunu içerik Not Defteri'nde açın ve hello yapıştırma **X.500 sertifika** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="96183-177">Open your downloaded base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it into hello **X.500 Certificate** textbox.</span></span>
    
    <span data-ttu-id="96183-178">c.</span><span class="sxs-lookup"><span data-stu-id="96183-178">c.</span></span> <span data-ttu-id="96183-179">Tıklatın **değişiklikleri kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="96183-179">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="96183-180">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="96183-180">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="96183-181">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="96183-181">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="96183-182">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="96183-182">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="96183-183">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="96183-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="96183-184">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="96183-184">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="96183-186">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="96183-186">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="96183-187">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="96183-187">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="96183-189">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="96183-189">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="96183-191">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="96183-191">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="96183-193">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="96183-193">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="96183-195">a.</span><span class="sxs-lookup"><span data-stu-id="96183-195">a.</span></span> <span data-ttu-id="96183-196">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="96183-196">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="96183-197">b.</span><span class="sxs-lookup"><span data-stu-id="96183-197">b.</span></span> <span data-ttu-id="96183-198">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="96183-198">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="96183-199">c.</span><span class="sxs-lookup"><span data-stu-id="96183-199">c.</span></span> <span data-ttu-id="96183-200">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="96183-200">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="96183-201">d.</span><span class="sxs-lookup"><span data-stu-id="96183-201">d.</span></span> <span data-ttu-id="96183-202">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="96183-202">Click **Create**.</span></span>
 
### <a name="creating-a-opsgenie-test-user"></a><span data-ttu-id="96183-203">OpsGenie test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="96183-203">Creating a OpsGenie test user</span></span>

<span data-ttu-id="96183-204">Bu bölümde Hello amacı toocreate Britta Simon içinde OpsGenie adlı bir kullanıcı ' dir.</span><span class="sxs-lookup"><span data-stu-id="96183-204">hello objective of this section is toocreate a user called Britta Simon in OpsGenie.</span></span> 

1. <span data-ttu-id="96183-205">Bir web tarayıcısı penceresinde OpsGenie Kiracı yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="96183-205">In a web browser window, log into your OpsGenie tenant as an administrator.</span></span>

2. <span data-ttu-id="96183-206">Tıklayarak tooUsers listesi gidin **kullanıcı** sol panelinde.</span><span class="sxs-lookup"><span data-stu-id="96183-206">Navigate tooUsers list by clicking **User** in left panel.</span></span>
   
   ![OpsGenie ayarları](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_10.png) 

3. <span data-ttu-id="96183-208">Tıklatın **kullanıcı ekleme**.</span><span class="sxs-lookup"><span data-stu-id="96183-208">Click **Add User**.</span></span>

4. <span data-ttu-id="96183-209">Merhaba üzerinde **Kullanıcı Ekle** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="96183-209">On hello **Add User** dialog, perform hello following steps:</span></span>
   
   ![OpsGenie ayarları](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_11.png)
   
   <span data-ttu-id="96183-211">a.</span><span class="sxs-lookup"><span data-stu-id="96183-211">a.</span></span> <span data-ttu-id="96183-212">Merhaba, **e-posta** metin kutusuna, Azure Active Directory'de ele BrittaSimon, hello e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="96183-212">In hello **Email** textbox, type hello email address of BrittaSimon addressed in Azure Active Directory.</span></span>
   
   <span data-ttu-id="96183-213">b.</span><span class="sxs-lookup"><span data-stu-id="96183-213">b.</span></span> <span data-ttu-id="96183-214">Merhaba, **tam adı** metin kutusuna, türü **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="96183-214">In hello **Full Name** textbox, type **Britta Simon**.</span></span>
   
   <span data-ttu-id="96183-215">c.</span><span class="sxs-lookup"><span data-stu-id="96183-215">c.</span></span> <span data-ttu-id="96183-216">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="96183-216">Click **Save**.</span></span> 

>[!NOTE]
><span data-ttu-id="96183-217">Britta kendi profili ayarlama yönergeleri içeren bir e-posta alır.</span><span class="sxs-lookup"><span data-stu-id="96183-217">Britta gets an email with instructions for setting up her profile.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="96183-218">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="96183-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="96183-219">Bu bölümde, erişim tooOpsGenie vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="96183-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooOpsGenie.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="96183-221">**tooassign Britta Simon tooOpsGenie hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="96183-221">**tooassign Britta Simon tooOpsGenie, perform hello following steps:**</span></span>

1. <span data-ttu-id="96183-222">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="96183-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="96183-224">Merhaba uygulamalar listesinde **OpsGenie**.</span><span class="sxs-lookup"><span data-stu-id="96183-224">In hello applications list, select **OpsGenie**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_app.png) 

3. <span data-ttu-id="96183-226">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="96183-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="96183-228">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="96183-228">Click **Add** button.</span></span> <span data-ttu-id="96183-229">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="96183-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="96183-231">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="96183-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="96183-232">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="96183-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="96183-233">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="96183-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="96183-234">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="96183-234">Testing single sign-on</span></span>

<span data-ttu-id="96183-235">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD SSO yapılandırmayı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="96183-235">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="96183-236">Merhaba OpsGenie hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour OpsGenie uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="96183-236">When you click hello OpsGenie tile in hello Access Panel, you should get automatically signed-on tooyour OpsGenie application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="96183-237">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="96183-237">Additional resources</span></span>

* [<span data-ttu-id="96183-238">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="96183-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="96183-239">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="96183-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_203.png

