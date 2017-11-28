---
title: "Öğretici: Azure Active Directory Tümleştirme Salesforce ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve Salesforce arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2d7d420-dc91-41b8-a6b3-59579e043b35
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 1d848518ee30910e051cdc4746c599219f3b5a3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce"></a><span data-ttu-id="616d1-103">Öğretici: Salesforce Azure Active Directory Tümleştirme</span><span class="sxs-lookup"><span data-stu-id="616d1-103">Tutorial: Azure Active Directory integration with Salesforce</span></span>

<span data-ttu-id="616d1-104">Bu öğreticide, bilgi nasıl toointegrate Salesforce Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="616d1-104">In this tutorial, you learn how toointegrate Salesforce with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="616d1-105">Salesforce Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="616d1-105">Integrating Salesforce with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="616d1-106">Erişim tooSalesforce sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="616d1-106">You can control in Azure AD who has access tooSalesforce</span></span>
- <span data-ttu-id="616d1-107">Kullanıcıların tooautomatically get açan tooSalesforce (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="616d1-107">You can enable your users tooautomatically get signed-on tooSalesforce (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="616d1-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="616d1-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="616d1-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="616d1-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="616d1-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="616d1-110">Prerequisites</span></span>

<span data-ttu-id="616d1-111">Salesforce ile Azure AD tümleştirme tooconfigure, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="616d1-111">tooconfigure Azure AD integration with Salesforce, you need hello following items:</span></span>

- <span data-ttu-id="616d1-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="616d1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="616d1-113">Bir Salesforce çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="616d1-113">A Salesforce single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="616d1-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="616d1-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="616d1-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="616d1-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="616d1-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="616d1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="616d1-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="616d1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="616d1-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="616d1-118">Scenario description</span></span>
<span data-ttu-id="616d1-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="616d1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="616d1-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="616d1-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="616d1-121">Salesforce hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="616d1-121">Adding Salesforce from hello gallery</span></span>
2. <span data-ttu-id="616d1-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="616d1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-salesforce-from-hello-gallery"></a><span data-ttu-id="616d1-123">Salesforce hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="616d1-123">Adding Salesforce from hello gallery</span></span>
<span data-ttu-id="616d1-124">Azure AD'ye tooconfigure hello tümleştirme Salesforce, tooadd Salesforce hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="616d1-124">tooconfigure hello integration of Salesforce into Azure AD, you need tooadd Salesforce from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="616d1-125">**tooadd hello galerisinden Salesforce hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="616d1-125">**tooadd Salesforce from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="616d1-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="616d1-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="616d1-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="616d1-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="616d1-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="616d1-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="616d1-131">Tıklatın **yeni uygulama** hello iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="616d1-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="616d1-133">Merhaba arama kutusuna yazın **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="616d1-133">In hello search box, type **Salesforce**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_search.png)

5. <span data-ttu-id="616d1-135">Merhaba Sonuçlar panelinde seçin **Salesforce**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="616d1-135">In hello results panel, select **Salesforce**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="616d1-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="616d1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="616d1-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Salesforce ile test etme</span><span class="sxs-lookup"><span data-stu-id="616d1-138">In this section, you configure and test Azure AD single sign-on with Salesforce based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="616d1-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Salesforce içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="616d1-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Salesforce is tooa user in Azure AD.</span></span> <span data-ttu-id="616d1-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Salesforce hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="616d1-140">In other words, a link relationship between an Azure AD user and hello related user in Salesforce needs toobe established.</span></span>

<span data-ttu-id="616d1-141">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** Salesforce içinde.</span><span class="sxs-lookup"><span data-stu-id="616d1-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Salesforce.</span></span>

<span data-ttu-id="616d1-142">tooconfigure ve Salesforce ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="616d1-142">tooconfigure and test Azure AD single sign-on with Salesforce, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="616d1-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="616d1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="616d1-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="616d1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="616d1-145">**[Salesforce test kullanıcısı oluşturma](#creating-a-salesforce-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Salesforce içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="616d1-145">**[Creating a Salesforce test user](#creating-a-salesforce-test-user)** - toohave a counterpart of Britta Simon in Salesforce that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="616d1-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="616d1-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="616d1-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="616d1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="616d1-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="616d1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="616d1-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Salesforce uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="616d1-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Salesforce application.</span></span>

<span data-ttu-id="616d1-150">**tooconfigure Azure AD çoklu oturum açma Salesforce ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="616d1-150">**tooconfigure Azure AD single sign-on with Salesforce, perform hello following steps:**</span></span>

1. <span data-ttu-id="616d1-151">Hello hello üzerinde Azure portal'ın **Salesforce** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="616d1-151">In hello Azure portal, on hello **Salesforce** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="616d1-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="616d1-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_samlbase.png)

3. <span data-ttu-id="616d1-155">Merhaba üzerinde **Salesforce etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="616d1-155">On hello **Salesforce Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_url.png)

    <span data-ttu-id="616d1-157">Merhaba, **oturum açma URL'si** metin kutusuna, desen aşağıdaki hello kullanarak türü hello değeri:</span><span class="sxs-lookup"><span data-stu-id="616d1-157">In hello **Sign-on URL** textbox, type hello value using hello following pattern:</span></span> 
   * <span data-ttu-id="616d1-158">Kurumsal hesap:`https://<subdomain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="616d1-158">Enterprise account: `https://<subdomain>.my.salesforce.com`</span></span>
   * <span data-ttu-id="616d1-159">Geliştirici hesabı:`https://<subdomain>-dev-ed.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="616d1-159">Developer account: `https://<subdomain>-dev-ed.my.salesforce.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="616d1-160">Bu değerler hello gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="616d1-160">These values are not hello real.</span></span> <span data-ttu-id="616d1-161">Bu değerleri hello gerçek oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="616d1-161">Update these values with hello actual Sign-on URL.</span></span> <span data-ttu-id="616d1-162">Kişi [Salesforce istemci destek ekibi](https://help.salesforce.com/support) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="616d1-162">Contact [Salesforce Client support team](https://help.salesforce.com/support) tooget these values.</span></span> 
 
4. <span data-ttu-id="616d1-163">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="616d1-163">On hello **SAML Signing Certificate** section, click **Certificate** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_certificate.png) 

5. <span data-ttu-id="616d1-165">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="616d1-165">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforce-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="616d1-167">Merhaba üzerinde **Salesforce yapılandırma** 'yi tıklatın **yapılandırma Salesforce** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="616d1-167">On hello **Salesforce Configuration** section, click **Configure Salesforce** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="616d1-168">Kopya hello **SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="616d1-168">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span> 

    <span data-ttu-id="616d1-169">![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="616d1-169">![Configure Single Sign-On](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_configure.png) 
<CS></span></span>
7.  <span data-ttu-id="616d1-170">Tarayıcınızda yeni bir sekme açın ve oturum tooyour Salesforce yönetici hesabı.</span><span class="sxs-lookup"><span data-stu-id="616d1-170">Open a new tab in your browser and log in tooyour Salesforce administrator account.</span></span>

8.  <span data-ttu-id="616d1-171">Merhaba altında **yönetici** Gezinti bölmesinde, tıklatın **güvenlik denetimleri** tooexpand hello ilgili bölümü.</span><span class="sxs-lookup"><span data-stu-id="616d1-171">Under hello **Administrator** navigation pane, click **Security Controls** tooexpand hello related section.</span></span> <span data-ttu-id="616d1-172">Ardından **çoklu oturum açma ayarları**.</span><span class="sxs-lookup"><span data-stu-id="616d1-172">Then click **Single Sign-On Settings**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso.png)

9.  <span data-ttu-id="616d1-174">Merhaba üzerinde **çoklu oturum açma ayarları** hello sayfasında, **Düzenle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="616d1-174">On hello **Single Sign-On Settings** page, click hello **Edit** button.</span></span>
    <span data-ttu-id="616d1-175">![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-edit.png)</span><span class="sxs-lookup"><span data-stu-id="616d1-175">![Configure Single Sign-On](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-edit.png)</span></span>

      > [!NOTE]
      > <span data-ttu-id="616d1-176">Salesforce hesabınız için oluşturulamıyor tooenable çoklu oturum açma ayarları varsa, toocontact gerekebilir [Salesforce istemci destek ekibi](https://help.salesforce.com/support).</span><span class="sxs-lookup"><span data-stu-id="616d1-176">If you are unable tooenable Single Sign-On settings for your Salesforce account, you may need toocontact [Salesforce Client support team](https://help.salesforce.com/support).</span></span> 

10. <span data-ttu-id="616d1-177">Seçin **SAML etkin**ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="616d1-177">Select **SAML Enabled**, and then click **Save**.</span></span>

      ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforce-tutorial/sf-enable-saml.png)
11. <span data-ttu-id="616d1-179">SAML çoklu oturum açma ayarlarınızı tooconfigure tıklatın **yeni**.</span><span class="sxs-lookup"><span data-stu-id="616d1-179">tooconfigure your SAML single sign-on settings, click **New**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-new.png)

