---
title: "Öğretici: Azure Active Directory Tümleştirme ile ServiceNow | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve ServiceNow ve ServiceNow Express arasında."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 1d8eb99e-8ce5-4ba4-8b54-5c3d9ae573f6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: df6a07dd1aa437198fbdb9d0a04ea14f3a320249
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-servicenow"></a><span data-ttu-id="dfbec-103">Öğretici: ServiceNow Azure Active Directory Tümleştirme</span><span class="sxs-lookup"><span data-stu-id="dfbec-103">Tutorial: Azure Active Directory integration with ServiceNow</span></span>
<span data-ttu-id="dfbec-104">Bu öğreticide, bilgi nasıl toointegrate ServiceNow ve ServiceNow Express Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dfbec-104">In this tutorial, you learn how toointegrate ServiceNow and ServiceNow Express with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dfbec-105">ServiceNow ve ServiceNow Express Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="dfbec-105">Integrating ServiceNow and ServiceNow Express with Azure AD provides you with hello following benefits:</span></span>

* <span data-ttu-id="dfbec-106">Erişim tooServiceNow olan Azure AD ve ServiceNow Express kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="dfbec-106">You can control in Azure AD who has access tooServiceNow and ServiceNow Express</span></span>
* <span data-ttu-id="dfbec-107">Azure AD hesaplarına açan kullanıcıları tooautomatically get tooServiceNow ve ServiceNow Express (çoklu oturum açma) etkinleştir</span><span class="sxs-lookup"><span data-stu-id="dfbec-107">You can enable your users tooautomatically get signed-on tooServiceNow and ServiceNow Express (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="dfbec-108">Hesaplarınızı bir merkezi konumda - hello Klasik Azure portalı Yönet</span><span class="sxs-lookup"><span data-stu-id="dfbec-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="dfbec-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="dfbec-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dfbec-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="dfbec-110">Prerequisites</span></span>
<span data-ttu-id="dfbec-111">Azure AD ile tümleştirme ServiceNow ve ServiceNow Express tooconfigure, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="dfbec-111">tooconfigure Azure AD integration with ServiceNow and ServiceNow Express, you need hello following items:</span></span>

* <span data-ttu-id="dfbec-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="dfbec-112">An Azure AD subscription</span></span>
* <span data-ttu-id="dfbec-113">ServiceNow, örneği veya ServiceNow, Calgary sürüm Kiracı için veya üzeri</span><span class="sxs-lookup"><span data-stu-id="dfbec-113">For ServiceNow, an instance or tenant of ServiceNow, Calgary version or higher</span></span>
* <span data-ttu-id="dfbec-114">ServiceNow Express, ServiceNow Express, Helsinki sürüm örneği için veya üzeri</span><span class="sxs-lookup"><span data-stu-id="dfbec-114">For ServiceNow Express, an instance of ServiceNow Express, Helsinki version or higher</span></span>
* <span data-ttu-id="dfbec-115">Merhaba ServiceNow Kiracı hello olmalıdır [birden çok sağlayıcı tek oturum üzerinde eklentisi](http://wiki.servicenow.com/index.php?title=Multiple_Provider_Single_Sign-On#gsc.tab=0) etkin.</span><span class="sxs-lookup"><span data-stu-id="dfbec-115">hello ServiceNow tenant must have hello [Multiple Provider Single Sign On Plugin](http://wiki.servicenow.com/index.php?title=Multiple_Provider_Single_Sign-On#gsc.tab=0) enabled.</span></span> <span data-ttu-id="dfbec-116">Bu yapılabilir [hizmet isteği göndererek](https://hi.service-now.com).</span><span class="sxs-lookup"><span data-stu-id="dfbec-116">This can be done by [submitting a service request](https://hi.service-now.com).</span></span> 

> [!NOTE]
> <span data-ttu-id="dfbec-117">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="dfbec-117">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="dfbec-118">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="dfbec-118">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="dfbec-119">Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="dfbec-119">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="dfbec-120">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dfbec-120">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dfbec-121">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="dfbec-121">Scenario description</span></span>
<span data-ttu-id="dfbec-122">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="dfbec-122">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dfbec-123">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="dfbec-123">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dfbec-124">ServiceNow hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="dfbec-124">Adding ServiceNow from hello gallery</span></span>
2. <span data-ttu-id="dfbec-125">Çoklu oturum açmayı ServiceNow veya ServiceNow Express için yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="dfbec-125">Configuring and testing Azure AD single sign-on for ServiceNow or ServiceNow Express</span></span>

## <a name="adding-servicenow-from-hello-gallery"></a><span data-ttu-id="dfbec-126">ServiceNow hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="dfbec-126">Adding ServiceNow from hello gallery</span></span>
<span data-ttu-id="dfbec-127">Azure AD'ye tooconfigure hello tümleştirme ServiceNow veya ServiceNow Express tooadd ServiceNow hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="dfbec-127">tooconfigure hello integration of ServiceNow or ServiceNow Express into Azure AD, you need tooadd ServiceNow from hello gallery tooyour list of managed SaaS apps.</span></span> 

<span data-ttu-id="dfbec-128">**tooadd ServiceNow hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="dfbec-128">**tooadd ServiceNow from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="dfbec-129">Merhaba, **Klasik Azure portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="dfbec-129">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="dfbec-131">Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.</span><span class="sxs-lookup"><span data-stu-id="dfbec-131">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="dfbec-132">Merhaba dizin görünümünde tooopen hello uygulamaları Görüntüle'yi tıklatın **uygulamaları** hello üst menüde.</span><span class="sxs-lookup"><span data-stu-id="dfbec-132">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Uygulamalar][2]
4. <span data-ttu-id="dfbec-134">Tıklatın **Ekle** hello sayfanın hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="dfbec-134">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Uygulamalar][3]
5. <span data-ttu-id="dfbec-136">Merhaba üzerinde **neler toodo istediğiniz** iletişim kutusunda, tıklatın **hello Galeriden bir uygulama eklemek**.</span><span class="sxs-lookup"><span data-stu-id="dfbec-136">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Uygulamalar][4]
6. <span data-ttu-id="dfbec-138">Merhaba arama kutusuna yazın **ServiceNow**.</span><span class="sxs-lookup"><span data-stu-id="dfbec-138">In hello search box, type **ServiceNow**.</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_01.png)
7. <span data-ttu-id="dfbec-140">Merhaba sonuçlar bölmesinde seçin **ServiceNow**ve ardından **tam** tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="dfbec-140">In hello results pane, select **ServiceNow**, and then click **Complete** tooadd hello application.</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_02.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="dfbec-142">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="dfbec-142">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="dfbec-143">Bu bölümde, yapılandırmanız ve ServiceNow veya ServiceNow Express ile Azure AD çoklu oturum açmayı test "Britta Simon" adlı bir test kullanıcı tabanlı.</span><span class="sxs-lookup"><span data-stu-id="dfbec-143">In this section, you configure and test Azure AD single sign-on with ServiceNow or ServiceNow Express based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="dfbec-144">Tek toowork'ın oturum açma hangi hello karşılık gelen ServiceNow içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="dfbec-144">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ServiceNow is tooa user in Azure AD.</span></span> <span data-ttu-id="dfbec-145">Diğer bir deyişle, bir Azure AD kullanıcısının ve ServiceNow hello ilgili kullanıcı arasındaki bağlantıyı ilişki kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="dfbec-145">In other words, a link relationship between an Azure AD user and hello related user in ServiceNow needs toobe established.</span></span>
<span data-ttu-id="dfbec-146">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** ServiceNow içinde.</span><span class="sxs-lookup"><span data-stu-id="dfbec-146">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ServiceNow.</span></span> <span data-ttu-id="dfbec-147">tooconfigure ve ServiceNow ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="dfbec-147">tooconfigure and test Azure AD single sign-on with ServiceNow, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="dfbec-148">**[Azure AD çoklu oturum açma için ServiceNow yapılandırma](#configuring-azure-ad-single-sign-on-for-servicenow)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="dfbec-148">**[Configuring Azure AD Single Sign-On for ServiceNow](#configuring-azure-ad-single-sign-on-for-servicenow)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="dfbec-149">**[Azure AD çoklu oturum açma için ServiceNow Express yapılandırma](#configuring-azure-ad-single-sign-on-for-servicenow-express)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="dfbec-149">**[Configuring Azure AD Single Sign-On for ServiceNow Express](#configuring-azure-ad-single-sign-on-for-servicenow-express)** - tooenable your users toouse this feature.</span></span>
3. <span data-ttu-id="dfbec-150">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="dfbec-150">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="dfbec-151">**[ServiceNow test kullanıcısı oluşturma](#creating-a-servicenow-test-user)**  -toohave karşılık gelen her bağlantılı toohello Azure AD gösterimidir ServiceNow içinde Britta Simon biri.</span><span class="sxs-lookup"><span data-stu-id="dfbec-151">**[Creating a ServiceNow test user](#creating-a-servicenow-test-user)** - toohave a counterpart of Britta Simon in ServiceNow that is linked toohello Azure AD representation of her.</span></span>
5. <span data-ttu-id="dfbec-152">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="dfbec-152">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
6. <span data-ttu-id="dfbec-153">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="dfbec-153">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

> [!NOTE]
> <span data-ttu-id="dfbec-154">2. adım tooconfigure ServiceNow istiyorsanız atlayın.</span><span class="sxs-lookup"><span data-stu-id="dfbec-154">If you want tooconfigure ServiceNow omit step 2.</span></span> <span data-ttu-id="dfbec-155">Benzer şekilde, tooconfigure istiyorsanız, 1. adım ServiceNow Express atlayın.</span><span class="sxs-lookup"><span data-stu-id="dfbec-155">Likewise, if you want tooconfigure ServiceNow Express omit step 1.</span></span>
> 
> 

### <a name="configuring-azure-ad-single-sign-on-for-servicenow"></a><span data-ttu-id="dfbec-156">Azure AD çoklu oturum açma ServiceNow için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="dfbec-156">Configuring Azure AD Single Sign-On for ServiceNow</span></span>
1. <span data-ttu-id="dfbec-157">Hello Azure AD Klasik portalında, hello **ServiceNow** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma yapılandırmak** tooopen hello **tek oturum yapılandırma üzerinde aktar** iletişim .</span><span class="sxs-lookup"><span data-stu-id="dfbec-157">In hello Azure AD classic portal, on hello **ServiceNow** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="dfbec-158">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-servicenow-tutorial/IC749323.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="dfbec-158">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="dfbec-159">Merhaba üzerinde **nasıl tooServiceNow üzerinde kullanıcılar toosign gibi yaptığınız** sayfasında, **Microsoft Azure AD çoklu oturum açma**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="dfbec-159">On hello **How would you like users toosign on tooServiceNow** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="dfbec-160">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-servicenow-tutorial/IC749324.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="dfbec-160">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configure single sign-on")</span></span>

3. <span data-ttu-id="dfbec-161">Merhaba üzerinde **uygulama ayarlarını yapılandır** sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="dfbec-161">On hello **Configure App Settings** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="dfbec-162">![Uygulama URL'sini Yapılandır](./media/active-directory-saas-servicenow-tutorial/IC769497.png "uygulama URL'sini yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="dfbec-162">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configure app URL")</span></span>
   
    <span data-ttu-id="dfbec-163">a.</span><span class="sxs-lookup"><span data-stu-id="dfbec-163">a.</span></span> <span data-ttu-id="dfbec-164">Merhaba, **üzerinde ServiceNow oturum URL'si** URL'nizi metin kutusuna, türü hello desen aşağıdaki kullanıcıların toosign üzerinde tooyour ServiceNow uygulamanız tarafından kullanılan: `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="dfbec-164">in hello **ServiceNow Sign On URL** textbox, type your URL used by your users toosign-on tooyour ServiceNow application following hello pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="dfbec-165">b.</span><span class="sxs-lookup"><span data-stu-id="dfbec-165">b.</span></span> <span data-ttu-id="dfbec-166">Merhaba, **tanımlayıcısı** URL'nizi metin kutusuna, türü hello desen aşağıdaki kullanıcıların toosign üzerinde tooyour ServiceNow uygulamanız tarafından kullanılan: `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="dfbec-166">In hello **Identifier** textbox,type your URL used by your users toosign-on tooyour ServiceNow application following hello pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="dfbec-167">c.</span><span class="sxs-lookup"><span data-stu-id="dfbec-167">c.</span></span> <span data-ttu-id="dfbec-168">**İleri**’ye tıklayın</span><span class="sxs-lookup"><span data-stu-id="dfbec-168">Click **Next**</span></span>

4. <span data-ttu-id="dfbec-169">toohave Azure AD otomatik olarak ServiceNow SAML tabanlı kimlik doğrulaması için yapılandırma, ServiceNow örneği adı, yönetici kullanıcı adı ve yönetici parolası hello girin **otomatik yapılandır çoklu oturum açma** form ve tıklayın  *Yapılandırma*.</span><span class="sxs-lookup"><span data-stu-id="dfbec-169">toohave Azure AD automatically configure ServiceNow for SAML-based authentication, enter your ServiceNow instance name, admin username, and admin password in hello **Auto configure single sign-on** form and click *Configure*.</span></span> <span data-ttu-id="dfbec-170">Sağlanan bu hello yönetici kullanıcı adı, hello olmalıdır Not **security_admin** ServiceNow içinde bu toowork için atanan rolü.</span><span class="sxs-lookup"><span data-stu-id="dfbec-170">Note that hello admin username provided must have hello **security_admin** role assigned in ServiceNow for this toowork.</span></span> <span data-ttu-id="dfbec-171">Aksi takdirde, toomanually ServiceNow toouse Azure AD SAML kimlik sağlayıcısı yapılandırın, tıklatın **el ile Merhaba uygulaması çoklu oturum açma için yapılandırma**, ardından **sonraki** ve tam hello Aşağıdaki adımlar.</span><span class="sxs-lookup"><span data-stu-id="dfbec-171">Otherwise, toomanually configure ServiceNow toouse Azure AD as a SAML identity provider, click **Manually configure hello application for single sign-on**, then click **Next** and complete hello following steps.</span></span>
   
    <span data-ttu-id="dfbec-172">![Uygulama URL'sini Yapılandır](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "uygulama URL'sini yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="dfbec-172">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configure app URL")</span></span>

5. <span data-ttu-id="dfbec-173">Hello üzerinde **Servicenow'da çoklu oturum açma yapılandırma** sayfasında, **indirme sertifika**, yerel olarak bilgisayarınızda hello sertifika dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="dfbec-173">On hello **Configure single sign-on at ServiceNow** page, click **Download certificate**, save hello certificate file locally on your computer.</span></span>
   
    <span data-ttu-id="dfbec-174">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-servicenow-tutorial/IC749325.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="dfbec-174">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configure single sign-on")</span></span>

6. <span data-ttu-id="dfbec-175">Oturum açma ServiceNow uygulama yönetici olarak tooyour.</span><span class="sxs-lookup"><span data-stu-id="dfbec-175">Sign-on tooyour ServiceNow application as an administrator.</span></span>

7. <span data-ttu-id="dfbec-176">Merhaba etkinleştirme *tümleştirmesi - birden çok sağlayıcı tek oturum açma yükleyicisini* izleyerek eklentisi hello sonraki adımlar:</span><span class="sxs-lookup"><span data-stu-id="dfbec-176">Activate hello *Integration - Multiple Provider Single Sign-On Installer* plugin by following hello next steps:</span></span>
   
    <span data-ttu-id="dfbec-177">a.</span><span class="sxs-lookup"><span data-stu-id="dfbec-177">a.</span></span> <span data-ttu-id="dfbec-178">Merhaba sol tarafında Hello Gezinti Bölmesi'nde çok Git**sistem tanımı** bölümünde ve ardından **eklentileri**.</span><span class="sxs-lookup"><span data-stu-id="dfbec-178">In hello navigation pane on hello left side, go too**System Definition** section and then click **Plugins**.</span></span>
   
    <span data-ttu-id="dfbec-179">![Uygulama URL'sini Yapılandır](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_03.png "eklentisini etkinleştirme")</span><span class="sxs-lookup"><span data-stu-id="dfbec-179">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_03.png "Activate plugin")</span></span>
   
    <span data-ttu-id="dfbec-180">b.</span><span class="sxs-lookup"><span data-stu-id="dfbec-180">b.</span></span> <span data-ttu-id="dfbec-181">Arama *tümleştirmesi - birden çok sağlayıcı tek oturum açma yükleyicisini*.</span><span class="sxs-lookup"><span data-stu-id="dfbec-181">Search for *Integration - Multiple Provider Single Sign-On Installer*.</span></span>
   
    <span data-ttu-id="dfbec-182">![Uygulama URL'sini Yapılandır](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_04.png "eklentisini etkinleştirme")</span><span class="sxs-lookup"><span data-stu-id="dfbec-182">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_04.png "Activate plugin")</span></span>
   
    <span data-ttu-id="dfbec-183">c.</span><span class="sxs-lookup"><span data-stu-id="dfbec-183">c.</span></span> <span data-ttu-id="dfbec-184">Merhaba eklentisi seçin.</span><span class="sxs-lookup"><span data-stu-id="dfbec-184">Select hello plugin.</span></span> <span data-ttu-id="dfbec-185">Rigth tıklayın ve **etkinleştir/yükseltme**.</span><span class="sxs-lookup"><span data-stu-id="dfbec-185">Rigth click and select **Activate/Upgrade**.</span></span>
   
    <span data-ttu-id="dfbec-186">d.</span><span class="sxs-lookup"><span data-stu-id="dfbec-186">d.</span></span> <span data-ttu-id="dfbec-187">Merhaba tıklatın **etkinleştirme** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="dfbec-187">Click hello **Activate** button.</span></span>

8. <span data-ttu-id="dfbec-188">Merhaba Gezinti hello sol taraftaki bölmede **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="dfbec-188">In hello navigation pane on hello left side, click **Properties**.</span></span>  
   
    <span data-ttu-id="dfbec-189">![Uygulama URL'sini Yapılandır](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_06.png "uygulama URL'sini yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="dfbec-189">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_06.png "Configure app URL")</span></span>

9. <span data-ttu-id="dfbec-190">Merhaba üzerinde **birden çok sağlayıcı SSO özelliklerini** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="dfbec-190">On hello **Multiple Provider SSO Properties** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="dfbec-191">![Uygulama URL'sini Yapılandır](./media/active-directory-saas-servicenow-tutorial/IC7694981.png "uygulama URL'sini yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="dfbec-191">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC7694981.png "Configure app URL")</span></span>
   
    <span data-ttu-id="dfbec-192">a.</span><span class="sxs-lookup"><span data-stu-id="dfbec-192">a.</span></span> <span data-ttu-id="dfbec-193">Olarak **birden çok sağlayıcı SSO etkinleştirme**seçin **Evet**.</span><span class="sxs-lookup"><span data-stu-id="dfbec-193">As **Enable multiple provider SSO**, select **Yes**.</span></span>
   
    <span data-ttu-id="dfbec-194">b.</span><span class="sxs-lookup"><span data-stu-id="dfbec-194">b.</span></span> <span data-ttu-id="dfbec-195">Olarak **hata ayıklama günlüğünü var etkinleştir hello birden çok sağlayıcı SSO tümleştirme**seçin **Evet**.</span><span class="sxs-lookup"><span data-stu-id="dfbec-195">As **Enable debug logging got hello multiple provider SSO integration**, select **Yes**.</span></span>
   
    <span data-ttu-id="dfbec-196">c.</span><span class="sxs-lookup"><span data-stu-id="dfbec-196">c.</span></span> <span data-ttu-id="dfbec-197">İçinde **hello alan hello kullanıcı tablo...**  metin kutusuna, türü **user_name**.</span><span class="sxs-lookup"><span data-stu-id="dfbec-197">In **hello field on hello user table that...** textbox, type **user_name**.</span></span>
   
    <span data-ttu-id="dfbec-198">d.</span><span class="sxs-lookup"><span data-stu-id="dfbec-198">d.</span></span> <span data-ttu-id="dfbec-199">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="dfbec-199">Click **Save**.</span></span>

10. <span data-ttu-id="dfbec-200">Merhaba Gezinti hello sol taraftaki bölmede **x509 sertifikaları**.</span><span class="sxs-lookup"><span data-stu-id="dfbec-200">In hello navigation pane on hello left side, click **x509 Certificates**.</span></span>
    
     <span data-ttu-id="dfbec-201">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_05.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="dfbec-201">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_05.png "Configure single sign-on")</span></span>

11. <span data-ttu-id="dfbec-202">Merhaba üzerinde **X.509 sertifikalarını** iletişim kutusunda, tıklatın **yeni**.</span><span class="sxs-lookup"><span data-stu-id="dfbec-202">On hello **X.509 Certificates** dialog, click **New**.</span></span>
    
     <span data-ttu-id="dfbec-203">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-servicenow-tutorial/IC7694974.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="dfbec-203">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694974.png "Configure single sign-on")</span></span>

12. <span data-ttu-id="dfbec-204">Merhaba üzerinde **X.509 sertifikalarını** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="dfbec-204">On hello **X.509 Certificates** dialog, perform hello following steps:</span></span>
    
     <span data-ttu-id="dfbec-205">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="dfbec-205">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configure single sign-on")</span></span>
    
     <span data-ttu-id="dfbec-206">a.</span><span class="sxs-lookup"><span data-stu-id="dfbec-206">a.</span></span> <span data-ttu-id="dfbec-207">**Yeni**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="dfbec-207">Click **New**.</span></span>
    
     <span data-ttu-id="dfbec-208">b.</span><span class="sxs-lookup"><span data-stu-id="dfbec-208">b.</span></span> <span data-ttu-id="dfbec-209">Merhaba, **adı** metin kutusuna, yapılandırmanız için bir ad yazın (örneğin: **TestSAML2.0**).</span><span class="sxs-lookup"><span data-stu-id="dfbec-209">In hello **Name** textbox, type a name for your configuration (e.g.: **TestSAML2.0**).</span></span>
    
     <span data-ttu-id="dfbec-210">c.</span><span class="sxs-lookup"><span data-stu-id="dfbec-210">c.</span></span> <span data-ttu-id="dfbec-211">Seçin **etkin**.</span><span class="sxs-lookup"><span data-stu-id="dfbec-211">Select **Active**.</span></span>
    
     <span data-ttu-id="dfbec-212">d.</span><span class="sxs-lookup"><span data-stu-id="dfbec-212">d.</span></span> <span data-ttu-id="dfbec-213">Olarak **biçimi**seçin **PEM**.</span><span class="sxs-lookup"><span data-stu-id="dfbec-213">As **Format**, select **PEM**.</span></span>
    
     <span data-ttu-id="dfbec-214">e.</span><span class="sxs-lookup"><span data-stu-id="dfbec-214">e.</span></span> <span data-ttu-id="dfbec-215">Olarak **türü**seçin **deposu sertifika güven**.</span><span class="sxs-lookup"><span data-stu-id="dfbec-215">As **Type**, select **Trust Store Cert**.</span></span>
    
     <span data-ttu-id="dfbec-216">f.</span><span class="sxs-lookup"><span data-stu-id="dfbec-216">f.</span></span> <span data-ttu-id="dfbec-217">Base64 ile kodlanmış sertifikanızı kopyalama hello panonuza bunu içerik Not Defteri'nde açın ve toohello yapıştırın **PEM sertifika** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="dfbec-217">Open your Base64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **PEM Certificate** textbox.</span></span>
    
     <span data-ttu-id="dfbec-218">g.</span><span class="sxs-lookup"><span data-stu-id="dfbec-218">g.</span></span> <span data-ttu-id="dfbec-219">Tıklatın **güncelleştirme**.</span><span class="sxs-lookup"><span data-stu-id="dfbec-219">Click **Update**.</span></span>

13. <span data-ttu-id="dfbec-220">Merhaba Gezinti hello sol taraftaki bölmede **kimlik sağlayıcıları**.</span><span class="sxs-lookup"><span data-stu-id="dfbec-220">In hello navigation pane on hello left side, click **Identity Providers**.</span></span>
    
     <span data-ttu-id="dfbec-221">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_07.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="dfbec-221">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_07.png "Configure single sign-on")</span></span>

14. <span data-ttu-id="dfbec-222">Merhaba üzerinde **kimlik sağlayıcıları** iletişim kutusunda, tıklatın **yeni**:</span><span class="sxs-lookup"><span data-stu-id="dfbec-222">On hello **Identity Providers** dialog, click **New**:</span></span>
    
     <span data-ttu-id="dfbec-223">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-servicenow-tutorial/IC7694977.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="dfbec-223">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694977.png "Configure single sign-on")</span></span>

15. <span data-ttu-id="dfbec-224">Merhaba üzerinde **kimlik sağlayıcıları** iletişim kutusunda, tıklatın **SAML2 Update1?**:</span><span class="sxs-lookup"><span data-stu-id="dfbec-224">On hello **Identity Providers** dialog, click **SAML2 Update1?**:</span></span>
    
     <span data-ttu-id="dfbec-225">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-servicenow-tutorial/IC7694978.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="dfbec-225">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694978.png "Configure single sign-on")</span></span>

16. <span data-ttu-id="dfbec-226">Merhaba SAML2 Update1 Özellikler iletişim kutusunda hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="dfbec-226">On hello SAML2 Update1 Properties dialog, perform hello following steps:</span></span>
    
     <span data-ttu-id="dfbec-227">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-servicenow-tutorial/IC7694982.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="dfbec-227">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694982.png "Configure single sign-on")</span></span>

    <span data-ttu-id="dfbec-228">a.</span><span class="sxs-lookup"><span data-stu-id="dfbec-228">a.</span></span> <span data-ttu-id="dfbec-229">Merhaba, **adı** metin kutusuna, yapılandırmanız için bir ad yazın (örneğin: **SAML 2.0**).</span><span class="sxs-lookup"><span data-stu-id="dfbec-229">in hello **Name** textbox, type a name for your configuration (e.g.: **SAML 2.0**).</span></span>

    <span data-ttu-id="dfbec-230">b.</span><span class="sxs-lookup"><span data-stu-id="dfbec-230">b.</span></span> <span data-ttu-id="dfbec-231">Merhaba, **kullanıcı alanı** metin kutusuna, türü **e-posta** veya **user_name**, toouniquely tanımlamak ServiceNow dağıtımınızda bulunan kullanıcılar hangi alan bağlı olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="dfbec-231">In hello **User Field** textbox, type **email** or **user_name**, depending on which field is used toouniquely identify users in your ServiceNow deployment.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="dfbec-232">Azure AD configue tooemit ya da hello Azure AD kullanıcı kimliği (kullanıcı asıl adı) olabilir ya da hello SAML belirteci benzersiz tanımlayıcı tarafından giderek toohello hello gibi e-posta adresi hello **ServiceNow > öznitelikler > çoklu oturum açma** bölümü Klasik Azure portalı ve eşleme istenen hello alan toohello hello **NameIdentifier** özniteliği.</span><span class="sxs-lookup"><span data-stu-id="dfbec-232">You can configue Azure AD tooemit either hello Azure AD user ID (user principal name) or hello email address as hello unique identifier in hello SAML token by going toohello **ServiceNow > Attributes > Single Sign-On** section of hello Azure classic portal and mapping hello desired field toohello **nameidentifier** attribute.</span></span> <span data-ttu-id="dfbec-233">Hello seçili öznitelik için Azure AD (örneğin kullanıcı asıl adı) depolanan hello değeri girilen hello alan (örneğin user_name) ServiceNow içinde depolanan hello değeriyle eşleşmelidir</span><span class="sxs-lookup"><span data-stu-id="dfbec-233">hello value stored for hello selected attribute in Azure AD (e.g. user principal name) must match hello value stored in ServiceNow for hello entered field (e.g. user_name)</span></span>

    <span data-ttu-id="dfbec-234">c.</span><span class="sxs-lookup"><span data-stu-id="dfbec-234">c.</span></span> <span data-ttu-id="dfbec-235">Hello Azure AD Klasik portalında hello kopyalama **kimlik sağlayıcı kimliği** değer ve hello yapıştırma **kimlik sağlayıcısı URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="dfbec-235">In hello Azure AD classic portal, copy hello **Identity Provider ID** value, and then paste it into hello **Identity Provider URL** textbox.</span></span>

    <span data-ttu-id="dfbec-236">d.</span><span class="sxs-lookup"><span data-stu-id="dfbec-236">d.</span></span> <span data-ttu-id="dfbec-237">Hello Azure AD Klasik portalında hello kopyalama **kimlik doğrulaması istek URL'si** değer ve hello yapıştırma **kimlik sağlayıcısının AuthnRequest** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="dfbec-237">In hello Azure AD classic portal, copy hello **Authentication Request URL** value, and then paste it into hello **Identity Provider's AuthnRequest** textbox.</span></span>

    <span data-ttu-id="dfbec-238">e.</span><span class="sxs-lookup"><span data-stu-id="dfbec-238">e.</span></span> <span data-ttu-id="dfbec-239">Hello Azure AD Klasik portalında hello kopyalama **tek Sign-Out hizmeti URL'si** değer ve hello yapıştırma **kimlik sağlayıcısının SingleLogoutRequest** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="dfbec-239">In hello Azure AD classic portal, copy hello **Single Sign-Out Service URL** value, and then paste it into hello **Identity Provider's SingleLogoutRequest** textbox.</span></span>

    <span data-ttu-id="dfbec-240">f.</span><span class="sxs-lookup"><span data-stu-id="dfbec-240">f.</span></span> <span data-ttu-id="dfbec-241">Merhaba, **ServiceNow giriş sayfası** metin kutusuna, ServiceNow örneği giriş sayfanız türü hello URL'si.</span><span class="sxs-lookup"><span data-stu-id="dfbec-241">In hello **ServiceNow Homepage** textbox, type hello URL of your ServiceNow instance homepage.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="dfbec-242">Merhaba ServiceNow örneği giriş sayfası olan bir birleşimini, **ServieNow Kiracı URL** ve **/navpage.do** (örn:`https://fabrikam.service-now.com/navpage.do`).</span><span class="sxs-lookup"><span data-stu-id="dfbec-242">hello ServiceNow instance homepage is a concatenation of your **ServieNow tenant URL** and **/navpage.do** (e.g.:`https://fabrikam.service-now.com/navpage.do`).</span></span>

    <span data-ttu-id="dfbec-243">g.</span><span class="sxs-lookup"><span data-stu-id="dfbec-243">g.</span></span> <span data-ttu-id="dfbec-244">Merhaba, **varlık kimliği / veren** metin kutusuna, ServiceNow kiracınızın türü hello URL.</span><span class="sxs-lookup"><span data-stu-id="dfbec-244">In hello **Entity ID / Issuer** textbox, type hello URL of your ServiceNow tenant.</span></span>

    <span data-ttu-id="dfbec-245">h.</span><span class="sxs-lookup"><span data-stu-id="dfbec-245">h.</span></span> <span data-ttu-id="dfbec-246">Merhaba, **İzleyici URL** metin kutusuna, ServiceNow kiracınızın türü hello URL.</span><span class="sxs-lookup"><span data-stu-id="dfbec-246">In hello **Audience URL** textbox, type hello URL of your ServiceNow tenant.</span></span> 

    <span data-ttu-id="dfbec-247">ı.</span><span class="sxs-lookup"><span data-stu-id="dfbec-247">i.</span></span> <span data-ttu-id="dfbec-248">Merhaba, **Protokolü bağlama hello IDP'ın SingleLogoutRequest için** metin kutusuna, türü **urn: OASIS: adları: tc: SAML:2.0:bindings:HTTP-yeniden yönlendirme**.</span><span class="sxs-lookup"><span data-stu-id="dfbec-248">In hello **Protocol Binding for hello IDP's SingleLogoutRequest** textbox, type **urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect**.</span></span>

    <span data-ttu-id="dfbec-249">j.</span><span class="sxs-lookup"><span data-stu-id="dfbec-249">j.</span></span> <span data-ttu-id="dfbec-250">Hello NameID İlkesi metin kutusuna, yazın **urn: OASIS: adları: tc: SAML:1.1:nameid-biçimi: belirtilmeyen**.</span><span class="sxs-lookup"><span data-stu-id="dfbec-250">In hello NameID Policy textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified**.</span></span>

    <span data-ttu-id="dfbec-251">k.</span><span class="sxs-lookup"><span data-stu-id="dfbec-251">k.</span></span> <span data-ttu-id="dfbec-252">Seçimini **bir AuthnContextClass oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="dfbec-252">Deselect **Create an AuthnContextClass**.</span></span>

    <span data-ttu-id="dfbec-253">l.</span><span class="sxs-lookup"><span data-stu-id="dfbec-253">l.</span></span> <span data-ttu-id="dfbec-254">Merhaba, **AuthnContextClassRef yöntemi**, türü `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`.</span><span class="sxs-lookup"><span data-stu-id="dfbec-254">In hello **AuthnContextClassRef Method**, type `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`.</span></span> <span data-ttu-id="dfbec-255">Bu, yalnızca bulut yalnızca kuruluş ise gereklidir.</span><span class="sxs-lookup"><span data-stu-id="dfbec-255">This is only needed if you are cloud only organization.</span></span> <span data-ttu-id="dfbec-256">Kullanıyorsanız, ADFS veya MFA kimlik doğrulaması için bu değeri yapılandırmamalısınız sonra şirket içi.</span><span class="sxs-lookup"><span data-stu-id="dfbec-256">If you are using on-premises ADFS or MFA for authentication then you should not configure this value.</span></span> 

    <span data-ttu-id="dfbec-257">m.</span><span class="sxs-lookup"><span data-stu-id="dfbec-257">m.</span></span> <span data-ttu-id="dfbec-258">İçinde **saat eğriltme** metin kutusuna, türü **60**.</span><span class="sxs-lookup"><span data-stu-id="dfbec-258">In **Clock Skew** textbox, type **60**.</span></span>

    <span data-ttu-id="dfbec-259">n.</span><span class="sxs-lookup"><span data-stu-id="dfbec-259">n.</span></span> <span data-ttu-id="dfbec-260">Olarak **üzerinde tek oturum betiği**seçin **MultiSSO_SAML2_Update1**.</span><span class="sxs-lookup"><span data-stu-id="dfbec-260">As **Single Sign On Script**, select **MultiSSO_SAML2_Update1**.</span></span>

    <span data-ttu-id="dfbec-261">o.</span><span class="sxs-lookup"><span data-stu-id="dfbec-261">o.</span></span> <span data-ttu-id="dfbec-262">Olarak **x509 sertifika**seçin hello önceki adımda oluşturduğunuz hello sertifika.</span><span class="sxs-lookup"><span data-stu-id="dfbec-262">As **x509 Certificate**, select hello certificate you have created in hello previous step.</span></span>

    <span data-ttu-id="dfbec-263">p.</span><span class="sxs-lookup"><span data-stu-id="dfbec-263">p.</span></span> <span data-ttu-id="dfbec-264">Tıklatın **gönderme**.</span><span class="sxs-lookup"><span data-stu-id="dfbec-264">Click **Submit**.</span></span> 

