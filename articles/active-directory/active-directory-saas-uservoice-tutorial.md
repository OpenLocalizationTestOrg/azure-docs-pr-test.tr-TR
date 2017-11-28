---
title: "Öğretici: Azure Active Directory Tümleştirme ile UserVoice | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile UserVoice arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 684a405b-8932-46f6-b43a-4d97a42b6b87
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.openlocfilehash: 9eade8435ae6c6a3821bbbec9ab7c27ed7ad91ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-uservoice"></a><span data-ttu-id="5a2df-103">Öğretici: Azure Active Directory Tümleştirme UserVoice ile</span><span class="sxs-lookup"><span data-stu-id="5a2df-103">Tutorial: Azure Active Directory integration with UserVoice</span></span>

<span data-ttu-id="5a2df-104">Bu öğreticide, bilgi nasıl toointegrate UserVoice Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5a2df-104">In this tutorial, you learn how toointegrate UserVoice with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5a2df-105">UserVoice Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="5a2df-105">Integrating UserVoice with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5a2df-106">Erişim tooUserVoice sahip Azure AD'de kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5a2df-106">You can control in Azure AD who has access tooUserVoice.</span></span>
- <span data-ttu-id="5a2df-107">Kullanıcıların tooautomatically get açan tooUserVoice (çoklu oturum açma) Azure AD hesaplarına ile etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5a2df-107">You can enable your users tooautomatically get signed-on tooUserVoice (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="5a2df-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="5a2df-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="5a2df-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5a2df-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5a2df-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="5a2df-110">Prerequisites</span></span>

<span data-ttu-id="5a2df-111">tooconfigure UserVoice ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="5a2df-111">tooconfigure Azure AD integration with UserVoice, you need hello following items:</span></span>

- <span data-ttu-id="5a2df-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="5a2df-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5a2df-113">Bir UserVoice çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="5a2df-113">A UserVoice single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5a2df-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="5a2df-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5a2df-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="5a2df-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5a2df-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="5a2df-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5a2df-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5a2df-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5a2df-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="5a2df-118">Scenario description</span></span>
<span data-ttu-id="5a2df-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="5a2df-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5a2df-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="5a2df-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5a2df-121">UserVoice hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="5a2df-121">Adding UserVoice from hello gallery</span></span>
2. <span data-ttu-id="5a2df-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="5a2df-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-uservoice-from-hello-gallery"></a><span data-ttu-id="5a2df-123">UserVoice hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="5a2df-123">Adding UserVoice from hello gallery</span></span>
<span data-ttu-id="5a2df-124">Azure AD'ye tooconfigure hello tümleştirme UserVoice, tooadd UserVoice hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="5a2df-124">tooconfigure hello integration of UserVoice into Azure AD, you need tooadd UserVoice from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5a2df-125">**tooadd UserVoice hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="5a2df-125">**tooadd UserVoice from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5a2df-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="5a2df-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory düğmesi][1]

2. <span data-ttu-id="5a2df-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="5a2df-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5a2df-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="5a2df-129">Then go too**All applications**.</span></span>

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="5a2df-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="5a2df-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Merhaba yeni uygulama düğmesi][3]

