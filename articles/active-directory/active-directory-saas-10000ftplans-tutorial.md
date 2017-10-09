---
title: "Öğretici: Azure Active Directory Tümleştirme 10.000 ft planına sahip | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve 10.000 ft arasında planlar."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b60c955e-8fa3-4872-a897-c4e81fd7beac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 9aa6fd079da4f931d4dd7277407a07e56091d7c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-10000ft-plans"></a><span data-ttu-id="06feb-103">Öğretici: Azure Active Directory Tümleştirme 10.000 ft planına sahip</span><span class="sxs-lookup"><span data-stu-id="06feb-103">Tutorial: Azure Active Directory integration with 10,000ft Plans</span></span>

<span data-ttu-id="06feb-104">Bu öğreticide, bilgi nasıl toointegrate 10.000 ft planları Azure Active Directory (Azure AD) ile.</span><span class="sxs-lookup"><span data-stu-id="06feb-104">In this tutorial, you learn how toointegrate 10,000ft Plans with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="06feb-105">10.000 ft planları Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="06feb-105">Integrating 10,000ft Plans with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="06feb-106">Erişim too10, 000 ft planları sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="06feb-106">You can control in Azure AD who has access too10,000ft Plans</span></span>
- <span data-ttu-id="06feb-107">Kullanıcıların tooautomatically get açan too10, 000 ft planlarıyla (çoklu oturum açma) Azure AD hesaplarına etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="06feb-107">You can enable your users tooautomatically get signed-on too10,000ft Plans (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="06feb-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="06feb-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="06feb-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="06feb-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="06feb-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="06feb-110">Prerequisites</span></span>

<span data-ttu-id="06feb-111">tooconfigure 10.000 ft planları ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="06feb-111">tooconfigure Azure AD integration with 10,000ft Plans, you need hello following items:</span></span>

- <span data-ttu-id="06feb-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="06feb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="06feb-113">Bir 10.000 ft planları çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="06feb-113">A 10,000ft Plans single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="06feb-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="06feb-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="06feb-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="06feb-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="06feb-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="06feb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="06feb-117">Bir Azure AD deneme ortam yoksa, burada bir aylık deneme alabilirsiniz [deneme teklifi](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="06feb-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="06feb-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="06feb-118">Scenario description</span></span>
<span data-ttu-id="06feb-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="06feb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="06feb-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="06feb-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="06feb-121">Merhaba Galerisi'nden planları 10.000 ft ekleme</span><span class="sxs-lookup"><span data-stu-id="06feb-121">Adding 10,000ft Plans from hello gallery</span></span>
2. <span data-ttu-id="06feb-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="06feb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-10000ft-plans-from-hello-gallery"></a><span data-ttu-id="06feb-123">Merhaba Galerisi'nden planları 10.000 ft ekleme</span><span class="sxs-lookup"><span data-stu-id="06feb-123">Adding 10,000ft Plans from hello gallery</span></span>
<span data-ttu-id="06feb-124">Azure AD'ye tooconfigure hello tümleştirme 10.000 ft planlardan tooadd ihtiyacınız 10.000 ft planları hello galeri tooyour listesinden yönetilen SaaS uygulamaları.</span><span class="sxs-lookup"><span data-stu-id="06feb-124">tooconfigure hello integration of 10,000ft Plans into Azure AD, you need tooadd 10,000ft Plans from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="06feb-125">**Merhaba Galerisi'nden tooadd 10.000 ft planları, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="06feb-125">**tooadd 10,000ft Plans from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="06feb-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="06feb-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="06feb-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="06feb-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="06feb-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="06feb-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="06feb-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="06feb-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="06feb-133">Merhaba arama kutusuna yazın **10.000 ft planları**.</span><span class="sxs-lookup"><span data-stu-id="06feb-133">In hello search box, type **10,000ft Plans**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_search.png)

5. <span data-ttu-id="06feb-135">Merhaba Sonuçlar panelinde seçin **10.000 ft planları**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="06feb-135">In hello results panel, select **10,000ft Plans**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="06feb-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="06feb-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="06feb-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma 10.000 ft "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı planları ile test etme</span><span class="sxs-lookup"><span data-stu-id="06feb-138">In this section, you configure and test Azure AD single sign-on with 10,000ft Plans based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="06feb-139">Tek toowork'ın oturum açma hangi hello karşılık gelen 10.000 ft planlarda tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="06feb-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in 10,000ft Plans is tooa user in Azure AD.</span></span> <span data-ttu-id="06feb-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı 10.000 ft hello arasında bir bağlantı ilişkisi planları gerekiyor toobe kuruldu.</span><span class="sxs-lookup"><span data-stu-id="06feb-140">In other words, a link relationship between an Azure AD user and hello related user in 10,000ft Plans needs toobe established.</span></span>

<span data-ttu-id="06feb-141">10.000 ft planlarda hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="06feb-141">In 10,000ft Plans, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="06feb-142">tooconfigure ve 10.000 ft planları ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="06feb-142">tooconfigure and test Azure AD single sign-on with 10,000ft Plans, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="06feb-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="06feb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="06feb-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="06feb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="06feb-145">**[Kullanıcı test planları 10.000 ft oluşturma](#creating-a-10000ft-plans-test-user)**  -bir Britta Simon karşılık gelen 10.000 ft içinde planları diğer bir deyişle toohave bağlı toohello Azure AD kullanıcı gösterimi.</span><span class="sxs-lookup"><span data-stu-id="06feb-145">**[Creating a 10,000ft Plans test user](#creating-a-10000ft-plans-test-user)** - toohave a counterpart of Britta Simon in 10,000ft Plans that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="06feb-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="06feb-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="06feb-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="06feb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="06feb-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="06feb-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="06feb-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma 10.000 ft planları uygulamanızı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="06feb-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your 10,000ft Plans application.</span></span>

<span data-ttu-id="06feb-150">**tooconfigure Azure AD çoklu oturum açma 10.000 ft planına sahip hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="06feb-150">**tooconfigure Azure AD single sign-on with 10,000ft Plans, perform hello following steps:**</span></span>

1. <span data-ttu-id="06feb-151">Merhaba hello üzerinde Azure portal'ın **10.000 ft planları** uygulama tümleştirmesi sayfasında, tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="06feb-151">In hello Azure portal, on hello **10,000ft Plans** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="06feb-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="06feb-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_samlbase.png)

3. <span data-ttu-id="06feb-155">Merhaba üzerinde **10.000 ft planları etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="06feb-155">On hello **10,000ft Plans Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_url.png)

    <span data-ttu-id="06feb-157">a.</span><span class="sxs-lookup"><span data-stu-id="06feb-157">a.</span></span> <span data-ttu-id="06feb-158">Merhaba, **oturum açma URL'si** metin kutusuna, türü hello URL'si:`https://app.10000ft.com`</span><span class="sxs-lookup"><span data-stu-id="06feb-158">In hello **Sign-on URL** textbox, type hello URL: `https://app.10000ft.com`</span></span>

    <span data-ttu-id="06feb-159">b.</span><span class="sxs-lookup"><span data-stu-id="06feb-159">b.</span></span> <span data-ttu-id="06feb-160">Merhaba, **tanımlayıcısı** metin kutusuna, türü hello URL'si:`https://app.10000ft.com/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="06feb-160">In hello **Identifier** textbox, type hello URL: `https://app.10000ft.com/saml/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="06feb-161">Merhaba değeri **tanımlayıcısı** özel bir etki alanı varsa farklıdır.</span><span class="sxs-lookup"><span data-stu-id="06feb-161">hello value for **Identifier** is different if you have a custom domain.</span></span> <span data-ttu-id="06feb-162">Kişi [10.000 ft planları destek ekibi](https://www.10000ft.com/plans/support) tooget bu değer.</span><span class="sxs-lookup"><span data-stu-id="06feb-162">Contact [10,000ft Plans support team](https://www.10000ft.com/plans/support) tooget this value.</span></span> 
 
4. <span data-ttu-id="06feb-163">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Raw)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="06feb-163">On hello **SAML Signing Certificate** section, click **Certificate(Raw)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_certificate.png) 

