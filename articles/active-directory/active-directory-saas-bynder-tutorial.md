---
title: "Öğretici: Azure Active Directory Tümleştirme ile Bynder | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Bynder arasında."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 4fb0ab26-b3b9-420a-8072-a0be80ea021e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: a2a8477580d28fe422f2836f483dff286bc71c93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bynder"></a><span data-ttu-id="884b9-103">Öğretici: Azure Active Directory Tümleştirme Bynder ile</span><span class="sxs-lookup"><span data-stu-id="884b9-103">Tutorial: Azure Active Directory integration with Bynder</span></span>
<span data-ttu-id="884b9-104">Bu öğreticinin Hello hedefi olan tooshow, nasıl toointegrate Bynder Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="884b9-104">hello objective of this tutorial is tooshow you how toointegrate Bynder with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="884b9-105">Bynder Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="884b9-105">Integrating Bynder with Azure AD provides you with hello following benefits:</span></span>

* <span data-ttu-id="884b9-106">Erişim tooBynder sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="884b9-106">You can control in Azure AD who has access tooBynder</span></span>
* <span data-ttu-id="884b9-107">Kullanıcıların tooautomatically get açan tooBynder çoklu oturum açma (SSO) ile Azure AD hesaplarına etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="884b9-107">You can enable your users tooautomatically get signed-on tooBynder single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="884b9-108">Hesaplarınızı bir merkezi konumda - hello Klasik Azure portalı Yönet</span><span class="sxs-lookup"><span data-stu-id="884b9-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="884b9-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="884b9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="884b9-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="884b9-110">Prerequisites</span></span>
<span data-ttu-id="884b9-111">tooconfigure Bynder ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="884b9-111">tooconfigure Azure AD integration with Bynder, you need hello following items:</span></span>

* <span data-ttu-id="884b9-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="884b9-112">An Azure AD subscription</span></span>
* <span data-ttu-id="884b9-113">Abonelik bir Bynder çoklu oturum açma (SSO) etkin</span><span class="sxs-lookup"><span data-stu-id="884b9-113">A Bynder single-sign on (SSO) enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="884b9-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="884b9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="884b9-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="884b9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="884b9-116">Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="884b9-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="884b9-117">Bir Azure AD deneme ortam yoksa, alabileceğiniz bir [bir aylık deneme](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="884b9-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="884b9-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="884b9-118">Scenario description</span></span>
<span data-ttu-id="884b9-119">Bu öğreticinin Hello hedefi olan tooenable, tootest Microsoft Azure AD SSO bir sınama ortamında.</span><span class="sxs-lookup"><span data-stu-id="884b9-119">hello objective of this tutorial is tooenable you tootest Microsoft Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="884b9-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="884b9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="884b9-121">Merhaba Galerisi'nden Bynder ekleme</span><span class="sxs-lookup"><span data-stu-id="884b9-121">Adding Bynder from hello gallery</span></span>
2. <span data-ttu-id="884b9-122">Yapılandırma ve Microsoft Azure AD SSO test etme</span><span class="sxs-lookup"><span data-stu-id="884b9-122">Configuring and testing Microsoft Azure AD SSO</span></span>