4. <span data-ttu-id="5a2df-133">Merhaba arama kutusuna yazın **UserVoice**seçin **UserVoice** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="5a2df-133">In hello search box, type **UserVoice**, select **UserVoice** from result panel then click **Add** button tooadd hello application.</span></span>

    ![UserVoice hello sonuçları listesinde](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="5a2df-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="5a2df-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="5a2df-136">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı UserVoice sınayın.</span><span class="sxs-lookup"><span data-stu-id="5a2df-136">In this section, you configure and test Azure AD single sign-on with UserVoice based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5a2df-137">Tek toowork'ın oturum açma hangi hello karşılık gelen UserVoice içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="5a2df-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in UserVoice is tooa user in Azure AD.</span></span> <span data-ttu-id="5a2df-138">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı UserVoice hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="5a2df-138">In other words, a link relationship between an Azure AD user and hello related user in UserVoice needs toobe established.</span></span>

<span data-ttu-id="5a2df-139">UserVoice içinde hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="5a2df-139">In UserVoice, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5a2df-140">tooconfigure ve UserVoice ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="5a2df-140">tooconfigure and test Azure AD single sign-on with UserVoice, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5a2df-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="5a2df-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5a2df-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="5a2df-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5a2df-143">**[UserVoice test kullanıcısı oluşturma](#create-a-uservoice-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir UserVoice içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="5a2df-143">**[Create a UserVoice test user](#create-a-uservoice-test-user)** - toohave a counterpart of Britta Simon in UserVoice that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5a2df-144">**[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="5a2df-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5a2df-145">**[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="5a2df-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="5a2df-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="5a2df-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="5a2df-147">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma UserVoice uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="5a2df-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your UserVoice application.</span></span>

<span data-ttu-id="5a2df-148">**tooconfigure Azure AD çoklu oturum açma ile UserVoice, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="5a2df-148">**tooconfigure Azure AD single sign-on with UserVoice, perform hello following steps:**</span></span>

1. <span data-ttu-id="5a2df-149">Hello hello üzerinde Azure portal'ın **UserVoice** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="5a2df-149">In hello Azure portal, on hello **UserVoice** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. <span data-ttu-id="5a2df-151">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="5a2df-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_samlbase.png)

3. <span data-ttu-id="5a2df-153">Merhaba üzerinde **UserVoice etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="5a2df-153">On hello **UserVoice Domain and URLs** section, perform hello following steps:</span></span>

    ![UserVoice etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_url.png)

    <span data-ttu-id="5a2df-155">a.</span><span class="sxs-lookup"><span data-stu-id="5a2df-155">a.</span></span> <span data-ttu-id="5a2df-156">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<tenantname>.UserVoice.com`</span><span class="sxs-lookup"><span data-stu-id="5a2df-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenantname>.UserVoice.com`</span></span>

    <span data-ttu-id="5a2df-157">b.</span><span class="sxs-lookup"><span data-stu-id="5a2df-157">b.</span></span> <span data-ttu-id="5a2df-158">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<tenantname>.UserVoice.com`</span><span class="sxs-lookup"><span data-stu-id="5a2df-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenantname>.UserVoice.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5a2df-159">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="5a2df-159">These values are not real.</span></span> <span data-ttu-id="5a2df-160">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="5a2df-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="5a2df-161">Kişi [UserVoice istemci destek ekibi](https://www.uservoice.com/) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="5a2df-161">Contact [UserVoice Client support team](https://www.uservoice.com/) tooget these values.</span></span>

4. <span data-ttu-id="5a2df-162">Merhaba üzerinde **SAML imzalama sertifikası** bölümü, kopyalama hello **parmak İZİ** sertifika değeri.</span><span class="sxs-lookup"><span data-stu-id="5a2df-162">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_certificate.png) 

5. <span data-ttu-id="5a2df-164">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="5a2df-164">Click **Save** button.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-uservoice-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5a2df-166">Merhaba üzerinde **UserVoice yapılandırma** 'yi tıklatın **yapılandırma UserVoice** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="5a2df-166">On hello **UserVoice Configuration** section, click **Configure UserVoice** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="5a2df-167">Kopya hello **Sign-Out URL ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="5a2df-167">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![UserVoice yapılandırma](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_configure.png) 

7. <span data-ttu-id="5a2df-169">Farklı web tarayıcısı penceresinde tooyour UserVoice şirket sitede yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="5a2df-169">In a different web browser window, log in tooyour UserVoice company site as an administrator.</span></span>

8. <span data-ttu-id="5a2df-170">Merhaba üstte Hello araç çubuğunda **ayarları**ve ardından **Web portalı** hello menüsünde.</span><span class="sxs-lookup"><span data-stu-id="5a2df-170">In hello toolbar on hello top, click **Settings**, and then select **Web portal** from hello menu.</span></span>
   
    <span data-ttu-id="5a2df-171">![Uygulama tarafında ayarları bölümünde](./media/active-directory-saas-uservoice-tutorial/ic777519.png "ayarları")</span><span class="sxs-lookup"><span data-stu-id="5a2df-171">![Settings Section On App Side](./media/active-directory-saas-uservoice-tutorial/ic777519.png "Settings")</span></span>

9. <span data-ttu-id="5a2df-172">Merhaba üzerinde **Web portalı** sekmede hello **kullanıcı kimlik doğrulaması** 'yi tıklatın **Düzenle** tooopen hello **kullanıcı kimlik doğrulamasını Düzenle** iletişim Sayfa.</span><span class="sxs-lookup"><span data-stu-id="5a2df-172">On hello **Web portal** tab, in hello **User authentication** section, click **Edit** tooopen hello **Edit User Authentication** dialog page.</span></span>
   
    <span data-ttu-id="5a2df-173">![Web portalı sekmesini](./media/active-directory-saas-uservoice-tutorial/ic777520.png "Web portalı")</span><span class="sxs-lookup"><span data-stu-id="5a2df-173">![Web portal Tab](./media/active-directory-saas-uservoice-tutorial/ic777520.png "Web portal")</span></span>

10. <span data-ttu-id="5a2df-174">Merhaba üzerinde **kullanıcı kimlik doğrulamasını Düzenle** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="5a2df-174">On hello **Edit User Authentication** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="5a2df-175">![Kullanıcı kimlik doğrulamasını Düzenle](./media/active-directory-saas-uservoice-tutorial/ic777521.png "düzenleme kullanıcı kimlik doğrulaması")</span><span class="sxs-lookup"><span data-stu-id="5a2df-175">![Edit user authentication](./media/active-directory-saas-uservoice-tutorial/ic777521.png "Edit user authentication")</span></span>
   
    <span data-ttu-id="5a2df-176">a.</span><span class="sxs-lookup"><span data-stu-id="5a2df-176">a.</span></span> <span data-ttu-id="5a2df-177">Tıklatın **çoklu oturum açma (SSO)**.</span><span class="sxs-lookup"><span data-stu-id="5a2df-177">Click **Single Sign-On (SSO)**.</span></span>
 
    <span data-ttu-id="5a2df-178">b.</span><span class="sxs-lookup"><span data-stu-id="5a2df-178">b.</span></span> <span data-ttu-id="5a2df-179">Yapıştır hello **SAML çoklu oturum açma hizmet URL'si** hello hello Azure portal ' kopyaladığınız değeri **SSO uzaktan oturum açma** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="5a2df-179">Paste hello **SAML Single Sign-On Service URL** value, which you have copied from hello Azure portal into hello **SSO Remote Sign-In** textbox.</span></span>

    <span data-ttu-id="5a2df-180">c.</span><span class="sxs-lookup"><span data-stu-id="5a2df-180">c.</span></span> <span data-ttu-id="5a2df-181">Yapıştır hello **Sign-Out URL** hello hello Azure portal ' kopyaladığınız değeri **SSO uzak Sign-Out textbox**.</span><span class="sxs-lookup"><span data-stu-id="5a2df-181">Paste hello **Sign-Out URL** value, which you have copied from hello Azure portal into hello **SSO Remote Sign-Out textbox**.</span></span>
 
    <span data-ttu-id="5a2df-182">d.</span><span class="sxs-lookup"><span data-stu-id="5a2df-182">d.</span></span> <span data-ttu-id="5a2df-183">Yapıştır hello **parmak izi** Azure portalından kopyaladığınız değeri **geçerli SHA1 sertifika parmak izi** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="5a2df-183">Paste hello **Thumbprint** value , which you have copied from Azure portal  into the **Current certificate SHA1 fingerprint** textbox.</span></span>
    
    <span data-ttu-id="5a2df-184">e.</span><span class="sxs-lookup"><span data-stu-id="5a2df-184">e.</span></span> <span data-ttu-id="5a2df-185">Tıklatın **kimlik doğrulama ayarlarını Kaydet**.</span><span class="sxs-lookup"><span data-stu-id="5a2df-185">Click **Save authentication settings**.</span></span>

> [!TIP]
> <span data-ttu-id="5a2df-186">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="5a2df-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5a2df-187">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="5a2df-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5a2df-188">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5a2df-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="5a2df-189">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5a2df-189">Create an Azure AD test user</span></span>

<span data-ttu-id="5a2df-190">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="5a2df-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="5a2df-192">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="5a2df-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5a2df-193">Merhaba hello sol bölmede Azure portal hello tıklatın **Azure Active Directory** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="5a2df-193">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-uservoice-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="5a2df-195">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="5a2df-195">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-uservoice-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="5a2df-197">tooopen hello **kullanıcı** iletişim kutusu, tıklatın **Ekle** hello hello üstündeki **tüm kullanıcılar** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="5a2df-197">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Merhaba Ekle düğmesi](./media/active-directory-saas-uservoice-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="5a2df-199">Merhaba, **kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="5a2df-199">In hello **User** dialog box, perform hello following steps:</span></span>

    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-uservoice-tutorial/create_aaduser_04.png)

    <span data-ttu-id="5a2df-201">a.</span><span class="sxs-lookup"><span data-stu-id="5a2df-201">a.</span></span> <span data-ttu-id="5a2df-202">Merhaba, **adı** kutusuna **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5a2df-202">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5a2df-203">b.</span><span class="sxs-lookup"><span data-stu-id="5a2df-203">b.</span></span> <span data-ttu-id="5a2df-204">Merhaba, **kullanıcı adı** kutusuna, kullanıcının Britta Simon hello e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="5a2df-204">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="5a2df-205">c.</span><span class="sxs-lookup"><span data-stu-id="5a2df-205">c.</span></span> <span data-ttu-id="5a2df-206">Select hello **Göster parola** onay kutusunu işaretleyin ve ardından hello görüntülenen hello değerini aşağı yazma **parola** kutusu.</span><span class="sxs-lookup"><span data-stu-id="5a2df-206">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="5a2df-207">d.</span><span class="sxs-lookup"><span data-stu-id="5a2df-207">d.</span></span> <span data-ttu-id="5a2df-208">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5a2df-208">Click **Create**.</span></span>
 
### <a name="create-a-uservoice-test-user"></a><span data-ttu-id="5a2df-209">UserVoice test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5a2df-209">Create a UserVoice test user</span></span>

<span data-ttu-id="5a2df-210">tooenable Azure AD kullanıcıların toolog tooUserVoice bunların UserVoice sağlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5a2df-210">tooenable Azure AD users toolog in tooUserVoice, they must be provisioned into UserVoice.</span></span> <span data-ttu-id="5a2df-211">UserVoice Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="5a2df-211">In hello case of UserVoice, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a><span data-ttu-id="5a2df-212">bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="5a2df-212">tooprovision a user account, perform hello following steps:</span></span>
1. <span data-ttu-id="5a2df-213">İçinde tooyour oturum **UserVoice** Kiracı.</span><span class="sxs-lookup"><span data-stu-id="5a2df-213">Log in tooyour **UserVoice** tenant.</span></span>

2. <span data-ttu-id="5a2df-214">Çok Git**ayarları**.</span><span class="sxs-lookup"><span data-stu-id="5a2df-214">Go too**Settings**.</span></span>
   
    <span data-ttu-id="5a2df-215">![Ayarları](./media/active-directory-saas-uservoice-tutorial/ic777811.png "ayarları")</span><span class="sxs-lookup"><span data-stu-id="5a2df-215">![Settings](./media/active-directory-saas-uservoice-tutorial/ic777811.png "Settings")</span></span>

3. <span data-ttu-id="5a2df-216">Tıklatın **genel**.</span><span class="sxs-lookup"><span data-stu-id="5a2df-216">Click **General**.</span></span>

4. <span data-ttu-id="5a2df-217">Tıklatın **aracıları ve izinleri**.</span><span class="sxs-lookup"><span data-stu-id="5a2df-217">Click **Agents and permissions**.</span></span>
   
    <span data-ttu-id="5a2df-218">![Aracılar ve izinleri](./media/active-directory-saas-uservoice-tutorial/ic777812.png "aracıları ve izinleri")</span><span class="sxs-lookup"><span data-stu-id="5a2df-218">![Agents and permissions](./media/active-directory-saas-uservoice-tutorial/ic777812.png "Agents and permissions")</span></span>

5. <span data-ttu-id="5a2df-219">Tıklatın **yöneticileri ekleyin**.</span><span class="sxs-lookup"><span data-stu-id="5a2df-219">Click **Add admins**.</span></span>
   
    <span data-ttu-id="5a2df-220">![Yöneticileri ekleyin](./media/active-directory-saas-uservoice-tutorial/ic777813.png "yöneticileri ekleyin")</span><span class="sxs-lookup"><span data-stu-id="5a2df-220">![Add admins](./media/active-directory-saas-uservoice-tutorial/ic777813.png "Add admins")</span></span>

6. <span data-ttu-id="5a2df-221">Merhaba üzerinde **davet admins** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="5a2df-221">On hello **Invite admins** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="5a2df-222">![Yöneticileri davet](./media/active-directory-saas-uservoice-tutorial/ic777814.png "davet yöneticileri")</span><span class="sxs-lookup"><span data-stu-id="5a2df-222">![Invite admins](./media/active-directory-saas-uservoice-tutorial/ic777814.png "Invite admins")</span></span>
   
    <span data-ttu-id="5a2df-223">a.</span><span class="sxs-lookup"><span data-stu-id="5a2df-223">a.</span></span> <span data-ttu-id="5a2df-224">Merhaba e-postaları metin kutusuna tooprovision istediğiniz ve ardından hello hesap hello e-posta adresini yazın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="5a2df-224">In hello Emails textbox, type hello email address of hello account you want tooprovision, and then click **Add**.</span></span>
   
    <span data-ttu-id="5a2df-225">b.</span><span class="sxs-lookup"><span data-stu-id="5a2df-225">b.</span></span> <span data-ttu-id="5a2df-226">Tıklatın **davet**.</span><span class="sxs-lookup"><span data-stu-id="5a2df-226">Click **Invite**.</span></span>

> [!NOTE]
> <span data-ttu-id="5a2df-227">API AAD kullanıcı hesaplarının UserVoice tooprovision tarafından sağlanan veya herhangi diğer UserVoice kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5a2df-227">You can use any other UserVoice user account creation tools or APIs provided by UserVoice tooprovision AAD user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="5a2df-228">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="5a2df-228">Assign hello Azure AD test user</span></span>

<span data-ttu-id="5a2df-229">Bu bölümde, erişim tooUserVoice vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="5a2df-229">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooUserVoice.</span></span>

![Merhaba kullanıcı rolü atayın][200] 

<span data-ttu-id="5a2df-231">**tooassign Britta Simon tooUserVoice hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="5a2df-231">**tooassign Britta Simon tooUserVoice, perform hello following steps:**</span></span>

1. <span data-ttu-id="5a2df-232">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="5a2df-232">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="5a2df-234">Merhaba uygulamalar listesinde **UserVoice**.</span><span class="sxs-lookup"><span data-stu-id="5a2df-234">In hello applications list, select **UserVoice**.</span></span>

    ![Merhaba UserVoice bağlantı hello uygulamalar listesinde](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_app.png)  

3. <span data-ttu-id="5a2df-236">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="5a2df-236">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202]

4. <span data-ttu-id="5a2df-238">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="5a2df-238">Click **Add** button.</span></span> <span data-ttu-id="5a2df-239">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="5a2df-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Merhaba eklemek atama bölmesi][203]

5. <span data-ttu-id="5a2df-241">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="5a2df-241">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5a2df-242">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="5a2df-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5a2df-243">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="5a2df-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="5a2df-244">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="5a2df-244">Test single sign-on</span></span>

<span data-ttu-id="5a2df-245">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="5a2df-245">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="5a2df-246">Merhaba UserVoice hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour UserVoice uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5a2df-246">When you click hello UserVoice tile in hello Access Panel, you should get automatically signed-on tooyour UserVoice application.</span></span>
<span data-ttu-id="5a2df-247">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5a2df-247">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="5a2df-248">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="5a2df-248">Additional resources</span></span>

* [<span data-ttu-id="5a2df-249">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="5a2df-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5a2df-250">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="5a2df-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_203.png

