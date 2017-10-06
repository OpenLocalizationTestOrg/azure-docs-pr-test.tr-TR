---
title: "Öğretici: Azure Active Directory Tümleştirme ile Merchlogix | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Merchlogix arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: a1f49bb8-6b17-433d-8f25-9d26fb390e77
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: jeedes
ms.openlocfilehash: bf8d244d9705c06651a65777d6f085b790a5207d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-merchlogix"></a><span data-ttu-id="affdc-103">Öğretici: Azure Active Directory Tümleştirme Merchlogix ile</span><span class="sxs-lookup"><span data-stu-id="affdc-103">Tutorial: Azure Active Directory integration with Merchlogix</span></span>

<span data-ttu-id="affdc-104">Bu öğreticide, bilgi nasıl toointegrate Merchlogix Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="affdc-104">In this tutorial, you learn how toointegrate Merchlogix with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="affdc-105">Merchlogix Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="affdc-105">Integrating Merchlogix with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="affdc-106">Erişim tooMerchlogix sahip Azure AD'de kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="affdc-106">You can control in Azure AD who has access tooMerchlogix.</span></span>
- <span data-ttu-id="affdc-107">Kullanıcıların tooautomatically get açan tooMerchlogix (çoklu oturum açma) Azure AD hesaplarına ile etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="affdc-107">You can enable your users tooautomatically get signed-on tooMerchlogix (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="affdc-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="affdc-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="affdc-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="affdc-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="affdc-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="affdc-110">Prerequisites</span></span>

<span data-ttu-id="affdc-111">tooconfigure Merchlogix ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="affdc-111">tooconfigure Azure AD integration with Merchlogix, you need hello following items:</span></span>

- <span data-ttu-id="affdc-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="affdc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="affdc-113">Bir Merchlogix çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="affdc-113">A Merchlogix single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="affdc-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="affdc-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="affdc-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="affdc-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="affdc-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="affdc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="affdc-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="affdc-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="affdc-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="affdc-118">Scenario description</span></span>
<span data-ttu-id="affdc-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="affdc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="affdc-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="affdc-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="affdc-121">Merhaba Galerisi'nden Merchlogix ekleme</span><span class="sxs-lookup"><span data-stu-id="affdc-121">Adding Merchlogix from hello gallery</span></span>
2. <span data-ttu-id="affdc-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="affdc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-merchlogix-from-hello-gallery"></a><span data-ttu-id="affdc-123">Merhaba Galerisi'nden Merchlogix ekleme</span><span class="sxs-lookup"><span data-stu-id="affdc-123">Adding Merchlogix from hello gallery</span></span>
<span data-ttu-id="affdc-124">Azure AD'ye tooconfigure hello tümleştirme Merchlogix, tooadd Merchlogix hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="affdc-124">tooconfigure hello integration of Merchlogix into Azure AD, you need tooadd Merchlogix from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="affdc-125">**tooadd Merchlogix hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="affdc-125">**tooadd Merchlogix from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="affdc-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="affdc-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory düğmesi][1]

2. <span data-ttu-id="affdc-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="affdc-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="affdc-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="affdc-129">Then go too**All applications**.</span></span>

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="affdc-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="affdc-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Merhaba yeni uygulama düğmesi][3]