1. <span data-ttu-id="dfbec-265">Hello Azure AD Klasik portalında hello tek oturum açma yapılandırması onay seçin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="dfbec-265">On hello Azure AD classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    <span data-ttu-id="dfbec-266">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="dfbec-266">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="dfbec-267">Merhaba üzerinde **tek oturum açma onay** sayfasında, **tam**.</span><span class="sxs-lookup"><span data-stu-id="dfbec-267">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    <span data-ttu-id="dfbec-268">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="dfbec-268">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configure single sign-on")</span></span>

### <a name="configuring-azure-ad-single-sign-on-for-servicenow-express"></a><span data-ttu-id="dfbec-269">Azure AD çoklu oturum açma ServiceNow Express için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="dfbec-269">Configuring Azure AD Single Sign-On for ServiceNow Express</span></span>
1. <span data-ttu-id="dfbec-270">Hello Azure AD Klasik portalında, hello **ServiceNow** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma yapılandırmak** tooopen hello **tek oturum yapılandırma üzerinde aktar** iletişim .</span><span class="sxs-lookup"><span data-stu-id="dfbec-270">In hello Azure AD classic portal, on hello **ServiceNow** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="dfbec-271">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-servicenow-tutorial/IC749323.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="dfbec-271">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="dfbec-272">Merhaba üzerinde **nasıl tooServiceNow üzerinde kullanıcılar toosign gibi yaptığınız** sayfasında, **Microsoft Azure AD çoklu oturum açma**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="dfbec-272">On hello **How would you like users toosign on tooServiceNow** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="dfbec-273">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-servicenow-tutorial/IC749324.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="dfbec-273">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configure single sign-on")</span></span>

