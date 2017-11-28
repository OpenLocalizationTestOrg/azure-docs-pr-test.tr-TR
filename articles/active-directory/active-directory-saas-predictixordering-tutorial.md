---
title: "Öğretici: Azure Active Directory Tümleştirme Predictix sıralama ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory arasındaki Predictix sıralama."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 2fe2f976-e97f-4368-9695-3e1624409e8b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 0418ef24d7942b6b751c0b4d64e7bd1fba1d6a56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-predictix-ordering"></a><span data-ttu-id="fbe29-103">Öğretici: Azure Active Directory Tümleştirme ile Predictix sıralama</span><span class="sxs-lookup"><span data-stu-id="fbe29-103">Tutorial: Azure Active Directory integration with Predictix Ordering</span></span>

<span data-ttu-id="fbe29-104">Bu öğreticide, bilgi nasıl toointegrate Predictix sıralama Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fbe29-104">In this tutorial, you learn how toointegrate Predictix Ordering with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fbe29-105">Azure AD ile tümleştirme Predictix sıralama ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="fbe29-105">Integrating Predictix Ordering with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="fbe29-106">Erişim tooPredictix sahip Azure AD'de Denetim sıralama.</span><span class="sxs-lookup"><span data-stu-id="fbe29-106">You can control in Azure AD who has access tooPredictix Ordering.</span></span>
- <span data-ttu-id="fbe29-107">Oturum açma, kullanıcıların tooautomatically get tooPredictix etkinleştirebilirsiniz sıralama (çoklu oturum açma) Azure AD hesaplarına sahip.</span><span class="sxs-lookup"><span data-stu-id="fbe29-107">You can enable your users tooautomatically get signed-on tooPredictix Ordering (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="fbe29-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="fbe29-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="fbe29-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fbe29-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fbe29-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="fbe29-110">Prerequisites</span></span>

<span data-ttu-id="fbe29-111">tooconfigure Predictix sıralama ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="fbe29-111">tooconfigure Azure AD integration with Predictix Ordering, you need hello following items:</span></span>

- <span data-ttu-id="fbe29-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="fbe29-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fbe29-113">Bir Predictix sıralama çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="fbe29-113">A Predictix Ordering single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fbe29-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="fbe29-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fbe29-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="fbe29-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fbe29-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="fbe29-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fbe29-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fbe29-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fbe29-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="fbe29-118">Scenario description</span></span>
<span data-ttu-id="fbe29-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="fbe29-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fbe29-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="fbe29-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fbe29-121">Predictix sıralama hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="fbe29-121">Adding Predictix Ordering from hello gallery</span></span>
2. <span data-ttu-id="fbe29-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="fbe29-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-predictix-ordering-from-hello-gallery"></a><span data-ttu-id="fbe29-123">Predictix sıralama hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="fbe29-123">Adding Predictix Ordering from hello gallery</span></span>
<span data-ttu-id="fbe29-124">Azure AD'ye tooconfigure hello tümleştirme Predictix sipariş tooadd Predictix sıralama hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="fbe29-124">tooconfigure hello integration of Predictix Ordering into Azure AD, you need tooadd Predictix Ordering from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="fbe29-125">**tooadd Predictix sıralama hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="fbe29-125">**tooadd Predictix Ordering from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="fbe29-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="fbe29-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory düğmesi][1]

2. <span data-ttu-id="fbe29-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="fbe29-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="fbe29-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="fbe29-129">Then go too**All applications**.</span></span>

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="fbe29-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="fbe29-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Merhaba yeni uygulama düğmesi][3]

