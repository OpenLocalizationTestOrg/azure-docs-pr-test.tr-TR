---
title: "Öğretici: Azure Active Directory Tümleştirme ile ön | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve ön arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 88270b6d-2571-434a-b139-b6ccc3a2b19f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: 4be363a3d338ec9268f3324daab4a80346ec3131
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-front"></a><span data-ttu-id="cc60e-103">Öğretici: Azure Active Directory Tümleştirme ön ile</span><span class="sxs-lookup"><span data-stu-id="cc60e-103">Tutorial: Azure Active Directory integration with Front</span></span>

<span data-ttu-id="cc60e-104">Bu öğreticide, bilgi nasıl toointegrate ön Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cc60e-104">In this tutorial, you learn how toointegrate Front with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cc60e-105">Ön Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="cc60e-105">Integrating Front with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="cc60e-106">Erişim tooFront sahip Azure AD'de kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cc60e-106">You can control in Azure AD who has access tooFront.</span></span>
- <span data-ttu-id="cc60e-107">Kullanıcıların tooautomatically get açan tooFront (çoklu oturum açma) Azure AD hesaplarına ile etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cc60e-107">You can enable your users tooautomatically get signed-on tooFront (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="cc60e-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="cc60e-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="cc60e-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cc60e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cc60e-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="cc60e-110">Prerequisites</span></span>

<span data-ttu-id="cc60e-111">Ön ile tooconfigure Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="cc60e-111">tooconfigure Azure AD integration with Front, you need hello following items:</span></span>

- <span data-ttu-id="cc60e-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="cc60e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cc60e-113">Bir ön çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="cc60e-113">A Front single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cc60e-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="cc60e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cc60e-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="cc60e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cc60e-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="cc60e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cc60e-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cc60e-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cc60e-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="cc60e-118">Scenario description</span></span>
<span data-ttu-id="cc60e-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="cc60e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cc60e-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="cc60e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cc60e-121">Ön hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="cc60e-121">Adding Front from hello gallery</span></span>
2. <span data-ttu-id="cc60e-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="cc60e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-front-from-hello-gallery"></a><span data-ttu-id="cc60e-123">Ön hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="cc60e-123">Adding Front from hello gallery</span></span>
<span data-ttu-id="cc60e-124">Azure AD'ye tooconfigure hello tümleştirme ön, tooadd ön hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="cc60e-124">tooconfigure hello integration of Front into Azure AD, you need tooadd Front from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="cc60e-125">**tooadd ön hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="cc60e-125">**tooadd Front from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="cc60e-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="cc60e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory düğmesi][1]

2. <span data-ttu-id="cc60e-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="cc60e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="cc60e-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="cc60e-129">Then go too**All applications**.</span></span>

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="cc60e-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="cc60e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Merhaba yeni uygulama düğmesi][3]

