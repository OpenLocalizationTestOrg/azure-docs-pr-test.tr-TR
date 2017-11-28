---
title: "Öğretici: Azure Active Directory Tümleştirme ile Teamphoria | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Teamphoria arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d569c705-6f0f-4ec1-b485-ba82526b5d32
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jeedes
ms.openlocfilehash: f32be9742b76f7fe464036dadc108c62e4a787a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamphoria"></a><span data-ttu-id="de7ef-103">Öğretici: Azure Active Directory Tümleştirme Teamphoria ile</span><span class="sxs-lookup"><span data-stu-id="de7ef-103">Tutorial: Azure Active Directory integration with Teamphoria</span></span>

<span data-ttu-id="de7ef-104">Bu öğreticide, bilgi nasıl toointegrate Teamphoria Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="de7ef-104">In this tutorial, you learn how toointegrate Teamphoria with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="de7ef-105">Teamphoria Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="de7ef-105">Integrating Teamphoria with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="de7ef-106">Erişim tooTeamphoria sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="de7ef-106">You can control in Azure AD who has access tooTeamphoria</span></span>
- <span data-ttu-id="de7ef-107">Kullanıcıların tooautomatically get açan tooTeamphoria (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="de7ef-107">You can enable your users tooautomatically get signed-on tooTeamphoria (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="de7ef-108">Bir merkezi konumda - hello Azure Yönetim Portalı hesaplarınızı yönetebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="de7ef-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="de7ef-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="de7ef-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

tooenable single sign-on with Teamphoria, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Teamphoria.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="de7ef-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="de7ef-110">Prerequisites</span></span>

<span data-ttu-id="de7ef-111">tooconfigure Teamphoria ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="de7ef-111">tooconfigure Azure AD integration with Teamphoria, you need hello following items:</span></span>

- <span data-ttu-id="de7ef-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="de7ef-112">An Azure AD subscription</span></span>
- <span data-ttu-id="de7ef-113">Bir Teamphoria çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="de7ef-113">A Teamphoria single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="de7ef-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="de7ef-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="de7ef-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="de7ef-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="de7ef-116">Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="de7ef-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="de7ef-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="de7ef-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="de7ef-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="de7ef-118">Scenario description</span></span>
<span data-ttu-id="de7ef-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="de7ef-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="de7ef-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="de7ef-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="de7ef-121">Merhaba Galerisi'nden Teamphoria ekleme</span><span class="sxs-lookup"><span data-stu-id="de7ef-121">Adding Teamphoria from hello gallery</span></span>
2. <span data-ttu-id="de7ef-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="de7ef-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-teamphoria-from-hello-gallery"></a><span data-ttu-id="de7ef-123">Merhaba Galerisi'nden Teamphoria ekleme</span><span class="sxs-lookup"><span data-stu-id="de7ef-123">Adding Teamphoria from hello gallery</span></span>
<span data-ttu-id="de7ef-124">Azure AD'ye tooconfigure hello tümleştirme Teamphoria, tooadd Teamphoria hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="de7ef-124">tooconfigure hello integration of Teamphoria into Azure AD, you need tooadd Teamphoria from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="de7ef-125">**tooadd Teamphoria hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="de7ef-125">**tooadd Teamphoria from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="de7ef-126">Merhaba,  **[Azure Yönetim Portalı](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="de7ef-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="de7ef-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="de7ef-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="de7ef-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="de7ef-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="de7ef-131">Tıklatın **Ekle** hello iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="de7ef-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="de7ef-133">Merhaba arama kutusuna yazın **Teamphoria**.</span><span class="sxs-lookup"><span data-stu-id="de7ef-133">In hello search box, type **Teamphoria**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_search.png)

5. <span data-ttu-id="de7ef-135">Merhaba Sonuçlar panelinde seçin **Teamphoria**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="de7ef-135">In hello results panel, select **Teamphoria**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="de7ef-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="de7ef-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="de7ef-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Teamphoria sınayın.</span><span class="sxs-lookup"><span data-stu-id="de7ef-138">In this section, you configure and test Azure AD single sign-on with Teamphoria based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="de7ef-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Teamphoria içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="de7ef-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Teamphoria is tooa user in Azure AD.</span></span> <span data-ttu-id="de7ef-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Teamphoria hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="de7ef-140">In other words, a link relationship between an Azure AD user and hello related user in Teamphoria needs toobe established.</span></span>

<span data-ttu-id="de7ef-141">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** Teamphoria içinde.</span><span class="sxs-lookup"><span data-stu-id="de7ef-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Teamphoria.</span></span>

<span data-ttu-id="de7ef-142">tooconfigure ve Teamphoria ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="de7ef-142">tooconfigure and test Azure AD single sign-on with Teamphoria, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="de7ef-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="de7ef-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="de7ef-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="de7ef-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="de7ef-145">**[Teamphoria test kullanıcısı oluşturma](#creating-a-teamphoria-test-user)**  -toohave karşılık gelen her bağlantılı toohello Azure AD gösterimidir Teamphoria içinde Britta Simon biri.</span><span class="sxs-lookup"><span data-stu-id="de7ef-145">**[Creating a Teamphoria test user](#creating-a-teamphoria-test-user)** - toohave a counterpart of Britta Simon in Teamphoria that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="de7ef-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="de7ef-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="de7ef-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="de7ef-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="de7ef-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="de7ef-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="de7ef-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure Yönetim Portalı'nda etkinleştirin ve çoklu oturum açma Teamphoria uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="de7ef-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Teamphoria application.</span></span>

<span data-ttu-id="de7ef-150">**tooconfigure Azure AD çoklu oturum açma ile Teamphoria, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="de7ef-150">**tooconfigure Azure AD single sign-on with Teamphoria, perform hello following steps:**</span></span>

1. <span data-ttu-id="de7ef-151">Merhaba üzerinde hello Azure Yönetim Portalı'nda **Teamphoria** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="de7ef-151">In hello Azure Management portal, on hello **Teamphoria** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="de7ef-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda, olarak **modu** seçin **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="de7ef-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_samlbase.png)

3. <span data-ttu-id="de7ef-155">Merhaba üzerinde **Teamphoria etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="de7ef-155">On hello **Teamphoria Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_url.png)

    <span data-ttu-id="de7ef-157">a.</span><span class="sxs-lookup"><span data-stu-id="de7ef-157">a.</span></span> <span data-ttu-id="de7ef-158">Merhaba, **oturum açma URL'si** metin kutusuna, desen aşağıdaki hello kullanarak türü hello URL'si:`https://<sub-domain>.teamphoria.com/login`</span><span class="sxs-lookup"><span data-stu-id="de7ef-158">In hello **Sign-on URL** textbox, type hello URL using hello following pattern: `https://<sub-domain>.teamphoria.com/login`</span></span>  

    > [!NOTE] 
    > <span data-ttu-id="de7ef-159">Lütfen bu hello gerçek değerler olmadığına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="de7ef-159">Please note that these are not hello real values.</span></span> <span data-ttu-id="de7ef-160">Tooupdate hello ile bu değerlere sahip gerçek oturum açma URL'si.</span><span class="sxs-lookup"><span data-stu-id="de7ef-160">You have tooupdate these values with hello actual Sign-On URL.</span></span> <span data-ttu-id="de7ef-161">Kişi [Teamphoria istemci destek ekibi](https://www.teamphoria.com/) tooget hello oturum açma URL'si.</span><span class="sxs-lookup"><span data-stu-id="de7ef-161">Contact [Teamphoria Client support team](https://www.teamphoria.com/) tooget hello Sign-on URL.</span></span> 

4. <span data-ttu-id="de7ef-162">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="de7ef-162">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_certificate.png) 

5. <span data-ttu-id="de7ef-164">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="de7ef-164">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-teamphoria-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="de7ef-166">Merhaba üzerinde **Teamphoria yapılandırma** 'yi tıklatın **yapılandırma Teamphoria** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="de7ef-166">On hello **Teamphoria Configuration** section, click **Configure Teamphoria** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="de7ef-167">Kopya hello **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="de7ef-167">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_configure.png) 

7. <span data-ttu-id="de7ef-169">tooconfigure çoklu oturum açma üzerinde **Teamphoria** tarafı, yönetici olarak oturum açma tooyour Teamphoria uygulama.</span><span class="sxs-lookup"><span data-stu-id="de7ef-169">tooconfigure single sign-on on **Teamphoria** side, Login tooyour Teamphoria application as an administrator.</span></span>

8. <span data-ttu-id="de7ef-170">Çok Git**yönetici ayarları** seçeneği hello sol araç ve yapılandırma sekmesini üzerinde hello hello altında **tek oturum açma** tooopen hello SSO yapılandırma penceresi.</span><span class="sxs-lookup"><span data-stu-id="de7ef-170">Go too**ADMIN SETTINGS** option in hello left toolbar and under hello hello Configure Tab click on **SINGLE SIGN-ON** tooopen hello SSO configuration window.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-teamphoria-tutorial/admin_sso_configure.png)

9. <span data-ttu-id="de7ef-172">Tıklayın **yeni kimlik sağlayıcı Ekle** hello sağ üst köşedeki tooopen hello formunda SSO hello ayarlarını ekleme seçeneği.</span><span class="sxs-lookup"><span data-stu-id="de7ef-172">Click on **ADD NEW IDENTITY PROVIDER** option in hello top right corner tooopen hello form for adding hello settings for SSO.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-teamphoria-tutorial/add_new_identity_provider.png)