4. <span data-ttu-id="fbe29-133">Merhaba arama kutusuna yazın **Predictix sıralama**seçin **Predictix sıralama** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="fbe29-133">In hello search box, type **Predictix Ordering**, select **Predictix Ordering** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Predictix sıralama hello sonuçları listesinde](./media/active-directory-saas-predictixordering-tutorial/tutorial_predictixordering_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="fbe29-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="fbe29-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="fbe29-136">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Predictix sıralama ile test etme.</span><span class="sxs-lookup"><span data-stu-id="fbe29-136">In this section, you configure and test Azure AD single sign-on with Predictix Ordering based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fbe29-137">Tek toowork'ın oturum açma hangi hello karşılık gelen Predictix sıralama içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="fbe29-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Predictix Ordering is tooa user in Azure AD.</span></span> <span data-ttu-id="fbe29-138">Diğer bir deyişle, bir Azure AD kullanıcısının ve hello ilgili kullanıcı Predictix sıralama arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="fbe29-138">In other words, a link relationship between an Azure AD user and hello related user in Predictix Ordering needs toobe established.</span></span>

<span data-ttu-id="fbe29-139">Predictix sıralamada hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="fbe29-139">In Predictix Ordering, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="fbe29-140">tooconfigure ve Predictix sıralama ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="fbe29-140">tooconfigure and test Azure AD single sign-on with Predictix Ordering, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="fbe29-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="fbe29-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="fbe29-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="fbe29-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fbe29-143">**[Predictix sıralama test kullanıcısı oluşturma](#create-a-predictix-ordering-test-user)**  -toohave Britta Simon Predictix bağlantılı toohello Azure AD kullanıcı gösterimi olan sıralama içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="fbe29-143">**[Create a Predictix Ordering test user](#create-a-predictix-ordering-test-user)** - toohave a counterpart of Britta Simon in Predictix Ordering that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="fbe29-144">**[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="fbe29-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fbe29-145">**[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="fbe29-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="fbe29-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="fbe29-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="fbe29-147">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Predictix sıralama uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="fbe29-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Predictix Ordering application.</span></span>

<span data-ttu-id="fbe29-148">**tooconfigure Azure AD çoklu oturum açma Predictix sıralama ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="fbe29-148">**tooconfigure Azure AD single sign-on with Predictix Ordering, perform hello following steps:**</span></span>

1. <span data-ttu-id="fbe29-149">Hello hello üzerinde Azure portal'ın **Predictix sıralama** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="fbe29-149">In hello Azure portal, on hello **Predictix Ordering** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. <span data-ttu-id="fbe29-151">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="fbe29-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-predictixordering-tutorial/tutorial_predictixordering_samlbase.png)

3. <span data-ttu-id="fbe29-153">Merhaba üzerinde **Predictix sıralama etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="fbe29-153">On hello **Predictix Ordering Domain and URLs** section, perform hello following steps:</span></span>

    ![Predictix sıralama etki alanı ve URL'leri tek oturum açma bilgilerini](./media/active-directory-saas-predictixordering-tutorial/tutorial_predictixordering_url.png)

    <span data-ttu-id="fbe29-155">a.</span><span class="sxs-lookup"><span data-stu-id="fbe29-155">a.</span></span> <span data-ttu-id="fbe29-156">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname-pricing>.ordering.predictix.com/sso/request`</span><span class="sxs-lookup"><span data-stu-id="fbe29-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname-pricing>.ordering.predictix.com/sso/request`</span></span>

    <span data-ttu-id="fbe29-157">b.</span><span class="sxs-lookup"><span data-stu-id="fbe29-157">b.</span></span> <span data-ttu-id="fbe29-158">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:</span><span class="sxs-lookup"><span data-stu-id="fbe29-158">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span> 
    | |
    |--|
    | `https://<companyname-pricing>.dev.ordering.predictix.com` |
    | `https://<companyname-pricing>.ordering.predictix.com` |

    > [!NOTE] 
    > <span data-ttu-id="fbe29-159">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="fbe29-159">These values are not real.</span></span> <span data-ttu-id="fbe29-160">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="fbe29-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="fbe29-161">Kişi [Predictix sıralama istemci destek ekibi](https://www.predix.io/support/) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="fbe29-161">Contact [Predictix Ordering Client support team](https://www.predix.io/support/) tooget these values.</span></span> 
 
4. <span data-ttu-id="fbe29-162">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="fbe29-162">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-predictixordering-tutorial/tutorial_predictixordering_certificate.png) 

5. <span data-ttu-id="fbe29-164">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="fbe29-164">Click **Save** button.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-predictixordering-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="fbe29-166">Merhaba üzerinde **Predictix sıralama yapılandırma** 'yi tıklatın **yapılandırma Predictix sıralama** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="fbe29-166">On hello **Predictix Ordering Configuration** section, click **Configure Predictix Ordering** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="fbe29-167">Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="fbe29-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Predictix sıralama yapılandırma](./media/active-directory-saas-predictixordering-tutorial/tutorial_predictixordering_configure.png) 

7. <span data-ttu-id="fbe29-169">tooconfigure çoklu oturum açma üzerinde **Predictix sıralama** yan, indirilen toosend hello ihtiyacınız **sertifika (Base64)**, **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si**  çok[Predictix sıralama destek ekibi](https://www.predix.io/support/).</span><span class="sxs-lookup"><span data-stu-id="fbe29-169">tooconfigure single sign-on on **Predictix Ordering** side, you need toosend hello downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Predictix Ordering support team](https://www.predix.io/support/).</span></span> <span data-ttu-id="fbe29-170">Bunlar, bu ayar toohave hello iki tarafta da ayarlamanızı SAML SSO bağlantı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="fbe29-170">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="fbe29-171">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="fbe29-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="fbe29-172">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="fbe29-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="fbe29-173">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fbe29-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="fbe29-174">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="fbe29-174">Create an Azure AD test user</span></span>
<span data-ttu-id="fbe29-175">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="fbe29-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="fbe29-177">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="fbe29-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="fbe29-178">Merhaba hello sol bölmede Azure portal hello tıklatın **Azure Active Directory** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="fbe29-178">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-predictixordering-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="fbe29-180">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="fbe29-180">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-predictixordering-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="fbe29-182">tooopen hello **kullanıcı** iletişim kutusu, tıklatın **Ekle** hello hello üstündeki **tüm kullanıcılar** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="fbe29-182">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Merhaba Ekle düğmesi](./media/active-directory-saas-predictixordering-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="fbe29-184">Merhaba, **kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="fbe29-184">In hello **User** dialog box, perform hello following steps:</span></span>

    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-predictixordering-tutorial/create_aaduser_04.png)

   <span data-ttu-id="fbe29-186">a.</span><span class="sxs-lookup"><span data-stu-id="fbe29-186">a.</span></span> <span data-ttu-id="fbe29-187">Merhaba, **adı** kutusuna **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fbe29-187">In hello **Name** box, type **BrittaSimon**.</span></span>

   <span data-ttu-id="fbe29-188">b.</span><span class="sxs-lookup"><span data-stu-id="fbe29-188">b.</span></span> <span data-ttu-id="fbe29-189">Merhaba, **kullanıcı adı** kutusuna, kullanıcının Britta Simon hello e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="fbe29-189">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

   <span data-ttu-id="fbe29-190">c.</span><span class="sxs-lookup"><span data-stu-id="fbe29-190">c.</span></span> <span data-ttu-id="fbe29-191">Select hello **Göster parola** onay kutusunu işaretleyin ve ardından hello görüntülenen hello değerini aşağı yazma **parola** kutusu.</span><span class="sxs-lookup"><span data-stu-id="fbe29-191">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

   <span data-ttu-id="fbe29-192">d.</span><span class="sxs-lookup"><span data-stu-id="fbe29-192">d.</span></span> <span data-ttu-id="fbe29-193">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fbe29-193">Click **Create**.</span></span>
 
### <a name="create-a-predictix-ordering-test-user"></a><span data-ttu-id="fbe29-194">Predictix sıralama test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="fbe29-194">Create a Predictix Ordering test user</span></span>

<span data-ttu-id="fbe29-195">Bu bölümde, Predictix sıralamada Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fbe29-195">In this section, you create a user called Britta Simon in Predictix Ordering.</span></span> <span data-ttu-id="fbe29-196">Çalışmak [Predictix sıralama destek ekibi](https://www.predix.io/support/) tooadd hello kullanıcılar hello Predictix sıralama Platform.</span><span class="sxs-lookup"><span data-stu-id="fbe29-196">Work with [Predictix Ordering support team](https://www.predix.io/support/) tooadd hello users in hello Predictix Ordering platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="fbe29-197">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="fbe29-197">Assign hello Azure AD test user</span></span>

<span data-ttu-id="fbe29-198">Bu bölümde, Azure çoklu oturum açma Britta Simon toouse erişim tooPredictix vererek etkinleştirmeniz sıralama.</span><span class="sxs-lookup"><span data-stu-id="fbe29-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPredictix Ordering.</span></span>

![Merhaba kullanıcı rolü atayın][200] 

<span data-ttu-id="fbe29-200">**tooassign Britta Simon tooPredictix sıralama, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="fbe29-200">**tooassign Britta Simon tooPredictix Ordering, perform hello following steps:**</span></span>

1. <span data-ttu-id="fbe29-201">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="fbe29-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="fbe29-203">Merhaba uygulamalar listesinde **Predictix sıralama**.</span><span class="sxs-lookup"><span data-stu-id="fbe29-203">In hello applications list, select **Predictix Ordering**.</span></span>

    ![Merhaba Predictix sıralama bağlantıyı hello uygulamalar listesi](./media/active-directory-saas-predictixordering-tutorial/tutorial_predictixordering_app.png)  

3. <span data-ttu-id="fbe29-205">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="fbe29-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202]

4. <span data-ttu-id="fbe29-207">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="fbe29-207">Click **Add** button.</span></span> <span data-ttu-id="fbe29-208">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="fbe29-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Merhaba eklemek atama bölmesi][203]

5. <span data-ttu-id="fbe29-210">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="fbe29-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="fbe29-211">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="fbe29-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fbe29-212">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="fbe29-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="fbe29-213">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="fbe29-213">Test single sign-on</span></span>

<span data-ttu-id="fbe29-214">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="fbe29-214">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="fbe29-215">Merhaba Predictix sıralama parçasında hello erişim paneli tıkladığınızda, otomatik olarak oturum açma Predictix siparişi uygulaması tooyour almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="fbe29-215">When you click hello Predictix Ordering tile in hello Access Panel, you should get automatically signed-on tooyour Predictix Ordering application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="fbe29-216">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="fbe29-216">Additional resources</span></span>

* [<span data-ttu-id="fbe29-217">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="fbe29-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fbe29-218">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="fbe29-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-predictixordering-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-predictixordering-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-predictixordering-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-predictixordering-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-predictixordering-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-predictixordering-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-predictixordering-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-predictixordering-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-predictixordering-tutorial/tutorial_general_203.png

