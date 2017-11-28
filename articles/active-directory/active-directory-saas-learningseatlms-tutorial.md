---
title: "Öğretici: Azure Active Directory Tümleştirme Learning bilgisayar başına LMS ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Learning bilgisayar başına LMS arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bb056fcf-4135-478e-85b1-5015d1f07b85
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: jeedes
ms.openlocfilehash: dc08aa444b85f35a4458768ac560ec663baa1c95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learning-seat-lms"></a><span data-ttu-id="fd6d4-103">Öğretici: Azure Active Directory Tümleştirme Learning bilgisayar başına LMS ile</span><span class="sxs-lookup"><span data-stu-id="fd6d4-103">Tutorial: Azure Active Directory integration with Learning Seat LMS</span></span>

<span data-ttu-id="fd6d4-104">Bu öğreticide, bilgi nasıl toointegrate Learning bilgisayar başına LMS Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fd6d4-104">In this tutorial, you learn how toointegrate Learning Seat LMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fd6d4-105">Learning bilgisayar başına LMS Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="fd6d4-105">Integrating Learning Seat LMS with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="fd6d4-106">Erişim tooLearning bilgisayar başına LMS sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="fd6d4-106">You can control in Azure AD who has access tooLearning Seat LMS</span></span>
- <span data-ttu-id="fd6d4-107">Azure AD hesaplarına ile kullanıcılar tooautomatically get açan tooLearning (çoklu oturum açma) bilgisayar başına LMS etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="fd6d4-107">You can enable your users tooautomatically get signed-on tooLearning Seat LMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fd6d4-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="fd6d4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="fd6d4-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz.</span><span class="sxs-lookup"><span data-stu-id="fd6d4-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="fd6d4-110">[Uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fd6d4-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fd6d4-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="fd6d4-111">Prerequisites</span></span>

<span data-ttu-id="fd6d4-112">tooconfigure Learning bilgisayar başına LMS ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="fd6d4-112">tooconfigure Azure AD integration with Learning Seat LMS, you need hello following items:</span></span>

- <span data-ttu-id="fd6d4-113">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="fd6d4-113">An Azure AD subscription</span></span>
- <span data-ttu-id="fd6d4-114">Bir Learning bilgisayar başına LMS çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="fd6d4-114">A Learning Seat LMS single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fd6d4-115">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="fd6d4-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fd6d4-116">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="fd6d4-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fd6d4-117">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="fd6d4-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fd6d4-118">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fd6d4-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fd6d4-119">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="fd6d4-119">Scenario description</span></span>
<span data-ttu-id="fd6d4-120">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="fd6d4-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fd6d4-121">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="fd6d4-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fd6d4-122">Learning bilgisayar başına LMS hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="fd6d4-122">Adding Learning Seat LMS from hello gallery</span></span>
2. <span data-ttu-id="fd6d4-123">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="fd6d4-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-learning-seat-lms-from-hello-gallery"></a><span data-ttu-id="fd6d4-124">Learning bilgisayar başına LMS hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="fd6d4-124">Adding Learning Seat LMS from hello gallery</span></span>
<span data-ttu-id="fd6d4-125">Azure AD'ye tooconfigure hello tümleştirme Learning bilgisayar başına LMS, tooadd Learning bilgisayar başına LMS hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="fd6d4-125">tooconfigure hello integration of Learning Seat LMS into Azure AD, you need tooadd Learning Seat LMS from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="fd6d4-126">**tooadd Learning bilgisayar başına LMS hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="fd6d4-126">**tooadd Learning Seat LMS from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="fd6d4-127">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="fd6d4-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="fd6d4-129">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="fd6d4-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="fd6d4-130">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="fd6d4-130">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="fd6d4-132">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="fd6d4-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="fd6d4-134">Merhaba arama kutusuna yazın **Learning bilgisayar başına LMS**.</span><span class="sxs-lookup"><span data-stu-id="fd6d4-134">In hello search box, type **Learning Seat LMS**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_search.png)

5. <span data-ttu-id="fd6d4-136">Merhaba Sonuçlar panelinde seçin **Learning bilgisayar başına LMS**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="fd6d4-136">In hello results panel, select **Learning Seat LMS**, and then click **Add** button tooadd hello application.</span></span>


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fd6d4-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="fd6d4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fd6d4-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma Learning bilgisayar başına "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı LMS ile test etme</span><span class="sxs-lookup"><span data-stu-id="fd6d4-138">In this section, you configure and test Azure AD single sign-on with Learning Seat LMS based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="fd6d4-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Learning bilgisayar başına LMS içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="fd6d4-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Learning Seat LMS is tooa user in Azure AD.</span></span> <span data-ttu-id="fd6d4-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Learning bilgisayar başına LMS hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="fd6d4-140">In other words, a link relationship between an Azure AD user and hello related user in Learning Seat LMS needs toobe established.</span></span>

