---
title: "Öğretici: Azure Active Directory Tümleştirme Lifesize bulut ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Lifesize bulut arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 75fab335-fdcd-4066-b42c-cc738fcb6513
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: ae599907e872571b3220de7122006c7db8db4a2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lifesize-cloud"></a><span data-ttu-id="73f41-103">Öğretici: Azure Active Directory Tümleştirme Lifesize bulut ile</span><span class="sxs-lookup"><span data-stu-id="73f41-103">Tutorial: Azure Active Directory integration with Lifesize Cloud</span></span>

<span data-ttu-id="73f41-104">Bu öğreticide, bilgi toointegrate Lifesize bulut nasıl Azure Active Directory (Azure AD) ile.</span><span class="sxs-lookup"><span data-stu-id="73f41-104">In this tutorial, you learn how toointegrate Lifesize Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="73f41-105">Lifesize bulut Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="73f41-105">Integrating Lifesize Cloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="73f41-106">Erişim tooLifesize bulut sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="73f41-106">You can control in Azure AD who has access tooLifesize Cloud</span></span>
- <span data-ttu-id="73f41-107">Kullanıcıların tooautomatically get açan tooLifesize bulut (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="73f41-107">You can enable your users tooautomatically get signed-on tooLifesize Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="73f41-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="73f41-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="73f41-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="73f41-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="73f41-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="73f41-110">Prerequisites</span></span>

<span data-ttu-id="73f41-111">tooconfigure Lifesize bulut ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="73f41-111">tooconfigure Azure AD integration with Lifesize Cloud, you need hello following items:</span></span>

- <span data-ttu-id="73f41-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="73f41-112">An Azure AD subscription</span></span>
- <span data-ttu-id="73f41-113">Bir Lifesize bulut çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="73f41-113">A Lifesize Cloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="73f41-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="73f41-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="73f41-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="73f41-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="73f41-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="73f41-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="73f41-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="73f41-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="73f41-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="73f41-118">Scenario description</span></span>
<span data-ttu-id="73f41-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="73f41-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="73f41-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="73f41-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="73f41-121">Merhaba Galerisi'nden Lifesize bulut ekleme</span><span class="sxs-lookup"><span data-stu-id="73f41-121">Adding Lifesize Cloud from hello gallery</span></span>
2. <span data-ttu-id="73f41-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="73f41-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lifesize-cloud-from-hello-gallery"></a><span data-ttu-id="73f41-123">Merhaba Galerisi'nden Lifesize bulut ekleme</span><span class="sxs-lookup"><span data-stu-id="73f41-123">Adding Lifesize Cloud from hello gallery</span></span>
<span data-ttu-id="73f41-124">Azure AD'ye tooconfigure hello tümleştirme Lifesize bulutun tooadd Lifesize bulut hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="73f41-124">tooconfigure hello integration of Lifesize Cloud into Azure AD, you need tooadd Lifesize Cloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="73f41-125">**tooadd Lifesize bulut hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="73f41-125">**tooadd Lifesize Cloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="73f41-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="73f41-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="73f41-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="73f41-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="73f41-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="73f41-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="73f41-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="73f41-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="73f41-133">Merhaba arama kutusuna yazın **Lifesize bulut**.</span><span class="sxs-lookup"><span data-stu-id="73f41-133">In hello search box, type **Lifesize Cloud**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_search.png)

5. <span data-ttu-id="73f41-135">Merhaba Sonuçlar panelinde seçin **Lifesize bulut**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="73f41-135">In hello results panel, select **Lifesize Cloud**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="73f41-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="73f41-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="73f41-138">Bu bölümde, yapılandırmanız ve Lifesize bulut ile Azure AD çoklu oturum açmayı test "Britta Simon" adlı bir test kullanıcı tabanlı.</span><span class="sxs-lookup"><span data-stu-id="73f41-138">In this section, you configure and test Azure AD single sign-on with Lifesize Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="73f41-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Lifesize bulutta tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="73f41-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Lifesize Cloud is tooa user in Azure AD.</span></span> <span data-ttu-id="73f41-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve Lifesize bulutta hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="73f41-140">In other words, a link relationship between an Azure AD user and hello related user in Lifesize Cloud needs toobe established.</span></span>

<span data-ttu-id="73f41-141">Merhaba hello değeri Lifesize buluta atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="73f41-141">In Lifesize Cloud, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="73f41-142">tooconfigure ve Lifesize bulut ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="73f41-142">tooconfigure and test Azure AD single sign-on with Lifesize Cloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="73f41-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="73f41-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="73f41-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="73f41-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="73f41-145">**[Lifesize bulut test kullanıcısı oluşturma](#creating-a-lifesize-cloud-test-user)**  -toohave karşılık gelen, Britta Simon Lifesize bulutta kullanıcı bağlantılı toohello Azure AD gösterimidir.</span><span class="sxs-lookup"><span data-stu-id="73f41-145">**[Creating a Lifesize Cloud test user](#creating-a-lifesize-cloud-test-user)** - toohave a counterpart of Britta Simon in Lifesize Cloud that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="73f41-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="73f41-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="73f41-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="73f41-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="73f41-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="73f41-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="73f41-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Lifesize bulut uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="73f41-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Lifesize Cloud application.</span></span>

<span data-ttu-id="73f41-150">**tooconfigure Azure AD çoklu oturum açma Lifesize bulut ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="73f41-150">**tooconfigure Azure AD single sign-on with Lifesize Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="73f41-151">Hello hello üzerinde Azure portal'ın **Lifesize bulut** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="73f41-151">In hello Azure portal, on hello **Lifesize Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="73f41-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="73f41-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_samlbase.png)

3. <span data-ttu-id="73f41-155">Merhaba üzerinde **Lifesize bulut etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="73f41-155">On hello **Lifesize Cloud Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_url.png)

    <span data-ttu-id="73f41-157">a.</span><span class="sxs-lookup"><span data-stu-id="73f41-157">a.</span></span> <span data-ttu-id="73f41-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://login.lifesizecloud.com/ls/?acs`</span><span class="sxs-lookup"><span data-stu-id="73f41-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://login.lifesizecloud.com/ls/?acs`</span></span>

    <span data-ttu-id="73f41-159">b.</span><span class="sxs-lookup"><span data-stu-id="73f41-159">b.</span></span> <span data-ttu-id="73f41-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://login.lifesizecloud.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="73f41-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://login.lifesizecloud.com/<companyname>`</span></span>

     
4. <span data-ttu-id="73f41-161">Denetleme **Göster Gelişmiş URL ayarları**, adım aşağıdaki hello gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="73f41-161">Check **Show advanced URL settings**, perform hello following step:</span></span>  
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_url1.png)

    <span data-ttu-id="73f41-163">Merhaba, **geçiş durumu** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://webapp.lifesizecloud.com/?ent=<identifier>`</span><span class="sxs-lookup"><span data-stu-id="73f41-163">In hello **Relay state** textbox, type a URL using hello following pattern: `https://webapp.lifesizecloud.com/?ent=<identifier>`</span></span>
   
   > [!NOTE] 
   ><span data-ttu-id="73f41-164">Lütfen bu hello gerçek değerler olmadığına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="73f41-164">Please note that these are not hello real values.</span></span> <span data-ttu-id="73f41-165">tooupdate hello ile bu değerlere sahip gerçek oturum açma URL'si, geçiş durumunu ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="73f41-165">you have tooupdate these values with hello actual Sign-On URL, Relay State, and Identifier.</span></span> <span data-ttu-id="73f41-166">Kişi [Lifesize bulut istemci destek ekibi](https://www.lifesize.com/support) tooget oturum açma URL'si ve tanımlayıcı değerlerini ve alabilirsiniz geçiş durum değeri SSO yapılandırmasından hello öğreticinin ilerleyen bölümlerinde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="73f41-166">Contact [Lifesize Cloud Client support team](https://www.lifesize.com/support) tooget Sign-On URL, and Identifier values and you can get Relay State  value from SSO Configuration that is explained later in hello tutorial.</span></span>

4. <span data-ttu-id="73f41-167">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="73f41-167">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_certificate.png) 