10. <span data-ttu-id="de7ef-174">Aşağıdaki - açıklandığı gibi hello alanlarında Hello ayrıntılarını girin</span><span class="sxs-lookup"><span data-stu-id="de7ef-174">Enter hello details in hello fields as described below-</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-teamphoria-tutorial/Teamphoria_sso_save.png)

    <span data-ttu-id="de7ef-176">a.</span><span class="sxs-lookup"><span data-stu-id="de7ef-176">a.</span></span> <span data-ttu-id="de7ef-177">**GÖRÜNEN adı** : hello Yönetim sayfasında hello eklentisi hello görünen adını girin.</span><span class="sxs-lookup"><span data-stu-id="de7ef-177">**DISPLAY NAME** : Enter hello display name of hello plugin on hello admin page.</span></span>

    <span data-ttu-id="de7ef-178">b.</span><span class="sxs-lookup"><span data-stu-id="de7ef-178">b.</span></span> <span data-ttu-id="de7ef-179">**DÜĞME adı** : SSO oturum açmayı için hello oturum açma sayfasında görüntüler hello sekmesini hello adı.</span><span class="sxs-lookup"><span data-stu-id="de7ef-179">**BUTTON NAME** : hello name of hello tab which will display on hello login page for logging in via SSO.</span></span>

    <span data-ttu-id="de7ef-180">c.</span><span class="sxs-lookup"><span data-stu-id="de7ef-180">c.</span></span> <span data-ttu-id="de7ef-181">**Sertifika** : açık hello sertifika önceki hello Not Defteri'nde, kopyalama Merhaba içeriğine hello Azure portalı aynı indirdiğiniz ve buraya hello kutusuna yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="de7ef-181">**CERTIFICATE** : Open hello Certificate downloaded earlier from hello Azure portal in notepad, copy hello contents of hello same and paste it here in hello box.</span></span>

    <span data-ttu-id="de7ef-182">d.</span><span class="sxs-lookup"><span data-stu-id="de7ef-182">d.</span></span> <span data-ttu-id="de7ef-183">**Giriş noktası** : Yapıştır hello **SAML çoklu oturum açma hizmet URL'si** önceki form hello Azure portal kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="de7ef-183">**ENTRY POINT** : Paste hello **SAML Single Sign-On Service URL** copied earlier form hello Azure portal.</span></span>

    <span data-ttu-id="de7ef-184">e.</span><span class="sxs-lookup"><span data-stu-id="de7ef-184">e.</span></span> <span data-ttu-id="de7ef-185">Merhaba seçeneği çok geçiş**ON** ve tıklayın **KAYDETMEK**.</span><span class="sxs-lookup"><span data-stu-id="de7ef-185">Switch hello option too**ON** and click on **SAVE**.</span></span> 

