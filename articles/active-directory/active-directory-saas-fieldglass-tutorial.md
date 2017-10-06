---
title: "Öğretici: Azure Active Directory Tümleştirme ile Fieldglass | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Fieldglass arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2510195f-d5b1-4684-b3da-283fb8619df2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: d953996bc3bf5721b8280dae4b9992aef7934b3a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-fieldglass"></a><span data-ttu-id="80fe8-103">Öğretici: Azure Active Directory Tümleştirme Fieldglass ile</span><span class="sxs-lookup"><span data-stu-id="80fe8-103">Tutorial: Azure Active Directory integration with Fieldglass</span></span>

<span data-ttu-id="80fe8-104">Bu öğreticide, bilgi nasıl toointegrate Fieldglass Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="80fe8-104">In this tutorial, you learn how toointegrate Fieldglass with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="80fe8-105">Fieldglass Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="80fe8-105">Integrating Fieldglass with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="80fe8-106">Erişim tooFieldglass sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="80fe8-106">You can control in Azure AD who has access tooFieldglass</span></span>
- <span data-ttu-id="80fe8-107">Kullanıcıların tooautomatically get açan tooFieldglass (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="80fe8-107">You can enable your users tooautomatically get signed-on tooFieldglass (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="80fe8-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="80fe8-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="80fe8-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="80fe8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="80fe8-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="80fe8-110">Prerequisites</span></span>

<span data-ttu-id="80fe8-111">tooconfigure Fieldglass ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="80fe8-111">tooconfigure Azure AD integration with Fieldglass, you need hello following items:</span></span>

- <span data-ttu-id="80fe8-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="80fe8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="80fe8-113">Bir Fieldglass çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="80fe8-113">A Fieldglass single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="80fe8-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="80fe8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="80fe8-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="80fe8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="80fe8-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="80fe8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="80fe8-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="80fe8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="80fe8-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="80fe8-118">Scenario description</span></span>
<span data-ttu-id="80fe8-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="80fe8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="80fe8-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="80fe8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="80fe8-121">Merhaba Galerisi'nden Fieldglass ekleme</span><span class="sxs-lookup"><span data-stu-id="80fe8-121">Adding Fieldglass from hello gallery</span></span>
2. <span data-ttu-id="80fe8-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="80fe8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-fieldglass-from-hello-gallery"></a><span data-ttu-id="80fe8-123">Merhaba Galerisi'nden Fieldglass ekleme</span><span class="sxs-lookup"><span data-stu-id="80fe8-123">Adding Fieldglass from hello gallery</span></span>
<span data-ttu-id="80fe8-124">Azure AD'ye tooconfigure hello tümleştirme Fieldglass, tooadd Fieldglass hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="80fe8-124">tooconfigure hello integration of Fieldglass into Azure AD, you need tooadd Fieldglass from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="80fe8-125">**tooadd Fieldglass hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="80fe8-125">**tooadd Fieldglass from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="80fe8-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="80fe8-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="80fe8-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="80fe8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="80fe8-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="80fe8-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="80fe8-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="80fe8-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="80fe8-133">Merhaba arama kutusuna yazın **Fieldglass**.</span><span class="sxs-lookup"><span data-stu-id="80fe8-133">In hello search box, type **Fieldglass**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-fieldglass-tutorial/tutorial_fieldglass_search.png)

5. <span data-ttu-id="80fe8-135">Merhaba Sonuçlar panelinde seçin **Fieldglass**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="80fe8-135">In hello results panel, select **Fieldglass**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-fieldglass-tutorial/tutorial_fieldglass_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="80fe8-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="80fe8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="80fe8-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Fieldglass ile test etme</span><span class="sxs-lookup"><span data-stu-id="80fe8-138">In this section, you configure and test Azure AD single sign-on with Fieldglass based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="80fe8-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Fieldglass içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="80fe8-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Fieldglass is tooa user in Azure AD.</span></span> <span data-ttu-id="80fe8-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Fieldglass hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="80fe8-140">In other words, a link relationship between an Azure AD user and hello related user in Fieldglass needs toobe established.</span></span>

<span data-ttu-id="80fe8-141">Merhaba hello değeri Fieldglass içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="80fe8-141">In Fieldglass, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="80fe8-142">tooconfigure ve Fieldglass ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="80fe8-142">tooconfigure and test Azure AD single sign-on with Fieldglass, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="80fe8-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="80fe8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="80fe8-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="80fe8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="80fe8-145">**[Fieldglass test kullanıcısı oluşturma](#creating-a-fieldglass-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Fieldglass içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="80fe8-145">**[Creating a Fieldglass test user](#creating-a-fieldglass-test-user)** - toohave a counterpart of Britta Simon in Fieldglass that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="80fe8-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="80fe8-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="80fe8-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="80fe8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="80fe8-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="80fe8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="80fe8-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Fieldglass uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="80fe8-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Fieldglass application.</span></span>

<span data-ttu-id="80fe8-150">**tooconfigure Azure AD çoklu oturum açma ile Fieldglass, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="80fe8-150">**tooconfigure Azure AD single sign-on with Fieldglass, perform hello following steps:**</span></span>

1. <span data-ttu-id="80fe8-151">Hello hello üzerinde Azure portal'ın **Fieldglass** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="80fe8-151">In hello Azure portal, on hello **Fieldglass** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="80fe8-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="80fe8-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-fieldglass-tutorial/tutorial_fieldglass_samlbase.png)

3. <span data-ttu-id="80fe8-155">Merhaba üzerinde **Fieldglass etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="80fe8-155">On hello **Fieldglass Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-fieldglass-tutorial/tutorial_fieldglass_url.png)

    <span data-ttu-id="80fe8-157">a.</span><span class="sxs-lookup"><span data-stu-id="80fe8-157">a.</span></span> <span data-ttu-id="80fe8-158">Merhaba, **tanımlayıcısı** metin kutusuna, bir URL türü `https://www.fieldglass.com` veya hello düzeni izleyin:`https://<company name>.fgvms.com`</span><span class="sxs-lookup"><span data-stu-id="80fe8-158">In hello **Identifier** textbox, type a URL as  `https://www.fieldglass.com` or follow hello pattern:  `https://<company name>.fgvms.com`</span></span>

    <span data-ttu-id="80fe8-159">b.</span><span class="sxs-lookup"><span data-stu-id="80fe8-159">b.</span></span> <span data-ttu-id="80fe8-160">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:</span><span class="sxs-lookup"><span data-stu-id="80fe8-160">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://www.fieldglass.net/<company name>`|
    | `https://<company name>.fgvms.com/<company name>`|

    > [!NOTE] 
    > <span data-ttu-id="80fe8-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="80fe8-161">These values are not real.</span></span> <span data-ttu-id="80fe8-162">Bu değerleri hello gerçek tanımlayıcısı ve yanıt URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="80fe8-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="80fe8-163">Kişi [Fieldglass destek ekibi](http://www.fieldglass.com/solutions/support) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="80fe8-163">Contact [Fieldglass support team](http://www.fieldglass.com/solutions/support) tooget these values.</span></span>
 
4. <span data-ttu-id="80fe8-164">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="80fe8-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-fieldglass-tutorial/tutorial_fieldglass_certificate.png) 

5. <span data-ttu-id="80fe8-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="80fe8-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-fieldglass-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="80fe8-168">Merhaba üzerinde **Fieldglass yapılandırma** 'yi tıklatın **yapılandırma Fieldglass** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="80fe8-168">On hello **Fieldglass Configuration** section, click **Configure Fieldglass** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="80fe8-169">Kopya hello **Sign-Out URL ve SAML varlık kimliği** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="80fe8-169">Copy hello **Sign-Out URL and SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-fieldglass-tutorial/tutorial_fieldglass_configure.png) 

7. <span data-ttu-id="80fe8-171">tooconfigure çoklu oturum açma üzerinde **Fieldglass** yan, indirilen toosend hello ihtiyacınız **Certificate(Base64)** ve **Sign-Out URL, SAML varlık kimliği** çok[ Fieldglass destek ekibi](http://www.fieldglass.com/solutions/support).</span><span class="sxs-lookup"><span data-stu-id="80fe8-171">tooconfigure single sign-on on **Fieldglass** side, you need toosend hello downloaded **Certificate(Base64)** and **Sign-Out URL, SAML Entity ID** too[Fieldglass support team](http://www.fieldglass.com/solutions/support).</span></span> <span data-ttu-id="80fe8-172">Bunlar, bu ayar toohave hello iki tarafta da ayarlamanızı SAML SSO bağlantı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="80fe8-172">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="80fe8-173">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="80fe8-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="80fe8-174">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="80fe8-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="80fe8-175">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="80fe8-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="80fe8-176">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="80fe8-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="80fe8-177">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="80fe8-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="80fe8-179">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="80fe8-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="80fe8-180">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="80fe8-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-fieldglass-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="80fe8-182">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="80fe8-182">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-fieldglass-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="80fe8-184">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="80fe8-184">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-fieldglass-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="80fe8-186">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="80fe8-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-fieldglass-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="80fe8-188">a.</span><span class="sxs-lookup"><span data-stu-id="80fe8-188">a.</span></span> <span data-ttu-id="80fe8-189">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="80fe8-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="80fe8-190">b.</span><span class="sxs-lookup"><span data-stu-id="80fe8-190">b.</span></span> <span data-ttu-id="80fe8-191">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="80fe8-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="80fe8-192">c.</span><span class="sxs-lookup"><span data-stu-id="80fe8-192">c.</span></span> <span data-ttu-id="80fe8-193">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="80fe8-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="80fe8-194">d.</span><span class="sxs-lookup"><span data-stu-id="80fe8-194">d.</span></span> <span data-ttu-id="80fe8-195">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="80fe8-195">Click **Create**.</span></span>
 
### <a name="creating-a-fieldglass-test-user"></a><span data-ttu-id="80fe8-196">Fieldglass test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="80fe8-196">Creating a Fieldglass test user</span></span>

<span data-ttu-id="80fe8-197">Bu bölümde Hello amacı toocreate Britta Simon içinde FieldGlass adlı bir kullanıcı ' dir.</span><span class="sxs-lookup"><span data-stu-id="80fe8-197">hello objective of this section is toocreate a user called Britta Simon in FieldGlass.</span></span> <span data-ttu-id="80fe8-198">Lütfen çalışmak, [Fieldglass destek ekibi](http://www.fieldglass.com/solutions/support) tooadd hello hello Fieldglass hesap kullanıcılar.</span><span class="sxs-lookup"><span data-stu-id="80fe8-198">Please work with your [Fieldglass support team](http://www.fieldglass.com/solutions/support) tooadd hello users in hello Fieldglass account.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="80fe8-199">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="80fe8-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="80fe8-200">Bu bölümde, erişim tooFieldglass vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="80fe8-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooFieldglass.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="80fe8-202">**tooassign Britta Simon tooFieldglass hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="80fe8-202">**tooassign Britta Simon tooFieldglass, perform hello following steps:**</span></span>

1. <span data-ttu-id="80fe8-203">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="80fe8-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="80fe8-205">Merhaba uygulamalar listesinde **Fieldglass**.</span><span class="sxs-lookup"><span data-stu-id="80fe8-205">In hello applications list, select **Fieldglass**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-fieldglass-tutorial/tutorial_fieldglass_app.png) 

3. <span data-ttu-id="80fe8-207">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="80fe8-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="80fe8-209">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="80fe8-209">Click **Add** button.</span></span> <span data-ttu-id="80fe8-210">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="80fe8-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="80fe8-212">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="80fe8-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="80fe8-213">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="80fe8-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="80fe8-214">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="80fe8-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="80fe8-215">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="80fe8-215">Testing single sign-on</span></span>

<span data-ttu-id="80fe8-216">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="80fe8-216">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="80fe8-217">Hello erişim paneli Fieldglass döşeme hello tıkladığınızda, otomatik olarak oturum açma Fieldglass uygulama tooyour almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="80fe8-217">When you click hello Fieldglass tile in hello Access Panel, you should get automatically signed-on tooyour Fieldglass application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="80fe8-218">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="80fe8-218">Additional resources</span></span>

* [<span data-ttu-id="80fe8-219">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="80fe8-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="80fe8-220">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="80fe8-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-fieldglass-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-fieldglass-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-fieldglass-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-fieldglass-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-fieldglass-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-fieldglass-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-fieldglass-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-fieldglass-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-fieldglass-tutorial/tutorial_general_203.png

