---
title: "Öğretici: Azure Active Directory Tümleştirme ile TeamSeer | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile TeamSeer arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6ec4806f-fe0f-4ed7-8cfa-32d1c840433f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 876d13e446115acd50b01c7f44db99357045e429
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamseer"></a><span data-ttu-id="f5c78-103">Öğretici: Azure Active Directory Tümleştirme TeamSeer ile</span><span class="sxs-lookup"><span data-stu-id="f5c78-103">Tutorial: Azure Active Directory integration with TeamSeer</span></span>

<span data-ttu-id="f5c78-104">Bu öğreticide, bilgi nasıl toointegrate TeamSeer Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f5c78-104">In this tutorial, you learn how toointegrate TeamSeer with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f5c78-105">TeamSeer Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="f5c78-105">Integrating TeamSeer with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f5c78-106">Erişim tooTeamSeer sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="f5c78-106">You can control in Azure AD who has access tooTeamSeer</span></span>
- <span data-ttu-id="f5c78-107">Kullanıcıların tooautomatically get açan tooTeamSeer (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="f5c78-107">You can enable your users tooautomatically get signed-on tooTeamSeer (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f5c78-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="f5c78-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f5c78-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f5c78-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f5c78-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="f5c78-110">Prerequisites</span></span>

<span data-ttu-id="f5c78-111">tooconfigure TeamSeer ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="f5c78-111">tooconfigure Azure AD integration with TeamSeer, you need hello following items:</span></span>

- <span data-ttu-id="f5c78-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="f5c78-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f5c78-113">Bir TeamSeer çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="f5c78-113">A TeamSeer single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f5c78-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="f5c78-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f5c78-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="f5c78-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f5c78-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="f5c78-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f5c78-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f5c78-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f5c78-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="f5c78-118">Scenario description</span></span>
<span data-ttu-id="f5c78-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="f5c78-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f5c78-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="f5c78-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f5c78-121">Merhaba Galerisi'nden TeamSeer ekleme</span><span class="sxs-lookup"><span data-stu-id="f5c78-121">Adding TeamSeer from hello gallery</span></span>
2. <span data-ttu-id="f5c78-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="f5c78-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-teamseer-from-hello-gallery"></a><span data-ttu-id="f5c78-123">Merhaba Galerisi'nden TeamSeer ekleme</span><span class="sxs-lookup"><span data-stu-id="f5c78-123">Adding TeamSeer from hello gallery</span></span>
<span data-ttu-id="f5c78-124">Merhaba tümleştirilmesi tooconfigure TeamSeer tooAzure AD içinde tooadd TeamSeer hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="f5c78-124">tooconfigure hello integration of TeamSeer in tooAzure AD, you need tooadd TeamSeer from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f5c78-125">**tooadd TeamSeer hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f5c78-125">**tooadd TeamSeer from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f5c78-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="f5c78-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f5c78-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="f5c78-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f5c78-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="f5c78-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="f5c78-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f5c78-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="f5c78-133">Merhaba arama kutusuna yazın **TeamSeer**.</span><span class="sxs-lookup"><span data-stu-id="f5c78-133">In hello search box, type **TeamSeer**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_search.png)

5. <span data-ttu-id="f5c78-135">Merhaba Sonuçlar panelinde seçin **TeamSeer**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="f5c78-135">In hello results panel, select **TeamSeer**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f5c78-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="f5c78-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f5c78-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı TeamSeer ile test etme</span><span class="sxs-lookup"><span data-stu-id="f5c78-138">In this section, you configure and test Azure AD single sign-on with TeamSeer based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f5c78-139">Tek toowork'ın oturum açma hangi hello karşılık gelen TeamSeer içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="f5c78-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TeamSeer is tooa user in Azure AD.</span></span> <span data-ttu-id="f5c78-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı TeamSeer hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="f5c78-140">In other words, a link relationship between an Azure AD user and hello related user in TeamSeer needs toobe established.</span></span>

<span data-ttu-id="f5c78-141">Merhaba hello değeri TeamSeer içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="f5c78-141">In TeamSeer, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f5c78-142">tooconfigure ve TeamSeer ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="f5c78-142">tooconfigure and test Azure AD single sign-on with TeamSeer, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f5c78-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="f5c78-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f5c78-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="f5c78-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f5c78-145">**[TeamSeer test kullanıcısı oluşturma](#creating-a-teamseer-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir TeamSeer içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="f5c78-145">**[Creating a TeamSeer test user](#creating-a-teamseer-test-user)** - toohave a counterpart of Britta Simon in TeamSeer that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f5c78-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="f5c78-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f5c78-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="f5c78-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f5c78-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f5c78-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f5c78-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma TeamSeer uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="f5c78-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TeamSeer application.</span></span>

<span data-ttu-id="f5c78-150">**tooconfigure Azure AD çoklu oturum açma ile TeamSeer, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f5c78-150">**tooconfigure Azure AD single sign-on with TeamSeer, perform hello following steps:**</span></span>

1. <span data-ttu-id="f5c78-151">Hello hello üzerinde Azure portal'ın **TeamSeer** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="f5c78-151">In hello Azure portal, on hello **TeamSeer** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="f5c78-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="f5c78-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_samlbase.png)

3. <span data-ttu-id="f5c78-155">Merhaba üzerinde **TeamSeer etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="f5c78-155">On hello **TeamSeer Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_url.png)

     <span data-ttu-id="f5c78-157">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://www.teamseer.com/<companyid>`</span><span class="sxs-lookup"><span data-stu-id="f5c78-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://www.teamseer.com/<companyid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f5c78-158">Merhaba değeri gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="f5c78-158">hello value is not real.</span></span> <span data-ttu-id="f5c78-159">Güncelleştirme hello değerle hello gerçek oturum açma URL'si.</span><span class="sxs-lookup"><span data-stu-id="f5c78-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="f5c78-160">Kişi [TeamSeer istemci destek ekibi](http://pages.theaccessgroup.com/solutions_business-suite_absence-management_contact.html) tooget hello değeri.</span><span class="sxs-lookup"><span data-stu-id="f5c78-160">Contact [TeamSeer Client support team](http://pages.theaccessgroup.com/solutions_business-suite_absence-management_contact.html) tooget hello value.</span></span> 
 
4. <span data-ttu-id="f5c78-161">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="f5c78-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_certificate.png) 

5. <span data-ttu-id="f5c78-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f5c78-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-teamseer-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f5c78-165">Merhaba üzerinde **TeamSeer yapılandırma** 'yi tıklatın **yapılandırma TeamSeer** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="f5c78-165">On hello **TeamSeer Configuration** section, click **Configure TeamSeer** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="f5c78-166">Kopya hello **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="f5c78-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_configure.png)

7. <span data-ttu-id="f5c78-168">Farklı web tarayıcısı penceresinde tooyour TeamSeer şirket sitede yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="f5c78-168">In a different web browser window, log in tooyour TeamSeer company site as an administrator.</span></span>

8. <span data-ttu-id="f5c78-169">Çok Git**ik yönetici**.</span><span class="sxs-lookup"><span data-stu-id="f5c78-169">Go too**HR Admin**.</span></span>
   
    <span data-ttu-id="f5c78-170">![HR yönetici](./media/active-directory-saas-teamseer-tutorial/ic789634.png "ik yönetici")</span><span class="sxs-lookup"><span data-stu-id="f5c78-170">![HR Admin](./media/active-directory-saas-teamseer-tutorial/ic789634.png "HR Admin")</span></span>

9. <span data-ttu-id="f5c78-171">Tıklatın **Kurulum**.</span><span class="sxs-lookup"><span data-stu-id="f5c78-171">Click **Setup**.</span></span>
   
    <span data-ttu-id="f5c78-172">![Kurulum](./media/active-directory-saas-teamseer-tutorial/ic789635.png "Kurulumu")</span><span class="sxs-lookup"><span data-stu-id="f5c78-172">![Setup](./media/active-directory-saas-teamseer-tutorial/ic789635.png "Setup")</span></span>

10. <span data-ttu-id="f5c78-173">Tıklatın **SAML sağlayıcı ayrıntılarını ayarlama**.</span><span class="sxs-lookup"><span data-stu-id="f5c78-173">Click **Set up SAML provider details**.</span></span>
   
    <span data-ttu-id="f5c78-174">![SAML ayarları](./media/active-directory-saas-teamseer-tutorial/ic789636.png "SAML ayarları")</span><span class="sxs-lookup"><span data-stu-id="f5c78-174">![SAML Settings](./media/active-directory-saas-teamseer-tutorial/ic789636.png "SAML Settings")</span></span>

11. <span data-ttu-id="f5c78-175">Hello SAML sağlayıcı ayrıntıları bölümü, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="f5c78-175">In hello SAML provider details section, perform hello following steps:</span></span>
   
    <span data-ttu-id="f5c78-176">![SAML ayarları](./media/active-directory-saas-teamseer-tutorial/ic789637.png "SAML ayarları")</span><span class="sxs-lookup"><span data-stu-id="f5c78-176">![SAML Settings](./media/active-directory-saas-teamseer-tutorial/ic789637.png "SAML Settings")</span></span>   

    <span data-ttu-id="f5c78-177">a.</span><span class="sxs-lookup"><span data-stu-id="f5c78-177">a.</span></span> <span data-ttu-id="f5c78-178">Yapıştır hello **çoklu oturum açma hizmet URL'si** toohello değerinde **URL** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="f5c78-178">Paste hello **Single Sign-On Service URL** value in toohello **URL** textbox.</span></span>
          
    <span data-ttu-id="f5c78-179">b.</span><span class="sxs-lookup"><span data-stu-id="f5c78-179">b.</span></span> <span data-ttu-id="f5c78-180">Base-64 kodlanmış sertifikanızı kopyalama hello tooyour Pano'da bunu içerik Not Defteri'nde açın ve toohello yapıştırın **IDP ortak sertifika** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="f5c78-180">Open your base-64 encoded certificate in notepad, copy hello content of it in tooyour clipboard, and then paste it toohello **IdP Public Certificate** textbox.</span></span>

12. <span data-ttu-id="f5c78-181">toocomplete hello SAML sağlayıcı yapılandırması hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="f5c78-181">toocomplete hello SAML provider configuration, perform hello following steps:</span></span>
    
    <span data-ttu-id="f5c78-182">![SAML ayarları](./media/active-directory-saas-teamseer-tutorial/ic789638.png "SAML ayarları")</span><span class="sxs-lookup"><span data-stu-id="f5c78-182">![SAML Settings](./media/active-directory-saas-teamseer-tutorial/ic789638.png "SAML Settings")</span></span> 

    <span data-ttu-id="f5c78-183">a.</span><span class="sxs-lookup"><span data-stu-id="f5c78-183">a.</span></span> <span data-ttu-id="f5c78-184">Merhaba, **Test e-posta adresleri**, hello test kullanıcının e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="f5c78-184">In hello **Test Email Addresses**, type hello test user’s email address.</span></span> 
  
    <span data-ttu-id="f5c78-185">b.</span><span class="sxs-lookup"><span data-stu-id="f5c78-185">b.</span></span> <span data-ttu-id="f5c78-186">Merhaba, **veren** metin kutusuna, türü hello hello hizmet sağlayıcısı'nın veren URL'si.</span><span class="sxs-lookup"><span data-stu-id="f5c78-186">In hello **Issuer** textbox, type hello Issuer URL of hello service provider.</span></span> 
  
    <span data-ttu-id="f5c78-187">c.</span><span class="sxs-lookup"><span data-stu-id="f5c78-187">c.</span></span> <span data-ttu-id="f5c78-188">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f5c78-188">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="f5c78-189">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="f5c78-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f5c78-190">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="f5c78-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f5c78-191">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f5c78-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f5c78-192">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f5c78-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="f5c78-193">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="f5c78-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="f5c78-195">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f5c78-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f5c78-196">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="f5c78-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-teamseer-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f5c78-198">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="f5c78-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-teamseer-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f5c78-200">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="f5c78-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-teamseer-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f5c78-202">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="f5c78-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-teamseer-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f5c78-204">a.</span><span class="sxs-lookup"><span data-stu-id="f5c78-204">a.</span></span> <span data-ttu-id="f5c78-205">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f5c78-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f5c78-206">b.</span><span class="sxs-lookup"><span data-stu-id="f5c78-206">b.</span></span> <span data-ttu-id="f5c78-207">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="f5c78-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f5c78-208">c.</span><span class="sxs-lookup"><span data-stu-id="f5c78-208">c.</span></span> <span data-ttu-id="f5c78-209">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="f5c78-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f5c78-210">d.</span><span class="sxs-lookup"><span data-stu-id="f5c78-210">d.</span></span> <span data-ttu-id="f5c78-211">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f5c78-211">Click **Create**.</span></span>
 
### <a name="creating-a-teamseer-test-user"></a><span data-ttu-id="f5c78-212">TeamSeer test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f5c78-212">Creating a TeamSeer test user</span></span>

<span data-ttu-id="f5c78-213">tooenable Azure AD kullanıcıların toolog tooTeamSeer bunlar içinde tooShiftPlanning sağlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f5c78-213">tooenable Azure AD users toolog in tooTeamSeer, they must be provisioned in tooShiftPlanning.</span></span> <span data-ttu-id="f5c78-214">TeamSeer Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="f5c78-214">In hello case of TeamSeer, provisioning is a manual task.</span></span>

<span data-ttu-id="f5c78-215">**bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f5c78-215">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="f5c78-216">İçinde tooyour oturum **TeamSeer** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="f5c78-216">Log in tooyour **TeamSeer** company site as an administrator.</span></span>

2. <span data-ttu-id="f5c78-217">Merhaba aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="f5c78-217">Perform hello following steps:</span></span>
   
    <span data-ttu-id="f5c78-218">![HR yönetici](./media/active-directory-saas-teamseer-tutorial/ic789640.png "ik yönetici")</span><span class="sxs-lookup"><span data-stu-id="f5c78-218">![HR Admin](./media/active-directory-saas-teamseer-tutorial/ic789640.png "HR Admin")</span></span>  
 
    <span data-ttu-id="f5c78-219">a.</span><span class="sxs-lookup"><span data-stu-id="f5c78-219">a.</span></span> <span data-ttu-id="f5c78-220">Çok Git**ik yönetici \> kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="f5c78-220">Go too**HR Admin \> Users**.</span></span>
  
    <span data-ttu-id="f5c78-221">b.</span><span class="sxs-lookup"><span data-stu-id="f5c78-221">b.</span></span> <span data-ttu-id="f5c78-222">Tıklatın **hello yeni kullanıcı Sihirbazı'nı çalıştırın**.</span><span class="sxs-lookup"><span data-stu-id="f5c78-222">Click **Run hello New User wizard**.</span></span>

3. <span data-ttu-id="f5c78-223">Merhaba, **kullanıcı ayrıntıları** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="f5c78-223">In hello **User Details** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="f5c78-224">![Kullanıcı ayrıntılarını](./media/active-directory-saas-teamseer-tutorial/ic789641.png "kullanıcı ayrıntıları")</span><span class="sxs-lookup"><span data-stu-id="f5c78-224">![User Details](./media/active-directory-saas-teamseer-tutorial/ic789641.png "User Details")</span></span>

    <span data-ttu-id="f5c78-225">a.</span><span class="sxs-lookup"><span data-stu-id="f5c78-225">a.</span></span> <span data-ttu-id="f5c78-226">Türü hello **ad**, **Soyadı**, **kullanıcı adı (e-posta adresi)** , metin kutuları toohello tooprovision istediğiniz geçerli bir AAD hesabıyla ilgili.</span><span class="sxs-lookup"><span data-stu-id="f5c78-226">Type hello **First Name**, **Surname**, **User name (Email address)** of a valid AAD account you want tooprovision in toohello related textboxes.</span></span>
  
    <span data-ttu-id="f5c78-227">b.</span><span class="sxs-lookup"><span data-stu-id="f5c78-227">b.</span></span> <span data-ttu-id="f5c78-228">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f5c78-228">Click **Next**.</span></span>

4. <span data-ttu-id="f5c78-229">Merhaba ekran yeni bir kullanıcı eklemek için yönergeleri izleyin ve tıklayın **son**.</span><span class="sxs-lookup"><span data-stu-id="f5c78-229">Follow hello on-screen instructions for adding a new user, and click **Finish**.</span></span>

>[!NOTE]
><span data-ttu-id="f5c78-230">API'leri, Azure AD kullanıcı hesapları TeamSeer tooprovision tarafından sağlanan veya herhangi diğer TeamSeer kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f5c78-230">You can use any other TeamSeer user account creation tools or APIs provided by TeamSeer tooprovision Azure AD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f5c78-231">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="f5c78-231">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f5c78-232">Bu bölümde, erişim tooTeamSeer vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="f5c78-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTeamSeer.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="f5c78-234">**tooassign Britta Simon tooTeamSeer hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f5c78-234">**tooassign Britta Simon tooTeamSeer, perform hello following steps:**</span></span>

1. <span data-ttu-id="f5c78-235">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="f5c78-235">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="f5c78-237">Merhaba uygulamalar listesinde **TeamSeer**.</span><span class="sxs-lookup"><span data-stu-id="f5c78-237">In hello applications list, select **TeamSeer**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_app.png) 

3. <span data-ttu-id="f5c78-239">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="f5c78-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="f5c78-241">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f5c78-241">Click **Add** button.</span></span> <span data-ttu-id="f5c78-242">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="f5c78-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="f5c78-244">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="f5c78-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f5c78-245">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="f5c78-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f5c78-246">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="f5c78-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f5c78-247">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="f5c78-247">Testing single sign-on</span></span>

<span data-ttu-id="f5c78-248">Çoklu oturum açma ayarlarınızı tootest istiyorsanız hello erişim paneli açın.</span><span class="sxs-lookup"><span data-stu-id="f5c78-248">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="f5c78-249">Merhaba erişim paneli hakkında daha fazla ayrıntı için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f5c78-249">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f5c78-250">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="f5c78-250">Additional resources</span></span>

* [<span data-ttu-id="f5c78-251">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="f5c78-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f5c78-252">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="f5c78-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_203.png