5. <span data-ttu-id="73f41-169">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="73f41-169">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="73f41-171">Merhaba üzerinde **Lifesize bulut Yapılandırması** 'yi tıklatın **Lifesize bulut yapılandırma** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="73f41-171">On hello **Lifesize Cloud Configuration** section, click **Configure Lifesize Cloud** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="73f41-172">Kopya hello **SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="73f41-172">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_configure.png) 

7. <span data-ttu-id="73f41-174">tooget SSO hello Lifesize bulut uygulama yönetici ayrıcalıklarıyla oturum uygulamanız için yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="73f41-174">tooget SSO configured for your application, login into hello Lifesize Cloud application with Admin privileges.</span></span>

8. <span data-ttu-id="73f41-175">Merhaba sağ üst köşedeki adınızın tıklayın ve üzerinde hello ardından **Gelişmiş ayarları**.</span><span class="sxs-lookup"><span data-stu-id="73f41-175">In hello top right corner click on your name and then click on hello **Advance Settings**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_06.png)

9. <span data-ttu-id="73f41-177">Gelişmiş şimdi ayarları üzerinde hello hello içinde **SSO yapılandırma** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="73f41-177">In hello Advance Settings now click on hello **SSO Configuration** link.</span></span> <span data-ttu-id="73f41-178">Örneğiniz için hello SSO yapılandırma sayfası açılır.</span><span class="sxs-lookup"><span data-stu-id="73f41-178">It will open hello SSO Configuration page for your instance.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_07.png)

