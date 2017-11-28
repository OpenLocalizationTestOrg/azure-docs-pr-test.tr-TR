---
title: "Öğretici: Azure Active Directory Tümleştirme M dosyalarla | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve M dosyalar arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4536fd49-3a65-4cff-9620-860904f726d0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: e1d268da53312b1d2c12e29d66b1a5b66d0cdcce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-m-files"></a><span data-ttu-id="a87a8-103">Öğretici: M-dosyalar Azure Active Directory Tümleştirme</span><span class="sxs-lookup"><span data-stu-id="a87a8-103">Tutorial: Azure Active Directory integration with M-Files</span></span>

<span data-ttu-id="a87a8-104">Bu öğreticide, bilgi nasıl toointegrate M-dosyaları Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a87a8-104">In this tutorial, you learn how toointegrate M-Files with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a87a8-105">M-dosyaları Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="a87a8-105">Integrating M-Files with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a87a8-106">TooM dosyalara erişim olan Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="a87a8-106">You can control in Azure AD who has access tooM-Files</span></span>
- <span data-ttu-id="a87a8-107">Kullanıcıların tooautomatically get açan tooM-dosyalarınızı (çoklu oturum açma) ile Azure AD hesaplarına etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="a87a8-107">You can enable your users tooautomatically get signed-on tooM-Files (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a87a8-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="a87a8-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a87a8-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a87a8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a87a8-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="a87a8-110">Prerequisites</span></span>

<span data-ttu-id="a87a8-111">M-dosyalar ile Azure AD tümleştirme tooconfigure, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="a87a8-111">tooconfigure Azure AD integration with M-Files, you need hello following items:</span></span>

- <span data-ttu-id="a87a8-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="a87a8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a87a8-113">Bir M dosyaları çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="a87a8-113">A M-Files single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a87a8-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="a87a8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a87a8-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="a87a8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a87a8-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="a87a8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a87a8-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a87a8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a87a8-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="a87a8-118">Scenario description</span></span>
<span data-ttu-id="a87a8-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="a87a8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a87a8-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="a87a8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a87a8-121">M-dosyaları hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="a87a8-121">Adding M-Files from hello gallery</span></span>
2. <span data-ttu-id="a87a8-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="a87a8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-m-files-from-hello-gallery"></a><span data-ttu-id="a87a8-123">M-dosyaları hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="a87a8-123">Adding M-Files from hello gallery</span></span>
<span data-ttu-id="a87a8-124">Azure AD'ye tooconfigure hello tümleştirme M dosyaların tooadd M dosyaları hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="a87a8-124">tooconfigure hello integration of M-Files into Azure AD, you need tooadd M-Files from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a87a8-125">**tooadd M dosyaları hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a87a8-125">**tooadd M-Files from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a87a8-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="a87a8-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a87a8-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="a87a8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a87a8-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="a87a8-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="a87a8-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a87a8-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="a87a8-133">Merhaba arama kutusuna yazın **M dosyaları**.</span><span class="sxs-lookup"><span data-stu-id="a87a8-133">In hello search box, type **M-Files**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_search.png)

5. <span data-ttu-id="a87a8-135">Merhaba Sonuçlar panelinde seçin **M dosyaları**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="a87a8-135">In hello results panel, select **M-Files**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a87a8-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="a87a8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a87a8-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı göre M-dosyalar ile test etme.</span><span class="sxs-lookup"><span data-stu-id="a87a8-138">In this section, you configure and test Azure AD single sign-on with M-Files based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a87a8-139">Tek toowork'ın oturum açma hangi hello karşılık gelen M dosyalarında tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="a87a8-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in M-Files is tooa user in Azure AD.</span></span> <span data-ttu-id="a87a8-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve M dosyalarında hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="a87a8-140">In other words, a link relationship between an Azure AD user and hello related user in M-Files needs toobe established.</span></span>

<span data-ttu-id="a87a8-141">M-dosyalarında hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="a87a8-141">In M-Files, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a87a8-142">tooconfigure ve M dosyalarla Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="a87a8-142">tooconfigure and test Azure AD single sign-on with M-Files, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a87a8-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="a87a8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a87a8-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="a87a8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a87a8-145">**[M-dosyaları test kullanıcısı oluşturma](#creating-a-m-files-test-user)**  -toohave karşılık gelen, Britta Simon M dosyalarında kullanıcı bağlantılı toohello Azure AD gösterimidir.</span><span class="sxs-lookup"><span data-stu-id="a87a8-145">**[Creating a M-Files test user](#creating-a-m-files-test-user)** - toohave a counterpart of Britta Simon in M-Files that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a87a8-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="a87a8-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a87a8-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="a87a8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a87a8-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a87a8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a87a8-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma M dosyaları uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="a87a8-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your M-Files application.</span></span>

<span data-ttu-id="a87a8-150">**tooconfigure Azure AD çoklu oturum açma M-dosyalar ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a87a8-150">**tooconfigure Azure AD single sign-on with M-Files, perform hello following steps:**</span></span>

1. <span data-ttu-id="a87a8-151">Merhaba hello üzerinde Azure portal'ın **M dosyaları** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="a87a8-151">In hello Azure portal, on hello **M-Files** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="a87a8-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="a87a8-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_samlbase.png)

3. <span data-ttu-id="a87a8-155">Merhaba üzerinde **M dosyaları etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a87a8-155">On hello **M-Files Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_url.png)

    <span data-ttu-id="a87a8-157">a.</span><span class="sxs-lookup"><span data-stu-id="a87a8-157">a.</span></span> <span data-ttu-id="a87a8-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<tenantname>.cloudvault.m-files.com/authentication/MFiles.AuthenticationProviders.Core/sso`</span><span class="sxs-lookup"><span data-stu-id="a87a8-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenantname>.cloudvault.m-files.com/authentication/MFiles.AuthenticationProviders.Core/sso`</span></span>

    <span data-ttu-id="a87a8-159">b.</span><span class="sxs-lookup"><span data-stu-id="a87a8-159">b.</span></span> <span data-ttu-id="a87a8-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<tenantname>.cloudvault.m-files.com`</span><span class="sxs-lookup"><span data-stu-id="a87a8-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenantname>.cloudvault.m-files.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a87a8-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="a87a8-161">These values are not real.</span></span> <span data-ttu-id="a87a8-162">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="a87a8-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="a87a8-163">Kişi [M dosyaları istemci destek ekibi](mailto:support@m-files.com) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="a87a8-163">Contact [M-Files Client support team](mailto:support@m-files.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="a87a8-164">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="a87a8-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_certificate.png) 

5. <span data-ttu-id="a87a8-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a87a8-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-m-files-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a87a8-168">tooget SSO yapılandırılmış uygulamanızın, kişi [M dosyaları destek ekibi](mailto:support@m-files.com) ve verin hello indirilen meta verileri.</span><span class="sxs-lookup"><span data-stu-id="a87a8-168">tooget SSO configured for your application, contact [M-Files support team](mailto:support@m-files.com) and provide them hello downloaded Metadata.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="a87a8-169">Tooconfigure SSO için M dosya masaüstü uygulaması isterseniz hello sonraki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="a87a8-169">Follow hello next steps if you want tooconfigure SSO for you M-File desktop application.</span></span> <span data-ttu-id="a87a8-170">M-dosyaları web sürümü için yalnızca tooconfigure SSO istiyorsanız, hiçbir ek adımlar gereklidir.</span><span class="sxs-lookup"><span data-stu-id="a87a8-170">No extra steps are required if you only want tooconfigure SSO for M-Files web version.</span></span>  

7. <span data-ttu-id="a87a8-171">Merhaba sonraki adımları tooconfigure hello M dosya masaüstü uygulaması tooenable SSO Azure AD ile izleyin.</span><span class="sxs-lookup"><span data-stu-id="a87a8-171">Follow hello next steps tooconfigure hello M-File desktop application tooenable SSO with Azure AD.</span></span> <span data-ttu-id="a87a8-172">M-dosyaları, toodownload Git çok[M dosyaları karşıdan](https://www.m-files.com/en/download-latest-version) sayfası.</span><span class="sxs-lookup"><span data-stu-id="a87a8-172">toodownload M-Files, go too[M-Files download](https://www.m-files.com/en/download-latest-version) page.</span></span>

8. <span data-ttu-id="a87a8-173">Açık hello **M dosyaları masaüstü ayarlarını** penceresi.</span><span class="sxs-lookup"><span data-stu-id="a87a8-173">Open hello **M-Files Desktop Settings** window.</span></span> <span data-ttu-id="a87a8-174">Ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="a87a8-174">Then, click **Add**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-m-files-tutorial/tutorial_m_files_10.png)

9. <span data-ttu-id="a87a8-176">Merhaba üzerinde **belge kasası bağlantı özelliklerini** penceresinde hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a87a8-176">On hello **Document Vault Connection Properties** window, perform hello following steps:</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-m-files-tutorial/tutorial_m_files_11.png)  

    <span data-ttu-id="a87a8-178">Sunucu bölüm türü Hello altında değerleri aşağıdaki gibi hello:</span><span class="sxs-lookup"><span data-stu-id="a87a8-178">Under hello Server section type, hello values as follows:</span></span>  

    <span data-ttu-id="a87a8-179">a.</span><span class="sxs-lookup"><span data-stu-id="a87a8-179">a.</span></span> <span data-ttu-id="a87a8-180">İçin **adı**, türü `<tenant-name>.cloudvault.m-files.com`.</span><span class="sxs-lookup"><span data-stu-id="a87a8-180">For **Name**, type `<tenant-name>.cloudvault.m-files.com`.</span></span> 
 
    <span data-ttu-id="a87a8-181">b.</span><span class="sxs-lookup"><span data-stu-id="a87a8-181">b.</span></span> <span data-ttu-id="a87a8-182">İçin **bağlantı noktası numarası**, türü **4466**.</span><span class="sxs-lookup"><span data-stu-id="a87a8-182">For **Port Number**, type **4466**.</span></span> 

    <span data-ttu-id="a87a8-183">c.</span><span class="sxs-lookup"><span data-stu-id="a87a8-183">c.</span></span> <span data-ttu-id="a87a8-184">İçin **Protokolü**seçin **HTTPS**.</span><span class="sxs-lookup"><span data-stu-id="a87a8-184">For **Protocol**, select **HTTPS**.</span></span> 

    <span data-ttu-id="a87a8-185">d.</span><span class="sxs-lookup"><span data-stu-id="a87a8-185">d.</span></span> <span data-ttu-id="a87a8-186">Merhaba, **kimlik doğrulaması** alan, select **belirli Windows kullanıcı**.</span><span class="sxs-lookup"><span data-stu-id="a87a8-186">In hello **Authentication** field, select **Specific Windows user**.</span></span> <span data-ttu-id="a87a8-187">Ardından, bir imzalama sayfası istenir.</span><span class="sxs-lookup"><span data-stu-id="a87a8-187">Then, you are prompted with a signing page.</span></span> <span data-ttu-id="a87a8-188">Azure AD kimlik bilgilerinizi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a87a8-188">Insert your Azure AD credentials.</span></span> 

    <span data-ttu-id="a87a8-189">e.</span><span class="sxs-lookup"><span data-stu-id="a87a8-189">e.</span></span> <span data-ttu-id="a87a8-190">Hello için **kasası sunucuda**, hello sunucuda karşılık gelen kasayı seçin.</span><span class="sxs-lookup"><span data-stu-id="a87a8-190">For hello **Vault on Server**,  select hello corresponding vault on server.</span></span>
 
    <span data-ttu-id="a87a8-191">f.</span><span class="sxs-lookup"><span data-stu-id="a87a8-191">f.</span></span> <span data-ttu-id="a87a8-192">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a87a8-192">Click **OK**.</span></span>

> [!TIP]
> <span data-ttu-id="a87a8-193">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="a87a8-193">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a87a8-194">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="a87a8-194">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a87a8-195">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a87a8-195">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a87a8-196">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a87a8-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="a87a8-197">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="a87a8-197">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="a87a8-199">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a87a8-199">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a87a8-200">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="a87a8-200">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-m-files-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a87a8-202">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="a87a8-202">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-m-files-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a87a8-204">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="a87a8-204">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-m-files-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a87a8-206">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a87a8-206">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-m-files-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a87a8-208">a.</span><span class="sxs-lookup"><span data-stu-id="a87a8-208">a.</span></span> <span data-ttu-id="a87a8-209">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a87a8-209">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a87a8-210">b.</span><span class="sxs-lookup"><span data-stu-id="a87a8-210">b.</span></span> <span data-ttu-id="a87a8-211">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="a87a8-211">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a87a8-212">c.</span><span class="sxs-lookup"><span data-stu-id="a87a8-212">c.</span></span> <span data-ttu-id="a87a8-213">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="a87a8-213">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a87a8-214">d.</span><span class="sxs-lookup"><span data-stu-id="a87a8-214">d.</span></span> <span data-ttu-id="a87a8-215">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a87a8-215">Click **Create**.</span></span>
 
### <a name="creating-a-m-files-test-user"></a><span data-ttu-id="a87a8-216">M-dosyaları test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a87a8-216">Creating a M-Files test user</span></span>

<span data-ttu-id="a87a8-217">Bu bölümde Hello amacı toocreate M dosyalarında Britta Simon adlı bir kullanıcı var.</span><span class="sxs-lookup"><span data-stu-id="a87a8-217">hello objective of this section is toocreate a user called Britta Simon in M-Files.</span></span> <span data-ttu-id="a87a8-218">Çalışmak [M dosyaları destek ekibi](mailto:support@m-files.com) hello M dosyaları tooadd hello kullanıcılar.</span><span class="sxs-lookup"><span data-stu-id="a87a8-218">Work with  [M-Files support team](mailto:support@m-files.com) tooadd hello users in hello M-Files.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a87a8-219">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="a87a8-219">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a87a8-220">Bu bölümde, tooM dosyalara erişim vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="a87a8-220">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooM-Files.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="a87a8-222">**tooassign Britta Simon tooM-dosyaları, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a87a8-222">**tooassign Britta Simon tooM-Files, perform hello following steps:**</span></span>

1. <span data-ttu-id="a87a8-223">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="a87a8-223">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="a87a8-225">Merhaba uygulamalar listesinde **M dosyaları**.</span><span class="sxs-lookup"><span data-stu-id="a87a8-225">In hello applications list, select **M-Files**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_app.png) 

3. <span data-ttu-id="a87a8-227">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="a87a8-227">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="a87a8-229">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a87a8-229">Click **Add** button.</span></span> <span data-ttu-id="a87a8-230">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="a87a8-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="a87a8-232">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="a87a8-232">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a87a8-233">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="a87a8-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a87a8-234">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="a87a8-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a87a8-235">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="a87a8-235">Testing single sign-on</span></span>

<span data-ttu-id="a87a8-236">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD SSO yapılandırmayı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="a87a8-236">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="a87a8-237">Merhaba tıklattığınızda M dosyaları hello erişim paneli döşeme, otomatik olarak oturum açma M dosyaları tooyour uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a87a8-237">When you click hello M-Files tile in hello Access Panel, you should get automatically signed-on tooyour M-Files application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a87a8-238">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="a87a8-238">Additional resources</span></span>

* [<span data-ttu-id="a87a8-239">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="a87a8-239">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a87a8-240">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="a87a8-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_203.png

