---
title: "Öğretici: Azure Active Directory Tümleştirme O.C. ile Etikan - AppreciateHub | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile O.C. arasında Etikan - AppreciateHub."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dee8fbca-0b60-4a21-8917-1fb6919de5a0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: jeedes
ms.openlocfilehash: 45052cf56e35746d7df5910162e40e3bbcad1aca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-oc-tanner---appreciatehub"></a><span data-ttu-id="3dd10-105">Öğretici: Azure Active Directory Tümleştirme O.C. ile</span><span class="sxs-lookup"><span data-stu-id="3dd10-105">Tutorial: Azure Active Directory integration with O.C.</span></span> <span data-ttu-id="3dd10-106">Etikan - AppreciateHub</span><span class="sxs-lookup"><span data-stu-id="3dd10-106">Tanner - AppreciateHub</span></span>

<span data-ttu-id="3dd10-107">Bu öğreticide, bilgi nasıl toointegrate O.C.</span><span class="sxs-lookup"><span data-stu-id="3dd10-107">In this tutorial, you learn how toointegrate O.C.</span></span> <span data-ttu-id="3dd10-108">Etikan - AppreciateHub Azure ile Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3dd10-108">Tanner - AppreciateHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3dd10-109">O.C. tümleştirme</span><span class="sxs-lookup"><span data-stu-id="3dd10-109">Integrating O.C.</span></span> <span data-ttu-id="3dd10-110">Etikan - Azure AD ile AppreciateHub ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="3dd10-110">Tanner - AppreciateHub with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3dd10-111">Erişim tooO.C sahip Azure AD'de kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3dd10-111">You can control in Azure AD who has access tooO.C.</span></span> <span data-ttu-id="3dd10-112">Etikan - AppreciateHub</span><span class="sxs-lookup"><span data-stu-id="3dd10-112">Tanner - AppreciateHub</span></span>
- <span data-ttu-id="3dd10-113">Oturum açma, kullanıcıların tooautomatically get tooO.C etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3dd10-113">You can enable your users tooautomatically get signed-on tooO.C.</span></span> <span data-ttu-id="3dd10-114">Etikan - Azure AD hesaplarına sahip AppreciateHub (çoklu oturum açma)</span><span class="sxs-lookup"><span data-stu-id="3dd10-114">Tanner - AppreciateHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3dd10-115">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="3dd10-115">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="3dd10-116">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3dd10-116">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3dd10-117">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="3dd10-117">Prerequisites</span></span>

<span data-ttu-id="3dd10-118">tooconfigure O.C. ile Azure AD tümleştirme</span><span class="sxs-lookup"><span data-stu-id="3dd10-118">tooconfigure Azure AD integration with O.C.</span></span> <span data-ttu-id="3dd10-119">Etikan - AppreciateHub, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="3dd10-119">Tanner - AppreciateHub, you need hello following items:</span></span>

- <span data-ttu-id="3dd10-120">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="3dd10-120">An Azure AD subscription</span></span>
- <span data-ttu-id="3dd10-121">BİR O.C.</span><span class="sxs-lookup"><span data-stu-id="3dd10-121">A O.C.</span></span> <span data-ttu-id="3dd10-122">Etikan - abonelik etkin AppreciateHub çoklu oturum açma</span><span class="sxs-lookup"><span data-stu-id="3dd10-122">Tanner - AppreciateHub single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3dd10-123">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="3dd10-123">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3dd10-124">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="3dd10-124">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3dd10-125">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="3dd10-125">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3dd10-126">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3dd10-126">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3dd10-127">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="3dd10-127">Scenario description</span></span>
<span data-ttu-id="3dd10-128">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="3dd10-128">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3dd10-129">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="3dd10-129">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3dd10-130">O.C. ekleme</span><span class="sxs-lookup"><span data-stu-id="3dd10-130">Adding O.C.</span></span> <span data-ttu-id="3dd10-131">Etikan - AppreciateHub hello Galeriden</span><span class="sxs-lookup"><span data-stu-id="3dd10-131">Tanner - AppreciateHub from hello gallery</span></span>
2. <span data-ttu-id="3dd10-132">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="3dd10-132">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-oc-tanner---appreciatehub-from-hello-gallery"></a><span data-ttu-id="3dd10-133">O.C. ekleme</span><span class="sxs-lookup"><span data-stu-id="3dd10-133">Adding O.C.</span></span> <span data-ttu-id="3dd10-134">Etikan - AppreciateHub hello Galeriden</span><span class="sxs-lookup"><span data-stu-id="3dd10-134">Tanner - AppreciateHub from hello gallery</span></span>
<span data-ttu-id="3dd10-135">tooconfigure hello O.C. tümleştirilmesi</span><span class="sxs-lookup"><span data-stu-id="3dd10-135">tooconfigure hello integration of O.C.</span></span> <span data-ttu-id="3dd10-136">Etikan - Azure AD'ye AppreciateHub tooadd O.C. gerekir</span><span class="sxs-lookup"><span data-stu-id="3dd10-136">Tanner - AppreciateHub into Azure AD, you need tooadd O.C.</span></span> <span data-ttu-id="3dd10-137">Etikan - AppreciateHub hello galeri tooyour listesinden yönetilen SaaS uygulamaları.</span><span class="sxs-lookup"><span data-stu-id="3dd10-137">Tanner - AppreciateHub from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3dd10-138">**tooadd O.C. Etikan - AppreciateHub hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="3dd10-138">**tooadd O.C. Tanner - AppreciateHub from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3dd10-139">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="3dd10-139">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3dd10-141">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="3dd10-141">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3dd10-142">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="3dd10-142">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="3dd10-144">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="3dd10-144">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="3dd10-146">Merhaba arama kutusuna yazın **O.C. Etikan - AppreciateHub**.</span><span class="sxs-lookup"><span data-stu-id="3dd10-146">In hello search box, type **O.C. Tanner - AppreciateHub**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_search.png)