## <a name="add-bynder-from-hello-gallery"></a><span data-ttu-id="884b9-123">Merhaba Galerisi'nden Bynder ekleme</span><span class="sxs-lookup"><span data-stu-id="884b9-123">Add Bynder from hello gallery</span></span>
<span data-ttu-id="884b9-124">Azure AD'ye tooconfigure hello tümleştirme Bynder, tooadd Bynder hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="884b9-124">tooconfigure hello integration of Bynder into Azure AD, you need tooadd Bynder from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="884b9-125">**tooadd Bynder hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="884b9-125">**tooadd Bynder from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="884b9-126">Merhaba, **Klasik Azure portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="884b9-126">In hello **Azure classic Portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="884b9-128">Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.</span><span class="sxs-lookup"><span data-stu-id="884b9-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="884b9-129">Merhaba dizin görünümünde tooopen hello uygulamaları Görüntüle'yi tıklatın **uygulamaları** hello üst menüde.</span><span class="sxs-lookup"><span data-stu-id="884b9-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Uygulamalar][2]
4. <span data-ttu-id="884b9-131">Tıklatın **Ekle** hello sayfanın hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="884b9-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Uygulamalar][3]
5. <span data-ttu-id="884b9-133">Merhaba üzerinde **neler toodo istediğiniz** iletişim kutusunda, tıklatın **hello Galeriden bir uygulama eklemek**.</span><span class="sxs-lookup"><span data-stu-id="884b9-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Uygulamalar][4]
6. <span data-ttu-id="884b9-135">Merhaba arama kutusuna yazın **Bynder**.</span><span class="sxs-lookup"><span data-stu-id="884b9-135">In hello search box, type **Bynder**.</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_01.png)
7. <span data-ttu-id="884b9-137">Merhaba Sonuçlar panelinde seçin **Bynder**ve ardından **tam** tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="884b9-137">In hello results panel, select **Bynder**, and then click **Complete** tooadd hello application.</span></span>
   
    ![Merhaba Galerisi'nde Hello uygulama seçme](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_001.png)

## <a name="configure-and-test-microsoft-azure-ad-sso"></a><span data-ttu-id="884b9-139">Yapılandırma ve Microsoft Azure AD SSO test etme</span><span class="sxs-lookup"><span data-stu-id="884b9-139">Configure and test Microsoft Azure AD SSO</span></span>
<span data-ttu-id="884b9-140">Bu bölümde Hello amacı olan tooshow nasıl tooconfigure ve test Bynder ile Microsoft Azure AD SSO temel alarak "Britta Simon" adlı bir test kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="884b9-140">hello objective of this section is tooshow you how tooconfigure and test Microsoft Azure AD SSO with Bynder based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="884b9-141">SSO toowork için Azure AD hangi hello karşılık gelen kullanıcı Bynder tooan kullanıcı Azure AD'de tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="884b9-141">For SSO toowork, Azure AD needs tooknow what hello counterpart user in Bynder tooan user in Azure AD is.</span></span> <span data-ttu-id="884b9-142">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Bynder hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="884b9-142">In other words, a link relationship between an Azure AD user and hello related user in Bynder needs toobe established.</span></span>

<span data-ttu-id="884b9-143">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** Bynder içinde.</span><span class="sxs-lookup"><span data-stu-id="884b9-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Bynder.</span></span>

<span data-ttu-id="884b9-144">tooconfigure ve Microsoft Azure AD Bynder SSO'su test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="884b9-144">tooconfigure and test Microsoft Azure AD SSO with Bynder, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="884b9-145">**[Microsoft Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="884b9-145">**[Configuring Microsoft Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="884b9-146">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -Microsoft Azure AD çoklu oturum açma Britta Simon ile tootest.</span><span class="sxs-lookup"><span data-stu-id="884b9-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Microsoft Azure AD Single Sign-On with Britta Simon.</span></span>
3. <span data-ttu-id="884b9-147">**[Bynder test kullanıcısı oluşturma](#creating-a-bynder-test-user)**  -toohave karşılık gelen her bağlantılı toohello Azure AD gösterimidir Bynder içinde Britta Simon biri.</span><span class="sxs-lookup"><span data-stu-id="884b9-147">**[Creating a Bynder test user](#creating-a-bynder-test-user)** - toohave a counterpart of Britta Simon in Bynder that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="884b9-148">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Microsoft Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="884b9-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Microsoft Azure AD Single Sign-On.</span></span>
5. <span data-ttu-id="884b9-149">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="884b9-149">**[Testing single sign-on](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-microsoft-azure-ad-sso"></a><span data-ttu-id="884b9-150">Microsoft Azure AD SSO yapılandırma</span><span class="sxs-lookup"><span data-stu-id="884b9-150">Configuring Microsoft Azure AD SSO</span></span>
<span data-ttu-id="884b9-151">Bu bölümde, Microsoft Azure AD SSO hello Klasik portalında etkinleştirin ve SSO Bynder uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="884b9-151">In this section, you enable Microsoft Azure AD SSO in hello classic portal and configure SSO in your Bynder application.</span></span>

<span data-ttu-id="884b9-152">**tooconfigure Bynder, Microsoft Azure AD SSO'su hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="884b9-152">**tooconfigure Microsoft Azure AD SSO with Bynder, perform hello following steps:**</span></span>

1. <span data-ttu-id="884b9-153">Merhaba üzerinde hello Klasik Portalı'nda **Bynder** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma özelliğini yapılandırın** tooopen hello **yapılandırma çoklu oturum açma** iletişim.</span><span class="sxs-lookup"><span data-stu-id="884b9-153">In hello classic portal, on hello **Bynder** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın][6] 
2. <span data-ttu-id="884b9-155">Merhaba üzerinde **nasıl tooBynder üzerinde kullanıcılar toosign gibi yaptığınız** sayfasında, **Microsoft Azure AD çoklu oturum açma**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="884b9-155">On hello **How would you like users toosign on tooBynder** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_03.png)
3. <span data-ttu-id="884b9-157">Merhaba üzerinde **uygulama ayarlarını yapılandır** tooconfigure hello uygulamada istiyorsanız iletişim sayfasında, **IDP başlatılan modu**, hello aşağıdaki adımları gerçekleştirin ve tıklayın **sonraki**:</span><span class="sxs-lookup"><span data-stu-id="884b9-157">On hello **Configure App Settings** dialog page, If you wish tooconfigure hello application in **IDP initiated mode**, perform hello following steps and click **Next**:</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_04.png)
  1. <span data-ttu-id="884b9-159">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<company name>.getbynder.com/sso/SAML/authenticate/`</span><span class="sxs-lookup"><span data-stu-id="884b9-159">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.getbynder.com/sso/SAML/authenticate/`</span></span>
  2. <span data-ttu-id="884b9-160">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="884b9-160">Click **Next**.</span></span>
4. <span data-ttu-id="884b9-161">Tooconfigure hello uygulamada istiyorsanız **SP tarafından başlatılan modu** hello üzerinde **uygulama ayarlarını yapılandır** iletişim sayfa sonra hello tıklatıldığında **"Göster Gelişmiş ayarları (isteğe bağlı)"**ve hello enter **oturum üzerinde URL'si** tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="884b9-161">If you wish tooconfigure hello application in **SP initiated mode** on hello **Configure App Settings** dialog page, then click on hello **“Show advanced settings (optional)”** and then enter hello **Sign On URL** and click **Next**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_10.png)
  1. <span data-ttu-id="884b9-163">Merhaba, **oturum üzerinde URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<company name>.getbynder.com/login/`</span><span class="sxs-lookup"><span data-stu-id="884b9-163">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://<company name>.getbynder.com/login/`</span></span>
  2. <span data-ttu-id="884b9-164">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="884b9-164">Click **Next**.</span></span>
  
   >[!NOTE]
   ><span data-ttu-id="884b9-165">Merhaba hello oturum üzerinde URL'si Bu öğreticide yalnızca bir placeholfer değeridir.</span><span class="sxs-lookup"><span data-stu-id="884b9-165">hello value for hello Sign On URL in this tutorial is just a placeholfer.</span></span> <span data-ttu-id="884b9-166">tooget hello gerçek vlaue, ortamınız için Bynder başvurun.</span><span class="sxs-lookup"><span data-stu-id="884b9-166">tooget hello actual vlaue for your environment, contact Bynder.</span></span>
   >

5. <span data-ttu-id="884b9-167">Merhaba üzerinde **çoklu oturum açma sırasında Bynder yapılandırma** sayfasında hello aşağıdaki adımları gerçekleştirin ve tıklayın **sonraki**:</span><span class="sxs-lookup"><span data-stu-id="884b9-167">On hello **Configure single sign-on at Bynder** page, perform hello following steps and click **Next**:</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_05.png)  
  1. <span data-ttu-id="884b9-169">Tıklatın **karşıdan meta veri**ve ardından hello dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="884b9-169">Click **Download metadata**, and then save hello file on your computer.</span></span>
  2. <span data-ttu-id="884b9-170">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="884b9-170">Click **Next**.</span></span>