10. <span data-ttu-id="73f41-180">Şimdi hello SSO yapılandırma kullanıcı Arabirimi değerleri aşağıdaki hello yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="73f41-180">Now configure hello following values in hello SSO configuration UI.</span></span>    
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_08.png)
    
    <span data-ttu-id="73f41-182">a.</span><span class="sxs-lookup"><span data-stu-id="73f41-182">a.</span></span> <span data-ttu-id="73f41-183">İçinde **kimlik sağlayıcısı veren** metin kutusuna, Yapıştır hello değerini **SAML varlık kimliği** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="73f41-183">In **Identity Provider Issuer** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="73f41-184">b.</span><span class="sxs-lookup"><span data-stu-id="73f41-184">b.</span></span>  <span data-ttu-id="73f41-185">İçinde **oturum açma URL'si** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="73f41-185">In **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="73f41-186">c.</span><span class="sxs-lookup"><span data-stu-id="73f41-186">c.</span></span> <span data-ttu-id="73f41-187">Base-64 kodlanmış sertifikanızı Azure portalından kopyalama hello panonuza bunu içerik indirilen Not Defteri'nde açın ve toohello Yapıştır **X.509 sertifikası** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="73f41-187">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox.</span></span>
  
    <span data-ttu-id="73f41-188">d.</span><span class="sxs-lookup"><span data-stu-id="73f41-188">d.</span></span> <span data-ttu-id="73f41-189">Hello SAML özniteliği hello değeri olarak eşlemeleri hello adı metin kutusuna girin **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**</span><span class="sxs-lookup"><span data-stu-id="73f41-189">In hello SAML Attribute mappings for hello First Name text box enter hello value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**</span></span>
    
    <span data-ttu-id="73f41-190">e.</span><span class="sxs-lookup"><span data-stu-id="73f41-190">e.</span></span> <span data-ttu-id="73f41-191">Merhaba SAML öznitelik eşlemesinde hello **Soyadı** metin kutusuna girin hello değeri olarak **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**</span><span class="sxs-lookup"><span data-stu-id="73f41-191">In hello SAML Attribute mapping for hello **Last Name** text box enter hello value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**</span></span>
    
    <span data-ttu-id="73f41-192">f.</span><span class="sxs-lookup"><span data-stu-id="73f41-192">f.</span></span> <span data-ttu-id="73f41-193">Merhaba SAML öznitelik eşlemesinde hello **e-posta** metin kutusuna girin hello değeri olarak **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**</span><span class="sxs-lookup"><span data-stu-id="73f41-193">In hello SAML Attribute mapping for hello **Email** text box enter hello value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**</span></span>

11. <span data-ttu-id="73f41-194">Merhaba üzerinde tıklayabilirsiniz toocheck hello yapılandırma **Test** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="73f41-194">toocheck hello configuration you can click on hello **Test** button.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="73f41-195">Başarılı test erişim toousers veya hello testi gerçekleştirebilirsiniz grupları da sağlar ve Azure AD içinde toocomplete hello Yapılandırma Sihirbazı'nı gerekir.</span><span class="sxs-lookup"><span data-stu-id="73f41-195">For successful testing you need toocomplete hello configuration wizard in Azure AD and also provide access toousers or groups who can perform hello test.</span></span>

12. <span data-ttu-id="73f41-196">Merhaba üzerinde denetleyerek Hello SSO etkinleştirmek **etkinleştirmek SSO** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="73f41-196">Enable hello SSO by checking on hello **Enable SSO** button.</span></span>