5. <span data-ttu-id="06feb-165">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="06feb-165">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="06feb-167">Merhaba üzerinde **10.000 ft planları yapılandırma** 'yi tıklatın **yapılandırma 10.000 ft planları** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="06feb-167">On hello **10,000ft Plans Configuration** section, click **Configure 10,000ft Plans** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="06feb-168">Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="06feb-168">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_configure.png) 

7. <span data-ttu-id="06feb-170">tooconfigure çoklu oturum açma üzerinde **10.000 ft planları** yan, indirilen toosend hello ihtiyacınız **Certificate(Raw), Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** çok[ 10.000 ft planları destek ekibi](https://www.10000ft.com/plans/support).</span><span class="sxs-lookup"><span data-stu-id="06feb-170">tooconfigure single sign-on on **10,000ft Plans** side, you need toosend hello downloaded **Certificate(Raw), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[10,000ft Plans support team](https://www.10000ft.com/plans/support).</span></span>

> [!TIP]
> <span data-ttu-id="06feb-171">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="06feb-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="06feb-172">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="06feb-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="06feb-173">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="06feb-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="06feb-174">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="06feb-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="06feb-175">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="06feb-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="06feb-177">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="06feb-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="06feb-178">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="06feb-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="06feb-180">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="06feb-180">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="06feb-182">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="06feb-182">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="06feb-184">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="06feb-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="06feb-186">a.</span><span class="sxs-lookup"><span data-stu-id="06feb-186">a.</span></span> <span data-ttu-id="06feb-187">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="06feb-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="06feb-188">b.</span><span class="sxs-lookup"><span data-stu-id="06feb-188">b.</span></span> <span data-ttu-id="06feb-189">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="06feb-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="06feb-190">c.</span><span class="sxs-lookup"><span data-stu-id="06feb-190">c.</span></span> <span data-ttu-id="06feb-191">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="06feb-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="06feb-192">d.</span><span class="sxs-lookup"><span data-stu-id="06feb-192">d.</span></span> <span data-ttu-id="06feb-193">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="06feb-193">Click **Create**.</span></span>
 
### <a name="creating-a-10000ft-plans-test-user"></a><span data-ttu-id="06feb-194">Kullanıcı test planları 10.000 ft oluşturma</span><span class="sxs-lookup"><span data-stu-id="06feb-194">Creating a 10,000ft Plans test user</span></span>

<span data-ttu-id="06feb-195">Bu bölümde Hello amacı toocreate Britta Simon 10.000 ft planlarda adlı bir kullanıcı var.</span><span class="sxs-lookup"><span data-stu-id="06feb-195">hello objective of this section is toocreate a user called Britta Simon in 10,000ft Plans.</span></span> <span data-ttu-id="06feb-196">10.000 ft planları yalnızca zaman kaynak sağlamayı destekler, varsayılan olarak etkin olduğu.</span><span class="sxs-lookup"><span data-stu-id="06feb-196">10,000ft Plans supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="06feb-197">Bu bölümde, eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="06feb-197">There is no action item for you in this section.</span></span> <span data-ttu-id="06feb-198">Henüz yoksa yeni bir kullanıcı bir girişim tooaccess 10.000 ft planları sırasında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="06feb-198">A new user is created during an attempt tooaccess 10,000ft Plans if it doesn't exist yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="06feb-199">Toocreate kullanıcı el ile gerekiyorsa, toocontact hello gereksinim [10.000 ft planları destek ekibi](https://www.10000ft.com/plans/support).</span><span class="sxs-lookup"><span data-stu-id="06feb-199">If you need toocreate a user manually, you need toocontact hello [10,000ft Plans support team](https://www.10000ft.com/plans/support).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="06feb-200">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="06feb-200">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="06feb-201">Bu bölümde, erişim too10, 000 ft planları vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="06feb-201">In this section, you enable Britta Simon toouse Azure single sign-on by granting access too10,000ft Plans.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="06feb-203">**tooassign Britta Simon too10 000ft planları hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="06feb-203">**tooassign Britta Simon too10,000ft Plans, perform hello following steps:**</span></span>

1. <span data-ttu-id="06feb-204">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="06feb-204">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="06feb-206">Merhaba uygulamalar listesinde **10.000 ft planları**.</span><span class="sxs-lookup"><span data-stu-id="06feb-206">In hello applications list, select **10,000ft Plans**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_app.png) 

3. <span data-ttu-id="06feb-208">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="06feb-208">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="06feb-210">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="06feb-210">Click **Add** button.</span></span> <span data-ttu-id="06feb-211">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="06feb-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="06feb-213">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="06feb-213">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="06feb-214">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="06feb-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="06feb-215">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="06feb-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="06feb-216">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="06feb-216">Testing single sign-on</span></span>

<span data-ttu-id="06feb-217">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="06feb-217">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="06feb-218">Merhaba 10.000 planları hello erişim paneli döşeme ft tıkladığınızda, otomatik olarak oturum açma tooyour 10.000 ft planları uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="06feb-218">When you click hello 10,000ft Plans tile in hello Access Panel, you should get automatically signed-on tooyour 10,000ft Plans application.</span></span>
 
## <a name="additional-resources"></a><span data-ttu-id="06feb-219">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="06feb-219">Additional resources</span></span>

* [<span data-ttu-id="06feb-220">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="06feb-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="06feb-221">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="06feb-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_203.png

