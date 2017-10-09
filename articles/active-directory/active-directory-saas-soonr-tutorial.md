---
title: "Öğretici: Azure Active Directory Tümleştirme ile Soonr çalışma | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Soonr çalışma arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
editor: na
ms.assetid: b75f5f00-ea8b-4850-ae2e-134e5d678d97
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: f950b45d0beceab2fa17b7690c9de81ec6603089
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-soonr-workplace"></a><span data-ttu-id="62c4a-103">Öğretici: Azure Active Directory Tümleştirme ile Soonr çalışma</span><span class="sxs-lookup"><span data-stu-id="62c4a-103">Tutorial: Azure Active Directory integration with Soonr Workplace</span></span>

<span data-ttu-id="62c4a-104">Bu öğreticinin Hello hedefi olan tooshow, nasıl toointegrate Soonr çalışma Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="62c4a-104">hello objective of this tutorial is tooshow you how toointegrate Soonr Workplace with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="62c4a-105">Soonr çalışma alanına Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="62c4a-105">Integrating Soonr Workplace with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="62c4a-106">Erişim tooSoonr çalışma alanına sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="62c4a-106">You can control in Azure AD who has access tooSoonr Workplace</span></span>
- <span data-ttu-id="62c4a-107">Kullanıcıların tooautomatically get açan tooSoonr çalışma (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="62c4a-107">You can enable your users tooautomatically get signed-on tooSoonr Workplace (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="62c4a-108">Hesaplarınızı bir merkezi konumda - hello Klasik Azure portalı Yönet</span><span class="sxs-lookup"><span data-stu-id="62c4a-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="62c4a-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="62c4a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="62c4a-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="62c4a-110">Prerequisites</span></span>

<span data-ttu-id="62c4a-111">tooconfigure Soonr çalışma alanı ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="62c4a-111">tooconfigure Azure AD integration with Soonr Workplace, you need hello following items:</span></span>

- <span data-ttu-id="62c4a-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="62c4a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="62c4a-113">Bir Soonr çalışma alanı çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="62c4a-113">A Soonr Workplace single-sign on enabled subscription</span></span>


> [!NOTE] 
> <span data-ttu-id="62c4a-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="62c4a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="62c4a-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="62c4a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="62c4a-116">Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="62c4a-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="62c4a-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="62c4a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="62c4a-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="62c4a-118">Scenario description</span></span>
<span data-ttu-id="62c4a-119">Bu öğreticinin Hello hedefi olan tooenable, tootest Azure AD çoklu oturum açma bir sınama ortamında.</span><span class="sxs-lookup"><span data-stu-id="62c4a-119">hello objective of this tutorial is tooenable you tootest Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="62c4a-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="62c4a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="62c4a-121">Merhaba Galerisi'nden Soonr çalışma alanına ekleme</span><span class="sxs-lookup"><span data-stu-id="62c4a-121">Adding Soonr Workplace from hello gallery</span></span>
2. <span data-ttu-id="62c4a-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="62c4a-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-soonr-workplace-from-hello-gallery"></a><span data-ttu-id="62c4a-123">Merhaba Galerisi'nden Soonr çalışma alanına ekleme</span><span class="sxs-lookup"><span data-stu-id="62c4a-123">Adding Soonr Workplace from hello gallery</span></span>
<span data-ttu-id="62c4a-124">Azure AD'ye tooconfigure hello tümleştirme Soonr çalışma alanı tooadd Soonr çalışma alanına hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="62c4a-124">tooconfigure hello integration of Soonr Workplace into Azure AD, you need tooadd Soonr Workplace from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="62c4a-125">**tooadd Soonr çalışma hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="62c4a-125">**tooadd Soonr Workplace from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="62c4a-126">Merhaba, **Klasik Azure portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="62c4a-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="62c4a-128">Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.</span><span class="sxs-lookup"><span data-stu-id="62c4a-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="62c4a-129">Merhaba dizin görünümünde tooopen hello uygulamaları Görüntüle'yi tıklatın **uygulamaları** hello üst menüde.</span><span class="sxs-lookup"><span data-stu-id="62c4a-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>

    ![Uygulamalar][2]

4. <span data-ttu-id="62c4a-131">Tıklatın **Ekle** hello sayfanın hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="62c4a-131">Click **Add** at hello bottom of hello page.</span></span>

    ![Uygulamalar][3]

5. <span data-ttu-id="62c4a-133">Merhaba üzerinde **neler toodo istediğiniz** iletişim kutusunda, tıklatın **hello Galeriden bir uygulama eklemek**.</span><span class="sxs-lookup"><span data-stu-id="62c4a-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
 
    ![Uygulamalar][4]

6. <span data-ttu-id="62c4a-135">Merhaba arama kutusuna yazın **Soonr çalışma alanına**.</span><span class="sxs-lookup"><span data-stu-id="62c4a-135">In hello search box, type **Soonr Workplace**.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_01.png)

7. <span data-ttu-id="62c4a-137">Merhaba sonuçlar bölmesinde seçin **Soonr çalışma alanına**ve ardından **tam** tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="62c4a-137">In hello results pane, select **Soonr Workplace**, and then click **Complete** tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_02.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="62c4a-139">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="62c4a-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="62c4a-140">Bu bölümde Hello amacı olan tooshow nasıl tooconfigure ve Azure AD çoklu oturum açmayı test Soonr çalışma alanı ile temel alarak "Britta Simon" adlı bir test kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="62c4a-140">hello objective of this section is tooshow you how tooconfigure and test Azure AD single sign-on with Soonr Workplace based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="62c4a-141">Tek toowork'ın oturum açma, Azure AD hangi hello karşılık gelen kullanıcı Soonr çalışma alanına tooan kullanıcı Azure AD'de tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="62c4a-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Soonr Workplace tooan user in Azure AD is.</span></span> <span data-ttu-id="62c4a-142">Diğer bir deyişle, bir Azure AD kullanıcısının ve Soonr çalışma hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="62c4a-142">In other words, a link relationship between an Azure AD user and hello related user in Soonr Workplace needs toobe established.</span></span>  

<span data-ttu-id="62c4a-143">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** Soonr çalışma.</span><span class="sxs-lookup"><span data-stu-id="62c4a-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Soonr Workplace.</span></span>

<span data-ttu-id="62c4a-144">tooconfigure ve Soonr çalışma alanı ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="62c4a-144">tooconfigure and test Azure AD single sign-on with Soonr Workplace, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="62c4a-145">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="62c4a-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="62c4a-146">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="62c4a-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="62c4a-147">**[Soonr çalışma alanına test kullanıcısı oluşturma](#creating-a-soonr-workplace-test-user)**  -toohave karşılık gelen her bağlantılı toohello Azure AD gösterimidir Soonr çalışma Britta Simon biri.</span><span class="sxs-lookup"><span data-stu-id="62c4a-147">**[Creating a Soonr Workplace test user](#creating-a-soonr-workplace-test-user)** - toohave a counterpart of Britta Simon in Soonr Workplace that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="62c4a-148">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="62c4a-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="62c4a-149">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="62c4a-149">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="62c4a-150">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="62c4a-150">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="62c4a-151">Bu bölümde, Azure AD çoklu oturum açma hello Klasik portalında etkinleştirin ve çoklu oturum açma Soonr çalışma alanına uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="62c4a-151">In this section, you enable Azure AD single sign-on in hello classic portal and configure single sign-on in your Soonr Workplace application.</span></span>


<span data-ttu-id="62c4a-152">**tooconfigure Azure AD çoklu oturum açma Soonr çalışma ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="62c4a-152">**tooconfigure Azure AD single sign-on with Soonr Workplace, perform hello following steps:**</span></span>

1. <span data-ttu-id="62c4a-153">Hello hello üzerinde Klasik Azure portalı içinde **Soonr çalışma alanına** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma özelliğini yapılandırın** tooopen hello **yapılandırma çoklu oturum açma**  iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="62c4a-153">In hello Azure classic portal, on hello **Soonr Workplace** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>

    ![Çoklu oturum açmayı yapılandırın][6] 

2. <span data-ttu-id="62c4a-155">Merhaba üzerinde **nasıl tooSoonr çalışma alanına üzerinde kullanıcılar toosign gibi yaptığınız** sayfasında, **Azure AD çoklu oturum açma**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="62c4a-155">On hello **How would you like users toosign on tooSoonr Workplace** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_03.png) 

3. <span data-ttu-id="62c4a-157">Merhaba üzerinde **uygulama ayarlarını yapılandır** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:.</span><span class="sxs-lookup"><span data-stu-id="62c4a-157">On hello **Configure App Settings** dialog page, perform hello following steps:.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_04.png) 

    <span data-ttu-id="62c4a-159">a.</span><span class="sxs-lookup"><span data-stu-id="62c4a-159">a.</span></span> <span data-ttu-id="62c4a-160">Merhaba, **oturum üzerinde URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın: `https://<server-name>.soonr.com/singlesignon/saml/SSO`.</span><span class="sxs-lookup"><span data-stu-id="62c4a-160">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://<server-name>.soonr.com/singlesignon/saml/SSO`.</span></span>

    <span data-ttu-id="62c4a-161">b.</span><span class="sxs-lookup"><span data-stu-id="62c4a-161">b.</span></span> <span data-ttu-id="62c4a-162">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="62c4a-162">Click **Next**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="62c4a-163">Lütfen bu hello gerçek değer olmadığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="62c4a-163">Please note that this is not hello real value.</span></span> <span data-ttu-id="62c4a-164">Bu değeri hello gerçek ile oturum URL'yi tooupdate sahip.</span><span class="sxs-lookup"><span data-stu-id="62c4a-164">You have tooupdate this value with hello actual Sign On URL.</span></span> <span data-ttu-id="62c4a-165">Bu değer Soonr çalışma alanına destek ekibi tooget başvurun.</span><span class="sxs-lookup"><span data-stu-id="62c4a-165">Contact Soonr Workplace support team tooget this value.</span></span>