4. <span data-ttu-id="cc60e-133">Merhaba arama kutusuna yazın **ön**seçin **ön** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="cc60e-133">In hello search box, type **Front**, select **Front** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Ön hello sonuçları listesinde](./media/active-directory-saas-front-tutorial/tutorial_front_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="cc60e-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="cc60e-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="cc60e-136">Bu bölümde, yapılandırmak ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı ön sınayın.</span><span class="sxs-lookup"><span data-stu-id="cc60e-136">In this section, you configure and test Azure AD single sign-on with Front based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cc60e-137">Tek toowork'ın oturum açma hangi hello karşılık gelen önde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="cc60e-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Front is tooa user in Azure AD.</span></span> <span data-ttu-id="cc60e-138">Diğer bir deyişle, bir Azure AD kullanıcısının ve Merhaba öne ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="cc60e-138">In other words, a link relationship between an Azure AD user and hello related user in Front needs toobe established.</span></span>

<span data-ttu-id="cc60e-139">Merhaba değeri Merhaba öne, atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="cc60e-139">In Front, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="cc60e-140">tooconfigure ve ön ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="cc60e-140">tooconfigure and test Azure AD single sign-on with Front, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="cc60e-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="cc60e-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="cc60e-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="cc60e-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cc60e-143">**[Ön test kullanıcısı oluşturma](#create-a-front-test-user)**  -kullanıcı bağlantılı toohello Azure AD gösterimidir önde bir karşılık gelen Britta Simon, toohave.</span><span class="sxs-lookup"><span data-stu-id="cc60e-143">**[Create a Front test user](#create-a-front-test-user)** - toohave a counterpart of Britta Simon in Front that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="cc60e-144">**[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="cc60e-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cc60e-145">**[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="cc60e-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="cc60e-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="cc60e-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="cc60e-147">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma ön uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="cc60e-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Front application.</span></span>

<span data-ttu-id="cc60e-148">**Azure AD çoklu oturum açma tooconfigure ön ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="cc60e-148">**tooconfigure Azure AD single sign-on with Front, perform hello following steps:**</span></span>

1. <span data-ttu-id="cc60e-149">Hello hello üzerinde Azure portal'ın **ön** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="cc60e-149">In hello Azure portal, on hello **Front** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. <span data-ttu-id="cc60e-151">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="cc60e-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-front-tutorial/tutorial_front_samlbase.png)

3. <span data-ttu-id="cc60e-153">Merhaba üzerinde **ön etki alanı ve URL'leri** tooconfigure hello uygulamada isterseniz, bölümü **IDP** modunda başlatılan:</span><span class="sxs-lookup"><span data-stu-id="cc60e-153">On hello **Front Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-front-tutorial/tutorial_front_url1.png)

    <span data-ttu-id="cc60e-155">a.</span><span class="sxs-lookup"><span data-stu-id="cc60e-155">a.</span></span> <span data-ttu-id="cc60e-156">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.frontapp.com`</span><span class="sxs-lookup"><span data-stu-id="cc60e-156">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.frontapp.com`</span></span>

    <span data-ttu-id="cc60e-157">b.</span><span class="sxs-lookup"><span data-stu-id="cc60e-157">b.</span></span> <span data-ttu-id="cc60e-158">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.frontapp.com/sso/saml/callback`</span><span class="sxs-lookup"><span data-stu-id="cc60e-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.frontapp.com/sso/saml/callback`</span></span>

4. <span data-ttu-id="cc60e-159">Denetleme **Göster Gelişmiş URL ayarları**, tooconfigure hello uygulamada istiyorsanız **SP** modunda başlatılan:</span><span class="sxs-lookup"><span data-stu-id="cc60e-159">Check **Show advanced URL settings**, If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-front-tutorial/tutorial_front_url2.png)

    <span data-ttu-id="cc60e-161">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.frontapp.com`</span><span class="sxs-lookup"><span data-stu-id="cc60e-161">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.frontapp.com`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="cc60e-162">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="cc60e-162">These values are not real.</span></span> <span data-ttu-id="cc60e-163">Bu değerleri ile Merhaba gerçek tanımlayıcı, yanıt URL'si ve oturum açma URL'si daha sonra öğreticide veya kişi açıklanacak güncelleştirme [ön istemci destek ekibi](mailto:support@frontapp.com) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="cc60e-163">Update these values with hello actual Identifier, Reply URL, and Sign-On URL which are explained later in tutorial or contact [Front Client support team](mailto:support@frontapp.com) tooget these values.</span></span> 

5. <span data-ttu-id="cc60e-164">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="cc60e-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-front-tutorial/tutorial_front_certificate.png) 

6. <span data-ttu-id="cc60e-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="cc60e-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-front-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="cc60e-168">Merhaba üzerinde **ön yapılandırma** 'yi tıklatın **yapılandırma ön** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="cc60e-168">On hello **Front Configuration** section, click **Configure Front** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="cc60e-169">Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="cc60e-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-front-tutorial/tutorial_front_configure.png) 

8. <span data-ttu-id="cc60e-171">Yönetici olarak oturum açma tooyour ön Kiracı.</span><span class="sxs-lookup"><span data-stu-id="cc60e-171">Sign-on tooyour Front tenant as an administrator.</span></span>

9. <span data-ttu-id="cc60e-172">Çok Git**ayarları (dişli simgesi hello sol kenar hello sonundaki) > Tercihler**.</span><span class="sxs-lookup"><span data-stu-id="cc60e-172">Go too**Settings (cog icon at hello bottom of hello left sidebar) > Preferences**.</span></span>
   
    ![Çoklu oturum açma üzerinde uygulama tarafı yapılandırma](./media/active-directory-saas-front-tutorial/tutorial_front_000.png)

