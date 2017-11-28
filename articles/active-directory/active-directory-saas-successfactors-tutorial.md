---
title: "Öğretici: Azure Active Directory Tümleştirme ile SuccessFactors | Microsoft Docs"
description: "Azure Active Directory tooenable ile toouse SuccessFactors nasıl tek oturum açma, otomatik sağlama ve daha fazlasını öğrenin!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 32bd8898-c2d2-4aa7-8c46-f1f5c2aa05f1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 3f7895d7d5e26fda27f555ae2f14a1645b50dcba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-successfactors"></a><span data-ttu-id="6d8f2-103">Öğretici: Azure Active Directory Tümleştirme SuccessFactors ile</span><span class="sxs-lookup"><span data-stu-id="6d8f2-103">Tutorial: Azure Active Directory integration with SuccessFactors</span></span>
<span data-ttu-id="6d8f2-104">Bu öğreticinin Hello hedefi olan tooshow, nasıl toointegrate SuccessFactors Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6d8f2-104">hello objective of this tutorial is tooshow you how toointegrate SuccessFactors with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6d8f2-105">SuccessFactors Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="6d8f2-105">Integrating SuccessFactors with Azure AD provides you with hello following benefits:</span></span>

* <span data-ttu-id="6d8f2-106">Erişim tooSuccessFactors sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="6d8f2-106">You can control in Azure AD who has access tooSuccessFactors</span></span>
* <span data-ttu-id="6d8f2-107">Kullanıcıların tooautomatically get açan tooSuccessFactors (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="6d8f2-107">You can enable your users tooautomatically get signed-on tooSuccessFactors (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="6d8f2-108">Hesaplarınızı bir merkezi konumda - hello Klasik Azure portalı Yönet</span><span class="sxs-lookup"><span data-stu-id="6d8f2-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="6d8f2-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6d8f2-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6d8f2-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="6d8f2-110">Prerequisites</span></span>
<span data-ttu-id="6d8f2-111">tooconfigure SuccessFactors ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="6d8f2-111">tooconfigure Azure AD integration with SuccessFactors, you need hello following items:</span></span>

* <span data-ttu-id="6d8f2-112">Geçerli bir Azure aboneliği</span><span class="sxs-lookup"><span data-stu-id="6d8f2-112">A valid Azure subscription</span></span>
* <span data-ttu-id="6d8f2-113">Bir kiracı SuccessFactors içinde</span><span class="sxs-lookup"><span data-stu-id="6d8f2-113">A tenant in SuccessFactors</span></span>

> [!NOTE]
> <span data-ttu-id="6d8f2-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="6d8f2-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="6d8f2-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="6d8f2-116">Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="6d8f2-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6d8f2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6d8f2-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="6d8f2-118">Scenario description</span></span>
<span data-ttu-id="6d8f2-119">Bu öğreticinin Hello hedefi olan tooenable, tootest Azure AD çoklu oturum açma bir sınama ortamında.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-119">hello objective of this tutorial is tooenable you tootest Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="6d8f2-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="6d8f2-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6d8f2-121">Merhaba Galerisi'nden SuccessFactors ekleme</span><span class="sxs-lookup"><span data-stu-id="6d8f2-121">Adding SuccessFactors from hello gallery</span></span>
2. <span data-ttu-id="6d8f2-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="6d8f2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-successfactors-from-hello-gallery"></a><span data-ttu-id="6d8f2-123">Merhaba Galerisi'nden SuccessFactors ekleme</span><span class="sxs-lookup"><span data-stu-id="6d8f2-123">Adding SuccessFactors from hello gallery</span></span>
<span data-ttu-id="6d8f2-124">Azure AD'ye tooconfigure hello tümleştirme SuccessFactors, tooadd SuccessFactors hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-124">tooconfigure hello integration of SuccessFactors into Azure AD, you need tooadd SuccessFactors from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6d8f2-125">**tooadd SuccessFactors hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6d8f2-125">**tooadd SuccessFactors from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6d8f2-126">Merhaba hello sol gezinti bölmesinde, Klasik Azure portalı tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-126">In hello Azure classic portal, on hello left navigation panel, click **Active Directory**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırma][1]
2. <span data-ttu-id="6d8f2-128">Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="6d8f2-129">Merhaba dizin görünümünde tooopen hello uygulamaları Görüntüle'yi tıklatın **uygulamaları** hello üst menüde.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Çoklu oturum açmayı yapılandırma][2]
4. <span data-ttu-id="6d8f2-131">Tıklatın **Ekle** hello sayfanın hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Uygulamalar][3]
5. <span data-ttu-id="6d8f2-133">Merhaba üzerinde **neler toodo istediğiniz** iletişim kutusunda, tıklatın **hello Galeriden bir uygulama eklemek**.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırma][4]
6. <span data-ttu-id="6d8f2-135">Merhaba, **arama kutusu**, türü **SuccessFactors**.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-135">In hello **search box**, type **SuccessFactors**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırma][5]
7. <span data-ttu-id="6d8f2-137">Merhaba Sonuçlar panelinde seçin **SuccessFactors**ve ardından **tam** tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-137">In hello results panel, select **SuccessFactors**, and then click **Complete** tooadd hello application.</span></span>
   
    ![Çoklu oturum açmayı yapılandırma][6]

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6d8f2-139">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="6d8f2-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6d8f2-140">Bu bölümde Hello amacı olan tooshow nasıl tooconfigure ve Azure AD çoklu oturum açmayı test SuccessFactors ile temel alarak "Britta Simon" adlı bir test kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-140">hello objective of this section is tooshow you how tooconfigure and test Azure AD single sign-on with SuccessFactors based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6d8f2-141">Tek toowork'ın oturum açma, Azure AD hangi hello karşılık gelen kullanıcı SuccessFactors tooan kullanıcı Azure AD'de tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SuccessFactors tooan user in Azure AD is.</span></span> <span data-ttu-id="6d8f2-142">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı SuccessFactors hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-142">In other words, a link relationship between an Azure AD user and hello related user in SuccessFactors needs toobe established.</span></span>

