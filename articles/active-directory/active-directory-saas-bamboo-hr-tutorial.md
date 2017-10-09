---
title: "Öğretici: Azure Active Directory Tümleştirme ile BambooHR | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile BambooHR arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f826b5d2-9c64-47df-bbbf-0adf9eb0fa71
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: jeedes
ms.openlocfilehash: f9083f846beb3a4bf4cebbf18b42aba2dfef2472
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bamboohr"></a><span data-ttu-id="73986-103">Öğretici: Azure Active Directory Tümleştirme BambooHR ile</span><span class="sxs-lookup"><span data-stu-id="73986-103">Tutorial: Azure Active Directory integration with BambooHR</span></span>

<span data-ttu-id="73986-104">Bu öğreticide, bilgi nasıl toointegrate BambooHR Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="73986-104">In this tutorial, you learn how toointegrate BambooHR with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="73986-105">BambooHR Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="73986-105">Integrating BambooHR with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="73986-106">Erişim tooBambooHR sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="73986-106">You can control in Azure AD who has access tooBambooHR</span></span>
- <span data-ttu-id="73986-107">Kullanıcıların tooautomatically get açan tooBambooHR (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="73986-107">You can enable your users tooautomatically get signed-on tooBambooHR (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="73986-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="73986-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="73986-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="73986-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="73986-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="73986-110">Prerequisites</span></span>

<span data-ttu-id="73986-111">tooconfigure BambooHR ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="73986-111">tooconfigure Azure AD integration with BambooHR, you need hello following items:</span></span>

- <span data-ttu-id="73986-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="73986-112">An Azure AD subscription</span></span>
- <span data-ttu-id="73986-113">Bir BambooHR çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="73986-113">A BambooHR single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="73986-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="73986-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="73986-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="73986-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="73986-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="73986-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="73986-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="73986-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="73986-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="73986-118">Scenario description</span></span>
<span data-ttu-id="73986-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="73986-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="73986-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="73986-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="73986-121">Merhaba Galerisi'nden BambooHR ekleme</span><span class="sxs-lookup"><span data-stu-id="73986-121">Adding BambooHR from hello gallery</span></span>
2. <span data-ttu-id="73986-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="73986-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bamboohr-from-hello-gallery"></a><span data-ttu-id="73986-123">Merhaba Galerisi'nden BambooHR ekleme</span><span class="sxs-lookup"><span data-stu-id="73986-123">Adding BambooHR from hello gallery</span></span>
<span data-ttu-id="73986-124">Azure AD'ye tooconfigure hello tümleştirme BambooHR, tooadd BambooHR hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="73986-124">tooconfigure hello integration of BambooHR into Azure AD, you need tooadd BambooHR from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="73986-125">**tooadd BambooHR hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="73986-125">**tooadd BambooHR from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="73986-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="73986-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="73986-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="73986-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="73986-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="73986-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="73986-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="73986-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="73986-133">Merhaba arama kutusuna yazın **BambooHR**.</span><span class="sxs-lookup"><span data-stu-id="73986-133">In hello search box, type **BambooHR**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_search.png)

5. <span data-ttu-id="73986-135">Merhaba Sonuçlar panelinde seçin **BambooHR**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="73986-135">In hello results panel, select **BambooHR**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="73986-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="73986-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="73986-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı BambooHR ile test etme</span><span class="sxs-lookup"><span data-stu-id="73986-138">In this section, you configure and test Azure AD single sign-on with BambooHR based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="73986-139">Tek toowork'ın oturum açma hangi hello karşılık gelen BambooHR içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="73986-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BambooHR is tooa user in Azure AD.</span></span> <span data-ttu-id="73986-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı BambooHR hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="73986-140">In other words, a link relationship between an Azure AD user and hello related user in BambooHR needs toobe established.</span></span>

<span data-ttu-id="73986-141">Merhaba hello değeri BambooHR içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="73986-141">In BambooHR, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="73986-142">tooconfigure ve BambooHR ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="73986-142">tooconfigure and test Azure AD single sign-on with BambooHR, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="73986-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="73986-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="73986-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="73986-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="73986-145">**[BambooHR test kullanıcısı oluşturma](#creating-a-bamboohr-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir BambooHR içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="73986-145">**[Creating a BambooHR test user](#creating-a-bamboohr-test-user)** - toohave a counterpart of Britta Simon in BambooHR that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="73986-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="73986-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="73986-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="73986-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="73986-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="73986-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="73986-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma BambooHR uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="73986-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BambooHR application.</span></span>

<span data-ttu-id="73986-150">**tooconfigure Azure AD çoklu oturum açma ile BambooHR, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="73986-150">**tooconfigure Azure AD single sign-on with BambooHR, perform hello following steps:**</span></span>

1. <span data-ttu-id="73986-151">Hello hello üzerinde Azure portal'ın **BambooHR** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="73986-151">In hello Azure portal, on hello **BambooHR** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="73986-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="73986-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_samlbase.png)

3. <span data-ttu-id="73986-155">Merhaba üzerinde **BambooHR etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="73986-155">On hello **BambooHR Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_url.png)

    <span data-ttu-id="73986-157">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<company>.bamboohr.com`</span><span class="sxs-lookup"><span data-stu-id="73986-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company>.bamboohr.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="73986-158">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="73986-158">This value is not real.</span></span> <span data-ttu-id="73986-159">Bu değer ile Merhaba güncelleştirme gerçek oturum açma URL'si.</span><span class="sxs-lookup"><span data-stu-id="73986-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="73986-160">Kişi [BambooHR istemci destek ekibi](https://www.bamboohr.com/contact.php) tooget bu değer.</span><span class="sxs-lookup"><span data-stu-id="73986-160">Contact [BambooHR Client support team](https://www.bamboohr.com/contact.php) tooget this value.</span></span> 
 
4. <span data-ttu-id="73986-161">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="73986-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_certificate.png) 

5. <span data-ttu-id="73986-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="73986-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="73986-165">Merhaba üzerinde **BambooHR yapılandırma** 'yi tıklatın **yapılandırma BambooHR** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="73986-165">On hello **BambooHR Configuration** section, click **Configure BambooHR** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="73986-166">Kopya hello **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="73986-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_configure.png) 

6. <span data-ttu-id="73986-168">Farklı web tarayıcısı penceresinde BambooHR şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="73986-168">In a different web browser window, log into your BambooHR company site as an administrator.</span></span>

7. <span data-ttu-id="73986-169">Merhaba giriş sayfasında hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="73986-169">On hello homepage, perform hello following steps:</span></span>
   
    <span data-ttu-id="73986-170">![Çoklu oturum açma](./media/active-directory-saas-bamboo-hr-tutorial/ic796691.png "çoklu oturum açma")</span><span class="sxs-lookup"><span data-stu-id="73986-170">![Single Sign-On](./media/active-directory-saas-bamboo-hr-tutorial/ic796691.png "Single Sign-On")</span></span>   

    <span data-ttu-id="73986-171">a.</span><span class="sxs-lookup"><span data-stu-id="73986-171">a.</span></span> <span data-ttu-id="73986-172">Tıklatın **uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="73986-172">Click **Apps**.</span></span>
   
    <span data-ttu-id="73986-173">b.</span><span class="sxs-lookup"><span data-stu-id="73986-173">b.</span></span> <span data-ttu-id="73986-174">Merhaba uygulamaları menüsünde hello sol tıklayın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="73986-174">In hello apps menu on hello left, click **Single Sign-On**.</span></span>
   
    <span data-ttu-id="73986-175">c.</span><span class="sxs-lookup"><span data-stu-id="73986-175">c.</span></span> <span data-ttu-id="73986-176">Tıklatın **SAML çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="73986-176">Click **SAML Single Sign-On**.</span></span>

8. <span data-ttu-id="73986-177">Merhaba, **SAML çoklu oturum açma** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="73986-177">In hello **SAML Single Sign-On** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="73986-178">![SAML çoklu oturum açma](./media/active-directory-saas-bamboo-hr-tutorial/ic796692.png "SAML çoklu oturum açma")</span><span class="sxs-lookup"><span data-stu-id="73986-178">![SAML Single Sign-On](./media/active-directory-saas-bamboo-hr-tutorial/ic796692.png "SAML Single Sign-On")</span></span>
   
    <span data-ttu-id="73986-179">a.</span><span class="sxs-lookup"><span data-stu-id="73986-179">a.</span></span> <span data-ttu-id="73986-180">Yapıştır hello **SAML çoklu oturum açma hizmet URL'si** hello değerine **SSO oturum açma URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="73986-180">Paste hello **SAML Single Sign-On Service URL** value into hello **SSO Login Url** textbox.</span></span>
      
    <span data-ttu-id="73986-181">b.</span><span class="sxs-lookup"><span data-stu-id="73986-181">b.</span></span> <span data-ttu-id="73986-182">Not Defteri'nde, kopyalama hello panonuza bunu içerik Azure portalından indirdiğiniz base-64 kodlanmış sertifikasını açın ve toohello Yapıştır **X.509 sertifikası** metin kutusu</span><span class="sxs-lookup"><span data-stu-id="73986-182">Open base-64 encoded certificate downloaded from Azure portal in notepad, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox</span></span>
   
    <span data-ttu-id="73986-183">c.</span><span class="sxs-lookup"><span data-stu-id="73986-183">c.</span></span> <span data-ttu-id="73986-184">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="73986-184">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="73986-185">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="73986-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="73986-186">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="73986-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="73986-187">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="73986-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="73986-188">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="73986-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="73986-189">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="73986-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="73986-191">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="73986-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="73986-192">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="73986-192">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="73986-194">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="73986-194">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="73986-196">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="73986-196">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="73986-198">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="73986-198">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="73986-200">a.</span><span class="sxs-lookup"><span data-stu-id="73986-200">a.</span></span> <span data-ttu-id="73986-201">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="73986-201">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="73986-202">b.</span><span class="sxs-lookup"><span data-stu-id="73986-202">b.</span></span> <span data-ttu-id="73986-203">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="73986-203">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="73986-204">c.</span><span class="sxs-lookup"><span data-stu-id="73986-204">c.</span></span> <span data-ttu-id="73986-205">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="73986-205">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="73986-206">d.</span><span class="sxs-lookup"><span data-stu-id="73986-206">d.</span></span> <span data-ttu-id="73986-207">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="73986-207">Click **Create**.</span></span>
 
### <a name="creating-a-bamboohr-test-user"></a><span data-ttu-id="73986-208">BambooHR test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="73986-208">Creating a BambooHR test user</span></span>

<span data-ttu-id="73986-209">tooenable Azure AD kullanıcıların toolog tooBambooHR bunların BambooHR sağlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="73986-209">tooenable Azure AD users toolog in tooBambooHR, they must be provisioned into BambooHR.</span></span>  

<span data-ttu-id="73986-210">BambooHR Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="73986-210">In hello case of BambooHR, provisioning is a manual task.</span></span>

<span data-ttu-id="73986-211">**bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="73986-211">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="73986-212">İçinde tooyour oturum **BambooHR** yönetici olarak site.</span><span class="sxs-lookup"><span data-stu-id="73986-212">Log in tooyour **BambooHR** site as administrator.</span></span>

2. <span data-ttu-id="73986-213">Merhaba üstte Hello araç çubuğunda **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="73986-213">In hello toolbar on hello top, click **Settings**.</span></span>
   
    <span data-ttu-id="73986-214">![Ayarı](./media/active-directory-saas-bamboo-hr-tutorial/ic796694.png "ayarı")</span><span class="sxs-lookup"><span data-stu-id="73986-214">![Setting](./media/active-directory-saas-bamboo-hr-tutorial/ic796694.png "Setting")</span></span>

3. <span data-ttu-id="73986-215">Tıklatın **genel bakış**.</span><span class="sxs-lookup"><span data-stu-id="73986-215">Click **Overview**.</span></span>

4. <span data-ttu-id="73986-216">Merhaba sol gezinti bölmesinde, çok Git**güvenlik \> kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="73986-216">In hello left navigation pane, go too**Security \> Users**.</span></span>

5. <span data-ttu-id="73986-217">Metin kutuları türü hello kullanıcı adı, parola ve e-posta adresini hello tooprovision istediğiniz geçerli bir AAD hesabıyla ilgili.</span><span class="sxs-lookup"><span data-stu-id="73986-217">Type hello user name, password, and email address of a valid AAD account you want tooprovision into hello related textboxes.</span></span>

6. <span data-ttu-id="73986-218">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="73986-218">Click **Save**.</span></span>
        
>[!NOTE]
><span data-ttu-id="73986-219">API AAD kullanıcı hesaplarının BambooHR tooprovision tarafından sağlanan veya herhangi diğer BambooHR kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="73986-219">You can use any other BambooHR user account creation tools or APIs provided by BambooHR tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="73986-220">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="73986-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="73986-221">Bu bölümde, erişim tooBambooHR vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="73986-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBambooHR.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="73986-223">**tooassign Britta Simon tooBambooHR hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="73986-223">**tooassign Britta Simon tooBambooHR, perform hello following steps:**</span></span>

1. <span data-ttu-id="73986-224">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="73986-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="73986-226">Merhaba uygulamalar listesinde **BambooHR**.</span><span class="sxs-lookup"><span data-stu-id="73986-226">In hello applications list, select **BambooHR**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_app.png) 

3. <span data-ttu-id="73986-228">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="73986-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="73986-230">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="73986-230">Click **Add** button.</span></span> <span data-ttu-id="73986-231">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="73986-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="73986-233">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="73986-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="73986-234">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="73986-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="73986-235">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="73986-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="73986-236">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="73986-236">Testing single sign-on</span></span>

<span data-ttu-id="73986-237">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="73986-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="73986-238">Merhaba BambooHR hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour BambooHR uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="73986-238">When you click hello BambooHR tile in hello Access Panel, you should get automatically signed-on tooyour BambooHR application.</span></span>
<span data-ttu-id="73986-239">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="73986-239">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="73986-240">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="73986-240">Additional resources</span></span>

* [<span data-ttu-id="73986-241">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="73986-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="73986-242">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="73986-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_203.png