4. <span data-ttu-id="62c4a-166">Merhaba üzerinde **çoklu oturum açma Soonr yerindeki yapılandırma** sayfasında, **karşıdan meta veri** ve hello dosyayı bilgisayarınıza kaydedin:</span><span class="sxs-lookup"><span data-stu-id="62c4a-166">On hello **Configure single sign-on at Soonr Workplace** page, click **Download metadata** and then save hello file on your computer:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_05.png) 

5. <span data-ttu-id="62c4a-168">tooget uygulamanız için yapılandırılmış SSO Soonr çalışma alanına destek ekibinize başvurun ve ile Merhaba aşağıdakileri sağlar:</span><span class="sxs-lookup"><span data-stu-id="62c4a-168">tooget SSO configured for your application, contact your Soonr Workplace support team and provide them with hello following:</span></span> 

    <span data-ttu-id="62c4a-169">• hello indirilen **meta veri** dosyası</span><span class="sxs-lookup"><span data-stu-id="62c4a-169">•  hello downloaded **Metadata** file</span></span>

    <span data-ttu-id="62c4a-170">• hello **veren URL'si**</span><span class="sxs-lookup"><span data-stu-id="62c4a-170">•  hello **Issuer URL**</span></span>

    <span data-ttu-id="62c4a-171">• hello **SAML SSO URL'si**</span><span class="sxs-lookup"><span data-stu-id="62c4a-171">•  hello **SAML SSO URL**</span></span>

    <span data-ttu-id="62c4a-172">• hello **tek Sign-Out hizmeti URL'si**</span><span class="sxs-lookup"><span data-stu-id="62c4a-172">•  hello **Single Sign-Out Service URL**</span></span>

    >[!NOTE]
    ><span data-ttu-id="62c4a-173">Bu uygulamanın yerine geçen <a href="https://azure.microsoft.com/en-us/marketplace/partners/autotask-corporataion/autotask/">Autotask çalışma alanına</a> ve başvuruda bulunabilir <a href="https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-autotaskworkplace-tutorial">bu</a> öğretici Azure AD ile Merhaba uygulaması yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="62c4a-173">This application is superseded by <a href="https://azure.microsoft.com/en-us/marketplace/partners/autotask-corporataion/autotask/">Autotask Workplace</a> and you can refer <a href="https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-autotaskworkplace-tutorial">this</a> tutorial for configuring hello application with Azure AD.</span></span>
   
