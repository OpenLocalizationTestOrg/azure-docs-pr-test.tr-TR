---
title: "Öğretici: Azure Active Directory Tümleştirme ile Kindling | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Kindling arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 71229751-74eb-4c2c-abb4-07caa95754c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 32ad6116c2690aea2060a2dd56e052f233ad7ae3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kindling"></a><span data-ttu-id="8cb35-103">Öğretici: Azure Active Directory Tümleştirme Kindling ile</span><span class="sxs-lookup"><span data-stu-id="8cb35-103">Tutorial: Azure Active Directory integration with Kindling</span></span>

<span data-ttu-id="8cb35-104">Bu öğreticide, bilgi nasıl toointegrate Azure Active Directory (Azure AD) ile Kindling.</span><span class="sxs-lookup"><span data-stu-id="8cb35-104">In this tutorial, you learn how toointegrate Kindling with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8cb35-105">Kindling Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="8cb35-105">Integrating Kindling with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8cb35-106">Erişim tooKindling sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="8cb35-106">You can control in Azure AD who has access tooKindling</span></span>
- <span data-ttu-id="8cb35-107">Kullanıcıların tooautomatically get açan tooKindling (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="8cb35-107">You can enable your users tooautomatically get signed-on tooKindling (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8cb35-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="8cb35-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8cb35-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz.</span><span class="sxs-lookup"><span data-stu-id="8cb35-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="8cb35-110">[uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8cb35-110">[what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8cb35-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="8cb35-111">Prerequisites</span></span>

<span data-ttu-id="8cb35-112">Kindling ile tooconfigure Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="8cb35-112">tooconfigure Azure AD integration with Kindling, you need hello following items:</span></span>

- <span data-ttu-id="8cb35-113">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="8cb35-113">An Azure AD subscription</span></span>
- <span data-ttu-id="8cb35-114">Bir Kindling çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="8cb35-114">A Kindling single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8cb35-115">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="8cb35-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8cb35-116">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="8cb35-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8cb35-117">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="8cb35-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8cb35-118">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8cb35-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8cb35-119">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="8cb35-119">Scenario description</span></span>
<span data-ttu-id="8cb35-120">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="8cb35-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8cb35-121">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="8cb35-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8cb35-122">Merhaba Galerisi'nden Kindling ekleme</span><span class="sxs-lookup"><span data-stu-id="8cb35-122">Adding Kindling from hello gallery</span></span>
2. <span data-ttu-id="8cb35-123">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="8cb35-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kindling-from-hello-gallery"></a><span data-ttu-id="8cb35-124">Merhaba Galerisi'nden Kindling ekleme</span><span class="sxs-lookup"><span data-stu-id="8cb35-124">Adding Kindling from hello gallery</span></span>
<span data-ttu-id="8cb35-125">Azure AD'ye Kindling tooconfigure hello tümleştirilmesi, gereksinim duyduğunuz tooadd hello galeri tooyour listesinden yönetilen SaaS uygulamaları Kindling.</span><span class="sxs-lookup"><span data-stu-id="8cb35-125">tooconfigure hello integration of Kindling into Azure AD, you need tooadd Kindling from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8cb35-126">**tooadd hello Galerisi'nden Kindling, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="8cb35-126">**tooadd Kindling from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8cb35-127">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="8cb35-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8cb35-129">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="8cb35-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8cb35-130">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="8cb35-130">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="8cb35-132">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="8cb35-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="8cb35-134">Merhaba arama kutusuna yazın **Kindling**.</span><span class="sxs-lookup"><span data-stu-id="8cb35-134">In hello search box, type **Kindling**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_search.png)

5. <span data-ttu-id="8cb35-136">Merhaba Sonuçlar panelinde seçin **Kindling**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="8cb35-136">In hello results panel, select **Kindling**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8cb35-138">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="8cb35-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8cb35-139">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Kindling ile test etme</span><span class="sxs-lookup"><span data-stu-id="8cb35-139">In this section, you configure and test Azure AD single sign-on with Kindling based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8cb35-140">Tek toowork'ın oturum açma hangi hello karşılık gelen Kindling içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="8cb35-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kindling is tooa user in Azure AD.</span></span> <span data-ttu-id="8cb35-141">Diğer bir deyişle, bir bağlantı bir Azure AD kullanıcı ve kullanıcı arasındaki ilişki hello ilgili kurulan Kindling gereksinimlerini toobe içinde.</span><span class="sxs-lookup"><span data-stu-id="8cb35-141">In other words, a link relationship between an Azure AD user and hello related user in Kindling needs toobe established.</span></span>

<span data-ttu-id="8cb35-142">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** Kindling içinde.</span><span class="sxs-lookup"><span data-stu-id="8cb35-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Kindling.</span></span>

<span data-ttu-id="8cb35-143">tooconfigure ve Kindling ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="8cb35-143">tooconfigure and test Azure AD single sign-on with Kindling, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8cb35-144">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="8cb35-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8cb35-145">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="8cb35-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8cb35-146">**[Kindling test kullanıcısı oluşturma](#creating-a-kindling-test-user)**  -toohave diğer bir deyişle Kindling içinde bir karşılık gelen Britta Simon, bağlı kullanıcı toohello Azure AD gösterimi.</span><span class="sxs-lookup"><span data-stu-id="8cb35-146">**[Creating a Kindling test user](#creating-a-kindling-test-user)** - toohave a counterpart of Britta Simon in Kindling that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8cb35-147">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="8cb35-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8cb35-148">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="8cb35-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8cb35-149">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="8cb35-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8cb35-150">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Kindling uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="8cb35-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kindling application.</span></span>

<span data-ttu-id="8cb35-151">**Azure AD çoklu oturum açma tooconfigure Kindling ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="8cb35-151">**tooconfigure Azure AD single sign-on with Kindling, perform hello following steps:**</span></span>

1. <span data-ttu-id="8cb35-152">Hello hello üzerinde Azure portal'ın **Kindling** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="8cb35-152">In hello Azure portal, on hello **Kindling** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="8cb35-154">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="8cb35-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_samlbase.png)

3. <span data-ttu-id="8cb35-156">Merhaba üzerinde **Kindling etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="8cb35-156">On hello **Kindling Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_url.png)

    <span data-ttu-id="8cb35-158">a.</span><span class="sxs-lookup"><span data-stu-id="8cb35-158">a.</span></span> <span data-ttu-id="8cb35-159">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.kindlingapp.com`</span><span class="sxs-lookup"><span data-stu-id="8cb35-159">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.kindlingapp.com`</span></span>

    <span data-ttu-id="8cb35-160">b.</span><span class="sxs-lookup"><span data-stu-id="8cb35-160">b.</span></span>  <span data-ttu-id="8cb35-161">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.kindlingapp.com/saml/module.php/saml/sp/metadata.php/clientIDP`</span><span class="sxs-lookup"><span data-stu-id="8cb35-161">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.kindlingapp.com/saml/module.php/saml/sp/metadata.php/clientIDP`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8cb35-162">Bu değerler hello gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="8cb35-162">These values are not hello real.</span></span> <span data-ttu-id="8cb35-163">Bu değerler, oturum açma hello gerçek URL ve tanımlayıcıdır ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="8cb35-163">Update these values with hello actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="8cb35-164">Kişi [Kindling destek ekibi](mailto:support@kindlingapp.com) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="8cb35-164">Contact [Kindling support team](mailto:support@kindlingapp.com) tooget these values.</span></span>
 
4. <span data-ttu-id="8cb35-165">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="8cb35-165">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_certificate.png) 

