---
title: "Öğretici: Azure Active Directory Tümleştirme ile Pantheon | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Pantheon arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2c965d1-666f-44c2-b08f-b73163096374
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 5c3e54aef1f64dbab77d40a8c098172d609bfec8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pantheon"></a><span data-ttu-id="37c21-103">Öğretici: Azure Active Directory Tümleştirme Pantheon ile</span><span class="sxs-lookup"><span data-stu-id="37c21-103">Tutorial: Azure Active Directory integration with Pantheon</span></span>

<span data-ttu-id="37c21-104">Bu öğreticide, bilgi nasıl toointegrate Pantheon Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="37c21-104">In this tutorial, you learn how toointegrate Pantheon with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="37c21-105">Pantheon Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="37c21-105">Integrating Pantheon with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="37c21-106">Erişim tooPantheon sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="37c21-106">You can control in Azure AD who has access tooPantheon</span></span>
- <span data-ttu-id="37c21-107">Kullanıcıların tooautomatically get açan tooPantheon (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="37c21-107">You can enable your users tooautomatically get signed-on tooPantheon (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="37c21-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="37c21-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="37c21-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="37c21-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="37c21-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="37c21-110">Prerequisites</span></span>

<span data-ttu-id="37c21-111">tooconfigure Pantheon ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="37c21-111">tooconfigure Azure AD integration with Pantheon, you need hello following items:</span></span>

- <span data-ttu-id="37c21-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="37c21-112">An Azure AD subscription</span></span>
- <span data-ttu-id="37c21-113">Bir Pantheon çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="37c21-113">A Pantheon single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="37c21-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="37c21-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="37c21-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="37c21-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="37c21-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="37c21-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="37c21-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="37c21-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="37c21-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="37c21-118">Scenario description</span></span>
<span data-ttu-id="37c21-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="37c21-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="37c21-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="37c21-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="37c21-121">Merhaba Galerisi'nden Pantheon ekleme</span><span class="sxs-lookup"><span data-stu-id="37c21-121">Adding Pantheon from hello gallery</span></span>
2. <span data-ttu-id="37c21-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="37c21-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pantheon-from-hello-gallery"></a><span data-ttu-id="37c21-123">Merhaba Galerisi'nden Pantheon ekleme</span><span class="sxs-lookup"><span data-stu-id="37c21-123">Adding Pantheon from hello gallery</span></span>
<span data-ttu-id="37c21-124">Azure AD'ye tooconfigure hello tümleştirme Pantheon, tooadd Pantheon hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="37c21-124">tooconfigure hello integration of Pantheon into Azure AD, you need tooadd Pantheon from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="37c21-125">**tooadd Pantheon hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="37c21-125">**tooadd Pantheon from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="37c21-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="37c21-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="37c21-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="37c21-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="37c21-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="37c21-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="37c21-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="37c21-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="37c21-133">Merhaba arama kutusuna yazın **Pantheon**.</span><span class="sxs-lookup"><span data-stu-id="37c21-133">In hello search box, type **Pantheon**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_search.png)

5. <span data-ttu-id="37c21-135">Merhaba Sonuçlar panelinde seçin **Pantheon**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="37c21-135">In hello results panel, select **Pantheon**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="37c21-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="37c21-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="37c21-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Pantheon sınayın.</span><span class="sxs-lookup"><span data-stu-id="37c21-138">In this section, you configure and test Azure AD single sign-on with Pantheon based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="37c21-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Pantheon içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="37c21-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Pantheon is tooa user in Azure AD.</span></span> <span data-ttu-id="37c21-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Pantheon hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="37c21-140">In other words, a link relationship between an Azure AD user and hello related user in Pantheon needs toobe established.</span></span>

<span data-ttu-id="37c21-141">Merhaba hello değeri Pantheon içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="37c21-141">In Pantheon, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="37c21-142">tooconfigure ve Pantheon ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="37c21-142">tooconfigure and test Azure AD single sign-on with Pantheon, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="37c21-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="37c21-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="37c21-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="37c21-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="37c21-145">**[Pantheon test kullanıcısı oluşturma](#creating-a-pantheon-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Pantheon içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="37c21-145">**[Creating a Pantheon test user](#creating-a-pantheon-test-user)** - toohave a counterpart of Britta Simon in Pantheon that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="37c21-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="37c21-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="37c21-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="37c21-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="37c21-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="37c21-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="37c21-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Pantheon uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="37c21-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Pantheon application.</span></span>

<span data-ttu-id="37c21-150">**tooconfigure Azure AD çoklu oturum açma ile Pantheon, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="37c21-150">**tooconfigure Azure AD single sign-on with Pantheon, perform hello following steps:**</span></span>

1. <span data-ttu-id="37c21-151">Hello hello üzerinde Azure portal'ın **Pantheon** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="37c21-151">In hello Azure portal, on hello **Pantheon** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="37c21-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="37c21-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_samlbase.png)

3. <span data-ttu-id="37c21-155">Merhaba üzerinde **Pantheon etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="37c21-155">On hello **Pantheon Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_url.png)

    <span data-ttu-id="37c21-157">a.</span><span class="sxs-lookup"><span data-stu-id="37c21-157">a.</span></span> <span data-ttu-id="37c21-158">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`urn:auth0:pantheon:<orgname>-SSO`</span><span class="sxs-lookup"><span data-stu-id="37c21-158">In hello **Identifier** textbox, type a URL using hello following pattern: `urn:auth0:pantheon:<orgname>-SSO`</span></span>

    <span data-ttu-id="37c21-159">b.</span><span class="sxs-lookup"><span data-stu-id="37c21-159">b.</span></span> <span data-ttu-id="37c21-160">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://pantheon.auth0.com/login/callback?connection=<orgname>-SSO`</span><span class="sxs-lookup"><span data-stu-id="37c21-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://pantheon.auth0.com/login/callback?connection=<orgname>-SSO`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="37c21-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="37c21-161">These values are not real.</span></span> <span data-ttu-id="37c21-162">Bu değerleri hello gerçek tanımlayıcısı ve yanıt URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="37c21-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="37c21-163">Kişi [Pantheon destek ekibi](https://pantheon.io/docs/getting-support/) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="37c21-163">Contact [Pantheon support team](https://pantheon.io/docs/getting-support/) tooget these values.</span></span>

4. <span data-ttu-id="37c21-164">Pantheon uygulama, tooset hello UserIdentifier öznitelik değeri hello kullanıcının e-posta adresiyle gerektiren belirli biçiminde hello SAML onayı bekler.</span><span class="sxs-lookup"><span data-stu-id="37c21-164">Pantheon application expects hello SAML assertion in specific format, which requires you tooset hello UserIdentifier attribute value with hello user’s email address.</span></span> <span data-ttu-id="37c21-165">Varsayılan olarak Azure AD hello UserPrincipalName UserIdentifier özniteliği için kullanır.</span><span class="sxs-lookup"><span data-stu-id="37c21-165">By default Azure AD uses hello UserPrincipalName for UserIdentifier attribute.</span></span> <span data-ttu-id="37c21-166">Ancak başarılı tümleştirme için kullanıcının e-posta adresi ile bu değeri toomatch tooadjust gerekir.</span><span class="sxs-lookup"><span data-stu-id="37c21-166">But for successful integration you need tooadjust this value toomatch with user’s email address.</span></span> <span data-ttu-id="37c21-167">Merhaba tümleştirme yalnızca hello doğru eşleme yaptıktan sonra çalışır.</span><span class="sxs-lookup"><span data-stu-id="37c21-167">hello integration will only work after doing hello correct mapping.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-pantheon-tutorial/tutorial_attribute.png)  


5. <span data-ttu-id="37c21-169">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="37c21-169">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_certificate.png)