3. <span data-ttu-id="dfbec-274">Merhaba üzerinde **uygulama ayarlarını yapılandır** sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="dfbec-274">On hello **Configure App Settings** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="dfbec-275">![Uygulama URL'sini Yapılandır](./media/active-directory-saas-servicenow-tutorial/IC769497.png "uygulama URL'sini yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="dfbec-275">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configure app URL")</span></span>
   
    <span data-ttu-id="dfbec-276">a.</span><span class="sxs-lookup"><span data-stu-id="dfbec-276">a.</span></span> <span data-ttu-id="dfbec-277">Merhaba, **üzerinde ServiceNow oturum URL'si** URL'nizi metin kutusuna, türü hello desen aşağıdaki kullanıcıların toosign üzerinde tooyour ServiceNow uygulamanız tarafından kullanılan: `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="dfbec-277">in hello **ServiceNow Sign On URL** textbox, type your URL used by your users toosign-on tooyour ServiceNow application following hello pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="dfbec-278">b.</span><span class="sxs-lookup"><span data-stu-id="dfbec-278">b.</span></span> <span data-ttu-id="dfbec-279">Merhaba, **veren URL'si** URL'nizi metin kutusuna, türü hello desen aşağıdaki kullanıcıların toosign üzerinde tooyour ServiceNow uygulamanız tarafından kullanılan `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="dfbec-279">In hello **Issuer URL** textbox,type your URL used by your users toosign-on tooyour ServiceNow application following hello pattern `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="dfbec-280">c.</span><span class="sxs-lookup"><span data-stu-id="dfbec-280">c.</span></span> <span data-ttu-id="dfbec-281">**İleri**’ye tıklayın</span><span class="sxs-lookup"><span data-stu-id="dfbec-281">Click **Next**</span></span>

4. <span data-ttu-id="dfbec-282">Tıklatın **el ile Merhaba uygulaması çoklu oturum açma için yapılandırma**, ardından **sonraki** tam hello adımları izleyerek.</span><span class="sxs-lookup"><span data-stu-id="dfbec-282">Click **Manually configure hello application for single sign-on**, then click **Next** and complete hello following steps.</span></span>
   
    <span data-ttu-id="dfbec-283">![Uygulama URL'sini Yapılandır](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "uygulama URL'sini yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="dfbec-283">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configure app URL")</span></span>

5. <span data-ttu-id="dfbec-284">Merhaba üzerinde **Servicenow'da çoklu oturum açma yapılandırma** sayfasında, **indirme sertifika**, yerel olarak bilgisayarınızda hello sertifika dosyasını kaydedin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="dfbec-284">On hello **Configure single sign-on at ServiceNow** page, click **Download certificate**, save hello certificate file locally on your computer, and then click **Next**.</span></span>
   
    <span data-ttu-id="dfbec-285">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-servicenow-tutorial/IC749325.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="dfbec-285">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configure single sign-on")</span></span>

6. <span data-ttu-id="dfbec-286">Oturum açma ServiceNow Express uygulama yönetici olarak tooyour.</span><span class="sxs-lookup"><span data-stu-id="dfbec-286">Sign-on tooyour ServiceNow Express application as an administrator.</span></span>

7. <span data-ttu-id="dfbec-287">Merhaba Gezinti hello sol taraftaki bölmede **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="dfbec-287">In hello navigation pane on hello left side, click **Single Sign-On**.</span></span>  
   
    <span data-ttu-id="dfbec-288">![Uygulama URL'sini Yapılandır](./media/active-directory-saas-servicenow-tutorial/ic7694980ex.png "uygulama URL'sini yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="dfbec-288">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/ic7694980ex.png "Configure app URL")</span></span>

8. <span data-ttu-id="dfbec-289">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda, hello üst sağ ve ayarlanmış hello özellikler aşağıdaki hello yapılandırma simgesine tıklayın:</span><span class="sxs-lookup"><span data-stu-id="dfbec-289">On hello **Single Sign-On** dialog, click hello configuration icon on hello upper right and set hello following properties:</span></span>
   
    <span data-ttu-id="dfbec-290">![Uygulama URL'sini Yapılandır](./media/active-directory-saas-servicenow-tutorial/ic7694981ex.png "uygulama URL'sini yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="dfbec-290">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/ic7694981ex.png "Configure app URL")</span></span>
   
    <span data-ttu-id="dfbec-291">a.</span><span class="sxs-lookup"><span data-stu-id="dfbec-291">a.</span></span> <span data-ttu-id="dfbec-292">İki durumlu **birden çok sağlayıcı SSO etkinleştirme** toohello sağ.</span><span class="sxs-lookup"><span data-stu-id="dfbec-292">Toggle **Enable multiple provider SSO** toohello right.</span></span>
   
    <span data-ttu-id="dfbec-293">b.</span><span class="sxs-lookup"><span data-stu-id="dfbec-293">b.</span></span> <span data-ttu-id="dfbec-294">İki durumlu **etkinleştir hata ayıklama hello için birden çok sağlayıcı SSO tümleştirme günlüğü** toohello sağ.</span><span class="sxs-lookup"><span data-stu-id="dfbec-294">Toggle **Enable debug logging for hello multiple provider SSO integration** toohello right.</span></span>
   
    <span data-ttu-id="dfbec-295">c.</span><span class="sxs-lookup"><span data-stu-id="dfbec-295">c.</span></span> <span data-ttu-id="dfbec-296">İçinde **hello alan hello kullanıcı tablo...**  metin kutusuna, türü **user_name**.</span><span class="sxs-lookup"><span data-stu-id="dfbec-296">In **hello field on hello user table that...** textbox, type **user_name**.</span></span>
9. <span data-ttu-id="dfbec-297">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda, tıklatın **yeni sertifika Ekle**.</span><span class="sxs-lookup"><span data-stu-id="dfbec-297">On hello **Single Sign-On** dialog, click **Add New Certificate**.</span></span>
   
    <span data-ttu-id="dfbec-298">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-servicenow-tutorial/ic7694973ex.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="dfbec-298">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694973ex.png "Configure single sign-on")</span></span>
10. <span data-ttu-id="dfbec-299">Merhaba üzerinde **X.509 sertifikalarını** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="dfbec-299">On hello **X.509 Certificates** dialog, perform hello following steps:</span></span>
    
    <span data-ttu-id="dfbec-300">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="dfbec-300">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configure single sign-on")</span></span>
    
    <span data-ttu-id="dfbec-301">a.</span><span class="sxs-lookup"><span data-stu-id="dfbec-301">a.</span></span> <span data-ttu-id="dfbec-302">Merhaba, **adı** metin kutusuna, yapılandırmanız için bir ad yazın (örneğin: **TestSAML2.0**).</span><span class="sxs-lookup"><span data-stu-id="dfbec-302">In hello **Name** textbox, type a name for your configuration (e.g.: **TestSAML2.0**).</span></span>
    
    <span data-ttu-id="dfbec-303">b.</span><span class="sxs-lookup"><span data-stu-id="dfbec-303">b.</span></span> <span data-ttu-id="dfbec-304">Seçin **etkin**.</span><span class="sxs-lookup"><span data-stu-id="dfbec-304">Select **Active**.</span></span>
    
    <span data-ttu-id="dfbec-305">c.</span><span class="sxs-lookup"><span data-stu-id="dfbec-305">c.</span></span> <span data-ttu-id="dfbec-306">Olarak **biçimi**seçin **PEM**.</span><span class="sxs-lookup"><span data-stu-id="dfbec-306">As **Format**, select **PEM**.</span></span>
    
    <span data-ttu-id="dfbec-307">d.</span><span class="sxs-lookup"><span data-stu-id="dfbec-307">d.</span></span> <span data-ttu-id="dfbec-308">Olarak **türü**seçin **deposu sertifika güven**.</span><span class="sxs-lookup"><span data-stu-id="dfbec-308">As **Type**, select **Trust Store Cert**.</span></span>
    
    <span data-ttu-id="dfbec-309">e.</span><span class="sxs-lookup"><span data-stu-id="dfbec-309">e.</span></span> <span data-ttu-id="dfbec-310">Bir Base64 ile kodlanmış dosyası indirilen sertifikanızı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="dfbec-310">Create a Base64 encoded file from your downloaded certificate.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="dfbec-311">Daha fazla ayrıntı için bkz: [nasıl tooconvert bir ikili sertifika bir metin dosyasına](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="dfbec-311">For more details, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>
    > 
    > 
    
    <span data-ttu-id="dfbec-312">f.</span><span class="sxs-lookup"><span data-stu-id="dfbec-312">f.</span></span> <span data-ttu-id="dfbec-313">Base64 ile kodlanmış sertifikanızı kopyalama hello panonuza bunu içerik Not Defteri'nde açın ve toohello yapıştırın **PEM sertifika** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="dfbec-313">Open your Base64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **PEM Certificate** textbox.</span></span>
    
    <span data-ttu-id="dfbec-314">g.</span><span class="sxs-lookup"><span data-stu-id="dfbec-314">g.</span></span> <span data-ttu-id="dfbec-315">Tıklatın **güncelleştirme**.</span><span class="sxs-lookup"><span data-stu-id="dfbec-315">Click **Update**.</span></span>
11. <span data-ttu-id="dfbec-316">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda, tıklatın **ekleme yeni IDP**.</span><span class="sxs-lookup"><span data-stu-id="dfbec-316">On hello **Single Sign-On** dialog, click **Add New IdP**.</span></span>
    
    <span data-ttu-id="dfbec-317">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-servicenow-tutorial/ic7694976ex.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="dfbec-317">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694976ex.png "Configure single sign-on")</span></span>
12. <span data-ttu-id="dfbec-318">Merhaba üzerinde **yeni kimlik sağlayıcı Ekle** iletişim altında **yapılandırma kimlik sağlayıcısı**, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="dfbec-318">On hello **Add New Identity Provider** dialog, under **Configure Identity Provider**, perform hello following steps:</span></span>
    
    <span data-ttu-id="dfbec-319">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-servicenow-tutorial/ic7694982ex.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="dfbec-319">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694982ex.png "Configure single sign-on")</span></span>

    <span data-ttu-id="dfbec-320">a.</span><span class="sxs-lookup"><span data-stu-id="dfbec-320">a.</span></span> <span data-ttu-id="dfbec-321">Merhaba, **adı** metin kutusuna, yapılandırmanız için bir ad yazın (örneğin: **SAML 2.0**).</span><span class="sxs-lookup"><span data-stu-id="dfbec-321">In hello **Name** textbox, type a name for your configuration (e.g.: **SAML 2.0**).</span></span>

    <span data-ttu-id="dfbec-322">b.</span><span class="sxs-lookup"><span data-stu-id="dfbec-322">b.</span></span> <span data-ttu-id="dfbec-323">Hello Azure AD Klasik portalında hello kopyalama **kimlik sağlayıcı kimliği** değer ve hello yapıştırma **kimlik sağlayıcısı URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="dfbec-323">In hello Azure AD classic portal, copy hello **Identity Provider ID** value, and then paste it into hello **Identity Provider URL** textbox.</span></span>

    <span data-ttu-id="dfbec-324">c.</span><span class="sxs-lookup"><span data-stu-id="dfbec-324">c.</span></span> <span data-ttu-id="dfbec-325">Hello Azure AD Klasik portalında hello kopyalama **kimlik doğrulaması istek URL'si** değer ve hello yapıştırma **kimlik sağlayıcısının AuthnRequest** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="dfbec-325">In hello Azure AD classic portal, copy hello **Authentication Request URL** value, and then paste it into hello **Identity Provider's AuthnRequest** textbox.</span></span>

    <span data-ttu-id="dfbec-326">d.</span><span class="sxs-lookup"><span data-stu-id="dfbec-326">d.</span></span> <span data-ttu-id="dfbec-327">Hello Azure AD Klasik portalında hello kopyalama **tek Sign-Out hizmeti URL'si** değer ve hello yapıştırma **kimlik sağlayıcısının SingleLogoutRequest** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="dfbec-327">In hello Azure AD classic portal, copy hello **Single Sign-Out Service URL** value, and then paste it into hello **Identity Provider's SingleLogoutRequest** textbox.</span></span>

    <span data-ttu-id="dfbec-328">e.</span><span class="sxs-lookup"><span data-stu-id="dfbec-328">e.</span></span> <span data-ttu-id="dfbec-329">Olarak **kimlik sağlayıcısı sertifikası**seçin hello önceki adımda oluşturduğunuz hello sertifika.</span><span class="sxs-lookup"><span data-stu-id="dfbec-329">As **Identity Provider Certificate**, select hello certificate you have created in hello previous step.</span></span>


1. <span data-ttu-id="dfbec-330">Tıklatın **Gelişmiş ayarları**ve altında **ek kimlik sağlayıcısı özellikleri**, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="dfbec-330">Click **Advanced Settings**, and under **Additional Identity Provider Properties**, perform hello following steps:</span></span>
   
    <span data-ttu-id="dfbec-331">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-servicenow-tutorial/ic7694983ex.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="dfbec-331">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694983ex.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="dfbec-332">a.</span><span class="sxs-lookup"><span data-stu-id="dfbec-332">a.</span></span> <span data-ttu-id="dfbec-333">Merhaba, **Protokolü bağlama hello IDP'ın SingleLogoutRequest için** metin kutusuna, türü **urn: OASIS: adları: tc: SAML:2.0:bindings:HTTP-yeniden yönlendirme**.</span><span class="sxs-lookup"><span data-stu-id="dfbec-333">In hello **Protocol Binding for hello IDP's SingleLogoutRequest** textbox, type **urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect**.</span></span>
   
    <span data-ttu-id="dfbec-334">b.</span><span class="sxs-lookup"><span data-stu-id="dfbec-334">b.</span></span> <span data-ttu-id="dfbec-335">Merhaba, **NameID İlkesi** metin kutusuna, türü **urn: OASIS: adları: tc: SAML:1.1:nameid-biçimi: belirtilmeyen**.</span><span class="sxs-lookup"><span data-stu-id="dfbec-335">In hello **NameID Policy** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified**.</span></span>    
   
    <span data-ttu-id="dfbec-336">c.</span><span class="sxs-lookup"><span data-stu-id="dfbec-336">c.</span></span> <span data-ttu-id="dfbec-337">Merhaba, **AuthnContextClassRef yöntemi**, türü **http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password**.</span><span class="sxs-lookup"><span data-stu-id="dfbec-337">In hello **AuthnContextClassRef Method**, type **http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password**.</span></span>
   
    <span data-ttu-id="dfbec-338">d.</span><span class="sxs-lookup"><span data-stu-id="dfbec-338">d.</span></span> <span data-ttu-id="dfbec-339">Seçimini **bir AuthnContextClass oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="dfbec-339">Deselect **Create an AuthnContextClass**.</span></span>

2. <span data-ttu-id="dfbec-340">Altında **ek hizmet sağlayıcısı özellikleri**, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="dfbec-340">Under **Additional Service Provider Properties**, perform hello following steps:</span></span>
   
    <span data-ttu-id="dfbec-341">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-servicenow-tutorial/ic7694984ex.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="dfbec-341">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694984ex.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="dfbec-342">a.</span><span class="sxs-lookup"><span data-stu-id="dfbec-342">a.</span></span> <span data-ttu-id="dfbec-343">Merhaba, **ServiceNow giriş sayfası** metin kutusuna, ServiceNow örneği giriş sayfanız türü hello URL'si.</span><span class="sxs-lookup"><span data-stu-id="dfbec-343">In hello **ServiceNow Homepage** textbox, type hello URL of your ServiceNow instance homepage.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="dfbec-344">Merhaba ServiceNow örneği giriş sayfası olan bir birleşimini, **ServieNow Kiracı URL** ve **/navpage.do** (örn: `https://fabrikam.service-now.com/navpage.do`).</span><span class="sxs-lookup"><span data-stu-id="dfbec-344">hello ServiceNow instance homepage is a concatenation of your **ServieNow tenant URL** and **/navpage.do** (e.g.: `https://fabrikam.service-now.com/navpage.do`).</span></span>
    > 
    > 
   
    <span data-ttu-id="dfbec-345">b.</span><span class="sxs-lookup"><span data-stu-id="dfbec-345">b.</span></span> <span data-ttu-id="dfbec-346">Merhaba, **varlık kimliği / veren** metin kutusuna, ServiceNow kiracınızın türü hello URL.</span><span class="sxs-lookup"><span data-stu-id="dfbec-346">In hello **Entity ID / Issuer** textbox, type hello URL of your ServiceNow tenant.</span></span>
   
    <span data-ttu-id="dfbec-347">c.</span><span class="sxs-lookup"><span data-stu-id="dfbec-347">c.</span></span> <span data-ttu-id="dfbec-348">Merhaba, **İzleyici URI'si** metin kutusuna, ServiceNow kiracınızın türü hello URL.</span><span class="sxs-lookup"><span data-stu-id="dfbec-348">In hello **Audience URI** textbox, type hello URL of your ServiceNow tenant.</span></span> 
   
    <span data-ttu-id="dfbec-349">d.</span><span class="sxs-lookup"><span data-stu-id="dfbec-349">d.</span></span> <span data-ttu-id="dfbec-350">İçinde **saat eğriltme** metin kutusuna, türü **60**.</span><span class="sxs-lookup"><span data-stu-id="dfbec-350">In **Clock Skew** textbox, type **60**.</span></span>
   
    <span data-ttu-id="dfbec-351">e.</span><span class="sxs-lookup"><span data-stu-id="dfbec-351">e.</span></span> <span data-ttu-id="dfbec-352">Merhaba, **kullanıcı alanı** metin kutusuna, türü **e-posta** veya **user_name**, toouniquely tanımlamak ServiceNow dağıtımınızda bulunan kullanıcılar hangi alan bağlı olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="dfbec-352">In hello **User Field** textbox, type **email** or **user_name**, depending on which field is used toouniquely identify users in your ServiceNow deployment.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="dfbec-353">Azure AD configue tooemit ya da hello Azure AD kullanıcı kimliği (kullanıcı asıl adı) olabilir ya da hello SAML belirteci benzersiz tanımlayıcı tarafından giderek toohello hello gibi e-posta adresi hello **ServiceNow > öznitelikler > çoklu oturum açma** bölümü Klasik Azure portalı ve eşleme istenen hello alan toohello hello **NameIdentifier** özniteliği.</span><span class="sxs-lookup"><span data-stu-id="dfbec-353">You can configue Azure AD tooemit either hello Azure AD user ID (user principal name) or hello email address as hello unique identifier in hello SAML token by going toohello **ServiceNow > Attributes > Single Sign-On** section of hello Azure classic portal and mapping hello desired field toohello **nameidentifier** attribute.</span></span> <span data-ttu-id="dfbec-354">Hello seçili öznitelik için Azure AD (örneğin kullanıcı asıl adı) depolanan hello değeri girilen hello alan (örneğin user_name) ServiceNow içinde depolanan hello değeriyle eşleşmelidir</span><span class="sxs-lookup"><span data-stu-id="dfbec-354">hello value stored for hello selected attribute in Azure AD (e.g. user principal name) must match hello value stored in ServiceNow for hello entered field (e.g. user_name)</span></span>
    > 
    > 
   
    <span data-ttu-id="dfbec-355">f.</span><span class="sxs-lookup"><span data-stu-id="dfbec-355">f.</span></span> <span data-ttu-id="dfbec-356">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="dfbec-356">Click **Save**.</span></span> 

3. <span data-ttu-id="dfbec-357">Hello Azure AD Klasik portalında hello tek oturum açma yapılandırması onay seçin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="dfbec-357">On hello Azure AD classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    <span data-ttu-id="dfbec-358">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="dfbec-358">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configure single sign-on")</span></span>

4. <span data-ttu-id="dfbec-359">Merhaba üzerinde **tek oturum açma onay** sayfasında, **tam**.</span><span class="sxs-lookup"><span data-stu-id="dfbec-359">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    <span data-ttu-id="dfbec-360">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="dfbec-360">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configure single sign-on")</span></span>

## <a name="configuring-user-provisioning"></a><span data-ttu-id="dfbec-361">Kullanıcı hazırlama işleminin yapılandırılması</span><span class="sxs-lookup"><span data-stu-id="dfbec-361">Configuring user provisioning</span></span>
<span data-ttu-id="dfbec-362">Bu bölümde Hello amacı olan toooutline tooServiceNow tooenable Active Directory kullanıcısı kullanıcı sağlamayı nasıl hesapları.</span><span class="sxs-lookup"><span data-stu-id="dfbec-362">hello objective of this section is toooutline how tooenable user provisioning of Active Directory user accounts tooServiceNow.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="dfbec-363">tooconfigure kullanıcı hazırlama, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="dfbec-363">tooconfigure user provisioning, perform hello following steps:</span></span>
1. <span data-ttu-id="dfbec-364">Hello Azure Yönetim Portalı'nda Klasik, hello üzerinde **ServiceNow** uygulama tümleştirme sayfasını tıklatın **kullanıcı sağlamayı Yapılandır**.</span><span class="sxs-lookup"><span data-stu-id="dfbec-364">In hello Azure Management classic portal, on hello **ServiceNow** application integration page, click **Configure user provisioning**.</span></span> 
   
    <span data-ttu-id="dfbec-365">![Kullanıcı sağlamayı](./media/active-directory-saas-servicenow-tutorial/IC769498.png "kullanıcı hazırlama")</span><span class="sxs-lookup"><span data-stu-id="dfbec-365">![User provisioning](./media/active-directory-saas-servicenow-tutorial/IC769498.png "User provisioning")</span></span>

2. <span data-ttu-id="dfbec-366">Merhaba üzerinde **, ServiceNow kimlik bilgileri tooenable otomatik kullanıcı sağlamayı girin** sayfasında, yapılandırma ayarlarını aşağıdaki hello sağlayın:</span><span class="sxs-lookup"><span data-stu-id="dfbec-366">On hello **Enter your ServiceNow credentials tooenable automatic user provisioning** page, provide hello following configuration settings:</span></span>
   
     <span data-ttu-id="dfbec-367">a.</span><span class="sxs-lookup"><span data-stu-id="dfbec-367">a.</span></span> <span data-ttu-id="dfbec-368">Merhaba, **ServiceNow örneği adı** metin kutusuna, tür hello ServiceNow örneğinin adı.</span><span class="sxs-lookup"><span data-stu-id="dfbec-368">In hello **ServiceNow Instance Name** textbox, type hello ServiceNow instance name.</span></span>
   
     <span data-ttu-id="dfbec-369">b.</span><span class="sxs-lookup"><span data-stu-id="dfbec-369">b.</span></span> <span data-ttu-id="dfbec-370">Merhaba, **ServiceNow yönetici kullanıcı adı** metin kutusuna, tür hello hello ServiceNow yönetici hesabı adını.</span><span class="sxs-lookup"><span data-stu-id="dfbec-370">In hello **ServiceNow Admin User Name** textbox, type hello name of hello ServiceNow admin account.</span></span>
   
     <span data-ttu-id="dfbec-371">c.</span><span class="sxs-lookup"><span data-stu-id="dfbec-371">c.</span></span> <span data-ttu-id="dfbec-372">Merhaba, **ServiceNow yönetici parolası** metin kutusuna, bu hesap için hello parolayı girin.</span><span class="sxs-lookup"><span data-stu-id="dfbec-372">In hello **ServiceNow Admin Password** textbox, type hello password for this account.</span></span>
   
     <span data-ttu-id="dfbec-373">d.</span><span class="sxs-lookup"><span data-stu-id="dfbec-373">d.</span></span> <span data-ttu-id="dfbec-374">Tıklatın **doğrulamak** tooverify yapılandırmanızı.</span><span class="sxs-lookup"><span data-stu-id="dfbec-374">Click **validate** tooverify your configuration.</span></span>
   
     <span data-ttu-id="dfbec-375">e.</span><span class="sxs-lookup"><span data-stu-id="dfbec-375">e.</span></span> <span data-ttu-id="dfbec-376">Merhaba tıklatın **sonraki** düğmesini tooopen hello **sonraki adımlar** sayfası.</span><span class="sxs-lookup"><span data-stu-id="dfbec-376">Click hello **Next** button tooopen hello **Next steps** page.</span></span>
   
     <span data-ttu-id="dfbec-377">f.</span><span class="sxs-lookup"><span data-stu-id="dfbec-377">f.</span></span> <span data-ttu-id="dfbec-378">Tüm kullanıcıların toothis uygulama tooprovision istiyorsanız seçin "**otomatik olarak hello dizin toothis uygulamadaki tüm kullanıcı hesapları sağlama**".</span><span class="sxs-lookup"><span data-stu-id="dfbec-378">If you want tooprovision all users toothis application, select “**Automatically provision all user accounts in hello directory toothis application**”.</span></span> 
   
    <span data-ttu-id="dfbec-379">![Sonraki adımlar](./media/active-directory-saas-servicenow-tutorial/IC698804.png "sonraki adımlar")</span><span class="sxs-lookup"><span data-stu-id="dfbec-379">![Next Steps](./media/active-directory-saas-servicenow-tutorial/IC698804.png "Next Steps")</span></span>
   
     <span data-ttu-id="dfbec-380">g.</span><span class="sxs-lookup"><span data-stu-id="dfbec-380">g.</span></span> <span data-ttu-id="dfbec-381">Merhaba üzerinde **sonraki adımlar** sayfasında, **tam** toosave yapılandırmanızı.</span><span class="sxs-lookup"><span data-stu-id="dfbec-381">On hello **Next steps** page, click **Complete** toosave your configuration.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="dfbec-382">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="dfbec-382">Creating an Azure AD test user</span></span>
<span data-ttu-id="dfbec-383">Bu bölümde, bir test kullanıcısı Britta Simon adlı hello Klasik portalda oluşturun.</span><span class="sxs-lookup"><span data-stu-id="dfbec-383">In this section, you create a test user in hello classic portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][20]

