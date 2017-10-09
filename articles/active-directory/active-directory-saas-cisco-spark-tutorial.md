---
title: "Öğretici: Cisco Spark Azure Active Directory Tümleştirme | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve Cisco Spark arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c47894b1-f5df-4755-845d-f12f4c602dc4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 386c4fd816095e1c61de01dd1dee1bbd00311a04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-spark"></a><span data-ttu-id="e2b06-103">Öğretici: Cisco Spark Azure Active Directory Tümleştirme</span><span class="sxs-lookup"><span data-stu-id="e2b06-103">Tutorial: Azure Active Directory integration with Cisco Spark</span></span>

<span data-ttu-id="e2b06-104">Bu öğreticide, bilgi toointegrate Cisco Spark nasıl Azure Active Directory (Azure AD) ile.</span><span class="sxs-lookup"><span data-stu-id="e2b06-104">In this tutorial, you learn how toointegrate Cisco Spark with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e2b06-105">Cisco Spark Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="e2b06-105">Integrating Cisco Spark with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e2b06-106">Erişim tooCisco Spark sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="e2b06-106">You can control in Azure AD who has access tooCisco Spark</span></span>
- <span data-ttu-id="e2b06-107">Kullanıcıların tooautomatically get açan tooCisco Spark (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="e2b06-107">You can enable your users tooautomatically get signed-on tooCisco Spark (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e2b06-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="e2b06-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e2b06-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e2b06-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e2b06-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e2b06-110">Prerequisites</span></span>

<span data-ttu-id="e2b06-111">Cisco Spark ile Azure AD tümleştirme tooconfigure, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="e2b06-111">tooconfigure Azure AD integration with Cisco Spark, you need hello following items:</span></span>

- <span data-ttu-id="e2b06-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="e2b06-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e2b06-113">Bir Cisco Spark çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="e2b06-113">A Cisco Spark single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e2b06-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="e2b06-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e2b06-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="e2b06-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e2b06-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="e2b06-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e2b06-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e2b06-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e2b06-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="e2b06-118">Scenario description</span></span>
<span data-ttu-id="e2b06-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="e2b06-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e2b06-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="e2b06-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e2b06-121">Cisco Spark hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="e2b06-121">Adding Cisco Spark from hello gallery</span></span>
2. <span data-ttu-id="e2b06-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="e2b06-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cisco-spark-from-hello-gallery"></a><span data-ttu-id="e2b06-123">Cisco Spark hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="e2b06-123">Adding Cisco Spark from hello gallery</span></span>
<span data-ttu-id="e2b06-124">Azure AD'ye tooconfigure hello tümleştirme Cisco Spark, tooadd Cisco Spark hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="e2b06-124">tooconfigure hello integration of Cisco Spark into Azure AD, you need tooadd Cisco Spark from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e2b06-125">**tooadd Cisco Spark hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e2b06-125">**tooadd Cisco Spark from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e2b06-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="e2b06-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e2b06-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="e2b06-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e2b06-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="e2b06-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="e2b06-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e2b06-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="e2b06-133">Merhaba arama kutusuna yazın **Cisco Spark**.</span><span class="sxs-lookup"><span data-stu-id="e2b06-133">In hello search box, type **Cisco Spark**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_search.png)

5. <span data-ttu-id="e2b06-135">Merhaba Sonuçlar panelinde seçin **Cisco Spark**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="e2b06-135">In hello results panel, select **Cisco Spark**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e2b06-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="e2b06-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e2b06-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma Cisco "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Spark ile test etme</span><span class="sxs-lookup"><span data-stu-id="e2b06-138">In this section, you configure and test Azure AD single sign-on with Cisco Spark based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e2b06-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Cisco Spark tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="e2b06-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Cisco Spark is tooa user in Azure AD.</span></span> <span data-ttu-id="e2b06-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve Cisco Spark hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="e2b06-140">In other words, a link relationship between an Azure AD user and hello related user in Cisco Spark needs toobe established.</span></span>

<span data-ttu-id="e2b06-141">Cisco Spark hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="e2b06-141">In Cisco Spark, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e2b06-142">tooconfigure ve Cisco Spark ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="e2b06-142">tooconfigure and test Azure AD single sign-on with Cisco Spark, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e2b06-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="e2b06-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e2b06-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="e2b06-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e2b06-145">**[Cisco Spark test kullanıcısı oluşturma](#creating-a-cisco-spark-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Cisco Spark, karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="e2b06-145">**[Creating a Cisco Spark test user](#creating-a-cisco-spark-test-user)** - toohave a counterpart of Britta Simon in Cisco Spark that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e2b06-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="e2b06-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e2b06-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="e2b06-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e2b06-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e2b06-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e2b06-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Cisco Spark uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="e2b06-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Cisco Spark application.</span></span>

<span data-ttu-id="e2b06-150">**tooconfigure Azure AD çoklu oturum açma Cisco Spark ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e2b06-150">**tooconfigure Azure AD single sign-on with Cisco Spark, perform hello following steps:**</span></span>

1. <span data-ttu-id="e2b06-151">Hello hello üzerinde Azure portal'ın **Cisco Spark** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="e2b06-151">In hello Azure portal, on hello **Cisco Spark** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="e2b06-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="e2b06-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_samlbase.png)

3. <span data-ttu-id="e2b06-155">Merhaba üzerinde **Cisco Spark etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e2b06-155">On hello **Cisco Spark Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_url.png)

    <span data-ttu-id="e2b06-157">a.</span><span class="sxs-lookup"><span data-stu-id="e2b06-157">a.</span></span> <span data-ttu-id="e2b06-158">Merhaba, **oturum açma URL'si** metin kutusuna, URL'yi yazın:`https://web.ciscospark.com/#/signin`</span><span class="sxs-lookup"><span data-stu-id="e2b06-158">In hello **Sign-on URL** textbox, type a URL as: `https://web.ciscospark.com/#/signin`</span></span>

    <span data-ttu-id="e2b06-159">b.</span><span class="sxs-lookup"><span data-stu-id="e2b06-159">b.</span></span> <span data-ttu-id="e2b06-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://idbroker.webex.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="e2b06-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://idbroker.webex.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e2b06-161">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="e2b06-161">This value is not real.</span></span> <span data-ttu-id="e2b06-162">Bu değer ile Merhaba güncelleştirme gerçek tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="e2b06-162">Update this value with hello actual Identifier.</span></span> <span data-ttu-id="e2b06-163">Kişi [Cisco Spark istemci destek ekibi](https://support.ciscospark.com/) tooget bu değer.</span><span class="sxs-lookup"><span data-stu-id="e2b06-163">Contact [Cisco Spark Client support team](https://support.ciscospark.com/) tooget this value.</span></span> 
 
4. <span data-ttu-id="e2b06-164">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e2b06-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_certificate.png) 

5. <span data-ttu-id="e2b06-166">Cisco Spark uygulama hello SAML onaylar toocontain özel öznitelikler bekler.</span><span class="sxs-lookup"><span data-stu-id="e2b06-166">Cisco Spark application expects hello SAML assertions toocontain specific attributes.</span></span> <span data-ttu-id="e2b06-167">Bu uygulama için öznitelikler aşağıdaki hello yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="e2b06-167">Configure hello following attributes  for this application.</span></span> <span data-ttu-id="e2b06-168">Hello başlangıç değerleri bu özniteliklerin yönetebilirsiniz **kullanıcı öznitelikleri** uygulama tümleştirmesi sayfasında bölüm.</span><span class="sxs-lookup"><span data-stu-id="e2b06-168">You can manage hello values of these attributes from hello **User Attributes** section on application integration page.</span></span> <span data-ttu-id="e2b06-169">Ekran aşağıdaki hello bunun bir örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="e2b06-169">hello following screenshot shows an example for this.</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_07.png) 

6. <span data-ttu-id="e2b06-171">Merhaba, **kullanıcı öznitelikleri** hello bölüm **çoklu oturum açma** iletişim kutusunda, SAML belirteci özniteliği yukarıdaki hello resimde gösterildiği gibi yapılandırmak ve hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e2b06-171">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="e2b06-172">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="e2b06-172">Attribute Name</span></span>  | <span data-ttu-id="e2b06-173">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="e2b06-173">Attribute Value</span></span> |
    | --------------- | -------------------- |    
    |   <span data-ttu-id="e2b06-174">Kullanıcı Kimliği</span><span class="sxs-lookup"><span data-stu-id="e2b06-174">uid</span></span>    | <span data-ttu-id="e2b06-175">User.userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="e2b06-175">user.userprincipalname</span></span> |   

    <span data-ttu-id="e2b06-176">a.</span><span class="sxs-lookup"><span data-stu-id="e2b06-176">a.</span></span> <span data-ttu-id="e2b06-177">Tıklatın **Ekle özniteliği** tooopen hello **özniteliği eklemek** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e2b06-177">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cisco-spark-tutorial/tutorial_attribute_04.png)

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cisco-spark-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="e2b06-180">b.</span><span class="sxs-lookup"><span data-stu-id="e2b06-180">b.</span></span> <span data-ttu-id="e2b06-181">Merhaba, **adı** metin kutusuna, ilgili satır için gösterilen türü hello öznitelik adı.</span><span class="sxs-lookup"><span data-stu-id="e2b06-181">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="e2b06-182">c.</span><span class="sxs-lookup"><span data-stu-id="e2b06-182">c.</span></span> <span data-ttu-id="e2b06-183">Merhaba gelen **değeri** listesinde, ilgili satır için gösterilen türü hello öznitelik değeri.</span><span class="sxs-lookup"><span data-stu-id="e2b06-183">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="e2b06-184">d.</span><span class="sxs-lookup"><span data-stu-id="e2b06-184">d.</span></span> <span data-ttu-id="e2b06-185">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e2b06-185">Click **Ok**.</span></span>

7. <span data-ttu-id="e2b06-186">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e2b06-186">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="e2b06-188">Çok oturum[Cisco bulut işbirliği Yönetimi](https://admin.ciscospark.com/) tam yönetici kimlik bilgilerinizle.</span><span class="sxs-lookup"><span data-stu-id="e2b06-188">Sign in too[Cisco Cloud Collaboration Management](https://admin.ciscospark.com/) with your full administrator credentials.</span></span>

9. <span data-ttu-id="e2b06-189">Seçin **ayarları** ve hello altında **kimlik doğrulaması** 'yi tıklatın **Değiştir**.</span><span class="sxs-lookup"><span data-stu-id="e2b06-189">Select **Settings** and under hello **Authentication** section, click **Modify**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_10.png)
    
10. <span data-ttu-id="e2b06-191">Seçin **3. taraf kimlik sağlayıcısı tümleştirin. (Gelişmiş)**  ve Git toohello sonraki ekran.</span><span class="sxs-lookup"><span data-stu-id="e2b06-191">Select **Integrate a 3rd-party identity provider. (Advanced)** and go toohello next screen.</span></span>

11. <span data-ttu-id="e2b06-192">Merhaba üzerinde **IDP meta verileri içeri aktarma** sayfasında, ya da sürükle ve bırak hello Azure AD meta veri dosyası hello sayfaya veya hello dosya tarayıcısı seçeneği toolocate kullanabilir ve hello Azure AD meta veri dosyasını karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="e2b06-192">On hello **Import Idp Metadata** page, either drag and drop hello Azure AD metadata file onto hello page or use hello file browser option toolocate and upload hello Azure AD metadata file.</span></span> <span data-ttu-id="e2b06-193">Ardından, seçin **meta veriler (daha güvenli) bir sertifika yetkilisi tarafından imzalanan sertifika gerekli** tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="e2b06-193">Then, select **Require certificate signed by a certificate authority in Metadata (more secure)** and click **Next**.</span></span> 
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_11.png)

