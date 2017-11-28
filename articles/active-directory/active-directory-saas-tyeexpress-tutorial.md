---
title: "Öğretici: T & E Express Azure Active Directory Tümleştirme | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve T & E Express arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: B42374E5-2559-4309-8EF2-820BEE7EBB0C
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: jeedes
ms.openlocfilehash: 9a568ace8dbc75fadbf37554996b1b597a813d56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-te-express"></a><span data-ttu-id="1aa6e-103">Öğretici: T & E Express Azure Active Directory Tümleştirme</span><span class="sxs-lookup"><span data-stu-id="1aa6e-103">Tutorial: Azure Active Directory integration with T&E Express</span></span>

<span data-ttu-id="1aa6e-104">Bu öğreticide, bilgi nasıl toointegrate T & E Express Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1aa6e-104">In this tutorial, you learn how toointegrate T&E Express with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1aa6e-105">T & E Express Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="1aa6e-105">Integrating T&E Express with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1aa6e-106">Erişim Systems olan Azure AD & E Express kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="1aa6e-106">You can control in Azure AD who has access tooT&E Express</span></span>
- <span data-ttu-id="1aa6e-107">Azure AD hesaplarına açan kullanıcıları tooautomatically get Systems & E Express (çoklu oturum açma) etkinleştir</span><span class="sxs-lookup"><span data-stu-id="1aa6e-107">You can enable your users tooautomatically get signed-on tooT&E Express (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1aa6e-108">Bir merkezi konumda - hello Azure Yönetim Portalı hesaplarınızı yönetebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="1aa6e-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="1aa6e-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1aa6e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1aa6e-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="1aa6e-110">Prerequisites</span></span>

<span data-ttu-id="1aa6e-111">T & E Express ile Azure AD tümleştirme tooconfigure, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="1aa6e-111">tooconfigure Azure AD integration with T&E Express, you need hello following items:</span></span>

- <span data-ttu-id="1aa6e-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="1aa6e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1aa6e-113">Bir T & E Express çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="1aa6e-113">A T&E Express single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1aa6e-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1aa6e-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="1aa6e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1aa6e-116">Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="1aa6e-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1aa6e-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1aa6e-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="1aa6e-118">Scenario description</span></span>
<span data-ttu-id="1aa6e-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1aa6e-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="1aa6e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1aa6e-121">T & E Express hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="1aa6e-121">Adding T&E Express from hello gallery</span></span>
2. <span data-ttu-id="1aa6e-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="1aa6e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-te-express-from-hello-gallery"></a><span data-ttu-id="1aa6e-123">T & E Express hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="1aa6e-123">Adding T&E Express from hello gallery</span></span>
<span data-ttu-id="1aa6e-124">Azure AD'ye tooconfigure hello tümleştirme T & E Express hello galeri tooyour listesinden yönetilen SaaS uygulamaları tooadd T & E Express gerekir.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-124">tooconfigure hello integration of T&E Express into Azure AD, you need tooadd T&E Express from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1aa6e-125">**tooadd T & E Express hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="1aa6e-125">**tooadd T&E Express from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1aa6e-126">Merhaba,  **[Azure Yönetim Portalı](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1aa6e-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1aa6e-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="1aa6e-131">Tıklatın **Ekle** hello iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="1aa6e-133">Merhaba arama kutusuna yazın **T & E Express**.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-133">In hello search box, type **T&E Express**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_search.png)

5. <span data-ttu-id="1aa6e-135">Merhaba Sonuçlar panelinde seçin **T & E Express**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-135">In hello results panel, select **T&E Express**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1aa6e-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="1aa6e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1aa6e-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma T & "Britta Simon" adlı bir test kullanıcıyı temel alarak E Express ile test etme.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-138">In this section, you configure and test Azure AD single sign-on with T&E Express based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1aa6e-139">Tek toowork'ın oturum açma hangi hello karşılık gelen T & E Express tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in T&E Express is tooa user in Azure AD.</span></span> <span data-ttu-id="1aa6e-140">Diğer bir deyişle, bir bağlantı bir Azure AD kullanıcı ve kullanıcı arasındaki ilişki hello ilgili kurulan T & E Express gereksinimlerini toobe içinde.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-140">In other words, a link relationship between an Azure AD user and hello related user in T&E Express needs toobe established.</span></span>

<span data-ttu-id="1aa6e-141">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** T & E Express.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in T&E Express.</span></span>

<span data-ttu-id="1aa6e-142">tooconfigure ve T & E Express ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="1aa6e-142">tooconfigure and test Azure AD single sign-on with T&E Express, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1aa6e-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1aa6e-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1aa6e-145">**[T & E Express test kullanıcısı oluşturma](#creating-a-te-express-test-user)**  -toohave Britta Simon T & E her bağlantılı toohello Azure AD gösterimi olan Express, karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-145">**[Creating a T&E Express test user](#creating-a-te-express-test-user)** - toohave a counterpart of Britta Simon in T&E Express that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="1aa6e-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1aa6e-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1aa6e-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="1aa6e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1aa6e-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure Yönetim Portalı'nda etkinleştirin ve çoklu oturum açma, T & E Express uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your T&E Express application.</span></span>

<span data-ttu-id="1aa6e-150">**T & E Express, Azure AD çoklu oturum açma tooconfigure hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="1aa6e-150">**tooconfigure Azure AD single sign-on with T&E Express, perform hello following steps:**</span></span>

1. <span data-ttu-id="1aa6e-151">Hello üzerinde hello Azure Yönetim Portalı'nda **T & E Express** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-151">In hello Azure Management portal, on hello **T&E Express** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="1aa6e-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda, olarak **modu** seçin **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_samlbase.png)

3. <span data-ttu-id="1aa6e-155">Merhaba üzerinde **T & E Express etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="1aa6e-155">On hello **T&E Express Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_url.png)

    <span data-ttu-id="1aa6e-157">a.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-157">a.</span></span> <span data-ttu-id="1aa6e-158">Merhaba, **tanımlayıcısı** metin kutusuna, türü hello değeri olarak:`https://<domain>.tyeexpress.com`</span><span class="sxs-lookup"><span data-stu-id="1aa6e-158">In hello **Identifier** textbox, type hello value as: `https://<domain>.tyeexpress.com`</span></span>

    <span data-ttu-id="1aa6e-159">b.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-159">b.</span></span> <span data-ttu-id="1aa6e-160">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<domain>.tyeexpress.com/authorize/samlConsume.aspx`</span><span class="sxs-lookup"><span data-stu-id="1aa6e-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<domain>.tyeexpress.com/authorize/samlConsume.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1aa6e-161">Lütfen bu hello gerçek değerler olmadığına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="1aa6e-162">Tooupdate hello gerçek tanımlayıcısı ve yanıt URL'si ile bu değerlere sahip.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-162">You have tooupdate these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="1aa6e-163">Burada, toouse hello benzersiz değerini hello tanımlayıcı dizesinde öneririz.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="1aa6e-164">Kişi [T & E Express desteğini takım](http://www.tyeexpress.com/contacto.aspx) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-164">Contact [T&E Express support team](http://www.tyeexpress.com/contacto.aspx) tooget these values.</span></span>

5. <span data-ttu-id="1aa6e-165">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello XML dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_certificate.png) 

6. <span data-ttu-id="1aa6e-167">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-167">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="1aa6e-169">tooconfigure çoklu oturum açma üzerinde **T & E Express** yan, oturum açma toohello T & E express uygulaması SAML olmadan tek yönetici kimlik bilgilerini kullanarak oturum.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-169">tooconfigure single sign-on on **T&E Express** side, login toohello T&E express application without SAML single sign on using admin credentials.</span></span>

9. <span data-ttu-id="1aa6e-170">Merhaba altında **yönetici** sekmesini ve ardından üzerinde **SAML etki alanı** tooOpen hello SAML Ayarları sayfası.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-170">Under hello **Admin** Tab, Click on **SAML domain** tooOpen hello SAML settings page.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tyeexpress-tutorial/tye-SAML.png)

10. <span data-ttu-id="1aa6e-172">Select hello **Activar(Activate)** gelen seçeneği **Hayır** çok**SI(Yes)**.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-172">Select hello **Activar(Activate)** option from **No** too**SI(Yes)**.</span></span> <span data-ttu-id="1aa6e-173">Merhaba, **kimlik sağlayıcısı meta verileri** metin kutusuna, Yapıştır hello meta verileri sahip XML donwloaded Azure portalından.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-173">In hello **Identity Provider Metadata** textbox, paste hello metadata XML which you have donwloaded from Azure portal.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tyeexpress-tutorial/tyeAdmin.png)