<span data-ttu-id="6d8f2-143">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** SuccessFactors içinde.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in SuccessFactors.</span></span>

<span data-ttu-id="6d8f2-144">tooconfigure ve SuccessFactors ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="6d8f2-144">tooconfigure and test Azure AD single sign-on with SuccessFactors, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6d8f2-145">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6d8f2-146">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6d8f2-147">**[SuccessFactors test kullanıcısı oluşturma](#creating-a-successfactors-test-user)**  -toohave karşılık gelen her bağlantılı toohello Azure AD gösterimidir SuccessFactors içinde Britta Simon biri.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-147">**[Creating a SuccessFactors test user](#creating-a-successfactors-test-user)** - toohave a counterpart of Britta Simon in SuccessFactors that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="6d8f2-148">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6d8f2-149">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-149">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6d8f2-150">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="6d8f2-150">Configuring Azure AD single sign-on</span></span>
<span data-ttu-id="6d8f2-151">Bu bölümde, Azure AD çoklu oturum açma hello Klasik portalında etkinleştirin ve çoklu oturum açma SuccessFactors uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-151">In this section, you enable Azure AD single sign-on in hello classic portal and configure single sign-on in your SuccessFactors application.</span></span>

<span data-ttu-id="6d8f2-152">**tooconfigure Azure AD çoklu oturum açma ile SuccessFactors, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6d8f2-152">**tooconfigure Azure AD single sign-on with SuccessFactors, perform hello following steps:**</span></span>

1. <span data-ttu-id="6d8f2-153">Merhaba hello üzerinde Klasik Azure portalı içinde **SuccessFactors** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma özelliğini yapılandırın** tooopen hello **tek oturum yapılandırma üzerinde aktar** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-153">In hello Azure classic portal, on hello **SuccessFactors** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
    ![Çoklu oturum açmayı yapılandırma][7]
2. <span data-ttu-id="6d8f2-155">Merhaba üzerinde **nasıl tooSuccessFactors üzerinde kullanıcılar toosign gibi yaptığınız** sayfasında, **Microsoft Azure AD çoklu oturum açma**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-155">On hello **How would you like users toosign on tooSuccessFactors** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırma][8]
3. <span data-ttu-id="6d8f2-157">Merhaba üzerinde **uygulama URL'sini Yapılandır** sayfasında, aşağıdaki adımları hello gerçekleştirmek ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-157">On hello **Configure App URL** page, perform hello following steps, and then click **Next**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırma][9]
   
    <span data-ttu-id="6d8f2-159">a.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-159">a.</span></span> <span data-ttu-id="6d8f2-160">Merhaba, **oturum üzerinde URL'si** metin kutusuna, URL desenlerini aşağıdaki hello birini kullanarak bir yazın:</span><span class="sxs-lookup"><span data-stu-id="6d8f2-160">In hello **Sign On URL** textbox, type a URL using one of hello following patterns:</span></span> 
   
    |  |
    | --- |
    | `https://<company name>.successfactors.com/<company name>` |
    | `https://<company name>.sapsf.com/<company name>` |
    | `https://<company name>.successfactors.eu/<company name>` |
    | `https://<company name>.sapsf.eu` |
   
    <span data-ttu-id="6d8f2-161">b.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-161">b.</span></span> <span data-ttu-id="6d8f2-162">Merhaba, **yanıt URL'si** metin kutusuna, URL desenlerini aşağıdaki hello birini kullanarak bir yazın:</span><span class="sxs-lookup"><span data-stu-id="6d8f2-162">In hello **Reply URL** textbox, type a URL using one of hello following patterns:</span></span> 
   
    |  |
    | --- |
    | `https://<company name>.successfactors.com/<company name>` |
    | `https://<company name>.sapsf.com/<company name>` |
    | `https://<company name>.successfactors.eu/<company name>` |
    | `https://<company name>.sapsf.eu` |
    | `https://<company name>.sapsf.eu/<company name>` |
   
    <span data-ttu-id="6d8f2-163">c.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-163">c.</span></span> <span data-ttu-id="6d8f2-164">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-164">Click **Next**.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="6d8f2-165">Lütfen bu hello gerçek değerler olmadığına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-165">Please note that these are not hello real values.</span></span> <span data-ttu-id="6d8f2-166">Tooupdate hello gerçek oturum üzerinde URL'si ve yanıt URL'si ile bu değerlere sahip.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-166">You have tooupdate these values with hello actual Sign On URL and Reply URL.</span></span> <span data-ttu-id="6d8f2-167">Bu değerleri tooget başvurun [SuccessFactors destek ekibi](https://www.successfactors.com/en_us/support.html).</span><span class="sxs-lookup"><span data-stu-id="6d8f2-167">tooget these values, contact [SuccessFactors support team](https://www.successfactors.com/en_us/support.html).</span></span>

1. <span data-ttu-id="6d8f2-168">Merhaba üzerinde **çoklu oturum açma sırasında SuccessFactors yapılandırma** sayfasında, **indirme sertifika**ve yerel olarak bilgisayarınızda hello sertifika dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-168">On hello **Configure single sign-on at SuccessFactors** page, click **Download certificate**, and then save hello certificate file locally on your computer.</span></span>
   
    ![Çoklu oturum açmayı yapılandırma][10]

2. <span data-ttu-id="6d8f2-170">Farklı web tarayıcısı penceresinde oturum açın, **SuccessFactors Yönetici portalı** yönetici olarak.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-170">In a different web browser window, log into your **SuccessFactors admin portal** as an administrator.</span></span>

3. <span data-ttu-id="6d8f2-171">Ziyaret **uygulama güvenliği** ve yerel çok**tek oturum açma özelliğini**.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-171">Visit **Application Security** and native too**Single Sign On Feature**.</span></span> 

4. <span data-ttu-id="6d8f2-172">Herhangi bir değer hello yerleştirin **sıfırlama belirteci** tıklatıp **Kaydet belirteci** tooenable SAML SSO.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-172">Place any value in hello **Reset Token** and click **Save Token** tooenable SAML SSO.</span></span>
   
    ![Çoklu oturum açma uygulama tarafında yapılandırma][11]

    > [!NOTE] 
    > <span data-ttu-id="6d8f2-174">Bu değer yalnızca başlangıç anahtarı açık/kapalı olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-174">This value is just used as hello on/off switch.</span></span> <span data-ttu-id="6d8f2-175">Herhangi bir değer kaydettiyseniz hello SAML SSO açık'tır.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-175">If any value is saved, hello SAML SSO is ON.</span></span> <span data-ttu-id="6d8f2-176">Boş bir değer kaydettiyseniz hello SAML SSO Kapalı'dır.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-176">If a blank value is saved hello SAML SSO is OFF.</span></span>

1. <span data-ttu-id="6d8f2-177">Yerel toobelow ekran ve hello aşağıdaki eylemleri gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-177">Native toobelow screenshot and perform hello following actions.</span></span>
   
    ![Çoklu oturum açma uygulama tarafında yapılandırma][12]
   
    <span data-ttu-id="6d8f2-179">a.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-179">a.</span></span> <span data-ttu-id="6d8f2-180">Select hello **SAML v2 SSO** radyo düğmesi</span><span class="sxs-lookup"><span data-stu-id="6d8f2-180">Select hello **SAML v2 SSO** Radio Button</span></span>
   
    <span data-ttu-id="6d8f2-181">b.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-181">b.</span></span> <span data-ttu-id="6d8f2-182">Merhaba SAML sunduğundan taraf Name(e.g. SAml issuer + company name) ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-182">Set hello SAML Asserting Party Name(e.g. SAml issuer + company name).</span></span>
   
    <span data-ttu-id="6d8f2-183">c.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-183">c.</span></span> <span data-ttu-id="6d8f2-184">Merhaba, **SAML veren** textbox put hello değerini **veren URL'si** Azure AD Uygulama Yapılandırma Sihirbazı'ndan.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-184">In hello **SAML Issuer** textbox put hello value of **Issuer URL** from Azure AD application configuration wizard.</span></span>
   
    <span data-ttu-id="6d8f2-185">d.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-185">d.</span></span> <span data-ttu-id="6d8f2-186">Seçin **yanıt (müşteri oluşturulan/IDP/AP)** olarak **zorunlu imza gerektir**.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-186">Select **Response(Customer Generated/IdP/AP)** as **Require Mandatory Signature**.</span></span>
   
    <span data-ttu-id="6d8f2-187">e.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-187">e.</span></span> <span data-ttu-id="6d8f2-188">Seçin **etkin** olarak **etkinleştirmek SAML bayrağı**.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-188">Select **Enabled** as **Enable SAML Flag**.</span></span>
   
    <span data-ttu-id="6d8f2-189">f.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-189">f.</span></span> <span data-ttu-id="6d8f2-190">Seçin **Hayır** olarak **oturum açma isteği imza (BT oluşturulan/SP/RP)**.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-190">Select **No** as **Login Request Signature(SF Generated/SP/RP)**.</span></span>
   
    <span data-ttu-id="6d8f2-191">g.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-191">g.</span></span> <span data-ttu-id="6d8f2-192">Seçin **tarayıcı/Post profili** olarak **SAML profili**.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-192">Select **Browser/Post Profile** as **SAML Profile**.</span></span>
   
    <span data-ttu-id="6d8f2-193">h.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-193">h.</span></span> <span data-ttu-id="6d8f2-194">Seçin **Hayır** olarak **sertifika geçerli süresi zorunlu**.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-194">Select **No** as **Enforce Certificate Valid Period**.</span></span>
   
    <span data-ttu-id="6d8f2-195">ı.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-195">i.</span></span> <span data-ttu-id="6d8f2-196">Merhaba hello indirilen sertifika dosyasının içeriğini kopyalayın ve hello yapıştırma **SAML doğrulama sertifikası** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-196">Copy hello content of hello downloaded certificate file, and then paste it into hello **SAML Verifying Certificate** textbox.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6d8f2-197">Merhaba sertifika içeriğini sahip başlamalıdır sertifika ve bitiş sertifika etiketler.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-197">hello certificate content must have begin certificate and end certificate tags.</span></span>

1. <span data-ttu-id="6d8f2-198">TooSAML V2 gidin ve ardından hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="6d8f2-198">Navigate tooSAML V2, and then perform hello following steps:</span></span>
   
    ![Çoklu oturum açma uygulama tarafında yapılandırma][13]
   
    <span data-ttu-id="6d8f2-200">a.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-200">a.</span></span> <span data-ttu-id="6d8f2-201">Seçin **Evet** olarak **destek SP tarafından başlatılan genel oturum kapatma**.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-201">Select **Yes** as **Support SP-initiated Global Logout**.</span></span>
   
    <span data-ttu-id="6d8f2-202">b.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-202">b.</span></span> <span data-ttu-id="6d8f2-203">Merhaba, **genel oturum kapatma hizmeti URL'si (LogoutRequest hedef)** textbox put hello değerini **uzak oturum kapatma URL'si** Azure AD Uygulama Yapılandırma Sihirbazı'ndan.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-203">In hello **Global Logout Service URL (LogoutRequest destination)** textbox put hello value of **Remote Logout URL** from Azure AD application configuration wizard.</span></span>
   
    <span data-ttu-id="6d8f2-204">c.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-204">c.</span></span> <span data-ttu-id="6d8f2-205">Seçin **Hayır** olarak **sp tüm NameID öğesi şifrelemek gerekir gerektiren**.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-205">Select **No** as **Require sp must encrypt all NameID element**.</span></span>
   
    <span data-ttu-id="6d8f2-206">d.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-206">d.</span></span> <span data-ttu-id="6d8f2-207">Seçin **belirtilmeyen** olarak **NameID biçimi**.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-207">Select **unspecified** as **NameID Format**.</span></span>
   
    <span data-ttu-id="6d8f2-208">e.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-208">e.</span></span> <span data-ttu-id="6d8f2-209">Seçin **Evet** olarak **etkinleştir sp tarafından başlatılan oturum açma (AuthnRequest)**.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-209">Select **Yes** as **Enable sp initiated login (AuthnRequest)**.</span></span>
   
    <span data-ttu-id="6d8f2-210">f.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-210">f.</span></span> <span data-ttu-id="6d8f2-211">Merhaba, **şirket çapında veren olarak gönderme isteği** textbox put hello değerini **uzaktan oturum açma URL'si** Azure AD Uygulama Yapılandırma Sihirbazı'ndan.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-211">In hello **Send request as Company-Wide issuer** textbox put hello value of **Remote Login URL** from Azure AD application configuration wizard.</span></span>
2. <span data-ttu-id="6d8f2-212">Toomake hello oturum açma kullanıcı adları istiyorsanız aşağıdaki adımları gerçekleştirin büyük küçük harf duyarsız.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-212">Perform these steps if you want toomake hello login usernames Case Insensitive, .</span></span>
   
    <span data-ttu-id="6d8f2-213">a.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-213">a.</span></span> <span data-ttu-id="6d8f2-214">Ziyaret **şirket ayarları**(yakın hello alt).</span><span class="sxs-lookup"><span data-stu-id="6d8f2-214">Visit **Company Settings**(near hello bottom).</span></span>
   
    <span data-ttu-id="6d8f2-215">b.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-215">b.</span></span> <span data-ttu-id="6d8f2-216">yakın onay kutusunu seçin **etkinleştirmek olmayan durumda duyarlı kullanıcıadı**.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-216">select checkbox near **Enable Non-Case-Sensitive Username**.</span></span>
   
    <span data-ttu-id="6d8f2-217">c.Click **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-217">c.Click **Save**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın][29]

    > [!NOTE] 
    > <span data-ttu-id="6d8f2-219">Bu tooenable çalışırsanız, yinelenen bir SAML oturum açma adı oluşturur, hello sistem denetler.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-219">If you try tooenable this, hello system checks if it will create a duplicate SAML login name.</span></span> <span data-ttu-id="6d8f2-220">Kullanıcı adları Kullanıcı1 hem Kullanıcı1 Hello müşteri varsa, örneğin.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-220">For example if hello customer has usernames User1 and user1.</span></span> <span data-ttu-id="6d8f2-221">Büyük küçük harfe duyarlılığın hemen alma bu yinelemeleri yapar.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-221">Taking away case sensitivity makes these duplicates.</span></span> <span data-ttu-id="6d8f2-222">Merhaba sistem bir hata iletisi alır ve hello özelliği izin vermez.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-222">hello system will give you an error message and will not enable hello feature.</span></span> <span data-ttu-id="6d8f2-223">gerçekte yazılmış şekilde hello müşteri toochange hello kullanıcı adları birini farklı gerekir.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-223">hello customer will need toochange one of hello usernames so it’s actually spelled different.</span></span> 

1. <span data-ttu-id="6d8f2-224">Hello Klasik Azure portalı, hello tek oturum açma yapılandırması onay seçin ve ardından **tam** tooclose hello **tek oturum yapılandırma üzerinde aktar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-224">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
   
    ![Uygulamalar][14]
2. <span data-ttu-id="6d8f2-226">Merhaba üzerinde **tek oturum açma onay** sayfasında, **tam**.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-226">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    ![Uygulamalar][15]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6d8f2-228">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6d8f2-228">Creating an Azure AD test user</span></span>
<span data-ttu-id="6d8f2-229">Bu bölümde Hello amacı toocreate bir test kullanıcısı Britta Simon adlı hello Klasik Portalı'nda ' dir.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-229">hello objective of this section is toocreate a test user in hello classic portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][16]

<span data-ttu-id="6d8f2-231">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6d8f2-231">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6d8f2-232">Merhaba, **Klasik Azure portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-232">In hello **Azure classic Portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma][17]
2. <span data-ttu-id="6d8f2-234">Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-234">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="6d8f2-235">toodisplay hello hello üstte hello menüde kullanıcıların listesini tıklatın **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-235">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma][18]
4. <span data-ttu-id="6d8f2-237">tooopen hello **Kullanıcı Ekle** hello araç çubuğunda hello altta iletişim tıklatın **Kullanıcı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-237">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma][19]
5. <span data-ttu-id="6d8f2-239">Merhaba üzerinde **bu kullanıcı hakkında bize** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="6d8f2-239">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma][20]
   
    <span data-ttu-id="6d8f2-241">a.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-241">a.</span></span> <span data-ttu-id="6d8f2-242">Kullanıcı türü olarak, kuruluşunuzdaki yeni kullanıcı seçin.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-242">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="6d8f2-243">b.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-243">b.</span></span> <span data-ttu-id="6d8f2-244">Merhaba kullanıcı adı olarak **textbox**, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-244">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="6d8f2-245">c.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-245">c.</span></span> <span data-ttu-id="6d8f2-246">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-246">Click **Next**.</span></span>
