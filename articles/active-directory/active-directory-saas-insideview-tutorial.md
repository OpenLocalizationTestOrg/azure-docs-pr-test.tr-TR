---
title: "Öğretici: Azure Active Directory Tümleştirme ile InsideView | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile InsideView arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c489a7ab-6b1f-4efb-8a66-8bc13bca78c3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 979c0c24f3a18a193616061b8c2e78292233a56d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-insideview"></a><span data-ttu-id="2cd29-103">Öğretici: Azure Active Directory Tümleştirme InsideView ile</span><span class="sxs-lookup"><span data-stu-id="2cd29-103">Tutorial: Azure Active Directory integration with InsideView</span></span>

<span data-ttu-id="2cd29-104">Bu öğreticide, bilgi nasıl toointegrate InsideView Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2cd29-104">In this tutorial, you learn how toointegrate InsideView with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2cd29-105">InsideView Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="2cd29-105">Integrating InsideView with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2cd29-106">Erişim tooInsideView sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="2cd29-106">You can control in Azure AD who has access tooInsideView</span></span>
- <span data-ttu-id="2cd29-107">Kullanıcıların tooautomatically get açan tooInsideView (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="2cd29-107">You can enable your users tooautomatically get signed-on tooInsideView (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2cd29-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="2cd29-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="2cd29-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2cd29-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2cd29-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="2cd29-110">Prerequisites</span></span>

<span data-ttu-id="2cd29-111">tooconfigure InsideView ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="2cd29-111">tooconfigure Azure AD integration with InsideView, you need hello following items:</span></span>

- <span data-ttu-id="2cd29-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="2cd29-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2cd29-113">Bir InsideView çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="2cd29-113">A InsideView single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2cd29-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="2cd29-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2cd29-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="2cd29-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2cd29-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="2cd29-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2cd29-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2cd29-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2cd29-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="2cd29-118">Scenario description</span></span>
<span data-ttu-id="2cd29-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="2cd29-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2cd29-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="2cd29-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2cd29-121">Merhaba Galerisi'nden InsideView ekleme</span><span class="sxs-lookup"><span data-stu-id="2cd29-121">Adding InsideView from hello gallery</span></span>
2. <span data-ttu-id="2cd29-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="2cd29-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-insideview-from-hello-gallery"></a><span data-ttu-id="2cd29-123">Merhaba Galerisi'nden InsideView ekleme</span><span class="sxs-lookup"><span data-stu-id="2cd29-123">Adding InsideView from hello gallery</span></span>
<span data-ttu-id="2cd29-124">Merhaba tümleştirilmesi tooconfigure InsideView tooAzure AD içinde tooadd InsideView hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="2cd29-124">tooconfigure hello integration of InsideView in tooAzure AD, you need tooadd InsideView from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2cd29-125">**tooadd InsideView hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2cd29-125">**tooadd InsideView from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2cd29-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="2cd29-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2cd29-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="2cd29-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2cd29-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="2cd29-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="2cd29-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2cd29-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="2cd29-133">Merhaba arama kutusuna yazın **InsideView**.</span><span class="sxs-lookup"><span data-stu-id="2cd29-133">In hello search box, type **InsideView**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_search.png)

5. <span data-ttu-id="2cd29-135">Merhaba Sonuçlar panelinde seçin **InsideView**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="2cd29-135">In hello results panel, select **InsideView**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2cd29-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="2cd29-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2cd29-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı InsideView ile test etme</span><span class="sxs-lookup"><span data-stu-id="2cd29-138">In this section, you configure and test Azure AD single sign-on with InsideView based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="2cd29-139">Tek toowork'ın oturum açma hangi hello karşılık gelen InsideView içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="2cd29-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in InsideView is tooa user in Azure AD.</span></span> <span data-ttu-id="2cd29-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı InsideView hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="2cd29-140">In other words, a link relationship between an Azure AD user and hello related user in InsideView needs toobe established.</span></span>

<span data-ttu-id="2cd29-141">Merhaba hello değeri InsideView içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="2cd29-141">In InsideView, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="2cd29-142">tooconfigure ve InsideView ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="2cd29-142">tooconfigure and test Azure AD single sign-on with InsideView, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2cd29-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="2cd29-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2cd29-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="2cd29-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2cd29-145">**[InsideView test kullanıcısı oluşturma](#creating-a-insideview-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir InsideView içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="2cd29-145">**[Creating a InsideView test user](#creating-a-insideview-test-user)** - toohave a counterpart of Britta Simon in InsideView that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="2cd29-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="2cd29-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2cd29-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="2cd29-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2cd29-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="2cd29-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2cd29-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma InsideView uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="2cd29-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your InsideView application.</span></span>

<span data-ttu-id="2cd29-150">**tooconfigure Azure AD çoklu oturum açma ile InsideView, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2cd29-150">**tooconfigure Azure AD single sign-on with InsideView, perform hello following steps:**</span></span>

1. <span data-ttu-id="2cd29-151">Hello hello üzerinde Azure portal'ın **InsideView** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="2cd29-151">In hello Azure portal, on hello **InsideView** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="2cd29-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="2cd29-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_samlbase.png)

3. <span data-ttu-id="2cd29-155">Merhaba üzerinde **InsideView etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2cd29-155">On hello **InsideView Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_url.png)
    
    <span data-ttu-id="2cd29-157">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://my.insideview.com/iv/<STS Name>/login.iv`</span><span class="sxs-lookup"><span data-stu-id="2cd29-157">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://my.insideview.com/iv/<STS Name>/login.iv`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2cd29-158">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="2cd29-158">This value is not real.</span></span> <span data-ttu-id="2cd29-159">Bu değer hello gerçek yanıt URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="2cd29-159">Update this value with hello actual Reply URL.</span></span> <span data-ttu-id="2cd29-160">Kişi [InsideView destek ekibi ](mailto:support@insideview.com) tooget bu değer.</span><span class="sxs-lookup"><span data-stu-id="2cd29-160">Contact [InsideView support team ](mailto:support@insideview.com) tooget this value.</span></span>
 
4. <span data-ttu-id="2cd29-161">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (ham)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="2cd29-161">On hello **SAML Signing Certificate** section, click **Certificate (Raw)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_certificate.png) 