5. <span data-ttu-id="3dd10-148">Merhaba Sonuçlar panelinde seçin **O.C. Etikan - AppreciateHub**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="3dd10-148">In hello results panel, select **O.C. Tanner - AppreciateHub**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3dd10-150">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="3dd10-150">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3dd10-151">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma O.C. ile test etme</span><span class="sxs-lookup"><span data-stu-id="3dd10-151">In this section, you configure and test Azure AD single sign-on with O.C.</span></span> <span data-ttu-id="3dd10-152">Etikan - AppreciateHub "Britta Simon" adlı bir test kullanıcı tabanlı.</span><span class="sxs-lookup"><span data-stu-id="3dd10-152">Tanner - AppreciateHub based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3dd10-153">Tek toowork'ın oturum açma Azure AD tooknow O.C. hangi hello karşılık gelen kullanıcı gerekiyor</span><span class="sxs-lookup"><span data-stu-id="3dd10-153">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in O.C.</span></span> <span data-ttu-id="3dd10-154">Etikan - AppreciateHub tooa Azure AD'de kullanıcıdır.</span><span class="sxs-lookup"><span data-stu-id="3dd10-154">Tanner - AppreciateHub is tooa user in Azure AD.</span></span> <span data-ttu-id="3dd10-155">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı O.C. hello arasında bir bağlantı ilişkisi</span><span class="sxs-lookup"><span data-stu-id="3dd10-155">In other words, a link relationship between an Azure AD user and hello related user in O.C.</span></span> <span data-ttu-id="3dd10-156">Etikan - AppreciateHub kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="3dd10-156">Tanner - AppreciateHub needs toobe established.</span></span>

<span data-ttu-id="3dd10-157">İçinde O.C.</span><span class="sxs-lookup"><span data-stu-id="3dd10-157">In O.C.</span></span> <span data-ttu-id="3dd10-158">Etikan - AppreciateHub, Ata hello hello değerini **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="3dd10-158">Tanner - AppreciateHub, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="3dd10-159">tooconfigure ve Azure AD çoklu oturum açma O.C. ile test</span><span class="sxs-lookup"><span data-stu-id="3dd10-159">tooconfigure and test Azure AD single sign-on with O.C.</span></span> <span data-ttu-id="3dd10-160">Etikan - AppreciateHub, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="3dd10-160">Tanner - AppreciateHub, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3dd10-161">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="3dd10-161">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3dd10-162">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="3dd10-162">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3dd10-163">**[Bir O.C. oluşturma Etikan - AppreciateHub test kullanıcısı](#creating-a-oc-tanner---appreciatehub-test-user)**  -toohave Britta Simon O.C. içinde karşılık gelen</span><span class="sxs-lookup"><span data-stu-id="3dd10-163">**[Creating a O.C. Tanner - AppreciateHub test user](#creating-a-oc-tanner---appreciatehub-test-user)** - toohave a counterpart of Britta Simon in O.C.</span></span> <span data-ttu-id="3dd10-164">Etikan - bağlantılı toohello Azure AD kullanıcı gösterimi olan AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="3dd10-164">Tanner - AppreciateHub that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="3dd10-165">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="3dd10-165">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3dd10-166">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="3dd10-166">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3dd10-167">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3dd10-167">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3dd10-168">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirme ve çoklu oturum açma, O.C. yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3dd10-168">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your O.C.</span></span> <span data-ttu-id="3dd10-169">Etikan - AppreciateHub uygulama.</span><span class="sxs-lookup"><span data-stu-id="3dd10-169">Tanner - AppreciateHub application.</span></span>