6. <span data-ttu-id="62c4a-174">Hello Klasik Azure portalı, hello tek oturum açma yapılandırması onay seçin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="62c4a-174">In hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span>

    ![Azure AD çoklu oturum açma][10]

7. <span data-ttu-id="62c4a-176">Merhaba üzerinde **tek oturum açma onay** sayfasında, **tam**.</span><span class="sxs-lookup"><span data-stu-id="62c4a-176">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
  
    ![Azure AD çoklu oturum açma][11]



### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="62c4a-178">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="62c4a-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="62c4a-179">Bu bölümde Hello amacı toocreate hello Britta Simon adlı Klasik Azure portalında bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="62c4a-179">hello objective of this section is toocreate a test user in hello Azure classic portal called Britta Simon.</span></span>  

![Azure AD Kullanıcı oluşturma][20]

<span data-ttu-id="62c4a-181">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="62c4a-181">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="62c4a-182">Merhaba, **Klasik Azure portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="62c4a-182">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-soonr-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="62c4a-184">Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.</span><span class="sxs-lookup"><span data-stu-id="62c4a-184">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="62c4a-185">toodisplay hello hello üstte hello menüde kullanıcıların listesini tıklatın **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="62c4a-185">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-soonr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="62c4a-187">tooopen hello **Kullanıcı Ekle** hello araç çubuğunda hello altta iletişim tıklatın **Kullanıcı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="62c4a-187">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-soonr-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="62c4a-189">Merhaba üzerinde **bu kullanıcı hakkında bize** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="62c4a-189">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-soonr-tutorial/create_aaduser_05.png) 

    <span data-ttu-id="62c4a-191">a.</span><span class="sxs-lookup"><span data-stu-id="62c4a-191">a.</span></span> <span data-ttu-id="62c4a-192">Kullanıcı türü olarak, kuruluşunuzdaki yeni kullanıcı seçin.</span><span class="sxs-lookup"><span data-stu-id="62c4a-192">As Type Of User, select New user in your organization.</span></span>

    <span data-ttu-id="62c4a-193">b.</span><span class="sxs-lookup"><span data-stu-id="62c4a-193">b.</span></span> <span data-ttu-id="62c4a-194">Merhaba kullanıcı adı olarak **textbox**, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="62c4a-194">In hello User Name **textbox**, type **BrittaSimon**.</span></span>

    <span data-ttu-id="62c4a-195">c.</span><span class="sxs-lookup"><span data-stu-id="62c4a-195">c.</span></span> <span data-ttu-id="62c4a-196">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="62c4a-196">Click **Next**.</span></span>