5. <span data-ttu-id="2cd29-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2cd29-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-insideview-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2cd29-165">Merhaba üzerinde **InsideView yapılandırma** 'yi tıklatın **yapılandırma InsideView** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="2cd29-165">On hello **InsideView Configuration** section, click **Configure InsideView** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="2cd29-166">Kopya hello **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="2cd29-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_configure.png) 

7. <span data-ttu-id="2cd29-168">Farklı web tarayıcısı penceresinde tooyour InsideView şirket sitede yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="2cd29-168">In a different web browser window, log in tooyour InsideView company site as an administrator.</span></span>

8. <span data-ttu-id="2cd29-169">Merhaba üstte Hello araç çubuğunda **yönetici**, **SingleSignOn ayarları**ve ardından **eklemek SAML**.</span><span class="sxs-lookup"><span data-stu-id="2cd29-169">In hello toolbar on hello top, click **Admin**, **SingleSignOn Settings**, and then click **Add SAML**.</span></span>
   
   <span data-ttu-id="2cd29-170">![SAML çoklu oturum açma ayarları](./media/active-directory-saas-insideview-tutorial/ic794135.png "SAML çoklu oturum açma ayarları")</span><span class="sxs-lookup"><span data-stu-id="2cd29-170">![SAML Single Sign On Settings](./media/active-directory-saas-insideview-tutorial/ic794135.png "SAML Single Sign On Settings")</span></span>