<span data-ttu-id="3dd10-170">**tooconfigure Azure AD çoklu oturum açma O.C. ile Etikan - AppreciateHub, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="3dd10-170">**tooconfigure Azure AD single sign-on with O.C. Tanner - AppreciateHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="3dd10-171">Merhaba hello üzerinde Azure portal'ın **O.C. Etikan - AppreciateHub** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="3dd10-171">In hello Azure portal, on hello **O.C. Tanner - AppreciateHub** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="3dd10-173">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="3dd10-173">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_samlbase.png)

3. <span data-ttu-id="3dd10-175">Merhaba üzerinde **O.C. Etikan - AppreciateHub etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="3dd10-175">On hello **O.C. Tanner - AppreciateHub Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_url.png)

    <span data-ttu-id="3dd10-177">a.</span><span class="sxs-lookup"><span data-stu-id="3dd10-177">a.</span></span> <span data-ttu-id="3dd10-178">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.appreciatehub.com/fed/sp/authnResponse20`</span><span class="sxs-lookup"><span data-stu-id="3dd10-178">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.appreciatehub.com/fed/sp/authnResponse20`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3dd10-179">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="3dd10-179">This value is not real.</span></span> <span data-ttu-id="3dd10-180">Bu değer hello gerçek yanıt URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="3dd10-180">Update this value with hello actual Reply URL.</span></span> <span data-ttu-id="3dd10-181">Kişi [O.C. Etikan - AppreciateHub destek ekibi](mailto:sso@octanner.com) tooget bu değer.</span><span class="sxs-lookup"><span data-stu-id="3dd10-181">Contact [O.C. Tanner - AppreciateHub support team](mailto:sso@octanner.com) tooget this value.</span></span>

    <span data-ttu-id="3dd10-182">b.</span><span class="sxs-lookup"><span data-stu-id="3dd10-182">b.</span></span> <span data-ttu-id="3dd10-183">Bağlantı aşağıdaki hello kullanarak açık hello meta veri dosyası: [https://fed.appreciatehub.com/fed/sp/metadata](https://fed.appreciatehub.com/fed/sp/metadata).</span><span class="sxs-lookup"><span data-stu-id="3dd10-183">Open hello metadata file using hello following link: [https://fed.appreciatehub.com/fed/sp/metadata](https://fed.appreciatehub.com/fed/sp/metadata).</span></span>
   
    <span data-ttu-id="3dd10-184">c.</span><span class="sxs-lookup"><span data-stu-id="3dd10-184">c.</span></span> <span data-ttu-id="3dd10-185">Merhaba bulun **md:AssertionConsumerService** düğümü.</span><span class="sxs-lookup"><span data-stu-id="3dd10-185">Locate hello **md:AssertionConsumerService** node.</span></span> 
   
    <span data-ttu-id="3dd10-186">d.</span><span class="sxs-lookup"><span data-stu-id="3dd10-186">d.</span></span> <span data-ttu-id="3dd10-187">Merhaba Hello değerini kopyalayın **konumu** özniteliği.</span><span class="sxs-lookup"><span data-stu-id="3dd10-187">Copy hello value of hello **Location** attribute.</span></span> 
   
    ![Uygulama ayarlarını yapılandırın][12]
   
    <span data-ttu-id="3dd10-189">e.</span><span class="sxs-lookup"><span data-stu-id="3dd10-189">e.</span></span> <span data-ttu-id="3dd10-190">Merhaba, **oturum üzerinde URL'si** hello önceki adımda elde hello değerini aşan bir metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="3dd10-190">In hello **Sign On URL** textbox, past hello value you have obtained in hello previous step.</span></span>

4. <span data-ttu-id="3dd10-191">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="3dd10-191">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_certificate.png) 

5. <span data-ttu-id="3dd10-193">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="3dd10-193">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3dd10-195">tooconfigure çoklu oturum açma üzerinde **O.C. Etikan - AppreciateHub** yan, indirilen toosend hello ihtiyacınız **meta veri XML** çok[O.C. Etikan - AppreciateHub destek ekibi](mailto:sso@octanner.com).</span><span class="sxs-lookup"><span data-stu-id="3dd10-195">tooconfigure single sign-on on **O.C. Tanner - AppreciateHub** side, you need toosend hello downloaded **Metadata XML** too[O.C. Tanner - AppreciateHub support team](mailto:sso@octanner.com).</span></span>

