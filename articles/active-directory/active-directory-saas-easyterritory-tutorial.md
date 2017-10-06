---
title: "Öğretici: Azure Active Directory Tümleştirme ile EasyTerritory | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile EasyTerritory arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d29b362d-e986-4f67-8ff2-e158e49353aa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 4f1e9fb4d615325f0d57bebaed955529d5dcd9b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-easyterritory"></a><span data-ttu-id="89908-103">Öğretici: Azure Active Directory Tümleştirme EasyTerritory ile</span><span class="sxs-lookup"><span data-stu-id="89908-103">Tutorial: Azure Active Directory integration with EasyTerritory</span></span>

<span data-ttu-id="89908-104">Bu öğreticide, bilgi nasıl toointegrate EasyTerritory Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="89908-104">In this tutorial, you learn how toointegrate EasyTerritory with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="89908-105">EasyTerritory Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="89908-105">Integrating EasyTerritory with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="89908-106">Erişim tooEasyTerritory sahip Azure AD'de kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="89908-106">You can control in Azure AD who has access tooEasyTerritory.</span></span>
- <span data-ttu-id="89908-107">Kullanıcıların tooautomatically get açan tooEasyTerritory (çoklu oturum açma) Azure AD hesaplarına ile etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="89908-107">You can enable your users tooautomatically get signed-on tooEasyTerritory (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="89908-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="89908-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="89908-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="89908-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="89908-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="89908-110">Prerequisites</span></span>

<span data-ttu-id="89908-111">tooconfigure EasyTerritory ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="89908-111">tooconfigure Azure AD integration with EasyTerritory, you need hello following items:</span></span>

- <span data-ttu-id="89908-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="89908-112">An Azure AD subscription</span></span>
- <span data-ttu-id="89908-113">Bir EasyTerritory çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="89908-113">A EasyTerritory single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="89908-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="89908-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="89908-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="89908-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="89908-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="89908-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="89908-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="89908-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="89908-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="89908-118">Scenario description</span></span>
<span data-ttu-id="89908-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="89908-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="89908-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="89908-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="89908-121">Merhaba Galerisi'nden EasyTerritory ekleme</span><span class="sxs-lookup"><span data-stu-id="89908-121">Adding EasyTerritory from hello gallery</span></span>
2. <span data-ttu-id="89908-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="89908-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-easyterritory-from-hello-gallery"></a><span data-ttu-id="89908-123">Merhaba Galerisi'nden EasyTerritory ekleme</span><span class="sxs-lookup"><span data-stu-id="89908-123">Adding EasyTerritory from hello gallery</span></span>
<span data-ttu-id="89908-124">Azure AD'ye tooconfigure hello tümleştirme EasyTerritory, tooadd EasyTerritory hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="89908-124">tooconfigure hello integration of EasyTerritory into Azure AD, you need tooadd EasyTerritory from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="89908-125">**tooadd EasyTerritory hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="89908-125">**tooadd EasyTerritory from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="89908-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="89908-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory düğmesi][1]

2. <span data-ttu-id="89908-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="89908-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="89908-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="89908-129">Then go too**All applications**.</span></span>

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="89908-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="89908-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Merhaba yeni uygulama düğmesi][3]