12. <span data-ttu-id="e2b06-195">Seçin **SSO Bağlantıyı Sına**ve yeni bir tarayıcı sekmesinde oturum açtığında, Azure AD ile oturum açarak kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="e2b06-195">Select **Test SSO Connection**, and when a new browser tab opens, authenticate with Azure AD by signing in.</span></span>

13. <span data-ttu-id="e2b06-196">Toohello iade **Cisco bulut işbirliği Yönetim** tarayıcı sekmesinde. Merhaba testi başarılı olursa seçin **bu test başarılı oldu. Çoklu oturum açma seçeneği etkinleştirme** tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="e2b06-196">Return toohello **Cisco Cloud Collaboration Management** browser tab. If hello test was successful, select **This test was successful. Enable Single Sign-On option** and click **Next**.</span></span>

> [!TIP]
> <span data-ttu-id="e2b06-197">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="e2b06-197">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e2b06-198">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="e2b06-198">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e2b06-199">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e2b06-199">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e2b06-200">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e2b06-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="e2b06-201">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="e2b06-201">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="e2b06-203">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e2b06-203">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e2b06-204">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="e2b06-204">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e2b06-206">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="e2b06-206">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e2b06-208">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="e2b06-208">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e2b06-210">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e2b06-210">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e2b06-212">a.</span><span class="sxs-lookup"><span data-stu-id="e2b06-212">a.</span></span> <span data-ttu-id="e2b06-213">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e2b06-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e2b06-214">b.</span><span class="sxs-lookup"><span data-stu-id="e2b06-214">b.</span></span> <span data-ttu-id="e2b06-215">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="e2b06-215">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e2b06-216">c.</span><span class="sxs-lookup"><span data-stu-id="e2b06-216">c.</span></span> <span data-ttu-id="e2b06-217">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="e2b06-217">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e2b06-218">d.</span><span class="sxs-lookup"><span data-stu-id="e2b06-218">d.</span></span> <span data-ttu-id="e2b06-219">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e2b06-219">Click **Create**.</span></span>
 
