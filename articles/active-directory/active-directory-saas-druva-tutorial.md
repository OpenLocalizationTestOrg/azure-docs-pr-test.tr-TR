---
title: "Öğretici: Azure Active Directory Tümleştirme ile Druva | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Druva arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ab92b600-1fea-4905-b1c7-ef8e4d8c495c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: a1c36c06d6d005e0aa363fbf34efe630e4cca1ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-druva"></a><span data-ttu-id="eb458-103">Öğretici: Azure Active Directory Tümleştirme Druva ile</span><span class="sxs-lookup"><span data-stu-id="eb458-103">Tutorial: Azure Active Directory integration with Druva</span></span>

<span data-ttu-id="eb458-104">Bu öğreticide, bilgi nasıl toointegrate Druva Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="eb458-104">In this tutorial, you learn how toointegrate Druva with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="eb458-105">Druva Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="eb458-105">Integrating Druva with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="eb458-106">Erişim tooDruva sahip Azure AD'de kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eb458-106">You can control in Azure AD who has access tooDruva.</span></span>
- <span data-ttu-id="eb458-107">Kullanıcıların tooautomatically get açan tooDruva (çoklu oturum açma) Azure AD hesaplarına ile etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eb458-107">You can enable your users tooautomatically get signed-on tooDruva (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="eb458-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="eb458-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="eb458-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="eb458-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eb458-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="eb458-110">Prerequisites</span></span>

<span data-ttu-id="eb458-111">tooconfigure Druva ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="eb458-111">tooconfigure Azure AD integration with Druva, you need hello following items:</span></span>

- <span data-ttu-id="eb458-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="eb458-112">An Azure AD subscription</span></span>
- <span data-ttu-id="eb458-113">Bir Druva çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="eb458-113">A Druva single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="eb458-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="eb458-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="eb458-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="eb458-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="eb458-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="eb458-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="eb458-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="eb458-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="eb458-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="eb458-118">Scenario description</span></span>
<span data-ttu-id="eb458-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="eb458-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="eb458-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="eb458-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="eb458-121">Merhaba Galerisi'nden Druva ekleme</span><span class="sxs-lookup"><span data-stu-id="eb458-121">Adding Druva from hello gallery</span></span>
2. <span data-ttu-id="eb458-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="eb458-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-druva-from-hello-gallery"></a><span data-ttu-id="eb458-123">Merhaba Galerisi'nden Druva ekleme</span><span class="sxs-lookup"><span data-stu-id="eb458-123">Adding Druva from hello gallery</span></span>
<span data-ttu-id="eb458-124">Azure AD'ye tooconfigure hello tümleştirme Druva, tooadd Druva hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="eb458-124">tooconfigure hello integration of Druva into Azure AD, you need tooadd Druva from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="eb458-125">**tooadd Druva hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="eb458-125">**tooadd Druva from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="eb458-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="eb458-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory düğmesi][1]

2. <span data-ttu-id="eb458-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="eb458-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="eb458-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="eb458-129">Then go too**All applications**.</span></span>

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="eb458-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="eb458-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Merhaba yeni uygulama düğmesi][3]

