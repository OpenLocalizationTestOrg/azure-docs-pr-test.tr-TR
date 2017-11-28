---
title: "Öğretici: Azure Active Directory Tümleştirme Rally yazılımı ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve Rally yazılımı arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ba25fade-e152-42dd-8377-a30bbc48c3ed
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: jeedes
ms.openlocfilehash: c75c8b98ce7fab19964c13de5ad7e19ef3ebd0e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rally-software"></a><span data-ttu-id="86d96-103">Öğretici: Azure Active Directory Tümleştirme Rally yazılımı</span><span class="sxs-lookup"><span data-stu-id="86d96-103">Tutorial: Azure Active Directory integration with Rally Software</span></span>

<span data-ttu-id="86d96-104">Bu öğreticide, bilgi nasıl toointegrate Rally yazılımı Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="86d96-104">In this tutorial, you learn how toointegrate Rally Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="86d96-105">RALLY yazılımı Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="86d96-105">Integrating Rally Software with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="86d96-106">Erişim tooRally yazılım sahip Azure AD'de kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="86d96-106">You can control in Azure AD who has access tooRally Software.</span></span>
- <span data-ttu-id="86d96-107">Kullanıcıların tooautomatically get açan tooRally yazılım (çoklu oturum açma) Azure AD hesaplarına ile etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="86d96-107">You can enable your users tooautomatically get signed-on tooRally Software (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="86d96-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="86d96-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="86d96-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="86d96-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="86d96-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="86d96-110">Prerequisites</span></span>

<span data-ttu-id="86d96-111">tooconfigure Rally yazılımı ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="86d96-111">tooconfigure Azure AD integration with Rally Software, you need hello following items:</span></span>

- <span data-ttu-id="86d96-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="86d96-112">An Azure AD subscription</span></span>
- <span data-ttu-id="86d96-113">Bir Rally yazılımı çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="86d96-113">A Rally Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="86d96-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="86d96-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="86d96-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="86d96-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="86d96-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="86d96-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="86d96-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="86d96-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="86d96-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="86d96-118">Scenario description</span></span>
<span data-ttu-id="86d96-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="86d96-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="86d96-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="86d96-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="86d96-121">RALLY yazılımı hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="86d96-121">Adding Rally Software from hello gallery</span></span>
2. <span data-ttu-id="86d96-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="86d96-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-rally-software-from-hello-gallery"></a><span data-ttu-id="86d96-123">RALLY yazılımı hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="86d96-123">Adding Rally Software from hello gallery</span></span>
<span data-ttu-id="86d96-124">Azure AD'ye tooconfigure hello tümleştirme Rally yazılımı tooadd Rally yazılımı hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="86d96-124">tooconfigure hello integration of Rally Software into Azure AD, you need tooadd Rally Software from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="86d96-125">**tooadd Rally yazılımı hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="86d96-125">**tooadd Rally Software from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="86d96-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="86d96-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory düğmesi][1]

2. <span data-ttu-id="86d96-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="86d96-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="86d96-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="86d96-129">Then go too**All applications**.</span></span>

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="86d96-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="86d96-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Merhaba yeni uygulama düğmesi][3]