6. <span data-ttu-id="884b9-171">Uygulamanız için yapılandırılmış SSO tooget Bynder destek ekibinize başvurun.</span><span class="sxs-lookup"><span data-stu-id="884b9-171">tooget SSO configured for your application, contact your Bynder support team.</span></span> <span data-ttu-id="884b9-172">Hello indirilen meta veri dosyası ekleme ve bunların tarafında SSO yukarı Bynder takım tooset ile paylaşın.</span><span class="sxs-lookup"><span data-stu-id="884b9-172">Attach hello downloaded metadata file and share it with Bynder team tooset up SSO on their side.</span></span>
7. <span data-ttu-id="884b9-173">Merhaba Klasik portalında hello tek oturum açma yapılandırması onay seçin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="884b9-173">In hello classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD çoklu oturum açma][10]
8. <span data-ttu-id="884b9-175">Merhaba üzerinde **tek oturum açma onay** sayfasında, **tam**.</span><span class="sxs-lookup"><span data-stu-id="884b9-175">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD çoklu oturum açma][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="884b9-177">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="884b9-177">Create an Azure AD test user</span></span>
<span data-ttu-id="884b9-178">Bu bölümde Hello amacı toocreate bir test kullanıcısı Britta Simon adlı hello Klasik Portalı'nda ' dir.</span><span class="sxs-lookup"><span data-stu-id="884b9-178">hello objective of this section is toocreate a test user in hello classic portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][20]