6.  <span data-ttu-id="62c4a-197">Merhaba üzerinde **kullanıcı profili** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="62c4a-197">On hello **User Profile** dialog page, perform hello following steps:</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-soonr-tutorial/create_aaduser_06.png) 

    <span data-ttu-id="62c4a-199">a.</span><span class="sxs-lookup"><span data-stu-id="62c4a-199">a.</span></span> <span data-ttu-id="62c4a-200">Merhaba, **ad** metin kutusuna, türü **Britta**.</span><span class="sxs-lookup"><span data-stu-id="62c4a-200">In hello **First Name** textbox, type **Britta**.</span></span>  

    <span data-ttu-id="62c4a-201">b.</span><span class="sxs-lookup"><span data-stu-id="62c4a-201">b.</span></span> <span data-ttu-id="62c4a-202">Merhaba, **Soyadı** metin kutusuna, türü, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="62c4a-202">In hello **Last Name** textbox, type, **Simon**.</span></span>

    <span data-ttu-id="62c4a-203">c.</span><span class="sxs-lookup"><span data-stu-id="62c4a-203">c.</span></span> <span data-ttu-id="62c4a-204">Merhaba, **görünen adı** metin kutusuna, türü **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="62c4a-204">In hello **Display Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="62c4a-205">d.</span><span class="sxs-lookup"><span data-stu-id="62c4a-205">d.</span></span> <span data-ttu-id="62c4a-206">Merhaba, **rol** listesinde **kullanıcı**.</span><span class="sxs-lookup"><span data-stu-id="62c4a-206">In hello **Role** list, select **User**.</span></span>

    <span data-ttu-id="62c4a-207">e.</span><span class="sxs-lookup"><span data-stu-id="62c4a-207">e.</span></span> <span data-ttu-id="62c4a-208">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="62c4a-208">Click **Next**.</span></span>

7. <span data-ttu-id="62c4a-209">Merhaba üzerinde **Get geçici parola** iletişim sayfasında, tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="62c4a-209">On hello **Get temporary password** dialog page, click **create**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-soonr-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="62c4a-211">Merhaba üzerinde **Get geçici parola** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="62c4a-211">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-soonr-tutorial/create_aaduser_08.png) 

    <span data-ttu-id="62c4a-213">a.</span><span class="sxs-lookup"><span data-stu-id="62c4a-213">a.</span></span> <span data-ttu-id="62c4a-214">Merhaba Hello değerini yazmak **yeni parola**.</span><span class="sxs-lookup"><span data-stu-id="62c4a-214">Write down hello value of hello **New Password**.</span></span>

    <span data-ttu-id="62c4a-215">b.</span><span class="sxs-lookup"><span data-stu-id="62c4a-215">b.</span></span> <span data-ttu-id="62c4a-216">**Tamamla**’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="62c4a-216">Click **Complete**.</span></span>   



### <a name="creating-a-soonr-workplace-test-user"></a><span data-ttu-id="62c4a-217">Soonr çalışma alanına test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="62c4a-217">Creating a Soonr Workplace test user</span></span>