6. <span data-ttu-id="6d8f2-247">Merhaba üzerinde **kullanıcı profili** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="6d8f2-247">On hello **User Profile** dialog page, perform hello following steps:</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma][21]
   
    <span data-ttu-id="6d8f2-249">a.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-249">a.</span></span> <span data-ttu-id="6d8f2-250">Merhaba, **ad** metin kutusuna, türü **Britta**.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-250">In hello **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="6d8f2-251">b.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-251">b.</span></span> <span data-ttu-id="6d8f2-252">Merhaba, **Soyadı** metin kutusuna, türü, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-252">In hello **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="6d8f2-253">c.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-253">c.</span></span> <span data-ttu-id="6d8f2-254">Merhaba, **görünen adı** metin kutusuna, türü **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-254">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="6d8f2-255">d.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-255">d.</span></span> <span data-ttu-id="6d8f2-256">Merhaba, **rol** listesinde **kullanıcı**.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-256">In hello **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="6d8f2-257">e.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-257">e.</span></span> <span data-ttu-id="6d8f2-258">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-258">Click **Next**.</span></span>
7. <span data-ttu-id="6d8f2-259">Merhaba üzerinde **Get geçici parola** iletişim sayfasında, tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-259">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma][22]
8. <span data-ttu-id="6d8f2-261">Merhaba üzerinde **Get geçici parola** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="6d8f2-261">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma][23]
   
    <span data-ttu-id="6d8f2-263">a.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-263">a.</span></span> <span data-ttu-id="6d8f2-264">Merhaba Hello değerini yazmak **yeni parola**.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-264">Write down hello value of hello **New Password**.</span></span>
   
    <span data-ttu-id="6d8f2-265">b.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-265">b.</span></span> <span data-ttu-id="6d8f2-266">**Tamamla**’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-266">Click **Complete**.</span></span>  