4. <span data-ttu-id="eb458-133">Merhaba arama kutusuna yazın **Druva**seçin **Druva** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="eb458-133">In hello search box, type **Druva**, select **Druva** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Merhaba sonuçları listesinde Druva](./media/active-directory-saas-druva-tutorial/tutorial_druva_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="eb458-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="eb458-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="eb458-136">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Druva sınayın.</span><span class="sxs-lookup"><span data-stu-id="eb458-136">In this section, you configure and test Azure AD single sign-on with Druva based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="eb458-137">Tek toowork'ın oturum açma hangi hello karşılık gelen Druva içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="eb458-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Druva is tooa user in Azure AD.</span></span> <span data-ttu-id="eb458-138">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Druva hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="eb458-138">In other words, a link relationship between an Azure AD user and hello related user in Druva needs toobe established.</span></span>

<span data-ttu-id="eb458-139">Merhaba hello değeri Druva içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="eb458-139">In Druva, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="eb458-140">tooconfigure ve Druva ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="eb458-140">tooconfigure and test Azure AD single sign-on with Druva, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="eb458-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="eb458-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="eb458-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="eb458-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="eb458-143">**[Druva test kullanıcısı oluşturma](#create-a-druva-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Druva içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="eb458-143">**[Create a Druva test user](#create-a-druva-test-user)** - toohave a counterpart of Britta Simon in Druva that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="eb458-144">**[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="eb458-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="eb458-145">**[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="eb458-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="eb458-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="eb458-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="eb458-147">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Druva uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="eb458-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Druva application.</span></span>

<span data-ttu-id="eb458-148">**tooconfigure Azure AD çoklu oturum açma ile Druva, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="eb458-148">**tooconfigure Azure AD single sign-on with Druva, perform hello following steps:**</span></span>

1. <span data-ttu-id="eb458-149">Hello hello üzerinde Azure portal'ın **Druva** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="eb458-149">In hello Azure portal, on hello **Druva** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. <span data-ttu-id="eb458-151">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="eb458-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-druva-tutorial/tutorial_druva_samlbase.png)

3. <span data-ttu-id="eb458-153">Merhaba üzerinde **Druva etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="eb458-153">On hello **Druva Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-druva-tutorial/tutorial_druva_url.png)

    <span data-ttu-id="eb458-155">Merhaba, **oturum açma URL'si** metin kutusuna, türü hello URL'si:`https://cloud.druva.com/home`</span><span class="sxs-lookup"><span data-stu-id="eb458-155">In hello **Sign-on URL** textbox, type hello URL: `https://cloud.druva.com/home`</span></span>

4. <span data-ttu-id="eb458-156">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="eb458-156">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-druva-tutorial/tutorial_druva_certificate.png) 

5. <span data-ttu-id="eb458-158">Druva uygulamanızı hello SAML onaylar tooadd özel öznitelik eşlemelerini tooyour gerektiren belirli bir biçimde, bekliyor **SAML belirteci öznitelikleri** yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="eb458-158">Your Druva application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour **SAML Token Attributes** configuration.</span></span> 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-druva-tutorial/tutorial_druva_attribute.png)

6. <span data-ttu-id="eb458-160">Merhaba, **kullanıcı öznitelikleri** hello bölüm **çoklu oturum açma** iletişim kutusunda, SAML belirteci özniteliği görüntü önceki hello gösterildiği gibi yapılandırmak ve hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="eb458-160">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello preceding image and perform hello following steps:</span></span>

    | <span data-ttu-id="eb458-161">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="eb458-161">Attribute Name</span></span>      | <span data-ttu-id="eb458-162">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="eb458-162">Attribute Value</span></span>      |
    | ------------------- | -------------------- |
    | <span data-ttu-id="eb458-163">insync\_auth\_belirteci</span><span class="sxs-lookup"><span data-stu-id="eb458-163">insync\_auth\_token</span></span> |<span data-ttu-id="eb458-164">Merhaba belirteç oluşturulan değerini girin</span><span class="sxs-lookup"><span data-stu-id="eb458-164">Enter hello token generated value</span></span> |
    
    <span data-ttu-id="eb458-165">a.</span><span class="sxs-lookup"><span data-stu-id="eb458-165">a.</span></span> <span data-ttu-id="eb458-166">Tıklatın **Ekle özniteliği** tooopen hello **özniteliği eklemek** iletişim.</span><span class="sxs-lookup"><span data-stu-id="eb458-166">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-druva-tutorial/tutorial_attribute_04.png)
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-druva-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="eb458-169">b.</span><span class="sxs-lookup"><span data-stu-id="eb458-169">b.</span></span> <span data-ttu-id="eb458-170">Merhaba, **adı** metin kutusuna, ilgili satır için gösterilen türü hello öznitelik adı.</span><span class="sxs-lookup"><span data-stu-id="eb458-170">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="eb458-171">c.</span><span class="sxs-lookup"><span data-stu-id="eb458-171">c.</span></span> <span data-ttu-id="eb458-172">Merhaba gelen **değeri** listesinde, ilgili satır için gösterilen türü hello öznitelik değeri.</span><span class="sxs-lookup"><span data-stu-id="eb458-172">From hello **Value** list, type hello attribute value shown for that row.</span></span> <span data-ttu-id="eb458-173">Merhaba belirteç oluşturulan değerini daha sonra öğreticide açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="eb458-173">hello token generated value is explained later in tutorial.</span></span>
    
    <span data-ttu-id="eb458-174">d.</span><span class="sxs-lookup"><span data-stu-id="eb458-174">d.</span></span> <span data-ttu-id="eb458-175">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="eb458-175">Click **Ok**.</span></span>    