4. <span data-ttu-id="affdc-133">Merhaba arama kutusuna yazın **Merchlogix**seçin **Merchlogix** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="affdc-133">In hello search box, type **Merchlogix**, select **Merchlogix** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Merhaba sonuçları listesinde Merchlogix](./media/active-directory-saas-merchlogix-tutorial/tutorial_merchlogix_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="affdc-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="affdc-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="affdc-136">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Merchlogix sınayın.</span><span class="sxs-lookup"><span data-stu-id="affdc-136">In this section, you configure and test Azure AD single sign-on with Merchlogix based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="affdc-137">Tek toowork'ın oturum açma hangi hello karşılık gelen Merchlogix içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="affdc-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Merchlogix is tooa user in Azure AD.</span></span> <span data-ttu-id="affdc-138">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Merchlogix hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="affdc-138">In other words, a link relationship between an Azure AD user and hello related user in Merchlogix needs toobe established.</span></span>

<span data-ttu-id="affdc-139">Merhaba hello değeri Merchlogix içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="affdc-139">In Merchlogix, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="affdc-140">tooconfigure ve Merchlogix ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="affdc-140">tooconfigure and test Azure AD single sign-on with Merchlogix, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="affdc-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="affdc-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="affdc-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="affdc-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="affdc-143">**[Merchlogix test kullanıcısı oluşturma](#create-a-merchlogix-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Merchlogix içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="affdc-143">**[Create a Merchlogix test user](#create-a-merchlogix-test-user)** - toohave a counterpart of Britta Simon in Merchlogix that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="affdc-144">**[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="affdc-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="affdc-145">**[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="affdc-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="affdc-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="affdc-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="affdc-147">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Merchlogix uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="affdc-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Merchlogix application.</span></span>

<span data-ttu-id="affdc-148">**tooconfigure Azure AD çoklu oturum açma ile Merchlogix, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="affdc-148">**tooconfigure Azure AD single sign-on with Merchlogix, perform hello following steps:**</span></span>

1. <span data-ttu-id="affdc-149">Hello hello üzerinde Azure portal'ın **Merchlogix** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="affdc-149">In hello Azure portal, on hello **Merchlogix** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. <span data-ttu-id="affdc-151">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="affdc-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-merchlogix-tutorial/tutorial_merchlogix_samlbase.png)

3. <span data-ttu-id="affdc-153">Merhaba üzerinde **Merchlogix etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="affdc-153">On hello **Merchlogix Domain and URLs** section, perform hello following steps:</span></span>

    ![Merchlogix etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-merchlogix-tutorial/tutorial_merchlogix_url.png)

    <span data-ttu-id="affdc-155">a.</span><span class="sxs-lookup"><span data-stu-id="affdc-155">a.</span></span> <span data-ttu-id="affdc-156">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<DOMAIN>/login.php?saml=true`</span><span class="sxs-lookup"><span data-stu-id="affdc-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<DOMAIN>/login.php?saml=true`</span></span>

    <span data-ttu-id="affdc-157">b.</span><span class="sxs-lookup"><span data-stu-id="affdc-157">b.</span></span> <span data-ttu-id="affdc-158">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<DOMAIN>/simplesaml/module.php/saml/sp/metadata.php/<SAML_NAME>`</span><span class="sxs-lookup"><span data-stu-id="affdc-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<DOMAIN>/simplesaml/module.php/saml/sp/metadata.php/<SAML_NAME>`</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="affdc-159">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="affdc-159">These values are not real.</span></span> <span data-ttu-id="affdc-160">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="affdc-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="affdc-161">Kişi [Merchlogix destek ekibi](http://www.merchlogix.com/contact/) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="affdc-161">Contact [Merchlogix support team](http://www.merchlogix.com/contact/) tooget these values.</span></span>

4. <span data-ttu-id="affdc-162">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="affdc-162">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-merchlogix-tutorial/tutorial_merchlogix_certificate.png) 

5. <span data-ttu-id="affdc-164">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="affdc-164">Click **Save** button.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-merchlogix-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="affdc-166">Merhaba üzerinde **Merchlogix yapılandırma** 'yi tıklatın **yapılandırma Merchlogix** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="affdc-166">On hello **Merchlogix Configuration** section, click **Configure Merchlogix** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="affdc-167">Kopya hello **Sign-Out URL, SAML varlık kimliği** ve **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="affdc-167">Copy hello **Sign-Out URL, SAML Entity ID,** and **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Merchlogix yapılandırma](./media/active-directory-saas-merchlogix-tutorial/tutorial_merchlogix_configure.png) 

7. <span data-ttu-id="affdc-169">tooconfigure çoklu oturum açma üzerinde **Merchlogix** yan, indirilen toosend hello ihtiyacınız **sertifika (Base64)**, **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** çok[Merchlogix destek ekibi](http://www.merchlogix.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="affdc-169">tooconfigure single sign-on on **Merchlogix** side, you need toosend hello downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Merchlogix support team](http://www.merchlogix.com/contact/).</span></span> <span data-ttu-id="affdc-170">Bunlar, bu ayar toohave hello iki tarafta da ayarlamanızı SAML SSO bağlantı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="affdc-170">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="affdc-171">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="affdc-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="affdc-172">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="affdc-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="affdc-173">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="affdc-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="affdc-174">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="affdc-174">Create an Azure AD test user</span></span>

<span data-ttu-id="affdc-175">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="affdc-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="affdc-177">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="affdc-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="affdc-178">Merhaba hello sol bölmede Azure portal hello tıklatın **Azure Active Directory** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="affdc-178">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-merchlogix-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="affdc-180">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="affdc-180">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-merchlogix-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="affdc-182">tooopen hello **kullanıcı** iletişim kutusu, tıklatın **Ekle** hello hello üstündeki **tüm kullanıcılar** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="affdc-182">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Merhaba Ekle düğmesi](./media/active-directory-saas-merchlogix-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="affdc-184">Merhaba, **kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="affdc-184">In hello **User** dialog box, perform hello following steps:</span></span>

    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-merchlogix-tutorial/create_aaduser_04.png)

    <span data-ttu-id="affdc-186">a.</span><span class="sxs-lookup"><span data-stu-id="affdc-186">a.</span></span> <span data-ttu-id="affdc-187">Merhaba, **adı** kutusuna **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="affdc-187">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="affdc-188">b.</span><span class="sxs-lookup"><span data-stu-id="affdc-188">b.</span></span> <span data-ttu-id="affdc-189">Merhaba, **kullanıcı adı** kutusuna, kullanıcının Britta Simon hello e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="affdc-189">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="affdc-190">c.</span><span class="sxs-lookup"><span data-stu-id="affdc-190">c.</span></span> <span data-ttu-id="affdc-191">Select hello **Göster parola** onay kutusunu işaretleyin ve ardından hello görüntülenen hello değerini aşağı yazma **parola** kutusu.</span><span class="sxs-lookup"><span data-stu-id="affdc-191">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="affdc-192">d.</span><span class="sxs-lookup"><span data-stu-id="affdc-192">d.</span></span> <span data-ttu-id="affdc-193">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="affdc-193">Click **Create**.</span></span>
 
### <a name="create-a-merchlogix-test-user"></a><span data-ttu-id="affdc-194">Merchlogix test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="affdc-194">Create a Merchlogix test user</span></span>

<span data-ttu-id="affdc-195">Bu bölümde, Merchlogix içinde Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="affdc-195">In this section, you create a user called Britta Simon in Merchlogix.</span></span> <span data-ttu-id="affdc-196">Çalışmak [Merchlogix destek ekibi](http://www.merchlogix.com/contact/) tooadd hello kullanıcılar hello Merchlogix Platform.</span><span class="sxs-lookup"><span data-stu-id="affdc-196">Work with [Merchlogix support team](http://www.merchlogix.com/contact/) tooadd hello users in hello Merchlogix platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="affdc-197">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="affdc-197">Assign hello Azure AD test user</span></span>

<span data-ttu-id="affdc-198">Bu bölümde, erişim tooMerchlogix vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="affdc-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMerchlogix.</span></span>

![Merhaba kullanıcı rolü atayın][200] 

<span data-ttu-id="affdc-200">**tooassign Britta Simon tooMerchlogix hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="affdc-200">**tooassign Britta Simon tooMerchlogix, perform hello following steps:**</span></span>

1. <span data-ttu-id="affdc-201">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="affdc-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="affdc-203">Merhaba uygulamalar listesinde **Merchlogix**.</span><span class="sxs-lookup"><span data-stu-id="affdc-203">In hello applications list, select **Merchlogix**.</span></span>

    ![Merhaba Merchlogix bağlantı hello uygulamalar listesinde](./media/active-directory-saas-merchlogix-tutorial/tutorial_merchlogix_app.png)  

3. <span data-ttu-id="affdc-205">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="affdc-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202]

4. <span data-ttu-id="affdc-207">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="affdc-207">Click **Add** button.</span></span> <span data-ttu-id="affdc-208">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="affdc-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Merhaba eklemek atama bölmesi][203]

5. <span data-ttu-id="affdc-210">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="affdc-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="affdc-211">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="affdc-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="affdc-212">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="affdc-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="affdc-213">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="affdc-213">Test single sign-on</span></span>

<span data-ttu-id="affdc-214">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="affdc-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="affdc-215">Merhaba Merchlogix hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Merchlogix uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="affdc-215">When you click hello Merchlogix tile in hello Access Panel, you should get automatically signed-on tooyour Merchlogix application.</span></span>
<span data-ttu-id="affdc-216">Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="affdc-216">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="affdc-217">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="affdc-217">Additional resources</span></span>

* [<span data-ttu-id="affdc-218">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="affdc-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="affdc-219">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="affdc-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-merchlogix-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-merchlogix-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-merchlogix-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-merchlogix-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-merchlogix-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-merchlogix-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-merchlogix-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-merchlogix-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-merchlogix-tutorial/tutorial_general_203.png

