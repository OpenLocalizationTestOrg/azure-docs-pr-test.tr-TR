---
title: "Öğretici: Azure Active Directory Tümleştirme ile Greenhouse | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Greenhouse arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 78ec1766-4f79-4f16-9a66-d5584c4b6151
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 1a7cdd00c4f2b15a1afc89522d79af22f4c5d866
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-greenhouse"></a><span data-ttu-id="73b34-103">Öğretici: Azure Active Directory Tümleştirme Greenhouse ile</span><span class="sxs-lookup"><span data-stu-id="73b34-103">Tutorial: Azure Active Directory integration with Greenhouse</span></span>

<span data-ttu-id="73b34-104">Bu öğreticide, bilgi nasıl toointegrate Greenhouse Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="73b34-104">In this tutorial, you learn how toointegrate Greenhouse with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="73b34-105">Greenhouse Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="73b34-105">Integrating Greenhouse with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="73b34-106">Erişim tooGreenhouse sahip Azure AD'de kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="73b34-106">You can control in Azure AD who has access tooGreenhouse.</span></span>
- <span data-ttu-id="73b34-107">Kullanıcıların tooautomatically get açan tooGreenhouse (çoklu oturum açma) Azure AD hesaplarına ile etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="73b34-107">You can enable your users tooautomatically get signed-on tooGreenhouse (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="73b34-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="73b34-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="73b34-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="73b34-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="73b34-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="73b34-110">Prerequisites</span></span>

<span data-ttu-id="73b34-111">tooconfigure Greenhouse ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="73b34-111">tooconfigure Azure AD integration with Greenhouse, you need hello following items:</span></span>

- <span data-ttu-id="73b34-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="73b34-112">An Azure AD subscription</span></span>
- <span data-ttu-id="73b34-113">Bir Greenhouse çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="73b34-113">A Greenhouse single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="73b34-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="73b34-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="73b34-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="73b34-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="73b34-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="73b34-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="73b34-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="73b34-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="73b34-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="73b34-118">Scenario description</span></span>
<span data-ttu-id="73b34-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="73b34-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="73b34-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="73b34-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="73b34-121">Merhaba Galerisi'nden Greenhouse ekleme</span><span class="sxs-lookup"><span data-stu-id="73b34-121">Adding Greenhouse from hello gallery</span></span>
2. <span data-ttu-id="73b34-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="73b34-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-greenhouse-from-hello-gallery"></a><span data-ttu-id="73b34-123">Merhaba Galerisi'nden Greenhouse ekleme</span><span class="sxs-lookup"><span data-stu-id="73b34-123">Adding Greenhouse from hello gallery</span></span>
<span data-ttu-id="73b34-124">Azure AD'ye tooconfigure hello tümleştirme Greenhouse, tooadd Greenhouse hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="73b34-124">tooconfigure hello integration of Greenhouse into Azure AD, you need tooadd Greenhouse from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="73b34-125">**tooadd Greenhouse hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="73b34-125">**tooadd Greenhouse from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="73b34-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="73b34-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory düğmesi][1]

2. <span data-ttu-id="73b34-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="73b34-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="73b34-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="73b34-129">Then go too**All applications**.</span></span>

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="73b34-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="73b34-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Merhaba yeni uygulama düğmesi][3]

