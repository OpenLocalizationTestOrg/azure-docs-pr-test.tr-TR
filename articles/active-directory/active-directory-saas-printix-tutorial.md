---
title: "Öğretici: Azure Active Directory Tümleştirme ile Printix | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Printix arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4aea7320-b2d5-49e0-9b63-aeaff0f6fe66
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 654810116091eb52912b377cc97afef803ee816e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-printix"></a><span data-ttu-id="f7ae8-103">Öğretici: Azure Active Directory Tümleştirme Printix ile</span><span class="sxs-lookup"><span data-stu-id="f7ae8-103">Tutorial: Azure Active Directory integration with Printix</span></span>

<span data-ttu-id="f7ae8-104">Bu öğreticide, bilgi nasıl toointegrate Printix Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f7ae8-104">In this tutorial, you learn how toointegrate Printix with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f7ae8-105">Printix Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="f7ae8-105">Integrating Printix with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f7ae8-106">Erişim tooPrintix sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="f7ae8-106">You can control in Azure AD who has access tooPrintix</span></span>
- <span data-ttu-id="f7ae8-107">Kullanıcıların tooautomatically get açan tooPrintix (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="f7ae8-107">You can enable your users tooautomatically get signed-on tooPrintix (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f7ae8-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="f7ae8-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f7ae8-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f7ae8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f7ae8-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="f7ae8-110">Prerequisites</span></span>

<span data-ttu-id="f7ae8-111">tooconfigure Printix ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="f7ae8-111">tooconfigure Azure AD integration with Printix, you need hello following items:</span></span>

- <span data-ttu-id="f7ae8-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="f7ae8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f7ae8-113">Bir Printix çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="f7ae8-113">A Printix single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f7ae8-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="f7ae8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f7ae8-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="f7ae8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f7ae8-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="f7ae8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f7ae8-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f7ae8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f7ae8-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="f7ae8-118">Scenario description</span></span>
<span data-ttu-id="f7ae8-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="f7ae8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f7ae8-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="f7ae8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f7ae8-121">Merhaba Galerisi'nden Printix ekleme</span><span class="sxs-lookup"><span data-stu-id="f7ae8-121">Adding Printix from hello gallery</span></span>
2. <span data-ttu-id="f7ae8-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="f7ae8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-printix-from-hello-gallery"></a><span data-ttu-id="f7ae8-123">Merhaba Galerisi'nden Printix ekleme</span><span class="sxs-lookup"><span data-stu-id="f7ae8-123">Adding Printix from hello gallery</span></span>
<span data-ttu-id="f7ae8-124">Azure AD'ye tooconfigure hello tümleştirme Printix, tooadd Printix hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="f7ae8-124">tooconfigure hello integration of Printix into Azure AD, you need tooadd Printix from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f7ae8-125">**tooadd Printix hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f7ae8-125">**tooadd Printix from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f7ae8-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="f7ae8-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f7ae8-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="f7ae8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f7ae8-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="f7ae8-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="f7ae8-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f7ae8-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="f7ae8-133">Merhaba arama kutusuna yazın **Printix**.</span><span class="sxs-lookup"><span data-stu-id="f7ae8-133">In hello search box, type **Printix**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-printix-tutorial/tutorial_printix_search.png)

5. <span data-ttu-id="f7ae8-135">Merhaba Sonuçlar panelinde seçin **Printix**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="f7ae8-135">In hello results panel, select **Printix**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-printix-tutorial/tutorial_printix_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f7ae8-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="f7ae8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f7ae8-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Printix sınayın.</span><span class="sxs-lookup"><span data-stu-id="f7ae8-138">In this section, you configure and test Azure AD single sign-on with Printix based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f7ae8-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Printix içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="f7ae8-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Printix is tooa user in Azure AD.</span></span> <span data-ttu-id="f7ae8-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Printix hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="f7ae8-140">In other words, a link relationship between an Azure AD user and hello related user in Printix needs toobe established.</span></span>

<span data-ttu-id="f7ae8-141">Merhaba hello değeri Printix içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="f7ae8-141">In Printix, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f7ae8-142">tooconfigure ve Printix ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="f7ae8-142">tooconfigure and test Azure AD single sign-on with Printix, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f7ae8-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="f7ae8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f7ae8-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="f7ae8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f7ae8-145">**[Printix test kullanıcısı oluşturma](#creating-a-printix-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Printix içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="f7ae8-145">**[Creating a Printix test user](#creating-a-printix-test-user)** - toohave a counterpart of Britta Simon in Printix that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f7ae8-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="f7ae8-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f7ae8-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="f7ae8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f7ae8-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f7ae8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f7ae8-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Printix uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="f7ae8-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Printix application.</span></span>

<span data-ttu-id="f7ae8-150">**tooconfigure Azure AD çoklu oturum açma ile Printix, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f7ae8-150">**tooconfigure Azure AD single sign-on with Printix, perform hello following steps:**</span></span>

1. <span data-ttu-id="f7ae8-151">Hello hello üzerinde Azure portal'ın **Printix** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="f7ae8-151">In hello Azure portal, on hello **Printix** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="f7ae8-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="f7ae8-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-printix-tutorial/tutorial_printix_samlbase.png)

3. <span data-ttu-id="f7ae8-155">Merhaba üzerinde **Printix etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="f7ae8-155">On hello **Printix Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-printix-tutorial/tutorial_printix_url.png)

    <span data-ttu-id="f7ae8-157">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.printix.net`</span><span class="sxs-lookup"><span data-stu-id="f7ae8-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.printix.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f7ae8-158">Merhaba değeri gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="f7ae8-158">hello value is not real.</span></span> <span data-ttu-id="f7ae8-159">Güncelleştirme hello değerle hello gerçek oturum açma URL'si.</span><span class="sxs-lookup"><span data-stu-id="f7ae8-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="f7ae8-160">Kişi [Printix istemci destek ekibi](mailto:support@printix.net) tooget hello değeri.</span><span class="sxs-lookup"><span data-stu-id="f7ae8-160">Contact [Printix Client support team](mailto:support@printix.net) tooget hello value.</span></span> 
 
4. <span data-ttu-id="f7ae8-161">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="f7ae8-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-printix-tutorial/tutorial_printix_certificate.png) 

5. <span data-ttu-id="f7ae8-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f7ae8-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-printix-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f7ae8-165">Yönetici olarak oturum açma tooyour Printix Kiracı.</span><span class="sxs-lookup"><span data-stu-id="f7ae8-165">Sign-on tooyour Printix tenant as an administrator.</span></span>

7. <span data-ttu-id="f7ae8-166">Merhaba menüde hello üstte hello sağ üst köşesindeki hello simgesini tıklatın ve seçin "**kimlik doğrulaması**".</span><span class="sxs-lookup"><span data-stu-id="f7ae8-166">In hello menu on hello top, click hello icon at hello upper right corner and select "**Authentication**".</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-printix-tutorial/tutorial_printix_06.png)

8. <span data-ttu-id="f7ae8-168">Merhaba üzerinde **Kurulum** sekmesine **etkinleştirmek Azure/Office 365 kimlik doğrulaması**</span><span class="sxs-lookup"><span data-stu-id="f7ae8-168">On hello **Setup** tab, select **Enable Azure/Office 365 authentication**</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-printix-tutorial/tutorial_printix_07.png)

9. <span data-ttu-id="f7ae8-170">Merhaba üzerinde **Azure** sekmesi, giriş Federasyon meta veri URL'sini toohello textbox, "**Federasyon meta veri belgesi**".</span><span class="sxs-lookup"><span data-stu-id="f7ae8-170">On hello **Azure** tab, input federation metadata URL toohello textbox of "**Federation metadata document**".</span></span> 

    <span data-ttu-id="f7ae8-171">Azure AD'den çok indirilen hello meta veri xml dosyası ekleme[Printix destek ekibi](mailto:support@printix.net).</span><span class="sxs-lookup"><span data-stu-id="f7ae8-171">Attach hello metadata xml file which you downloaded from Azure AD too[Printix support team](mailto:support@printix.net).</span></span> <span data-ttu-id="f7ae8-172">Ardından hello xml dosyasını karşıya yüklemek ve Federasyon meta veri URL'sini girin.</span><span class="sxs-lookup"><span data-stu-id="f7ae8-172">Then they upload hello xml file and provide a federation metadata URL.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-printix-tutorial/tutorial_printix_08.png)
   
10. <span data-ttu-id="f7ae8-174">Merhaba tıklayın "**Test**"düğmesini tıklatın ve tıklatın"**Tamam**" Merhaba testi başarılı olursa düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f7ae8-174">Click hello "**Test**" button and click "**OK**" button if hello test was successful.</span></span>
   
     <span data-ttu-id="f7ae8-175">Azure active directory sayfasında hello tıkladıktan sonra gösterilir **test** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f7ae8-175">Azure active directory page will show after clicking hello **test** button.</span></span> <span data-ttu-id="f7ae8-176">"hello test başarılı oldu" Buraya pop Azure test hesabınız hello kimlik bilgilerini girdikten sonra bir iletiyi "test Tamam ayarları" anlamına gelir. Merhaba ardından **Tamam** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f7ae8-176">"hello test was successful" here means after entering hello credentials of your Azure test account it will pop up a message "Settings tested OK".Then click hello **OK** button.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-printix-tutorial/tutorial_printix_09.png)

11. <span data-ttu-id="f7ae8-178">Merhaba tıklatın **kaydetmek** düğmesini "**kimlik doğrulaması**" sayfası.</span><span class="sxs-lookup"><span data-stu-id="f7ae8-178">Click hello **Save** button on "**Authentication**" page.</span></span>


> [!TIP]
> <span data-ttu-id="f7ae8-179">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="f7ae8-179">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f7ae8-180">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="f7ae8-180">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f7ae8-181">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f7ae8-181">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f7ae8-182">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f7ae8-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="f7ae8-183">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="f7ae8-183">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="f7ae8-185">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f7ae8-185">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f7ae8-186">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="f7ae8-186">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-printix-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f7ae8-188">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="f7ae8-188">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-printix-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f7ae8-190">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="f7ae8-190">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-printix-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f7ae8-192">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="f7ae8-192">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-printix-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f7ae8-194">a.</span><span class="sxs-lookup"><span data-stu-id="f7ae8-194">a.</span></span> <span data-ttu-id="f7ae8-195">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f7ae8-195">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f7ae8-196">b.</span><span class="sxs-lookup"><span data-stu-id="f7ae8-196">b.</span></span> <span data-ttu-id="f7ae8-197">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="f7ae8-197">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f7ae8-198">c.</span><span class="sxs-lookup"><span data-stu-id="f7ae8-198">c.</span></span> <span data-ttu-id="f7ae8-199">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="f7ae8-199">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f7ae8-200">d.</span><span class="sxs-lookup"><span data-stu-id="f7ae8-200">d.</span></span> <span data-ttu-id="f7ae8-201">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f7ae8-201">Click **Create**.</span></span>
 
### <a name="creating-a-printix-test-user"></a><span data-ttu-id="f7ae8-202">Printix test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f7ae8-202">Creating a Printix test user</span></span>

<span data-ttu-id="f7ae8-203">Bu bölümde Hello amacı toocreate Britta Simon içinde Printix adlı bir kullanıcı ' dir.</span><span class="sxs-lookup"><span data-stu-id="f7ae8-203">hello objective of this section is toocreate a user called Britta Simon in Printix.</span></span> <span data-ttu-id="f7ae8-204">Printix yalnızca zaman sağlama, varsayılan olarak etkin olduğu destekler.</span><span class="sxs-lookup"><span data-stu-id="f7ae8-204">Printix supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="f7ae8-205">Bu bölümde, eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="f7ae8-205">There is no action item for you in this section.</span></span> <span data-ttu-id="f7ae8-206">Henüz yoksa yeni bir kullanıcı bir girişim tooaccess Printix sırasında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="f7ae8-206">A new user is created during an attempt tooaccess Printix if it doesn't exist yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="f7ae8-207">Toocreate kullanıcı el ile gerekiyorsa, toocontact hello gereksinim [Printix destek ekibi](mailto:support@printix.net).</span><span class="sxs-lookup"><span data-stu-id="f7ae8-207">If you need toocreate a user manually, you need toocontact hello [Printix support team](mailto:support@printix.net).</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f7ae8-208">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="f7ae8-208">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f7ae8-209">Bu bölümde, erişim tooPrintix vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="f7ae8-209">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPrintix.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="f7ae8-211">**tooassign Britta Simon tooPrintix hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f7ae8-211">**tooassign Britta Simon tooPrintix, perform hello following steps:**</span></span>

1. <span data-ttu-id="f7ae8-212">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="f7ae8-212">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="f7ae8-214">Merhaba uygulamalar listesinde **Printix**.</span><span class="sxs-lookup"><span data-stu-id="f7ae8-214">In hello applications list, select **Printix**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-printix-tutorial/tutorial_printix_app.png) 

3. <span data-ttu-id="f7ae8-216">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="f7ae8-216">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="f7ae8-218">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f7ae8-218">Click **Add** button.</span></span> <span data-ttu-id="f7ae8-219">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="f7ae8-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="f7ae8-221">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="f7ae8-221">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f7ae8-222">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="f7ae8-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f7ae8-223">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="f7ae8-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f7ae8-224">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="f7ae8-224">Testing single sign-on</span></span>

<span data-ttu-id="f7ae8-225">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="f7ae8-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f7ae8-226">Merhaba Printix hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Printix uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f7ae8-226">When you click hello Printix tile in hello Access Panel, you should get automatically signed-on tooyour Printix application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f7ae8-227">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="f7ae8-227">Additional resources</span></span>

* [<span data-ttu-id="f7ae8-228">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="f7ae8-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f7ae8-229">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="f7ae8-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-printix-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-printix-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-printix-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-printix-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-printix-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-printix-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-printix-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-printix-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-printix-tutorial/tutorial_general_203.png