10. <span data-ttu-id="cc60e-174">Tıklatın **çoklu oturum açma** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="cc60e-174">Click **Single Sign On** link.</span></span>
   
    ![Çoklu oturum açma üzerinde uygulama tarafı yapılandırma](./media/active-directory-saas-front-tutorial/tutorial_front_001.png)

11. <span data-ttu-id="cc60e-176">Seçin **SAML** hello aşağı açılan listesinde **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="cc60e-176">Select **SAML** in hello drop-down list of **Single Sign On**.</span></span>
   
    ![Çoklu oturum açma üzerinde uygulama tarafı yapılandırma](./media/active-directory-saas-front-tutorial/tutorial_front_002.png)

12. <span data-ttu-id="cc60e-178">Merhaba, **giriş noktası** textbox put hello değerini **çoklu oturum açma hizmet URL'si** Azure AD Uygulama Yapılandırma Sihirbazı'ndan.</span><span class="sxs-lookup"><span data-stu-id="cc60e-178">In hello **Entry Point** textbox put hello value of **Single Sign-on Service URL** from Azure AD application configuration wizard.</span></span>
    
    ![Çoklu oturum açma üzerinde uygulama tarafı yapılandırma](./media/active-directory-saas-front-tutorial/tutorial_front_003.png)

13. <span data-ttu-id="cc60e-180">İndirilen açmak **Certificate(Base64)** dosyasını Not Defteri'nde, kopyalama hello panonuza bunu içerik ve toohello Yapıştır **imzalama sertifikası** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="cc60e-180">Open your downloaded **Certificate(Base64)** file in notepad, copy hello content of it into your clipboard, and then paste it toohello **Signing certificate** textbox.</span></span>
    
    ![Çoklu oturum açma üzerinde uygulama tarafı yapılandırma](./media/active-directory-saas-front-tutorial/tutorial_front_004.png)

14. <span data-ttu-id="cc60e-182">Merhaba üzerinde **hizmet sağlayıcı ayarları** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="cc60e-182">On hello **Service provider settings** section, perform hello following steps:</span></span>

    ![Çoklu oturum açma üzerinde uygulama tarafı yapılandırma](./media/active-directory-saas-front-tutorial/tutorial_front_005.png)

    <span data-ttu-id="cc60e-184">a.</span><span class="sxs-lookup"><span data-stu-id="cc60e-184">a.</span></span> <span data-ttu-id="cc60e-185">Merhaba değerini kopyalayın **varlık kimliği** ve hello yapıştırma **tanımlayıcısı** metin kutusuna **ön etki alanı ve URL'leri** Azure portalı bölümünde.</span><span class="sxs-lookup"><span data-stu-id="cc60e-185">Copy hello value of **Entity ID** and paste it into hello **Identifier** textbox in **Front Domain and URLs** section in Azure portal.</span></span>

    <span data-ttu-id="cc60e-186">b.</span><span class="sxs-lookup"><span data-stu-id="cc60e-186">b.</span></span> <span data-ttu-id="cc60e-187">Merhaba değerini kopyalayın **ACS URL** ve hello yapıştırma **oturum açma URL'si** metin kutusuna **ön etki alanı ve URL'leri** Azure portalı bölümünde.</span><span class="sxs-lookup"><span data-stu-id="cc60e-187">Copy hello value of **ACS URL** and paste it into hello **Sign-on URL** textbox in **Front Domain and URLs** section in Azure portal.</span></span>
    
15. <span data-ttu-id="cc60e-188">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="cc60e-188">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="cc60e-189">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="cc60e-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="cc60e-190">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="cc60e-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="cc60e-191">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cc60e-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="cc60e-192">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="cc60e-192">Create an Azure AD test user</span></span>

