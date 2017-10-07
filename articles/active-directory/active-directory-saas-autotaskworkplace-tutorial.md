---
title: "Öğretici: Azure Active Directory Tümleştirme ile Autotask çalışma | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Autotask çalışma arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: a9a7ff71-c389-4169-aafd-d7a505244797
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 7f820f24e8e9493fa2e1c075f2ef61d7eaa84f73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-autotask-workplace"></a><span data-ttu-id="7e393-103">Öğretici: Azure Active Directory Tümleştirme ile Autotask çalışma</span><span class="sxs-lookup"><span data-stu-id="7e393-103">Tutorial: Azure Active Directory integration with Autotask Workplace</span></span>

<span data-ttu-id="7e393-104">Bu öğreticide, bilgi nasıl toointegrate Autotask çalışma Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7e393-104">In this tutorial, you learn how toointegrate Autotask Workplace with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7e393-105">Autotask çalışma alanına Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="7e393-105">Integrating Autotask Workplace with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7e393-106">Erişim tooAutotask çalışma alanına sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="7e393-106">You can control in Azure AD who has access tooAutotask Workplace</span></span>
- <span data-ttu-id="7e393-107">Kullanıcıların tooautomatically get açan tooAutotask çalışma (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="7e393-107">You can enable your users tooautomatically get signed-on tooAutotask Workplace (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7e393-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="7e393-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7e393-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7e393-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7e393-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="7e393-110">Prerequisites</span></span>

<span data-ttu-id="7e393-111">tooconfigure Autotask çalışma alanı ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="7e393-111">tooconfigure Azure AD integration with Autotask Workplace, you need hello following items:</span></span>

- <span data-ttu-id="7e393-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="7e393-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7e393-113">Bir Autotask çalışma alanı çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="7e393-113">An Autotask Workplace single-sign on enabled subscription</span></span>
- <span data-ttu-id="7e393-114">Bir yönetici ya da çalışma Süper yönetici olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7e393-114">You must be an administrator or super administrator in Workplace.</span></span>
- <span data-ttu-id="7e393-115">Bir yönetici hesabı hello Azure AD olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7e393-115">You must have an administrator account in hello Azure AD.</span></span>
- <span data-ttu-id="7e393-116">Bu özellik yararlanacak olan hello kullanıcıların çalışma alanına ve hello Azure AD içinde hesapların olmalıdır ve e-posta adreslerini her ikisi için aynı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7e393-116">hello users that will utilize this feature must have accounts within Workplace and hello Azure AD, and their email addresses for both must match.</span></span>

> [!NOTE]
> <span data-ttu-id="7e393-117">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="7e393-117">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7e393-118">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="7e393-118">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7e393-119">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="7e393-119">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7e393-120">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7e393-120">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7e393-121">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="7e393-121">Scenario description</span></span>
<span data-ttu-id="7e393-122">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="7e393-122">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7e393-123">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="7e393-123">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7e393-124">Merhaba Galerisi'nden Autotask çalışma alanına ekleme</span><span class="sxs-lookup"><span data-stu-id="7e393-124">Adding Autotask Workplace from hello gallery</span></span>
2. <span data-ttu-id="7e393-125">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="7e393-125">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-autotask-workplace-from-hello-gallery"></a><span data-ttu-id="7e393-126">Merhaba Galerisi'nden Autotask çalışma alanına ekleme</span><span class="sxs-lookup"><span data-stu-id="7e393-126">Adding Autotask Workplace from hello gallery</span></span>
<span data-ttu-id="7e393-127">Azure AD'ye tooconfigure hello tümleştirme Autotask çalışma alanı tooadd Autotask çalışma alanına hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="7e393-127">tooconfigure hello integration of Autotask Workplace into Azure AD, you need tooadd Autotask Workplace from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7e393-128">**tooadd Autotask çalışma hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7e393-128">**tooadd Autotask Workplace from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7e393-129">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="7e393-129">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory düğmesi][1]

2. <span data-ttu-id="7e393-131">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="7e393-131">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7e393-132">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="7e393-132">Then go too**All applications**.</span></span>

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="7e393-134">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7e393-134">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Merhaba yeni uygulama düğmesi][3]

4. <span data-ttu-id="7e393-136">Merhaba arama kutusuna yazın **Autotask çalışma alanına**seçin **Autotask çalışma alanına** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="7e393-136">In hello search box, type **Autotask Workplace**, select  **Autotask Workplace**  from result panel then click **Add** button tooadd hello application.</span></span>

    ![Liste hello Autotask yerinde sonuçları](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="7e393-138">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="7e393-138">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="7e393-139">Bu bölümde, yapılandırmanız ve Autotask çalışma alanı ile Azure AD çoklu oturum açmayı test "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı</span><span class="sxs-lookup"><span data-stu-id="7e393-139">In this section, you configure and test Azure AD single sign-on with Autotask Workplace based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7e393-140">Tek toowork'ın oturum açma hangi hello karşılık gelen Autotask çalışma tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="7e393-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Autotask Workplace is tooa user in Azure AD.</span></span> <span data-ttu-id="7e393-141">Diğer bir deyişle, bir Azure AD kullanıcısının ve Autotask çalışma hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="7e393-141">In other words, a link relationship between an Azure AD user and hello related user in Autotask Workplace needs toobe established.</span></span>

<span data-ttu-id="7e393-142">Merhaba hello değeri Autotask çalışma alanı'ndaki atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="7e393-142">In Autotask Workplace, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7e393-143">tooconfigure ve Autotask çalışma alanı ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="7e393-143">tooconfigure and test Azure AD single sign-on with Autotask Workplace, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7e393-144">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="7e393-144">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7e393-145">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="7e393-145">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7e393-146">**[Autotask çalışma alanına test kullanıcısı oluşturma](#create-an-autotask-workplace-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Autotask çalışma, karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="7e393-146">**[Create an Autotask Workplace test user](#create-an-autotask-workplace-test-user)** - toohave a counterpart of Britta Simon in Autotask Workplace that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7e393-147">**[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="7e393-147">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7e393-148">**[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="7e393-148">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="7e393-149">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="7e393-149">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="7e393-150">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Autotask çalışma alanına uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="7e393-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Autotask Workplace application.</span></span>

<span data-ttu-id="7e393-151">**tooconfigure Azure AD çoklu oturum açma Autotask çalışma ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7e393-151">**tooconfigure Azure AD single sign-on with Autotask Workplace, perform hello following steps:**</span></span>

1. <span data-ttu-id="7e393-152">Merhaba hello üzerinde Azure portal'ın **Autotask çalışma alanına** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="7e393-152">In hello Azure portal, on hello **Autotask Workplace** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. <span data-ttu-id="7e393-154">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="7e393-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_samlbase.png)

3. <span data-ttu-id="7e393-156">Tooconfigure hello uygulamada istiyorsanız **IDP** modunda başlatılan hello hello üzerinde aşağıdaki adımları gerçekleştirin **Autotask çalışma alanına etki alanı ve URL'leri** bölümü:</span><span class="sxs-lookup"><span data-stu-id="7e393-156">If you wish tooconfigure hello application in **IDP** initiated mode, perform hello following steps on hello **Autotask Workplace Domain and URLs** section:</span></span>

    ![Autotask çalışma alanına etki alanı ve URL'leri tek oturum açma bilgilerini IDP](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_url.png)

    <span data-ttu-id="7e393-158">a.</span><span class="sxs-lookup"><span data-stu-id="7e393-158">a.</span></span> <span data-ttu-id="7e393-159">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.awp.autotask.net/singlesignon/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="7e393-159">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.awp.autotask.net/singlesignon/saml/metadata`</span></span>

    <span data-ttu-id="7e393-160">b.</span><span class="sxs-lookup"><span data-stu-id="7e393-160">b.</span></span> <span data-ttu-id="7e393-161">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.awp.autotask.net/singlesignon/saml/SSO`</span><span class="sxs-lookup"><span data-stu-id="7e393-161">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.awp.autotask.net/singlesignon/saml/SSO`</span></span>

4. <span data-ttu-id="7e393-162">Tooconfigure hello uygulamada istiyorsanız **SP** başlatılan modu, onay **Göster Gelişmiş URL ayarları** ve hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="7e393-162">If you wish tooconfigure hello application in **SP** initiated mode, check **Show advanced URL settings** and perform hello following steps:</span></span>

    ![Autotask çalışma alanına etki alanı ve URL'leri tek oturum açma bilgilerini SP](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_url1.png)

    <span data-ttu-id="7e393-164">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.awp.autotask.net/loginsso`</span><span class="sxs-lookup"><span data-stu-id="7e393-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.awp.autotask.net/loginsso`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="7e393-165">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="7e393-165">These values are not real.</span></span> <span data-ttu-id="7e393-166">Bu güncelleştirme tanımlayıcısı, yanıt URL'si ve oturum açma URL'si ile Merhaba gerçek değerler.</span><span class="sxs-lookup"><span data-stu-id="7e393-166">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="7e393-167">Kişi [Autotask çalışma istemci destek ekibi](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="7e393-167">Contact [Autotask Workplace Client support team](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) tooget these values.</span></span> 

5. <span data-ttu-id="7e393-168">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="7e393-168">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_certificate.png) 

6. <span data-ttu-id="7e393-170">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7e393-170">Click **Save** button.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="7e393-172">Farklı web tarayıcısı penceresinde tooWorkplace çevrimiçi kullanarak oturum açın, yönetici kimlik bilgileri hello.</span><span class="sxs-lookup"><span data-stu-id="7e393-172">In a different web browser window, Log in tooWorkplace Online using hello administrator credentials.</span></span>

    >[!Note]
    ><span data-ttu-id="7e393-173">Merhaba IDP yapılandırırken, bir alt etki alanı belirtilen toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="7e393-173">When configuring hello IdP, a subdomain will need toobe specified.</span></span> <span data-ttu-id="7e393-174">tooconfirm hello doğru alt etki alanı, oturum açma tooWorkplace çevrimiçi.</span><span class="sxs-lookup"><span data-stu-id="7e393-174">tooconfirm hello correct subdomain, login tooWorkplace Online.</span></span> <span data-ttu-id="7e393-175">Oturum açtıktan sonra Not toohello alt etki alanı hello URL'de olun.</span><span class="sxs-lookup"><span data-stu-id="7e393-175">Once logged in, make note toohello subdomain in hello URL.</span></span>
    ><span data-ttu-id="7e393-176">Merhaba alt etki alanı arasında hello "https://" ve ".awp.autotask.net/" Merhaba parçasıdır ve bize, AB, ca veya au olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7e393-176">hello subdomain is hello part between hello “https://“ and “.awp.autotask.net/“ and should be us, eu, ca, or au.</span></span>

8. <span data-ttu-id="7e393-177">Çok Git**yapılandırma** > **çoklu oturum açma** ve hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="7e393-177">Go too**Configuration** > **Single Sign-On** and perform hello following steps:</span></span>

    ![Autotask tek oturum açma yapılandırması](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskssoconfig1.png)
 
    <span data-ttu-id="7e393-179">a.</span><span class="sxs-lookup"><span data-stu-id="7e393-179">a.</span></span> <span data-ttu-id="7e393-180">Select hello **XML meta veri dosyası** seçeneğini ve ardından hello karşıya **meta veri XML** Azure portalından indirdiğiniz.</span><span class="sxs-lookup"><span data-stu-id="7e393-180">Select hello **XML Metadata File** option, and then upload hello **Metadata XML** downloaded from Azure portal.</span></span>

    <span data-ttu-id="7e393-181">b.</span><span class="sxs-lookup"><span data-stu-id="7e393-181">b.</span></span> <span data-ttu-id="7e393-182">Tıklatın **etkinleştirmek SSO**.</span><span class="sxs-lookup"><span data-stu-id="7e393-182">Click **Enable SSO**.</span></span>
    
    ![Autotask çoklu oturum açma yapılandırması Onayla](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskssoconfig2.png)

    <span data-ttu-id="7e393-184">c.</span><span class="sxs-lookup"><span data-stu-id="7e393-184">c.</span></span> <span data-ttu-id="7e393-185">Select hello **bu bilgilerin doğru olduğundan ve bu IDP güven onaylayın** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="7e393-185">Select hello **I confirm this information is correct and I trust this IdP** check box.</span></span>

    <span data-ttu-id="7e393-186">d.</span><span class="sxs-lookup"><span data-stu-id="7e393-186">d.</span></span> <span data-ttu-id="7e393-187">Tıklatın **onaylama**.</span><span class="sxs-lookup"><span data-stu-id="7e393-187">Click **Approve**.</span></span>
     
>[!Note]
><span data-ttu-id="7e393-188">Autotask çalışma alanına yapılandırma ile ilgili Yardım gerekiyorsa, lütfen bkz [bu sayfayı](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) iş yeri hesabınızı tooget Yardım.</span><span class="sxs-lookup"><span data-stu-id="7e393-188">If you require assistance with configuring Autotask Workplace, please see [this page](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) tooget assistance with your Workplace account.</span></span>

> [!TIP]
> <span data-ttu-id="7e393-189">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="7e393-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7e393-190">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="7e393-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7e393-191">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7e393-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="7e393-192">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7e393-192">Create an Azure AD test user</span></span>

<span data-ttu-id="7e393-193">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="7e393-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="7e393-195">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7e393-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7e393-196">Merhaba hello sol bölmede Azure portal hello tıklatın **Azure Active Directory** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7e393-196">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="7e393-198">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="7e393-198">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="7e393-200">tooopen hello **kullanıcı** iletişim kutusu, tıklatın **Ekle** hello hello üstündeki **tüm kullanıcılar** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="7e393-200">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Merhaba Ekle düğmesi](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="7e393-202">Merhaba, **kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="7e393-202">In hello **User** dialog box, perform hello following steps:</span></span>

    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_04.png)

    <span data-ttu-id="7e393-204">a.</span><span class="sxs-lookup"><span data-stu-id="7e393-204">a.</span></span> <span data-ttu-id="7e393-205">Merhaba, **adı** kutusuna **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7e393-205">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7e393-206">b.</span><span class="sxs-lookup"><span data-stu-id="7e393-206">b.</span></span> <span data-ttu-id="7e393-207">Merhaba, **kullanıcı adı** kutusuna, kullanıcının Britta Simon hello e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="7e393-207">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="7e393-208">c.</span><span class="sxs-lookup"><span data-stu-id="7e393-208">c.</span></span> <span data-ttu-id="7e393-209">Select hello **Göster parola** onay kutusunu işaretleyin ve ardından hello görüntülenen hello değerini aşağı yazma **parola** kutusu.</span><span class="sxs-lookup"><span data-stu-id="7e393-209">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="7e393-210">d.</span><span class="sxs-lookup"><span data-stu-id="7e393-210">d.</span></span> <span data-ttu-id="7e393-211">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7e393-211">Click **Create**.</span></span>

### <a name="create-an-autotask-workplace-test-user"></a><span data-ttu-id="7e393-212">Autotask çalışma alanına test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7e393-212">Create an Autotask Workplace test user</span></span>

<span data-ttu-id="7e393-213">Bu bölümde, Autotask içinde Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7e393-213">In this section, you create a user called Britta Simon in Autotask.</span></span> <span data-ttu-id="7e393-214">Lütfen çalışmak [Autotask çalışma alanına destek ekibi](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) hello Autotask çalışma alanına platform tooadd hello kullanıcılar.</span><span class="sxs-lookup"><span data-stu-id="7e393-214">Please work with [Autotask Workplace support team](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) tooadd hello users in hello Autotask Workplace platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="7e393-215">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="7e393-215">Assign hello Azure AD test user</span></span>

<span data-ttu-id="7e393-216">Bu bölümde, çalışma alanına erişim tooAutotask vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="7e393-216">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAutotask Workplace.</span></span>

![Merhaba kullanıcı rolü atayın][200] 

<span data-ttu-id="7e393-218">**tooassign Britta Simon tooAutotask çalışma alanı hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7e393-218">**tooassign Britta Simon tooAutotask Workplace, perform hello following steps:**</span></span>

1. <span data-ttu-id="7e393-219">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="7e393-219">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="7e393-221">Merhaba uygulamalar listesinde **Autotask çalışma alanına**.</span><span class="sxs-lookup"><span data-stu-id="7e393-221">In hello applications list, select **Autotask Workplace**.</span></span>

    ![Merhaba hello uygulamalar listesinde Autotask çalışma alanına bağlantısı](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_app.png) 

3. <span data-ttu-id="7e393-223">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="7e393-223">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202]

4. <span data-ttu-id="7e393-225">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7e393-225">Click **Add** button.</span></span> <span data-ttu-id="7e393-226">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="7e393-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Merhaba eklemek atama bölmesi][203]

5. <span data-ttu-id="7e393-228">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="7e393-228">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7e393-229">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="7e393-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7e393-230">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="7e393-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="7e393-231">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="7e393-231">Test single sign-on</span></span>

<span data-ttu-id="7e393-232">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="7e393-232">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="7e393-233">Autotask çalışma alanına döşeme hello erişim paneli hello tıkladığınızda, otomatik olarak oturum açma Autotask çalışma alanına uygulama tooyour almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7e393-233">When you click hello Autotask Workplace tile in hello Access Panel, you should get automatically signed-on tooyour Autotask Workplace application.</span></span>
<span data-ttu-id="7e393-234">Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7e393-234">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7e393-235">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="7e393-235">Additional resources</span></span>

* [<span data-ttu-id="7e393-236">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="7e393-236">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7e393-237">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="7e393-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_203.png