<!--### Next steps

tooensure users can sign-in tooTeamphoria after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Teamphoria prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooTeamphoria in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Teamphoria users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="de7ef-186">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="de7ef-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="de7ef-187">Bu bölümde Hello amacı toocreate Britta Simon adlı hello Azure Yönetim Portalı'nda bir sınama kullanıcısı ' dir.</span><span class="sxs-lookup"><span data-stu-id="de7ef-187">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="de7ef-189">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="de7ef-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="de7ef-190">Merhaba, **Azure Yönetim Portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="de7ef-190">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="de7ef-192">Çok Git**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar** toodisplay hello kullanıcılar listesi.</span><span class="sxs-lookup"><span data-stu-id="de7ef-192">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="de7ef-194">Merhaba hello iletişim üstündeki **Ekle** tooopen hello **kullanıcı** iletişim.</span><span class="sxs-lookup"><span data-stu-id="de7ef-194">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="de7ef-196">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="de7ef-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="de7ef-198">a.</span><span class="sxs-lookup"><span data-stu-id="de7ef-198">a.</span></span> <span data-ttu-id="de7ef-199">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="de7ef-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="de7ef-200">b.</span><span class="sxs-lookup"><span data-stu-id="de7ef-200">b.</span></span> <span data-ttu-id="de7ef-201">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="de7ef-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="de7ef-202">c.</span><span class="sxs-lookup"><span data-stu-id="de7ef-202">c.</span></span> <span data-ttu-id="de7ef-203">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="de7ef-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="de7ef-204">d.</span><span class="sxs-lookup"><span data-stu-id="de7ef-204">d.</span></span> <span data-ttu-id="de7ef-205">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="de7ef-205">Click **Create**.</span></span>
 
