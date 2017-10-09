---
title: "Öğretici: Azure Active Directory Tümleştirme ile Zoho | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Zoho arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 9874e1f3-ade5-42e7-a700-e08b3731236a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jeedes
ms.openlocfilehash: 5d1c196d3b97babab196f509ea68e7d61523a7e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zoho"></a><span data-ttu-id="fbf26-103">Öğretici: Azure Active Directory Tümleştirme Zoho ile</span><span class="sxs-lookup"><span data-stu-id="fbf26-103">Tutorial: Azure Active Directory integration with Zoho</span></span>

<span data-ttu-id="fbf26-104">Bu öğreticide, bilgi nasıl toointegrate Zoho Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fbf26-104">In this tutorial, you learn how toointegrate Zoho with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fbf26-105">Zoho Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="fbf26-105">Integrating Zoho with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="fbf26-106">Erişim tooZoho sahip Azure AD'de kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fbf26-106">You can control in Azure AD who has access tooZoho.</span></span>
- <span data-ttu-id="fbf26-107">Kullanıcıların tooautomatically get açan tooZoho (çoklu oturum açma) Azure AD hesaplarına ile etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fbf26-107">You can enable your users tooautomatically get signed-on tooZoho (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="fbf26-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="fbf26-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="fbf26-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fbf26-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fbf26-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="fbf26-110">Prerequisites</span></span>

<span data-ttu-id="fbf26-111">tooconfigure Zoho ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="fbf26-111">tooconfigure Azure AD integration with Zoho, you need hello following items:</span></span>

- <span data-ttu-id="fbf26-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="fbf26-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fbf26-113">Bir Zoho çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="fbf26-113">A Zoho single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fbf26-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="fbf26-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fbf26-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="fbf26-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fbf26-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="fbf26-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fbf26-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fbf26-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fbf26-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="fbf26-118">Scenario description</span></span>
<span data-ttu-id="fbf26-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="fbf26-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fbf26-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="fbf26-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fbf26-121">Merhaba Galerisi'nden Zoho ekleme</span><span class="sxs-lookup"><span data-stu-id="fbf26-121">Adding Zoho from hello gallery</span></span>
2. <span data-ttu-id="fbf26-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="fbf26-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zoho-from-hello-gallery"></a><span data-ttu-id="fbf26-123">Merhaba Galerisi'nden Zoho ekleme</span><span class="sxs-lookup"><span data-stu-id="fbf26-123">Adding Zoho from hello gallery</span></span>
<span data-ttu-id="fbf26-124">Azure AD'ye tooconfigure hello tümleştirme Zoho, tooadd Zoho hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="fbf26-124">tooconfigure hello integration of Zoho into Azure AD, you need tooadd Zoho from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="fbf26-125">**tooadd Zoho hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="fbf26-125">**tooadd Zoho from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="fbf26-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="fbf26-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory düğmesi][1]

2. <span data-ttu-id="fbf26-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="fbf26-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="fbf26-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="fbf26-129">Then go too**All applications**.</span></span>

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="fbf26-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="fbf26-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Merhaba yeni uygulama düğmesi][3]

