---
title: "Öğretici: Azure Active Directory Tümleştirme ile Kintone | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Kintone arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2b947dc-e1a8-4f5f-b40e-2c5180648e4f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: 4f61fb95c643743504699b175beeff06e01c95c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kintone"></a><span data-ttu-id="a78ee-103">Öğretici: Azure Active Directory Tümleştirme Kintone ile</span><span class="sxs-lookup"><span data-stu-id="a78ee-103">Tutorial: Azure Active Directory integration with Kintone</span></span>

<span data-ttu-id="a78ee-104">Bu öğreticide, bilgi nasıl toointegrate Kintone Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a78ee-104">In this tutorial, you learn how toointegrate Kintone with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a78ee-105">Kintone Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="a78ee-105">Integrating Kintone with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a78ee-106">Erişim tooKintone sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="a78ee-106">You can control in Azure AD who has access tooKintone</span></span>
- <span data-ttu-id="a78ee-107">Kullanıcıların tooautomatically get açan tooKintone (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="a78ee-107">You can enable your users tooautomatically get signed-on tooKintone (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a78ee-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="a78ee-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a78ee-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a78ee-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a78ee-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="a78ee-110">Prerequisites</span></span>

<span data-ttu-id="a78ee-111">tooconfigure Kintone ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="a78ee-111">tooconfigure Azure AD integration with Kintone, you need hello following items:</span></span>

- <span data-ttu-id="a78ee-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="a78ee-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a78ee-113">Bir Kintone çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="a78ee-113">A Kintone single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a78ee-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="a78ee-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a78ee-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="a78ee-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a78ee-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="a78ee-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a78ee-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a78ee-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a78ee-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="a78ee-118">Scenario description</span></span>
<span data-ttu-id="a78ee-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="a78ee-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a78ee-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="a78ee-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a78ee-121">Merhaba Galerisi'nden Kintone ekleme</span><span class="sxs-lookup"><span data-stu-id="a78ee-121">Adding Kintone from hello gallery</span></span>
2. <span data-ttu-id="a78ee-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="a78ee-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kintone-from-hello-gallery"></a><span data-ttu-id="a78ee-123">Merhaba Galerisi'nden Kintone ekleme</span><span class="sxs-lookup"><span data-stu-id="a78ee-123">Adding Kintone from hello gallery</span></span>
<span data-ttu-id="a78ee-124">Azure AD'ye tooconfigure hello tümleştirme Kintone, tooadd Kintone hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="a78ee-124">tooconfigure hello integration of Kintone into Azure AD, you need tooadd Kintone from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a78ee-125">**tooadd Kintone hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a78ee-125">**tooadd Kintone from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a78ee-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="a78ee-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a78ee-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="a78ee-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a78ee-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="a78ee-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="a78ee-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a78ee-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="a78ee-133">Merhaba arama kutusuna yazın **Kintone**.</span><span class="sxs-lookup"><span data-stu-id="a78ee-133">In hello search box, type **Kintone**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_search.png)

5. <span data-ttu-id="a78ee-135">Merhaba Sonuçlar panelinde seçin **Kintone**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="a78ee-135">In hello results panel, select **Kintone**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a78ee-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="a78ee-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a78ee-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Kintone sınayın.</span><span class="sxs-lookup"><span data-stu-id="a78ee-138">In this section, you configure and test Azure AD single sign-on with Kintone based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a78ee-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Kintone içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="a78ee-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kintone is tooa user in Azure AD.</span></span> <span data-ttu-id="a78ee-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Kintone hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="a78ee-140">In other words, a link relationship between an Azure AD user and hello related user in Kintone needs toobe established.</span></span>

<span data-ttu-id="a78ee-141">Merhaba hello değeri Kintone içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="a78ee-141">In Kintone, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a78ee-142">tooconfigure ve Kintone ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="a78ee-142">tooconfigure and test Azure AD single sign-on with Kintone, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a78ee-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="a78ee-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a78ee-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="a78ee-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a78ee-145">**[Kintone test kullanıcısı oluşturma](#creating-a-kintone-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Kintone içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="a78ee-145">**[Creating a Kintone test user](#creating-a-kintone-test-user)** - toohave a counterpart of Britta Simon in Kintone that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a78ee-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="a78ee-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a78ee-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="a78ee-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a78ee-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a78ee-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a78ee-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Kintone uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="a78ee-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kintone application.</span></span>

<span data-ttu-id="a78ee-150">**tooconfigure Azure AD çoklu oturum açma ile Kintone, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a78ee-150">**tooconfigure Azure AD single sign-on with Kintone, perform hello following steps:**</span></span>

1. <span data-ttu-id="a78ee-151">Hello hello üzerinde Azure portal'ın **Kintone** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="a78ee-151">In hello Azure portal, on hello **Kintone** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="a78ee-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="a78ee-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_samlbase.png)

3. <span data-ttu-id="a78ee-155">Merhaba üzerinde **Kintone etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a78ee-155">On hello **Kintone Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_url.png)

    <span data-ttu-id="a78ee-157">a.</span><span class="sxs-lookup"><span data-stu-id="a78ee-157">a.</span></span> <span data-ttu-id="a78ee-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.kintone.com`</span><span class="sxs-lookup"><span data-stu-id="a78ee-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.kintone.com`</span></span>

    <span data-ttu-id="a78ee-159">b.</span><span class="sxs-lookup"><span data-stu-id="a78ee-159">b.</span></span> <span data-ttu-id="a78ee-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:</span><span class="sxs-lookup"><span data-stu-id="a78ee-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.cybozu.com`|
    | `https://<companyname>.kintone.com`|

    > [!NOTE] 
    > <span data-ttu-id="a78ee-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="a78ee-161">These values are not real.</span></span> <span data-ttu-id="a78ee-162">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="a78ee-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="a78ee-163">Kişi [Kintone istemci destek ekibi](https://www.kintone.com/contact/) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="a78ee-163">Contact [Kintone Client support team](https://www.kintone.com/contact/) tooget these values.</span></span> 
 
4. <span data-ttu-id="a78ee-164">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="a78ee-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_certificate.png) 

5. <span data-ttu-id="a78ee-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a78ee-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kintone-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a78ee-168">Merhaba üzerinde **Kintone yapılandırma** 'yi tıklatın **yapılandırma Kintone** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="a78ee-168">On hello **Kintone Configuration** section, click **Configure Kintone** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="a78ee-169">Kopya hello **Sign-Out URL ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="a78ee-169">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_configure.png) 

7. <span data-ttu-id="a78ee-171">Farklı web tarayıcısı penceresinde oturum açın, **Kintone** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="a78ee-171">In a different web browser window, log into your **Kintone** company site as an administrator.</span></span>

8. <span data-ttu-id="a78ee-172">Tıklatın **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="a78ee-172">Click **Settings**.</span></span>
   
    <span data-ttu-id="a78ee-173">![Ayarları](./media/active-directory-saas-kintone-tutorial/ic785879.png "ayarları")</span><span class="sxs-lookup"><span data-stu-id="a78ee-173">![Settings](./media/active-directory-saas-kintone-tutorial/ic785879.png "Settings")</span></span>

9. <span data-ttu-id="a78ee-174">Tıklatın **kullanıcılar ve sistem yönetimini**.</span><span class="sxs-lookup"><span data-stu-id="a78ee-174">Click **Users & System Administration**.</span></span>
   
    <span data-ttu-id="a78ee-175">![Kullanıcılar ve sistem yönetimini](./media/active-directory-saas-kintone-tutorial/ic785880.png "kullanıcılar ve Sistem Yönetimi")</span><span class="sxs-lookup"><span data-stu-id="a78ee-175">![Users & System Administration](./media/active-directory-saas-kintone-tutorial/ic785880.png "Users & System Administration")</span></span>

10. <span data-ttu-id="a78ee-176">Altında **Sistem Yönetimi \> güvenlik** tıklatın **oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="a78ee-176">Under **System Administration \> Security** click **Login**.</span></span>
   
    <span data-ttu-id="a78ee-177">![Oturum açma](./media/active-directory-saas-kintone-tutorial/ic785881.png "oturum açma")</span><span class="sxs-lookup"><span data-stu-id="a78ee-177">![Login](./media/active-directory-saas-kintone-tutorial/ic785881.png "Login")</span></span>

11. <span data-ttu-id="a78ee-178">Tıklatın **etkinleştirmek SAML kimlik doğrulaması**.</span><span class="sxs-lookup"><span data-stu-id="a78ee-178">Click **Enable SAML authentication**.</span></span>
   
    <span data-ttu-id="a78ee-179">![SAML kimlik doğrulaması](./media/active-directory-saas-kintone-tutorial/ic785882.png "SAML kimlik doğrulaması")</span><span class="sxs-lookup"><span data-stu-id="a78ee-179">![SAML Authentication](./media/active-directory-saas-kintone-tutorial/ic785882.png "SAML Authentication")</span></span>

12. <span data-ttu-id="a78ee-180">Hello SAML kimlik doğrulaması bölümü, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a78ee-180">In hello SAML Authentication section, perform hello following steps:</span></span>
    
    <span data-ttu-id="a78ee-181">![SAML kimlik doğrulaması](./media/active-directory-saas-kintone-tutorial/ic785883.png "SAML kimlik doğrulaması")</span><span class="sxs-lookup"><span data-stu-id="a78ee-181">![SAML Authentication](./media/active-directory-saas-kintone-tutorial/ic785883.png "SAML Authentication")</span></span>
    
    <span data-ttu-id="a78ee-182">a.</span><span class="sxs-lookup"><span data-stu-id="a78ee-182">a.</span></span> <span data-ttu-id="a78ee-183">Merhaba, **oturum açma URL'si** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="a78ee-183">In hello **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="a78ee-184">b.</span><span class="sxs-lookup"><span data-stu-id="a78ee-184">b.</span></span> <span data-ttu-id="a78ee-185">Merhaba, **oturum kapatma URL'si** metin kutusuna, Yapıştır hello değerini **Sign-Out URL** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="a78ee-185">In hello **Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="a78ee-186">c.</span><span class="sxs-lookup"><span data-stu-id="a78ee-186">c.</span></span> <span data-ttu-id="a78ee-187">Tıklatın **Gözat** tooupload indirilen sertifikanızı.</span><span class="sxs-lookup"><span data-stu-id="a78ee-187">Click **Browse** tooupload your downloaded certificate.</span></span>
    
    <span data-ttu-id="a78ee-188">d.</span><span class="sxs-lookup"><span data-stu-id="a78ee-188">d.</span></span> <span data-ttu-id="a78ee-189">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a78ee-189">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="a78ee-190">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="a78ee-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a78ee-191">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="a78ee-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a78ee-192">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a78ee-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a78ee-193">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a78ee-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="a78ee-194">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="a78ee-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="a78ee-196">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a78ee-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a78ee-197">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="a78ee-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kintone-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a78ee-199">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="a78ee-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kintone-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a78ee-201">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="a78ee-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kintone-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a78ee-203">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a78ee-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kintone-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a78ee-205">a.</span><span class="sxs-lookup"><span data-stu-id="a78ee-205">a.</span></span> <span data-ttu-id="a78ee-206">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a78ee-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a78ee-207">b.</span><span class="sxs-lookup"><span data-stu-id="a78ee-207">b.</span></span> <span data-ttu-id="a78ee-208">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="a78ee-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a78ee-209">c.</span><span class="sxs-lookup"><span data-stu-id="a78ee-209">c.</span></span> <span data-ttu-id="a78ee-210">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="a78ee-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a78ee-211">d.</span><span class="sxs-lookup"><span data-stu-id="a78ee-211">d.</span></span> <span data-ttu-id="a78ee-212">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a78ee-212">Click **Create**.</span></span>
 
### <a name="creating-a-kintone-test-user"></a><span data-ttu-id="a78ee-213">Kintone test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a78ee-213">Creating a Kintone test user</span></span>

<span data-ttu-id="a78ee-214">tooenable Azure AD kullanıcıların toolog tooKintone bunların Kintone sağlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a78ee-214">tooenable Azure AD users toolog in tooKintone, they must be provisioned into Kintone.</span></span>  
<span data-ttu-id="a78ee-215">Kintone Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="a78ee-215">In hello case of Kintone, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a><span data-ttu-id="a78ee-216">bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a78ee-216">tooprovision a user account, perform hello following steps:</span></span>

1. <span data-ttu-id="a78ee-217">İçinde tooyour oturum **Kintone** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="a78ee-217">Log in tooyour **Kintone** company site as an administrator.</span></span>

2. <span data-ttu-id="a78ee-218">Tıklatın **ayarı**.</span><span class="sxs-lookup"><span data-stu-id="a78ee-218">Click **Setting**.</span></span>
   
    <span data-ttu-id="a78ee-219">![Ayarları](./media/active-directory-saas-kintone-tutorial/ic785879.png "ayarları")</span><span class="sxs-lookup"><span data-stu-id="a78ee-219">![Settings](./media/active-directory-saas-kintone-tutorial/ic785879.png "Settings")</span></span>

3. <span data-ttu-id="a78ee-220">Tıklatın **kullanıcılar ve sistem yönetimini**.</span><span class="sxs-lookup"><span data-stu-id="a78ee-220">Click **Users & System Administration**.</span></span>
   
    <span data-ttu-id="a78ee-221">![Kullanıcı & Sistem Yönetimi](./media/active-directory-saas-kintone-tutorial/ic785880.png "kullanıcı & Sistem Yönetimi")</span><span class="sxs-lookup"><span data-stu-id="a78ee-221">![User & System Administration](./media/active-directory-saas-kintone-tutorial/ic785880.png "User & System Administration")</span></span>

4. <span data-ttu-id="a78ee-222">Altında **kullanıcı yönetimi**, tıklatın **Departmanlar k & ullanıcıların**.</span><span class="sxs-lookup"><span data-stu-id="a78ee-222">Under **User Administration**, click **Departments & Users**.</span></span>
   
    <span data-ttu-id="a78ee-223">![K & ullanıcıların departmanı](./media/active-directory-saas-kintone-tutorial/ic785888.png "departmanı ve kullanıcılar")</span><span class="sxs-lookup"><span data-stu-id="a78ee-223">![Department & Users](./media/active-directory-saas-kintone-tutorial/ic785888.png "Department & Users")</span></span>

5. <span data-ttu-id="a78ee-224">Tıklatın **yeni kullanıcı**.</span><span class="sxs-lookup"><span data-stu-id="a78ee-224">Click **New User**.</span></span>
   
    <span data-ttu-id="a78ee-225">![Yeni kullanıcılar](./media/active-directory-saas-kintone-tutorial/ic785889.png "yeni kullanıcılar")</span><span class="sxs-lookup"><span data-stu-id="a78ee-225">![New Users](./media/active-directory-saas-kintone-tutorial/ic785889.png "New Users")</span></span>

6. <span data-ttu-id="a78ee-226">Merhaba, **yeni kullanıcı** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a78ee-226">In hello **New User** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="a78ee-227">![Yeni kullanıcılar](./media/active-directory-saas-kintone-tutorial/ic785890.png "yeni kullanıcılar")</span><span class="sxs-lookup"><span data-stu-id="a78ee-227">![New Users](./media/active-directory-saas-kintone-tutorial/ic785890.png "New Users")</span></span>
   
    <span data-ttu-id="a78ee-228">a.</span><span class="sxs-lookup"><span data-stu-id="a78ee-228">a.</span></span> <span data-ttu-id="a78ee-229">Tür a **görünen adı**, **oturum açma adı**, **yeni parola**, **parolayı onaylayın**, **e-posta adresi**, ve ilgili diğer ayrıntıları hello tooprovision istediğiniz geçerli bir AAD hesabının metin kutuları.</span><span class="sxs-lookup"><span data-stu-id="a78ee-229">Type a **Display Name**, **Login Name**, **New Password**, **Confirm Password**, **E-mail Address**, and other details of a valid AAD account you want tooprovision into hello related textboxes.</span></span>
 
    <span data-ttu-id="a78ee-230">b.</span><span class="sxs-lookup"><span data-stu-id="a78ee-230">b.</span></span> <span data-ttu-id="a78ee-231">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a78ee-231">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="a78ee-232">API AAD kullanıcı hesaplarının Kintone tooprovision tarafından sağlanan veya herhangi diğer Kintone kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a78ee-232">You can use any other Kintone user account creation tools or APIs provided by Kintone tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a78ee-233">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="a78ee-233">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a78ee-234">Bu bölümde, erişim tooKintone vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="a78ee-234">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKintone.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="a78ee-236">**tooassign Britta Simon tooKintone hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a78ee-236">**tooassign Britta Simon tooKintone, perform hello following steps:**</span></span>

1. <span data-ttu-id="a78ee-237">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="a78ee-237">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="a78ee-239">Merhaba uygulamalar listesinde **Kintone**.</span><span class="sxs-lookup"><span data-stu-id="a78ee-239">In hello applications list, select **Kintone**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_app.png) 

3. <span data-ttu-id="a78ee-241">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="a78ee-241">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="a78ee-243">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a78ee-243">Click **Add** button.</span></span> <span data-ttu-id="a78ee-244">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="a78ee-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="a78ee-246">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="a78ee-246">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a78ee-247">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="a78ee-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a78ee-248">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="a78ee-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a78ee-249">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="a78ee-249">Testing single sign-on</span></span>

<span data-ttu-id="a78ee-250">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="a78ee-250">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a78ee-251">Merhaba Kintone hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Kintone uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a78ee-251">When you click hello Kintone tile in hello Access Panel, you should get automatically signed-on tooyour Kintone application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a78ee-252">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="a78ee-252">Additional resources</span></span>

* [<span data-ttu-id="a78ee-253">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="a78ee-253">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a78ee-254">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="a78ee-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_203.png