<span data-ttu-id="dfbec-385">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="dfbec-385">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="dfbec-386">Merhaba, **Klasik Azure portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="dfbec-386">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-servicenow-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="dfbec-388">Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.</span><span class="sxs-lookup"><span data-stu-id="dfbec-388">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="dfbec-389">toodisplay hello hello üstte hello menüde kullanıcıların listesini tıklatın **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="dfbec-389">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-servicenow-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="dfbec-391">tooopen hello **Kullanıcı Ekle** hello araç çubuğunda hello altta iletişim tıklatın **Kullanıcı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="dfbec-391">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-servicenow-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="dfbec-393">Merhaba üzerinde **bu kullanıcı hakkında bize** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="dfbec-393">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-servicenow-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="dfbec-395">a.</span><span class="sxs-lookup"><span data-stu-id="dfbec-395">a.</span></span> <span data-ttu-id="dfbec-396">Kullanıcı türü olarak, kuruluşunuzdaki yeni kullanıcı seçin.</span><span class="sxs-lookup"><span data-stu-id="dfbec-396">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="dfbec-397">b.</span><span class="sxs-lookup"><span data-stu-id="dfbec-397">b.</span></span> <span data-ttu-id="dfbec-398">Merhaba kullanıcı adı olarak **textbox**, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dfbec-398">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="dfbec-399">c.</span><span class="sxs-lookup"><span data-stu-id="dfbec-399">c.</span></span> <span data-ttu-id="dfbec-400">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="dfbec-400">Click **Next**.</span></span>

