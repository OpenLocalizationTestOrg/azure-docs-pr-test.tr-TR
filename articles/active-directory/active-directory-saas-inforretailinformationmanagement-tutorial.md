---
title: "Öğretici: Azure Active Directory Tümleştirme Böl perakende – bilgi yönetimi ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Böl perakende – bilgi yönetimi arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 5ff49168-ef81-4169-8e5e-dc86e24dd5e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: 9cd8ab65d41d01832e0611f7f8254aa257120508
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-infor-retail--information-management"></a><span data-ttu-id="9eb52-103">Öğretici: Azure Active Directory Tümleştirme ile Böl perakende – bilgi yönetimi</span><span class="sxs-lookup"><span data-stu-id="9eb52-103">Tutorial: Azure Active Directory integration with Infor Retail – Information Management</span></span>

<span data-ttu-id="9eb52-104">Bu öğreticide, bilgi nasıl toointegrate etmek perakende – Azure Active Directory (Azure AD) ile bilgi yönetimi.</span><span class="sxs-lookup"><span data-stu-id="9eb52-104">In this tutorial, you learn how toointegrate Infor Retail – Information Management with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9eb52-105">Böl perakende – bilgi yönetimi Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="9eb52-105">Integrating Infor Retail – Information Management with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9eb52-106">Erişim tooInfor perakende – bilgi yönetimi sahip Azure AD'de kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9eb52-106">You can control in Azure AD who has access tooInfor Retail – Information Management.</span></span>
- <span data-ttu-id="9eb52-107">Kullanıcıların tooautomatically get açan tooInfor perakende – bilgi yönetimi (çoklu oturum açma) Azure AD hesaplarına ile etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9eb52-107">You can enable your users tooautomatically get signed-on tooInfor Retail – Information Management (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="9eb52-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="9eb52-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="9eb52-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9eb52-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9eb52-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="9eb52-110">Prerequisites</span></span>

<span data-ttu-id="9eb52-111">tooconfigure etmek perakende – bilgi yönetimi ile Azure AD tümleştirme aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="9eb52-111">tooconfigure Azure AD integration with Infor Retail – Information Management, you need hello following items:</span></span>

- <span data-ttu-id="9eb52-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="9eb52-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9eb52-113">Böl perakende – bilgi yönetimi çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="9eb52-113">An Infor Retail – Information Management single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9eb52-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="9eb52-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9eb52-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="9eb52-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9eb52-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="9eb52-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9eb52-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9eb52-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9eb52-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="9eb52-118">Scenario description</span></span>
<span data-ttu-id="9eb52-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="9eb52-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9eb52-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="9eb52-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9eb52-121">Bilgi Yönetimi hello galerisinden Böl perakende – ekleme</span><span class="sxs-lookup"><span data-stu-id="9eb52-121">Adding Infor Retail – Information Management from hello gallery</span></span>
2. <span data-ttu-id="9eb52-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="9eb52-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-infor-retail--information-management-from-hello-gallery"></a><span data-ttu-id="9eb52-123">Bilgi Yönetimi hello galerisinden Böl perakende – ekleme</span><span class="sxs-lookup"><span data-stu-id="9eb52-123">Adding Infor Retail – Information Management from hello gallery</span></span>
<span data-ttu-id="9eb52-124">Böl perakende – Azure AD, bilgi yönetime tooconfigure hello tümleştirme tooadd etmek perakende – bilgi yönetimi hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="9eb52-124">tooconfigure hello integration of Infor Retail – Information Management into Azure AD, you need tooadd Infor Retail – Information Management from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9eb52-125">**tooadd etmek perakende – bilgi yönetimi hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="9eb52-125">**tooadd Infor Retail – Information Management from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9eb52-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="9eb52-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory düğmesi][1]

2. <span data-ttu-id="9eb52-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="9eb52-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9eb52-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="9eb52-129">Then go too**All applications**.</span></span>

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="9eb52-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="9eb52-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Merhaba yeni uygulama düğmesi][3]