<span data-ttu-id="fd6d4-141">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** Learning bilgisayar başına LMS içinde.</span><span class="sxs-lookup"><span data-stu-id="fd6d4-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Learning Seat LMS.</span></span>

<span data-ttu-id="fd6d4-142">tooconfigure ve Learning bilgisayar başına LMS ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="fd6d4-142">tooconfigure and test Azure AD single sign-on with Learning Seat LMS, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="fd6d4-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="fd6d4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="fd6d4-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="fd6d4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fd6d4-145">**[Learning bilgisayar başına LMS test kullanıcısı oluşturma](#creating-a-learnconnect-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Learning bilgisayar başına LMS içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="fd6d4-145">**[Creating a Learning Seat LMS test user](#creating-a-learnconnect-test-user)** - toohave a counterpart of Britta Simon in Learning Seat LMS that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="fd6d4-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="fd6d4-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fd6d4-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="fd6d4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fd6d4-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="fd6d4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fd6d4-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Learning bilgisayar başına LMS uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="fd6d4-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Learning Seat LMS application.</span></span>

<span data-ttu-id="fd6d4-150">**Azure AD çoklu oturum açma tooconfigure Learning bilgisayar başına LMS ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="fd6d4-150">**tooconfigure Azure AD single sign-on with Learning Seat LMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="fd6d4-151">Hello hello üzerinde Azure portal'ın **Learning bilgisayar başına LMS** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="fd6d4-151">In hello Azure portal, on hello **Learning Seat LMS** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="fd6d4-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="fd6d4-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_samlbase.png)

3. <span data-ttu-id="fd6d4-155">Merhaba üzerinde **Learning bilgisayar başına LMS etki alanı ve URL'leri** bölümünde, hello tooconfigure hello uygulamada istiyorsanız aşağıdaki adımları gerçekleştirin **IDP** modu tarafından başlatılan:</span><span class="sxs-lookup"><span data-stu-id="fd6d4-155">On hello **Learning Seat LMS Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_url.png)

    <span data-ttu-id="fd6d4-157">a.</span><span class="sxs-lookup"><span data-stu-id="fd6d4-157">a.</span></span> <span data-ttu-id="fd6d4-158">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.learningseatlms.com`</span><span class="sxs-lookup"><span data-stu-id="fd6d4-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.learningseatlms.com`</span></span>

    <span data-ttu-id="fd6d4-159">b.</span><span class="sxs-lookup"><span data-stu-id="fd6d4-159">b.</span></span> <span data-ttu-id="fd6d4-160">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.learningseatlms.com/Account/AssertionConsumerService`</span><span class="sxs-lookup"><span data-stu-id="fd6d4-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.learningseatlms.com/Account/AssertionConsumerService`</span></span>

4. <span data-ttu-id="fd6d4-161">Denetleme **Göster Gelişmiş URL ayarları**, tooconfigure hello uygulamada istiyorsanız **SP** modunda başlatılan:</span><span class="sxs-lookup"><span data-stu-id="fd6d4-161">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_url2.png)

    <span data-ttu-id="fd6d4-163">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.learningseatlms.com`</span><span class="sxs-lookup"><span data-stu-id="fd6d4-163">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.learningseatlms.com`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="fd6d4-164">Bu değerleri hello gerçek değerleri değildir.</span><span class="sxs-lookup"><span data-stu-id="fd6d4-164">These values are not hello real values.</span></span> <span data-ttu-id="fd6d4-165">Bu güncelleştirme tanımlayıcı, yanıt URL'si ve oturum açma URL'si ile Merhaba gerçek değerler.</span><span class="sxs-lookup"><span data-stu-id="fd6d4-165">Update these values with hello actual Identifier, Reply URL and Sign-On URL.</span></span> <span data-ttu-id="fd6d4-166">Kişi [Learning bilgisayarı destek ekibi](http://help.learningseatlms.com/help) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="fd6d4-166">Contact [Learning Seat support team](http://help.learningseatlms.com/help) tooget these values.</span></span> 

5. <span data-ttu-id="fd6d4-167">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="fd6d4-167">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_certificate.png) 