4. <span data-ttu-id="86d96-133">Merhaba arama kutusuna yazın **Rally yazılımı**seçin **Rally yazılımı** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="86d96-133">In hello search box, type **Rally Software**, select **Rally Software** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Merhaba sonuçlar listesinde rally yazılımı](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="86d96-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="86d96-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="86d96-136">Bu bölümde, yapılandırmak ve yazılım Rally "Britta Simon" adlı bir test kullanıcı tabanlı Azure AD çoklu oturum açmayı sınayın.</span><span class="sxs-lookup"><span data-stu-id="86d96-136">In this section, you configure and test Azure AD single sign-on with Rally Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="86d96-137">Tek toowork'ın oturum açma hangi hello karşılık gelen Rally yazılım tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="86d96-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Rally Software is tooa user in Azure AD.</span></span> <span data-ttu-id="86d96-138">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Rally yazılımı hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="86d96-138">In other words, a link relationship between an Azure AD user and hello related user in Rally Software needs toobe established.</span></span>

<span data-ttu-id="86d96-139">RALLY yazılımı hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="86d96-139">In Rally Software, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="86d96-140">tooconfigure ve Rally yazılımı ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="86d96-140">tooconfigure and test Azure AD single sign-on with Rally Software, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="86d96-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="86d96-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="86d96-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="86d96-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="86d96-143">**[Rally yazılımı test kullanıcısı oluşturma](#create-a-rally-software-test-user)**  -toohave Britta Simon Rally kullanıcı bağlantılı toohello Azure AD gösterimidir yazılım, karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="86d96-143">**[Create a Rally Software test user](#create-a-rally-software-test-user)** - toohave a counterpart of Britta Simon in Rally Software that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="86d96-144">**[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="86d96-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="86d96-145">**[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="86d96-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="86d96-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="86d96-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="86d96-147">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Rally yazılımı uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="86d96-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Rally Software application.</span></span>

<span data-ttu-id="86d96-148">**tooconfigure Azure AD çoklu oturum açma Rally yazılımı ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="86d96-148">**tooconfigure Azure AD single sign-on with Rally Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="86d96-149">Hello hello üzerinde Azure portal'ın **Rally yazılımı** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="86d96-149">In hello Azure portal, on hello **Rally Software** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. <span data-ttu-id="86d96-151">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="86d96-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_samlbase.png)

3. <span data-ttu-id="86d96-153">Merhaba üzerinde **Rally yazılımı etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="86d96-153">On hello **Rally Software Domain and URLs** section, perform hello following steps:</span></span>

    ![Rally yazılımı etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_url.png)

    <span data-ttu-id="86d96-155">a.</span><span class="sxs-lookup"><span data-stu-id="86d96-155">a.</span></span> <span data-ttu-id="86d96-156">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<tenant-name>.rally.com`</span><span class="sxs-lookup"><span data-stu-id="86d96-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.rally.com`</span></span>

    <span data-ttu-id="86d96-157">b.</span><span class="sxs-lookup"><span data-stu-id="86d96-157">b.</span></span> <span data-ttu-id="86d96-158">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<tenant-name>.rally.com`</span><span class="sxs-lookup"><span data-stu-id="86d96-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenant-name>.rally.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="86d96-159">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="86d96-159">These values are not real.</span></span> <span data-ttu-id="86d96-160">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="86d96-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="86d96-161">Kişi [Rally yazılımı istemci destek ekibi](https://help.rallydev.com/) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="86d96-161">Contact [Rally Software Client support team](https://help.rallydev.com/) tooget these values.</span></span> 
 


4. <span data-ttu-id="86d96-162">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="86d96-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_certificate.png) 

5. <span data-ttu-id="86d96-164">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="86d96-164">Click **Save** button.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-rally-software-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="86d96-166">Merhaba üzerinde **Rally yazılımı Yapılandırması** 'yi tıklatın **Rally yazılımı Yapılandır** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="86d96-166">On hello **Rally Software Configuration** section, click **Configure Rally Software** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="86d96-167">Kopya hello **Sign-Out URL ve SAML varlık kimliği** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="86d96-167">Copy hello **Sign-Out URL, and SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Rally yazılımı yapılandırması](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_configure.png) 

7. <span data-ttu-id="86d96-169">İçinde tooyour oturum **Rally yazılımı** Kiracı.</span><span class="sxs-lookup"><span data-stu-id="86d96-169">Log in tooyour **Rally Software** tenant.</span></span>

8. <span data-ttu-id="86d96-170">Merhaba üstte Hello araç çubuğunda **Kurulum**ve ardından **abonelik**.</span><span class="sxs-lookup"><span data-stu-id="86d96-170">In hello toolbar on hello top, click **Setup**, and then select **Subscription**.</span></span>
   
    <span data-ttu-id="86d96-171">![Abonelik](./media/active-directory-saas-rally-software-tutorial/ic769531.png "abonelik")</span><span class="sxs-lookup"><span data-stu-id="86d96-171">![Subscription](./media/active-directory-saas-rally-software-tutorial/ic769531.png "Subscription")</span></span>

9. <span data-ttu-id="86d96-172">Merhaba tıklatın **eylem** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="86d96-172">Click hello **Action** button.</span></span> <span data-ttu-id="86d96-173">Seçin **Düzenle abonelik** hello üst sağ tarafında hello araç.</span><span class="sxs-lookup"><span data-stu-id="86d96-173">Select **Edit Subscription** at hello top right side of hello toolbar.</span></span>

10. <span data-ttu-id="86d96-174">Merhaba üzerinde **abonelik** iletişim sayfa hello aşağıdaki adımları gerçekleştirin ve ardından **Kaydet ve Kapat**:</span><span class="sxs-lookup"><span data-stu-id="86d96-174">On hello **Subscription** dialog page, perform hello following steps, and then click **Save & Close**:</span></span>
   
    <span data-ttu-id="86d96-175">![Kimlik doğrulama](./media/active-directory-saas-rally-software-tutorial/ic769542.png "kimlik doğrulaması")</span><span class="sxs-lookup"><span data-stu-id="86d96-175">![Authentication](./media/active-directory-saas-rally-software-tutorial/ic769542.png "Authentication")</span></span>
   
    <span data-ttu-id="86d96-176">a.</span><span class="sxs-lookup"><span data-stu-id="86d96-176">a.</span></span> <span data-ttu-id="86d96-177">Seçin **yarışı veya SSO kimlik doğrulaması** gelen kimlik doğrulama açılır.</span><span class="sxs-lookup"><span data-stu-id="86d96-177">Select **Rally or SSO authentication** from Authentication dropdown.</span></span>

    <span data-ttu-id="86d96-178">b.</span><span class="sxs-lookup"><span data-stu-id="86d96-178">b.</span></span> <span data-ttu-id="86d96-179">Merhaba, **kimlik sağlayıcısı URL'si** metin kutusuna, Yapıştır hello değerini **SAML varlık kimliği**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="86d96-179">In hello **Identity provider URL** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="86d96-180">c.</span><span class="sxs-lookup"><span data-stu-id="86d96-180">c.</span></span> <span data-ttu-id="86d96-181">Merhaba, **SSO oturum kapatma** metin kutusuna, Yapıştır hello değerini **Sign-Out URL**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="86d96-181">In hello **SSO Logout** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

> [!TIP]
> <span data-ttu-id="86d96-182">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="86d96-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="86d96-183">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="86d96-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="86d96-184">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="86d96-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="86d96-185">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="86d96-185">Create an Azure AD test user</span></span>

<span data-ttu-id="86d96-186">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="86d96-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="86d96-188">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="86d96-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="86d96-189">Merhaba hello sol bölmede Azure portal hello tıklatın **Azure Active Directory** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="86d96-189">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-rally-software-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="86d96-191">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="86d96-191">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-rally-software-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="86d96-193">tooopen hello **kullanıcı** iletişim kutusu, tıklatın **Ekle** hello hello üstündeki **tüm kullanıcılar** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="86d96-193">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Merhaba Ekle düğmesi](./media/active-directory-saas-rally-software-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="86d96-195">Merhaba, **kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="86d96-195">In hello **User** dialog box, perform hello following steps:</span></span>

    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-rally-software-tutorial/create_aaduser_04.png)

    <span data-ttu-id="86d96-197">a.</span><span class="sxs-lookup"><span data-stu-id="86d96-197">a.</span></span> <span data-ttu-id="86d96-198">Merhaba, **adı** kutusuna **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="86d96-198">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="86d96-199">b.</span><span class="sxs-lookup"><span data-stu-id="86d96-199">b.</span></span> <span data-ttu-id="86d96-200">Merhaba, **kullanıcı adı** kutusuna, kullanıcının Britta Simon hello e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="86d96-200">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="86d96-201">c.</span><span class="sxs-lookup"><span data-stu-id="86d96-201">c.</span></span> <span data-ttu-id="86d96-202">Select hello **Göster parola** onay kutusunu işaretleyin ve ardından hello görüntülenen hello değerini aşağı yazma **parola** kutusu.</span><span class="sxs-lookup"><span data-stu-id="86d96-202">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="86d96-203">d.</span><span class="sxs-lookup"><span data-stu-id="86d96-203">d.</span></span> <span data-ttu-id="86d96-204">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="86d96-204">Click **Create**.</span></span>
 
### <a name="create-a-rally-software-test-user"></a><span data-ttu-id="86d96-205">Rally yazılımı test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="86d96-205">Create a Rally Software test user</span></span>

<span data-ttu-id="86d96-206">Sağlanan toohello Rally yazılımı uygulama Azure Active Directory kullanıcı adlarını kullanarak Azure AD kullanıcıların toobe mümkün toosign için olmaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="86d96-206">For Azure AD users toobe able toosign in, they must be provisioned toohello Rally Software application using their Azure Active Directory user names.</span></span>

<span data-ttu-id="86d96-207">**tooconfigure kullanıcı hazırlama, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="86d96-207">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="86d96-208">İçinde tooyour Rally yazılımı Kiracı oturum açın.</span><span class="sxs-lookup"><span data-stu-id="86d96-208">Log in tooyour Rally Software tenant.</span></span>

2. <span data-ttu-id="86d96-209">Çok Git**Kurulum \> kullanıcılar**ve ardından **+ yeni Ekle**.</span><span class="sxs-lookup"><span data-stu-id="86d96-209">Go too**Setup \> USERS**, and then click **+ Add New**.</span></span>
   
    <span data-ttu-id="86d96-210">![Kullanıcıların](./media/active-directory-saas-rally-software-tutorial/ic781039.png "kullanıcılar")</span><span class="sxs-lookup"><span data-stu-id="86d96-210">![Users](./media/active-directory-saas-rally-software-tutorial/ic781039.png "Users")</span></span>

3. <span data-ttu-id="86d96-211">Merhaba yeni kullanıcı metin kutusuna hello adını yazın ve ardından **ayrıntılarla Ekle**.</span><span class="sxs-lookup"><span data-stu-id="86d96-211">Type hello name in hello New User textbox, and then click **Add with Details**.</span></span>

4. <span data-ttu-id="86d96-212">Merhaba, **kullanıcı oluştur** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="86d96-212">In hello **Create User** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="86d96-213">![Kullanıcı oluşturma](./media/active-directory-saas-rally-software-tutorial/ic781040.png "kullanıcı oluştur")</span><span class="sxs-lookup"><span data-stu-id="86d96-213">![Create User](./media/active-directory-saas-rally-software-tutorial/ic781040.png "Create User")</span></span>

    <span data-ttu-id="86d96-214">a.</span><span class="sxs-lookup"><span data-stu-id="86d96-214">a.</span></span> <span data-ttu-id="86d96-215">Merhaba, **kullanıcı adı** metin kutusuna, tür hello gibi kullanıcı adını **Brittsimon**.</span><span class="sxs-lookup"><span data-stu-id="86d96-215">In hello **User Name** textbox, type hello name of user like **Brittsimon**.</span></span>
   
    <span data-ttu-id="86d96-216">b.</span><span class="sxs-lookup"><span data-stu-id="86d96-216">b.</span></span> <span data-ttu-id="86d96-217">İçinde **e-posta adresi** metin kutusuna, bir kullanıcı gibi hello e-posta girin  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="86d96-217">In **E-mail Address** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="86d96-218">c.</span><span class="sxs-lookup"><span data-stu-id="86d96-218">c.</span></span> <span data-ttu-id="86d96-219">İçinde **ad** metin kutusuna, hello ilk gibi kullanıcı adını girin **Britta**.</span><span class="sxs-lookup"><span data-stu-id="86d96-219">In **First Name** text box, enter hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="86d96-220">d.</span><span class="sxs-lookup"><span data-stu-id="86d96-220">d.</span></span> <span data-ttu-id="86d96-221">İçinde **Soyadı** metin kutusuna, hello kullanıcının soyadını gibi girin **Simon**.</span><span class="sxs-lookup"><span data-stu-id="86d96-221">In **Last Name** text box, enter hello last name of user like **Simon**.</span></span>

    <span data-ttu-id="86d96-222">e.</span><span class="sxs-lookup"><span data-stu-id="86d96-222">e.</span></span> <span data-ttu-id="86d96-223">Tıklatın **Kaydet ve Kapat**.</span><span class="sxs-lookup"><span data-stu-id="86d96-223">Click **Save & Close**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="86d96-224">API'leri, Azure AD kullanıcı hesapları Rally yazılımı tooprovision tarafından sağlanan veya herhangi diğer Rally yazılımı kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="86d96-224">You can use any other Rally Software user account creation tools or APIs provided by Rally Software tooprovision Azure AD user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="86d96-225">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="86d96-225">Assign hello Azure AD test user</span></span>

<span data-ttu-id="86d96-226">Bu bölümde, erişim tooRally yazılım vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="86d96-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRally Software.</span></span>

![Merhaba kullanıcı rolü atayın][200] 

<span data-ttu-id="86d96-228">**tooassign Britta Simon tooRally yazılım, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="86d96-228">**tooassign Britta Simon tooRally Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="86d96-229">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="86d96-229">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="86d96-231">Merhaba uygulamalar listesinde **Rally yazılımı**.</span><span class="sxs-lookup"><span data-stu-id="86d96-231">In hello applications list, select **Rally Software**.</span></span>

    ![Merhaba Rally yazılımı bağlantı hello uygulamalar listesinde](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_app.png)  

3. <span data-ttu-id="86d96-233">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="86d96-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202]

4. <span data-ttu-id="86d96-235">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="86d96-235">Click **Add** button.</span></span> <span data-ttu-id="86d96-236">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="86d96-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Merhaba eklemek atama bölmesi][203]

5. <span data-ttu-id="86d96-238">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="86d96-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="86d96-239">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="86d96-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="86d96-240">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="86d96-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="86d96-241">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="86d96-241">Test single sign-on</span></span>

<span data-ttu-id="86d96-242">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="86d96-242">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="86d96-243">Merhaba Rally yazılımı hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma Rally yazılımı uygulama tooyour almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="86d96-243">When you click hello Rally Software tile in hello Access Panel, you should get automatically signed-on tooyour Rally Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="86d96-244">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="86d96-244">Additional resources</span></span>

* [<span data-ttu-id="86d96-245">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="86d96-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="86d96-246">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="86d96-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_203.png

