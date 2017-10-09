---
title: "Öğretici: Azure Active Directory Tümleştirme ile Zscaler özel erişim (ZPA) | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Zscaler özel erişim (ZPA) arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 83711115-1c4f-4dd7-907b-3da24b37c89e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: jeedes
ms.openlocfilehash: 0370cff60c8ac15bd1919acccc924da1e50dc45b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-private-access-zpa"></a><span data-ttu-id="a15e3-103">Öğretici: Azure Active Directory Tümleştirme ile Zscaler özel erişim (ZPA)</span><span class="sxs-lookup"><span data-stu-id="a15e3-103">Tutorial: Azure Active Directory integration with Zscaler Private Access (ZPA)</span></span>

<span data-ttu-id="a15e3-104">Bu öğreticide, bilgi nasıl toointegrate Zscaler özel erişim (ZPA) Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a15e3-104">In this tutorial, you learn how toointegrate Zscaler Private Access (ZPA) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a15e3-105">Zscaler özel erişim (ZPA) Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="a15e3-105">Integrating Zscaler Private Access (ZPA) with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a15e3-106">Erişim tooZscaler özel erişim (ZPA) sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="a15e3-106">You can control in Azure AD who has access tooZscaler Private Access (ZPA)</span></span>
- <span data-ttu-id="a15e3-107">Azure AD hesaplarına ile kullanıcılar tooautomatically get açan tooZscaler özel erişim (ZPA) (çoklu oturum açma) etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="a15e3-107">You can enable your users tooautomatically get signed-on tooZscaler Private Access (ZPA) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a15e3-108">Bir merkezi konumda - hello Azure Yönetim Portalı hesaplarınızı yönetebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="a15e3-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="a15e3-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a15e3-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a15e3-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="a15e3-110">Prerequisites</span></span>

<span data-ttu-id="a15e3-111">Azure AD Tümleştirmesi ile Zscaler özel erişim (ZPA) tooconfigure, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="a15e3-111">tooconfigure Azure AD integration with Zscaler Private Access (ZPA), you need hello following items:</span></span>

- <span data-ttu-id="a15e3-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="a15e3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a15e3-113">Bir Zscaler özel erişim (ZPA) çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="a15e3-113">A Zscaler Private Access (ZPA) single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="a15e3-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="a15e3-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="a15e3-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="a15e3-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a15e3-116">Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a15e3-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="a15e3-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a15e3-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="a15e3-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="a15e3-118">Scenario description</span></span>
<span data-ttu-id="a15e3-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="a15e3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a15e3-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="a15e3-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a15e3-121">Merhaba Galerisi'nden Zscaler özel erişim (ZPA) ekleme</span><span class="sxs-lookup"><span data-stu-id="a15e3-121">Adding Zscaler Private Access (ZPA) from hello gallery</span></span>
2. <span data-ttu-id="a15e3-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="a15e3-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-zscaler-private-access-zpa-from-hello-gallery"></a><span data-ttu-id="a15e3-123">Merhaba Galerisi'nden Zscaler özel erişim (ZPA) ekleme</span><span class="sxs-lookup"><span data-stu-id="a15e3-123">Adding Zscaler Private Access (ZPA) from hello gallery</span></span>
<span data-ttu-id="a15e3-124">Azure AD'ye tooconfigure hello tümleştirmesi, Zscaler özel erişim (ZPA), tooadd Zscaler özel erişim (ZPA) hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="a15e3-124">tooconfigure hello integration of Zscaler Private Access (ZPA) into Azure AD, you need tooadd Zscaler Private Access (ZPA) from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a15e3-125">**tooadd Zscaler özel erişim (ZPA) hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a15e3-125">**tooadd Zscaler Private Access (ZPA) from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a15e3-126">Merhaba,  **[Azure Yönetim Portalı](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="a15e3-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a15e3-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="a15e3-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a15e3-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="a15e3-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="a15e3-131">Tıklatın **Ekle** hello iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a15e3-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="a15e3-133">Merhaba arama kutusuna yazın **Zscaler özel erişim (ZPA)**.</span><span class="sxs-lookup"><span data-stu-id="a15e3-133">In hello search box, type **Zscaler Private Access (ZPA)**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_001.png)

