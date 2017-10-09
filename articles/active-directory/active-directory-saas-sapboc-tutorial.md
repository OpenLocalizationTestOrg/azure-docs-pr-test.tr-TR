---
title: "Öğretici: SAP Business nesnesi bulut Azure Active Directory Tümleştirme | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve SAP Business nesnesi bulut arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 6c5e44f0-4e52-463f-b879-834d80a55cdf
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jeedes
ms.openlocfilehash: a3e9bd93897271531f91bcbc50cd361e8a20551e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-business-object-cloud"></a><span data-ttu-id="c5044-103">Öğretici: SAP Business nesnesi bulut Azure Active Directory Tümleştirme</span><span class="sxs-lookup"><span data-stu-id="c5044-103">Tutorial: Azure Active Directory integration with SAP Business Object Cloud</span></span>

<span data-ttu-id="c5044-104">Bu öğreticide, nasıl toointegrate SAP öğrenin iş nesnesi bulut Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c5044-104">In this tutorial, you learn how toointegrate SAP Business Object Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c5044-105">SAP Business nesnesi bulut Azure AD ile tümleştirdiğinizde avantajları aşağıdaki hello alın:</span><span class="sxs-lookup"><span data-stu-id="c5044-105">You get hello following benefits when you integrate SAP Business Object Cloud with Azure AD:</span></span>

- <span data-ttu-id="c5044-106">Azure AD'de erişim tooSAP iş nesnesi bulut olanların kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c5044-106">In Azure AD, you can control who has access tooSAP Business Object Cloud.</span></span>
- <span data-ttu-id="c5044-107">Çoklu oturum açma ve bir kullanıcının Azure AD hesabı kullanarak otomatik olarak, kullanıcılar tooSAP iş nesnesi bulut imzalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c5044-107">You can automatically sign in your users tooSAP Business Object Cloud by using single sign-on and a user's Azure AD account.</span></span>
- <span data-ttu-id="c5044-108">Hesaplarınızı tek, merkezi bir konumda, hello Azure portalında yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="c5044-108">You can manage your accounts in one, central location, hello Azure portal.</span></span>