<span data-ttu-id="884b9-180">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="884b9-180">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="884b9-181">Merhaba, **Klasik Azure portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="884b9-181">In hello **Azure classic Portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bynder-tutorial/create_aaduser_09.png)
2. <span data-ttu-id="884b9-183">Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.</span><span class="sxs-lookup"><span data-stu-id="884b9-183">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="884b9-184">toodisplay hello hello üstte hello menüde kullanıcıların listesini tıklatın **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="884b9-184">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bynder-tutorial/create_aaduser_03.png)
4. <span data-ttu-id="884b9-186">tooopen hello **Kullanıcı Ekle** hello araç çubuğunda hello altta iletişim tıklatın **Kullanıcı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="884b9-186">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bynder-tutorial/create_aaduser_04.png)
5. <span data-ttu-id="884b9-188">Merhaba üzerinde **bu kullanıcı hakkında bize** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="884b9-188">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bynder-tutorial/create_aaduser_05.png)
  1. <span data-ttu-id="884b9-190">Kullanıcı türü olarak, kuruluşunuzdaki yeni kullanıcı seçin.</span><span class="sxs-lookup"><span data-stu-id="884b9-190">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="884b9-191">Merhaba kullanıcı adı olarak **textbox**, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="884b9-191">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="884b9-192">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="884b9-192">Click **Next**.</span></span>
6. <span data-ttu-id="884b9-193">Merhaba üzerinde **kullanıcı profili** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="884b9-193">On hello **User Profile** dialog page, perform hello following steps:</span></span>
   
   ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bynder-tutorial/create_aaduser_06.png)
  1. <span data-ttu-id="884b9-195">Merhaba, **ad** metin kutusuna, türü **Britta**.</span><span class="sxs-lookup"><span data-stu-id="884b9-195">In hello **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="884b9-196">Merhaba, **Soyadı** metin kutusuna, türü, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="884b9-196">In hello **Last Name** textbox, type, **Simon**.</span></span> 
  3. <span data-ttu-id="884b9-197">Merhaba, **görünen adı** metin kutusuna, türü **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="884b9-197">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="884b9-198">Merhaba, **rol** listesinde **kullanıcı**.</span><span class="sxs-lookup"><span data-stu-id="884b9-198">In hello **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="884b9-199">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="884b9-199">Click **Next**.</span></span>