9. <span data-ttu-id="2cd29-171">Merhaba, **yeni bir SAML eklemek** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2cd29-171">In hello **Add a New SAML** section, perform hello following steps:</span></span>

    <span data-ttu-id="2cd29-172">![Yeni bir SAML eklemek](./media/active-directory-saas-insideview-tutorial/ic794136.png "yeni bir SAML ekleme")</span><span class="sxs-lookup"><span data-stu-id="2cd29-172">![Add a New SAML](./media/active-directory-saas-insideview-tutorial/ic794136.png "Add a New SAML")</span></span>
   
    <span data-ttu-id="2cd29-173">a.</span><span class="sxs-lookup"><span data-stu-id="2cd29-173">a.</span></span> <span data-ttu-id="2cd29-174">Merhaba, **STS adını** metin kutusuna, yapılandırmanız için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="2cd29-174">In hello **STS Name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="2cd29-175">b.</span><span class="sxs-lookup"><span data-stu-id="2cd29-175">b.</span></span> <span data-ttu-id="2cd29-176">İçinde **SamlP/WS-Fed istenmeyen EndPoint** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="2cd29-176">In **SamlP/WS-Fed Unsolicited EndPoint** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="2cd29-177">c.</span><span class="sxs-lookup"><span data-stu-id="2cd29-177">c.</span></span> <span data-ttu-id="2cd29-178">Azure portal, kopyalama hello panonuza bunu içerik gelen yüklediğiniz, base-64 kodlanmış sertifika açın ve ardından toohello yapıştırın **STS sertifikası** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="2cd29-178">Open your base-64 encoded certificate, which you have downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **STS Certificate** textbox.</span></span>

    <span data-ttu-id="2cd29-179">d.</span><span class="sxs-lookup"><span data-stu-id="2cd29-179">d.</span></span> <span data-ttu-id="2cd29-180">Merhaba, **Crm kullanıcı kimliği eşleme** metin kutusuna, türü `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="2cd29-180">In hello **Crm User Id Mapping** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
        
    <span data-ttu-id="2cd29-181">e.</span><span class="sxs-lookup"><span data-stu-id="2cd29-181">e.</span></span> <span data-ttu-id="2cd29-182">Merhaba, **Crm e-posta eşleme** metin kutusuna, türü `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="2cd29-182">In hello **Crm Email Mapping** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>

    <span data-ttu-id="2cd29-183">f.</span><span class="sxs-lookup"><span data-stu-id="2cd29-183">f.</span></span> <span data-ttu-id="2cd29-184">Merhaba, **ilk adı Crm eşleme** metin kutusuna, türü `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span><span class="sxs-lookup"><span data-stu-id="2cd29-184">In hello **Crm First Name Mapping** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>
    
    <span data-ttu-id="2cd29-185">g.</span><span class="sxs-lookup"><span data-stu-id="2cd29-185">g.</span></span> <span data-ttu-id="2cd29-186">Merhaba, **Crm lastName eşleme** metin kutusuna, türü `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span><span class="sxs-lookup"><span data-stu-id="2cd29-186">In hello **Crm lastName Mapping** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>  

    <span data-ttu-id="2cd29-187">h.</span><span class="sxs-lookup"><span data-stu-id="2cd29-187">h.</span></span> <span data-ttu-id="2cd29-188">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2cd29-188">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="2cd29-189">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="2cd29-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2cd29-190">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="2cd29-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2cd29-191">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2cd29-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2cd29-192">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="2cd29-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="2cd29-193">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="2cd29-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="2cd29-195">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2cd29-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2cd29-196">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="2cd29-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-insideview-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2cd29-198">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="2cd29-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-insideview-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2cd29-200">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="2cd29-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-insideview-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2cd29-202">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2cd29-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-insideview-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2cd29-204">a.</span><span class="sxs-lookup"><span data-stu-id="2cd29-204">a.</span></span> <span data-ttu-id="2cd29-205">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2cd29-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2cd29-206">b.</span><span class="sxs-lookup"><span data-stu-id="2cd29-206">b.</span></span> <span data-ttu-id="2cd29-207">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="2cd29-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2cd29-208">c.</span><span class="sxs-lookup"><span data-stu-id="2cd29-208">c.</span></span> <span data-ttu-id="2cd29-209">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="2cd29-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="2cd29-210">d.</span><span class="sxs-lookup"><span data-stu-id="2cd29-210">d.</span></span> <span data-ttu-id="2cd29-211">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2cd29-211">Click **Create**.</span></span>
 
### <a name="creating-a-insideview-test-user"></a><span data-ttu-id="2cd29-212">InsideView test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="2cd29-212">Creating a InsideView test user</span></span>

<span data-ttu-id="2cd29-213">tooenable Azure AD kullanıcıların toolog tooInsideView bunlar içinde tooInsideView sağlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="2cd29-213">tooenable Azure AD users toolog in tooInsideView, they must be provisioned in tooInsideView.</span></span> <span data-ttu-id="2cd29-214">InsideView Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="2cd29-214">In hello case of InsideView, provisioning is a manual task.</span></span>

<span data-ttu-id="2cd29-215">tooget kullanıcılar ve kişiler oluşturulan InsideView, kişi [InsideView destek ekibi](mailto:support@insideview.com).</span><span class="sxs-lookup"><span data-stu-id="2cd29-215">tooget users or contacts created in InsideView, Contact [InsideView support team](mailto:support@insideview.com).</span></span>

>[!NOTE]
><span data-ttu-id="2cd29-216">API'leri, Azure AD kullanıcı hesapları InsideView tooprovision tarafından sağlanan veya herhangi diğer InsideView kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2cd29-216">You can use any other InsideView user account creation tools or APIs provided by InsideView tooprovision Azure AD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="2cd29-217">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="2cd29-217">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="2cd29-218">Bu bölümde, erişim tooInsideView vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="2cd29-218">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooInsideView.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="2cd29-220">**tooassign Britta Simon tooInsideView hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2cd29-220">**tooassign Britta Simon tooInsideView, perform hello following steps:**</span></span>

1. <span data-ttu-id="2cd29-221">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="2cd29-221">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="2cd29-223">Merhaba uygulamalar listesinde **InsideView**.</span><span class="sxs-lookup"><span data-stu-id="2cd29-223">In hello applications list, select **InsideView**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_app.png) 

3. <span data-ttu-id="2cd29-225">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="2cd29-225">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="2cd29-227">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2cd29-227">Click **Add** button.</span></span> <span data-ttu-id="2cd29-228">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="2cd29-228">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="2cd29-230">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="2cd29-230">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2cd29-231">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="2cd29-231">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2cd29-232">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="2cd29-232">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2cd29-233">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="2cd29-233">Testing single sign-on</span></span>

<span data-ttu-id="2cd29-234">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="2cd29-234">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="2cd29-235">Merhaba InsideView hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour InsideView uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2cd29-235">When you click hello InsideView tile in hello Access Panel, you should get automatically signed-on tooyour InsideView application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2cd29-236">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="2cd29-236">Additional resources</span></span>

* [<span data-ttu-id="2cd29-237">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="2cd29-237">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2cd29-238">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="2cd29-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_203.png