11. <span data-ttu-id="1aa6e-175">Tıklatın hello üzerinde **Guardar(Save)** düğmesini toosave hello ayarları.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-175">Click on hello **Guardar(Save)** button toosave hello settings.</span></span> 


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1aa6e-176">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="1aa6e-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="1aa6e-177">Bu bölümde Hello amacı toocreate Britta Simon adlı hello Azure Yönetim Portalı'nda bir sınama kullanıcısı ' dir.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-177">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="1aa6e-179">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="1aa6e-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1aa6e-180">Merhaba, **Azure Yönetim Portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-180">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1aa6e-182">Çok Git**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar** toodisplay hello kullanıcılar listesi.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-182">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1aa6e-184">Merhaba hello iletişim üstündeki **Ekle** tooopen hello **kullanıcı** iletişim.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-184">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1aa6e-186">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="1aa6e-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1aa6e-188">a.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-188">a.</span></span> <span data-ttu-id="1aa6e-189">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1aa6e-190">b.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-190">b.</span></span> <span data-ttu-id="1aa6e-191">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1aa6e-192">c.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-192">c.</span></span> <span data-ttu-id="1aa6e-193">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1aa6e-194">d.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-194">d.</span></span> <span data-ttu-id="1aa6e-195">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-195">Click **Create**.</span></span>
 
