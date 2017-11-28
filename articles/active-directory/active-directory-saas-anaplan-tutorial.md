---
title: "Öğretici: Azure Active Directory Tümleştirme ile Anaplan | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Anaplan arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4a9c2914-6c8c-4a88-93e3-3753afb40e6b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jeedes
ms.openlocfilehash: 38eb210d090e7aa720060680259124e941e30541
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-anaplan"></a><span data-ttu-id="77452-103">Öğretici: Azure Active Directory Tümleştirme Anaplan ile</span><span class="sxs-lookup"><span data-stu-id="77452-103">Tutorial: Azure Active Directory integration with Anaplan</span></span>

<span data-ttu-id="77452-104">Bu öğreticide, bilgi nasıl toointegrate Anaplan Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="77452-104">In this tutorial, you learn how toointegrate Anaplan with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="77452-105">Anaplan Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="77452-105">Integrating Anaplan with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="77452-106">Erişim tooAnaplan sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="77452-106">You can control in Azure AD who has access tooAnaplan</span></span>
- <span data-ttu-id="77452-107">Kullanıcıların tooautomatically get açan tooAnaplan (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="77452-107">You can enable your users tooautomatically get signed-on tooAnaplan (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="77452-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="77452-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="77452-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="77452-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="77452-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="77452-110">Prerequisites</span></span>

<span data-ttu-id="77452-111">tooconfigure Anaplan ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="77452-111">tooconfigure Azure AD integration with Anaplan, you need hello following items:</span></span>

- <span data-ttu-id="77452-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="77452-112">An Azure AD subscription</span></span>
- <span data-ttu-id="77452-113">Bir Anaplan çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="77452-113">An Anaplan single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="77452-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="77452-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="77452-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="77452-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="77452-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="77452-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="77452-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="77452-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="77452-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="77452-118">Scenario description</span></span>
<span data-ttu-id="77452-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="77452-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="77452-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="77452-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="77452-121">Merhaba Galerisi'nden Anaplan ekleme</span><span class="sxs-lookup"><span data-stu-id="77452-121">Adding Anaplan from hello gallery</span></span>
2. <span data-ttu-id="77452-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="77452-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-anaplan-from-hello-gallery"></a><span data-ttu-id="77452-123">Merhaba Galerisi'nden Anaplan ekleme</span><span class="sxs-lookup"><span data-stu-id="77452-123">Adding Anaplan from hello gallery</span></span>
<span data-ttu-id="77452-124">Azure AD'ye tooconfigure hello tümleştirme Anaplan, tooadd Anaplan hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="77452-124">tooconfigure hello integration of Anaplan into Azure AD, you need tooadd Anaplan from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="77452-125">**tooadd Anaplan hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="77452-125">**tooadd Anaplan from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="77452-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="77452-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="77452-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="77452-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="77452-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="77452-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="77452-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="77452-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="77452-133">Merhaba arama kutusuna yazın **Anaplan**.</span><span class="sxs-lookup"><span data-stu-id="77452-133">In hello search box, type **Anaplan**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-anaplan-tutorial/tutorial_anaplan_search.png)

5. <span data-ttu-id="77452-135">Merhaba Sonuçlar panelinde seçin **Anaplan**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="77452-135">In hello results panel, select **Anaplan**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-anaplan-tutorial/tutorial_anaplan_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="77452-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="77452-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="77452-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Anaplan ile test etme</span><span class="sxs-lookup"><span data-stu-id="77452-138">In this section, you configure and test Azure AD single sign-on with Anaplan based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="77452-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Anaplan içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="77452-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Anaplan is tooa user in Azure AD.</span></span> <span data-ttu-id="77452-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Anaplan hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="77452-140">In other words, a link relationship between an Azure AD user and hello related user in Anaplan needs toobe established.</span></span>

<span data-ttu-id="77452-141">Merhaba hello değeri Anaplan içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="77452-141">In Anaplan, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="77452-142">tooconfigure ve Anaplan ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="77452-142">tooconfigure and test Azure AD single sign-on with Anaplan, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="77452-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="77452-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="77452-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="77452-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="77452-145">**[Bir Anaplan test kullanıcısı oluşturma](#creating-an-anaplan-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Anaplan içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="77452-145">**[Creating an Anaplan test user](#creating-an-anaplan-test-user)** - toohave a counterpart of Britta Simon in Anaplan that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="77452-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="77452-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="77452-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="77452-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="77452-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="77452-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="77452-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Anaplan uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="77452-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Anaplan application.</span></span>

<span data-ttu-id="77452-150">**tooconfigure Azure AD çoklu oturum açma ile Anaplan, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="77452-150">**tooconfigure Azure AD single sign-on with Anaplan, perform hello following steps:**</span></span>

1. <span data-ttu-id="77452-151">Hello hello üzerinde Azure portal'ın **Anaplan** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="77452-151">In hello Azure portal, on hello **Anaplan** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="77452-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="77452-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-anaplan-tutorial/tutorial_anaplan_samlbase.png)

3. <span data-ttu-id="77452-155">Merhaba üzerinde **Anaplan etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="77452-155">On hello **Anaplan Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-anaplan-tutorial/tutorial_anaplan_url.png)

    <span data-ttu-id="77452-157">a.</span><span class="sxs-lookup"><span data-stu-id="77452-157">a.</span></span> <span data-ttu-id="77452-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://sdp.anaplan.com/frontdoor/saml/<tenant name>`</span><span class="sxs-lookup"><span data-stu-id="77452-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://sdp.anaplan.com/frontdoor/saml/<tenant name>`</span></span>

    <span data-ttu-id="77452-159">b.</span><span class="sxs-lookup"><span data-stu-id="77452-159">b.</span></span> <span data-ttu-id="77452-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.anaplan.com`</span><span class="sxs-lookup"><span data-stu-id="77452-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.anaplan.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="77452-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="77452-161">These values are not real.</span></span> <span data-ttu-id="77452-162">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="77452-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="77452-163">Kişi [Anaplan istemci destek ekibi](mailto:support@anaplan.com) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="77452-163">Contact [Anaplan Client support team](mailto:support@anaplan.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="77452-164">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="77452-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-anaplan-tutorial/tutorial_anaplan_certificate.png) 

5. <span data-ttu-id="77452-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="77452-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-anaplan-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="77452-168">Merhaba üzerinde **Anaplan yapılandırma** 'yi tıklatın **yapılandırma Anaplan** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="77452-168">On hello **Anaplan Configuration** section, click **Configure Anaplan** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="77452-169">Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="77452-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-anaplan-tutorial/tutorial_anaplan_configure.png) 

7. <span data-ttu-id="77452-171">tooconfigure çoklu oturum açma üzerinde **Anaplan** yan, indirilen toosend hello ihtiyacınız **meta veri XML**, **SAML varlık kimliği**, **SAML çoklu oturum açma hizmet URL'si**  ve **Sign-Out URL** çok[Anaplan destek ekibi](mailto:support@anaplan.com).</span><span class="sxs-lookup"><span data-stu-id="77452-171">tooconfigure single sign-on on **Anaplan** side, you need toosend hello downloaded **Metadata XML**, **SAML Entity ID**, **SAML Single Sign-On Service URL** and **Sign-Out URL**   too[Anaplan support team](mailto:support@anaplan.com).</span></span> <span data-ttu-id="77452-172">Bunlar, bu ayar toohave hello iki tarafta da ayarlamanızı SAML SSO bağlantı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="77452-172">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="77452-173">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="77452-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="77452-174">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="77452-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="77452-175">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="77452-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="77452-176">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="77452-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="77452-177">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="77452-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="77452-179">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="77452-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="77452-180">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="77452-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-anaplan-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="77452-182">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="77452-182">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-anaplan-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="77452-184">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="77452-184">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-anaplan-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="77452-186">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="77452-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-anaplan-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="77452-188">a.</span><span class="sxs-lookup"><span data-stu-id="77452-188">a.</span></span> <span data-ttu-id="77452-189">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="77452-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="77452-190">b.</span><span class="sxs-lookup"><span data-stu-id="77452-190">b.</span></span> <span data-ttu-id="77452-191">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="77452-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="77452-192">c.</span><span class="sxs-lookup"><span data-stu-id="77452-192">c.</span></span> <span data-ttu-id="77452-193">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="77452-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="77452-194">d.</span><span class="sxs-lookup"><span data-stu-id="77452-194">d.</span></span> <span data-ttu-id="77452-195">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="77452-195">Click **Create**.</span></span>
 
### <a name="creating-an-anaplan-test-user"></a><span data-ttu-id="77452-196">Bir Anaplan test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="77452-196">Creating an Anaplan test user</span></span>

<span data-ttu-id="77452-197">Bu bölümde, Anaplan içinde Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="77452-197">In this section, you create a user called Britta Simon in Anaplan.</span></span> <span data-ttu-id="77452-198">Lütfen çalışmak [Anaplan destek ekibi](mailto:support@anaplan.com) tooadd hello kullanıcılar hello Anaplan Platform.</span><span class="sxs-lookup"><span data-stu-id="77452-198">Please work with [Anaplan support team](mailto:support@anaplan.com) tooadd hello users in hello Anaplan platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="77452-199">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="77452-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="77452-200">Bu bölümde, erişim tooAnaplan vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="77452-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAnaplan.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="77452-202">**tooassign Britta Simon tooAnaplan hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="77452-202">**tooassign Britta Simon tooAnaplan, perform hello following steps:**</span></span>

1. <span data-ttu-id="77452-203">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="77452-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="77452-205">Merhaba uygulamalar listesinde **Anaplan**.</span><span class="sxs-lookup"><span data-stu-id="77452-205">In hello applications list, select **Anaplan**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-anaplan-tutorial/tutorial_anaplan_app.png) 

3. <span data-ttu-id="77452-207">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="77452-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="77452-209">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="77452-209">Click **Add** button.</span></span> <span data-ttu-id="77452-210">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="77452-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="77452-212">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="77452-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="77452-213">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="77452-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="77452-214">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="77452-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="77452-215">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="77452-215">Testing single sign-on</span></span>

<span data-ttu-id="77452-216">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="77452-216">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="77452-217">Merhaba Anaplan hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Anaplan uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="77452-217">When you click hello Anaplan tile in hello Access Panel, you should get automatically signed-on tooyour Anaplan application.</span></span>

<span data-ttu-id="77452-218">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="77452-218">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="77452-219">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="77452-219">Additional resources</span></span>

* [<span data-ttu-id="77452-220">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="77452-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="77452-221">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="77452-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_203.png

