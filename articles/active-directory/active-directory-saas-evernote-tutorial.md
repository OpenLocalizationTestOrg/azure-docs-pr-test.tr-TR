---
title: "Öğretici: Azure Active Directory Tümleştirme ile Evernote | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Evernote arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 4d7017e571ed12a0b155aa188c6b0ecb3c9898a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-evernote"></a><span data-ttu-id="7a372-103">Öğretici: Azure Active Directory Tümleştirme Evernote ile</span><span class="sxs-lookup"><span data-stu-id="7a372-103">Tutorial: Azure Active Directory integration with Evernote</span></span>

<span data-ttu-id="7a372-104">Bu öğreticide, bilgi nasıl toointegrate Evernote Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7a372-104">In this tutorial, you learn how toointegrate Evernote with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7a372-105">Evernote Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="7a372-105">Integrating Evernote with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7a372-106">Erişim tooEvernote sahip Azure AD'de kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7a372-106">You can control in Azure AD who has access tooEvernote.</span></span>
- <span data-ttu-id="7a372-107">Kullanıcıların tooautomatically get açan tooEvernote (çoklu oturum açma) Azure AD hesaplarına ile etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7a372-107">You can enable your users tooautomatically get signed-on tooEvernote (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="7a372-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="7a372-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="7a372-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7a372-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7a372-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="7a372-110">Prerequisites</span></span>

<span data-ttu-id="7a372-111">tooconfigure Evernote ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="7a372-111">tooconfigure Azure AD integration with Evernote, you need hello following items:</span></span>

- <span data-ttu-id="7a372-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="7a372-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7a372-113">Bir Evernote çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="7a372-113">An Evernote single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7a372-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="7a372-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7a372-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="7a372-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7a372-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="7a372-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7a372-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7a372-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7a372-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="7a372-118">Scenario description</span></span>
<span data-ttu-id="7a372-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="7a372-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7a372-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="7a372-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7a372-121">Merhaba Galerisi'nden Evernote ekleme</span><span class="sxs-lookup"><span data-stu-id="7a372-121">Adding Evernote from hello gallery</span></span>
2. <span data-ttu-id="7a372-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="7a372-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-evernote-from-hello-gallery"></a><span data-ttu-id="7a372-123">Merhaba Galerisi'nden Evernote ekleme</span><span class="sxs-lookup"><span data-stu-id="7a372-123">Adding Evernote from hello gallery</span></span>
<span data-ttu-id="7a372-124">Azure AD'ye tooconfigure hello tümleştirme Evernote, tooadd Evernote hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="7a372-124">tooconfigure hello integration of Evernote into Azure AD, you need tooadd Evernote from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7a372-125">**tooadd Evernote hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7a372-125">**tooadd Evernote from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7a372-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="7a372-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory düğmesi][1]

2. <span data-ttu-id="7a372-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="7a372-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7a372-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="7a372-129">Then go too**All applications**.</span></span>

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="7a372-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7a372-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Merhaba yeni uygulama düğmesi][3]