6. <span data-ttu-id="fd6d4-169">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="fd6d4-169">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-learnconnect-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="fd6d4-171">tooconfigure çoklu oturum açma üzerinde **Learning bilgisayar başına LMS** yan, indirilen toosend hello ihtiyacınız **meta veri XML** çok[Learning bilgisayarı destek ekibi](http://help.learningseatlms.com/help).</span><span class="sxs-lookup"><span data-stu-id="fd6d4-171">tooconfigure single sign-on on **Learning Seat LMS** side, you need toosend hello downloaded **Metadata XML** too[Learning Seat support team](http://help.learningseatlms.com/help).</span></span>

> [!TIP]
> <span data-ttu-id="fd6d4-172">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="fd6d4-172">You can now read a concise version of these instructions inside hello [Azure  portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="fd6d4-173">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="fd6d4-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="fd6d4-174">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler](https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fd6d4-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation](https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fd6d4-175">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="fd6d4-175">Creating an Azure AD test user</span></span>

<span data-ttu-id="fd6d4-176">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="fd6d4-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="fd6d4-178">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="fd6d4-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="fd6d4-179">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="fd6d4-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-learnconnect-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fd6d4-181">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="fd6d4-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-learnconnect-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fd6d4-183">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="fd6d4-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-learnconnect-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fd6d4-185">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="fd6d4-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-learnconnect-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fd6d4-187">a.</span><span class="sxs-lookup"><span data-stu-id="fd6d4-187">a.</span></span> <span data-ttu-id="fd6d4-188">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fd6d4-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fd6d4-189">b.</span><span class="sxs-lookup"><span data-stu-id="fd6d4-189">b.</span></span> <span data-ttu-id="fd6d4-190">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="fd6d4-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fd6d4-191">c.</span><span class="sxs-lookup"><span data-stu-id="fd6d4-191">c.</span></span> <span data-ttu-id="fd6d4-192">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="fd6d4-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="fd6d4-193">d.</span><span class="sxs-lookup"><span data-stu-id="fd6d4-193">d.</span></span> <span data-ttu-id="fd6d4-194">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fd6d4-194">Click **Create**.</span></span>
 
### <a name="creating-a-learning-seat-lms-test-user"></a><span data-ttu-id="fd6d4-195">Learning bilgisayar başına LMS test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="fd6d4-195">Creating a Learning Seat LMS test user</span></span>

<span data-ttu-id="fd6d4-196">Bu bölümde, Learning bilgisayar başına LMS Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fd6d4-196">In this section, you create a user called Britta Simon in Learning Seat LMS.</span></span> <span data-ttu-id="fd6d4-197">Kişi [Learning bilgisayarı destek ekibi](http://help.learningseatlms.com/help) kullanıcılarla tüm hello kullanıcı bilgileri tooadd hello hello Learning bilgisayar başına LMS uygulama.</span><span class="sxs-lookup"><span data-stu-id="fd6d4-197">Contact [Learning Seat support team](http://help.learningseatlms.com/help) with all hello user information tooadd hello users in hello Learning Seat LMS application.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="fd6d4-198">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="fd6d4-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="fd6d4-199">Bu bölümde, erişim tooLearning bilgisayar başına LMS vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="fd6d4-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLearning Seat LMS.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="fd6d4-201">**tooassign Britta Simon tooLearning bilgisayar başına LMS hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="fd6d4-201">**tooassign Britta Simon tooLearning Seat LMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="fd6d4-202">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="fd6d4-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="fd6d4-204">Merhaba uygulamalar listesinde **Learning bilgisayar başına LMS**.</span><span class="sxs-lookup"><span data-stu-id="fd6d4-204">In hello applications list, select **Learning Seat LMS**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_app.png) 

3. <span data-ttu-id="fd6d4-206">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="fd6d4-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="fd6d4-208">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="fd6d4-208">Click **Add** button.</span></span> <span data-ttu-id="fd6d4-209">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="fd6d4-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="fd6d4-211">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="fd6d4-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="fd6d4-212">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="fd6d4-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fd6d4-213">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="fd6d4-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="fd6d4-214">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="fd6d4-214">Testing single sign-on</span></span>

<span data-ttu-id="fd6d4-215">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="fd6d4-215">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span> 

<span data-ttu-id="fd6d4-216">Learning bilgisayar başına LMS döşeme hello erişim paneli hello tıklatın otomatik olarak oturum açma tooyour Learning bilgisayar başına LMS uygulama olacaktır.</span><span class="sxs-lookup"><span data-stu-id="fd6d4-216">Click hello Learning Seat LMS tile in hello Access Panel, you will be automatically signed-on tooyour Learning Seat LMS application.</span></span> <span data-ttu-id="fd6d4-217">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="fd6d4-217">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fd6d4-218">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="fd6d4-218">Additional resources</span></span>

* [<span data-ttu-id="fd6d4-219">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="fd6d4-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fd6d4-220">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="fd6d4-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_203.png