13. <span data-ttu-id="73f41-197">Şimdi üzerinde hello tıklayın **güncelleştirme** böylece kaydedilen tüm hello ayarları düğmesi.</span><span class="sxs-lookup"><span data-stu-id="73f41-197">Now click on hello **Update** button so that all hello settings are saved.</span></span> <span data-ttu-id="73f41-198">Bu hello RelayState değer oluşturur.</span><span class="sxs-lookup"><span data-stu-id="73f41-198">This will generate hello RelayState value.</span></span> <span data-ttu-id="73f41-199">Kopya hello hello metin kutusuna oluşturulur, RelayState değeri yapıştırın, hello **geçiş durumunu** metin kutusu altında **Lifesize bulut etki alanı ve URL'leri** bölümü.</span><span class="sxs-lookup"><span data-stu-id="73f41-199">Copy hello RelayState value, which is generated in hello text box, paste it in hello **Relay State** textbox under **Lifesize Cloud Domain and URLs** section.</span></span> 

> [!TIP]
> <span data-ttu-id="73f41-200">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="73f41-200">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="73f41-201">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="73f41-201">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="73f41-202">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="73f41-202">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="73f41-203">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="73f41-203">Creating an Azure AD test user</span></span>

<span data-ttu-id="73f41-204">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="73f41-204">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="73f41-206">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="73f41-206">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="73f41-207">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="73f41-207">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="73f41-209">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="73f41-209">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="73f41-211">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="73f41-211">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="73f41-213">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="73f41-213">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="73f41-215">a.</span><span class="sxs-lookup"><span data-stu-id="73f41-215">a.</span></span> <span data-ttu-id="73f41-216">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="73f41-216">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="73f41-217">b.</span><span class="sxs-lookup"><span data-stu-id="73f41-217">b.</span></span> <span data-ttu-id="73f41-218">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="73f41-218">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="73f41-219">c.</span><span class="sxs-lookup"><span data-stu-id="73f41-219">c.</span></span> <span data-ttu-id="73f41-220">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="73f41-220">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="73f41-221">d.</span><span class="sxs-lookup"><span data-stu-id="73f41-221">d.</span></span> <span data-ttu-id="73f41-222">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="73f41-222">Click **Create**.</span></span>
 
### <a name="creating-a-lifesize-cloud-test-user"></a><span data-ttu-id="73f41-223">Lifesize bulut test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="73f41-223">Creating a Lifesize Cloud test user</span></span>

<span data-ttu-id="73f41-224">Bu bölümde, Britta Simon Lifesize bulutta adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="73f41-224">In this section, you create a user called Britta Simon in Lifesize Cloud.</span></span> <span data-ttu-id="73f41-225">Lifesize bulut otomatik kullanıcı sağlamayı desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="73f41-225">Lifesize cloud does support automatic user provisioning.</span></span> <span data-ttu-id="73f41-226">Azure AD, başarılı kimlik doğrulamasından sonra hello kullanıcı otomatik olarak hello uygulamada sağlanacak.</span><span class="sxs-lookup"><span data-stu-id="73f41-226">After successful authentication at Azure AD, hello user will be automatically provisioned in hello application.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="73f41-227">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="73f41-227">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="73f41-228">Bu bölümde, erişim tooLifesize bulut vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="73f41-228">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLifesize Cloud.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="73f41-230">**tooassign Britta Simon tooLifesize bulut hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="73f41-230">**tooassign Britta Simon tooLifesize Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="73f41-231">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="73f41-231">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="73f41-233">Merhaba uygulamalar listesinde **Lifesize bulut**.</span><span class="sxs-lookup"><span data-stu-id="73f41-233">In hello applications list, select **Lifesize Cloud**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_app.png) 

3. <span data-ttu-id="73f41-235">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="73f41-235">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="73f41-237">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="73f41-237">Click **Add** button.</span></span> <span data-ttu-id="73f41-238">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="73f41-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="73f41-240">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="73f41-240">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="73f41-241">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="73f41-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="73f41-242">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="73f41-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="73f41-243">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="73f41-243">Testing single sign-on</span></span>

<span data-ttu-id="73f41-244">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="73f41-244">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="73f41-245">Lifesize bulut döşeme hello erişim paneli hello tıkladığınızda, oturum açma sayfasına Lifesize bulut uygulamasının almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="73f41-245">When you click hello Lifesize Cloud tile in hello Access Panel, you should get login page of Lifesize Cloud application.</span></span>
<span data-ttu-id="73f41-246">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="73f41-246">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="73f41-247">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="73f41-247">Additional resources</span></span>

* [<span data-ttu-id="73f41-248">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="73f41-248">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="73f41-249">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="73f41-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_203.png