<span data-ttu-id="62c4a-218">Bu bölümde Hello amacı toocreate Britta Simon Soonr çalışma alanında adlı bir kullanıcı var.</span><span class="sxs-lookup"><span data-stu-id="62c4a-218">hello objective of this section is toocreate a user called Britta Simon in Soonr Workplace.</span></span> <span data-ttu-id="62c4a-219">Lütfen bir kullanıcı hello Platform Soonr çalışma alanına destek ekibi toocreate ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="62c4a-219">Please work with Soonr Workplace support team toocreate a user in hello platform.</span></span> <span data-ttu-id="62c4a-220">Merhaba destek bileti Soonr ile yükseltebilirsiniz <a href="https://na01.safelinks.protection.outlook.com/?url=http%3A%2F%2Fsoonr.com%2FAWPHelp%2FContent%2F0_HOME%2FSupport_for_End_Clients.htm&data=01%7C01%7Cv-saikra%40microsoft.com%7Ccbb4367ab09b4dacaac408d3eebe3f42%7C72f988bf86f141af91ab2d7cd011db47%7C1&sdata=FB92qtE6m%2Fd8yox7AnL2f1h%2FGXwSkma9x9H8Pz0955M%3D&reserved=0/">burada</a>.</span><span class="sxs-lookup"><span data-stu-id="62c4a-220">You can raise hello support ticket with Soonr from <a href="https://na01.safelinks.protection.outlook.com/?url=http%3A%2F%2Fsoonr.com%2FAWPHelp%2FContent%2F0_HOME%2FSupport_for_End_Clients.htm&data=01%7C01%7Cv-saikra%40microsoft.com%7Ccbb4367ab09b4dacaac408d3eebe3f42%7C72f988bf86f141af91ab2d7cd011db47%7C1&sdata=FB92qtE6m%2Fd8yox7AnL2f1h%2FGXwSkma9x9H8Pz0955M%3D&reserved=0/">here</a>.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="62c4a-221">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="62c4a-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="62c4a-222">Merhaba amacı, bu bölümde, kendi çalışma alanına erişim tooSoonr vererek tooenabling Britta Simon toouse Azure çoklu oturum açma olur.</span><span class="sxs-lookup"><span data-stu-id="62c4a-222">hello objective of this section is tooenabling Britta Simon toouse Azure single sign-on by granting her access tooSoonr Workplace.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="62c4a-224">**tooassign Britta Simon tooSoonr çalışma alanı hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="62c4a-224">**tooassign Britta Simon tooSoonr Workplace, perform hello following steps:**</span></span>

1. <span data-ttu-id="62c4a-225">Hello üzerinde Azure Klasik portalı, hello dizin görünümünde tooopen hello uygulamaları Görünüm'e tıklayın **uygulamaları** hello üst menüde.</span><span class="sxs-lookup"><span data-stu-id="62c4a-225">On hello Azure classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="62c4a-227">Merhaba uygulamalar listesinde **Soonr çalışma alanına**.</span><span class="sxs-lookup"><span data-stu-id="62c4a-227">In hello applications list, select **Soonr Workplace**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_50.png) 

1. <span data-ttu-id="62c4a-229">Hello içinde hello üst menüsünde **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="62c4a-229">In hello menu on hello top, click **Users**.</span></span>

    ![Kullanıcı atama][203] 

1. <span data-ttu-id="62c4a-231">Merhaba kullanıcılar listesinden seçin **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="62c4a-231">In hello Users list, select **Britta Simon**.</span></span>

2. <span data-ttu-id="62c4a-232">Merhaba altta Hello araç çubuğunda **atamak**.</span><span class="sxs-lookup"><span data-stu-id="62c4a-232">In hello toolbar on hello bottom, click **Assign**.</span></span>

    ![Kullanıcı atama][205]



### <a name="testing-single-sign-on"></a><span data-ttu-id="62c4a-234">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="62c4a-234">Testing single sign-on</span></span>

<span data-ttu-id="62c4a-235">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="62c4a-235">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="62c4a-236">Soonr çalışma alanına döşeme hello erişim paneli hello tıkladığınızda, otomatik olarak oturum açma Soonr çalışma alanına uygulama tooyour almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="62c4a-236">When you click hello Soonr Workplace tile in hello Access Panel, you should get automatically signed-on tooyour Soonr Workplace application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="62c4a-237">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="62c4a-237">Additional resources</span></span>

* [<span data-ttu-id="62c4a-238">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="62c4a-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="62c4a-239">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="62c4a-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_205.png
