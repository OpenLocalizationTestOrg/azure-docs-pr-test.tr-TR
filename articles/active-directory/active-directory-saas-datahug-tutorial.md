---
title: "Öğretici: Azure Active Directory Tümleştirme ile Datahug | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Datahug arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5c0dc1ea-7ff4-4554-b60b-0f2fa9f5abaa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/18/2017
ms.author: jeedes
ms.openlocfilehash: 79ccb939c7a19720bcf696af141f747db00c8a2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-datahug"></a><span data-ttu-id="e8b5d-103">Öğretici: Azure Active Directory Tümleştirme Datahug ile</span><span class="sxs-lookup"><span data-stu-id="e8b5d-103">Tutorial: Azure Active Directory integration with Datahug</span></span>

<span data-ttu-id="e8b5d-104">Bu öğreticide, bilgi nasıl toointegrate Datahug Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e8b5d-104">In this tutorial, you learn how toointegrate Datahug with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e8b5d-105">Datahug Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="e8b5d-105">Integrating Datahug with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e8b5d-106">Erişim tooDatahug sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="e8b5d-106">You can control in Azure AD who has access tooDatahug</span></span>
- <span data-ttu-id="e8b5d-107">Kullanıcıların tooautomatically get açan tooDatahug (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="e8b5d-107">You can enable your users tooautomatically get signed-on tooDatahug (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e8b5d-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="e8b5d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e8b5d-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="e8b5d-110">[Uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e8b5d-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e8b5d-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e8b5d-111">Prerequisites</span></span>

<span data-ttu-id="e8b5d-112">tooconfigure Datahug ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="e8b5d-112">tooconfigure Azure AD integration with Datahug, you need hello following items:</span></span>

- <span data-ttu-id="e8b5d-113">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="e8b5d-113">An Azure AD subscription</span></span>
- <span data-ttu-id="e8b5d-114">Bir Datahug çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="e8b5d-114">A Datahug single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e8b5d-115">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e8b5d-116">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="e8b5d-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e8b5d-117">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e8b5d-118">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e8b5d-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e8b5d-119">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="e8b5d-119">Scenario description</span></span>
<span data-ttu-id="e8b5d-120">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e8b5d-121">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="e8b5d-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e8b5d-122">Merhaba Galerisi'nden Datahug ekleme</span><span class="sxs-lookup"><span data-stu-id="e8b5d-122">Adding Datahug from hello gallery</span></span>
2. <span data-ttu-id="e8b5d-123">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="e8b5d-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-datahug-from-hello-gallery"></a><span data-ttu-id="e8b5d-124">Merhaba Galerisi'nden Datahug ekleme</span><span class="sxs-lookup"><span data-stu-id="e8b5d-124">Adding Datahug from hello gallery</span></span>
<span data-ttu-id="e8b5d-125">Azure AD'ye tooconfigure hello tümleştirme Datahug, tooadd Datahug hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-125">tooconfigure hello integration of Datahug into Azure AD, you need tooadd Datahug from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e8b5d-126">**tooadd Datahug hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e8b5d-126">**tooadd Datahug from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e8b5d-127">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e8b5d-129">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e8b5d-130">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-130">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="e8b5d-132">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="e8b5d-134">Merhaba arama kutusuna yazın **Datahug**.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-134">In hello search box, type **Datahug**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_search.png)

5. <span data-ttu-id="e8b5d-136">Merhaba Sonuçlar panelinde seçin **Datahug**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-136">In hello results panel, select **Datahug**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e8b5d-138">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="e8b5d-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e8b5d-139">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Datahug ile test etme</span><span class="sxs-lookup"><span data-stu-id="e8b5d-139">In this section, you configure and test Azure AD single sign-on with Datahug based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e8b5d-140">Tek toowork'ın oturum açma hangi hello karşılık gelen Datahug içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Datahug is tooa user in Azure AD.</span></span> <span data-ttu-id="e8b5d-141">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Datahug hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-141">In other words, a link relationship between an Azure AD user and hello related user in Datahug needs toobe established.</span></span>

<span data-ttu-id="e8b5d-142">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** Datahug içinde.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Datahug.</span></span>

<span data-ttu-id="e8b5d-143">tooconfigure ve Datahug ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="e8b5d-143">tooconfigure and test Azure AD single sign-on with Datahug, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e8b5d-144">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e8b5d-145">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e8b5d-146">**[Datahug test kullanıcısı oluşturma](#creating-a-datahug-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Datahug içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-146">**[Creating a Datahug test user](#creating-a-datahug-test-user)** - toohave a counterpart of Britta Simon in Datahug that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e8b5d-147">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e8b5d-148">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e8b5d-149">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e8b5d-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e8b5d-150">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Datahug uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Datahug application.</span></span>

<span data-ttu-id="e8b5d-151">**tooconfigure Azure AD çoklu oturum açma ile Datahug, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e8b5d-151">**tooconfigure Azure AD single sign-on with Datahug, perform hello following steps:**</span></span>

1. <span data-ttu-id="e8b5d-152">Hello hello üzerinde Azure portal'ın **Datahug** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-152">In hello Azure portal, on hello **Datahug** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="e8b5d-154">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_samlbase.png)

3. <span data-ttu-id="e8b5d-156">Merhaba üzerinde **Datahug etki alanı ve URL'leri** tooconfigure hello uygulamada isterseniz, bölümü **IDP** modunda başlatılan:</span><span class="sxs-lookup"><span data-stu-id="e8b5d-156">On hello **Datahug Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_ur1.png)

    <span data-ttu-id="e8b5d-158">a.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-158">a.</span></span> <span data-ttu-id="e8b5d-159">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://apps.datahug.com/identity/<uniqueID>`</span><span class="sxs-lookup"><span data-stu-id="e8b5d-159">In hello **Identifier** textbox, type a URL using hello following pattern: `https://apps.datahug.com/identity/<uniqueID>`</span></span>

    <span data-ttu-id="e8b5d-160">b.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-160">b.</span></span> <span data-ttu-id="e8b5d-161">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://apps.datahug.com/identity/<uniqueID>/acs`</span><span class="sxs-lookup"><span data-stu-id="e8b5d-161">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://apps.datahug.com/identity/<uniqueID>/acs`</span></span>

4. <span data-ttu-id="e8b5d-162">Denetleme **Göster Gelişmiş URL ayarları**.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-162">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="e8b5d-163">Tooconfigure hello uygulamada istiyorsanız **SP** modu tarafından başlatılan:</span><span class="sxs-lookup"><span data-stu-id="e8b5d-163">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_url2.png)

    <span data-ttu-id="e8b5d-165">Merhaba, **oturum açma URL'si** metin kutusuna, URL'yi yazın:`https://apps.datahug.com/`</span><span class="sxs-lookup"><span data-stu-id="e8b5d-165">In hello **Sign-on URL** textbox, type a URL as: `https://apps.datahug.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="e8b5d-166">Bu değerler hello gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-166">These values are not hello real.</span></span> <span data-ttu-id="e8b5d-167">Bu değerleri hello gerçek tanımlayıcısı ve yanıt URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-167">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="e8b5d-168">Burada, toouse hello benzersiz değer hello tanımlayıcı dizesinde ve yanıt URL'si öneririz.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-168">Here we suggest you toouse hello unique value of string in hello Identifier and Reply URL.</span></span> <span data-ttu-id="e8b5d-169">Kişi [Datahug istemci destek ekibi](http://datahug.com/about/contact-us/) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-169">Contact [Datahug Client support team](http://datahug.com/about/contact-us/) tooget these values.</span></span> 

5. <span data-ttu-id="e8b5d-170">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-170">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_certificate.png) 

6.  <span data-ttu-id="e8b5d-172">Denetleme **"Göster gelişmiş sertifika imzalama ayarları"** ve hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e8b5d-172">Check **“Show advanced certificate signing settings”** and perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_cert.png)

    <span data-ttu-id="e8b5d-174">a.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-174">a.</span></span> <span data-ttu-id="e8b5d-175">İçinde **imzalama seçeneği**seçin **oturum SAML onayı**.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-175">In **Signing Option**, select **Sign SAML assertion**.</span></span>
    
    <span data-ttu-id="e8b5d-176">b.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-176">b.</span></span> <span data-ttu-id="e8b5d-177">İçinde **imzalama algoritması**seçin **SHA1**.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-177">In **Signing algorithm**, select **SHA1**.</span></span>
 
7. <span data-ttu-id="e8b5d-178">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-178">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-datahug-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="e8b5d-180">Merhaba üzerinde **Datahug yapılandırma** 'yi tıklatın **yapılandırma Datahug** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-180">On hello **Datahug Configuration** section, click **Configure Datahug** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="e8b5d-181">Kopya hello **SAML varlık kimliği** ve **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="e8b5d-181">Copy hello **SAML Entity ID** and **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_configure.png) 

9. <span data-ttu-id="e8b5d-183">tooconfigure çoklu oturum açma üzerinde **Datahug** yan, indirilen toosend hello ihtiyacınız **meta veri XML**, **SAML varlık kimliği** ve **SAML çoklu oturum açma hizmeti URL** çok[Datahug Destek](http://datahug.com/about/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="e8b5d-183">tooconfigure single sign-on on **Datahug** side, you need toosend hello downloaded **Metadata XML**, **SAML Entity ID** and **SAML Single Sign-On Service URL** too[Datahug support](http://datahug.com/about/contact-us/).</span></span> <span data-ttu-id="e8b5d-184">Bunlar, bu uygulama toohave hello iki tarafta da ayarlamanızı SAML SSO bağlantı ayarlama.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-184">They set this application up toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="e8b5d-185">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="e8b5d-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e8b5d-186">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e8b5d-187">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e8b5d-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e8b5d-188">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e8b5d-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="e8b5d-189">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="e8b5d-191">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e8b5d-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e8b5d-192">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-192">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-datahug-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e8b5d-194">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-194">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-datahug-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e8b5d-196">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-196">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-datahug-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e8b5d-198">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e8b5d-198">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-datahug-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e8b5d-200">a.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-200">a.</span></span> <span data-ttu-id="e8b5d-201">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-201">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e8b5d-202">b.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-202">b.</span></span> <span data-ttu-id="e8b5d-203">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-203">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e8b5d-204">c.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-204">c.</span></span> <span data-ttu-id="e8b5d-205">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-205">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e8b5d-206">d.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-206">d.</span></span> <span data-ttu-id="e8b5d-207">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-207">Click **Create**.</span></span>
 
### <a name="creating-a-datahug-test-user"></a><span data-ttu-id="e8b5d-208">Datahug test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e8b5d-208">Creating a Datahug test user</span></span>

<span data-ttu-id="e8b5d-209">tooenable Azure AD kullanıcıların toolog tooDatahug bunların Datahug sağlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-209">tooenable Azure AD users toolog in tooDatahug, they must be provisioned into Datahug.</span></span>  
<span data-ttu-id="e8b5d-210">Datahug, sağlama el ile bir görev olduğunda.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-210">When Datahug, provisioning is a manual task.</span></span>

<span data-ttu-id="e8b5d-211">**bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e8b5d-211">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="e8b5d-212">İçinde tooyour Datahug şirket site yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-212">Log in tooyour Datahug company site as an administrator.</span></span>

2. <span data-ttu-id="e8b5d-213">Merhaba getirin **dişlisine** hello sağ üst ve tıklatın **ayarları**</span><span class="sxs-lookup"><span data-stu-id="e8b5d-213">Hover over hello **cog** in hello top right-hand corner and click **Settings**</span></span>
   
   ![Çalışanı ekleyin](./media/active-directory-saas-datahug-tutorial/1.png)

3. <span data-ttu-id="e8b5d-215">Seçin **kişiler** hello tıklatıp **Kullanıcı Ekle** sekmesi</span><span class="sxs-lookup"><span data-stu-id="e8b5d-215">Choose **People** and click hello **Add Users** tab</span></span>

    ![Çalışanı ekleyin](./media/active-directory-saas-datahug-tutorial/2.png)

4. <span data-ttu-id="e8b5d-217">Yazın gibi hello kişinin hello e-posta hesabı için bir toocreate tıklatıp **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-217">Type hello email of hello person you would like toocreate an account for and click **Add**.</span></span>

    ![Çalışanı ekleyin](./media/active-directory-saas-datahug-tutorial/3.png)

    > [!NOTE] 
    > <span data-ttu-id="e8b5d-219">Seçerek kayıt posta toouser gönderebilirsiniz **Hoş Geldiniz e-posta Gönder** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-219">You can send registration mail toouser by selecting **Send welcome email** checkbox.</span></span>  
    > <span data-ttu-id="e8b5d-220">Oluşturuyorsanız, Salesforce için bir hesap göndermeyin hello Hoş Geldiniz e-posta.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-220">If you are creating an account for Salesforce do not send hello welcome email.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e8b5d-221">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="e8b5d-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e8b5d-222">Bu bölümde, erişim tooDatahug vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDatahug.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="e8b5d-224">**tooassign Britta Simon tooDatahug hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e8b5d-224">**tooassign Britta Simon tooDatahug, perform hello following steps:**</span></span>

1. <span data-ttu-id="e8b5d-225">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-225">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="e8b5d-227">Merhaba uygulamalar listesinde **Datahug**.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-227">In hello applications list, select **Datahug**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_app.png) 

3. <span data-ttu-id="e8b5d-229">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="e8b5d-231">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-231">Click **Add** button.</span></span> <span data-ttu-id="e8b5d-232">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="e8b5d-234">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e8b5d-235">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e8b5d-236">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e8b5d-237">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="e8b5d-237">Testing single sign-on</span></span>

<span data-ttu-id="e8b5d-238">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-238">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>
<span data-ttu-id="e8b5d-239">Merhaba Datahug hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Datahug uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e8b5d-239">When you click hello Datahug tile in hello Access Panel, you should get automatically signed-on tooyour Datahug application.</span></span> <span data-ttu-id="e8b5d-240">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="e8b5d-240">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="e8b5d-241">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="e8b5d-241">Additional resources</span></span>

* [<span data-ttu-id="e8b5d-242">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="e8b5d-242">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e8b5d-243">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="e8b5d-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_203.png