> [!TIP]
> <span data-ttu-id="3dd10-196">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="3dd10-196">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="3dd10-197">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="3dd10-197">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3dd10-198">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3dd10-198">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3dd10-199">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="3dd10-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="3dd10-200">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="3dd10-200">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="3dd10-202">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="3dd10-202">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3dd10-203">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="3dd10-203">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3dd10-205">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="3dd10-205">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3dd10-207">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="3dd10-207">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3dd10-209">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="3dd10-209">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3dd10-211">a.</span><span class="sxs-lookup"><span data-stu-id="3dd10-211">a.</span></span> <span data-ttu-id="3dd10-212">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3dd10-212">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3dd10-213">b.</span><span class="sxs-lookup"><span data-stu-id="3dd10-213">b.</span></span> <span data-ttu-id="3dd10-214">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="3dd10-214">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3dd10-215">c.</span><span class="sxs-lookup"><span data-stu-id="3dd10-215">c.</span></span> <span data-ttu-id="3dd10-216">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="3dd10-216">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="3dd10-217">d.</span><span class="sxs-lookup"><span data-stu-id="3dd10-217">d.</span></span> <span data-ttu-id="3dd10-218">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3dd10-218">Click **Create**.</span></span>
 
### <a name="creating-a-oc-tanner---appreciatehub-test-user"></a><span data-ttu-id="3dd10-219">Bir O.C. oluşturma</span><span class="sxs-lookup"><span data-stu-id="3dd10-219">Creating a O.C.</span></span> <span data-ttu-id="3dd10-220">Etikan - AppreciateHub test kullanıcısı</span><span class="sxs-lookup"><span data-stu-id="3dd10-220">Tanner - AppreciateHub test user</span></span>

<span data-ttu-id="3dd10-221">Hello amacı, bu bölümde toocreate içinde O.C. Britta Simon adlı bir kullanıcı değil</span><span class="sxs-lookup"><span data-stu-id="3dd10-221">hello objective of this section is toocreate a user called Britta Simon in O.C.</span></span> <span data-ttu-id="3dd10-222">Etikan - AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="3dd10-222">Tanner - AppreciateHub.</span></span>

<span data-ttu-id="3dd10-223">**toocreate bir kullanıcı Britta Simon O.C. denir. Etikan - AppreciateHub, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="3dd10-223">**toocreate a user called Britta Simon in O.C. Tanner - AppreciateHub, perform hello following steps:**</span></span>

<span data-ttu-id="3dd10-224">Sorun, [O.C. Etikan - AppreciateHub destek ekibi](mailto:sso@octanner.com) toocreate nameID özniteliği hello Azure AD'de aynı değeri Britta Simon hello kullanıcı adı olarak sahip bir kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="3dd10-224">Ask your [O.C. Tanner - AppreciateHub support team](mailto:sso@octanner.com) toocreate a user that has as nameID attribute hello same value as hello user name of Britta Simon in Azure AD.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="3dd10-225">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="3dd10-225">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="3dd10-226">Bu bölümde, erişim tooO.C vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="3dd10-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooO.C.</span></span> <span data-ttu-id="3dd10-227">Etikan - AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="3dd10-227">Tanner - AppreciateHub.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="3dd10-229">**tooassign Britta Simon tooO.C. Etikan - AppreciateHub, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="3dd10-229">**tooassign Britta Simon tooO.C. Tanner - AppreciateHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="3dd10-230">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="3dd10-230">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="3dd10-232">Merhaba uygulamalar listesinde **O.C. Etikan - AppreciateHub**.</span><span class="sxs-lookup"><span data-stu-id="3dd10-232">In hello applications list, select **O.C. Tanner - AppreciateHub**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_app.png) 

3. <span data-ttu-id="3dd10-234">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="3dd10-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="3dd10-236">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="3dd10-236">Click **Add** button.</span></span> <span data-ttu-id="3dd10-237">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="3dd10-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="3dd10-239">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="3dd10-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3dd10-240">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="3dd10-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3dd10-241">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="3dd10-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3dd10-242">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="3dd10-242">Testing single sign-on</span></span>

<span data-ttu-id="3dd10-243">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="3dd10-243">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="3dd10-244">Merhaba O.C. tıkladığınızda</span><span class="sxs-lookup"><span data-stu-id="3dd10-244">When you click hello O.C.</span></span> <span data-ttu-id="3dd10-245">Etikan - AppreciateHub parçasında Merhaba erişim paneli, otomatik olarak oturum açma O.C. tooyour almanız gerekir</span><span class="sxs-lookup"><span data-stu-id="3dd10-245">Tanner - AppreciateHub tile in hello Access Panel, you should get automatically signed-on tooyour O.C.</span></span> <span data-ttu-id="3dd10-246">Etikan - AppreciateHub uygulama.</span><span class="sxs-lookup"><span data-stu-id="3dd10-246">Tanner - AppreciateHub application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3dd10-247">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="3dd10-247">Additional resources</span></span>

* [<span data-ttu-id="3dd10-248">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="3dd10-248">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3dd10-249">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="3dd10-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_04.png

[12]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_octanner_08.png

[100]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_203.png