6. <span data-ttu-id="dfbec-401">Merhaba üzerinde **kullanıcı profili** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="dfbec-401">On hello **User Profile** dialog page, perform hello following steps:</span></span>
   
   ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-servicenow-tutorial/create_aaduser_06.png) 
   
   <span data-ttu-id="dfbec-403">a.</span><span class="sxs-lookup"><span data-stu-id="dfbec-403">a.</span></span> <span data-ttu-id="dfbec-404">Merhaba, **ad** metin kutusuna, türü **Britta**.</span><span class="sxs-lookup"><span data-stu-id="dfbec-404">In hello **First Name** textbox, type **Britta**.</span></span>  
   
   <span data-ttu-id="dfbec-405">b.</span><span class="sxs-lookup"><span data-stu-id="dfbec-405">b.</span></span> <span data-ttu-id="dfbec-406">Merhaba, **Soyadı** metin kutusuna, türü, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="dfbec-406">In hello **Last Name** textbox, type, **Simon**.</span></span>
   
   <span data-ttu-id="dfbec-407">c.</span><span class="sxs-lookup"><span data-stu-id="dfbec-407">c.</span></span> <span data-ttu-id="dfbec-408">Merhaba, **görünen adı** metin kutusuna, türü **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="dfbec-408">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
   
   <span data-ttu-id="dfbec-409">d.</span><span class="sxs-lookup"><span data-stu-id="dfbec-409">d.</span></span> <span data-ttu-id="dfbec-410">Merhaba, **rol** listesinde **kullanıcı**.</span><span class="sxs-lookup"><span data-stu-id="dfbec-410">In hello **Role** list, select **User**.</span></span>
   
   <span data-ttu-id="dfbec-411">e.</span><span class="sxs-lookup"><span data-stu-id="dfbec-411">e.</span></span> <span data-ttu-id="dfbec-412">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="dfbec-412">Click **Next**.</span></span>