### <a name="creating-a-teamphoria-test-user"></a><span data-ttu-id="de7ef-206">Teamphoria test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="de7ef-206">Creating a Teamphoria test user</span></span>

<span data-ttu-id="de7ef-207">Teamphoria içine sipariş tooenable Azure AD kullanıcıların toolog bunların Teamphoria sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="de7ef-207">In order tooenable Azure AD users toolog into Teamphoria, they must be provisioned into Teamphoria.</span></span> <span data-ttu-id="de7ef-208">Teamphoria Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="de7ef-208">In hello case of Teamphoria, provisioning is a manual task.</span></span>

<span data-ttu-id="de7ef-209">**bir kullanıcı hesapları tooprovision gerçekleştirmek hello adımları izleyin:**</span><span class="sxs-lookup"><span data-stu-id="de7ef-209">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="de7ef-210">İçinde tooyour Teamphoria şirket site yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="de7ef-210">Log in tooyour Teamphoria company site as an administrator.</span></span>

2. <span data-ttu-id="de7ef-211">Tıklayın **yönetici** ayarları hello sol araç çubuğunda ve hello altında **Yönet** tıklatın sekmesi **kullanıcılar** tooopen hello Yönetim sayfası kullanıcılar için.</span><span class="sxs-lookup"><span data-stu-id="de7ef-211">Click on **ADMIN** settings on hello left toolbar and under hello **MANAGE** tab Click on **USERS** tooopen hello admin page for users.</span></span>

    ![Çalışanı ekleyin](./media/active-directory-saas-teamphoria-tutorial/admin_manage_users.png)