### <a name="creating-a-te-express-test-user"></a><span data-ttu-id="1aa6e-196">T & E Express test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="1aa6e-196">Creating a T&E Express test user</span></span>

<span data-ttu-id="1aa6e-197">T & E Express içine sipariş tooenable Azure AD kullanıcıların toolog bunlar T & E Express sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-197">In order tooenable Azure AD users toolog into T&E Express, they must be provisioned into T&E Express.</span></span>  
<span data-ttu-id="1aa6e-198">T & E Express durumunda, sağlama el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-198">In case of T&E Express, provisioning is a manual task.</span></span>

<span data-ttu-id="1aa6e-199">**bir kullanıcı hesapları tooprovision gerçekleştirmek hello adımları izleyin:**</span><span class="sxs-lookup"><span data-stu-id="1aa6e-199">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="1aa6e-200">Tooyour T & E Express şirket site yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-200">Log in tooyour T&E Express company site as an administrator.</span></span>

2. <span data-ttu-id="1aa6e-201">Yönetici etiketi altında kullanıcıları tooopen hello kullanıcılar ana sayfasında tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-201">Under Admin tag, click on Users tooopen hello Users master page.</span></span>

    ![Çalışanı ekleyin](./media/active-directory-saas-tyeexpress-tutorial/tye-adminusers.png)

3. <span data-ttu-id="1aa6e-203">Merhaba giriş sayfasında, tıklatın  **+**  tooadd hello kullanıcılar.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-203">On hello home page, click on **+** tooadd hello users.</span></span>

    ![Çalışanı ekleyin](./media/active-directory-saas-tyeexpress-tutorial/tye-usershome.png)

4. <span data-ttu-id="1aa6e-205">Merhaba formunda sorular gibi tüm hello zorunlu ayrıntılarını girin ve hello Kaydet düğmesine toosave hello Ayrıntılar'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-205">Enter all hello mandatory details as asked in hello form and click hello save button toosave hello details.</span></span>

    ![Çalışanı ekleyin](./media/active-directory-saas-tyeexpress-tutorial/tye-usersadd.png)

    ![Çalışanı ekleyin](./media/active-directory-saas-tyeexpress-tutorial/tye-userssave.png)


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1aa6e-208">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="1aa6e-208">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1aa6e-209">Bu bölümde, kendi erişim Systems & E Express vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-209">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooT&E Express.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="1aa6e-211">**tooassign Britta Simon Systems & E Express, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="1aa6e-211">**tooassign Britta Simon tooT&E Express, perform hello following steps:**</span></span>

1. <span data-ttu-id="1aa6e-212">Hello uygulamaları görünümü, Hello Azure Yönetim Portalı'nda açın ve ardından toohello dizin görünümüne gidin ve çok gidin**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-212">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="1aa6e-214">Merhaba uygulamalar listesinde **T & E Express**.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-214">In hello applications list, select **T&E Express**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_app.png) 

3. <span data-ttu-id="1aa6e-216">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-216">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="1aa6e-218">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-218">Click **Add** button.</span></span> <span data-ttu-id="1aa6e-219">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="1aa6e-221">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-221">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1aa6e-222">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1aa6e-223">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1aa6e-224">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="1aa6e-224">Testing single sign-on</span></span>

<span data-ttu-id="1aa6e-225">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1aa6e-226">Merhaba T & hello erişim paneli E Express parçasında tıkladığınızda, otomatik olarak oturum açma tooyour T & E Express uygulaması almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1aa6e-226">When you click hello T&E Express tile in hello Access Panel, you should get automatically signed-on tooyour T&E Express application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1aa6e-227">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="1aa6e-227">Additional resources</span></span>

* [<span data-ttu-id="1aa6e-228">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="1aa6e-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1aa6e-229">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="1aa6e-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_203.png