4. <span data-ttu-id="9eb52-133">Merhaba arama kutusuna yazın **etmek perakende – bilgi yönetimi**seçin **etmek perakende – bilgi yönetimi** sonuç panelinden ardından **Ekle** düğmesini tooadd hello uygulama.</span><span class="sxs-lookup"><span data-stu-id="9eb52-133">In hello search box, type **Infor Retail – Information Management**, select **Infor Retail – Information Management** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Böl perakende – hello sonuçları listesinde bilgi yönetimi](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="9eb52-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="9eb52-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="9eb52-136">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma Böl perakende – bilgi "Britta Simon" adlı bir test kullanıcı tabanlı yönetim ile test etme.</span><span class="sxs-lookup"><span data-stu-id="9eb52-136">In this section, you configure and test Azure AD single sign-on with Infor Retail – Information Management based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9eb52-137">Çoklu oturum açma toowork için Azure AD tooknow etmek perakende hangi hello karşılık gelen kullanıcı gerekir – Azure AD içinde bilgi yönetimi tooa kullanıcıdır.</span><span class="sxs-lookup"><span data-stu-id="9eb52-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Infor Retail – Information Management is tooa user in Azure AD.</span></span> <span data-ttu-id="9eb52-138">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Böl perakende – bilgi yönetimi hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="9eb52-138">In other words, a link relationship between an Azure AD user and hello related user in Infor Retail – Information Management needs toobe established.</span></span>

<span data-ttu-id="9eb52-139">Böl perakende – bilgi yönetimi hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="9eb52-139">In Infor Retail – Information Management, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="9eb52-140">tooconfigure ve Azure AD çoklu oturum açmayı test etmek perakende – bilgi yönetimi ile aşağıdaki yapı taşları toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="9eb52-140">tooconfigure and test Azure AD single sign-on with Infor Retail – Information Management, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9eb52-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="9eb52-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9eb52-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="9eb52-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9eb52-143">**[Böl perakende – bilgi yönetimi test kullanıcısı oluşturma](#create-an-infor-retail--information-management-test-user)**  - toohave Britta Simon Böl perakende içinde karşılık gelen – bilgi yönetimi, kullanıcı bağlantılı toohello Azure AD gösterimidir.</span><span class="sxs-lookup"><span data-stu-id="9eb52-143">**[Create an Infor Retail – Information Management test user](#create-an-infor-retail--information-management-test-user)** - toohave a counterpart of Britta Simon in Infor Retail – Information Management that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9eb52-144">**[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="9eb52-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9eb52-145">**[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="9eb52-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="9eb52-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="9eb52-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="9eb52-147">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma, Böl perakende – bilgi yönetimi uygulamasını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="9eb52-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Infor Retail – Information Management application.</span></span>

<span data-ttu-id="9eb52-148">**Azure AD çoklu oturum açma tooconfigure etmek perakende – bilgi yönetimi ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="9eb52-148">**tooconfigure Azure AD single sign-on with Infor Retail – Information Management, perform hello following steps:**</span></span>

1. <span data-ttu-id="9eb52-149">Merhaba hello üzerinde Azure portal'ın **etmek perakende – bilgi yönetimi** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="9eb52-149">In hello Azure portal, on hello **Infor Retail – Information Management** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. <span data-ttu-id="9eb52-151">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="9eb52-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_samlbase.png)

3. <span data-ttu-id="9eb52-153">Merhaba üzerinde **etmek perakende – bilgi yönetim etki alanı ve URL'leri** bölümünde, hello tooconfigure hello IDP uygulamada başlatılan modu istiyorsanız aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="9eb52-153">On hello **Infor Retail – Information Management Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in IDP initiated mode:</span></span>

    ![Böl perakende – bilgi yönetim etki alanı ve URL'ler tek oturum açma bilgileri IDP](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_url.png)

    <span data-ttu-id="9eb52-155">a.</span><span class="sxs-lookup"><span data-stu-id="9eb52-155">a.</span></span> <span data-ttu-id="9eb52-156">Merhaba, **tanımlayıcısı** metin kutusuna, türü aşağıdaki hello kullanarak bir URL düzenleri:</span><span class="sxs-lookup"><span data-stu-id="9eb52-156">In hello **Identifier** textbox, type a URL using hello following patterns:</span></span> 
    |   |
    | -- |
    | `https://<company name>.mingle.infor.com` |
    | `http://<company name>.mingledev.infor.com` |

    <span data-ttu-id="9eb52-157">b.</span><span class="sxs-lookup"><span data-stu-id="9eb52-157">b.</span></span> <span data-ttu-id="9eb52-158">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<company name>.mingle.infor.com/sp/ACS.saml2`</span><span class="sxs-lookup"><span data-stu-id="9eb52-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.mingle.infor.com/sp/ACS.saml2`</span></span>

4. <span data-ttu-id="9eb52-159">Denetleme **Göster Gelişmiş URL ayarları** ve adım tooconfigure hello uygulamada istiyorsanız aşağıdaki hello gerçekleştirmek **SP** modunda başlatılan:</span><span class="sxs-lookup"><span data-stu-id="9eb52-159">Check **Show advanced URL settings** and perform hello following step if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Böl perakende – bilgi yönetim etki alanı ve URL'leri tek oturum açma bilgileri SP](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_url1.png)

    <span data-ttu-id="9eb52-161">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<company name>.mingle.infor.com/<company code>`</span><span class="sxs-lookup"><span data-stu-id="9eb52-161">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.mingle.infor.com/<company code>`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="9eb52-162">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="9eb52-162">These values are not real.</span></span> <span data-ttu-id="9eb52-163">Bu güncelleştirme tanımlayıcısı, yanıt URL'si ve oturum açma URL'si ile Merhaba gerçek değerler.</span><span class="sxs-lookup"><span data-stu-id="9eb52-163">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="9eb52-164">Kişi [etmek perakende – bilgi yönetimi istemci destek ekibi](mailto:innovate@infor.com) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="9eb52-164">Contact [Infor Retail – Information Management Client support team](mailto:innovate@infor.com) tooget these values.</span></span> 

5. <span data-ttu-id="9eb52-165">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="9eb52-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_certificate.png) 

6. <span data-ttu-id="9eb52-167">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="9eb52-167">Click **Save** button.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="9eb52-169">tooconfigure çoklu oturum açma üzerinde **etmek perakende – bilgi yönetimi** yan, indirilen toosend hello ihtiyacınız **meta veri XML** çok[etmek perakende – bilgi yönetimi destek ekibi ](mailto:innovate@infor.com).</span><span class="sxs-lookup"><span data-stu-id="9eb52-169">tooconfigure single sign-on on **Infor Retail – Information Management** side, you need toosend hello downloaded **Metadata XML** too[Infor Retail – Information Management support team](mailto:innovate@infor.com).</span></span> <span data-ttu-id="9eb52-170">Bunlar, bu ayar toohave hello iki tarafta da ayarlamanızı SAML SSO bağlantı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9eb52-170">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="9eb52-171">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="9eb52-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9eb52-172">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="9eb52-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9eb52-173">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9eb52-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="9eb52-174">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="9eb52-174">Create an Azure AD test user</span></span>

<span data-ttu-id="9eb52-175">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="9eb52-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="9eb52-177">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="9eb52-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9eb52-178">Merhaba hello sol bölmede Azure portal hello tıklatın **Azure Active Directory** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="9eb52-178">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-inforretailinformationmanagement-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="9eb52-180">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="9eb52-180">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-inforretailinformationmanagement-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="9eb52-182">tooopen hello **kullanıcı** iletişim kutusu, tıklatın **Ekle** hello hello üstündeki **tüm kullanıcılar** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="9eb52-182">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Merhaba Ekle düğmesi](./media/active-directory-saas-inforretailinformationmanagement-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="9eb52-184">Merhaba, **kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="9eb52-184">In hello **User** dialog box, perform hello following steps:</span></span>

    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-inforretailinformationmanagement-tutorial/create_aaduser_04.png)

    <span data-ttu-id="9eb52-186">a.</span><span class="sxs-lookup"><span data-stu-id="9eb52-186">a.</span></span> <span data-ttu-id="9eb52-187">Merhaba, **adı** kutusuna **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9eb52-187">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9eb52-188">b.</span><span class="sxs-lookup"><span data-stu-id="9eb52-188">b.</span></span> <span data-ttu-id="9eb52-189">Merhaba, **kullanıcı adı** kutusuna, kullanıcının Britta Simon hello e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="9eb52-189">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="9eb52-190">c.</span><span class="sxs-lookup"><span data-stu-id="9eb52-190">c.</span></span> <span data-ttu-id="9eb52-191">Select hello **Göster parola** onay kutusunu işaretleyin ve ardından hello görüntülenen hello değerini aşağı yazma **parola** kutusu.</span><span class="sxs-lookup"><span data-stu-id="9eb52-191">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="9eb52-192">d.</span><span class="sxs-lookup"><span data-stu-id="9eb52-192">d.</span></span> <span data-ttu-id="9eb52-193">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9eb52-193">Click **Create**.</span></span>
 
### <a name="create-an-infor-retail--information-management-test-user"></a><span data-ttu-id="9eb52-194">Böl perakende – bilgi yönetimi test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="9eb52-194">Create an Infor Retail – Information Management test user</span></span>

<span data-ttu-id="9eb52-195">Bu bölümde, Britta Simon Böl perakende – bilgi yönetimi adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9eb52-195">In this section, you create a user called Britta Simon in Infor Retail – Information Management.</span></span> <span data-ttu-id="9eb52-196">Lütfen çalışmak [etmek perakende – bilgi yönetimi destek ekibi](mailto:innovate@infor.com) tooadd hello kullanıcılar hello Böl perakende – bilgi yönetimi platformu.</span><span class="sxs-lookup"><span data-stu-id="9eb52-196">Please work with [Infor Retail – Information Management support team](mailto:innovate@infor.com) tooadd hello users in hello Infor Retail – Information Management platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="9eb52-197">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="9eb52-197">Assign hello Azure AD test user</span></span>

<span data-ttu-id="9eb52-198">Bu bölümde, erişim tooInfor perakende – bilgi yönetimi vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="9eb52-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooInfor Retail – Information Management.</span></span>

![Merhaba kullanıcı rolü atayın][200] 

<span data-ttu-id="9eb52-200">**tooassign Britta Simon tooInfor perakende – bilgi yönetimi hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="9eb52-200">**tooassign Britta Simon tooInfor Retail – Information Management, perform hello following steps:**</span></span>

1. <span data-ttu-id="9eb52-201">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="9eb52-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="9eb52-203">Merhaba uygulamalar listesinde **etmek perakende – bilgi yönetimi**.</span><span class="sxs-lookup"><span data-stu-id="9eb52-203">In hello applications list, select **Infor Retail – Information Management**.</span></span>

    ![Merhaba Böl perakende – bilgi yönetimi bağlantı hello uygulamalar listesinde](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_app.png)  

3. <span data-ttu-id="9eb52-205">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="9eb52-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202]

4. <span data-ttu-id="9eb52-207">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="9eb52-207">Click **Add** button.</span></span> <span data-ttu-id="9eb52-208">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="9eb52-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Merhaba eklemek atama bölmesi][203]

5. <span data-ttu-id="9eb52-210">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="9eb52-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9eb52-211">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="9eb52-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9eb52-212">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="9eb52-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="9eb52-213">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="9eb52-213">Test single sign-on</span></span>

<span data-ttu-id="9eb52-214">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="9eb52-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="9eb52-215">Merhaba Böl perakende – hello erişim paneli, bilgi yönetimi parçasında tıkladığınızda otomatik olarak oturum açma tooyour etmek perakende – bilgi yönetimi uygulamasını almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9eb52-215">When you click hello Infor Retail – Information Management tile in hello Access Panel, you should get automatically signed-on tooyour Infor Retail – Information Management application.</span></span>
<span data-ttu-id="9eb52-216">Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9eb52-216">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="9eb52-217">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="9eb52-217">Additional resources</span></span>

* [<span data-ttu-id="9eb52-218">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="9eb52-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9eb52-219">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="9eb52-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_203.png