12. <span data-ttu-id="616d1-181">Merhaba üzerinde **SAML çoklu oturum açma ayarını Düzenle** sayfasında, aşağıdaki yapılandırmaları hello olun:</span><span class="sxs-lookup"><span data-stu-id="616d1-181">On hello **SAML Single Sign-On Setting Edit** page, make hello following configurations:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforce-tutorial/sf-saml-config.png)

    <span data-ttu-id="616d1-183">a.</span><span class="sxs-lookup"><span data-stu-id="616d1-183">a.</span></span> <span data-ttu-id="616d1-184">Hello için **adı** alanına, bu yapılandırma için bir kolay ad yazın.</span><span class="sxs-lookup"><span data-stu-id="616d1-184">For hello **Name** field, type in a friendly name for this configuration.</span></span> <span data-ttu-id="616d1-185">İçin bir değer sağlama **adı** hello otomatik olarak doldurulması **API adı** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="616d1-185">Providing a value for **Name** automatically populate hello **API Name** textbox.</span></span>

    <span data-ttu-id="616d1-186">b.</span><span class="sxs-lookup"><span data-stu-id="616d1-186">b.</span></span> <span data-ttu-id="616d1-187">Yapıştır **SMAL varlık kimliği** hello değerine **veren** Salesforce alanındaki.</span><span class="sxs-lookup"><span data-stu-id="616d1-187">Paste **SMAL Entity ID** value into hello **Issuer** field in Salesforce.</span></span>

    <span data-ttu-id="616d1-188">c.</span><span class="sxs-lookup"><span data-stu-id="616d1-188">c.</span></span> <span data-ttu-id="616d1-189">Merhaba, **varlık kimliği textbox**, desen aşağıdaki hello kullanarak Salesforce etki alanı adınızı yazın:</span><span class="sxs-lookup"><span data-stu-id="616d1-189">In hello **Entity Id textbox**, type your Salesforce domain name using hello following pattern:</span></span>
      
      * <span data-ttu-id="616d1-190">Kurumsal hesap:`https://<subdomain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="616d1-190">Enterprise account: `https://<subdomain>.my.salesforce.com`</span></span>
      * <span data-ttu-id="616d1-191">Geliştirici hesabı:`https://<subdomain>-dev-ed.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="616d1-191">Developer account: `https://<subdomain>-dev-ed.my.salesforce.com`</span></span>
      
    <span data-ttu-id="616d1-192">d.</span><span class="sxs-lookup"><span data-stu-id="616d1-192">d.</span></span> <span data-ttu-id="616d1-193">Tıklatın **Gözat** veya **Dosya Seç** tooopen hello **Dosya Seç tooUpload** iletişim kutusunda, Salesforce sertifikanızı seçin ve ardından **açmak**tooupload hello sertifika.</span><span class="sxs-lookup"><span data-stu-id="616d1-193">Click **Browse** or **Choose File** tooopen hello **Choose File tooUpload** dialog, select your Salesforce certificate, and then click **Open** tooupload hello certificate.</span></span>

    <span data-ttu-id="616d1-194">e.</span><span class="sxs-lookup"><span data-stu-id="616d1-194">e.</span></span> <span data-ttu-id="616d1-195">İçin **SAML kimlik türü**seçin **onaylamayı kullanıcının salesforce.com kullanıcı adını içeren**.</span><span class="sxs-lookup"><span data-stu-id="616d1-195">For **SAML Identity Type**, select **Assertion contains User's salesforce.com username**.</span></span>

    <span data-ttu-id="616d1-196">f.</span><span class="sxs-lookup"><span data-stu-id="616d1-196">f.</span></span> <span data-ttu-id="616d1-197">İçin **SAML kimlik konumu**seçin **kimliktir hello NameIdentifier öğesinde hello konu deyimi**</span><span class="sxs-lookup"><span data-stu-id="616d1-197">For **SAML Identity Location**, select **Identity is in hello NameIdentifier element of hello Subject statement**</span></span>

    <span data-ttu-id="616d1-198">g.</span><span class="sxs-lookup"><span data-stu-id="616d1-198">g.</span></span> <span data-ttu-id="616d1-199">Yapıştır **çoklu oturum açma hizmet URL'si** hello içine **kimlik sağlayıcısı oturum açma URL'si** Salesforce alanındaki.</span><span class="sxs-lookup"><span data-stu-id="616d1-199">Paste **Single Sign-On Service URL** into hello **Identity Provider Login URL** field in Salesforce.</span></span>
    
    <span data-ttu-id="616d1-200">h.</span><span class="sxs-lookup"><span data-stu-id="616d1-200">h.</span></span> <span data-ttu-id="616d1-201">İçin **hizmet sağlayıcısı tarafından başlatılan bağlama isteği**seçin **HTTP yeniden yönlendirme**.</span><span class="sxs-lookup"><span data-stu-id="616d1-201">For **Service Provider Initiated Request Binding**, select **HTTP Redirect**.</span></span>
    
    <span data-ttu-id="616d1-202">ı.</span><span class="sxs-lookup"><span data-stu-id="616d1-202">i.</span></span> <span data-ttu-id="616d1-203">Son olarak, tıklatın **kaydetmek** tooapply, SAML çoklu oturum açma ayarları.</span><span class="sxs-lookup"><span data-stu-id="616d1-203">Finally, click **Save** tooapply your SAML single sign-on settings.</span></span>