### <a name="creating-a-cisco-spark-test-user"></a><span data-ttu-id="e2b06-220">Cisco Spark test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e2b06-220">Creating a Cisco Spark test user</span></span>

<span data-ttu-id="e2b06-221">Bu bölümde, Cisco Spark Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e2b06-221">In this section, you create a user called Britta Simon in Cisco Spark.</span></span> <span data-ttu-id="e2b06-222">Bu bölümde, Cisco Spark Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e2b06-222">In this section, you create a user called Britta Simon in Cisco Spark.</span></span>

1. <span data-ttu-id="e2b06-223">Toohello Git [Cisco bulut işbirliği Yönetimi](https://admin.ciscospark.com/) tam yönetici kimlik bilgilerinizle.</span><span class="sxs-lookup"><span data-stu-id="e2b06-223">Go toohello [Cisco Cloud Collaboration Management](https://admin.ciscospark.com/) with your full administrator credentials.</span></span>

2. <span data-ttu-id="e2b06-224">Tıklatın **kullanıcılar** ve ardından **kullanıcıları yönetme**.</span><span class="sxs-lookup"><span data-stu-id="e2b06-224">Click **Users** and then **Manage Users**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_12.png) 

3. <span data-ttu-id="e2b06-226">Merhaba, **yönetmek kullanıcı** penceresinde, seçin **el ile ekleyin veya kullanıcıları değiştirin** tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="e2b06-226">In hello **Manage User** window, select **Manually add or modify users** and click **Next**.</span></span>