6. <span data-ttu-id="37c21-171">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="37c21-171">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-pantheon-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="37c21-173">Merhaba üzerinde **Pantheon yapılandırma** 'yi tıklatın **yapılandırma Pantheon** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="37c21-173">On hello **Pantheon Configuration** section, click **Configure Pantheon** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="37c21-174">Kopya hello **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="37c21-174">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_configure.png) 

8. <span data-ttu-id="37c21-176">tooconfigure çoklu oturum açma üzerinde **Pantheon** yan, indirilen toosend hello ihtiyacınız **sertifika** ve **SAML çoklu oturum açma hizmet URL'si** çok[Pantheon Takım Destek](https://pantheon.io/docs/getting-support/).</span><span class="sxs-lookup"><span data-stu-id="37c21-176">tooconfigure single sign-on on **Pantheon** side, you need toosend hello downloaded **Certificate** and **SAML Single Sign-On Service URL** too[Pantheon support team](https://pantheon.io/docs/getting-support/).</span></span>

     > [!Note]
     > <span data-ttu-id="37c21-177">Bu bağlantı tooenable istediğinizde tooprovide hello e-posta etki alanlarındaki bilgileri ve tarih saat de gerekir.</span><span class="sxs-lookup"><span data-stu-id="37c21-177">You also need tooprovide hello Email Domain(s) information and Date Time when you want tooenable this connection.</span></span> <span data-ttu-id="37c21-178">Buradan hakkında daha fazla ayrıntı bulabilirsiniz [burada](https://pantheon.io/docs/sso-organizations/)</span><span class="sxs-lookup"><span data-stu-id="37c21-178">You can find more details about it from [here](https://pantheon.io/docs/sso-organizations/)</span></span>

> [!TIP]
> <span data-ttu-id="37c21-179">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="37c21-179">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="37c21-180">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="37c21-180">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="37c21-181">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="37c21-181">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="37c21-182">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="37c21-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="37c21-183">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="37c21-183">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="37c21-185">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="37c21-185">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="37c21-186">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="37c21-186">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-pantheon-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="37c21-188">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="37c21-188">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-pantheon-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="37c21-190">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="37c21-190">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-pantheon-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="37c21-192">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="37c21-192">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-pantheon-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="37c21-194">a.</span><span class="sxs-lookup"><span data-stu-id="37c21-194">a.</span></span> <span data-ttu-id="37c21-195">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="37c21-195">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="37c21-196">b.</span><span class="sxs-lookup"><span data-stu-id="37c21-196">b.</span></span> <span data-ttu-id="37c21-197">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="37c21-197">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="37c21-198">c.</span><span class="sxs-lookup"><span data-stu-id="37c21-198">c.</span></span> <span data-ttu-id="37c21-199">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="37c21-199">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="37c21-200">d.</span><span class="sxs-lookup"><span data-stu-id="37c21-200">d.</span></span> <span data-ttu-id="37c21-201">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="37c21-201">Click **Create**.</span></span>
 
### <a name="creating-a-pantheon-test-user"></a><span data-ttu-id="37c21-202">Pantheon test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="37c21-202">Creating a Pantheon test user</span></span>

<span data-ttu-id="37c21-203">Bu bölümde, Pantheon içinde Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="37c21-203">In this section, you create a user called Britta Simon in Pantheon.</span></span> <span data-ttu-id="37c21-204">Lütfen başlangıç adımları tooadd hello kullanıcı Pantheon aşağıda izleyin.</span><span class="sxs-lookup"><span data-stu-id="37c21-204">Please follow hello below steps tooadd hello user in Pantheon.</span></span> 

>[!NOTE] 
><span data-ttu-id="37c21-205">SSO için ilk Pantheon oluşturulan toobe toowork kullanıcı gerekir.</span><span class="sxs-lookup"><span data-stu-id="37c21-205">For SSO toowork user needs toobe created first in Pantheon.</span></span>

1. <span data-ttu-id="37c21-206">Yönetici kimlik bilgileriyle oturum açma tooPantheon.</span><span class="sxs-lookup"><span data-stu-id="37c21-206">Login tooPantheon with admin credentials.</span></span>

2. <span data-ttu-id="37c21-207">Çok gidin**kuruluş** Pano sayfası.</span><span class="sxs-lookup"><span data-stu-id="37c21-207">Navigate too**Organization** dashboard page.</span></span>
 
3. <span data-ttu-id="37c21-208">Tıklatın **kişiler**.</span><span class="sxs-lookup"><span data-stu-id="37c21-208">Click **People**.</span></span>

4. <span data-ttu-id="37c21-209">Tıklatın **Kullanıcı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="37c21-209">Click **Add user**.</span></span>

5. <span data-ttu-id="37c21-210">Merhaba kullanıcının e-posta adresi girin.</span><span class="sxs-lookup"><span data-stu-id="37c21-210">Enter hello user's email address.</span></span>

6. <span data-ttu-id="37c21-211">Merhaba kullanıcı rolü seçin.</span><span class="sxs-lookup"><span data-stu-id="37c21-211">Choose hello user's role.</span></span>

7. <span data-ttu-id="37c21-212">Tıklatın **Kullanıcı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="37c21-212">Click **Add user**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="37c21-213">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="37c21-213">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="37c21-214">Bu bölümde, erişim tooPantheon vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="37c21-214">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPantheon.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="37c21-216">**tooassign Britta Simon tooPantheon hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="37c21-216">**tooassign Britta Simon tooPantheon, perform hello following steps:**</span></span>

1. <span data-ttu-id="37c21-217">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="37c21-217">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="37c21-219">Merhaba uygulamalar listesinde **Pantheon**.</span><span class="sxs-lookup"><span data-stu-id="37c21-219">In hello applications list, select **Pantheon**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_app.png) 

3. <span data-ttu-id="37c21-221">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="37c21-221">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="37c21-223">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="37c21-223">Click **Add** button.</span></span> <span data-ttu-id="37c21-224">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="37c21-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="37c21-226">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="37c21-226">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="37c21-227">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="37c21-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="37c21-228">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="37c21-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="37c21-229">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="37c21-229">Testing single sign-on</span></span>

<span data-ttu-id="37c21-230">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="37c21-230">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="37c21-231">Merhaba Pantheon hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Pantheon uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="37c21-231">When you click hello Pantheon tile in hello Access Panel, you should get automatically signed-on tooyour Pantheon application.</span></span>
<span data-ttu-id="37c21-232">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="37c21-232">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="37c21-233">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="37c21-233">Additional resources</span></span>

* [<span data-ttu-id="37c21-234">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="37c21-234">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="37c21-235">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="37c21-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_203.png