4. <span data-ttu-id="7a372-133">Merhaba arama kutusuna yazın **Evernote**seçin **Evernote** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="7a372-133">In hello search box, type **Evernote**, select **Evernote** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Merhaba sonuçları listesinde Evernote](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="7a372-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="7a372-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="7a372-136">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Evernote sınayın.</span><span class="sxs-lookup"><span data-stu-id="7a372-136">In this section, you configure and test Azure AD single sign-on with Evernote based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7a372-137">Tek toowork'ın oturum açma hangi hello karşılık gelen Evernote içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="7a372-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Evernote is tooa user in Azure AD.</span></span> <span data-ttu-id="7a372-138">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Evernote hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="7a372-138">In other words, a link relationship between an Azure AD user and hello related user in Evernote needs toobe established.</span></span>

<span data-ttu-id="7a372-139">Merhaba hello değeri Evernote içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="7a372-139">In Evernote, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7a372-140">tooconfigure ve Evernote ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="7a372-140">tooconfigure and test Azure AD single sign-on with Evernote, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7a372-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="7a372-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7a372-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="7a372-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7a372-143">**[Bir Evernote test kullanıcısı oluşturma](#create-an-evernote-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Evernote içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="7a372-143">**[Create an Evernote test user](#create-an-evernote-test-user)** - toohave a counterpart of Britta Simon in Evernote that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7a372-144">**[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="7a372-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7a372-145">**[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="7a372-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="7a372-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="7a372-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="7a372-147">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Evernote uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="7a372-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Evernote application.</span></span>

<span data-ttu-id="7a372-148">**tooconfigure Azure AD çoklu oturum açma ile Evernote, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7a372-148">**tooconfigure Azure AD single sign-on with Evernote, perform hello following steps:**</span></span>

1. <span data-ttu-id="7a372-149">Hello hello üzerinde Azure portal'ın **Evernote** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="7a372-149">In hello Azure portal, on hello **Evernote** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. <span data-ttu-id="7a372-151">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="7a372-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_samlbase.png)

3. <span data-ttu-id="7a372-153">Merhaba üzerinde **Evernote etki alanı ve URL'leri** bölümünde, hello tooconfigure hello IDP uygulamada başlatılan modu istiyorsanız aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="7a372-153">On hello **Evernote Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in IDP initiated mode:</span></span>

    ![Evernote etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_url.png)

    <span data-ttu-id="7a372-155">Merhaba, **tanımlayıcısı** metin kutusuna, türü hello URL'si:`https://www.evernote.com/saml2`</span><span class="sxs-lookup"><span data-stu-id="7a372-155">In hello **Identifier** textbox, type hello URL: `https://www.evernote.com/saml2`</span></span>

4. <span data-ttu-id="7a372-156">Denetleme **Göster Gelişmiş URL ayarları** ve adım tooconfigure hello uygulamada istiyorsanız aşağıdaki hello gerçekleştirmek **SP** modunda başlatılan:</span><span class="sxs-lookup"><span data-stu-id="7a372-156">Check **Show advanced URL settings** and perform hello following step if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Evernote etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_url1.png)

    <span data-ttu-id="7a372-158">Merhaba, **URL üzerinde oturum** metin kutusuna, türü hello URL'si:`https://www.evernote.com/Login.action`</span><span class="sxs-lookup"><span data-stu-id="7a372-158">In hello **Sign on URL** textbox, type hello URL: `https://www.evernote.com/Login.action`</span></span>   

5. <span data-ttu-id="7a372-159">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="7a372-159">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_certificate.png) 

6. <span data-ttu-id="7a372-161">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7a372-161">Click **Save** button.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-evernote-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="7a372-163">Merhaba üzerinde **Evernote yapılandırma** 'yi tıklatın **yapılandırma Evernote** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="7a372-163">On hello **Evernote Configuration** section, click **Configure Evernote** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="7a372-164">Kopya hello **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="7a372-164">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Evernote yapılandırma](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_configure.png) 

8. <span data-ttu-id="7a372-166">Farklı web tarayıcısı penceresinde Evernote şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="7a372-166">In a different web browser window, log into your Evernote company site as an administrator.</span></span>

9. <span data-ttu-id="7a372-167">Çok Git**'Yönetici Konsolu'**</span><span class="sxs-lookup"><span data-stu-id="7a372-167">Go too**'Admin Console'**</span></span>

    ![Yönetim Konsolu](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_adminconsole.png)

10. <span data-ttu-id="7a372-169">Merhaba gelen **'Yönetici Konsolu'**, çok Git**'Security'** seçip **' çoklu oturum açma '**</span><span class="sxs-lookup"><span data-stu-id="7a372-169">From hello **'Admin Console'**, go too**‘Security’** and select **‘Single Sign-On’**</span></span>

    ![SSO ayarı](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_sso.png)