7. <span data-ttu-id="dfbec-413">Merhaba üzerinde **Get geçici parola** iletişim sayfasında, tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="dfbec-413">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-servicenow-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="dfbec-415">Merhaba üzerinde **Get geçici parola** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="dfbec-415">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-servicenow-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="dfbec-417">a.</span><span class="sxs-lookup"><span data-stu-id="dfbec-417">a.</span></span> <span data-ttu-id="dfbec-418">Merhaba Hello değerini yazmak **yeni parola**.</span><span class="sxs-lookup"><span data-stu-id="dfbec-418">Write down hello value of hello **New Password**.</span></span>
   
    <span data-ttu-id="dfbec-419">b.</span><span class="sxs-lookup"><span data-stu-id="dfbec-419">b.</span></span> <span data-ttu-id="dfbec-420">**Tamamla**’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="dfbec-420">Click **Complete**.</span></span>   

### <a name="creating-a-servicenow-test-user"></a><span data-ttu-id="dfbec-421">ServiceNow test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="dfbec-421">Creating a ServiceNow test user</span></span>
<span data-ttu-id="dfbec-422">Bu bölümde, ServiceNow içinde Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="dfbec-422">In this section, you create a user called Britta Simon in ServiceNow.</span></span> <span data-ttu-id="dfbec-423">Bu bölümde, ServiceNow içinde Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="dfbec-423">In this section, you create a user called Britta Simon in ServiceNow.</span></span> <span data-ttu-id="dfbec-424">Nasıl tooadd ServiceNow veya ServiceNow hızlı bir kullanıcı hesabı bilmiyorsanız, ServiceNow Destek ekibine başvurun.</span><span class="sxs-lookup"><span data-stu-id="dfbec-424">If you don't know how tooadd a user in your ServiceNow or ServiceNow Express account, contact ServiceNow support team.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="dfbec-425">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="dfbec-425">Assigning hello Azure AD test user</span></span>
<span data-ttu-id="dfbec-426">Bu bölümde, kendi erişim tooServiceNow vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="dfbec-426">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooServiceNow.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="dfbec-428">**tooassign Britta Simon tooServiceNow hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="dfbec-428">**tooassign Britta Simon tooServiceNow, perform hello following steps:**</span></span>