<span data-ttu-id="c5044-109">toolearn yazılım olarak Azure AD ile hizmet (SaaS) uygulama tümleştirmesi hakkında daha fazla bilgi görmek [uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c5044-109">toolearn more about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c5044-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="c5044-110">Prerequisites</span></span>

<span data-ttu-id="c5044-111">SAP Business nesnesi bulut ile Azure AD tümleştirme tooset, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="c5044-111">tooset up Azure AD integration with SAP Business Object Cloud, you need hello following items:</span></span>

- <span data-ttu-id="c5044-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="c5044-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c5044-113">SAP Business nesnesi olan bir buluta, tekli açık oturum</span><span class="sxs-lookup"><span data-stu-id="c5044-113">An SAP Business Object Cloud, with single sign-on turned on</span></span>

> [!NOTE]
> <span data-ttu-id="c5044-114">Bu öğreticide hello adımları test ederseniz, bunları bir üretim ortamında sınamanızı yok öneririz.</span><span class="sxs-lookup"><span data-stu-id="c5044-114">If you test hello steps in this tutorial, we recommend that you don't test them in a production environment.</span></span>

<span data-ttu-id="c5044-115">Bu öğreticide hello adımları test etmek için öneriler:</span><span class="sxs-lookup"><span data-stu-id="c5044-115">Recommendations for testing hello steps in this tutorial:</span></span>

- <span data-ttu-id="c5044-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="c5044-116">Do not use your production environment, unless it's necessary.</span></span>
- <span data-ttu-id="c5044-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık ücretsiz deneme sürümü alma](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c5044-117">If you don't have an Azure AD trial environment, you can [get a one-month free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c5044-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="c5044-118">Scenario description</span></span>
<span data-ttu-id="c5044-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="c5044-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="c5044-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="c5044-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c5044-121">SAP Business nesnesi bulut hello Galerisi'nden ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c5044-121">Add SAP Business Object Cloud from hello gallery.</span></span>
2. <span data-ttu-id="c5044-122">Ayarlama ve Azure AD çoklu oturum açmayı test edin.</span><span class="sxs-lookup"><span data-stu-id="c5044-122">Set up and test Azure AD single sign-on.</span></span>

## <a name="add-sap-business-object-cloud-from-hello-gallery"></a><span data-ttu-id="c5044-123">SAP Business nesnesi bulut hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="c5044-123">Add SAP Business Object Cloud from hello gallery</span></span>
<span data-ttu-id="c5044-124">Itanium tabanlı sistemler için SAP Business nesnesi bulut Azure AD ile Merhaba galerisinde hello tümleştirme tooset SAP Business nesnesi bulut tooyour yönetilen SaaS uygulamaları listesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c5044-124">tooset up hello integration of SAP Business Object Cloud with Azure AD, in hello gallery, add SAP Business Object Cloud tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c5044-125">SAP Business nesnesi bulut hello galerisinden tooadd:</span><span class="sxs-lookup"><span data-stu-id="c5044-125">tooadd SAP Business Object Cloud from hello gallery:</span></span>

1. <span data-ttu-id="c5044-126">Merhaba, [Azure portal](https://portal.azure.com), buna hello soldaki menüden, seçin **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c5044-126">In hello [Azure portal](https://portal.azure.com), in hello left menu, select **Azure Active Directory**.</span></span> 

    ![Hello Azure Active Directory düğmesi][1]

2. <span data-ttu-id="c5044-128">Seçin **kurumsal uygulamalar**ve ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="c5044-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Merhaba kurumsal uygulamalar sayfası][2]
    
3. <span data-ttu-id="c5044-130">tooadd yeni bir uygulama seçin **yeni uygulama**.</span><span class="sxs-lookup"><span data-stu-id="c5044-130">tooadd a new application, select **New application**.</span></span>

    ![Merhaba yeni uygulama düğmesi][3]

4. <span data-ttu-id="c5044-132">Merhaba arama kutusuna **SAP Business nesnesi bulut**.</span><span class="sxs-lookup"><span data-stu-id="c5044-132">In hello search box, enter **SAP Business Object Cloud**.</span></span>

    ![Merhaba arama kutusu](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_search.png)

5. <span data-ttu-id="c5044-134">Merhaba Sonuçlar panelinde seçin **SAP Business nesnesi bulut**ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="c5044-134">In hello results panel, select **SAP Business Object Cloud**, and then select **Add**.</span></span>

    ![SAP Business nesnesi bulut hello sonuçları listesinde](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_addfromgallery.png)

##  <a name="set-up-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="c5044-136">Ayarlama ve Azure AD çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="c5044-136">Set up and test Azure AD single sign-on</span></span>

<span data-ttu-id="c5044-137">Bu bölümde, ayarladığınız ve SAP Business nesnesi bulut ile Azure AD çoklu oturum açmayı test adlı bir test kullanıcı tabanlı *Britta Simon*.</span><span class="sxs-lookup"><span data-stu-id="c5044-137">In this section, you set up and test Azure AD single sign-on with SAP Business Object Cloud based on a test user named *Britta Simon*.</span></span>

<span data-ttu-id="c5044-138">Tek toowork'ın oturum açma tooknow hello Azure AD karşılık gelen kullanıcı SAP Business nesnesi bulutta Azure AD gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="c5044-138">For single sign-on toowork, Azure AD needs tooknow hello Azure AD counterpart user in SAP Business Object Cloud.</span></span> <span data-ttu-id="c5044-139">Bir Azure AD kullanıcısının ve SAP Business nesnesi bulutta hello ilgili kullanıcı arasındaki bağlantıyı ilişkisi kurulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c5044-139">A link relationship between an Azure AD user and hello related user in SAP Business Object Cloud must be established.</span></span>

<span data-ttu-id="c5044-140">tooestablish hello için bulutta SAP iş nesnesi, ilişki bağlantı **kullanıcıadı**, hello hello değerini atayın **kullanıcı adı** Azure AD'de.</span><span class="sxs-lookup"><span data-stu-id="c5044-140">tooestablish hello link relationship, in SAP Business Object Cloud, for **Username**, assign hello value of hello **user name** in Azure AD.</span></span>

<span data-ttu-id="c5044-141">tooconfigure ve Azure AD çoklu oturum açmayı test SAP Business nesnesi bulut, görevleri aşağıdaki tam hello ile:</span><span class="sxs-lookup"><span data-stu-id="c5044-141">tooconfigure and test Azure AD single sign-on with SAP Business Object Cloud, complete hello following tasks:</span></span>

1. <span data-ttu-id="c5044-142">[Azure AD çoklu oturum açmayı ayarlama](#set-up-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="c5044-142">[Set up Azure AD single sign-on](#set-up-azure-ad-single-sign-on).</span></span> <span data-ttu-id="c5044-143">Bu özellik bir kullanıcının toouse ayarlar.</span><span class="sxs-lookup"><span data-stu-id="c5044-143">Sets up a user toouse this feature.</span></span>
2. <span data-ttu-id="c5044-144">[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user).</span><span class="sxs-lookup"><span data-stu-id="c5044-144">[Create an Azure AD test user](#create-an-azure-ad-test-user).</span></span> <span data-ttu-id="c5044-145">Testleri Azure AD çoklu oturum açma Britta Simon hello kullanıcıyla.</span><span class="sxs-lookup"><span data-stu-id="c5044-145">Tests Azure AD single sign-on with hello user Britta Simon.</span></span>
3. <span data-ttu-id="c5044-146">[SAP Business nesnesi bulut test kullanıcısı oluşturma](#create-an-sap-business-object-cloud-test-user).</span><span class="sxs-lookup"><span data-stu-id="c5044-146">[Create an SAP Business Object Cloud test user](#create-an-sap-business-object-cloud-test-user).</span></span> <span data-ttu-id="c5044-147">Karşılık gelen Britta Simon, SAP iş nesnesi, bağlantılı toohello hello kullanıcı Azure AD gösterimi bulutta oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c5044-147">Creates a counterpart of Britta Simon in SAP Business Object Cloud that is linked toohello Azure AD representation of hello user.</span></span>
4. <span data-ttu-id="c5044-148">[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user).</span><span class="sxs-lookup"><span data-stu-id="c5044-148">[Assign hello Azure AD test user](#assign-the-azure-ad-test-user).</span></span> <span data-ttu-id="c5044-149">Azure AD çoklu oturum açma Britta Simon toouse ayarlar.</span><span class="sxs-lookup"><span data-stu-id="c5044-149">Sets up Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c5044-150">[Test çoklu oturum açma](#test-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="c5044-150">[Test single sign-on](#test-single-sign-on).</span></span> <span data-ttu-id="c5044-151">Merhaba yapılandırmayı çalıştığını doğrular.</span><span class="sxs-lookup"><span data-stu-id="c5044-151">Verifies that hello configuration works.</span></span>

### <a name="set-up-azure-ad-single-sign-on"></a><span data-ttu-id="c5044-152">Azure AD çoklu oturum açmayı ayarlayın</span><span class="sxs-lookup"><span data-stu-id="c5044-152">Set up Azure AD single sign-on</span></span>

<span data-ttu-id="c5044-153">Bu bölümde, üzerinde Azure AD çoklu hello Azure portalında oturum açın.</span><span class="sxs-lookup"><span data-stu-id="c5044-153">In this section, you turn on Azure AD single sign-on in hello Azure portal.</span></span> <span data-ttu-id="c5044-154">Sonra tek oturum açma SAP Business nesnesi bulut uygulamanızda ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="c5044-154">Then, you set up single sign-on in your SAP Business Object Cloud application.</span></span>

<span data-ttu-id="c5044-155">Azure AD çoklu oturum açma SAP Business nesnesi bulut ile yukarı tooset:</span><span class="sxs-lookup"><span data-stu-id="c5044-155">tooset up Azure AD single sign-on with SAP Business Object Cloud:</span></span>

1. <span data-ttu-id="c5044-156">Merhaba hello üzerinde Azure portal'ın **SAP Business nesnesi bulut** uygulama tümleştirmesi sayfasında, **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="c5044-156">In hello Azure portal, on hello **SAP Business Object Cloud** application integration page, select **Single sign-on**.</span></span>

    ![Çoklu oturum açma seçin][4]

2. <span data-ttu-id="c5044-158">Merhaba üzerinde **çoklu oturum açma** sayfası için **modu**seçin **SAML tabanlı oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="c5044-158">On hello **Single sign-on** page, for **Mode**, select **SAML-based Sign-on**.</span></span>
 
    ![SAML tabanlı oturum açma seçin](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_samlbase.png)

3. <span data-ttu-id="c5044-160">Altında **SAP Business nesnesi bulut etki alanı ve URL'leri**tam hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="c5044-160">Under **SAP Business Object Cloud Domain and URLs**, complete hello following steps:</span></span>

    1. <span data-ttu-id="c5044-161">Merhaba, **oturum açma URL'si** kutusuna, desen aşağıdaki hello bir URL girin:</span><span class="sxs-lookup"><span data-stu-id="c5044-161">In hello **Sign-on URL** box, enter a URL that has hello following pattern:</span></span> 
    | |
    |-|-|
    | `https://<sub-domain>.sapanalytics.cloud/` |
    | `https://<sub-domain>.sapbusinessobjects.cloud/` |

    2. <span data-ttu-id="c5044-162">Merhaba, **tanımlayıcısı** kutusuna, desen aşağıdaki hello bir URL girin:</span><span class="sxs-lookup"><span data-stu-id="c5044-162">In hello **Identifier** box, enter a URL that has hello following pattern:</span></span>
    | |
    |-|-|
    | `<sub-domain>.sapbusinessobjects.cloud` |
    | `<sub-domain>.sapanalytics.cloud` |

    ![SAP Business nesnesi bulut etki alanı ve URL'leri sayfa URL'leri](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_url.png)
 
    > [!NOTE] 
    > <span data-ttu-id="c5044-164">Merhaba bu URL'leri yalnızca tanıtım değerler.</span><span class="sxs-lookup"><span data-stu-id="c5044-164">hello values in these URLs are for demonstration only.</span></span> <span data-ttu-id="c5044-165">Güncelleştirme hello hello gerçek değerlerle URL ve tanımlayıcıdır URL oturum.</span><span class="sxs-lookup"><span data-stu-id="c5044-165">Update hello values with hello actual sign-on URL and identifier URL.</span></span> <span data-ttu-id="c5044-166">tooget hello oturum açma URL'si kişi hello [SAP Business nesnesi bulut istemci destek ekibi](https://www.sap.com/product/analytics/cloud-analytics.support.html).</span><span class="sxs-lookup"><span data-stu-id="c5044-166">tooget hello sign-on URL, contact hello [SAP Business Object Cloud Client support team](https://www.sap.com/product/analytics/cloud-analytics.support.html).</span></span> <span data-ttu-id="c5044-167">Merhaba yönetici konsolundan hello SAP Business nesnesi bulut meta verileri yükleyerek hello tanımlayıcı URL'sini alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c5044-167">You can get hello identifier URL by downloading hello SAP Business Object Cloud metadata from hello admin console.</span></span> <span data-ttu-id="c5044-168">Bu hello öğreticinin ilerleyen bölümlerinde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="c5044-168">This is explained later in hello tutorial.</span></span> 

4. <span data-ttu-id="c5044-169">Altında **SAML imzalama sertifikası**seçin **meta veri XML**.</span><span class="sxs-lookup"><span data-stu-id="c5044-169">Under **SAML Signing Certificate**, select **Metadata XML**.</span></span> <span data-ttu-id="c5044-170">Daha sonra hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="c5044-170">Then, save hello metadata file on your computer.</span></span>

    ![Meta veri XML seçin](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_certificate.png) 

5. <span data-ttu-id="c5044-172">**Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="c5044-172">Select **Save**.</span></span>

    ![Kaydet'i seçin](./media/active-directory-saas-sapboc-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c5044-174">Farklı web tarayıcısı penceresinde tooyour SAP Business nesnesi bulut şirket sitede yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="c5044-174">In a different web browser window, sign in tooyour SAP Business Object Cloud company site as an administrator.</span></span>

7. <span data-ttu-id="c5044-175">Seçin **menü** > **sistem** > **Yönetim**.</span><span class="sxs-lookup"><span data-stu-id="c5044-175">Select **Menu** > **System** > **Administration**.</span></span>
    
    ![Menüsünü, sonra sistem ve yönetim seçin](./media/active-directory-saas-sapboc-tutorial/config1.png)

8. <span data-ttu-id="c5044-177">Merhaba üzerinde **güvenlik** sekmesi, select hello **Düzenle** (Kalem) simgesi.</span><span class="sxs-lookup"><span data-stu-id="c5044-177">On hello **Security** tab, select hello **Edit** (pen) icon.</span></span>
    
    ![Merhaba Güvenlik sekmesinde hello Düzenle simgesini seçin](./media/active-directory-saas-sapboc-tutorial/config2.png)  

9. <span data-ttu-id="c5044-179">İçin **kimlik doğrulama yöntemini**seçin **SAML çoklu oturum açma (SSO)**.</span><span class="sxs-lookup"><span data-stu-id="c5044-179">For **Authentication Method**, select **SAML Single Sign-On (SSO)**.</span></span>

    ![SAML çoklu oturum açma için hello kimlik doğrulama yöntemini seçin](./media/active-directory-saas-sapboc-tutorial/config3.png)  

10. <span data-ttu-id="c5044-181">toodownload hello hizmet sağlayıcısı meta verileri (1. adım), select **karşıdan**.</span><span class="sxs-lookup"><span data-stu-id="c5044-181">toodownload hello service provider metadata (Step 1), select **Download**.</span></span> <span data-ttu-id="c5044-182">Merhaba meta veri dosyasını bulun ve kopyalama hello **Entityıd** değeri.</span><span class="sxs-lookup"><span data-stu-id="c5044-182">In hello metadata file, find and copy hello **entityID** value.</span></span> <span data-ttu-id="c5044-183">Hello Azure'nın altında portal **SAP Business nesnesi bulut etki alanı ve URL'leri**, hello hello değeri yapıştırın **tanımlayıcısı** kutusu.</span><span class="sxs-lookup"><span data-stu-id="c5044-183">In hello Azure portal, under **SAP Business Object Cloud Domain and URLs**, paste hello value in hello **Identifier** box.</span></span>

    ![Kopyalama ve yapıştırma hello Entityıd değeri](./media/active-directory-saas-sapboc-tutorial/config4.png)  

11. <span data-ttu-id="c5044-185">tooupload hello hizmet sağlayıcısı meta verileri (2. adım) kaynağından indirdiğiniz hello dosyasında hello Azure portal altında **karşıya kimlik sağlayıcısı meta verileri**seçin **karşıya**.</span><span class="sxs-lookup"><span data-stu-id="c5044-185">tooupload hello service provider metadata (Step 2) in hello file that you downloaded from hello Azure portal, under **Upload Identity Provider metadata**, select **Upload**.</span></span>  

    ![Karşıya yükleme karşıya kimlik sağlayıcısı meta verileri altında seçin](./media/active-directory-saas-sapboc-tutorial/config5.png)

12. <span data-ttu-id="c5044-187">Merhaba, **kullanıcı özniteliği** listesinde, uygulamanız için toouse istediğinizi seçin hello kullanıcı özniteliği (adım 3).</span><span class="sxs-lookup"><span data-stu-id="c5044-187">In hello **User Attribute** list, select hello user attribute (Step 3) that you want toouse for your implementation.</span></span> <span data-ttu-id="c5044-188">Bu kullanıcı özniteliği toohello kimlik sağlayıcısı eşler.</span><span class="sxs-lookup"><span data-stu-id="c5044-188">This user attribute maps toohello identity provider.</span></span> <span data-ttu-id="c5044-189">tooenter hello kullanıcının sayfasında, kullanım hello özel bir öznitelik **özel SAML eşleme** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="c5044-189">tooenter a custom attribute on hello user's page, use hello **Custom SAML Mapping** option.</span></span> <span data-ttu-id="c5044-190">Ya da her ikisini seçebilirsiniz **e-posta** veya **kullanıcı kimliği** hello kullanıcı özniteliği olarak.</span><span class="sxs-lookup"><span data-stu-id="c5044-190">Or, you can select either **Email** or **USER ID** as hello user attribute.</span></span> <span data-ttu-id="c5044-191">Bizim örneğimizde, biz seçili **e-posta** biz hello kullanıcı tanımlayıcısı talep hello ile eşlenmiş olduğundan **userprincipalname** hello özniteliğinde **kullanıcı öznitelikleri** hello bölümünde Azure portalı.</span><span class="sxs-lookup"><span data-stu-id="c5044-191">In our example, we selected **Email** because we mapped hello user identifier claim with hello **userprincipalname** attribute in hello **User Attributes** section in hello Azure portal.</span></span> <span data-ttu-id="c5044-192">Bu, toohello SAP Business nesnesi bulut uygulaması her başarılı SAML yanıt olarak gönderilen bir benzersiz kullanıcı e-posta, sağlar.</span><span class="sxs-lookup"><span data-stu-id="c5044-192">This provides a unique user email, which is sent toohello SAP Business Object Cloud application in every successful SAML response.</span></span>

    ![Kullanıcı özniteliğini seçin](./media/active-directory-saas-sapboc-tutorial/config6.png)

13. <span data-ttu-id="c5044-194">Merhaba hello kimlik sağlayıcısı (4. adım), tooverify hello hesabıyla **oturum açma kimlik bilgileri (e-posta)** kutusuna, hello kullanıcının e-posta adresi girin.</span><span class="sxs-lookup"><span data-stu-id="c5044-194">tooverify hello account with hello identity provider (Step 4), in hello **Login Credential (Email)** box, enter hello user's email address.</span></span> <span data-ttu-id="c5044-195">Ardından, seçin **hesabı doğrula**.</span><span class="sxs-lookup"><span data-stu-id="c5044-195">Then, select **Verify Account**.</span></span> <span data-ttu-id="c5044-196">Merhaba sistem oturum açma kimlik bilgileri toohello kullanıcı hesabı ekler.</span><span class="sxs-lookup"><span data-stu-id="c5044-196">hello system adds sign-in credentials toohello user account.</span></span>

    ![E-posta girin ve Doğrula hesabı seçin](./media/active-directory-saas-sapboc-tutorial/config7.png)

14. <span data-ttu-id="c5044-198">Select hello **kaydetmek** simgesi.</span><span class="sxs-lookup"><span data-stu-id="c5044-198">Select hello **Save** icon.</span></span>

    ![Kaydet simgesine](./media/active-directory-saas-sapboc-tutorial/save.png)

> [!TIP]
> <span data-ttu-id="c5044-200">Bu yönergelerde hello kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulamanızı ayarlama yaparken!</span><span class="sxs-lookup"><span data-stu-id="c5044-200">You can read a concise version of these instructions in hello [Azure portal](https://portal.azure.com), while you are setting up your app!</span></span> <span data-ttu-id="c5044-201">Seçerek hello uygulama ekledikten sonra **Active Directory** > **kurumsal uygulamalar**seçin hello **çoklu oturum açma** sekmesi. Merhaba katıştırılmış hello belgelerinde erişebilirsiniz **yapılandırma** kısmına hello sayfanın hello.</span><span class="sxs-lookup"><span data-stu-id="c5044-201">After you add hello app by selecting **Active Directory** > **Enterprise Applications**, select hello **Single Sign-On** tab. You can access hello embedded documentation in hello **Configuration** section, at hello bottom of hello page.</span></span> <span data-ttu-id="c5044-202">Daha fazla bilgi için bkz: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="c5044-202">For more information, see [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="c5044-203">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c5044-203">Create an Azure AD test user</span></span>
<span data-ttu-id="c5044-204">Bu bölümde Britta Simon hello Azure portal adlı bir test kullanıcısı oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="c5044-204">In this section, you create a test user named Britta Simon in hello Azure portal.</span></span>

<span data-ttu-id="c5044-205">toocreate Azure AD'de bir sınama kullanıcısı:</span><span class="sxs-lookup"><span data-stu-id="c5044-205">toocreate a test user in Azure AD:</span></span>

1. <span data-ttu-id="c5044-206">Merhaba hello soldaki menüde Azure portal seçin **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c5044-206">In hello Azure portal, in hello left menu, select **Azure Active Directory**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sapboc-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c5044-208">Kullanıcıların, select toodisplay hello listesini **kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="c5044-208">toodisplay hello list of users, select **Users and groups**, and then select **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sapboc-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c5044-210">tooopen hello **kullanıcı** iletişim kutusunda **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="c5044-210">tooopen hello **User** dialog box, select **Add**.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sapboc-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c5044-212">Merhaba, **kullanıcı** iletişim kutusunda, aşağıdaki adımları tam hello:</span><span class="sxs-lookup"><span data-stu-id="c5044-212">In hello **User** dialog box, complete hello following steps:</span></span>
 
    1. <span data-ttu-id="c5044-213">Merhaba, **adı** kutusuna **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c5044-213">In hello **Name** box, enter **BrittaSimon**.</span></span>

    2. <span data-ttu-id="c5044-214">Merhaba, **kullanıcı adı** kutusuna, hello kullanıcının Britta Simon hello e-posta adresi girin.</span><span class="sxs-lookup"><span data-stu-id="c5044-214">In hello **User name** box, enter hello email address of hello user Britta Simon.</span></span>

    3. <span data-ttu-id="c5044-215">Select hello **Göster parola** onay kutusunu işaretleyin ve ardından hello görüntülenen hello değerini aşağı yazma **parola** kutusu.</span><span class="sxs-lookup"><span data-stu-id="c5044-215">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    4. <span data-ttu-id="c5044-216">**Oluştur**’u seçin.</span><span class="sxs-lookup"><span data-stu-id="c5044-216">Select **Create**.</span></span>

        ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-sapboc-tutorial/create_aaduser_04.png) 

    ![Azure AD Kullanıcı oluşturma][100]

### <a name="create-an-sap-business-object-cloud-test-user"></a><span data-ttu-id="c5044-219">SAP Business nesnesi bulut test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c5044-219">Create an SAP Business Object Cloud test user</span></span>

<span data-ttu-id="c5044-220">TooSAP iş nesnesi bulut oturum önce azure AD kullanıcıları SAP Business nesnesi bulutta sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c5044-220">Azure AD users must be provisioned in SAP Business Object Cloud before they can sign in tooSAP Business Object Cloud.</span></span> <span data-ttu-id="c5044-221">SAP Business nesnesi bulutta sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="c5044-221">In SAP Business Object Cloud, provisioning is a manual task.</span></span>

<span data-ttu-id="c5044-222">tooprovision bir kullanıcı hesabı:</span><span class="sxs-lookup"><span data-stu-id="c5044-222">tooprovision a user account:</span></span>

1. <span data-ttu-id="c5044-223">İçinde tooyour SAP Business nesnesi bulut şirket site yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="c5044-223">Sign in tooyour SAP Business Object Cloud company site as an administrator.</span></span>

2. <span data-ttu-id="c5044-224">Seçin **menü** > **güvenlik** > **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="c5044-224">Select **Menu** > **Security** > **Users**.</span></span>

    ![Çalışanı ekleyin](./media/active-directory-saas-sapboc-tutorial/user1.png)

3. <span data-ttu-id="c5044-226">Merhaba üzerinde **kullanıcılar** seçme sayfası, yeni kullanıcı ayrıntılarını tooadd,  **+** .</span><span class="sxs-lookup"><span data-stu-id="c5044-226">On hello **Users** page, tooadd new user details, select **+**.</span></span> 

    ![Kullanıcılar Sayfası Ekle](./media/active-directory-saas-sapboc-tutorial/user4.png)

    <span data-ttu-id="c5044-228">Ardından, hello aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="c5044-228">Then, complete hello following steps:</span></span>

    1. <span data-ttu-id="c5044-229">Merhaba, **kullanıcı kimliği** kutusuna, gibi hello kullanıcının hello kullanıcı Kimliğini girin **Britta**.</span><span class="sxs-lookup"><span data-stu-id="c5044-229">In hello **USER ID** box, enter hello user ID of hello user, like **Britta**.</span></span>

    2. <span data-ttu-id="c5044-230">Merhaba, **ad** kutusuna, gibi hello ilk hello kullanıcı adını girin **Britta**.</span><span class="sxs-lookup"><span data-stu-id="c5044-230">In hello **FIRST NAME** box, enter hello first name of hello user, like **Britta**.</span></span>

    3. <span data-ttu-id="c5044-231">Merhaba, **SOYADI** kutusuna, gibi hello son hello kullanıcı adını girin **Simon**.</span><span class="sxs-lookup"><span data-stu-id="c5044-231">In hello **LAST NAME** box, enter hello last name of hello user, like **Simon**.</span></span>

    4. <span data-ttu-id="c5044-232">Merhaba, **GÖRÜNEN adı** kutusuna, hello kullanıcının tam adını hello gibi girin **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="c5044-232">In hello **DISPLAY NAME** box, enter hello full name of hello user, like **Britta Simon**.</span></span>

    5. <span data-ttu-id="c5044-233">Merhaba, **e-posta** kutusuna, hello kullanıcının hello e-posta adresi gibi girin  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="c5044-233">In hello **E-MAIL** box, enter hello email address of hello user, like **brittasimon@contoso.com**.</span></span>

    6. <span data-ttu-id="c5044-234">Merhaba üzerinde **Rollerini Seç** sayfasında hello hello kullanıcı için uygun rolü seçin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="c5044-234">On hello **Select Roles** page, select hello appropriate role for hello user, and then select **OK**.</span></span>

      ![Rol seç](./media/active-directory-saas-sapboc-tutorial/user3.png)

    7. <span data-ttu-id="c5044-236">Select hello **kaydetmek** simgesi.</span><span class="sxs-lookup"><span data-stu-id="c5044-236">Select hello **Save** icon.</span></span>  


### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="c5044-237">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="c5044-237">Assign hello Azure AD test user</span></span>

<span data-ttu-id="c5044-238">Bu bölümde, hello kullanıcı Britta Simon toouse Azure AD çoklu oturum açma hello kullanıcı hesabı erişimi tooSAP iş nesnesi bulut vererek sağlar.</span><span class="sxs-lookup"><span data-stu-id="c5044-238">In this section, you allow hello user Britta Simon toouse Azure AD single sign-on by granting hello user account access tooSAP Business Object Cloud.</span></span>

<span data-ttu-id="c5044-239">tooassign Britta Simon tooSAP iş nesnesi bulut:</span><span class="sxs-lookup"><span data-stu-id="c5044-239">tooassign Britta Simon tooSAP Business Object Cloud:</span></span>

1. <span data-ttu-id="c5044-240">Hello Azure portal, hello uygulamaları görünümünü açın ve toohello dizini görünümü gidin.</span><span class="sxs-lookup"><span data-stu-id="c5044-240">In hello Azure portal, open hello applications view, and then go toohello directory view.</span></span> <span data-ttu-id="c5044-241">Seçin **kurumsal uygulamalar**ve ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="c5044-241">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="c5044-243">Merhaba uygulamalar listesinde **SAP Business nesnesi bulut**.</span><span class="sxs-lookup"><span data-stu-id="c5044-243">In hello applications list, select **SAP Business Object Cloud**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_app.png) 

3. <span data-ttu-id="c5044-245">Merhaba soldaki menüde seçin **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="c5044-245">In hello left menu, select **Users and groups**.</span></span>

    ![Kullanıcıları ve grupları seçin][202] 

4. <span data-ttu-id="c5044-247">**Add (Ekle)** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="c5044-247">Select **Add**.</span></span> <span data-ttu-id="c5044-248">Ardından, hello **eklemek atama** sayfasında, **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="c5044-248">Then, on hello **Add Assignment** page, select **Users and groups**.</span></span>

    ![Merhaba atama Ekle sayfası][203]

5. <span data-ttu-id="c5044-250">Merhaba üzerinde **kullanıcılar ve gruplar** sayfasında, kullanıcıların, select hello listesinde **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="c5044-250">On hello **Users and groups** page, in hello list of users, select **Britta Simon**.</span></span>

6. <span data-ttu-id="c5044-251">Merhaba üzerinde **kullanıcılar ve gruplar** sayfasında, **seçin**.</span><span class="sxs-lookup"><span data-stu-id="c5044-251">On hello **Users and groups** page, select **Select**.</span></span>

7. <span data-ttu-id="c5044-252">Merhaba üzerinde **eklemek atama** sayfasında, **atamak**.</span><span class="sxs-lookup"><span data-stu-id="c5044-252">On hello **Add Assignment** page, select **Assign**.</span></span>

![Merhaba kullanıcı rolü atayın][200] 
    
### <a name="test-single-sign-on"></a><span data-ttu-id="c5044-254">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="c5044-254">Test single sign-on</span></span>

<span data-ttu-id="c5044-255">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test.</span><span class="sxs-lookup"><span data-stu-id="c5044-255">In this section, you test your Azure AD single sign-on configuration by using hello access panel.</span></span>

<span data-ttu-id="c5044-256">Merhaba erişim panelinde hello SAP Business nesnesi bulut döşeme seçtiğinizde tooyour SAP Business nesnesi bulut uygulama otomatik olarak imzalanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c5044-256">When you select hello SAP Business Object Cloud tile in hello access panel, you should be automatically signed in tooyour SAP Business Object Cloud application.</span></span>

<span data-ttu-id="c5044-257">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c5044-257">For more information about hello access panel, see [Introduction toohello access panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c5044-258">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="c5044-258">Additional resources</span></span>

* [<span data-ttu-id="c5044-259">İlgili nasıl öğreticiler listesi Azure Active Directory ile toointegrate SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="c5044-259">List of tutorials on how toointegrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c5044-260">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="c5044-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_203.png