5. <span data-ttu-id="8cb35-167">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="8cb35-167">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kindling-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8cb35-169">Merhaba üzerinde **Kindling yapılandırma** 'yi tıklatın **yapılandırma Kindling** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="8cb35-169">On hello **Kindling Configuration** section, click **Configure Kindling** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="8cb35-170">Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="8cb35-170">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_configure.png) 

7. <span data-ttu-id="8cb35-172">tooconfigure çoklu oturum açma üzerinde **Kindling** yan, indirilen toosend hello ihtiyacınız **sertifika (Base64)**, **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si**çok[Kindling destek ekibi](mailto:support@kindlingapp.com).</span><span class="sxs-lookup"><span data-stu-id="8cb35-172">tooconfigure single sign-on on **Kindling** side, you need toosend hello downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Kindling support team](mailto:support@kindlingapp.com).</span></span>

> [!TIP]
> <span data-ttu-id="8cb35-173">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="8cb35-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8cb35-174">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="8cb35-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8cb35-175">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8cb35-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8cb35-176">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="8cb35-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="8cb35-177">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="8cb35-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="8cb35-179">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="8cb35-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8cb35-180">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="8cb35-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kindling-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8cb35-182">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="8cb35-182">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kindling-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8cb35-184">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="8cb35-184">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kindling-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8cb35-186">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="8cb35-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kindling-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8cb35-188">a.</span><span class="sxs-lookup"><span data-stu-id="8cb35-188">a.</span></span> <span data-ttu-id="8cb35-189">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8cb35-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8cb35-190">b.</span><span class="sxs-lookup"><span data-stu-id="8cb35-190">b.</span></span> <span data-ttu-id="8cb35-191">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="8cb35-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8cb35-192">c.</span><span class="sxs-lookup"><span data-stu-id="8cb35-192">c.</span></span> <span data-ttu-id="8cb35-193">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="8cb35-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8cb35-194">d.</span><span class="sxs-lookup"><span data-stu-id="8cb35-194">d.</span></span> <span data-ttu-id="8cb35-195">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8cb35-195">Click **Create**.</span></span>
 
