---
title: "Öğretici: Azure Active Directory Tümleştirme SkyDesk e-posta ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile SkyDesk e-posta arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a9d0bbcb-ddb5-473f-a4aa-028ae88ced1a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: 19c670a60f581a2be55b74eacdb5393a36e38be3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-skydesk-email"></a><span data-ttu-id="e1518-103">Öğretici: Azure Active Directory Tümleştirme SkyDesk e-posta ile</span><span class="sxs-lookup"><span data-stu-id="e1518-103">Tutorial: Azure Active Directory integration with SkyDesk Email</span></span>

<span data-ttu-id="e1518-104">Bu öğreticide, bilgi SkyDesk toointegrate e-posta nasıl Azure Active Directory (Azure AD) ile.</span><span class="sxs-lookup"><span data-stu-id="e1518-104">In this tutorial, you learn how toointegrate SkyDesk Email with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e1518-105">Azure AD ile SkyDesk e-posta tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="e1518-105">Integrating SkyDesk Email with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e1518-106">E-posta erişimi tooSkyDesk sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="e1518-106">You can control in Azure AD who has access tooSkyDesk Email</span></span>
- <span data-ttu-id="e1518-107">Kullanıcıların tooautomatically get açan tooSkyDesk e-posta (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="e1518-107">You can enable your users tooautomatically get signed-on tooSkyDesk Email (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e1518-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="e1518-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e1518-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e1518-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e1518-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e1518-110">Prerequisites</span></span>

<span data-ttu-id="e1518-111">tooconfigure SkyDesk e-posta ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="e1518-111">tooconfigure Azure AD integration with SkyDesk Email, you need hello following items:</span></span>

- <span data-ttu-id="e1518-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="e1518-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e1518-113">Bir SkyDesk e-posta çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="e1518-113">A SkyDesk Email single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e1518-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="e1518-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e1518-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="e1518-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e1518-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="e1518-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e1518-117">Bir Azure AD deneme ortam yoksa, burada bir aylık deneme alabilirsiniz [deneme teklifi](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e1518-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e1518-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="e1518-118">Scenario description</span></span>
<span data-ttu-id="e1518-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="e1518-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e1518-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="e1518-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e1518-121">Merhaba Galerisi'nden SkyDesk e-posta ekleme</span><span class="sxs-lookup"><span data-stu-id="e1518-121">Adding SkyDesk Email from hello gallery</span></span>
2. <span data-ttu-id="e1518-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="e1518-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-skydesk-email-from-hello-gallery"></a><span data-ttu-id="e1518-123">Merhaba Galerisi'nden SkyDesk e-posta ekleme</span><span class="sxs-lookup"><span data-stu-id="e1518-123">Adding SkyDesk Email from hello gallery</span></span>
<span data-ttu-id="e1518-124">Azure AD'ye tooconfigure hello tümleştirme SkyDesk e-posta tooadd SkyDesk e-posta hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="e1518-124">tooconfigure hello integration of SkyDesk Email into Azure AD, you need tooadd SkyDesk Email from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e1518-125">**tooadd SkyDesk e-posta hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e1518-125">**tooadd SkyDesk Email from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e1518-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="e1518-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e1518-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="e1518-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e1518-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="e1518-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="e1518-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e1518-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="e1518-133">Merhaba arama kutusuna yazın **SkyDesk e-posta**.</span><span class="sxs-lookup"><span data-stu-id="e1518-133">In hello search box, type **SkyDesk Email**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_search.png)

5. <span data-ttu-id="e1518-135">Merhaba Sonuçlar panelinde seçin **SkyDesk e-posta**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="e1518-135">In hello results panel, select **SkyDesk Email**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e1518-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="e1518-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e1518-138">Bu bölümde, yapılandırmanız ve SkyDesk e-posta ile Azure AD çoklu oturum açmayı test "Britta Simon" adlı bir test kullanıcı tabanlı.</span><span class="sxs-lookup"><span data-stu-id="e1518-138">In this section, you configure and test Azure AD single sign-on with SkyDesk Email based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e1518-139">Tek toowork'ın oturum açma hangi hello karşılık gelen SkyDesk e-posta tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="e1518-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SkyDesk Email is tooa user in Azure AD.</span></span> <span data-ttu-id="e1518-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcıya SkyDesk e-posta hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="e1518-140">In other words, a link relationship between an Azure AD user and hello related user in SkyDesk Email needs toobe established.</span></span>

<span data-ttu-id="e1518-141">Merhaba hello değeri SkyDesk postada atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="e1518-141">In SkyDesk Email, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e1518-142">tooconfigure ve SkyDesk e-posta ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="e1518-142">tooconfigure and test Azure AD single sign-on with SkyDesk Email, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e1518-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="e1518-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e1518-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="e1518-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e1518-145">**[SkyDesk e-posta test kullanıcısı oluşturma](#creating-a-skydesk-email-test-user)**  -toohave Britta Simon bağlantılı toohello Azure AD kullanıcı gösterimini SkyDesk e-postadaki, karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="e1518-145">**[Creating a SkyDesk Email test user](#creating-a-skydesk-email-test-user)** - toohave a counterpart of Britta Simon in SkyDesk Email that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e1518-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="e1518-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e1518-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="e1518-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e1518-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e1518-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e1518-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma SkyDesk e-posta uygulamanızı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="e1518-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SkyDesk Email application.</span></span>

<span data-ttu-id="e1518-150">**tooconfigure Azure AD çoklu oturum açma SkyDesk e-posta ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e1518-150">**tooconfigure Azure AD single sign-on with SkyDesk Email, perform hello following steps:**</span></span>

1. <span data-ttu-id="e1518-151">Hello hello üzerinde Azure portal'ın **SkyDesk e-posta** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="e1518-151">In hello Azure portal, on hello **SkyDesk Email** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="e1518-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="e1518-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_samlbase.png)

3. <span data-ttu-id="e1518-155">Merhaba üzerinde **SkyDesk e-posta etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e1518-155">On hello **SkyDesk Email Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_url.png)

    <span data-ttu-id="e1518-157">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://mail.skydesk.jp/portal/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="e1518-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://mail.skydesk.jp/portal/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e1518-158">Merhaba değeri gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="e1518-158">hello value is not real.</span></span> <span data-ttu-id="e1518-159">Güncelleştirme hello değerle hello gerçek oturum açma URL'si.</span><span class="sxs-lookup"><span data-stu-id="e1518-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="e1518-160">Kişi [SkyDesk e-posta istemcisi destek ekibi](https://www.skydesk.sg/support/) tooget hello değeri.</span><span class="sxs-lookup"><span data-stu-id="e1518-160">Contact [SkyDesk Email Client support team](https://www.skydesk.sg/support/) tooget hello value.</span></span> 
 
4. <span data-ttu-id="e1518-161">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e1518-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_certificate.png) 

5. <span data-ttu-id="e1518-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e1518-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e1518-165">Merhaba üzerinde **SkyDesk e-posta Yapılandırması** 'yi tıklatın **SkyDesk e-posta Yapılandırma** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="e1518-165">On hello **SkyDesk Email Configuration** section, click **Configure SkyDesk Email** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="e1518-166">Kopya hello **Sign-Out URL ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="e1518-166">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_configure.png) 

7. <span data-ttu-id="e1518-168">tooenable SSO içinde **SkyDesk e-posta**, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e1518-168">tooenable SSO in **SkyDesk Email**, perform hello following steps:</span></span>

    <span data-ttu-id="e1518-169">a.</span><span class="sxs-lookup"><span data-stu-id="e1518-169">a.</span></span> <span data-ttu-id="e1518-170">Oturum açma SkyDesk e-posta hesabı yönetici olarak tooyour.</span><span class="sxs-lookup"><span data-stu-id="e1518-170">Sign-on tooyour SkyDesk Email account as administrator.</span></span>

    <span data-ttu-id="e1518-171">b.</span><span class="sxs-lookup"><span data-stu-id="e1518-171">b.</span></span> <span data-ttu-id="e1518-172">Hello içinde hello üst menüsünde **Kurulum**seçip **Org**.</span><span class="sxs-lookup"><span data-stu-id="e1518-172">In hello menu on hello top, click **Setup**, and select **Org**.</span></span> 
    
      ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_51.png)
  
    <span data-ttu-id="e1518-174">c.</span><span class="sxs-lookup"><span data-stu-id="e1518-174">c.</span></span> <span data-ttu-id="e1518-175">Tıklayın **etki alanları** hello sol panelindeki.</span><span class="sxs-lookup"><span data-stu-id="e1518-175">Click on **Domains** from hello left panel.</span></span>
    
      ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_53.png)

    <span data-ttu-id="e1518-177">d.</span><span class="sxs-lookup"><span data-stu-id="e1518-177">d.</span></span> <span data-ttu-id="e1518-178">Tıklayın **etki alanı ekleme**.</span><span class="sxs-lookup"><span data-stu-id="e1518-178">Click on **Add Domain**.</span></span>
    
      ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_54.png)

    <span data-ttu-id="e1518-180">e.</span><span class="sxs-lookup"><span data-stu-id="e1518-180">e.</span></span> <span data-ttu-id="e1518-181">Etki alanı adınızı girin ve ardından hello etki alanını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="e1518-181">Enter your Domain name, and then verify hello Domain.</span></span>
    
      ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_55.png)

    <span data-ttu-id="e1518-183">f.</span><span class="sxs-lookup"><span data-stu-id="e1518-183">f.</span></span> <span data-ttu-id="e1518-184">Tıklayın **SAML kimlik doğrulaması** hello sol panelindeki.</span><span class="sxs-lookup"><span data-stu-id="e1518-184">Click on **SAML Authentication** from hello left panel.</span></span>
    
      ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_52.png)