### <a name="creating-a-successfactors-test-user"></a><span data-ttu-id="6d8f2-267">SuccessFactors test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6d8f2-267">Creating a SuccessFactors test user</span></span>
<span data-ttu-id="6d8f2-268">SuccessFactors içine sipariş tooenable Azure AD kullanıcıların toolog bunların SuccessFactors sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-268">In order tooenable Azure AD users toolog into SuccessFactors, they must be provisioned into SuccessFactors.</span></span>  
<span data-ttu-id="6d8f2-269">SuccessFactors Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-269">In hello case of SuccessFactors, provisioning is a manual task.</span></span>

<span data-ttu-id="6d8f2-270">SuccessFactors içinde oluşturulan tooget kullanıcıların toocontact hello ihtiyacınız [SuccessFactors destek ekibi](https://www.successfactors.com/en_us/support.html).</span><span class="sxs-lookup"><span data-stu-id="6d8f2-270">tooget users created in SuccessFactors, you need toocontact hello [SuccessFactors support team](https://www.successfactors.com/en_us/support.html).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="6d8f2-271">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="6d8f2-271">Assigning hello Azure AD test user</span></span>
<span data-ttu-id="6d8f2-272">Bu bölümde Hello amacı kendi erişim tooSuccessFactors vererek tooenabling Britta Simon toouse Azure çoklu oturum açma olur.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-272">hello objective of this section is tooenabling Britta Simon toouse Azure single sign-on by granting her access tooSuccessFactors.</span></span>

![Kullanıcı atama][24]

<span data-ttu-id="6d8f2-274">**tooassign Britta Simon tooSuccessFactors hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6d8f2-274">**tooassign Britta Simon tooSuccessFactors, perform hello following steps:**</span></span>

1. <span data-ttu-id="6d8f2-275">Merhaba Klasik portalında hello dizin görünümünde tooopen hello uygulamaları Görüntüle'yi tıklatın **uygulamaları** hello üst menüde.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-275">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Kullanıcı atama][25]
2. <span data-ttu-id="6d8f2-277">Merhaba uygulamalar listesinde **SuccessFactors**.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-277">In hello applications list, select **SuccessFactors**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın][26]
3. <span data-ttu-id="6d8f2-279">Hello içinde hello üst menüsünde **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-279">In hello menu on hello top, click **Users**.</span></span>
   
    ![Kullanıcı atama][27]
4. <span data-ttu-id="6d8f2-281">Merhaba kullanıcılar listesinden seçin **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-281">In hello Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="6d8f2-282">Merhaba altta Hello araç çubuğunda **atamak**.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-282">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Kullanıcı atama][28]