5. <span data-ttu-id="a15e3-135">Merhaba Sonuçlar panelinde seçin **Zscaler özel erişim (ZPA)**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="a15e3-135">In hello results panel, select **Zscaler Private Access (ZPA)**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a15e3-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="a15e3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a15e3-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma ile Zscaler özel erişim ("Britta Simon" adlı bir test kullanıcı tabanlı ZPA) test etme.</span><span class="sxs-lookup"><span data-stu-id="a15e3-138">In this section, you configure and test Azure AD single sign-on with Zscaler Private Access (ZPA) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a15e3-139">Tek toowork'ın oturum açma hangi hello karşılık gelen içinde Zscaler özel erişim (ZPA) tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="a15e3-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zscaler Private Access (ZPA) is tooa user in Azure AD.</span></span> <span data-ttu-id="a15e3-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve hello ilgili kullanıcı içinde Zscaler özel erişim (ZPA) arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="a15e3-140">In other words, a link relationship between an Azure AD user and hello related user in Zscaler Private Access (ZPA) needs toobe established.</span></span>

<span data-ttu-id="a15e3-141">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** içinde Zscaler özel erişim (ZPA).</span><span class="sxs-lookup"><span data-stu-id="a15e3-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Zscaler Private Access (ZPA).</span></span>

<span data-ttu-id="a15e3-142">tooconfigure ve test ile Zscaler özel erişim (ZPA) Azure AD çoklu oturum açma, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="a15e3-142">tooconfigure and test Azure AD single sign-on with Zscaler Private Access (ZPA), you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a15e3-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="a15e3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a15e3-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="a15e3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a15e3-145">**[Zscaler özel erişim (ZPA) test kullanıcısı oluşturma](#creating-a-zscaler-private-access-(zpa)-test-user)**  -toohave Britta Simon içinde Zscaler özel erişim (her bağlantılı toohello Azure AD gösterimi olan ZPA), karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="a15e3-145">**[Creating a Zscaler Private Access (ZPA) test user](#creating-a-zscaler-private-access-(zpa)-test-user)** - toohave a counterpart of Britta Simon in Zscaler Private Access (ZPA) that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="a15e3-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="a15e3-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a15e3-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="a15e3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a15e3-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a15e3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a15e3-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure Yönetim Portalı'nda etkinleştirin ve çoklu oturum açma Zscaler özel erişim (ZPA) uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="a15e3-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Zscaler Private Access (ZPA) application.</span></span>

<span data-ttu-id="a15e3-150">**tooconfigure ile Zscaler özel erişim (ZPA), Azure AD çoklu oturum açma hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a15e3-150">**tooconfigure Azure AD single sign-on with Zscaler Private Access (ZPA), perform hello following steps:**</span></span>

1. <span data-ttu-id="a15e3-151">Merhaba üzerinde hello Azure Yönetim Portalı'nda **Zscaler özel erişim (ZPA)** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="a15e3-151">In hello Azure Management portal, on hello **Zscaler Private Access (ZPA)** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="a15e3-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda, olarak **modu** seçin **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="a15e3-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_300.png)
    