8. <span data-ttu-id="e1518-186">Merhaba üzerinde **SAML kimlik doğrulaması** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e1518-186">On hello **SAML Authentication** dialog page, perform hello following steps:</span></span>
   
      ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_56.png)
   
    >[!NOTE]
    ><span data-ttu-id="e1518-188">toouse SAML tabanlı kimlik doğrulaması, ya da olmalıdır **etki alanını doğruladıysanız** veya **portalı URL'si** kurulumu.</span><span class="sxs-lookup"><span data-stu-id="e1518-188">toouse SAML based authentication, you should either have **verified domain** or **portal URL** setup.</span></span> <span data-ttu-id="e1518-189">Merhaba portal ayarlayabilirsiniz URL hello benzersiz bir ad ile.</span><span class="sxs-lookup"><span data-stu-id="e1518-189">You can set hello portal URL with hello unique name.</span></span>
    > 
    > 
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_57.png)

    <span data-ttu-id="e1518-191">a.</span><span class="sxs-lookup"><span data-stu-id="e1518-191">a.</span></span> <span data-ttu-id="e1518-192">Merhaba, **oturum açma URL'si** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="e1518-192">In hello **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="e1518-193">b.</span><span class="sxs-lookup"><span data-stu-id="e1518-193">b.</span></span> <span data-ttu-id="e1518-194">Merhaba, **oturum kapatma** URL'si metin kutusuna, Yapıştır hello değerini **Sign-Out URL**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="e1518-194">In hello **Logout** URL textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="e1518-195">c.</span><span class="sxs-lookup"><span data-stu-id="e1518-195">c.</span></span> <span data-ttu-id="e1518-196">**Değiştirme parola URL'si** isteğe bağlı olduğu kadar boş bırakın.</span><span class="sxs-lookup"><span data-stu-id="e1518-196">**Change Password URL** is optional so leave it blank.</span></span>

    <span data-ttu-id="e1518-197">d.</span><span class="sxs-lookup"><span data-stu-id="e1518-197">d.</span></span> <span data-ttu-id="e1518-198">Tıklayın **anahtarı dosyadan al** tooselect Azure portal ve ardından indirilen sertifikanızı **açık** tooupload hello sertifika.</span><span class="sxs-lookup"><span data-stu-id="e1518-198">Click on **Get Key From File** tooselect your downloaded certificate from Azure portal, and then click **Open** tooupload hello certificate.</span></span>

    <span data-ttu-id="e1518-199">e.</span><span class="sxs-lookup"><span data-stu-id="e1518-199">e.</span></span> <span data-ttu-id="e1518-200">Olarak **algoritması**seçin **RSA**.</span><span class="sxs-lookup"><span data-stu-id="e1518-200">As **Algorithm**, select **RSA**.</span></span>

    <span data-ttu-id="e1518-201">f.</span><span class="sxs-lookup"><span data-stu-id="e1518-201">f.</span></span> <span data-ttu-id="e1518-202">Tıklatın **Tamam** toosave hello değişiklikleri.</span><span class="sxs-lookup"><span data-stu-id="e1518-202">Click **Ok** toosave hello changes.</span></span>