7. <span data-ttu-id="884b9-200">Merhaba üzerinde **Get geçici parola** iletişim sayfasında, tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="884b9-200">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bynder-tutorial/create_aaduser_07.png)
8. <span data-ttu-id="884b9-202">Merhaba üzerinde **Get geçici parola** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="884b9-202">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bynder-tutorial/create_aaduser_08.png)
   1. <span data-ttu-id="884b9-204">Merhaba Hello değerini yazmak **yeni parola**.</span><span class="sxs-lookup"><span data-stu-id="884b9-204">Write down hello value of hello **New Password**.</span></span>
   2. <span data-ttu-id="884b9-205">**Tamamla**’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="884b9-205">Click **Complete**.</span></span>   

### <a name="create-a-bynder-test-user"></a><span data-ttu-id="884b9-206">Bynder test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="884b9-206">Create a Bynder test user</span></span>
<span data-ttu-id="884b9-207">Bu bölümde Hello amacı toocreate Britta Simon içinde Bynder adlı bir kullanıcı ' dir.</span><span class="sxs-lookup"><span data-stu-id="884b9-207">hello objective of this section is toocreate a user called Britta Simon in Bynder.</span></span> <span data-ttu-id="884b9-208">Bynder yalnızca zaman sağlama, varsayılan olarak etkin olduğu destekler.</span><span class="sxs-lookup"><span data-stu-id="884b9-208">Bynder supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="884b9-209">Bu bölümde, eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="884b9-209">There is no action item for you in this section.</span></span> <span data-ttu-id="884b9-210">Henüz yoksa yeni bir kullanıcı bir girişim tooaccess Bynder sırasında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="884b9-210">A new user will be created during an attempt tooaccess Bynder if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="884b9-211">Bir kullanıcı toocreate el ile gerekiyorsa, toocontact hello Bynder destek ekibi gerekir.</span><span class="sxs-lookup"><span data-stu-id="884b9-211">If you need toocreate an user manually, you need toocontact hello Bynder support team.</span></span> 
> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="884b9-212">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="884b9-212">Assign hello Azure AD test user</span></span>
<span data-ttu-id="884b9-213">Bu bölümde Hello amacı her erişim tooBynder vererek tooenabling Britta Simon toouse Azure SSO olur.</span><span class="sxs-lookup"><span data-stu-id="884b9-213">hello objective of this section is tooenabling Britta Simon toouse Azure SSO by granting her access tooBynder.</span></span>

   ![Kullanıcı atama][200]

<span data-ttu-id="884b9-215">**tooassign Britta Simon tooBynder hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="884b9-215">**tooassign Britta Simon tooBynder, perform hello following steps:**</span></span>

1. <span data-ttu-id="884b9-216">Merhaba Klasik portalında hello dizin görünümünde tooopen hello uygulamaları Görüntüle'yi tıklatın **uygulamaları** hello üst menüde.</span><span class="sxs-lookup"><span data-stu-id="884b9-216">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Kullanıcı atama][201]
2. <span data-ttu-id="884b9-218">Merhaba uygulamalar listesinde **Bynder**.</span><span class="sxs-lookup"><span data-stu-id="884b9-218">In hello applications list, select **Bynder**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_50.png)
3. <span data-ttu-id="884b9-220">Hello içinde hello üst menüsünde **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="884b9-220">In hello menu on hello top, click **Users**.</span></span>
   
    ![Kullanıcı atama][203]
4. <span data-ttu-id="884b9-222">Merhaba kullanıcılar listesinden seçin **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="884b9-222">In hello Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="884b9-223">Merhaba altta Hello araç çubuğunda **atamak**.</span><span class="sxs-lookup"><span data-stu-id="884b9-223">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Kullanıcı atama][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="884b9-225">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="884b9-225">Test single sign-on</span></span>
<span data-ttu-id="884b9-226">Bu bölümde Hello amacı olan tootest hello erişim paneli Microsoft Azure AD SSO kullanarak yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="884b9-226">hello objective of this section is tootest your Microsoft Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="884b9-227">Merhaba Bynder hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Bynder uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="884b9-227">When you click hello Bynder tile in hello Access Panel, you should get automatically signed-on tooyour Bynder application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="884b9-228">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="884b9-228">Additional resources</span></span>
* [<span data-ttu-id="884b9-229">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="884b9-229">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="884b9-230">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="884b9-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_205.png
