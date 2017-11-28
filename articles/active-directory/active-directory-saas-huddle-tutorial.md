---
title: "Öğretici: Azure Active Directory Tümleştirme ile Huddle | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Huddle arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8389ba4c-f5f8-4ede-b2f4-32eae844ceb0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 0b2f6c4d839943cdd07699a1ff95dc8f90505699
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-huddle"></a><span data-ttu-id="9bfa2-103">Öğretici: Azure Active Directory Tümleştirme Huddle ile</span><span class="sxs-lookup"><span data-stu-id="9bfa2-103">Tutorial: Azure Active Directory integration with Huddle</span></span>

<span data-ttu-id="9bfa2-104">Bu öğreticide, bilgi nasıl toointegrate Huddle Azure Active Directory (Azure AD) ile.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-104">In this tutorial, you learn how toointegrate Huddle with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9bfa2-105">Huddle Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="9bfa2-105">Integrating Huddle with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9bfa2-106">Erişim tooHuddle sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="9bfa2-106">You can control in Azure AD who has access tooHuddle</span></span>
- <span data-ttu-id="9bfa2-107">Kullanıcıların tooautomatically get açan tooHuddle (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="9bfa2-107">You can enable your users tooautomatically get signed-on tooHuddle (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9bfa2-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="9bfa2-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="9bfa2-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9bfa2-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9bfa2-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="9bfa2-110">Prerequisites</span></span>

<span data-ttu-id="9bfa2-111">Huddle ile tooconfigure Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="9bfa2-111">tooconfigure Azure AD integration with Huddle, you need hello following items:</span></span>

- <span data-ttu-id="9bfa2-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="9bfa2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9bfa2-113">Bir Huddle çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="9bfa2-113">A Huddle single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9bfa2-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9bfa2-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="9bfa2-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9bfa2-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9bfa2-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9bfa2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9bfa2-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="9bfa2-118">Scenario description</span></span>

<span data-ttu-id="9bfa2-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9bfa2-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="9bfa2-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9bfa2-121">Merhaba Galerisi'nden Huddle ekleme</span><span class="sxs-lookup"><span data-stu-id="9bfa2-121">Adding Huddle from hello gallery</span></span>
2. <span data-ttu-id="9bfa2-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="9bfa2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-huddle-from-hello-gallery"></a><span data-ttu-id="9bfa2-123">Merhaba Galerisi'nden Huddle ekleme</span><span class="sxs-lookup"><span data-stu-id="9bfa2-123">Adding Huddle from hello gallery</span></span>
<span data-ttu-id="9bfa2-124">Azure AD'ye Huddle tooconfigure hello tümleştirilmesi, tooadd Huddle hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-124">tooconfigure hello integration of Huddle into Azure AD, you need tooadd Huddle from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9bfa2-125">**tooadd Huddle hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="9bfa2-125">**tooadd Huddle from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9bfa2-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9bfa2-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9bfa2-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="9bfa2-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="9bfa2-133">Merhaba arama kutusuna yazın **Huddle**.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-133">In hello search box, type **Huddle**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_search.png)

5. <span data-ttu-id="9bfa2-135">Merhaba Sonuçlar panelinde seçin **Huddle**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-135">In hello results panel, select **Huddle**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9bfa2-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="9bfa2-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="9bfa2-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Huddle ile test etme</span><span class="sxs-lookup"><span data-stu-id="9bfa2-138">In this section, you configure and test Azure AD single sign-on with Huddle based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9bfa2-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Huddle içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Huddle is tooa user in Azure AD.</span></span> <span data-ttu-id="9bfa2-140">Diğer bir deyişle, bir bağlantı bir Azure AD kullanıcı ve kullanıcı arasındaki ilişki hello ilgili kurulan Huddle gereksinimlerini toobe içinde.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-140">In other words, a link relationship between an Azure AD user and hello related user in Huddle needs toobe established.</span></span>

<span data-ttu-id="9bfa2-141">Merhaba hello değeri Huddle içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-141">In Huddle, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="9bfa2-142">tooconfigure ve Huddle ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="9bfa2-142">tooconfigure and test Azure AD single sign-on with Huddle, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9bfa2-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>

2. <span data-ttu-id="9bfa2-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>

3. <span data-ttu-id="9bfa2-145">**[Huddle test kullanıcısı oluşturma](#creating-a-huddle-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Huddle içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-145">**[Creating a Huddle test user](#creating-a-huddle-test-user)** - toohave a counterpart of Britta Simon in Huddle that is linked toohello Azure AD representation of user.</span></span>

4. <span data-ttu-id="9bfa2-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>

5. <span data-ttu-id="9bfa2-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9bfa2-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="9bfa2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9bfa2-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Huddle uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Huddle application.</span></span>

<span data-ttu-id="9bfa2-150">**Azure AD çoklu oturum açma tooconfigure Huddle ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="9bfa2-150">**tooconfigure Azure AD single sign-on with Huddle, perform hello following steps:**</span></span>

1. <span data-ttu-id="9bfa2-151">Hello hello üzerinde Azure portal'ın **Huddle** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-151">In hello Azure portal, on hello **Huddle** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="9bfa2-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_samlbase.png)

3. <span data-ttu-id="9bfa2-155">Merhaba üzerinde **Huddle etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="9bfa2-155">On hello **Huddle Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_url.png)

    <span data-ttu-id="9bfa2-157">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`http://<company name>.huddle.com`</span><span class="sxs-lookup"><span data-stu-id="9bfa2-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `http://<company name>.huddle.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9bfa2-158">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-158">This value is not real.</span></span> <span data-ttu-id="9bfa2-159">Bu değer ile Merhaba güncelleştirme gerçek oturum açma URL'si.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="9bfa2-160">Kişi [Huddle istemci destek ekibi](https://huddle.zendesk.com) tooget bu değer.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-160">Contact [Huddle Client support team](https://huddle.zendesk.com) tooget this value.</span></span> 

4. <span data-ttu-id="9bfa2-161">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_certificate.png) 

5. <span data-ttu-id="9bfa2-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-huddle-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9bfa2-165">Merhaba üzerinde **Huddle yapılandırma** 'yi tıklatın **yapılandırma Huddle** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-165">On hello **Huddle Configuration** section, click **Configure Huddle** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="9bfa2-166">Kopya hello **SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="9bfa2-166">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span> 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_configure.png) 
    
7. <span data-ttu-id="9bfa2-168">tooconfigure çoklu oturum açma Huddle tarafında, indirilen toosend hello ihtiyacınız **sertifika**, **SAML çoklu oturum açma hizmet URL'si**, ve **SAML varlık kimliği** çok[Huddle istemci destek ekibi](https://huddle.zendesk.com).</span><span class="sxs-lookup"><span data-stu-id="9bfa2-168">tooconfigure single sign-on on Huddle side, you need toosend hello downloaded  **Certificate**, **SAML Single Sign-On Service URL**, and **SAML Entity ID** too[Huddle Client support team](https://huddle.zendesk.com).</span></span> <span data-ttu-id="9bfa2-169">Bunlar, bu ayar toohave hello iki tarafta da ayarlamanızı SAML SSO bağlantı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-169">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>  
   
    >[!NOTE]
    > <span data-ttu-id="9bfa2-170">Çoklu oturum açma hello Huddle destek ekibi tarafından etkin toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-170">Single sign-on needs toobe enabled by hello Huddle support team.</span></span> <span data-ttu-id="9bfa2-171">Merhaba Yapılandırma tamamlandığında, bir bildirim alırsınız.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-171">You get a notification when hello configuration has been completed.</span></span> 
    > 

> [!TIP]
> <span data-ttu-id="9bfa2-172">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="9bfa2-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9bfa2-173">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9bfa2-174">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9bfa2-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 
   
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9bfa2-175">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="9bfa2-175">Creating an Azure AD test user</span></span>

<span data-ttu-id="9bfa2-176">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="9bfa2-178">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="9bfa2-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9bfa2-179">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-huddle-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9bfa2-181">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-huddle-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9bfa2-183">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-huddle-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9bfa2-185">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="9bfa2-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-huddle-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9bfa2-187">a.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-187">a.</span></span> <span data-ttu-id="9bfa2-188">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9bfa2-189">b.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-189">b.</span></span> <span data-ttu-id="9bfa2-190">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9bfa2-191">c.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-191">c.</span></span> <span data-ttu-id="9bfa2-192">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9bfa2-193">d.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-193">d.</span></span> <span data-ttu-id="9bfa2-194">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-194">Click **Create**.</span></span>
 
### <a name="creating-a-huddle-test-user"></a><span data-ttu-id="9bfa2-195">Huddle test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="9bfa2-195">Creating a Huddle test user</span></span>

<span data-ttu-id="9bfa2-196">tooenable Azure AD kullanıcıların toolog tooHuddle bunların Huddle sağlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-196">tooenable Azure AD users toolog in tooHuddle, they must be provisioned into Huddle.</span></span> <span data-ttu-id="9bfa2-197">Huddle Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-197">In hello case of Huddle, provisioning is a manual task.</span></span>

<span data-ttu-id="9bfa2-198">**tooconfigure kullanıcı hazırlama, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="9bfa2-198">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="9bfa2-199">İçinde tooyour oturum **Huddle** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-199">Log in tooyour **Huddle** company site as administrator.</span></span>
2. <span data-ttu-id="9bfa2-200">Tıklatın **çalışma**.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-200">Click **Workspace**.</span></span>
3. <span data-ttu-id="9bfa2-201">Tıklatın **kişiler \> kişileri davet edin**.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-201">Click **People \> Invite People**.</span></span>
   
   <span data-ttu-id="9bfa2-202">![Kişiler](./media/active-directory-saas-huddle-tutorial/IC787838.png "kişiler")</span><span class="sxs-lookup"><span data-stu-id="9bfa2-202">![People](./media/active-directory-saas-huddle-tutorial/IC787838.png "People")</span></span>

4. <span data-ttu-id="9bfa2-203">Merhaba, **yeni bir davet oluşturma** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="9bfa2-203">In hello **Create a new invitation** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="9bfa2-204">![Yeni davet](./media/active-directory-saas-huddle-tutorial/IC787839.png "yeni davet")</span><span class="sxs-lookup"><span data-stu-id="9bfa2-204">![New Invitation](./media/active-directory-saas-huddle-tutorial/IC787839.png "New Invitation")</span></span>
   
   <span data-ttu-id="9bfa2-205">a.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-205">a.</span></span> <span data-ttu-id="9bfa2-206">Merhaba, **Seç takım tooinvite kişiler toojoin** listesinde **takım**.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-206">In hello **Choose a team tooinvite people toojoin** list, select **team**.</span></span>

   <span data-ttu-id="9bfa2-207">b.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-207">b.</span></span> <span data-ttu-id="9bfa2-208">Türü hello **e-posta adresi** geçerli bir Azure AD hesabı tooprovision çok istediğiniz**Enter e-posta adresi tooinvite istediğiniz kişiler için** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-208">Type hello **Email Address** of a valid Azure AD account you want tooprovision in too**Enter email address for people you'd like tooinvite** textbox.</span></span>

   <span data-ttu-id="9bfa2-209">c.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-209">c.</span></span> <span data-ttu-id="9bfa2-210">Tıklatın **davet**.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-210">Click **Invite**.</span></span>   
   
    >[!NOTE]
    > <span data-ttu-id="9bfa2-211">Hello Azure AD hesabının sahibi etkin hale önce bir bağlantı tooconfirm hello hesabı da dahil olmak üzere bir e-posta alacaksınız.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-211">hello Azure AD account holder will receive an email including a link tooconfirm hello account before it becomes active.</span></span> 
    > 

>[!NOTE]
><span data-ttu-id="9bfa2-212">API'leri, Azure AD kullanıcı hesapları Huddle tooprovision tarafından sağlanan veya herhangi diğer Huddle kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-212">You can use any other Huddle user account creation tools or APIs provided by Huddle tooprovision Azure AD user accounts.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="9bfa2-213">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="9bfa2-213">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="9bfa2-214">Bu bölümde, erişim tooHuddle vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-214">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHuddle.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="9bfa2-216">**tooassign Britta Simon tooHuddle hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="9bfa2-216">**tooassign Britta Simon tooHuddle, perform hello following steps:**</span></span>

1. <span data-ttu-id="9bfa2-217">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-217">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="9bfa2-219">Merhaba uygulamalar listesinde **Huddle**.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-219">In hello applications list, select **Huddle**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_app.png) 

3. <span data-ttu-id="9bfa2-221">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-221">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="9bfa2-223">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-223">Click **Add** button.</span></span> <span data-ttu-id="9bfa2-224">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="9bfa2-226">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-226">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9bfa2-227">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9bfa2-228">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9bfa2-229">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="9bfa2-229">Testing single sign-on</span></span>

<span data-ttu-id="9bfa2-230">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-230">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="9bfa2-231">Merhaba Huddle hello erişim paneli parçasında tıkladığınızda, oturum açma sayfasına Huddle uygulamasının otomatik olarak almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9bfa2-231">When you click hello Huddle tile in hello Access Panel, you should get automatically login page of Huddle application.</span></span>
<span data-ttu-id="9bfa2-232">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9bfa2-232">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9bfa2-233">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="9bfa2-233">Additional resources</span></span>

* [<span data-ttu-id="9bfa2-234">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="9bfa2-234">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9bfa2-235">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="9bfa2-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_04.png
[100]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_100.png
[200]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_203.png