3. <span data-ttu-id="de7ef-213">Tıklatın hello üzerinde **el ile davet** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="de7ef-213">Click on hello **MANUAL INVITE** option.</span></span>

    ![Kişileri davet edin](./media/active-directory-saas-teamphoria-tutorial/admin_manage_add_users.png)  

4. <span data-ttu-id="de7ef-215">Bu sayfada, eylemi gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="de7ef-215">On this page, perform following action.</span></span> 
    
    ![Kişileri davet edin](./media/active-directory-saas-teamphoria-tutorial/manual_user_invite.png)  

    <span data-ttu-id="de7ef-217">a.</span><span class="sxs-lookup"><span data-stu-id="de7ef-217">a.</span></span> <span data-ttu-id="de7ef-218">Merhaba, **e-posta adresi** metin kutusuna, hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="de7ef-218">In hello **EMAIL ADDRESS** textbox, hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="de7ef-219">b.</span><span class="sxs-lookup"><span data-stu-id="de7ef-219">b.</span></span> <span data-ttu-id="de7ef-220">Merhaba, **ad** metin kutusuna, türü **Britta**.</span><span class="sxs-lookup"><span data-stu-id="de7ef-220">In hello **FIRST NAME** textbox, type **Britta**.</span></span>

    <span data-ttu-id="de7ef-221">c.</span><span class="sxs-lookup"><span data-stu-id="de7ef-221">c.</span></span> <span data-ttu-id="de7ef-222">Merhaba, **SOYADI** metin kutusuna, türü **Simon**.</span><span class="sxs-lookup"><span data-stu-id="de7ef-222">In hello **LAST NAME** textbox, type **Simon**.</span></span>

    <span data-ttu-id="de7ef-223">d.</span><span class="sxs-lookup"><span data-stu-id="de7ef-223">d.</span></span> <span data-ttu-id="de7ef-224">Tıklatın **davet 1 kullanıcı**.</span><span class="sxs-lookup"><span data-stu-id="de7ef-224">Click **INVITE 1 USER**.</span></span> <span data-ttu-id="de7ef-225">Kullanıcı hello sistemde oluşturulan tooaccept hello davet tooget gerekir.</span><span class="sxs-lookup"><span data-stu-id="de7ef-225">User needs tooaccept hello invite tooget created in hello system.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="de7ef-226">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="de7ef-226">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="de7ef-227">Bu bölümde, kendi erişim tooTeamphoria vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="de7ef-227">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooTeamphoria.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="de7ef-229">**tooassign Britta Simon tooTeamphoria hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="de7ef-229">**tooassign Britta Simon tooTeamphoria, perform hello following steps:**</span></span>

1. <span data-ttu-id="de7ef-230">Hello uygulamaları görünümü, Hello Azure Yönetim Portalı'nda açın ve ardından toohello dizin görünümüne gidin ve çok gidin**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="de7ef-230">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="de7ef-232">Merhaba uygulamalar listesinde **Teamphoria**.</span><span class="sxs-lookup"><span data-stu-id="de7ef-232">In hello applications list, select **Teamphoria**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_app.png) 

3. <span data-ttu-id="de7ef-234">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="de7ef-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="de7ef-236">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="de7ef-236">Click **Add** button.</span></span> <span data-ttu-id="de7ef-237">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="de7ef-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="de7ef-239">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="de7ef-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="de7ef-240">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="de7ef-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="de7ef-241">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="de7ef-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="de7ef-242">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="de7ef-242">Testing single sign-on</span></span>

<span data-ttu-id="de7ef-243">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="de7ef-243">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="de7ef-244">Çoklu oturum açma ayarlarınızı test etmek isterseniz, erişim paneli açın.</span><span class="sxs-lookup"><span data-stu-id="de7ef-244">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="de7ef-245">Erişim paneli hakkında daha fazla ayrıntı için bkz: [erişim Paneli'ne giriş](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="de7ef-245">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="de7ef-246">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="de7ef-246">Additional resources</span></span>

* [<span data-ttu-id="de7ef-247">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="de7ef-247">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="de7ef-248">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="de7ef-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_203.png

