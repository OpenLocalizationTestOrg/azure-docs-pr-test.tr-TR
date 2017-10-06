---
title: "Öğretici: Azure Active Directory Tümleştirme Atlassian bulut ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Atlassian bulut arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 729b8eb6-efc4-47fb-9f34-8998ca2c9545
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: f679e8b3306bf0efb9373d8baa0cfe095b760aaf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-atlassian-cloud"></a><span data-ttu-id="b44ff-103">Öğretici: Azure Active Directory Tümleştirme Atlassian bulut ile</span><span class="sxs-lookup"><span data-stu-id="b44ff-103">Tutorial: Azure Active Directory integration with Atlassian Cloud</span></span>

<span data-ttu-id="b44ff-104">Bu öğreticide, bilgi toointegrate Atlassian bulut nasıl Azure Active Directory (Azure AD) ile.</span><span class="sxs-lookup"><span data-stu-id="b44ff-104">In this tutorial, you learn how toointegrate Atlassian Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b44ff-105">Atlassian bulut Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="b44ff-105">Integrating Atlassian Cloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b44ff-106">Erişim tooAtlassian bulut sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="b44ff-106">You can control in Azure AD who has access tooAtlassian Cloud</span></span>
- <span data-ttu-id="b44ff-107">Kullanıcıların tooautomatically get açan tooAtlassian bulut (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="b44ff-107">You can enable your users tooautomatically get signed-on tooAtlassian Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b44ff-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="b44ff-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b44ff-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b44ff-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b44ff-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="b44ff-110">Prerequisites</span></span>

<span data-ttu-id="b44ff-111">tooconfigure Atlassian bulut ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="b44ff-111">tooconfigure Azure AD integration with Atlassian Cloud, you need hello following items:</span></span>

- <span data-ttu-id="b44ff-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="b44ff-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b44ff-113">Bir Atlassian bulut çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="b44ff-113">An Atlassian Cloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b44ff-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="b44ff-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b44ff-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="b44ff-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b44ff-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="b44ff-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b44ff-117">Bir Azure AD deneme ortam yoksa, burada bir aylık deneme elde edebilirsiniz: [deneme teklifi](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b44ff-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b44ff-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="b44ff-118">Scenario description</span></span>
<span data-ttu-id="b44ff-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="b44ff-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b44ff-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="b44ff-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b44ff-121">Merhaba Galerisi'nden Atlassian bulut ekleme</span><span class="sxs-lookup"><span data-stu-id="b44ff-121">Adding Atlassian Cloud from hello gallery</span></span>
2. <span data-ttu-id="b44ff-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="b44ff-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-atlassian-cloud-from-hello-gallery"></a><span data-ttu-id="b44ff-123">Merhaba Galerisi'nden Atlassian bulut ekleme</span><span class="sxs-lookup"><span data-stu-id="b44ff-123">Adding Atlassian Cloud from hello gallery</span></span>
<span data-ttu-id="b44ff-124">Azure AD'ye tooconfigure hello tümleştirme Atlassian bulutun tooadd Atlassian bulut hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="b44ff-124">tooconfigure hello integration of Atlassian Cloud into Azure AD, you need tooadd Atlassian Cloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b44ff-125">**tooadd Atlassian bulut hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="b44ff-125">**tooadd Atlassian Cloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b44ff-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="b44ff-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b44ff-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="b44ff-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b44ff-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="b44ff-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="b44ff-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="b44ff-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="b44ff-133">Merhaba arama kutusuna yazın **Atlassian bulut**.</span><span class="sxs-lookup"><span data-stu-id="b44ff-133">In hello search box, type **Atlassian Cloud**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_search.png)

5. <span data-ttu-id="b44ff-135">Merhaba Sonuçlar panelinde seçin **Atlassian bulut**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="b44ff-135">In hello results panel, select **Atlassian Cloud**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b44ff-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="b44ff-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b44ff-138">Bu bölümde, yapılandırmanız ve Atlassian bulut ile Azure AD çoklu oturum açmayı test "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı</span><span class="sxs-lookup"><span data-stu-id="b44ff-138">In this section, you configure and test Azure AD single sign-on with Atlassian Cloud based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b44ff-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Atlassian bulutta tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="b44ff-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Atlassian Cloud is tooa user in Azure AD.</span></span> <span data-ttu-id="b44ff-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve Atlassian bulutta hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="b44ff-140">In other words, a link relationship between an Azure AD user and hello related user in Atlassian Cloud needs toobe established.</span></span>

<span data-ttu-id="b44ff-141">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** Atlassian bulutta.</span><span class="sxs-lookup"><span data-stu-id="b44ff-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Atlassian Cloud.</span></span>

<span data-ttu-id="b44ff-142">tooconfigure ve Atlassian bulut ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="b44ff-142">tooconfigure and test Azure AD single sign-on with Atlassian Cloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b44ff-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="b44ff-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b44ff-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="b44ff-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b44ff-145">**[Bir Atlassian bulut test kullanıcısı oluşturma](#creating-an-atlassian-cloud-test-user)**  -toohave karşılık gelen, Britta Simon Atlassian bulutta kullanıcı bağlantılı toohello Azure AD gösterimidir.</span><span class="sxs-lookup"><span data-stu-id="b44ff-145">**[Creating an Atlassian Cloud test user](#creating-an-atlassian-cloud-test-user)** - toohave a counterpart of Britta Simon in Atlassian Cloud that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b44ff-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="b44ff-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b44ff-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="b44ff-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b44ff-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b44ff-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b44ff-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Atlassian bulut uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="b44ff-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Atlassian Cloud application.</span></span>

<span data-ttu-id="b44ff-150">**tooconfigure Azure AD çoklu oturum açma Atlassian bulut ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="b44ff-150">**tooconfigure Azure AD single sign-on with Atlassian Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="b44ff-151">Hello hello üzerinde Azure portal'ın **Atlassian bulut** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="b44ff-151">In hello Azure portal, on hello **Atlassian Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="b44ff-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="b44ff-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_samlbase.png)

3. <span data-ttu-id="b44ff-155">Merhaba üzerinde **Atlassian bulut etki alanı ve URL'leri** bölümünde, hello tooconfigure hello uygulamada istiyorsanız aşağıdaki adımları gerçekleştirin **IDP** modu tarafından başlatılan:</span><span class="sxs-lookup"><span data-stu-id="b44ff-155">On hello **Atlassian Cloud Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_url.png)

    <span data-ttu-id="b44ff-157">a.</span><span class="sxs-lookup"><span data-stu-id="b44ff-157">a.</span></span> <span data-ttu-id="b44ff-158">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<instancename>.atlassian.net/admin/saml/edit`</span><span class="sxs-lookup"><span data-stu-id="b44ff-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<instancename>.atlassian.net/admin/saml/edit`</span></span>

    <span data-ttu-id="b44ff-159">b.</span><span class="sxs-lookup"><span data-stu-id="b44ff-159">b.</span></span> <span data-ttu-id="b44ff-160">Merhaba, **yanıt URL'si** metin kutusuna, URL'yi yazın:`https://id.atlassian.com/login/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="b44ff-160">In hello **Reply URL** textbox, type a URL as: `https://id.atlassian.com/login/saml/acs`</span></span>

4. <span data-ttu-id="b44ff-161">Denetleme **Göster Gelişmiş URL ayarları** ve adım tooconfigure hello uygulamada istiyorsanız aşağıdaki hello gerçekleştirmek **SP** modunda başlatılan:</span><span class="sxs-lookup"><span data-stu-id="b44ff-161">Check **Show advanced URL settings** and perform hello following step if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_url1.png)

    <span data-ttu-id="b44ff-163">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<instancename>.atlassian.net`</span><span class="sxs-lookup"><span data-stu-id="b44ff-163">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<instancename>.atlassian.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b44ff-164">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="b44ff-164">These values are not real.</span></span> <span data-ttu-id="b44ff-165">Bu güncelleştirme tanımlayıcısı ve oturum açma URL'si ile Merhaba gerçek değerler.</span><span class="sxs-lookup"><span data-stu-id="b44ff-165">Update these values with hello actual Identifier and Sign-On URL.</span></span> <span data-ttu-id="b44ff-166">Atlassian bulut SAML Yapılandırma ekranından hello tam değerleri alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b44ff-166">You can get hello exact values from Atlassian Cloud SAML Configuration screen.</span></span>
 
5. <span data-ttu-id="b44ff-167">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="b44ff-167">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_certificate.png) 

6. <span data-ttu-id="b44ff-169">Merhaba üzerinde **Atlassian bulut Yapılandırması** 'yi tıklatın **Atlassian bulut yapılandırma** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="b44ff-169">On hello **Atlassian Cloud Configuration** section, click **Configure Atlassian Cloud** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="b44ff-170">Kopya hello **SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="b44ff-170">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_configure.png) 

7. <span data-ttu-id="b44ff-172">tooget SSO hello yönetici hakları kullanarak Atlassian portalı oturum açma toohello, uygulamanız için yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="b44ff-172">tooget SSO configured for your application, login toohello Atlassian Portal using hello administrator rights.</span></span>

8. <span data-ttu-id="b44ff-173">Sol gezinti Merhaba, kimlik doğrulaması bölümü Hello tıklatın **etki alanları**.</span><span class="sxs-lookup"><span data-stu-id="b44ff-173">In hello Authentication section of hello left navigation click **Domains**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_06.png)

    <span data-ttu-id="b44ff-175">a.</span><span class="sxs-lookup"><span data-stu-id="b44ff-175">a.</span></span> <span data-ttu-id="b44ff-176">Merhaba metin kutusuna, etki alanı adınızı yazın ve ardından **etki alanı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="b44ff-176">In hello textbox, type your domain name, and then click **Add domain**.</span></span>
        
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_07.png)

    <span data-ttu-id="b44ff-178">b.</span><span class="sxs-lookup"><span data-stu-id="b44ff-178">b.</span></span> <span data-ttu-id="b44ff-179">tooverify hello etki alanı, tıklatın **doğrula**.</span><span class="sxs-lookup"><span data-stu-id="b44ff-179">tooverify hello domain, click **Verify**.</span></span> 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_08.png)

    <span data-ttu-id="b44ff-181">c.</span><span class="sxs-lookup"><span data-stu-id="b44ff-181">c.</span></span> <span data-ttu-id="b44ff-182">Merhaba etki alanı doğrulama html dosya indirme, etki alanınızın Web sitesinin kök klasörü toohello karşıya yükleyin ve ardından **etki alanını doğrula**.</span><span class="sxs-lookup"><span data-stu-id="b44ff-182">Download hello domain verification html file, upload it toohello root folder of your domain's website, and then click **Verify domain**.</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_09.png)

    <span data-ttu-id="b44ff-184">d.</span><span class="sxs-lookup"><span data-stu-id="b44ff-184">d.</span></span> <span data-ttu-id="b44ff-185">Merhaba etki alanı doğrulandıktan sonra hello değerini hello **durum** alandır **doğrulandı**.</span><span class="sxs-lookup"><span data-stu-id="b44ff-185">Once hello domain is verified, hello value of hello **Status** field is **Verified**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_10.png)

9. <span data-ttu-id="b44ff-187">Merhaba sol gezinti çubuğunda, **SAML**.</span><span class="sxs-lookup"><span data-stu-id="b44ff-187">In hello left navigation bar, click **SAML**.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_11.png)

10. <span data-ttu-id="b44ff-189">SAML yapılandırması oluşturun ve hello kimlik sağlayıcı yapılandırması ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b44ff-189">Create a SAML Configuration and add hello Identity provider configuration.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_12.png)

    <span data-ttu-id="b44ff-191">a.</span><span class="sxs-lookup"><span data-stu-id="b44ff-191">a.</span></span> <span data-ttu-id="b44ff-192">Merhaba, **kimlik sağlayıcısı varlık kimliği** metin kutusuna, Yapıştır hello değerini **SAML varlık kimliği** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="b44ff-192">In hello **Identity provider Entity ID** text box, paste hello value of  **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="b44ff-193">b.</span><span class="sxs-lookup"><span data-stu-id="b44ff-193">b.</span></span> <span data-ttu-id="b44ff-194">Merhaba, **kimlik sağlayıcısı SSO URL** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="b44ff-194">In hello **Identity provider SSO URL** text box, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="b44ff-195">c.</span><span class="sxs-lookup"><span data-stu-id="b44ff-195">c.</span></span> <span data-ttu-id="b44ff-196">İndirilen hello sertifika hello başlangıç olmadan Azure portal ve kopyalama hello değerlerden ve satır sonu karakteri açın ve hello yapıştırın **ortak X509 sertifika** kutusu.</span><span class="sxs-lookup"><span data-stu-id="b44ff-196">Open hello downloaded certificate from Azure portal and copy hello values without hello Begin and End lines and paste it in hello **Public X509 certificate** box.</span></span>
    
    <span data-ttu-id="b44ff-197">d.</span><span class="sxs-lookup"><span data-stu-id="b44ff-197">d.</span></span> <span data-ttu-id="b44ff-198">Tıklatın **yapılandırmayı Kaydet** tooSave hello ayarları.</span><span class="sxs-lookup"><span data-stu-id="b44ff-198">Click **Save Configuration**  tooSave hello settings.</span></span>
     
11. <span data-ttu-id="b44ff-199">Hello Azure AD ayarları toomake tanımlayıcı URL'si düzeltmek Kurulum hello sahip olduğunuzdan emin güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="b44ff-199">Update hello Azure AD settings toomake sure that you have setup hello correct Identifier URL.</span></span>
  
    <span data-ttu-id="b44ff-200">a.</span><span class="sxs-lookup"><span data-stu-id="b44ff-200">a.</span></span> <span data-ttu-id="b44ff-201">Kopya hello **SP kimlik kimliği** SAML hello ekranında ve hello olarak Azure AD yapıştırın **tanımlayıcısı** değeri.</span><span class="sxs-lookup"><span data-stu-id="b44ff-201">Copy hello **SP Identity ID** from hello SAML screen and paste it in Azure AD as hello **Identifier** value.</span></span>

    <span data-ttu-id="b44ff-202">b.</span><span class="sxs-lookup"><span data-stu-id="b44ff-202">b.</span></span> <span data-ttu-id="b44ff-203">Oturum üzerinde hello Kiracı Atlassian bulutun URL'dir.</span><span class="sxs-lookup"><span data-stu-id="b44ff-203">Sign On URL is hello tenant URL of your Atlassian Cloud.</span></span>     

     ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_13.png)
    
12. <span data-ttu-id="b44ff-205">Hello Azure portal'ı tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="b44ff-205">In hello Azure portal, Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_400.png)

> [!TIP]
> <span data-ttu-id="b44ff-207">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="b44ff-207">You can now read a concise version of these instructions inside hello [Azure  portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b44ff-208">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="b44ff-208">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b44ff-209">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b44ff-209">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b44ff-210">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="b44ff-210">Creating an Azure AD test user</span></span>
<span data-ttu-id="b44ff-211">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="b44ff-211">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="b44ff-213">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="b44ff-213">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b44ff-214">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="b44ff-214">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b44ff-216">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="b44ff-216">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b44ff-218">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="b44ff-218">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b44ff-220">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="b44ff-220">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b44ff-222">a.</span><span class="sxs-lookup"><span data-stu-id="b44ff-222">a.</span></span> <span data-ttu-id="b44ff-223">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b44ff-223">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b44ff-224">b.</span><span class="sxs-lookup"><span data-stu-id="b44ff-224">b.</span></span> <span data-ttu-id="b44ff-225">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="b44ff-225">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b44ff-226">c.</span><span class="sxs-lookup"><span data-stu-id="b44ff-226">c.</span></span> <span data-ttu-id="b44ff-227">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="b44ff-227">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b44ff-228">d.</span><span class="sxs-lookup"><span data-stu-id="b44ff-228">d.</span></span> <span data-ttu-id="b44ff-229">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b44ff-229">Click **Create**.</span></span>
 
### <a name="creating-an-atlassian-cloud-test-user"></a><span data-ttu-id="b44ff-230">Bir Atlassian bulut test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="b44ff-230">Creating an Atlassian Cloud test user</span></span>

<span data-ttu-id="b44ff-231">tooenable Azure AD kullanıcıların toolog tooAtlassian bulut'da, bunlar Atlassian bulutunu sağlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b44ff-231">tooenable Azure AD users toolog in tooAtlassian Cloud, they must be provisioned into Atlassian Cloud.</span></span>  
<span data-ttu-id="b44ff-232">Atlassian bulut durumunda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="b44ff-232">In case of Atlassian Cloud, provisioning is a manual task.</span></span>

<span data-ttu-id="b44ff-233">**bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="b44ff-233">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="b44ff-234">Hello Site Yönetim bölümünde, hello tıklatın **kullanıcılar** düğmesi</span><span class="sxs-lookup"><span data-stu-id="b44ff-234">In hello Site administration section, click hello **Users** button</span></span>

    ![Atlassian bulut kullanıcı oluştur](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_14.png) 

2. <span data-ttu-id="b44ff-236">Merhaba tıklatın **kullanıcı oluştur** düğmesini toocreate hello Atlassian bulut uygulamasında bir kullanıcı</span><span class="sxs-lookup"><span data-stu-id="b44ff-236">Click hello **Create User** button toocreate a user in hello Atlassian Cloud</span></span>

    ![Atlassian bulut kullanıcı oluştur](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_15.png) 

3. <span data-ttu-id="b44ff-238">Merhaba kullanıcının girin **e-posta adresi**, **kullanıcıadı**, ve **tam adı** ve hello uygulama erişimi atayın.</span><span class="sxs-lookup"><span data-stu-id="b44ff-238">Enter hello user's **Email address**, **Username**, and **Full Name** and assign hello application access.</span></span> 

    ![Atlassian bulut kullanıcı oluştur](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_16.png)
 
4. <span data-ttu-id="b44ff-240">Tıklatın **kullanıcı oluşturma** düğmesi, onu hello e-posta daveti toohello kullanıcı gönderir ve kabul sonra hello davet hello kullanıcı hello sistemde etkin olacaktır.</span><span class="sxs-lookup"><span data-stu-id="b44ff-240">Click **Create user** button, it will send hello email invitation toohello user and after accepting hello invitation hello user will be active in hello system.</span></span> 

>[!NOTE] 
><span data-ttu-id="b44ff-241">Merhaba tıklayarak toplu kullanıcılar hello oluşturabilir **Toplu oluşturma** hello kullanıcılar bölümü düğmesini.</span><span class="sxs-lookup"><span data-stu-id="b44ff-241">You can also create hello bulk users by clicking hello **Bulk Create** button in hello Users section.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b44ff-242">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="b44ff-242">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b44ff-243">Bu bölümde, erişim tooAtlassian bulut vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="b44ff-243">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAtlassian Cloud.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="b44ff-245">**tooassign Britta Simon tooAtlassian bulut hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="b44ff-245">**tooassign Britta Simon tooAtlassian Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="b44ff-246">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="b44ff-246">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="b44ff-248">Merhaba uygulamalar listesinde **Atlassian bulut**.</span><span class="sxs-lookup"><span data-stu-id="b44ff-248">In hello applications list, select **Atlassian Cloud**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_app.png) 

3. <span data-ttu-id="b44ff-250">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="b44ff-250">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="b44ff-252">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="b44ff-252">Click **Add** button.</span></span> <span data-ttu-id="b44ff-253">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="b44ff-253">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="b44ff-255">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="b44ff-255">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b44ff-256">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="b44ff-256">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b44ff-257">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="b44ff-257">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b44ff-258">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="b44ff-258">Testing single sign-on</span></span>

<span data-ttu-id="b44ff-259">Bu bölümde, Azure AD SSO yapılandırmanızı hello erişim paneli kullanarak sınayın.</span><span class="sxs-lookup"><span data-stu-id="b44ff-259">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="b44ff-260">Atlassian bulut döşeme hello erişim paneli hello tıkladığınızda, otomatik olarak oturum açma Atlassian bulut uygulaması tooyour almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b44ff-260">When you click hello Atlassian Cloud tile in hello Access Panel, you should get automatically signed-on tooyour Atlassian Cloud application.</span></span> <span data-ttu-id="b44ff-261">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b44ff-261">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b44ff-262">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="b44ff-262">Additional resources</span></span>

* [<span data-ttu-id="b44ff-263">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="b44ff-263">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b44ff-264">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="b44ff-264">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_203.png