4. <span data-ttu-id="fbf26-133">Merhaba arama kutusuna yazın **Zoho**seçin **Zoho** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="fbf26-133">In hello search box, type **Zoho**, select **Zoho** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Merhaba sonuçları listesinde Zoho](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="fbf26-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="fbf26-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="fbf26-136">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Zoho sınayın.</span><span class="sxs-lookup"><span data-stu-id="fbf26-136">In this section, you configure and test Azure AD single sign-on with Zoho based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fbf26-137">Tek toowork'ın oturum açma hangi hello karşılık gelen Zoho içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="fbf26-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zoho is tooa user in Azure AD.</span></span> <span data-ttu-id="fbf26-138">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Zoho hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="fbf26-138">In other words, a link relationship between an Azure AD user and hello related user in Zoho needs toobe established.</span></span>

<span data-ttu-id="fbf26-139">Merhaba hello değeri Zoho içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="fbf26-139">In Zoho, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="fbf26-140">tooconfigure ve Zoho ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="fbf26-140">tooconfigure and test Azure AD single sign-on with Zoho, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="fbf26-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="fbf26-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="fbf26-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="fbf26-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fbf26-143">**[Zoho test kullanıcısı oluşturma](#create-a-zoho-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Zoho içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="fbf26-143">**[Create a Zoho test user](#create-a-zoho-test-user)** - toohave a counterpart of Britta Simon in Zoho that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="fbf26-144">**[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="fbf26-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fbf26-145">**[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="fbf26-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="fbf26-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="fbf26-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="fbf26-147">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Zoho uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="fbf26-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Zoho application.</span></span>

<span data-ttu-id="fbf26-148">**tooconfigure Azure AD çoklu oturum açma ile Zoho, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="fbf26-148">**tooconfigure Azure AD single sign-on with Zoho, perform hello following steps:**</span></span>

1. <span data-ttu-id="fbf26-149">Hello hello üzerinde Azure portal'ın **Zoho** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="fbf26-149">In hello Azure portal, on hello **Zoho** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. <span data-ttu-id="fbf26-151">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="fbf26-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_samlbase.png)

3. <span data-ttu-id="fbf26-153">Merhaba üzerinde **Zoho etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="fbf26-153">On hello **Zoho Domain and URLs** section, perform hello following steps:</span></span>

    ![Zoho etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_url.png)

    <span data-ttu-id="fbf26-155">a.</span><span class="sxs-lookup"><span data-stu-id="fbf26-155">a.</span></span> <span data-ttu-id="fbf26-156">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<company name>.zohomail.com`</span><span class="sxs-lookup"><span data-stu-id="fbf26-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.zohomail.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="fbf26-157">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="fbf26-157">This value is not real.</span></span> <span data-ttu-id="fbf26-158">Bu değer ile Merhaba güncelleştirme gerçek oturum açma URL'si.</span><span class="sxs-lookup"><span data-stu-id="fbf26-158">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="fbf26-159">Kişi [Zoho istemci destek ekibi](https://www.zoho.com/mail/contact.html) tooget bu değer.</span><span class="sxs-lookup"><span data-stu-id="fbf26-159">Contact [Zoho Client support team](https://www.zoho.com/mail/contact.html) tooget this value.</span></span> 
 
4. <span data-ttu-id="fbf26-160">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="fbf26-160">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_certificate.png) 

5. <span data-ttu-id="fbf26-162">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="fbf26-162">Click **Save** button.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="fbf26-164">Merhaba üzerinde **Zoho yapılandırma** 'yi tıklatın **yapılandırma Zoho** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="fbf26-164">On hello **Zoho Configuration** section, click **Configure Zoho** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="fbf26-165">Kopya hello **Sign-Out URL, değişiklik parola URL'si ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="fbf26-165">Copy hello **Sign-Out URL, Change Password URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Zoho yapılandırma](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_configure.png) 

7. <span data-ttu-id="fbf26-167">Farklı web tarayıcısı penceresinde Zoho posta şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="fbf26-167">In a different web browser window, log into your Zoho Mail company site as an administrator.</span></span>

8. <span data-ttu-id="fbf26-168">Toohello Git **Denetim Masası**.</span><span class="sxs-lookup"><span data-stu-id="fbf26-168">Go toohello **Control panel**.</span></span>
   
    <span data-ttu-id="fbf26-169">![Denetim Masası](./media/active-directory-saas-zoho-mail-tutorial/ic789607.png "Denetim Masası")</span><span class="sxs-lookup"><span data-stu-id="fbf26-169">![Control Panel](./media/active-directory-saas-zoho-mail-tutorial/ic789607.png "Control Panel")</span></span>

9. <span data-ttu-id="fbf26-170">Merhaba tıklatın **SAML kimlik doğrulaması** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="fbf26-170">Click hello **SAML Authentication** tab.</span></span>
   
    <span data-ttu-id="fbf26-171">![SAML kimlik doğrulaması](./media/active-directory-saas-zoho-mail-tutorial/ic789608.png "SAML kimlik doğrulaması")</span><span class="sxs-lookup"><span data-stu-id="fbf26-171">![SAML Authentication](./media/active-directory-saas-zoho-mail-tutorial/ic789608.png "SAML Authentication")</span></span>

10. <span data-ttu-id="fbf26-172">Merhaba, **SAML kimlik doğrulama ayrıntıları** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="fbf26-172">In hello **SAML Authentication Details** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="fbf26-173">![SAML kimlik doğrulama ayrıntıları](./media/active-directory-saas-zoho-mail-tutorial/ic789609.png "SAML kimlik doğrulama ayrıntıları")</span><span class="sxs-lookup"><span data-stu-id="fbf26-173">![SAML Authentication Details](./media/active-directory-saas-zoho-mail-tutorial/ic789609.png "SAML Authentication Details")</span></span>
   
    <span data-ttu-id="fbf26-174">a.</span><span class="sxs-lookup"><span data-stu-id="fbf26-174">a.</span></span> <span data-ttu-id="fbf26-175">Merhaba, **oturum açma URL'si** metin kutusuna, Yapıştır **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="fbf26-175">In hello **Login URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="fbf26-176">b.</span><span class="sxs-lookup"><span data-stu-id="fbf26-176">b.</span></span> <span data-ttu-id="fbf26-177">Merhaba, **oturum kapatma URL'si** metin kutusuna, Yapıştır **Sign-Out URL** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="fbf26-177">In hello **Logout URL** textbox, paste **Sign-Out URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="fbf26-178">c.</span><span class="sxs-lookup"><span data-stu-id="fbf26-178">c.</span></span> <span data-ttu-id="fbf26-179">Merhaba, **değişiklik parola URL'si** metin kutusuna, Yapıştır **değişiklik parola URL'si** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="fbf26-179">In hello **Change Password URL** textbox, paste **Change Password URL** which you have copied from Azure portal.</span></span>
       
    <span data-ttu-id="fbf26-180">d.</span><span class="sxs-lookup"><span data-stu-id="fbf26-180">d.</span></span> <span data-ttu-id="fbf26-181">Not Defteri'nde, kopyalama hello panonuza bunu içerik Azure portalından indirdiğiniz, base-64 kodlanmış sertifikasını açın ve ardından toohello yapıştırın **PublicKey** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="fbf26-181">Open your base-64 encoded certificate downloaded from Azure portal in notepad, copy hello content of it into your clipboard, and then paste it toohello **PublicKey** textbox.</span></span>
   
    <span data-ttu-id="fbf26-182">e.</span><span class="sxs-lookup"><span data-stu-id="fbf26-182">e.</span></span> <span data-ttu-id="fbf26-183">Olarak **algoritması**seçin **RSA**.</span><span class="sxs-lookup"><span data-stu-id="fbf26-183">As **Algorithm**, select **RSA**.</span></span>
   
    <span data-ttu-id="fbf26-184">f.</span><span class="sxs-lookup"><span data-stu-id="fbf26-184">f.</span></span> <span data-ttu-id="fbf26-185">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fbf26-185">Click **OK**.</span></span>

> [!TIP]
> <span data-ttu-id="fbf26-186">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="fbf26-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="fbf26-187">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="fbf26-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="fbf26-188">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fbf26-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="fbf26-189">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="fbf26-189">Create an Azure AD test user</span></span>

<span data-ttu-id="fbf26-190">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="fbf26-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="fbf26-192">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="fbf26-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="fbf26-193">Merhaba hello sol bölmede Azure portal hello tıklatın **Azure Active Directory** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="fbf26-193">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="fbf26-195">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="fbf26-195">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="fbf26-197">tooopen hello **kullanıcı** iletişim kutusu, tıklatın **Ekle** hello hello üstündeki **tüm kullanıcılar** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="fbf26-197">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Merhaba Ekle düğmesi](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="fbf26-199">Merhaba, **kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="fbf26-199">In hello **User** dialog box, perform hello following steps:</span></span>

    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_04.png)

    <span data-ttu-id="fbf26-201">a.</span><span class="sxs-lookup"><span data-stu-id="fbf26-201">a.</span></span> <span data-ttu-id="fbf26-202">Merhaba, **adı** kutusuna **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fbf26-202">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fbf26-203">b.</span><span class="sxs-lookup"><span data-stu-id="fbf26-203">b.</span></span> <span data-ttu-id="fbf26-204">Merhaba, **kullanıcı adı** kutusuna, kullanıcının Britta Simon hello e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="fbf26-204">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="fbf26-205">c.</span><span class="sxs-lookup"><span data-stu-id="fbf26-205">c.</span></span> <span data-ttu-id="fbf26-206">Select hello **Göster parola** onay kutusunu işaretleyin ve ardından hello görüntülenen hello değerini aşağı yazma **parola** kutusu.</span><span class="sxs-lookup"><span data-stu-id="fbf26-206">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="fbf26-207">d.</span><span class="sxs-lookup"><span data-stu-id="fbf26-207">d.</span></span> <span data-ttu-id="fbf26-208">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fbf26-208">Click **Create**.</span></span>
 
### <a name="create-a-zoho-test-user"></a><span data-ttu-id="fbf26-209">Zoho test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="fbf26-209">Create a Zoho test user</span></span>

<span data-ttu-id="fbf26-210">Zoho posta uygulamasına sipariş tooenable Azure AD kullanıcıların toolog bunlar Zoho postaya sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="fbf26-210">In order tooenable Azure AD users toolog into Zoho Mail, they must be provisioned into Zoho Mail.</span></span> <span data-ttu-id="fbf26-211">Zoho posta Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="fbf26-211">In hello case of Zoho Mail, provisioning is a manual task.</span></span>

> [!NOTE]
> <span data-ttu-id="fbf26-212">API AAD kullanıcı hesaplarının Zoho posta tooprovision tarafından sağlanan veya herhangi diğer Zoho posta kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fbf26-212">You can use any other Zoho Mail user account creation tools or APIs provided by Zoho Mail tooprovision AAD user accounts.</span></span>

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a><span data-ttu-id="fbf26-213">bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="fbf26-213">tooprovision a user account, perform hello following steps:</span></span>

1. <span data-ttu-id="fbf26-214">İçinde tooyour oturum **Zoho posta** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="fbf26-214">Log in tooyour **Zoho Mail** company site as an administrator.</span></span>

2. <span data-ttu-id="fbf26-215">Çok Git**Denetim Masası \> posta & belgeleri**.</span><span class="sxs-lookup"><span data-stu-id="fbf26-215">Go too**Control Panel \> Mail & Docs**.</span></span>

3. <span data-ttu-id="fbf26-216">Çok Git**kullanıcı ayrıntıları \> Kullanıcı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="fbf26-216">Go too**User Details \> Add User**.</span></span>
   
    <span data-ttu-id="fbf26-217">![Kullanıcı ekleme](./media/active-directory-saas-zoho-mail-tutorial/ic789611.png "kullanıcı ekleme")</span><span class="sxs-lookup"><span data-stu-id="fbf26-217">![Add User](./media/active-directory-saas-zoho-mail-tutorial/ic789611.png "Add User")</span></span>

4. <span data-ttu-id="fbf26-218">Merhaba üzerinde **kullanıcıları eklemek** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="fbf26-218">On hello **Add users** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="fbf26-219">![Kullanıcı ekleme](./media/active-directory-saas-zoho-mail-tutorial/ic789612.png "kullanıcı ekleme")</span><span class="sxs-lookup"><span data-stu-id="fbf26-219">![Add User](./media/active-directory-saas-zoho-mail-tutorial/ic789612.png "Add User")</span></span>
   
    <span data-ttu-id="fbf26-220">a.</span><span class="sxs-lookup"><span data-stu-id="fbf26-220">a.</span></span> <span data-ttu-id="fbf26-221">Merhaba, **ad** metin kutusuna, tür hello ilk gibi kullanıcı adını **Britta**.</span><span class="sxs-lookup"><span data-stu-id="fbf26-221">In hello **First Name** textbox, type hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="fbf26-222">b.</span><span class="sxs-lookup"><span data-stu-id="fbf26-222">b.</span></span> <span data-ttu-id="fbf26-223">Merhaba, **Soyadı** metin kutusuna, türü hello kullanıcının soyadını gibi **Simon**.</span><span class="sxs-lookup"><span data-stu-id="fbf26-223">In hello **Last Name** textbox, type hello last name of user like **Simon**.</span></span>

    <span data-ttu-id="fbf26-224">c.</span><span class="sxs-lookup"><span data-stu-id="fbf26-224">c.</span></span> <span data-ttu-id="fbf26-225">Merhaba, **e-posta kimliği** metin kutusuna, tür hello e-posta gibi kullanıcı kimliğini  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="fbf26-225">In hello **Email ID** textbox, type hello email id of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="fbf26-226">d.</span><span class="sxs-lookup"><span data-stu-id="fbf26-226">d.</span></span> <span data-ttu-id="fbf26-227">Merhaba, **parola** metin kutusu, kullanıcı parolasını girin.</span><span class="sxs-lookup"><span data-stu-id="fbf26-227">In hello **Password** textbox, enter password of user.</span></span>
   
    <span data-ttu-id="fbf26-228">e.</span><span class="sxs-lookup"><span data-stu-id="fbf26-228">e.</span></span> <span data-ttu-id="fbf26-229">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fbf26-229">Click **OK**.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="fbf26-230">etkin duruma gelmesi hello Azure Active Directory hesap sahibi bağlantı tooconfirm hello hesabı olan bir e-posta alırsınız.</span><span class="sxs-lookup"><span data-stu-id="fbf26-230">hello Azure Active Directory account holder will receive an email with a link tooconfirm hello account before it becomes active.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="fbf26-231">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="fbf26-231">Assign hello Azure AD test user</span></span>

<span data-ttu-id="fbf26-232">Bu bölümde, erişim tooZoho vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="fbf26-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooZoho.</span></span>

![Merhaba kullanıcı rolü atayın][200] 

<span data-ttu-id="fbf26-234">**tooassign Britta Simon tooZoho hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="fbf26-234">**tooassign Britta Simon tooZoho, perform hello following steps:**</span></span>

1. <span data-ttu-id="fbf26-235">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="fbf26-235">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="fbf26-237">Merhaba uygulamalar listesinde **Zoho**.</span><span class="sxs-lookup"><span data-stu-id="fbf26-237">In hello applications list, select **Zoho**.</span></span>

    ![Merhaba Zoho bağlantı hello uygulamalar listesinde](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_app.png)  

3. <span data-ttu-id="fbf26-239">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="fbf26-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202]

4. <span data-ttu-id="fbf26-241">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="fbf26-241">Click **Add** button.</span></span> <span data-ttu-id="fbf26-242">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="fbf26-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Merhaba eklemek atama bölmesi][203]

5. <span data-ttu-id="fbf26-244">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="fbf26-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="fbf26-245">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="fbf26-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fbf26-246">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="fbf26-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="fbf26-247">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="fbf26-247">Test single sign-on</span></span>

<span data-ttu-id="fbf26-248">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="fbf26-248">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="fbf26-249">Merhaba Zoho hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Zoho uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="fbf26-249">When you click hello Zoho tile in hello Access Panel, you should get automatically signed-on tooyour Zoho application.</span></span>
<span data-ttu-id="fbf26-250">Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="fbf26-250">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="fbf26-251">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="fbf26-251">Additional resources</span></span>

* [<span data-ttu-id="fbf26-252">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="fbf26-252">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fbf26-253">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="fbf26-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_203.png