> [!TIP]
> <span data-ttu-id="e1518-203">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="e1518-203">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e1518-204">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="e1518-204">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e1518-205">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e1518-205">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e1518-206">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e1518-206">Creating an Azure AD test user</span></span>
<span data-ttu-id="e1518-207">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="e1518-207">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="e1518-209">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e1518-209">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e1518-210">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="e1518-210">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e1518-212">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="e1518-212">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e1518-214">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="e1518-214">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e1518-216">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e1518-216">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e1518-218">a.</span><span class="sxs-lookup"><span data-stu-id="e1518-218">a.</span></span> <span data-ttu-id="e1518-219">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e1518-219">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e1518-220">b.</span><span class="sxs-lookup"><span data-stu-id="e1518-220">b.</span></span> <span data-ttu-id="e1518-221">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="e1518-221">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e1518-222">c.</span><span class="sxs-lookup"><span data-stu-id="e1518-222">c.</span></span> <span data-ttu-id="e1518-223">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="e1518-223">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e1518-224">d.</span><span class="sxs-lookup"><span data-stu-id="e1518-224">d.</span></span> <span data-ttu-id="e1518-225">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e1518-225">Click **Create**.</span></span>
 
### <a name="creating-a-skydesk-email-test-user"></a><span data-ttu-id="e1518-226">SkyDesk e-posta test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e1518-226">Creating a SkyDesk Email test user</span></span>