4. <span data-ttu-id="e2b06-227">Seçin **adlarını ve e-posta adresi**.</span><span class="sxs-lookup"><span data-stu-id="e2b06-227">Select **Names and Email address**.</span></span> <span data-ttu-id="e2b06-228">Ardından, hello textbox aşağıdaki gibi doldurun:</span><span class="sxs-lookup"><span data-stu-id="e2b06-228">Then, fill out hello textbox as follows:</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_13.png) 
    
    <span data-ttu-id="e2b06-230">a.</span><span class="sxs-lookup"><span data-stu-id="e2b06-230">a.</span></span> <span data-ttu-id="e2b06-231">Merhaba, **ad** metin kutusuna, türü **Britta**.</span><span class="sxs-lookup"><span data-stu-id="e2b06-231">In hello **First Name** textbox, type **Britta**.</span></span> 
    
    <span data-ttu-id="e2b06-232">b.</span><span class="sxs-lookup"><span data-stu-id="e2b06-232">b.</span></span> <span data-ttu-id="e2b06-233">Merhaba, **Soyadı** metin kutusuna, türü **Simon**.</span><span class="sxs-lookup"><span data-stu-id="e2b06-233">In hello **Last Name** textbox, type **Simon**.</span></span>
    
    <span data-ttu-id="e2b06-234">c.</span><span class="sxs-lookup"><span data-stu-id="e2b06-234">c.</span></span> <span data-ttu-id="e2b06-235">Merhaba, **e-posta adresi** metin kutusuna, türü  **britta.simon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="e2b06-235">In hello **Email address** textbox, type **britta.simon@contoso.com**.</span></span>