3. <span data-ttu-id="a15e3-155">Merhaba üzerinde **Zscaler özel erişim (ZPA) etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a15e3-155">On hello **Zscaler Private Access (ZPA) Domain and URLs** section, perform hello following steps:</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_01.png)

    <span data-ttu-id="a15e3-157">a.</span><span class="sxs-lookup"><span data-stu-id="a15e3-157">a.</span></span> <span data-ttu-id="a15e3-158">Merhaba, **oturum üzerinde URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://samlsp.private.zscaler.com/auth/login?domain=<your-domain-name>`</span><span class="sxs-lookup"><span data-stu-id="a15e3-158">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://samlsp.private.zscaler.com/auth/login?domain=<your-domain-name>`</span></span>

    <span data-ttu-id="a15e3-159">b.</span><span class="sxs-lookup"><span data-stu-id="a15e3-159">b.</span></span> <span data-ttu-id="a15e3-160">Merhaba, **tanımlayıcısı** metin kutusuna, türü:`https://samlsp.private.zscaler.com/auth/metadata`</span><span class="sxs-lookup"><span data-stu-id="a15e3-160">In hello **Identifier** textbox, type: `https://samlsp.private.zscaler.com/auth/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a15e3-161">Lütfen bu hello gerçek değerler olmadığına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="a15e3-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="a15e3-162">Bu değerlerle hello gerçek oturum açma URL'si ve tanımlayıcı tooupdate sahip.</span><span class="sxs-lookup"><span data-stu-id="a15e3-162">You have tooupdate these values with hello actual Sign On URL and Identifier.</span></span> <span data-ttu-id="a15e3-163">Burada, toouse hello benzersiz değer URL'nin hello tanımlayıcı öneririz.</span><span class="sxs-lookup"><span data-stu-id="a15e3-163">Here we suggest you toouse hello unique value of URL in hello Identifier.</span></span> <span data-ttu-id="a15e3-164">Kişi [Zscaler özel erişim (ZPA) destek ekibi](https://help.zscaler.com/zpa-submit-ticket) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="a15e3-164">Contact [Zscaler Private Access (ZPA) support team](https://help.zscaler.com/zpa-submit-ticket) tooget these values.</span></span>

4. <span data-ttu-id="a15e3-165">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **yeni sertifika oluştur**.</span><span class="sxs-lookup"><span data-stu-id="a15e3-165">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_400.png)   

5. <span data-ttu-id="a15e3-167">Merhaba üzerinde **yeni sertifika oluştur** iletişim kutusunda, hello Takvim simgesine tıklayın ve bir **sona erme tarihi**.</span><span class="sxs-lookup"><span data-stu-id="a15e3-167">On hello **Create New Certificate** dialog, click hello calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="a15e3-168">Ardından **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a15e3-168">Then click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_500.png)

6. <span data-ttu-id="a15e3-170">Merhaba üzerinde **SAML imzalama sertifikası** bölümünde, select **yeni sertifika etkin hale getirin** tıklatıp **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a15e3-170">On hello **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_02.png)

7. <span data-ttu-id="a15e3-172">Merhaba açılır pencere üzerinde **geçiş sertifikası** penceresinde tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="a15e3-172">On hello pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_600.png)

8. <span data-ttu-id="a15e3-174">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="a15e3-174">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_03.png) 

9. <span data-ttu-id="a15e3-176">Farklı web tarayıcısı penceresinde Zscaler özel erişim (ZPA) şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="a15e3-176">In a different web browser window, log into your Zscaler Private Access (ZPA) company site as an administrator.</span></span>

10. <span data-ttu-id="a15e3-177">Çok gidin**yönetici** ve ardından **IDP yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="a15e3-177">Navigate too**Administrator** and then click **Idp Configuration**.</span></span>

    ![Çoklu oturum açma uygulama tarafında yapılandırma](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_04.png)

11. <span data-ttu-id="a15e3-179">Merhaba, **IDP yapılandırma** 'yi tıklatın **yeni IDP Yapılandırması Ekle**.</span><span class="sxs-lookup"><span data-stu-id="a15e3-179">In hello **Idp Configuration** section, click **Add New IDP Configuration**.</span></span>

    ![Çoklu oturum açma uygulama tarafında yapılandırma](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_05.png)

12. <span data-ttu-id="a15e3-181">Merhaba, **yeni IDP yapılandırma** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a15e3-181">In hello **New IDP Configuration** section, perform hello following steps:</span></span>

    ![Çoklu oturum açma uygulama tarafında yapılandırma](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_06.png)

    <span data-ttu-id="a15e3-183">a.</span><span class="sxs-lookup"><span data-stu-id="a15e3-183">a.</span></span> <span data-ttu-id="a15e3-184">Tıklatın **Dosya Seç** ve indirilen meta veri dosyasını karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="a15e3-184">Click **Select File** and upload your downloaded metadata file.</span></span>

    <span data-ttu-id="a15e3-185">b.</span><span class="sxs-lookup"><span data-stu-id="a15e3-185">b.</span></span> <span data-ttu-id="a15e3-186">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a15e3-186">Click **Save** button.</span></span>
    


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a15e3-187">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a15e3-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="a15e3-188">Bu bölümde Hello amacı toocreate Britta Simon adlı hello Azure Yönetim Portalı'nda bir sınama kullanıcısı ' dir.</span><span class="sxs-lookup"><span data-stu-id="a15e3-188">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="a15e3-190">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a15e3-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a15e3-191">Merhaba, **Azure Yönetim Portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="a15e3-191">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a15e3-193">Çok Git**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar** toodisplay hello kullanıcılar listesi.</span><span class="sxs-lookup"><span data-stu-id="a15e3-193">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a15e3-195">Merhaba hello iletişim üstündeki **Ekle** tooopen hello **kullanıcı** iletişim.</span><span class="sxs-lookup"><span data-stu-id="a15e3-195">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a15e3-197">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a15e3-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a15e3-199">a.</span><span class="sxs-lookup"><span data-stu-id="a15e3-199">a.</span></span> <span data-ttu-id="a15e3-200">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a15e3-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a15e3-201">b.</span><span class="sxs-lookup"><span data-stu-id="a15e3-201">b.</span></span> <span data-ttu-id="a15e3-202">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="a15e3-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a15e3-203">c.</span><span class="sxs-lookup"><span data-stu-id="a15e3-203">c.</span></span> <span data-ttu-id="a15e3-204">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="a15e3-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a15e3-205">d.</span><span class="sxs-lookup"><span data-stu-id="a15e3-205">d.</span></span> <span data-ttu-id="a15e3-206">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a15e3-206">Click **Create**.</span></span> 



### <a name="creating-a-zscaler-private-access-zpa-test-user"></a><span data-ttu-id="a15e3-207">Zscaler özel erişim (ZPA) test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a15e3-207">Creating a Zscaler Private Access (ZPA) test user</span></span>

<span data-ttu-id="a15e3-208">Bu bölümde, Britta Simon Zscaler özel erişim (ZPA içinde) adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a15e3-208">In this section, you create a user called Britta Simon in Zscaler Private Access (ZPA).</span></span> <span data-ttu-id="a15e3-209">Lütfen çalışmak [Zscaler özel erişim (ZPA) destek ekibi](https://help.zscaler.com/zpa-submit-ticket) tooadd hello kullanıcılar hello Zscaler özel erişim (ZPA) Platform.</span><span class="sxs-lookup"><span data-stu-id="a15e3-209">Please work with [Zscaler Private Access (ZPA) support team](https://help.zscaler.com/zpa-submit-ticket) tooadd hello users in hello Zscaler Private Access (ZPA) platform.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a15e3-210">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="a15e3-210">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a15e3-211">Bu bölümde, kendi özel erişim (ZPA) erişim tooZscaler vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="a15e3-211">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooZscaler Private Access (ZPA).</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="a15e3-213">**tooassign Britta Simon tooZscaler özel erişim (ZPA), hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a15e3-213">**tooassign Britta Simon tooZscaler Private Access (ZPA), perform hello following steps:**</span></span>

1. <span data-ttu-id="a15e3-214">Hello uygulamaları görünümü, Hello Azure Yönetim Portalı'nda açın ve ardından toohello dizin görünümüne gidin ve çok gidin**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="a15e3-214">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="a15e3-216">Merhaba uygulamalar listesinde **Zscaler özel erişim (ZPA)**.</span><span class="sxs-lookup"><span data-stu-id="a15e3-216">In hello applications list, select **Zscaler Private Access (ZPA)**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_50.png) 

3. <span data-ttu-id="a15e3-218">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="a15e3-218">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="a15e3-220">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a15e3-220">Click **Add** button.</span></span> <span data-ttu-id="a15e3-221">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="a15e3-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="a15e3-223">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="a15e3-223">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a15e3-224">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="a15e3-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a15e3-225">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="a15e3-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="a15e3-226">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="a15e3-226">Testing single sign-on</span></span>

<span data-ttu-id="a15e3-227">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="a15e3-227">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a15e3-228">Merhaba Zscaler özel erişim (ZPA) hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Zscaler özel erişim (ZPA) uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a15e3-228">When you click hello Zscaler Private Access (ZPA) tile in hello Access Panel, you should get automatically signed-on tooyour Zscaler Private Access (ZPA) application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="a15e3-229">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="a15e3-229">Additional resources</span></span>

* [<span data-ttu-id="a15e3-230">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="a15e3-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a15e3-231">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="a15e3-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_203.png