<span data-ttu-id="e1518-227">Bu bölümde, Britta Simon SkyDesk e-postayla adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e1518-227">In this section, you create a user called Britta Simon in SkyDesk Email.</span></span>

1. <span data-ttu-id="e1518-228">Tıklayın **kullanıcı erişimini** hello sol panel SkyDesk e-posta ve kullanıcı adınızı girin.</span><span class="sxs-lookup"><span data-stu-id="e1518-228">Click on **User Access** from hello left panel in SkyDesk Email and then enter your username.</span></span> 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_58.png)

>[!NOTE] 
><span data-ttu-id="e1518-230">Toocreate toplu kullanıcılar gerekiyorsa, toocontact hello gereksinim [SkyDesk e-posta istemcisi destek ekibi](https://www.skydesk.sg/support/).</span><span class="sxs-lookup"><span data-stu-id="e1518-230">If you need toocreate bulk users, you need toocontact hello [SkyDesk Email Client support team](https://www.skydesk.sg/support/).</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e1518-231">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="e1518-231">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e1518-232">Bu bölümde, e-posta erişimi tooSkyDesk vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="e1518-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSkyDesk Email.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="e1518-234">**tooassign Britta Simon tooSkyDesk e-posta, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e1518-234">**tooassign Britta Simon tooSkyDesk Email, perform hello following steps:**</span></span>

1. <span data-ttu-id="e1518-235">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="e1518-235">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="e1518-237">Merhaba uygulamalar listesinde **SkyDesk e-posta**.</span><span class="sxs-lookup"><span data-stu-id="e1518-237">In hello applications list, select **SkyDesk Email**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_app.png) 

3. <span data-ttu-id="e1518-239">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="e1518-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="e1518-241">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e1518-241">Click **Add** button.</span></span> <span data-ttu-id="e1518-242">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e1518-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="e1518-244">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="e1518-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e1518-245">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e1518-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e1518-246">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e1518-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e1518-247">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="e1518-247">Testing single sign-on</span></span>

<span data-ttu-id="e1518-248">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD SSO yapılandırmayı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="e1518-248">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="e1518-249">SkyDesk e-posta döşeme hello erişim paneli hello tıkladığınızda, otomatik olarak oturum açma SkyDesk e-posta uygulamasının tooyour almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e1518-249">When you click hello SkyDesk Email tile in hello Access Panel, you should get automatically signed-on tooyour SkyDesk Email application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e1518-250">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="e1518-250">Additional resources</span></span>

* [<span data-ttu-id="e1518-251">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="e1518-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e1518-252">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="e1518-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_203.png

