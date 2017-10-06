---
title: "Öğretici: Azure Active Directory Tümleştirme ile çalışma alanına Facebook tarafından | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve Facebook ile çalışma alanına arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 30f2ee64-95d3-44ef-b832-8a0a27e2967c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: f71a59527394730757d501a973251dc293fd3683
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workplace-by-facebook"></a><span data-ttu-id="45694-103">Öğretici: Facebook ile çalışma alanına Azure Active Directory Tümleştirme</span><span class="sxs-lookup"><span data-stu-id="45694-103">Tutorial: Azure Active Directory integration with Workplace by Facebook</span></span>

<span data-ttu-id="45694-104">Bu öğreticide, bilgi nasıl toointegrate Facebook ile Azure Active Directory (Azure AD) ile çalışma.</span><span class="sxs-lookup"><span data-stu-id="45694-104">In this tutorial, you learn how toointegrate Workplace by Facebook with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="45694-105">Çalışma alanına Facebook ile Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="45694-105">Integrating Workplace by Facebook with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="45694-106">Facebook tarafından erişim tooWorkplace sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="45694-106">You can control in Azure AD who has access tooWorkplace by Facebook</span></span>
- <span data-ttu-id="45694-107">Kullanıcıların tooautomatically get açan tooWorkplace Facebook (çoklu oturum açma) tarafından kendi Azure AD hesapları ile etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="45694-107">You can enable your users tooautomatically get signed-on tooWorkplace by Facebook (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="45694-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="45694-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="45694-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="45694-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="45694-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="45694-110">Prerequisites</span></span>

<span data-ttu-id="45694-111">Facebook ile çalışma alanına ile Azure AD tümleştirme tooconfigure, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="45694-111">tooconfigure Azure AD integration with Workplace by Facebook, you need hello following items:</span></span>

- <span data-ttu-id="45694-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="45694-112">An Azure AD subscription</span></span>
- <span data-ttu-id="45694-113">Abonelik çalışma alanına Facebook çoklu oturum açma tarafından etkin</span><span class="sxs-lookup"><span data-stu-id="45694-113">A Workplace by Facebook single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="45694-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="45694-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="45694-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="45694-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="45694-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="45694-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="45694-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="45694-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="45694-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="45694-118">Scenario description</span></span>
<span data-ttu-id="45694-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="45694-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="45694-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="45694-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="45694-121">Facebook ile çalışma alanına hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="45694-121">Adding Workplace by Facebook from hello gallery</span></span>
2. <span data-ttu-id="45694-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="45694-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workplace-by-facebook-from-hello-gallery"></a><span data-ttu-id="45694-123">Facebook ile çalışma alanına hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="45694-123">Adding Workplace by Facebook from hello gallery</span></span>
<span data-ttu-id="45694-124">Azure AD'ye tooconfigure hello tümleştirme çalışma alanı Facebook tarafından tooadd Facebook ile çalışma alanına hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="45694-124">tooconfigure hello integration of Workplace by Facebook into Azure AD, you need tooadd Workplace by Facebook from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="45694-125">**tooadd çalışma alanına hello galerisinden Facebook tarafından hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="45694-125">**tooadd Workplace by Facebook from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="45694-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="45694-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="45694-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="45694-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="45694-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="45694-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="45694-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="45694-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="45694-133">Merhaba arama kutusuna yazın **Facebook ile çalışma alanına**.</span><span class="sxs-lookup"><span data-stu-id="45694-133">In hello search box, type **Workplace by Facebook**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_search.png)

5. <span data-ttu-id="45694-135">Merhaba Sonuçlar panelinde seçin **Facebook ile çalışma alanına**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="45694-135">In hello results panel, select **Workplace by Facebook**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="45694-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="45694-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="45694-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma ile çalışma alanına Facebook "Britta Simon." olarak adlandırılan bir test kullanıcıya bağlı olarak test etme</span><span class="sxs-lookup"><span data-stu-id="45694-138">In this section, you configure and test Azure AD single sign-on with Workplace by Facebook based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="45694-139">Tek toowork'ın oturum açma hangi hello karşılık gelen çalışma Facebook tarafından tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="45694-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Workplace by Facebook is tooa user in Azure AD.</span></span> <span data-ttu-id="45694-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve Facebook ile çalışma hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="45694-140">In other words, a link relationship between an Azure AD user and hello related user in Workplace by Facebook needs toobe established.</span></span>

<span data-ttu-id="45694-141">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcı adı** Facebook ile çalışma.</span><span class="sxs-lookup"><span data-stu-id="45694-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Workplace by Facebook.</span></span>

<span data-ttu-id="45694-142">tooconfigure ve Facebook ile çalışma alanına ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="45694-142">tooconfigure and test Azure AD single sign-on with Workplace by Facebook, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="45694-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="45694-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="45694-144">**[Yeniden kimlik doğrulamanın sıklığını yapılandırma](#configuring-reauthentication-frequency)**  -tooconfigure çalışma alanına tooprompt SAML olmadığını kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="45694-144">**[Configuring Reauthentication Frequency](#configuring-reauthentication-frequency)** - tooconfigure Workplace tooprompt for a SAML check.</span></span>
3. <span data-ttu-id="45694-145">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="45694-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="45694-146">**[Facebook test kullanıcı tarafından bir çalışma alanı oluşturma](#creating-a-workplace-by-facebook-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Facebook tarafından çalışma, karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="45694-146">**[Creating a Workplace by Facebook test user](#creating-a-workplace-by-facebook-test-user)** - toohave a counterpart of Britta Simon in Workplace by Facebook that is linked toohello Azure AD representation of user.</span></span>
5. <span data-ttu-id="45694-147">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="45694-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
6. <span data-ttu-id="45694-148">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="45694-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="45694-149">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="45694-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="45694-150">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Facebook uygulama tarafından çalışma alanınızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="45694-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Workplace by Facebook application.</span></span>

<span data-ttu-id="45694-151">**tooconfigure Azure AD çoklu oturum açma ile çalışma alanına Facebook tarafından hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="45694-151">**tooconfigure Azure AD single sign-on with Workplace by Facebook, perform hello following steps:**</span></span>

1. <span data-ttu-id="45694-152">Merhaba hello üzerinde Azure portal'ın **Facebook ile çalışma alanına** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="45694-152">In hello Azure portal, on hello **Workplace by Facebook** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="45694-154">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="45694-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_samlbase.png)

3. <span data-ttu-id="45694-156">Merhaba üzerinde **Facebook etki alanı ve URL'ler ile çalışma alanına** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="45694-156">On hello **Workplace by Facebook Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_url.png)

    <span data-ttu-id="45694-158">a.</span><span class="sxs-lookup"><span data-stu-id="45694-158">a.</span></span> <span data-ttu-id="45694-159">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<instancename>.facebook.com`</span><span class="sxs-lookup"><span data-stu-id="45694-159">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<instancename>.facebook.com`</span></span>

    <span data-ttu-id="45694-160">b.</span><span class="sxs-lookup"><span data-stu-id="45694-160">b.</span></span> <span data-ttu-id="45694-161">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://www.facebook.com/company/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="45694-161">In hello **Identifier** textbox, type a URL using hello following pattern: `https://www.facebook.com/company/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="45694-162">Bu değerler hello gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="45694-162">These values are not hello real.</span></span> <span data-ttu-id="45694-163">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="45694-163">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="45694-164">Kişi [Facebook istemcisini destek ekibi ile çalışma alanına](https://workplace.fb.com/faq/) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="45694-164">Contact [Workplace by Facebook Client support team](https://workplace.fb.com/faq/) tooget these values.</span></span> 

4. <span data-ttu-id="45694-165">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="45694-165">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_certificate.png) 

5. <span data-ttu-id="45694-167">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="45694-167">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="45694-169">Merhaba üzerinde **Facebook yapılandırmaya göre çalışma alanına** 'yi tıklatın **yapılandırma çalışma Facebook tarafından** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="45694-169">On hello **Workplace by Facebook Configuration** section, click **Configure Workplace by Facebook** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="45694-170">Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="45694-170">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-workplacebyfacebook-tutorial/config.png) 

7. <span data-ttu-id="45694-172">Bir farklı web tarayıcısı penceresinde, oturum açma tooyour yönetici olarak Facebook şirket site tarafından çalışma alanı.</span><span class="sxs-lookup"><span data-stu-id="45694-172">In a different web browser window, login tooyour Workplace by Facebook company site as an administrator.</span></span>
  
   > [!NOTE] 
   > <span data-ttu-id="45694-173">Merhaba SAML kimlik doğrulama işleminin bir parçası olarak, çalışma alanına sorgu dizelerini too2.5 sipariş toopass parametreleri tooAzure AD boyutu kilobayt yukarı değerlendirebilir.</span><span class="sxs-lookup"><span data-stu-id="45694-173">As part of hello SAML authentication process, Workplace may utilize query strings of up too2.5 kilobytes in size in order toopass parameters tooAzure AD.</span></span>

8. <span data-ttu-id="45694-174">Merhaba, **şirket Pano**, Git toohello **kimlik doğrulaması** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="45694-174">In hello **Company Dashboard**, go toohello **Authentication** tab.</span></span>

9. <span data-ttu-id="45694-175">Altında **SAML kimlik doğrulaması**seçin **yalnızca SSO** hello aşağı açılan listeden.</span><span class="sxs-lookup"><span data-stu-id="45694-175">Under **SAML Authentication**, select **SSO Only** from hello drop-down list.</span></span>

10. <span data-ttu-id="45694-176">Kopyalanan giriş hello değerleri **Facebook yapılandırmaya göre çalışma alanına** hello hello karşılık gelen alanlara Azure portalı bölümünde:</span><span class="sxs-lookup"><span data-stu-id="45694-176">Input hello values copied from **Workplace by Facebook Configuration** section of hello Azure portal into hello corresponding fields:</span></span>

    *   <span data-ttu-id="45694-177">İçinde **SAML URL** metin kutusuna, Yapıştır hello değerini **çoklu oturum açma hizmet URL'si**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="45694-177">In **SAML URL** textbox, paste hello value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    *   <span data-ttu-id="45694-178">İçinde **SAML veren URL'si metin kutusuna**, hello değerini yapıştırın **SAML varlık kimliği**, hangi Azure portalından kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="45694-178">In **SAML Issuer URL textbox**, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>
    *   <span data-ttu-id="45694-179">İçinde **SAML oturum kapatma yönlendirme** (isteğe bağlı) hello değerini yapıştırın **Sign-Out URL**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="45694-179">In **SAML Logout Redirect** (Optional), paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>
    *   <span data-ttu-id="45694-180">Açık, **base-64 kodlamalı sertifika** Azure portalından indirdiğiniz Defteri'nde Merhaba içeriğine, panoya kopyalayın ve toothe Yapıştır **SAML sertifika** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="45694-180">Open your **base-64 encoded certificate** in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toothe **SAML Certificate** textbox.</span></span>

11. <span data-ttu-id="45694-181">Tooenter hello İzleyici URL alıcı URL gerekebilir ve ACS (onaylama tüketici hizmeti) URL hello altında listelenen **SAML Yapılandırması** bölümü.</span><span class="sxs-lookup"><span data-stu-id="45694-181">You may need tooenter hello Audience URL, Recipient URL, and ACS (Assertion Consumer Service) URL listed under hello **SAML Configuration** section.</span></span>

12. <span data-ttu-id="45694-182">Merhaba bölümünün toohello altına kaydırın ve hello tıklatın **Test SSO** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="45694-182">Scroll toohello bottom of hello section and click hello **Test SSO** button.</span></span> <span data-ttu-id="45694-183">Bu sonuç ile Azure AD oturum açma sayfası görünen açılır pencerede sunulur.</span><span class="sxs-lookup"><span data-stu-id="45694-183">This results in a popup window appearing with Azure AD login page presented.</span></span> <span data-ttu-id="45694-184">Kimlik bilgilerinizi normal tooauthenticate girin.</span><span class="sxs-lookup"><span data-stu-id="45694-184">Enter your credentials in as normal tooauthenticate.</span></span> 

    <span data-ttu-id="45694-185">**Sorun giderme:** olun hello e-posta adresi geri Azure AD'den döndürülen iş yeri hesabı ile oturum hello aynı hello olduğu.</span><span class="sxs-lookup"><span data-stu-id="45694-185">**Troubleshooting:** Ensure hello email address being returned back from Azure AD is hello same as hello Workplace account you are logged in with.</span></span>

13. <span data-ttu-id="45694-186">Merhaba test başarıyla tamamlandıktan sonra hello sayfanın toohello'e gidin ve hello tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="45694-186">Once hello test has been completed successfully, scroll toohello bottom of hello page and click hello **Save** button.</span></span>

14. <span data-ttu-id="45694-187">Çalışma alanına kullanan tüm kullanıcıların kimlik doğrulaması için Azure AD oturum açma sayfası artık sunulur.</span><span class="sxs-lookup"><span data-stu-id="45694-187">All users using Workplace will now be presented with Azure AD login page for authentication.</span></span>

15. <span data-ttu-id="45694-188">**SAML oturum kapatma yeniden yönlendir (isteğe bağlı)** -</span><span class="sxs-lookup"><span data-stu-id="45694-188">**SAML Logout Redirect (optional)** -</span></span> 

    <span data-ttu-id="45694-189">Seçebileceğiniz toooptionally Azure AD oturum kapatma sayfasını kullanılan toopoint olabilen bir SAML oturum kapatma URL'si yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="45694-189">You can choose toooptionally configure a SAML Logout Url, which can be used toopoint at Azure AD's logout page.</span></span> <span data-ttu-id="45694-190">Bu ayar etkin ve yapılandırılmış durumda olduğunda hello kullanıcı artık yönlendirilmiş toohello çalışma alanına oturum kapatma sayfasının olacaktır.</span><span class="sxs-lookup"><span data-stu-id="45694-190">When this setting is enabled and configured, hello user will no longer be directed toohello Workplace logout page.</span></span> <span data-ttu-id="45694-191">Bunun yerine, hello kullanıcı hello SAML oturum kapatma yönlendirme ayarında eklendi yeniden yönlendirilen toohello url olacaktır.</span><span class="sxs-lookup"><span data-stu-id="45694-191">Instead, hello user will be redirected toohello url that was added in hello SAML Logout Redirect setting.</span></span>


> [!TIP]
> <span data-ttu-id="45694-192">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="45694-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="45694-193">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="45694-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="45694-194">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="45694-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="configuring-reauthentication-frequency"></a><span data-ttu-id="45694-195">Yeniden kimlik doğrulamanın sıklığını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="45694-195">Configuring Reauthentication Frequency</span></span>

<span data-ttu-id="45694-196">SAML onay günde üç gün, hafta, iki hafta, ay için çalışma alanına tooprompt yapılandırabilirsiniz ya da hiç.</span><span class="sxs-lookup"><span data-stu-id="45694-196">You can configure Workplace tooprompt for a SAML check every day, three days, week, two weeks, month or never.</span></span>

> [!NOTE] 
><span data-ttu-id="45694-197">Merhaba mobil uygulamalar üzerinde hello SAML denetimi için en düşük değer ayarlanmış tooone hafta.</span><span class="sxs-lookup"><span data-stu-id="45694-197">hello minimum value for hello SAML check on mobile applications is set tooone week.</span></span>

<span data-ttu-id="45694-198">Ayrıca, bir SAML hello düğmesini kullanarak tüm kullanıcılar için sıfırlama zorlayabilirsiniz: artık gerektiren SAML kimlik doğrulaması tüm kullanıcılar için.</span><span class="sxs-lookup"><span data-stu-id="45694-198">You can also force a SAML reset for all users using hello button: Require SAML authentication for all users now.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="45694-199">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="45694-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="45694-200">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="45694-200">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="45694-202">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="45694-202">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="45694-203">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="45694-203">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="45694-205">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="45694-205">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="45694-207">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="45694-207">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="45694-209">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="45694-209">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="45694-211">a.</span><span class="sxs-lookup"><span data-stu-id="45694-211">a.</span></span> <span data-ttu-id="45694-212">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="45694-212">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="45694-213">b.</span><span class="sxs-lookup"><span data-stu-id="45694-213">b.</span></span> <span data-ttu-id="45694-214">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="45694-214">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="45694-215">c.</span><span class="sxs-lookup"><span data-stu-id="45694-215">c.</span></span> <span data-ttu-id="45694-216">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="45694-216">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="45694-217">d.</span><span class="sxs-lookup"><span data-stu-id="45694-217">d.</span></span> <span data-ttu-id="45694-218">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="45694-218">Click **Create**.</span></span>
 
### <a name="creating-a-workplace-by-facebook-test-user"></a><span data-ttu-id="45694-219">Facebook test kullanıcı tarafından bir çalışma alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="45694-219">Creating a Workplace by Facebook test user</span></span>

<span data-ttu-id="45694-220">Bu bölümde, Britta Simon adlı bir kullanıcı tarafından Facebook çalışma alanında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="45694-220">In this section, a user called Britta Simon is created in Workplace by Facebook.</span></span> <span data-ttu-id="45694-221">Çalışma alanına Facebook tarafından yalnızca zaman sağlama, varsayılan olarak etkin olduğu destekler.</span><span class="sxs-lookup"><span data-stu-id="45694-221">Workplace by Facebook supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="45694-222">Bu bölümdeki hiçbir şey yoktur.</span><span class="sxs-lookup"><span data-stu-id="45694-222">There is no action for you in this section.</span></span> <span data-ttu-id="45694-223">Bir kullanıcı çalışma Facebook tarafından yoksa, yeni bir tooaccess çalışma alanına çalıştığınızda Facebook tarafından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="45694-223">If a user doesn't exist in Workplace by Facebook, a new one is created when you attempt tooaccess Workplace by Facebook.</span></span>

>[!Note]
><span data-ttu-id="45694-224">El ile bir kullanıcıyla iletişim toocreate gerekiyorsa [Facebook istemcisini destek ekibi ile çalışma](https://workplace.fb.com/faq/)</span><span class="sxs-lookup"><span data-stu-id="45694-224">If you need toocreate a user manually, Contact [Workplace by Facebook Client support team](https://workplace.fb.com/faq/)</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="45694-225">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="45694-225">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="45694-226">Bu bölümde, Facebook tarafından erişim tooWorkplace vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="45694-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWorkplace by Facebook.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="45694-228">**tooassign Britta Simon tooWorkplace Facebook tarafından hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="45694-228">**tooassign Britta Simon tooWorkplace by Facebook, perform hello following steps:**</span></span>

1. <span data-ttu-id="45694-229">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="45694-229">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="45694-231">Merhaba uygulamalar listesinde **Facebook ile çalışma alanına**.</span><span class="sxs-lookup"><span data-stu-id="45694-231">In hello applications list, select **Workplace by Facebook**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_app.png) 

3. <span data-ttu-id="45694-233">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="45694-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="45694-235">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="45694-235">Click **Add** button.</span></span> <span data-ttu-id="45694-236">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="45694-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="45694-238">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="45694-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="45694-239">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="45694-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="45694-240">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="45694-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="45694-241">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="45694-241">Testing single sign-on</span></span>

<span data-ttu-id="45694-242">Çoklu oturum açma ayarlarınızı tootest istiyorsanız hello erişim paneli açın.</span><span class="sxs-lookup"><span data-stu-id="45694-242">If you want tootest your single sign-on settings, open hello Access Panel.</span></span>
<span data-ttu-id="45694-243">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="45694-243">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="45694-244">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="45694-244">Additional resources</span></span>

* [<span data-ttu-id="45694-245">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="45694-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="45694-246">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="45694-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="45694-247">Kullanıcı sağlamayı Yapılandır</span><span class="sxs-lookup"><span data-stu-id="45694-247">Configure User Provisioning</span></span>](active-directory-saas-workplacebyfacebook-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_203.png