7. <span data-ttu-id="eb458-176">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="eb458-176">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-druva-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="eb458-178">Merhaba üzerinde **Druva yapılandırma** 'yi tıklatın **yapılandırma Druva** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="eb458-178">On hello **Druva Configuration** section, click **Configure Druva** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="eb458-179">Kopya hello **Sign-Out URL ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="eb458-179">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-druva-tutorial/tutorial_druva_configure.png) 

9. <span data-ttu-id="eb458-181">Farklı web tarayıcısı penceresinde tooyour Druva şirket sitede yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="eb458-181">In a different web browser window, log in tooyour Druva company site as an administrator.</span></span>

10. <span data-ttu-id="eb458-182">Çok Git**Yönet \> ayarları**.</span><span class="sxs-lookup"><span data-stu-id="eb458-182">Go too**Manage \> Settings**.</span></span>

    <span data-ttu-id="eb458-183">![Ayarları](./media/active-directory-saas-druva-tutorial/ic795091.png "ayarları")</span><span class="sxs-lookup"><span data-stu-id="eb458-183">![Settings](./media/active-directory-saas-druva-tutorial/ic795091.png "Settings")</span></span>

11. <span data-ttu-id="eb458-184">Merhaba çoklu oturum açma ayarları iletişim kutusunda hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="eb458-184">On hello Single Sign-On Settings dialog, perform hello following steps:</span></span>

    <span data-ttu-id="eb458-185">![Çoklu oturum açma ayarları](./media/active-directory-saas-druva-tutorial/ic795092.png "tek oturum açma ayarları")</span><span class="sxs-lookup"><span data-stu-id="eb458-185">![Single Sign-On Settings](./media/active-directory-saas-druva-tutorial/ic795092.png "Single Sign-On Settings")</span></span>
    
    <span data-ttu-id="eb458-186">a.</span><span class="sxs-lookup"><span data-stu-id="eb458-186">a.</span></span> <span data-ttu-id="eb458-187">Yapıştır **SAML çoklu oturum açma hizmet URL'si** hello hello Azure portal ' kopyaladığınız değeri **kimlik sağlayıcısı oturum açma URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="eb458-187">Paste **SAML Single Sign-On Service URL** value, which you have copied from hello Azure portal into hello **ID Provider Login URL** textbox.</span></span>
    
    <span data-ttu-id="eb458-188">b.</span><span class="sxs-lookup"><span data-stu-id="eb458-188">b.</span></span> <span data-ttu-id="eb458-189">Yapıştır **Sign-Out URL** hello hello Azure portal ' kopyaladığınız değeri **kimlik sağlayıcısı oturum kapatma URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="eb458-189">Paste **Sign-Out URL** value, which you have copied from hello Azure portal into hello **ID Provider Logout URL** textbox.</span></span>
    
     <span data-ttu-id="eb458-190">c.</span><span class="sxs-lookup"><span data-stu-id="eb458-190">c.</span></span> <span data-ttu-id="eb458-191">Base-64 kodlanmış sertifikanızı kopyalama hello panonuza bunu içerik Not Defteri'nde açın ve toohello yapıştırın **kimlik sağlayıcısının sertifikasını** metin kutusu</span><span class="sxs-lookup"><span data-stu-id="eb458-191">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **ID Provider Certificate** textbox</span></span>
     
     <span data-ttu-id="eb458-192">d.</span><span class="sxs-lookup"><span data-stu-id="eb458-192">d.</span></span> <span data-ttu-id="eb458-193">tooopen hello **ayarları** sayfasında, **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="eb458-193">tooopen hello **Settings** page, click **Save**.</span></span>

12. <span data-ttu-id="eb458-194">Merhaba üzerinde **ayarları** sayfasında, **SSO belirteç Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="eb458-194">On hello **Settings** page, click **Generate SSO Token**.</span></span>

    <span data-ttu-id="eb458-195">![Ayarları](./media/active-directory-saas-druva-tutorial/ic795093.png "ayarları")</span><span class="sxs-lookup"><span data-stu-id="eb458-195">![Settings](./media/active-directory-saas-druva-tutorial/ic795093.png "Settings")</span></span>