4. <span data-ttu-id="89908-133">Merhaba arama kutusuna yazın **EasyTerritory**seçin **EasyTerritory** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="89908-133">In hello search box, type **EasyTerritory**, select **EasyTerritory** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Merhaba sonuçları listesinde EasyTerritory](./media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="89908-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="89908-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="89908-136">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı EasyTerritory sınayın.</span><span class="sxs-lookup"><span data-stu-id="89908-136">In this section, you configure and test Azure AD single sign-on with EasyTerritory based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="89908-137">Tek toowork'ın oturum açma hangi hello karşılık gelen EasyTerritory içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="89908-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in EasyTerritory is tooa user in Azure AD.</span></span> <span data-ttu-id="89908-138">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı EasyTerritory hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="89908-138">In other words, a link relationship between an Azure AD user and hello related user in EasyTerritory needs toobe established.</span></span>

<span data-ttu-id="89908-139">Merhaba hello değeri EasyTerritory içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="89908-139">In EasyTerritory, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="89908-140">tooconfigure ve EasyTerritory ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="89908-140">tooconfigure and test Azure AD single sign-on with EasyTerritory, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="89908-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="89908-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="89908-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="89908-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="89908-143">**[EasyTerritory test kullanıcısı oluşturma](#create-a-easyterritory-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir EasyTerritory içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="89908-143">**[Create a EasyTerritory test user](#create-a-easyterritory-test-user)** - toohave a counterpart of Britta Simon in EasyTerritory that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="89908-144">**[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="89908-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="89908-145">**[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="89908-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="89908-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="89908-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="89908-147">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma EasyTerritory uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="89908-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your EasyTerritory application.</span></span>

<span data-ttu-id="89908-148">**tooconfigure Azure AD çoklu oturum açma ile EasyTerritory, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="89908-148">**tooconfigure Azure AD single sign-on with EasyTerritory, perform hello following steps:**</span></span>

1. <span data-ttu-id="89908-149">Hello hello üzerinde Azure portal'ın **EasyTerritory** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="89908-149">In hello Azure portal, on hello **EasyTerritory** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. <span data-ttu-id="89908-151">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="89908-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_samlbase.png)

3. <span data-ttu-id="89908-153">Merhaba üzerinde **EasyTerritory etki alanı ve URL'leri** bölümünde, hello tooconfigure hello IDP uygulamada başlatılan modu istiyorsanız aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="89908-153">On hello **EasyTerritory Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in IDP initiated mode:</span></span>

    ![EasyTerritory etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_url.png)

    <span data-ttu-id="89908-155">a.</span><span class="sxs-lookup"><span data-stu-id="89908-155">a.</span></span> <span data-ttu-id="89908-156">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://apps.easyterritory.com/<tenant id>/dev/`</span><span class="sxs-lookup"><span data-stu-id="89908-156">In hello **Identifier** textbox, type a URL using hello following pattern: `https://apps.easyterritory.com/<tenant id>/dev/`</span></span>

    <span data-ttu-id="89908-157">b.</span><span class="sxs-lookup"><span data-stu-id="89908-157">b.</span></span> <span data-ttu-id="89908-158">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://apps.easyterritory.com/<tenant id>/dev/authservices/acs`</span><span class="sxs-lookup"><span data-stu-id="89908-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://apps.easyterritory.com/<tenant id>/dev/authservices/acs`</span></span>

4. <span data-ttu-id="89908-159">Denetleme **Göster Gelişmiş URL ayarları** ve adım tooconfigure hello uygulamada istiyorsanız aşağıdaki hello gerçekleştirmek **SP** modunda başlatılan:</span><span class="sxs-lookup"><span data-stu-id="89908-159">Check **Show advanced URL settings** and perform hello following step if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![EasyTerritory etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_url1.png)

    <span data-ttu-id="89908-161">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<company name>.easyterritory.com/`</span><span class="sxs-lookup"><span data-stu-id="89908-161">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.easyterritory.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="89908-162">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="89908-162">These values are not real.</span></span> <span data-ttu-id="89908-163">Bu güncelleştirme tanımlayıcısı, yanıt URL'si ve oturum açma URL'si ile Merhaba gerçek değerler.</span><span class="sxs-lookup"><span data-stu-id="89908-163">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="89908-164">Kişi [EasyTerritory istemci destek ekibi](mailto:sales@easyterritory.com) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="89908-164">Contact [EasyTerritory Client support team](mailto:sales@easyterritory.com) tooget these values.</span></span> 

5. <span data-ttu-id="89908-165">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="89908-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_certificate.png) 

6. <span data-ttu-id="89908-167">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="89908-167">Click **Save** button.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-easyterritory-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="89908-169">tooconfigure çoklu oturum açma üzerinde **EasyTerritory** yan, indirilen toosend hello ihtiyacınız **meta veri XML** çok[EasyTerritory destek ekibi](mailto:sales@easyterritory.com).</span><span class="sxs-lookup"><span data-stu-id="89908-169">tooconfigure single sign-on on **EasyTerritory** side, you need toosend hello downloaded **Metadata XML** too[EasyTerritory support team](mailto:sales@easyterritory.com).</span></span> <span data-ttu-id="89908-170">Bunlar, bu ayar toohave hello iki tarafta da ayarlamanızı SAML SSO bağlantı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="89908-170">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="89908-171">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="89908-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="89908-172">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="89908-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="89908-173">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="89908-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="89908-174">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="89908-174">Create an Azure AD test user</span></span>

<span data-ttu-id="89908-175">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="89908-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="89908-177">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="89908-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="89908-178">Merhaba hello sol bölmede Azure portal hello tıklatın **Azure Active Directory** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="89908-178">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-easyterritory-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="89908-180">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="89908-180">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-easyterritory-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="89908-182">tooopen hello **kullanıcı** iletişim kutusu, tıklatın **Ekle** hello hello üstündeki **tüm kullanıcılar** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="89908-182">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Merhaba Ekle düğmesi](./media/active-directory-saas-easyterritory-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="89908-184">Merhaba, **kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="89908-184">In hello **User** dialog box, perform hello following steps:</span></span>

    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-easyterritory-tutorial/create_aaduser_04.png)

    <span data-ttu-id="89908-186">a.</span><span class="sxs-lookup"><span data-stu-id="89908-186">a.</span></span> <span data-ttu-id="89908-187">Merhaba, **adı** kutusuna **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="89908-187">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="89908-188">b.</span><span class="sxs-lookup"><span data-stu-id="89908-188">b.</span></span> <span data-ttu-id="89908-189">Merhaba, **kullanıcı adı** kutusuna, kullanıcının Britta Simon hello e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="89908-189">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="89908-190">c.</span><span class="sxs-lookup"><span data-stu-id="89908-190">c.</span></span> <span data-ttu-id="89908-191">Select hello **Göster parola** onay kutusunu işaretleyin ve ardından hello görüntülenen hello değerini aşağı yazma **parola** kutusu.</span><span class="sxs-lookup"><span data-stu-id="89908-191">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="89908-192">d.</span><span class="sxs-lookup"><span data-stu-id="89908-192">d.</span></span> <span data-ttu-id="89908-193">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="89908-193">Click **Create**.</span></span>
 
### <a name="create-a-easyterritory-test-user"></a><span data-ttu-id="89908-194">EasyTerritory test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="89908-194">Create a EasyTerritory test user</span></span>

<span data-ttu-id="89908-195">Bu bölümde, EasyTerritory içinde Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="89908-195">In this section, you create a user called Britta Simon in EasyTerritory.</span></span> <span data-ttu-id="89908-196">Lütfen çalışmak [EasyTerritory destek ekibi](mailto:sales@easyterritory.com) tooadd hello kullanıcılar hello EasyTerritory Platform.</span><span class="sxs-lookup"><span data-stu-id="89908-196">Please work with [EasyTerritory support team](mailto:sales@easyterritory.com) tooadd hello users in hello EasyTerritory platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="89908-197">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="89908-197">Assign hello Azure AD test user</span></span>

<span data-ttu-id="89908-198">Bu bölümde, erişim tooEasyTerritory vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="89908-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooEasyTerritory.</span></span>

![Merhaba kullanıcı rolü atayın][200] 

<span data-ttu-id="89908-200">**tooassign Britta Simon tooEasyTerritory hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="89908-200">**tooassign Britta Simon tooEasyTerritory, perform hello following steps:**</span></span>

1. <span data-ttu-id="89908-201">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="89908-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="89908-203">Merhaba uygulamalar listesinde **EasyTerritory**.</span><span class="sxs-lookup"><span data-stu-id="89908-203">In hello applications list, select **EasyTerritory**.</span></span>

    ![Merhaba EasyTerritory bağlantı hello uygulamalar listesinde](./media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_app.png)  

3. <span data-ttu-id="89908-205">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="89908-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202]

4. <span data-ttu-id="89908-207">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="89908-207">Click **Add** button.</span></span> <span data-ttu-id="89908-208">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="89908-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Merhaba eklemek atama bölmesi][203]

5. <span data-ttu-id="89908-210">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="89908-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="89908-211">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="89908-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="89908-212">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="89908-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="89908-213">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="89908-213">Test single sign-on</span></span>

<span data-ttu-id="89908-214">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="89908-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="89908-215">Merhaba EasyTerritory hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour EasyTerritory uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="89908-215">When you click hello EasyTerritory tile in hello Access Panel, you should get automatically signed-on tooyour EasyTerritory application.</span></span>
<span data-ttu-id="89908-216">Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="89908-216">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="89908-217">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="89908-217">Additional resources</span></span>

* [<span data-ttu-id="89908-218">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="89908-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="89908-219">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="89908-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)




<!--Image references-->

[1]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_203.png