1. <span data-ttu-id="dfbec-429">Merhaba Klasik portalında hello dizin görünümünde tooopen hello uygulamaları Görüntüle'yi tıklatın **uygulamaları** hello üst menüde.</span><span class="sxs-lookup"><span data-stu-id="dfbec-429">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Kullanıcı atama][201] 

2. <span data-ttu-id="dfbec-431">Merhaba uygulamalar listesinde **ServiceNow**.</span><span class="sxs-lookup"><span data-stu-id="dfbec-431">In hello applications list, select **ServiceNow**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_10.png) 

3. <span data-ttu-id="dfbec-433">Hello içinde hello üst menüsünde **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="dfbec-433">In hello menu on hello top, click **Users**.</span></span>
   
    ![Kullanıcı atama][203] 

4. <span data-ttu-id="dfbec-435">Merhaba tüm kullanıcılar listesinden seçin **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="dfbec-435">In hello All Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="dfbec-436">Merhaba altta Hello araç çubuğunda **atamak**.</span><span class="sxs-lookup"><span data-stu-id="dfbec-436">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Kullanıcı atama][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="dfbec-438">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="dfbec-438">Testing single sign-on</span></span>
<span data-ttu-id="dfbec-439">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="dfbec-439">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="dfbec-440">Merhaba ServiceNow hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour ServiceNow uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="dfbec-440">When you click hello ServiceNow tile in hello Access Panel, you should get automatically signed-on tooyour ServiceNow application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="dfbec-441">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="dfbec-441">Additional resources</span></span>
* [<span data-ttu-id="dfbec-442">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="dfbec-442">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="dfbec-443">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="dfbec-443">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_04.png


[5]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_05.png
[6]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_06.png
[7]:  ./media/active-directory-saas-servicenow-tutorial/tutorial_general_050.png
[10]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_060.png
[11]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_070.png
[20]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_205.png
