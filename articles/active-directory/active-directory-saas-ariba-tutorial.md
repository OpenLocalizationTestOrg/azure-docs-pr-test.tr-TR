---
title: "Öğretici: Azure Active Directory Tümleştirme ile aralarında Ariba | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile aralarında Ariba arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 45a8364c-55d1-4dc7-b079-9eb2a701842d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/02/2017
ms.author: jeedes
ms.openlocfilehash: a1b17129c1298b59c155a0890e41e41ff9544a24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ariba"></a><span data-ttu-id="8a1ff-103">Öğretici: Azure Active Directory Tümleştirme biçimi Ariba ile</span><span class="sxs-lookup"><span data-stu-id="8a1ff-103">Tutorial: Azure Active Directory integration with Ariba</span></span>

<span data-ttu-id="8a1ff-104">Bu öğreticide, bilgi nasıl toointegrate biçimi Ariba Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8a1ff-104">In this tutorial, you learn how toointegrate Ariba with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8a1ff-105">Aralarında Ariba Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="8a1ff-105">Integrating Ariba with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8a1ff-106">Erişim tooAriba sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="8a1ff-106">You can control in Azure AD who has access tooAriba</span></span>
- <span data-ttu-id="8a1ff-107">Kullanıcıların tooautomatically get açan tooAriba (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="8a1ff-107">You can enable your users tooautomatically get signed-on tooAriba (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8a1ff-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="8a1ff-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8a1ff-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8a1ff-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8a1ff-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="8a1ff-110">Prerequisites</span></span>

<span data-ttu-id="8a1ff-111">tooconfigure biçimi Ariba ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="8a1ff-111">tooconfigure Azure AD integration with Ariba, you need hello following items:</span></span>

- <span data-ttu-id="8a1ff-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="8a1ff-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8a1ff-113">Bir biçimi Ariba çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="8a1ff-113">An Ariba single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8a1ff-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="8a1ff-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8a1ff-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="8a1ff-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8a1ff-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="8a1ff-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8a1ff-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8a1ff-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8a1ff-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="8a1ff-118">Scenario description</span></span>
<span data-ttu-id="8a1ff-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="8a1ff-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8a1ff-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="8a1ff-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8a1ff-121">Merhaba Galerisi'nden biçimi Ariba ekleme</span><span class="sxs-lookup"><span data-stu-id="8a1ff-121">Adding Ariba from hello gallery</span></span>
2. <span data-ttu-id="8a1ff-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="8a1ff-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ariba-from-hello-gallery"></a><span data-ttu-id="8a1ff-123">Merhaba Galerisi'nden biçimi Ariba ekleme</span><span class="sxs-lookup"><span data-stu-id="8a1ff-123">Adding Ariba from hello gallery</span></span>
<span data-ttu-id="8a1ff-124">Azure AD'ye tooconfigure hello tümleştirme biçimi Ariba, tooadd biçimi Ariba hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="8a1ff-124">tooconfigure hello integration of Ariba into Azure AD, you need tooadd Ariba from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8a1ff-125">**tooadd biçimi Ariba hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="8a1ff-125">**tooadd Ariba from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8a1ff-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="8a1ff-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8a1ff-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="8a1ff-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8a1ff-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="8a1ff-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="8a1ff-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="8a1ff-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="8a1ff-133">Merhaba arama kutusuna yazın **biçimi Ariba**.</span><span class="sxs-lookup"><span data-stu-id="8a1ff-133">In hello search box, type **Ariba**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_search.png)

5. <span data-ttu-id="8a1ff-135">Merhaba Sonuçlar panelinde seçin **biçimi Ariba**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="8a1ff-135">In hello results panel, select **Ariba**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8a1ff-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="8a1ff-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8a1ff-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı biçimi Ariba ile test etme</span><span class="sxs-lookup"><span data-stu-id="8a1ff-138">In this section, you configure and test Azure AD single sign-on with Ariba based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8a1ff-139">Tek toowork'ın oturum açma hangi hello karşılık gelen biçimi Ariba içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="8a1ff-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Ariba is tooa user in Azure AD.</span></span> <span data-ttu-id="8a1ff-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı biçimi Ariba hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="8a1ff-140">In other words, a link relationship between an Azure AD user and hello related user in Ariba needs toobe established.</span></span>

<span data-ttu-id="8a1ff-141">Aralarında Ariba içinde hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="8a1ff-141">In Ariba, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8a1ff-142">tooconfigure ve Azure AD çoklu oturum açma biçimi Ariba ile test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="8a1ff-142">tooconfigure and test Azure AD single sign-on with Ariba, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8a1ff-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="8a1ff-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8a1ff-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="8a1ff-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8a1ff-145">**[Aralarında Ariba test kullanıcısı oluşturma](#creating-an-ariba-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir biçimi Ariba içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="8a1ff-145">**[Creating an Ariba test user](#creating-an-ariba-test-user)** - toohave a counterpart of Britta Simon in Ariba that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8a1ff-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="8a1ff-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8a1ff-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="8a1ff-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8a1ff-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="8a1ff-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8a1ff-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma biçimi Ariba uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="8a1ff-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Ariba application.</span></span>

<span data-ttu-id="8a1ff-150">**tooconfigure Azure AD çoklu oturum açma ile aralarında Ariba, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="8a1ff-150">**tooconfigure Azure AD single sign-on with Ariba, perform hello following steps:**</span></span>

1. <span data-ttu-id="8a1ff-151">Merhaba hello üzerinde Azure portal'ın **biçimi Ariba** uygulama tümleştirmesi sayfasında, tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="8a1ff-151">In hello Azure portal, on hello **Ariba** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="8a1ff-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="8a1ff-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_samlbase.png)

3. <span data-ttu-id="8a1ff-155">Merhaba üzerinde **biçimi Ariba etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="8a1ff-155">On hello **Ariba Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_url.png)

    <span data-ttu-id="8a1ff-157">a.</span><span class="sxs-lookup"><span data-stu-id="8a1ff-157">a.</span></span> <span data-ttu-id="8a1ff-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın: `https://<subdomain>.sourcing.ariba.com` veya`https://<subdomain>.supplier.ariba.com`</span><span class="sxs-lookup"><span data-stu-id="8a1ff-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.sourcing.ariba.com` or `https://<subdomain>.supplier.ariba.com`</span></span>

    <span data-ttu-id="8a1ff-159">b.</span><span class="sxs-lookup"><span data-stu-id="8a1ff-159">b.</span></span> <span data-ttu-id="8a1ff-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`http://<subdomain>.procurement-2.ariba.com`</span><span class="sxs-lookup"><span data-stu-id="8a1ff-160">In hello **Identifier** textbox, type a URL using hello following pattern: `http://<subdomain>.procurement-2.ariba.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8a1ff-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="8a1ff-161">These values are not real.</span></span> <span data-ttu-id="8a1ff-162">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="8a1ff-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="8a1ff-163">Burada, toouse hello benzersiz değerini hello tanımlayıcı dizesinde öneririz.</span><span class="sxs-lookup"><span data-stu-id="8a1ff-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="8a1ff-164">Aralarında Ariba istemci destek ekibi ile iletişime geçin **1-866-218-2155** tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="8a1ff-164">Contact Ariba Client support team at **1-866-218-2155** tooget these values.</span></span> 
 

4. <span data-ttu-id="8a1ff-165">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="8a1ff-165">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate  file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_certificate.png) 

5. <span data-ttu-id="8a1ff-167">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="8a1ff-167">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ariba-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8a1ff-169">tooget SSO yapılandırıldığında, uygulamanız için aralarında Ariba destek ekibi çağırmak **1-866-218-2155** ve bunlar, daha fazla nasıl bunları hello tooprovide indirilen üzerinde yardımcı **sertifika (Base64)** dosyası.</span><span class="sxs-lookup"><span data-stu-id="8a1ff-169">tooget SSO configured for your application, call Ariba support team on **1-866-218-2155** and they'll assist you further on how tooprovide them hello downloaded **Certificate (Base64)** file.</span></span>  
 
> [!TIP]
> <span data-ttu-id="8a1ff-170">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="8a1ff-170">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8a1ff-171">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="8a1ff-171">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8a1ff-172">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8a1ff-172">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8a1ff-173">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="8a1ff-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="8a1ff-174">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="8a1ff-174">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="8a1ff-176">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="8a1ff-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8a1ff-177">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="8a1ff-177">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-ariba-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8a1ff-179">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="8a1ff-179">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-ariba-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8a1ff-181">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="8a1ff-181">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-ariba-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8a1ff-183">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="8a1ff-183">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-ariba-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8a1ff-185">a.</span><span class="sxs-lookup"><span data-stu-id="8a1ff-185">a.</span></span> <span data-ttu-id="8a1ff-186">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8a1ff-186">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8a1ff-187">b.</span><span class="sxs-lookup"><span data-stu-id="8a1ff-187">b.</span></span> <span data-ttu-id="8a1ff-188">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="8a1ff-188">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8a1ff-189">c.</span><span class="sxs-lookup"><span data-stu-id="8a1ff-189">c.</span></span> <span data-ttu-id="8a1ff-190">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="8a1ff-190">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8a1ff-191">d.</span><span class="sxs-lookup"><span data-stu-id="8a1ff-191">d.</span></span> <span data-ttu-id="8a1ff-192">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8a1ff-192">Click **Create**.</span></span>
 
### <a name="creating-an-ariba-test-user"></a><span data-ttu-id="8a1ff-193">Aralarında Ariba test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="8a1ff-193">Creating an Ariba test user</span></span>

<span data-ttu-id="8a1ff-194">Bu bölümde Hello amacı toocreate biçimi Ariba içinde Britta Simon adlı bir kullanıcı ' dir.</span><span class="sxs-lookup"><span data-stu-id="8a1ff-194">hello objective of this section is toocreate a user called Britta Simon in Ariba.</span></span> <span data-ttu-id="8a1ff-195">Çalışma biçimi Ariba destek ekibi ile **1-866-218-2155** hello biçimi Ariba sistem tooadd hello kullanıcılar.</span><span class="sxs-lookup"><span data-stu-id="8a1ff-195">Work with Ariba support team at **1-866-218-2155** tooadd hello users in hello Ariba system.</span></span> 

 >[!NOTE]
 ><span data-ttu-id="8a1ff-196">Bir kullanıcı toocreate el ile yapmanız gerekir, toocontact hello biçimi Ariba destek ekibi gerekir **1-866-218-2155**.</span><span class="sxs-lookup"><span data-stu-id="8a1ff-196">If you need toocreate a user manually, you need toocontact hello Ariba support team at **1-866-218-2155**.</span></span>
 >  

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8a1ff-197">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="8a1ff-197">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8a1ff-198">Bu bölümde, erişim tooAriba vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="8a1ff-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAriba.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="8a1ff-200">**tooassign Britta Simon tooAriba hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="8a1ff-200">**tooassign Britta Simon tooAriba, perform hello following steps:**</span></span>

1. <span data-ttu-id="8a1ff-201">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="8a1ff-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="8a1ff-203">Merhaba uygulamalar listesinde **biçimi Ariba**.</span><span class="sxs-lookup"><span data-stu-id="8a1ff-203">In hello applications list, select **Ariba**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_app.png) 

3. <span data-ttu-id="8a1ff-205">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="8a1ff-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="8a1ff-207">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="8a1ff-207">Click **Add** button.</span></span> <span data-ttu-id="8a1ff-208">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="8a1ff-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="8a1ff-210">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="8a1ff-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8a1ff-211">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="8a1ff-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8a1ff-212">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="8a1ff-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8a1ff-213">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="8a1ff-213">Testing single sign-on</span></span>
<span data-ttu-id="8a1ff-214">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD SSO yapılandırmayı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="8a1ff-214">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="8a1ff-215">Merhaba biçimi Ariba hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour biçimi Ariba uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8a1ff-215">When you click hello Ariba tile in hello Access Panel, you should get automatically signed-on tooyour Ariba application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="8a1ff-216">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="8a1ff-216">Additional resources</span></span>

* [<span data-ttu-id="8a1ff-217">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="8a1ff-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8a1ff-218">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="8a1ff-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_203.png