### <a name="testing-single-sign-on"></a><span data-ttu-id="6d8f2-284">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="6d8f2-284">Testing single sign-on</span></span>
<span data-ttu-id="6d8f2-285">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-285">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="6d8f2-286">Hello erişim paneli SuccessFactors döşeme hello tıkladığınızda, otomatik olarak oturum açma SuccessFactors uygulama tooyour almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6d8f2-286">When you click hello SuccessFactors tile in hello Access Panel, you should get automatically signed-on tooyour SuccessFactors application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6d8f2-287">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="6d8f2-287">Additional resources</span></span>
* [<span data-ttu-id="6d8f2-288">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="6d8f2-288">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6d8f2-289">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="6d8f2-289">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[0]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_00.png
[1]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_01.png
[6]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_02.png
[7]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_03.png
[8]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_04.png
[9]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_05.png
[10]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_06.png

[11]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_07.png
[12]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_08.png
[13]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_09.png
[14]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_05.png
[15]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_06.png

[16]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_00.png
[17]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_01.png
[18]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_02.png
[19]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_03.png
[20]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_04.png
[21]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_05.png
[22]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_06.png
[23]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_07.png

[24]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_07.png
[25]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_08.png
[26]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_11.png
[27]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_09.png
[28]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_10.png
[29]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_10.png