4. <span data-ttu-id="73b34-133">Merhaba arama kutusuna yazın **Greenhouse**seçin **Greenhouse** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="73b34-133">In hello search box, type **Greenhouse**, select **Greenhouse** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Merhaba sonuçları listesinde greenhouse](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="73b34-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="73b34-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="73b34-136">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Greenhouse sınayın.</span><span class="sxs-lookup"><span data-stu-id="73b34-136">In this section, you configure and test Azure AD single sign-on with Greenhouse based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="73b34-137">Tek toowork'ın oturum açma hangi hello karşılık gelen Greenhouse içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="73b34-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Greenhouse is tooa user in Azure AD.</span></span> <span data-ttu-id="73b34-138">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Greenhouse hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="73b34-138">In other words, a link relationship between an Azure AD user and hello related user in Greenhouse needs toobe established.</span></span>

<span data-ttu-id="73b34-139">Merhaba hello değeri Greenhouse içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="73b34-139">In Greenhouse, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="73b34-140">tooconfigure ve Greenhouse ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="73b34-140">tooconfigure and test Azure AD single sign-on with Greenhouse, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="73b34-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="73b34-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="73b34-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="73b34-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="73b34-143">**[Greenhouse test kullanıcısı oluşturma](#create-a-greenhouse-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Greenhouse içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="73b34-143">**[Create a Greenhouse test user](#create-a-greenhouse-test-user)** - toohave a counterpart of Britta Simon in Greenhouse that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="73b34-144">**[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="73b34-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="73b34-145">**[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="73b34-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="73b34-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="73b34-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="73b34-147">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Greenhouse uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="73b34-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Greenhouse application.</span></span>

<span data-ttu-id="73b34-148">**tooconfigure Azure AD çoklu oturum açma ile Greenhouse, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="73b34-148">**tooconfigure Azure AD single sign-on with Greenhouse, perform hello following steps:**</span></span>

1. <span data-ttu-id="73b34-149">Hello hello üzerinde Azure portal'ın **Greenhouse** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="73b34-149">In hello Azure portal, on hello **Greenhouse** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. <span data-ttu-id="73b34-151">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="73b34-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_samlbase.png)

3. <span data-ttu-id="73b34-153">Merhaba üzerinde **Greenhouse etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="73b34-153">On hello **Greenhouse Domain and URLs** section, perform hello following steps:</span></span>

    ![Greenhouse etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_url.png)

    <span data-ttu-id="73b34-155">a.</span><span class="sxs-lookup"><span data-stu-id="73b34-155">a.</span></span> <span data-ttu-id="73b34-156">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.greenhouse.io`</span><span class="sxs-lookup"><span data-stu-id="73b34-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.greenhouse.io`</span></span>

    <span data-ttu-id="73b34-157">b.</span><span class="sxs-lookup"><span data-stu-id="73b34-157">b.</span></span> <span data-ttu-id="73b34-158">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.greenhouse.io`</span><span class="sxs-lookup"><span data-stu-id="73b34-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.greenhouse.io`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="73b34-159">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="73b34-159">These values are not real.</span></span> <span data-ttu-id="73b34-160">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="73b34-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="73b34-161">Kişi [Greenhouse istemci destek ekibi](https://www.greenhouse.io/contact) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="73b34-161">Contact [Greenhouse Client support team](https://www.greenhouse.io/contact) tooget these values.</span></span> 
 


4. <span data-ttu-id="73b34-162">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="73b34-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_certificate.png) 

5. <span data-ttu-id="73b34-164">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="73b34-164">Click **Save** button.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-greenhouse-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="73b34-166">tooconfigure çoklu oturum açma üzerinde **Greenhouse** yan, indirilen toosend hello ihtiyacınız **meta veri XML** çok[Greenhouse destek ekibi](http://www.greenhouse.io/contact).</span><span class="sxs-lookup"><span data-stu-id="73b34-166">tooconfigure single sign-on on **Greenhouse** side, you need toosend hello downloaded **Metadata XML** too[Greenhouse support team](http://www.greenhouse.io/contact).</span></span>

> [!TIP]
> <span data-ttu-id="73b34-167">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="73b34-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="73b34-168">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="73b34-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="73b34-169">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="73b34-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="73b34-170">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="73b34-170">Create an Azure AD test user</span></span>

<span data-ttu-id="73b34-171">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="73b34-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="73b34-173">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="73b34-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="73b34-174">Merhaba hello sol bölmede Azure portal hello tıklatın **Azure Active Directory** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="73b34-174">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-greenhouse-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="73b34-176">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="73b34-176">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-greenhouse-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="73b34-178">tooopen hello **kullanıcı** iletişim kutusu, tıklatın **Ekle** hello hello üstündeki **tüm kullanıcılar** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="73b34-178">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Merhaba Ekle düğmesi](./media/active-directory-saas-greenhouse-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="73b34-180">Merhaba, **kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="73b34-180">In hello **User** dialog box, perform hello following steps:</span></span>

    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-greenhouse-tutorial/create_aaduser_04.png)

    <span data-ttu-id="73b34-182">a.</span><span class="sxs-lookup"><span data-stu-id="73b34-182">a.</span></span> <span data-ttu-id="73b34-183">Merhaba, **adı** kutusuna **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="73b34-183">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="73b34-184">b.</span><span class="sxs-lookup"><span data-stu-id="73b34-184">b.</span></span> <span data-ttu-id="73b34-185">Merhaba, **kullanıcı adı** kutusuna, kullanıcının Britta Simon hello e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="73b34-185">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="73b34-186">c.</span><span class="sxs-lookup"><span data-stu-id="73b34-186">c.</span></span> <span data-ttu-id="73b34-187">Select hello **Göster parola** onay kutusunu işaretleyin ve ardından hello görüntülenen hello değerini aşağı yazma **parola** kutusu.</span><span class="sxs-lookup"><span data-stu-id="73b34-187">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="73b34-188">d.</span><span class="sxs-lookup"><span data-stu-id="73b34-188">d.</span></span> <span data-ttu-id="73b34-189">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="73b34-189">Click **Create**.</span></span>
 
### <a name="create-a-greenhouse-test-user"></a><span data-ttu-id="73b34-190">Greenhouse test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="73b34-190">Create a Greenhouse test user</span></span>

<span data-ttu-id="73b34-191">Greenhouse içine sipariş tooenable Azure AD kullanıcıların toolog bunların Greenhouse sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="73b34-191">In order tooenable Azure AD users toolog into Greenhouse, they must be provisioned into Greenhouse.</span></span> <span data-ttu-id="73b34-192">Greenhouse Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="73b34-192">In hello case of Greenhouse, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="73b34-193">API AAD kullanıcı hesaplarının Greenhouse tooprovision tarafından sağlanan veya herhangi diğer Greenhouse kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="73b34-193">You can use any other Greenhouse user account creation tools or APIs provided by Greenhouse tooprovision AAD user accounts.</span></span> 

<span data-ttu-id="73b34-194">**bir kullanıcı hesapları tooprovision gerçekleştirmek hello adımları izleyin:**</span><span class="sxs-lookup"><span data-stu-id="73b34-194">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="73b34-195">İçinde tooyour oturum **Greenhouse** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="73b34-195">Log in tooyour **Greenhouse** company site as an administrator.</span></span>

2. <span data-ttu-id="73b34-196">Hello içinde hello üst menüsünde **yapılandırma**ve ardından **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="73b34-196">In hello menu on hello top, click **Configure**, and then click **Users**.</span></span>
   
   <span data-ttu-id="73b34-197">![Kullanıcıların](./media/active-directory-saas-greenhouse-tutorial/ic790791.png "kullanıcılar")</span><span class="sxs-lookup"><span data-stu-id="73b34-197">![Users](./media/active-directory-saas-greenhouse-tutorial/ic790791.png "Users")</span></span>

3. <span data-ttu-id="73b34-198">Tıklatın **yeni kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="73b34-198">Click **New Users**.</span></span>
   
   <span data-ttu-id="73b34-199">![Yeni kullanıcı](./media/active-directory-saas-greenhouse-tutorial/ic790792.png "yeni kullanıcı")</span><span class="sxs-lookup"><span data-stu-id="73b34-199">![New User](./media/active-directory-saas-greenhouse-tutorial/ic790792.png "New User")</span></span>

4. <span data-ttu-id="73b34-200">Merhaba, **yeni kullanıcı Ekle** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="73b34-200">In hello **Add New User** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="73b34-201">![Yeni Kullanıcı Ekle](./media/active-directory-saas-greenhouse-tutorial/ic790793.png "yeni kullanıcı Ekle")</span><span class="sxs-lookup"><span data-stu-id="73b34-201">![Add New User](./media/active-directory-saas-greenhouse-tutorial/ic790793.png "Add New User")</span></span>

   <span data-ttu-id="73b34-202">a.</span><span class="sxs-lookup"><span data-stu-id="73b34-202">a.</span></span> <span data-ttu-id="73b34-203">Merhaba, **girin kullanıcı e-postaları** metin kutusuna, tooprovision istediğiniz geçerli bir Azure Active Directory hesabının hello e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="73b34-203">In hello **Enter user emails** textbox, type hello email address of a valid Azure Active Directory account you want tooprovision.</span></span>

   <span data-ttu-id="73b34-204">b.</span><span class="sxs-lookup"><span data-stu-id="73b34-204">b.</span></span> <span data-ttu-id="73b34-205">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="73b34-205">Click **Save**.</span></span>    
   
      >[!NOTE]
      ><span data-ttu-id="73b34-206">Hello Azure Active Directory hesap sahipleri, etkinleştirilmeden önce bir bağlantı tooconfirm hello hesabı dahil olmak üzere bir e-posta alacaksınız.</span><span class="sxs-lookup"><span data-stu-id="73b34-206">hello Azure Active Directory account holders will receive an email including a link tooconfirm hello account before it becomes active.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="73b34-207">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="73b34-207">Assign hello Azure AD test user</span></span>

<span data-ttu-id="73b34-208">Bu bölümde, erişim tooGreenhouse vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="73b34-208">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooGreenhouse.</span></span>

![Merhaba kullanıcı rolü atayın][200] 

<span data-ttu-id="73b34-210">**tooassign Britta Simon tooGreenhouse hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="73b34-210">**tooassign Britta Simon tooGreenhouse, perform hello following steps:**</span></span>

1. <span data-ttu-id="73b34-211">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="73b34-211">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="73b34-213">Merhaba uygulamalar listesinde **Greenhouse**.</span><span class="sxs-lookup"><span data-stu-id="73b34-213">In hello applications list, select **Greenhouse**.</span></span>

    ![Merhaba Greenhouse bağlantı hello uygulamalar listesinde](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_app.png)  

3. <span data-ttu-id="73b34-215">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="73b34-215">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202]

4. <span data-ttu-id="73b34-217">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="73b34-217">Click **Add** button.</span></span> <span data-ttu-id="73b34-218">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="73b34-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Merhaba eklemek atama bölmesi][203]

5. <span data-ttu-id="73b34-220">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="73b34-220">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="73b34-221">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="73b34-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="73b34-222">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="73b34-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="73b34-223">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="73b34-223">Test single sign-on</span></span>

<span data-ttu-id="73b34-224">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="73b34-224">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="73b34-225">Merhaba Greenhouse hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Greenhouse uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="73b34-225">When you click hello Greenhouse tile in hello Access Panel, you should get automatically signed-on tooyour Greenhouse application.</span></span>
<span data-ttu-id="73b34-226">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="73b34-226">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="73b34-227">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="73b34-227">Additional resources</span></span>

* [<span data-ttu-id="73b34-228">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="73b34-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="73b34-229">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="73b34-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_203.png