13. <span data-ttu-id="eb458-196">Merhaba üzerinde **tek oturum açma kimlik doğrulaması belirteci** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="eb458-196">On hello **Single Sign-on Authentication Token** dialog, perform hello following steps:</span></span>

    <span data-ttu-id="eb458-197">![SSO belirteci](./media/active-directory-saas-druva-tutorial/ic795094.png "SSO belirteci")</span><span class="sxs-lookup"><span data-stu-id="eb458-197">![SSO Token](./media/active-directory-saas-druva-tutorial/ic795094.png "SSO Token")</span></span>
    
    <span data-ttu-id="eb458-198">a.</span><span class="sxs-lookup"><span data-stu-id="eb458-198">a.</span></span> <span data-ttu-id="eb458-199">Tıklatın **kopyalama**, Yapıştır kopyaladığınız değeri hello **değeri** metin kutusuna hello **özniteliği eklemek** bölümü.</span><span class="sxs-lookup"><span data-stu-id="eb458-199">Click **Copy**, Paste copied value in hello **Value** textbox in hello **Add Attribute** section.</span></span>
    
    <span data-ttu-id="eb458-200">b.</span><span class="sxs-lookup"><span data-stu-id="eb458-200">b.</span></span> <span data-ttu-id="eb458-201">**Kapat**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="eb458-201">Click **Close**.</span></span>

> [!TIP]
> <span data-ttu-id="eb458-202">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="eb458-202">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="eb458-203">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="eb458-203">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="eb458-204">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="eb458-204">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="eb458-205">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="eb458-205">Create an Azure AD test user</span></span>

<span data-ttu-id="eb458-206">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="eb458-206">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="eb458-208">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="eb458-208">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="eb458-209">Merhaba hello sol bölmede Azure portal hello tıklatın **Azure Active Directory** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="eb458-209">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-druva-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="eb458-211">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="eb458-211">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-druva-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="eb458-213">tooopen hello **kullanıcı** iletişim kutusu, tıklatın **Ekle** hello hello üstündeki **tüm kullanıcılar** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="eb458-213">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Merhaba Ekle düğmesi](./media/active-directory-saas-druva-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="eb458-215">Merhaba, **kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="eb458-215">In hello **User** dialog box, perform hello following steps:</span></span>

    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-druva-tutorial/create_aaduser_04.png)

    <span data-ttu-id="eb458-217">a.</span><span class="sxs-lookup"><span data-stu-id="eb458-217">a.</span></span> <span data-ttu-id="eb458-218">Merhaba, **adı** kutusuna **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="eb458-218">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="eb458-219">b.</span><span class="sxs-lookup"><span data-stu-id="eb458-219">b.</span></span> <span data-ttu-id="eb458-220">Merhaba, **kullanıcı adı** kutusuna, kullanıcının Britta Simon hello e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="eb458-220">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="eb458-221">c.</span><span class="sxs-lookup"><span data-stu-id="eb458-221">c.</span></span> <span data-ttu-id="eb458-222">Select hello **Göster parola** onay kutusunu işaretleyin ve ardından hello görüntülenen hello değerini aşağı yazma **parola** kutusu.</span><span class="sxs-lookup"><span data-stu-id="eb458-222">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="eb458-223">d.</span><span class="sxs-lookup"><span data-stu-id="eb458-223">d.</span></span> <span data-ttu-id="eb458-224">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="eb458-224">Click **Create**.</span></span>
 
### <a name="create-a-druva-test-user"></a><span data-ttu-id="eb458-225">Druva test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="eb458-225">Create a Druva test user</span></span>

<span data-ttu-id="eb458-226">TooDruva içinde sipariş tooenable Azure AD kullanıcıların toolog bunların Druva sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="eb458-226">In order tooenable Azure AD users toolog in tooDruva, they must be provisioned into Druva.</span></span> <span data-ttu-id="eb458-227">Druva Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="eb458-227">In hello case of Druva, provisioning is a manual task.</span></span>

<span data-ttu-id="eb458-228">**tooconfigure kullanıcı hazırlama, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="eb458-228">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="eb458-229">İçinde tooyour oturum **Druva** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="eb458-229">Log in tooyour **Druva** company site as administrator.</span></span>

2. <span data-ttu-id="eb458-230">Çok Git**Yönet \> kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="eb458-230">Go too**Manage \> Users**.</span></span>
   
   <span data-ttu-id="eb458-231">![Kullanıcıları yönetme](./media/active-directory-saas-druva-tutorial/ic795097.png "kullanıcıları yönetme")</span><span class="sxs-lookup"><span data-stu-id="eb458-231">![Manage Users](./media/active-directory-saas-druva-tutorial/ic795097.png "Manage Users")</span></span>