### <a name="creating-a-kindling-test-user"></a><span data-ttu-id="8cb35-196">Kindling test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="8cb35-196">Creating a Kindling test user</span></span>

<span data-ttu-id="8cb35-197">Bu bölümde Hello amacı toocreate Britta Simon içinde Kindling adlı bir kullanıcı ' dir.</span><span class="sxs-lookup"><span data-stu-id="8cb35-197">hello objective of this section is toocreate a user called Britta Simon in Kindling.</span></span> <span data-ttu-id="8cb35-198">Yalnızca zaman sağlama kindling destekler.</span><span class="sxs-lookup"><span data-stu-id="8cb35-198">Kindling supports just-in-time provisioning.</span></span> <span data-ttu-id="8cb35-199">İçinde zaten etkinleştirdiğiniz [yapılandırma Azure AD çoklu oturum açma](#configuring-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="8cb35-199">You have already enabled it in [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

<span data-ttu-id="8cb35-200">Bu bölümde, eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="8cb35-200">There is no action item for you in this section.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8cb35-201">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="8cb35-201">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8cb35-202">Bu bölümde, erişim tooKindling vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="8cb35-202">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKindling.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="8cb35-204">**tooassign Britta Simon tooKindling hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="8cb35-204">**tooassign Britta Simon tooKindling, perform hello following steps:**</span></span>

1. <span data-ttu-id="8cb35-205">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="8cb35-205">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="8cb35-207">Merhaba uygulamalar listesinde **Kindling**.</span><span class="sxs-lookup"><span data-stu-id="8cb35-207">In hello applications list, select **Kindling**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_app.png) 

3. <span data-ttu-id="8cb35-209">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="8cb35-209">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="8cb35-211">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="8cb35-211">Click **Add** button.</span></span> <span data-ttu-id="8cb35-212">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="8cb35-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="8cb35-214">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="8cb35-214">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8cb35-215">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="8cb35-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8cb35-216">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="8cb35-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8cb35-217">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="8cb35-217">Testing single sign-on</span></span>

<span data-ttu-id="8cb35-218">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="8cb35-218">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8cb35-219">Merhaba Kindling hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Kindling uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8cb35-219">When you click hello Kindling tile in hello Access Panel, you should get automatically signed-on tooyour Kindling application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="8cb35-220">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="8cb35-220">Additional resources</span></span>

* [<span data-ttu-id="8cb35-221">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="8cb35-221">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8cb35-222">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="8cb35-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_203.png

