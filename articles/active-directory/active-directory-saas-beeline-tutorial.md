---
title: "Öğretici: Azure Active Directory Tümleştirme ile BeeLine | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile BeeLine arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0726859d-1dac-44a0-810b-da56d89039ee
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 92f228d33980c21ad934185ab89d73795f7f69bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-beeline"></a><span data-ttu-id="0dc01-103">Öğretici: Azure Active Directory Tümleştirme BeeLine ile</span><span class="sxs-lookup"><span data-stu-id="0dc01-103">Tutorial: Azure Active Directory integration with BeeLine</span></span>

<span data-ttu-id="0dc01-104">Bu öğreticide, bilgi nasıl toointegrate BeeLine Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0dc01-104">In this tutorial, you learn how toointegrate BeeLine with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0dc01-105">BeeLine Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="0dc01-105">Integrating BeeLine with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0dc01-106">Erişim tooBeeLine sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="0dc01-106">You can control in Azure AD who has access tooBeeLine</span></span>
- <span data-ttu-id="0dc01-107">Kullanıcıların tooautomatically get açan tooBeeLine (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="0dc01-107">You can enable your users tooautomatically get signed-on tooBeeLine (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0dc01-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="0dc01-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0dc01-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0dc01-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0dc01-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="0dc01-110">Prerequisites</span></span>

<span data-ttu-id="0dc01-111">tooconfigure BeeLine ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="0dc01-111">tooconfigure Azure AD integration with BeeLine, you need hello following items:</span></span>

- <span data-ttu-id="0dc01-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="0dc01-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0dc01-113">Bir BeeLine çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="0dc01-113">A BeeLine single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0dc01-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="0dc01-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0dc01-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="0dc01-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0dc01-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="0dc01-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0dc01-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0dc01-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0dc01-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="0dc01-118">Scenario description</span></span>
<span data-ttu-id="0dc01-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="0dc01-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0dc01-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="0dc01-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0dc01-121">Merhaba Galerisi'nden BeeLine ekleme</span><span class="sxs-lookup"><span data-stu-id="0dc01-121">Adding BeeLine from hello gallery</span></span>
2. <span data-ttu-id="0dc01-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="0dc01-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-beeline-from-hello-gallery"></a><span data-ttu-id="0dc01-123">Merhaba Galerisi'nden BeeLine ekleme</span><span class="sxs-lookup"><span data-stu-id="0dc01-123">Adding BeeLine from hello gallery</span></span>
<span data-ttu-id="0dc01-124">Azure AD'ye tooconfigure hello tümleştirme BeeLine, tooadd BeeLine hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="0dc01-124">tooconfigure hello integration of BeeLine into Azure AD, you need tooadd BeeLine from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0dc01-125">**tooadd BeeLine hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0dc01-125">**tooadd BeeLine from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0dc01-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="0dc01-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0dc01-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="0dc01-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0dc01-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="0dc01-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="0dc01-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="0dc01-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="0dc01-133">Merhaba arama kutusuna yazın **BeeLine**.</span><span class="sxs-lookup"><span data-stu-id="0dc01-133">In hello search box, type **BeeLine**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_search.png)

5. <span data-ttu-id="0dc01-135">Merhaba Sonuçlar panelinde seçin **BeeLine**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="0dc01-135">In hello results panel, select **BeeLine**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0dc01-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="0dc01-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0dc01-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı BeeLine ile test etme</span><span class="sxs-lookup"><span data-stu-id="0dc01-138">In this section, you configure and test Azure AD single sign-on with BeeLine based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0dc01-139">Tek toowork'ın oturum açma hangi hello karşılık gelen BeeLine içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="0dc01-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BeeLine is tooa user in Azure AD.</span></span> <span data-ttu-id="0dc01-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı BeeLine hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="0dc01-140">In other words, a link relationship between an Azure AD user and hello related user in BeeLine needs toobe established.</span></span>

<span data-ttu-id="0dc01-141">Merhaba hello değeri BeeLine içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="0dc01-141">In BeeLine, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0dc01-142">tooconfigure ve BeeLine ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="0dc01-142">tooconfigure and test Azure AD single sign-on with BeeLine, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0dc01-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="0dc01-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0dc01-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="0dc01-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0dc01-145">**[BeeLine test kullanıcısı oluşturma](#creating-a-beeline-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir BeeLine içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="0dc01-145">**[Creating a BeeLine test user](#creating-a-beeline-test-user)** - toohave a counterpart of Britta Simon in BeeLine that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0dc01-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="0dc01-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0dc01-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="0dc01-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0dc01-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0dc01-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0dc01-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma BeeLine uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="0dc01-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BeeLine application.</span></span>

<span data-ttu-id="0dc01-150">**tooconfigure Azure AD çoklu oturum açma ile BeeLine, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0dc01-150">**tooconfigure Azure AD single sign-on with BeeLine, perform hello following steps:**</span></span>

1. <span data-ttu-id="0dc01-151">Hello hello üzerinde Azure portal'ın **BeeLine** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="0dc01-151">In hello Azure portal, on hello **BeeLine** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="0dc01-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="0dc01-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_samlbase.png)

3. <span data-ttu-id="0dc01-155">Merhaba üzerinde **BeeLine etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="0dc01-155">On hello **BeeLine Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_url.png)

    <span data-ttu-id="0dc01-157">a.</span><span class="sxs-lookup"><span data-stu-id="0dc01-157">a.</span></span> <span data-ttu-id="0dc01-158">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://projects.beeline.net/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="0dc01-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://projects.beeline.net/<instancename>`</span></span>

    <span data-ttu-id="0dc01-159">b.</span><span class="sxs-lookup"><span data-stu-id="0dc01-159">b.</span></span> <span data-ttu-id="0dc01-160">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:</span><span class="sxs-lookup"><span data-stu-id="0dc01-160">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://projects.beeline.net/<instancename>/SSO_External.ashx`|
    | `https://projects.beeline.net/<companyname>/SSO_External.ashx` |

    > [!NOTE] 
    > <span data-ttu-id="0dc01-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="0dc01-161">These values are not real.</span></span> <span data-ttu-id="0dc01-162">Bu değerleri hello gerçek tanımlayıcısı ve yanıt URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="0dc01-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="0dc01-163">Kişi [BeeLine destek ekibi](https://www.beeline.com/contact-us/) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="0dc01-163">Contact [BeeLine support team](https://www.beeline.com/contact-us/) tooget these values.</span></span>
 
4. <span data-ttu-id="0dc01-164">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="0dc01-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_certificate.png) 

5. <span data-ttu-id="0dc01-166">Beeline uygulamanızı belirli bir biçimde hello SAML onaylar bekliyor.</span><span class="sxs-lookup"><span data-stu-id="0dc01-166">Your Beeline application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="0dc01-167">Lütfen çalışmak [BeeLine destek ekibi](https://www.beeline.com/contact-us/) ilk tooidentify hello hello uygulamasına eşlenen doğru kullanıcı tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="0dc01-167">Please work with [BeeLine support team](https://www.beeline.com/contact-us/) first tooidentify hello correct user identifier which will be mapped into hello application.</span></span> <span data-ttu-id="0dc01-168">Ayrıca Lütfen hello rehberliği almak [BeeLine destek ekibi](https://www.beeline.com/contact-us/) hello hakkında öznitelik Bu eşleme için toouse istedikleri.</span><span class="sxs-lookup"><span data-stu-id="0dc01-168">Also please take hello guidance from [BeeLine support team](https://www.beeline.com/contact-us/) about hello attribute which they want toouse for this mapping.</span></span> <span data-ttu-id="0dc01-169">Merhaba bu özniteliğin değeri, hello yönetebilirsiniz **kullanıcı öznitelikleri** hello uygulama sekmesinde.</span><span class="sxs-lookup"><span data-stu-id="0dc01-169">You can manage hello value of this attribute from hello **User Attributes** tab of hello application.</span></span> <span data-ttu-id="0dc01-170">Ekran aşağıdaki hello bunun bir örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="0dc01-170">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="0dc01-171">Burada size hello eşledikten **kullanıcı tanımlayıcısı** ile Merhaba talep **userprincipalname** her başarılı SAML gönderilen toohello Beeline hello uygulamada olacak benzersiz kullanıcı Kimliğini sağlar özniteliği Yanıt.</span><span class="sxs-lookup"><span data-stu-id="0dc01-171">Here we have mapped hello **User Identifier** claim with hello **userprincipalname** attribute, which provides unique user ID, which will be sent toohello Beeline application in hello every successful SAML Response.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-beeline-tutorial/tutorial_attribute.png)  

6. <span data-ttu-id="0dc01-173">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="0dc01-173">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-beeline-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="0dc01-175">Merhaba üzerinde **BeeLine yapılandırma** 'yi tıklatın **yapılandırma BeeLine** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="0dc01-175">On hello **BeeLine Configuration** section, click **Configure BeeLine** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="0dc01-176">Kopya hello **Sign-Out URL** ve **SAML varlık kimliği** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="0dc01-176">Copy hello **Sign-Out URL** and **SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_configure.png) 

8. <span data-ttu-id="0dc01-178">tooconfigure çoklu oturum açma üzerinde **BeeLine** yan, indirilen toosend hello ihtiyacınız **meta veri XML** ve **SAML varlık kimliği**, **Sign-Out URL**çok[BeeLine destek ekibi](https://www.beeline.com/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="0dc01-178">tooconfigure single sign-on on **BeeLine** side, you need toosend hello downloaded **Metadata XML** and **SAML Entity ID**, **Sign-Out URL** too[BeeLine support team](https://www.beeline.com/contact-us/).</span></span>

> [!TIP]
> <span data-ttu-id="0dc01-179">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="0dc01-179">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0dc01-180">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="0dc01-180">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0dc01-181">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0dc01-181">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0dc01-182">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="0dc01-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="0dc01-183">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="0dc01-183">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="0dc01-185">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0dc01-185">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0dc01-186">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="0dc01-186">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-beeline-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0dc01-188">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="0dc01-188">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-beeline-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0dc01-190">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="0dc01-190">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-beeline-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0dc01-192">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="0dc01-192">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-beeline-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0dc01-194">a.</span><span class="sxs-lookup"><span data-stu-id="0dc01-194">a.</span></span> <span data-ttu-id="0dc01-195">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0dc01-195">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0dc01-196">b.</span><span class="sxs-lookup"><span data-stu-id="0dc01-196">b.</span></span> <span data-ttu-id="0dc01-197">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="0dc01-197">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0dc01-198">c.</span><span class="sxs-lookup"><span data-stu-id="0dc01-198">c.</span></span> <span data-ttu-id="0dc01-199">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="0dc01-199">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0dc01-200">d.</span><span class="sxs-lookup"><span data-stu-id="0dc01-200">d.</span></span> <span data-ttu-id="0dc01-201">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0dc01-201">Click **Create**.</span></span>
 
### <a name="creating-a-beeline-test-user"></a><span data-ttu-id="0dc01-202">BeeLine test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="0dc01-202">Creating a BeeLine test user</span></span>

<span data-ttu-id="0dc01-203">Bu bölümde, Beeline içinde Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0dc01-203">In this section, you create a user called Britta Simon in Beeline.</span></span> <span data-ttu-id="0dc01-204">Çoklu oturum açma işleminden önce hello uygulamada sağlanan tüm hello kullanıcılar toobe beeline uygulama gerekir.</span><span class="sxs-lookup"><span data-stu-id="0dc01-204">Beeline application needs all hello users toobe provisioned in hello application before doing Single Sign On.</span></span> <span data-ttu-id="0dc01-205">Böylece iş hello ile [BeeLine destek ekibi](https://www.beeline.com/contact-us/) tooprovision bu kullanıcılar hello uygulamaya.</span><span class="sxs-lookup"><span data-stu-id="0dc01-205">So work with hello [BeeLine support team](https://www.beeline.com/contact-us/) tooprovision all these users into hello application.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0dc01-206">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="0dc01-206">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0dc01-207">Bu bölümde, erişim tooBeeLine vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="0dc01-207">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBeeLine.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="0dc01-209">**tooassign Britta Simon tooBeeLine hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0dc01-209">**tooassign Britta Simon tooBeeLine, perform hello following steps:**</span></span>

1. <span data-ttu-id="0dc01-210">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="0dc01-210">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="0dc01-212">Merhaba uygulamalar listesinde **BeeLine**.</span><span class="sxs-lookup"><span data-stu-id="0dc01-212">In hello applications list, select **BeeLine**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_app.png) 

3. <span data-ttu-id="0dc01-214">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="0dc01-214">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="0dc01-216">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="0dc01-216">Click **Add** button.</span></span> <span data-ttu-id="0dc01-217">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="0dc01-217">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="0dc01-219">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="0dc01-219">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0dc01-220">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="0dc01-220">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0dc01-221">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="0dc01-221">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0dc01-222">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="0dc01-222">Testing single sign-on</span></span>

<span data-ttu-id="0dc01-223">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="0dc01-223">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span> <span data-ttu-id="0dc01-224">Merhaba Beeline hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Beeline uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0dc01-224">When you click hello Beeline tile in hello Access Panel, you should get automatically signed-on tooyour Beeline application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0dc01-225">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="0dc01-225">Additional resources</span></span>

* [<span data-ttu-id="0dc01-226">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="0dc01-226">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0dc01-227">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="0dc01-227">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_203.png