11. <span data-ttu-id="7a372-171">Hello aşağıdaki değerleri yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="7a372-171">Configure hello following values:</span></span>

    ![Sertifika ayarları](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_certx.png)
    
    <span data-ttu-id="7a372-173">a.</span><span class="sxs-lookup"><span data-stu-id="7a372-173">a.</span></span>  <span data-ttu-id="7a372-174">**SSO etkinleştir:** SSO varsayılan olarak etkindir (tıklatın **devre dışı çoklu oturum açma** tooremove hello SSO gereksinim)</span><span class="sxs-lookup"><span data-stu-id="7a372-174">**Enable SSO:** SSO is enabled by default (Click **Disable Single Sign-on** tooremove hello SSO requirement)</span></span>

    <span data-ttu-id="7a372-175">b.</span><span class="sxs-lookup"><span data-stu-id="7a372-175">b.</span></span> <span data-ttu-id="7a372-176">Yapıştır **SAML çoklu oturum açma hizmet URL'si** hello hello Azure portal ' kopyaladığınız değeri **SAML HTTP istek URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="7a372-176">Paste **SAML Single sign-on Service URL** value, which you have copied from hello Azure portal into hello **SAML HTTP Request URL** textbox.</span></span>

    <span data-ttu-id="7a372-177">c.</span><span class="sxs-lookup"><span data-stu-id="7a372-177">c.</span></span> <span data-ttu-id="7a372-178">"Sertifika başlayın" ve "Son SERTİFİKAYI" gibi bir not defteri ve kopyalama hello içerik Azure AD'den hello indirilen sertifika açın ve hello yapıştırma **X.509 sertifikası** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="7a372-178">Open hello downloaded certificate from Azure AD in a notepad and copy hello content including "BEGIN CERTIFICATE" and "END CERTIFICATE" and paste it into hello **X.509 Certificate** textbox.</span></span> 

    <span data-ttu-id="7a372-179">d.Click **Değişiklikleri Kaydet**</span><span class="sxs-lookup"><span data-stu-id="7a372-179">d.Click **Save Changes**</span></span>

> [!TIP]
> <span data-ttu-id="7a372-180">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="7a372-180">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7a372-181">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="7a372-181">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7a372-182">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7a372-182">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="7a372-183">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7a372-183">Create an Azure AD test user</span></span>

<span data-ttu-id="7a372-184">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="7a372-184">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="7a372-186">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7a372-186">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7a372-187">Merhaba hello sol bölmede Azure portal hello tıklatın **Azure Active Directory** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7a372-187">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-evernote-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="7a372-189">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="7a372-189">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-evernote-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="7a372-191">tooopen hello **kullanıcı** iletişim kutusu, tıklatın **Ekle** hello hello üstündeki **tüm kullanıcılar** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="7a372-191">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Merhaba Ekle düğmesi](./media/active-directory-saas-evernote-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="7a372-193">Merhaba, **kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="7a372-193">In hello **User** dialog box, perform hello following steps:</span></span>

    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-evernote-tutorial/create_aaduser_04.png)

    <span data-ttu-id="7a372-195">a.</span><span class="sxs-lookup"><span data-stu-id="7a372-195">a.</span></span> <span data-ttu-id="7a372-196">Merhaba, **adı** kutusuna **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7a372-196">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7a372-197">b.</span><span class="sxs-lookup"><span data-stu-id="7a372-197">b.</span></span> <span data-ttu-id="7a372-198">Merhaba, **kullanıcı adı** kutusuna, kullanıcının Britta Simon hello e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="7a372-198">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="7a372-199">c.</span><span class="sxs-lookup"><span data-stu-id="7a372-199">c.</span></span> <span data-ttu-id="7a372-200">Select hello **Göster parola** onay kutusunu işaretleyin ve ardından hello görüntülenen hello değerini aşağı yazma **parola** kutusu.</span><span class="sxs-lookup"><span data-stu-id="7a372-200">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="7a372-201">d.</span><span class="sxs-lookup"><span data-stu-id="7a372-201">d.</span></span> <span data-ttu-id="7a372-202">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7a372-202">Click **Create**.</span></span>
 
### <a name="create-an-evernote-test-user"></a><span data-ttu-id="7a372-203">Bir Evernote test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7a372-203">Create an Evernote test user</span></span>

<span data-ttu-id="7a372-204">Evernote içine sipariş tooenable Azure AD kullanıcıların toolog bunların Evernote sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7a372-204">In order tooenable Azure AD users toolog into Evernote, they must be provisioned into Evernote.</span></span>  
<span data-ttu-id="7a372-205">Evernote Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="7a372-205">In hello case of Evernote, provisioning is a manual task.</span></span>