13. <span data-ttu-id="616d1-204">Merhaba sol gezinti Salesforce bölmesinde **etki alanı yönetimi** tooexpand hello ilgili bölümü ve ardından **My etki alanı**.</span><span class="sxs-lookup"><span data-stu-id="616d1-204">On hello left navigation pane in Salesforce, click **Domain Management** tooexpand hello related section, and then click **My Domain**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforce-tutorial/sf-my-domain.png)

14. <span data-ttu-id="616d1-206">Toohello aşağı **kimlik doğrulama Yapılandırması** bölümünde ve hello tıklatın **Düzenle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="616d1-206">Scroll down toohello **Authentication Configuration** section, and click hello **Edit** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforce-tutorial/sf-edit-auth-config.png)

15. <span data-ttu-id="616d1-208">Merhaba, **kimlik doğrulama hizmeti** bölümünde, SAML SSO yapılandırmanızın hello kolay ad seçin ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="616d1-208">In hello **Authentication Service** section, select hello friendly name of your SAML SSO configuration, and then click **Save**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforce-tutorial/sf-auth-config.png)

    > [!NOTE]
    > <span data-ttu-id="616d1-210">Birden fazla kimlik doğrulama hizmeti seçili ise, hangi kimlik doğrulama hizmeti oldukları gibi istendiğinde tooselect kullanıcılardır tek oturum açma tooyour Salesforce ortamını başlatma sırasında toosign ile.</span><span class="sxs-lookup"><span data-stu-id="616d1-210">If more than one authentication service is selected, users are prompted tooselect which authentication service they like toosign in with while initiating single sign-on tooyour Salesforce environment.</span></span> <span data-ttu-id="616d1-211">Toohappen istemediğiniz sonra yapmanız gerekenler **diğer tüm kimlik doğrulama hizmetleri işaretlemeden bırakın**.</span><span class="sxs-lookup"><span data-stu-id="616d1-211">If you don’t want it toohappen, then you should **leave all other authentication services unchecked**.</span></span>
