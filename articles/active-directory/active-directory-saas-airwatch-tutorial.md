---
title: "Öğretici: Azure Active Directory Tümleştirme ile AirWatch | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile AirWatch arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 96a3bb1c-96c6-40dc-8ea0-060b0c2a62e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: e5230d5a36824778a4d9804dadf9f13a0d11a68d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-airwatch"></a><span data-ttu-id="dfe94-103">Öğretici: Azure Active Directory Tümleştirme AirWatch ile</span><span class="sxs-lookup"><span data-stu-id="dfe94-103">Tutorial: Azure Active Directory integration with AirWatch</span></span>

<span data-ttu-id="dfe94-104">Bu öğreticide, bilgi nasıl toointegrate AirWatch Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dfe94-104">In this tutorial, you learn how toointegrate AirWatch with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dfe94-105">AirWatch Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="dfe94-105">Integrating AirWatch with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="dfe94-106">Erişim tooAirWatch sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="dfe94-106">You can control in Azure AD who has access tooAirWatch</span></span>
- <span data-ttu-id="dfe94-107">Kullanıcıların tooautomatically get açan tooAirWatch (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="dfe94-107">You can enable your users tooautomatically get signed-on tooAirWatch (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="dfe94-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="dfe94-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="dfe94-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="dfe94-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dfe94-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="dfe94-110">Prerequisites</span></span>

<span data-ttu-id="dfe94-111">tooconfigure AirWatch ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="dfe94-111">tooconfigure Azure AD integration with AirWatch, you need hello following items:</span></span>

- <span data-ttu-id="dfe94-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="dfe94-112">An Azure AD subscription</span></span>
- <span data-ttu-id="dfe94-113">Bir AirWatch çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="dfe94-113">An AirWatch single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dfe94-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="dfe94-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="dfe94-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="dfe94-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="dfe94-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="dfe94-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="dfe94-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dfe94-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dfe94-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="dfe94-118">Scenario description</span></span>
<span data-ttu-id="dfe94-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="dfe94-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dfe94-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="dfe94-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dfe94-121">Merhaba Galerisi'nden AirWatch ekleme</span><span class="sxs-lookup"><span data-stu-id="dfe94-121">Adding AirWatch from hello gallery</span></span>
2. <span data-ttu-id="dfe94-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="dfe94-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-airwatch-from-hello-gallery"></a><span data-ttu-id="dfe94-123">Merhaba Galerisi'nden AirWatch ekleme</span><span class="sxs-lookup"><span data-stu-id="dfe94-123">Adding AirWatch from hello gallery</span></span>
<span data-ttu-id="dfe94-124">Azure AD'ye tooconfigure hello tümleştirme AirWatch, tooadd AirWatch hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="dfe94-124">tooconfigure hello integration of AirWatch into Azure AD, you need tooadd AirWatch from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="dfe94-125">**tooadd AirWatch hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="dfe94-125">**tooadd AirWatch from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="dfe94-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="dfe94-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="dfe94-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="dfe94-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="dfe94-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="dfe94-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="dfe94-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="dfe94-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="dfe94-133">Merhaba arama kutusuna yazın **AirWatch**.</span><span class="sxs-lookup"><span data-stu-id="dfe94-133">In hello search box, type **AirWatch**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_search.png)

5. <span data-ttu-id="dfe94-135">Merhaba Sonuçlar panelinde seçin **AirWatch**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="dfe94-135">In hello results panel, select **AirWatch**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="dfe94-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="dfe94-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="dfe94-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı AirWatch ile test etme</span><span class="sxs-lookup"><span data-stu-id="dfe94-138">In this section, you configure and test Azure AD single sign-on with AirWatch based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="dfe94-139">Tek toowork'ın oturum açma hangi hello karşılık gelen AirWatch içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="dfe94-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in AirWatch is tooa user in Azure AD.</span></span> <span data-ttu-id="dfe94-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı AirWatch hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="dfe94-140">In other words, a link relationship between an Azure AD user and hello related user in AirWatch needs toobe established.</span></span>

<span data-ttu-id="dfe94-141">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** AirWatch içinde.</span><span class="sxs-lookup"><span data-stu-id="dfe94-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in AirWatch.</span></span>

<span data-ttu-id="dfe94-142">tooconfigure ve AirWatch ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="dfe94-142">tooconfigure and test Azure AD single sign-on with AirWatch, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="dfe94-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="dfe94-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="dfe94-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="dfe94-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="dfe94-145">**[AirWatch test kullanıcısı oluşturma](#creating-a-airwatch-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir AirWatch içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="dfe94-145">**[Creating a AirWatch test user](#creating-a-airwatch-test-user)** - toohave a counterpart of Britta Simon in AirWatch that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="dfe94-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="dfe94-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="dfe94-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="dfe94-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="dfe94-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="dfe94-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="dfe94-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma AirWatch uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="dfe94-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your AirWatch application.</span></span>

<span data-ttu-id="dfe94-150">**tooconfigure Azure AD çoklu oturum açma ile AirWatch, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="dfe94-150">**tooconfigure Azure AD single sign-on with AirWatch, perform hello following steps:**</span></span>

1. <span data-ttu-id="dfe94-151">Hello hello üzerinde Azure portal'ın **AirWatch** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="dfe94-151">In hello Azure portal, on hello **AirWatch** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="dfe94-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="dfe94-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_samlbase.png)

3. <span data-ttu-id="dfe94-155">Merhaba üzerinde **AirWatch etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="dfe94-155">On hello **AirWatch Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_url.png)

    <span data-ttu-id="dfe94-157">a.</span><span class="sxs-lookup"><span data-stu-id="dfe94-157">a.</span></span> <span data-ttu-id="dfe94-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.awmdm.com/AirWatch/Login?gid=companycode`</span><span class="sxs-lookup"><span data-stu-id="dfe94-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.awmdm.com/AirWatch/Login?gid=companycode`</span></span>

    <span data-ttu-id="dfe94-159">b.</span><span class="sxs-lookup"><span data-stu-id="dfe94-159">b.</span></span> <span data-ttu-id="dfe94-160">Merhaba, **tanımlayıcısı** metin kutusuna, türü hello değeri olarak`AirWatch`</span><span class="sxs-lookup"><span data-stu-id="dfe94-160">In hello **Identifier** textbox, type hello value as `AirWatch`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="dfe94-161">Bu değer hello gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="dfe94-161">This value is not hello real.</span></span> <span data-ttu-id="dfe94-162">Bu değer hello gerçek oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="dfe94-162">Update this value with hello actual Sign-on URL.</span></span> <span data-ttu-id="dfe94-163">Kişi [AirWatch istemci destek ekibi](http://www.air-watch.com/company/contact-us/) tooget bu değer.</span><span class="sxs-lookup"><span data-stu-id="dfe94-163">Contact [AirWatch Client support team](http://www.air-watch.com/company/contact-us/) tooget this value.</span></span> 
 
4. <span data-ttu-id="dfe94-164">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello XML dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="dfe94-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_certificate.png) 

5. <span data-ttu-id="dfe94-166">Merhaba üzerinde **AirWatch yapılandırma** 'yi tıklatın **yapılandırma AirWatch** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="dfe94-166">On hello **AirWatch Configuration** section, click **Configure AirWatch** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="dfe94-167">Kopya hello **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="dfe94-167">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_configure.png) 

6. <span data-ttu-id="dfe94-169">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="dfe94-169">Click **Save** button.</span></span>

    <span data-ttu-id="dfe94-170">![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-airwatch-tutorial/tutorial_general_400.png)
<CS></span><span class="sxs-lookup"><span data-stu-id="dfe94-170">![Configure Single Sign-On](./media/active-directory-saas-airwatch-tutorial/tutorial_general_400.png)
<CS></span></span>
7. <span data-ttu-id="dfe94-171">Farklı web tarayıcısı penceresinde tooyour AirWatch şirket sitede yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="dfe94-171">In a different web browser window, log in tooyour AirWatch company site as an administrator.</span></span>

8. <span data-ttu-id="dfe94-172">Merhaba sol gezinti bölmesinde **hesapları**ve ardından **Yöneticiler**.</span><span class="sxs-lookup"><span data-stu-id="dfe94-172">In hello left navigation pane, click **Accounts**, and then click **Administrators**.</span></span>
   
   <span data-ttu-id="dfe94-173">![Yöneticiler](./media/active-directory-saas-airwatch-tutorial/ic791920.png "yöneticileri")</span><span class="sxs-lookup"><span data-stu-id="dfe94-173">![Administrators](./media/active-directory-saas-airwatch-tutorial/ic791920.png "Administrators")</span></span>

9. <span data-ttu-id="dfe94-174">Merhaba genişletin **ayarları** menüsüne ve ardından **Dizin Hizmetleri**.</span><span class="sxs-lookup"><span data-stu-id="dfe94-174">Expand hello **Settings** menu, and then click **Directory Services**.</span></span>
   
   <span data-ttu-id="dfe94-175">![Ayarları](./media/active-directory-saas-airwatch-tutorial/ic791921.png "ayarları")</span><span class="sxs-lookup"><span data-stu-id="dfe94-175">![Settings](./media/active-directory-saas-airwatch-tutorial/ic791921.png "Settings")</span></span>

10. <span data-ttu-id="dfe94-176">Merhaba tıklatın **kullanıcı** sekmede hello **temel DN** metin kutusuna, etki alanı adınızı yazın ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="dfe94-176">Click hello **User** tab, in hello **Base DN** textbox, type your domain name, and then click **Save**.</span></span>
   
   <span data-ttu-id="dfe94-177">![Kullanıcı](./media/active-directory-saas-airwatch-tutorial/ic791922.png "kullanıcı")</span><span class="sxs-lookup"><span data-stu-id="dfe94-177">![User](./media/active-directory-saas-airwatch-tutorial/ic791922.png "User")</span></span>

11. <span data-ttu-id="dfe94-178">Merhaba tıklatın **Server** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="dfe94-178">Click hello **Server** tab.</span></span>
   
   <span data-ttu-id="dfe94-179">![Sunucu](./media/active-directory-saas-airwatch-tutorial/ic791923.png "sunucu")</span><span class="sxs-lookup"><span data-stu-id="dfe94-179">![Server](./media/active-directory-saas-airwatch-tutorial/ic791923.png "Server")</span></span>

12. <span data-ttu-id="dfe94-180">Merhaba aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="dfe94-180">Perform hello following steps:</span></span>
    
    <span data-ttu-id="dfe94-181">![Karşıya yükleme](./media/active-directory-saas-airwatch-tutorial/ic791924.png "karşıya yükle")</span><span class="sxs-lookup"><span data-stu-id="dfe94-181">![Upload](./media/active-directory-saas-airwatch-tutorial/ic791924.png "Upload")</span></span>   
    
    <span data-ttu-id="dfe94-182">a.</span><span class="sxs-lookup"><span data-stu-id="dfe94-182">a.</span></span> <span data-ttu-id="dfe94-183">Olarak **Directory türü**seçin **hiçbiri**.</span><span class="sxs-lookup"><span data-stu-id="dfe94-183">As **Directory Type**, select **None**.</span></span>

    <span data-ttu-id="dfe94-184">b.</span><span class="sxs-lookup"><span data-stu-id="dfe94-184">b.</span></span> <span data-ttu-id="dfe94-185">Seçin **SAML kimlik doğrulaması için kullanmak**.</span><span class="sxs-lookup"><span data-stu-id="dfe94-185">Select **Use SAML For Authentication**.</span></span>

    <span data-ttu-id="dfe94-186">c.</span><span class="sxs-lookup"><span data-stu-id="dfe94-186">c.</span></span> <span data-ttu-id="dfe94-187">tooupload Merhaba indirilen sertifika, tıklatın **karşıya**.</span><span class="sxs-lookup"><span data-stu-id="dfe94-187">tooupload hello downloaded certificate, click **Upload**.</span></span>

13. <span data-ttu-id="dfe94-188">Merhaba, **isteği** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="dfe94-188">In hello **Request** section, perform hello following steps:</span></span>
    
    <span data-ttu-id="dfe94-189">![İstek](./media/active-directory-saas-airwatch-tutorial/ic791925.png "isteği")</span><span class="sxs-lookup"><span data-stu-id="dfe94-189">![Request](./media/active-directory-saas-airwatch-tutorial/ic791925.png "Request")</span></span>  

    <span data-ttu-id="dfe94-190">a.</span><span class="sxs-lookup"><span data-stu-id="dfe94-190">a.</span></span> <span data-ttu-id="dfe94-191">Olarak **bağlama türü isteği**seçin **POST**.</span><span class="sxs-lookup"><span data-stu-id="dfe94-191">As **Request Binding Type**, select **POST**.</span></span>

    <span data-ttu-id="dfe94-192">b.</span><span class="sxs-lookup"><span data-stu-id="dfe94-192">b.</span></span> <span data-ttu-id="dfe94-193">Merhaba hello üzerinde Azure portal'ın **çoklu oturum açma sırasında Airwatch yapılandırma** iletişim sayfası, kopyalama hello **SAML çoklu oturum açma hizmet URL'si** değer ve hello yapıştırma **kimlik sağlayıcısı Tek bir oturum üzerinde URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="dfe94-193">In hello Azure portal, on hello **Configure single sign-on at Airwatch** dialog page, copy hello **SAML Single Sign-On Service URL** value, and then paste it into hello **Identity Provider Single Sign On URL** textbox.</span></span>

    <span data-ttu-id="dfe94-194">c.</span><span class="sxs-lookup"><span data-stu-id="dfe94-194">c.</span></span> <span data-ttu-id="dfe94-195">Olarak **NameID biçimi**seçin **e-posta adresi**.</span><span class="sxs-lookup"><span data-stu-id="dfe94-195">As **NameID Format**, select **Email Address**.</span></span>

    <span data-ttu-id="dfe94-196">d.</span><span class="sxs-lookup"><span data-stu-id="dfe94-196">d.</span></span> <span data-ttu-id="dfe94-197">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="dfe94-197">Click **Save**.</span></span>

14. <span data-ttu-id="dfe94-198">Merhaba tıklatın **kullanıcı** yeniden sekmesinde.</span><span class="sxs-lookup"><span data-stu-id="dfe94-198">Click hello **User** tab again.</span></span>
    
    <span data-ttu-id="dfe94-199">![Kullanıcı](./media/active-directory-saas-airwatch-tutorial/ic791926.png "kullanıcı")</span><span class="sxs-lookup"><span data-stu-id="dfe94-199">![User](./media/active-directory-saas-airwatch-tutorial/ic791926.png "User")</span></span>

15. <span data-ttu-id="dfe94-200">Merhaba, **özniteliği** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="dfe94-200">In hello **Attribute** section, perform hello following steps:</span></span>
    
    <span data-ttu-id="dfe94-201">![Öznitelik](./media/active-directory-saas-airwatch-tutorial/ic791927.png "özniteliği")</span><span class="sxs-lookup"><span data-stu-id="dfe94-201">![Attribute](./media/active-directory-saas-airwatch-tutorial/ic791927.png "Attribute")</span></span>

    <span data-ttu-id="dfe94-202">a.</span><span class="sxs-lookup"><span data-stu-id="dfe94-202">a.</span></span> <span data-ttu-id="dfe94-203">Merhaba, **nesne tanımlayıcısı** metin kutusuna, türü **http://schemas.microsoft.com/identity/claims/objectidentifier**.</span><span class="sxs-lookup"><span data-stu-id="dfe94-203">In hello **Object Identifier** textbox, type **http://schemas.microsoft.com/identity/claims/objectidentifier**.</span></span>

    <span data-ttu-id="dfe94-204">b.</span><span class="sxs-lookup"><span data-stu-id="dfe94-204">b.</span></span> <span data-ttu-id="dfe94-205">Merhaba, **kullanıcıadı** metin kutusuna, türü **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="dfe94-205">In hello **Username** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>

    <span data-ttu-id="dfe94-206">c.</span><span class="sxs-lookup"><span data-stu-id="dfe94-206">c.</span></span> <span data-ttu-id="dfe94-207">Merhaba, **görünen adı** metin kutusuna, türü **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span><span class="sxs-lookup"><span data-stu-id="dfe94-207">In hello **Display Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>

    <span data-ttu-id="dfe94-208">d.</span><span class="sxs-lookup"><span data-stu-id="dfe94-208">d.</span></span> <span data-ttu-id="dfe94-209">Merhaba, **ad** metin kutusuna, türü **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span><span class="sxs-lookup"><span data-stu-id="dfe94-209">In hello **First Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>

    <span data-ttu-id="dfe94-210">e.</span><span class="sxs-lookup"><span data-stu-id="dfe94-210">e.</span></span> <span data-ttu-id="dfe94-211">Merhaba, **Soyadı** metin kutusuna, türü **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span><span class="sxs-lookup"><span data-stu-id="dfe94-211">In hello **Last Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span></span>

    <span data-ttu-id="dfe94-212">f.</span><span class="sxs-lookup"><span data-stu-id="dfe94-212">f.</span></span> <span data-ttu-id="dfe94-213">Merhaba, **e-posta** metin kutusuna, türü **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="dfe94-213">In hello **Email** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>

    <span data-ttu-id="dfe94-214">g.</span><span class="sxs-lookup"><span data-stu-id="dfe94-214">g.</span></span> <span data-ttu-id="dfe94-215">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="dfe94-215">Click **Save**.</span></span>

<CE>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="dfe94-216">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="dfe94-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="dfe94-217">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="dfe94-217">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="dfe94-219">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="dfe94-219">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="dfe94-220">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="dfe94-220">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-airwatch-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="dfe94-222">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="dfe94-222">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-airwatch-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="dfe94-224">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="dfe94-224">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-airwatch-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="dfe94-226">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="dfe94-226">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-airwatch-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="dfe94-228">a.</span><span class="sxs-lookup"><span data-stu-id="dfe94-228">a.</span></span> <span data-ttu-id="dfe94-229">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dfe94-229">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dfe94-230">b.</span><span class="sxs-lookup"><span data-stu-id="dfe94-230">b.</span></span> <span data-ttu-id="dfe94-231">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** Britta Simon biri.</span><span class="sxs-lookup"><span data-stu-id="dfe94-231">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="dfe94-232">c.</span><span class="sxs-lookup"><span data-stu-id="dfe94-232">c.</span></span> <span data-ttu-id="dfe94-233">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="dfe94-233">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="dfe94-234">d.</span><span class="sxs-lookup"><span data-stu-id="dfe94-234">d.</span></span> <span data-ttu-id="dfe94-235">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="dfe94-235">Click **Create**.</span></span>
 
### <a name="creating-a-airwatch-test-user"></a><span data-ttu-id="dfe94-236">AirWatch test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="dfe94-236">Creating a AirWatch test user</span></span>

<span data-ttu-id="dfe94-237">tooenable Azure AD kullanıcıların toolog tooAirWatch bunlar içinde tooAirWatch sağlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="dfe94-237">tooenable Azure AD users toolog in tooAirWatch, they must be provisioned in tooAirWatch.</span></span>

* <span data-ttu-id="dfe94-238">AirWatch, sağlama el ile bir görev olduğunda.</span><span class="sxs-lookup"><span data-stu-id="dfe94-238">When AirWatch, provisioning is a manual task.</span></span>

<span data-ttu-id="dfe94-239">**bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="dfe94-239">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="dfe94-240">İçinde tooyour oturum **AirWatch** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="dfe94-240">Log in tooyour **AirWatch** company site as administrator.</span></span>
2. <span data-ttu-id="dfe94-241">Merhaba Gezinti hello sol taraftaki bölmede **hesapları**ve ardından **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="dfe94-241">In hello navigation pane on hello left side, click **Accounts**, and then click **Users**.</span></span>
   
   <span data-ttu-id="dfe94-242">![Kullanıcıların](./media/active-directory-saas-airwatch-tutorial/ic791929.png "kullanıcılar")</span><span class="sxs-lookup"><span data-stu-id="dfe94-242">![Users](./media/active-directory-saas-airwatch-tutorial/ic791929.png "Users")</span></span>
3. <span data-ttu-id="dfe94-243">Merhaba, **kullanıcılar** menüsünde tıklatın **liste görünümü**ve ardından **Ekle \> Kullanıcı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="dfe94-243">In hello **Users** menu, click **List View**, and then click **Add \> Add User**.</span></span>
   
   <span data-ttu-id="dfe94-244">![Kullanıcı ekleme](./media/active-directory-saas-airwatch-tutorial/ic791930.png "kullanıcı ekleme")</span><span class="sxs-lookup"><span data-stu-id="dfe94-244">![Add User](./media/active-directory-saas-airwatch-tutorial/ic791930.png "Add User")</span></span>
4. <span data-ttu-id="dfe94-245">Merhaba üzerinde **Ekle / Düzenle kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="dfe94-245">On hello **Add / Edit User** dialog, perform hello following steps:</span></span>

   <span data-ttu-id="dfe94-246">![Kullanıcı ekleme](./media/active-directory-saas-airwatch-tutorial/ic791931.png "kullanıcı ekleme")</span><span class="sxs-lookup"><span data-stu-id="dfe94-246">![Add User](./media/active-directory-saas-airwatch-tutorial/ic791931.png "Add User")</span></span>   
   1. <span data-ttu-id="dfe94-247">Türü hello **kullanıcıadı**, **parola**, **parolayı onayla**, **ad**, **Soyadı**,  **E-posta adresi** geçerli bir Azure hello tooprovision istediğiniz Active Directory hesabı kutularındaki ilgili.</span><span class="sxs-lookup"><span data-stu-id="dfe94-247">Type hello **Username**, **Password**, **Confirm Password**, **First Name**, **Last Name**, **Email Address** of a valid Azure Active Directory account you want tooprovision into hello related textboxes.</span></span>
   2. <span data-ttu-id="dfe94-248">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="dfe94-248">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="dfe94-249">API AAD kullanıcı hesaplarının AirWatch tooprovision tarafından sağlanan veya herhangi diğer AirWatch kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dfe94-249">You can use any other AirWatch user account creation tools or APIs provided by AirWatch tooprovision AAD user accounts.</span></span>
>  

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="dfe94-250">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="dfe94-250">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="dfe94-251">Bu bölümde, erişim tooAirWatch vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="dfe94-251">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAirWatch.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="dfe94-253">**tooassign Britta Simon tooAirWatch hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="dfe94-253">**tooassign Britta Simon tooAirWatch, perform hello following steps:**</span></span>

1. <span data-ttu-id="dfe94-254">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="dfe94-254">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="dfe94-256">Merhaba uygulamalar listesinde **AirWatch**.</span><span class="sxs-lookup"><span data-stu-id="dfe94-256">In hello applications list, select **AirWatch**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_app.png) 

3. <span data-ttu-id="dfe94-258">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="dfe94-258">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="dfe94-260">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="dfe94-260">Click **Add** button.</span></span> <span data-ttu-id="dfe94-261">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="dfe94-261">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="dfe94-263">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="dfe94-263">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="dfe94-264">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="dfe94-264">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="dfe94-265">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="dfe94-265">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="dfe94-266">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="dfe94-266">Testing single sign-on</span></span>

<span data-ttu-id="dfe94-267">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="dfe94-267">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="dfe94-268">Çoklu oturum açma ayarlarınızı tootest istiyorsanız hello erişim paneli açın.</span><span class="sxs-lookup"><span data-stu-id="dfe94-268">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="dfe94-269">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="dfe94-269">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="dfe94-270">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="dfe94-270">Additional resources</span></span>

* [<span data-ttu-id="dfe94-271">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="dfe94-271">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="dfe94-272">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="dfe94-272">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_203.png