<span data-ttu-id="7a372-206">**bir kullanıcı hesapları tooprovision gerçekleştirmek hello adımları izleyin:**</span><span class="sxs-lookup"><span data-stu-id="7a372-206">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="7a372-207">İçinde tooyour Evernote şirket site yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="7a372-207">Log in tooyour Evernote company site as an administrator.</span></span>

2. <span data-ttu-id="7a372-208">Merhaba tıklatın **'Yönetici Konsolu'**.</span><span class="sxs-lookup"><span data-stu-id="7a372-208">Click hello **'Admin Console'**.</span></span>

    ![Yönetim Konsolu](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_adminconsole.png)

3. <span data-ttu-id="7a372-210">Merhaba gelen **'Yönetici Konsolu'**, çok Git**'kullanıcıları eklemek'**.</span><span class="sxs-lookup"><span data-stu-id="7a372-210">From hello **'Admin Console'**, go too**‘Add users’**.</span></span>

    ![Ekleme testUser](./media/active-directory-saas-evernote-tutorial/create_aaduser_0001.png)

4. <span data-ttu-id="7a372-212">**Ekip üyeleri ekleme** hello içinde **e-posta** metin kutusu, kullanıcı hesabı hello e-posta adresini yazın ve'ı tıklatın **davet edin.**</span><span class="sxs-lookup"><span data-stu-id="7a372-212">**Add team members** in hello **Email** textbox, type hello email address of user account and click **Invite.**</span></span>

    ![Ekleme testUser](./media/active-directory-saas-evernote-tutorial/create_aaduser_0002.png)
    
5. <span data-ttu-id="7a372-214">Davet gönderildikten sonra hello Azure Active Directory hesap sahibinin e-posta tooaccept hello davetiye alır.</span><span class="sxs-lookup"><span data-stu-id="7a372-214">After invitation is sent, hello Azure Active Directory account holder will receive an email tooaccept hello invitation.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="7a372-215">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="7a372-215">Assign hello Azure AD test user</span></span>

<span data-ttu-id="7a372-216">Bu bölümde, erişim tooEvernote vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="7a372-216">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooEvernote.</span></span>

![Merhaba kullanıcı rolü atayın][200] 

<span data-ttu-id="7a372-218">**tooassign Britta Simon tooEvernote hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7a372-218">**tooassign Britta Simon tooEvernote, perform hello following steps:**</span></span>

1. <span data-ttu-id="7a372-219">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="7a372-219">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="7a372-221">Merhaba uygulamalar listesinde **Evernote**.</span><span class="sxs-lookup"><span data-stu-id="7a372-221">In hello applications list, select **Evernote**.</span></span>

    ![Merhaba Evernote bağlantı hello uygulamalar listesinde](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_app.png)  

3. <span data-ttu-id="7a372-223">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="7a372-223">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202]

4. <span data-ttu-id="7a372-225">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7a372-225">Click **Add** button.</span></span> <span data-ttu-id="7a372-226">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="7a372-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Merhaba eklemek atama bölmesi][203]

5. <span data-ttu-id="7a372-228">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="7a372-228">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7a372-229">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="7a372-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7a372-230">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="7a372-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="7a372-231">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="7a372-231">Test single sign-on</span></span>

<span data-ttu-id="7a372-232">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="7a372-232">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="7a372-233">Merhaba Evernote hello erişim paneli parçasında tıkladığınızda, oturum açma Evernote uygulama tooyour almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7a372-233">When you click hello Evernote tile in hello Access Panel, you should get signed-on tooyour Evernote application.</span></span> <span data-ttu-id="7a372-234">Bir kuruluş hesabı ancak gerek toolog sonra kişisel hesabınızla oturum.</span><span class="sxs-lookup"><span data-stu-id="7a372-234">You'll be logging in as an Organization account but then need toolog in with your personal account.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7a372-235">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="7a372-235">Additional resources</span></span>

* [<span data-ttu-id="7a372-236">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="7a372-236">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7a372-237">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="7a372-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_203.png