<CE>    
> [!TIP]
> <span data-ttu-id="616d1-212">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="616d1-212">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="616d1-213">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="616d1-213">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="616d1-214">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="616d1-214">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="616d1-215">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="616d1-215">Creating an Azure AD test user</span></span>
<span data-ttu-id="616d1-216">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="616d1-216">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="616d1-218">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="616d1-218">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="616d1-219">Merhaba hello sol gezinti bölmesindeki **Azure portal**, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="616d1-219">On hello left navigation pane in hello **Azure portal**, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-salesforce-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="616d1-221">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="616d1-221">toodisplay hello list of users, Go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-salesforce-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="616d1-223">Merhaba iletişim Hello üstünde tıklatın **Ekle** tooopen hello **kullanıcı** iletişim.</span><span class="sxs-lookup"><span data-stu-id="616d1-223">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-salesforce-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="616d1-225">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="616d1-225">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-salesforce-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="616d1-227">a.</span><span class="sxs-lookup"><span data-stu-id="616d1-227">a.</span></span> <span data-ttu-id="616d1-228">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="616d1-228">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="616d1-229">b.</span><span class="sxs-lookup"><span data-stu-id="616d1-229">b.</span></span> <span data-ttu-id="616d1-230">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="616d1-230">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="616d1-231">c.</span><span class="sxs-lookup"><span data-stu-id="616d1-231">c.</span></span> <span data-ttu-id="616d1-232">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="616d1-232">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="616d1-233">d.</span><span class="sxs-lookup"><span data-stu-id="616d1-233">d.</span></span> <span data-ttu-id="616d1-234">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="616d1-234">Click **Create**.</span></span>
 