<span data-ttu-id="cc60e-193">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="cc60e-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="cc60e-195">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="cc60e-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="cc60e-196">Merhaba hello sol bölmede Azure portal hello tıklatın **Azure Active Directory** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="cc60e-196">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-front-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="cc60e-198">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="cc60e-198">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-front-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="cc60e-200">tooopen hello **kullanıcı** iletişim kutusu, tıklatın **Ekle** hello hello üstündeki **tüm kullanıcılar** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="cc60e-200">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Merhaba Ekle düğmesi](./media/active-directory-saas-front-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="cc60e-202">Merhaba, **kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="cc60e-202">In hello **User** dialog box, perform hello following steps:</span></span>

    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-front-tutorial/create_aaduser_04.png)

    <span data-ttu-id="cc60e-204">a.</span><span class="sxs-lookup"><span data-stu-id="cc60e-204">a.</span></span> <span data-ttu-id="cc60e-205">Merhaba, **adı** kutusuna **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cc60e-205">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cc60e-206">b.</span><span class="sxs-lookup"><span data-stu-id="cc60e-206">b.</span></span> <span data-ttu-id="cc60e-207">Merhaba, **kullanıcı adı** kutusuna, kullanıcının Britta Simon hello e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="cc60e-207">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="cc60e-208">c.</span><span class="sxs-lookup"><span data-stu-id="cc60e-208">c.</span></span> <span data-ttu-id="cc60e-209">Select hello **Göster parola** onay kutusunu işaretleyin ve ardından hello görüntülenen hello değerini aşağı yazma **parola** kutusu.</span><span class="sxs-lookup"><span data-stu-id="cc60e-209">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="cc60e-210">d.</span><span class="sxs-lookup"><span data-stu-id="cc60e-210">d.</span></span> <span data-ttu-id="cc60e-211">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="cc60e-211">Click **Create**.</span></span>
 
### <a name="create-a-front-test-user"></a><span data-ttu-id="cc60e-212">Ön test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="cc60e-212">Create a Front test user</span></span>

<span data-ttu-id="cc60e-213">Bu bölümde, Britta Simon önde adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cc60e-213">In this section, you create a user called Britta Simon in Front.</span></span> <span data-ttu-id="cc60e-214">Çalışmak [ön istemci destek ekibi](mailto:support@frontapp.com) Merhaba öne platformunda hello kullanıcıları eklemek için.</span><span class="sxs-lookup"><span data-stu-id="cc60e-214">Work with [Front Client support team](mailto:support@frontapp.com) to add hello users in hello Front platform.</span></span> <span data-ttu-id="cc60e-215">Kullanıcıların oluşturulan ve çoklu oturum açma kullanmadan önce etkinleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="cc60e-215">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="cc60e-216">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="cc60e-216">Assign hello Azure AD test user</span></span>

<span data-ttu-id="cc60e-217">Bu bölümde, erişim tooFront vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="cc60e-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooFront.</span></span>

![Merhaba kullanıcı rolü atayın][200] 

<span data-ttu-id="cc60e-219">**tooassign Britta Simon tooFront hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="cc60e-219">**tooassign Britta Simon tooFront, perform hello following steps:**</span></span>

1. <span data-ttu-id="cc60e-220">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="cc60e-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="cc60e-222">Merhaba uygulamalar listesinde **ön**.</span><span class="sxs-lookup"><span data-stu-id="cc60e-222">In hello applications list, select **Front**.</span></span>

    ![Merhaba öne bağlantı hello uygulamalar listesinde](./media/active-directory-saas-front-tutorial/tutorial_front_app.png)  

3. <span data-ttu-id="cc60e-224">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="cc60e-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202]

4. <span data-ttu-id="cc60e-226">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="cc60e-226">Click **Add** button.</span></span> <span data-ttu-id="cc60e-227">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="cc60e-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Merhaba eklemek atama bölmesi][203]

5. <span data-ttu-id="cc60e-229">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="cc60e-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="cc60e-230">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="cc60e-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cc60e-231">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="cc60e-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="cc60e-232">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="cc60e-232">Test single sign-on</span></span>

<span data-ttu-id="cc60e-233">Bu bölümde Hello amacı olan tootest kullanarak Azure AD SSOconfiguration hello erişim paneli.</span><span class="sxs-lookup"><span data-stu-id="cc60e-233">hello objective of this section is tootest your Azure AD SSOconfiguration using hello Access Panel.</span></span>

<span data-ttu-id="cc60e-234">Merhaba öne hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour ön uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="cc60e-234">When you click hello Front tile in hello Access Panel, you should get automatically signed-on tooyour Front application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="cc60e-235">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="cc60e-235">Additional resources</span></span>

* [<span data-ttu-id="cc60e-236">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="cc60e-236">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cc60e-237">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="cc60e-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-front-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-front-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-front-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-front-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-front-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-front-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-front-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-front-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-front-tutorial/tutorial_general_203.png