3. <span data-ttu-id="eb458-232">Tıklatın **Yeni Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="eb458-232">Click **Create New**.</span></span>
   
   <span data-ttu-id="eb458-233">![Kullanıcıları yönetme](./media/active-directory-saas-druva-tutorial/ic795098.png "kullanıcıları yönetme")</span><span class="sxs-lookup"><span data-stu-id="eb458-233">![Manage Users](./media/active-directory-saas-druva-tutorial/ic795098.png "Manage Users")</span></span>

4. <span data-ttu-id="eb458-234">Merhaba yeni kullanıcı oluştur iletişim kutusunda hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="eb458-234">On hello Create New User dialog, perform hello following steps:</span></span>
   
   <span data-ttu-id="eb458-235">![NewUser oluşturma](./media/active-directory-saas-druva-tutorial/ic795099.png "NewUser oluşturma")</span><span class="sxs-lookup"><span data-stu-id="eb458-235">![Create NewUser](./media/active-directory-saas-druva-tutorial/ic795099.png "Create NewUser")</span></span>
   
   <span data-ttu-id="eb458-236">a.</span><span class="sxs-lookup"><span data-stu-id="eb458-236">a.</span></span> <span data-ttu-id="eb458-237">Merhaba, **e-posta adresi** metin kutusuna, bir kullanıcı gibi hello e-posta girin  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="eb458-237">In hello **Email address** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>
   
   <span data-ttu-id="eb458-238">b.</span><span class="sxs-lookup"><span data-stu-id="eb458-238">b.</span></span> <span data-ttu-id="eb458-239">Merhaba, **adı** metin kutusuna, bir kullanıcı gibi hello adını girin **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="eb458-239">In hello **Name** textbox, enter hello name of user like **BrittaSimon**.</span></span>
   
   <span data-ttu-id="eb458-240">c.</span><span class="sxs-lookup"><span data-stu-id="eb458-240">c.</span></span> <span data-ttu-id="eb458-241">Tıklatın **kullanıcı oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="eb458-241">Click **Create User**.</span></span>

>[!NOTE]
><span data-ttu-id="eb458-242">API'leri, Azure AD kullanıcı hesapları Druva tooprovision tarafından sağlanan veya herhangi diğer Druva kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eb458-242">You can use any other Druva user account creation tools or APIs provided by Druva tooprovision Azure AD user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="eb458-243">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="eb458-243">Assign hello Azure AD test user</span></span>

<span data-ttu-id="eb458-244">Bu bölümde, erişim tooDruva vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="eb458-244">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDruva.</span></span>

![Merhaba kullanıcı rolü atayın][200] 

<span data-ttu-id="eb458-246">**tooassign Britta Simon tooDruva hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="eb458-246">**tooassign Britta Simon tooDruva, perform hello following steps:**</span></span>

1. <span data-ttu-id="eb458-247">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="eb458-247">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="eb458-249">Merhaba uygulamalar listesinde **Druva**.</span><span class="sxs-lookup"><span data-stu-id="eb458-249">In hello applications list, select **Druva**.</span></span>

    ![Merhaba Druva bağlantı hello uygulamalar listesinde](./media/active-directory-saas-druva-tutorial/tutorial_druva_app.png)  

3. <span data-ttu-id="eb458-251">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="eb458-251">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202]

4. <span data-ttu-id="eb458-253">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="eb458-253">Click **Add** button.</span></span> <span data-ttu-id="eb458-254">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="eb458-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Merhaba eklemek atama bölmesi][203]

5. <span data-ttu-id="eb458-256">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="eb458-256">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="eb458-257">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="eb458-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="eb458-258">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="eb458-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="eb458-259">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="eb458-259">Test single sign-on</span></span>

<span data-ttu-id="eb458-260">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="eb458-260">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="eb458-261">Merhaba Druva hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Druva uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="eb458-261">When you click hello Druva tile in hello Access Panel, you should get automatically signed-on tooyour Druva application.</span></span>
<span data-ttu-id="eb458-262">Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="eb458-262">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="eb458-263">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="eb458-263">Additional resources</span></span>

* [<span data-ttu-id="eb458-264">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="eb458-264">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="eb458-265">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="eb458-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-druva-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-druva-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-druva-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-druva-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-druva-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-druva-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-druva-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-druva-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-druva-tutorial/tutorial_general_203.png