### <a name="creating-a-salesforce-test-user"></a><span data-ttu-id="616d1-235">Salesforce test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="616d1-235">Creating a Salesforce test user</span></span>

<span data-ttu-id="616d1-236">Bu bölümde, Britta Simon adlı bir kullanıcı Salesforce'ta oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="616d1-236">In this section, a user called Britta Simon is created in Salesforce.</span></span> <span data-ttu-id="616d1-237">Salesforce yalnızca zaman sağlama, varsayılan olarak etkin olduğu destekler.</span><span class="sxs-lookup"><span data-stu-id="616d1-237">Salesforce supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="616d1-238">Bu bölümde, eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="616d1-238">There is no action item for you in this section.</span></span> <span data-ttu-id="616d1-239">Bir kullanıcı zaten Salesforce'ta yoksa, tooaccess Salesforce çalıştığında yeni bir tane oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="616d1-239">If a user doesn't already exist in Salesforce, a new one is created when you attempt tooaccess Salesforce.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="616d1-240">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="616d1-240">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="616d1-241">Bu bölümde, erişim tooSalesforce vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="616d1-241">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSalesforce.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="616d1-243">**tooassign Britta Simon tooSalesforce hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="616d1-243">**tooassign Britta Simon tooSalesforce, perform hello following steps:**</span></span>

1. <span data-ttu-id="616d1-244">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="616d1-244">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="616d1-246">Merhaba uygulamalar listesinde **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="616d1-246">In hello applications list, select **Salesforce**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_app.png) 

3. <span data-ttu-id="616d1-248">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="616d1-248">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="616d1-250">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="616d1-250">Click **Add** button.</span></span> <span data-ttu-id="616d1-251">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="616d1-251">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="616d1-253">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="616d1-253">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="616d1-254">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="616d1-254">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="616d1-255">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="616d1-255">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="616d1-256">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="616d1-256">Testing single sign-on</span></span>

<span data-ttu-id="616d1-257">tootest, çoklu oturum açma ayarları, açık hello adresinden erişim Paneli'nde [https://myapps.microsoft.com](https://myapps.microsoft.com/)hello test hesaba oturum açın ve tıklatın **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="616d1-257">tootest your single sign-on settings, open hello Access Panel at [https://myapps.microsoft.com](https://myapps.microsoft.com/), then sign into hello test account, and click **Salesforce**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="616d1-258">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="616d1-258">Additional resources</span></span>

* [<span data-ttu-id="616d1-259">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="616d1-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="616d1-260">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="616d1-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="616d1-261">Kullanıcı sağlamayı Yapılandır</span><span class="sxs-lookup"><span data-stu-id="616d1-261">Configure User Provisioning</span></span>](active-directory-saas-salesforce-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_203.png

