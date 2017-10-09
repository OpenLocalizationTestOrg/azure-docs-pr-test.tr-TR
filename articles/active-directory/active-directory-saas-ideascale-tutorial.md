---
title: "Öğretici: Azure Active Directory Tümleştirme ile IdeaScale | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile IdeaScale arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e16dda6b-fdf9-43cc-9bbb-a523f085a8af
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 10722b137e7565ee165e73994fd5a60b994719bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ideascale"></a><span data-ttu-id="531b7-103">Öğretici: Azure Active Directory Tümleştirme IdeaScale ile</span><span class="sxs-lookup"><span data-stu-id="531b7-103">Tutorial: Azure Active Directory integration with IdeaScale</span></span>

<span data-ttu-id="531b7-104">Bu öğreticide, bilgi nasıl toointegrate IdeaScale Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="531b7-104">In this tutorial, you learn how toointegrate IdeaScale with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="531b7-105">IdeaScale Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="531b7-105">Integrating IdeaScale with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="531b7-106">Erişim tooIdeaScale sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="531b7-106">You can control in Azure AD who has access tooIdeaScale</span></span>
- <span data-ttu-id="531b7-107">Kullanıcıların tooautomatically get açan tooIdeaScale (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="531b7-107">You can enable your users tooautomatically get signed-on tooIdeaScale (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="531b7-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="531b7-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="531b7-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="531b7-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="531b7-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="531b7-110">Prerequisites</span></span>

<span data-ttu-id="531b7-111">tooconfigure IdeaScale ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="531b7-111">tooconfigure Azure AD integration with IdeaScale, you need hello following items:</span></span>

- <span data-ttu-id="531b7-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="531b7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="531b7-113">Bir IdeaScale çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="531b7-113">An IdeaScale single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="531b7-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="531b7-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="531b7-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="531b7-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="531b7-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="531b7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="531b7-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="531b7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="531b7-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="531b7-118">Scenario description</span></span>
<span data-ttu-id="531b7-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="531b7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="531b7-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="531b7-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="531b7-121">Merhaba Galerisi'nden IdeaScale ekleme</span><span class="sxs-lookup"><span data-stu-id="531b7-121">Adding IdeaScale from hello gallery</span></span>
2. <span data-ttu-id="531b7-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="531b7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ideascale-from-hello-gallery"></a><span data-ttu-id="531b7-123">Merhaba Galerisi'nden IdeaScale ekleme</span><span class="sxs-lookup"><span data-stu-id="531b7-123">Adding IdeaScale from hello gallery</span></span>
<span data-ttu-id="531b7-124">Azure AD'ye tooconfigure hello tümleştirme IdeaScale, tooadd IdeaScale hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="531b7-124">tooconfigure hello integration of IdeaScale into Azure AD, you need tooadd IdeaScale from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="531b7-125">**tooadd IdeaScale hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="531b7-125">**tooadd IdeaScale from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="531b7-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="531b7-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="531b7-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="531b7-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="531b7-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="531b7-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="531b7-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="531b7-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="531b7-133">Merhaba arama kutusuna yazın **IdeaScale**.</span><span class="sxs-lookup"><span data-stu-id="531b7-133">In hello search box, type **IdeaScale**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_search.png)

5. <span data-ttu-id="531b7-135">Merhaba Sonuçlar panelinde seçin **IdeaScale**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="531b7-135">In hello results panel, select **IdeaScale**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="531b7-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="531b7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="531b7-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı IdeaScale ile test etme</span><span class="sxs-lookup"><span data-stu-id="531b7-138">In this section, you configure and test Azure AD single sign-on with IdeaScale based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="531b7-139">Tek toowork'ın oturum açma hangi hello karşılık gelen IdeaScale içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="531b7-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in IdeaScale is tooa user in Azure AD.</span></span> <span data-ttu-id="531b7-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı IdeaScale hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="531b7-140">In other words, a link relationship between an Azure AD user and hello related user in IdeaScale needs toobe established.</span></span>

<span data-ttu-id="531b7-141">Merhaba hello değeri IdeaScale içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="531b7-141">In IdeaScale, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="531b7-142">tooconfigure ve IdeaScale ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="531b7-142">tooconfigure and test Azure AD single sign-on with IdeaScale, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="531b7-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="531b7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="531b7-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="531b7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="531b7-145">**[Bir IdeaScale test kullanıcısı oluşturma](#creating-an-ideascale-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir IdeaScale içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="531b7-145">**[Creating an IdeaScale test user](#creating-an-ideascale-test-user)** - toohave a counterpart of Britta Simon in IdeaScale that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="531b7-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="531b7-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="531b7-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="531b7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="531b7-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="531b7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="531b7-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma IdeaScale uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="531b7-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your IdeaScale application.</span></span>

<span data-ttu-id="531b7-150">**tooconfigure Azure AD çoklu oturum açma ile IdeaScale, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="531b7-150">**tooconfigure Azure AD single sign-on with IdeaScale, perform hello following steps:**</span></span>

1. <span data-ttu-id="531b7-151">Hello hello üzerinde Azure portal'ın **IdeaScale** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="531b7-151">In hello Azure portal, on hello **IdeaScale** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="531b7-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="531b7-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_samlbase.png)

3. <span data-ttu-id="531b7-155">Merhaba üzerinde **IdeaScale etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="531b7-155">On hello **IdeaScale Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_url.png)

    <span data-ttu-id="531b7-157">a.</span><span class="sxs-lookup"><span data-stu-id="531b7-157">a.</span></span> <span data-ttu-id="531b7-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.ideascale.com`</span><span class="sxs-lookup"><span data-stu-id="531b7-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.ideascale.com`</span></span>

    <span data-ttu-id="531b7-159">b.</span><span class="sxs-lookup"><span data-stu-id="531b7-159">b.</span></span> <span data-ttu-id="531b7-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:</span><span class="sxs-lookup"><span data-stu-id="531b7-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `http://<companyname>.ideascale.com`  |
    | `https://<companyname>.ideascale.com` |

    > [!NOTE] 
    > <span data-ttu-id="531b7-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="531b7-161">These values are not real.</span></span> <span data-ttu-id="531b7-162">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="531b7-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="531b7-163">Kişi [IdeaScale istemci destek ekibi](http://support.ideascale.com/) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="531b7-163">Contact [IdeaScale Client support team](http://support.ideascale.com/) tooget these values.</span></span> 
 
4. <span data-ttu-id="531b7-164">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="531b7-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_certificate.png) 

5. <span data-ttu-id="531b7-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="531b7-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ideascale-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="531b7-168">Merhaba üzerinde **IdeaScale yapılandırma** 'yi tıklatın **yapılandırma IdeaScale** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="531b7-168">On hello **IdeaScale Configuration** section, click **Configure IdeaScale** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="531b7-169">Kopya hello **Sign-Out URL ve SAML varlık kimliği** hello gelen **hızlı başvuru bölümünde**.</span><span class="sxs-lookup"><span data-stu-id="531b7-169">Copy hello **Sign-Out URL, and SAML Entity ID** from hello **Quick Reference section**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_configure.png) 

7. <span data-ttu-id="531b7-171">Farklı web tarayıcısı penceresinde tooyour IdeaScale şirket sitede yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="531b7-171">In a different web browser window, log in tooyour IdeaScale company site as an administrator.</span></span>

8. <span data-ttu-id="531b7-172">Çok Git**topluluk ayarları**.</span><span class="sxs-lookup"><span data-stu-id="531b7-172">Go too**Community Settings**.</span></span>
   
    <span data-ttu-id="531b7-173">![Topluluk ayarları](./media/active-directory-saas-ideascale-tutorial/ic790847.png "topluluk ayarları")</span><span class="sxs-lookup"><span data-stu-id="531b7-173">![Community Settings](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Community Settings")</span></span>

9. <span data-ttu-id="531b7-174">Çok Git**güvenlik \> çoklu oturum açma ayarları**.</span><span class="sxs-lookup"><span data-stu-id="531b7-174">Go too**Security \> Single Signon Settings**.</span></span>
   
    <span data-ttu-id="531b7-175">![Çoklu oturum açma ayarları](./media/active-directory-saas-ideascale-tutorial/ic790848.png "tek oturum açma ayarları")</span><span class="sxs-lookup"><span data-stu-id="531b7-175">![Single Signon Settings](./media/active-directory-saas-ideascale-tutorial/ic790848.png "Single Signon Settings")</span></span>

10. <span data-ttu-id="531b7-176">Olarak **çoklu oturum açma türü**seçin **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="531b7-176">As **Single-Signon Type**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="531b7-177">![Oturum açma türü tek](./media/active-directory-saas-ideascale-tutorial/ic790849.png "tek oturum açma türü")</span><span class="sxs-lookup"><span data-stu-id="531b7-177">![Single Signon Type](./media/active-directory-saas-ideascale-tutorial/ic790849.png "Single Signon Type")</span></span>

11. <span data-ttu-id="531b7-178">Merhaba üzerinde **çoklu oturum açma ayarları** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="531b7-178">On hello **Single Signon Settings** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="531b7-179">![Çoklu oturum açma ayarları](./media/active-directory-saas-ideascale-tutorial/ic790850.png "tek oturum açma ayarları")</span><span class="sxs-lookup"><span data-stu-id="531b7-179">![Single Signon Settings](./media/active-directory-saas-ideascale-tutorial/ic790850.png "Single Signon Settings")</span></span>
   
    <span data-ttu-id="531b7-180">a.</span><span class="sxs-lookup"><span data-stu-id="531b7-180">a.</span></span> <span data-ttu-id="531b7-181">İçinde **SAML IDP varlık kimliği** metin kutusuna, Yapıştır hello değerini **SAML varlık kimliği** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="531b7-181">In **SAML IdP Entity ID** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="531b7-182">b.</span><span class="sxs-lookup"><span data-stu-id="531b7-182">b.</span></span> <span data-ttu-id="531b7-183">Azure Portalı'ndan indirilen meta veri dosyasının Hello içeriği Kopyala ve hello yapıştırma **SAML IDP meta veri** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="531b7-183">Copy hello content of your downloaded metadata file from Azure portal, and paste it into hello **SAML IdP Metadata** textbox.</span></span>

    <span data-ttu-id="531b7-184">c.</span><span class="sxs-lookup"><span data-stu-id="531b7-184">c.</span></span> <span data-ttu-id="531b7-185">İçinde **oturum kapatma başarı URL** metin kutusuna, Yapıştır hello değerini **Sign-Out URL** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="531b7-185">In **Logout Success URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="531b7-186">d.</span><span class="sxs-lookup"><span data-stu-id="531b7-186">d.</span></span> <span data-ttu-id="531b7-187">Tıklatın **değişiklikleri kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="531b7-187">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="531b7-188">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="531b7-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="531b7-189">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="531b7-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="531b7-190">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="531b7-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="531b7-191">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="531b7-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="531b7-192">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="531b7-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="531b7-194">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="531b7-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="531b7-195">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="531b7-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-ideascale-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="531b7-197">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="531b7-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-ideascale-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="531b7-199">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="531b7-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-ideascale-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="531b7-201">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="531b7-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-ideascale-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="531b7-203">a.</span><span class="sxs-lookup"><span data-stu-id="531b7-203">a.</span></span> <span data-ttu-id="531b7-204">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="531b7-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="531b7-205">b.</span><span class="sxs-lookup"><span data-stu-id="531b7-205">b.</span></span> <span data-ttu-id="531b7-206">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="531b7-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="531b7-207">c.</span><span class="sxs-lookup"><span data-stu-id="531b7-207">c.</span></span> <span data-ttu-id="531b7-208">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="531b7-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="531b7-209">d.</span><span class="sxs-lookup"><span data-stu-id="531b7-209">d.</span></span> <span data-ttu-id="531b7-210">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="531b7-210">Click **Create**.</span></span>
 
### <a name="creating-an-ideascale-test-user"></a><span data-ttu-id="531b7-211">Bir IdeaScale test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="531b7-211">Creating an IdeaScale test user</span></span>

<span data-ttu-id="531b7-212">tooenable Azure AD kullanıcıların toolog IdeaScale bunlar içinde tooIdeaScale sağlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="531b7-212">tooenable Azure AD users toolog into IdeaScale, they must be provisioned in tooIdeaScale.</span></span> <span data-ttu-id="531b7-213">IdeaScale Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="531b7-213">In hello case of IdeaScale, provisioning is a manual task.</span></span>

<span data-ttu-id="531b7-214">**tooconfigure kullanıcı hazırlama, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="531b7-214">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="531b7-215">İçinde tooyour oturum **IdeaScale** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="531b7-215">Log in tooyour **IdeaScale** company site as administrator.</span></span>

2. <span data-ttu-id="531b7-216">Çok Git**topluluk ayarları**.</span><span class="sxs-lookup"><span data-stu-id="531b7-216">Go too**Community Settings**.</span></span>
   
    <span data-ttu-id="531b7-217">![Topluluk ayarları](./media/active-directory-saas-ideascale-tutorial/ic790847.png "topluluk ayarları")</span><span class="sxs-lookup"><span data-stu-id="531b7-217">![Community Settings](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Community Settings")</span></span>

3. <span data-ttu-id="531b7-218">Çok Git**temel ayarları \> üye yönetim**.</span><span class="sxs-lookup"><span data-stu-id="531b7-218">Go too**Basic Settings \> Member Management**.</span></span>

4. <span data-ttu-id="531b7-219">Tıklatın **üye ekleme**.</span><span class="sxs-lookup"><span data-stu-id="531b7-219">Click **Add Member**.</span></span>
   
    <span data-ttu-id="531b7-220">![Üye yönetim](./media/active-directory-saas-ideascale-tutorial/ic790852.png "üye Yönetimi")</span><span class="sxs-lookup"><span data-stu-id="531b7-220">![Member Management](./media/active-directory-saas-ideascale-tutorial/ic790852.png "Member Management")</span></span>

5. <span data-ttu-id="531b7-221">Hello yeni üye ekle bölümü, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="531b7-221">In hello Add New Member section, perform hello following steps:</span></span>
   
    <span data-ttu-id="531b7-222">![Yeni üye eklemek](./media/active-directory-saas-ideascale-tutorial/ic790853.png "yeni üye ekleme")</span><span class="sxs-lookup"><span data-stu-id="531b7-222">![Add New Member](./media/active-directory-saas-ideascale-tutorial/ic790853.png "Add New Member")</span></span>
   
    <span data-ttu-id="531b7-223">a.</span><span class="sxs-lookup"><span data-stu-id="531b7-223">a.</span></span> <span data-ttu-id="531b7-224">Merhaba, **e-posta adresleri** metin kutusuna, tooprovision istediğiniz geçerli bir AAD hesabının hello e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="531b7-224">In hello **Email Addresses** textbox, type hello email address of a valid AAD account you want tooprovision.</span></span>
   
    <span data-ttu-id="531b7-225">b.</span><span class="sxs-lookup"><span data-stu-id="531b7-225">b.</span></span> <span data-ttu-id="531b7-226">Tıklatın **değişiklikleri kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="531b7-226">Click **Save Changes**.</span></span> 
   
    >[!NOTE]
    ><span data-ttu-id="531b7-227">etkin duruma gelmesi hello Azure Active Directory hesap sahibi bağlantı tooconfirm hello hesabı olan bir e-posta alır.</span><span class="sxs-lookup"><span data-stu-id="531b7-227">hello Azure Active Directory account holder gets an email with a link tooconfirm hello account before it becomes active.</span></span>
      
>[!NOTE]
><span data-ttu-id="531b7-228">API AAD kullanıcı hesaplarının IdeaScale tooprovision tarafından sağlanan veya herhangi diğer IdeaScale kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="531b7-228">You can use any other IdeaScale user account creation tools or APIs provided by IdeaScale tooprovision AAD user accounts.</span></span>
 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="531b7-229">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="531b7-229">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="531b7-230">Bu bölümde, erişim tooIdeaScale vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="531b7-230">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooIdeaScale.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="531b7-232">**tooassign Britta Simon tooIdeaScale hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="531b7-232">**tooassign Britta Simon tooIdeaScale, perform hello following steps:**</span></span>

1. <span data-ttu-id="531b7-233">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="531b7-233">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="531b7-235">Merhaba uygulamalar listesinde **IdeaScale**.</span><span class="sxs-lookup"><span data-stu-id="531b7-235">In hello applications list, select **IdeaScale**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_app.png) 

3. <span data-ttu-id="531b7-237">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="531b7-237">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="531b7-239">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="531b7-239">Click **Add** button.</span></span> <span data-ttu-id="531b7-240">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="531b7-240">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="531b7-242">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="531b7-242">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="531b7-243">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="531b7-243">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="531b7-244">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="531b7-244">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="531b7-245">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="531b7-245">Testing single sign-on</span></span>


<span data-ttu-id="531b7-246">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="531b7-246">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="531b7-247">Merhaba IdeaScale hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour IdeaScale uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="531b7-247">When you click hello IdeaScale tile in hello Access Panel, you should get automatically signed-on tooyour IdeaScale application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="531b7-248">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="531b7-248">Additional resources</span></span>

* [<span data-ttu-id="531b7-249">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="531b7-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="531b7-250">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="531b7-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_203.png