5. <span data-ttu-id="e2b06-236">Yanı sıra tooadd Britta Simon oturum Hello'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="e2b06-236">Click hello plus sign tooadd Britta Simon.</span></span> <span data-ttu-id="e2b06-237">Ardından **İleri**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e2b06-237">Then, click **Next**.</span></span>

6. <span data-ttu-id="e2b06-238">Merhaba, **Hizmetleri kullanıcıları eklemek** penceresinde tıklatın **kaydetmek** ve ardından **son**.</span><span class="sxs-lookup"><span data-stu-id="e2b06-238">In hello **Add Services for Users** window, click **Save** and then **Finish**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e2b06-239">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="e2b06-239">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e2b06-240">Bu bölümde, erişim tooCisco Spark vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="e2b06-240">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCisco Spark.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="e2b06-242">**tooassign Britta Simon tooCisco Spark, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e2b06-242">**tooassign Britta Simon tooCisco Spark, perform hello following steps:**</span></span>

1. <span data-ttu-id="e2b06-243">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="e2b06-243">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="e2b06-245">Merhaba uygulamalar listesinde **Cisco Spark**.</span><span class="sxs-lookup"><span data-stu-id="e2b06-245">In hello applications list, select **Cisco Spark**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_app.png) 

3. <span data-ttu-id="e2b06-247">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="e2b06-247">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="e2b06-249">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e2b06-249">Click **Add** button.</span></span> <span data-ttu-id="e2b06-250">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e2b06-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="e2b06-252">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="e2b06-252">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e2b06-253">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e2b06-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e2b06-254">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e2b06-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e2b06-255">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="e2b06-255">Testing single sign-on</span></span>

<span data-ttu-id="e2b06-256">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD SSO yapılandırmayı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="e2b06-256">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="e2b06-257">Merhaba Cisco Spark hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Cisco Spark uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e2b06-257">When you click hello Cisco Spark tile in hello Access Panel, you should get automatically signed-on tooyour Cisco Spark application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e2b06-258">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="e2b06-258">Additional resources</span></span>

* [<span data-ttu-id="e2b06-259">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="e2b06-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e2b06-260">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="e2b06-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_04.png
[10]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_060.png
[100]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_203.png

