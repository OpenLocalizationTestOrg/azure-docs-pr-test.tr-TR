---
title: "Öğretici: Azure Active Directory Tümleştirme Questetra BPM Suite ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve Questetra BPM Suite arasında."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: fb6d5b73-e491-4dd2-92d6-94e5aba21465
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/14/2017
ms.author: jeedes
ms.openlocfilehash: 4907e3b5751cd79f994fbd2ebcb7faec4eac34e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-questetra-bpm-suite"></a><span data-ttu-id="a4a37-103">Öğretici: Azure Active Directory Tümleştirme Questetra BPM Suite ile</span><span class="sxs-lookup"><span data-stu-id="a4a37-103">Tutorial: Azure Active Directory integration with Questetra BPM Suite</span></span>
<span data-ttu-id="a4a37-104">Bu öğreticinin Hello hedefi olan tooshow, nasıl toointegrate Questetra BPM Suite Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a4a37-104">hello objective of this tutorial is tooshow you how toointegrate Questetra BPM Suite with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="a4a37-105">Questetra BPM Suite Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="a4a37-105">Integrating Questetra BPM Suite with Azure AD provides you with hello following benefits:</span></span> 

* <span data-ttu-id="a4a37-106">Erişim tooQuestetra BPM paketine sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="a4a37-106">You can control in Azure AD who has access tooQuestetra BPM Suite</span></span> 
* <span data-ttu-id="a4a37-107">Azure AD hesaplarına ile kullanıcılar tooautomatically get açan tooQuestetra (çoklu oturum açma) BPM Suite etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="a4a37-107">You can enable your users tooautomatically get signed-on tooQuestetra BPM Suite (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="a4a37-108">Hesaplarınızı bir merkezi konumda - hello Klasik Azure portalı Yönet</span><span class="sxs-lookup"><span data-stu-id="a4a37-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="a4a37-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a4a37-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a4a37-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="a4a37-110">Prerequisites</span></span>
<span data-ttu-id="a4a37-111">tooconfigure Questetra BPM Suite ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="a4a37-111">tooconfigure Azure AD integration with Questetra BPM Suite, you need hello following items:</span></span>

* <span data-ttu-id="a4a37-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="a4a37-112">An Azure AD subscription</span></span>
* <span data-ttu-id="a4a37-113">Bir [Questetra BPM Suite](https://senbon-imadegawa-988.questetra.net/) çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="a4a37-113">An [Questetra BPM Suite](https://senbon-imadegawa-988.questetra.net/) single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a4a37-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="a4a37-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="a4a37-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="a4a37-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="a4a37-116">Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a4a37-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="a4a37-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a4a37-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="a4a37-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="a4a37-118">Scenario Description</span></span>
<span data-ttu-id="a4a37-119">Bu öğreticinin Hello hedefi olan tooenable, tootest Azure AD çoklu oturum açma bir sınama ortamında.</span><span class="sxs-lookup"><span data-stu-id="a4a37-119">hello objective of this tutorial is tooenable you tootest Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="a4a37-120">Bu öğreticide gösterilen hello senaryo üç ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="a4a37-120">hello scenario outlined in this tutorial consists of three main building blocks:</span></span>

1. <span data-ttu-id="a4a37-121">Merhaba Galerisi'nden Questetra BPM paketi ekleme</span><span class="sxs-lookup"><span data-stu-id="a4a37-121">Adding Questetra BPM Suite from hello gallery</span></span> 
2. <span data-ttu-id="a4a37-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="a4a37-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-questetra-bpm-suite-from-hello-gallery"></a><span data-ttu-id="a4a37-123">Merhaba Galerisi'nden Questetra BPM paketi ekleme</span><span class="sxs-lookup"><span data-stu-id="a4a37-123">Adding Questetra BPM Suite from hello gallery</span></span>
<span data-ttu-id="a4a37-124">Azure AD'ye tooconfigure hello tümleştirme Questetra BPM paketinin tooadd Questetra BPM Suite hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="a4a37-124">tooconfigure hello integration of Questetra BPM Suite into Azure AD, you need tooadd Questetra BPM Suite from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a4a37-125">**tooadd Questetra BPM hello galeri paketinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a4a37-125">**tooadd Questetra BPM Suite from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a4a37-126">Merhaba, **Klasik Azure portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a4a37-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="a4a37-128">Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.</span><span class="sxs-lookup"><span data-stu-id="a4a37-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="a4a37-129">Merhaba dizin görünümünde tooopen hello uygulamaları Görüntüle'yi tıklatın **uygulamaları** hello üst menüde.</span><span class="sxs-lookup"><span data-stu-id="a4a37-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Uygulamalar][2]

4. <span data-ttu-id="a4a37-131">Tıklatın **Ekle** hello sayfanın hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="a4a37-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Uygulamalar][3]

5. <span data-ttu-id="a4a37-133">Merhaba üzerinde **neler toodo istediğiniz** iletişim kutusunda, tıklatın **hello Galeriden bir uygulama eklemek**.</span><span class="sxs-lookup"><span data-stu-id="a4a37-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Uygulamalar][4]

6. <span data-ttu-id="a4a37-135">Merhaba arama kutusuna yazın **Questetra BPM Suite**.</span><span class="sxs-lookup"><span data-stu-id="a4a37-135">In hello search box, type **Questetra BPM Suite**.</span></span>
   
    ![Uygulamalar][5]

7. <span data-ttu-id="a4a37-137">Merhaba sonuçlar bölmesinde seçin **Questetra BPM Suite**ve ardından **tam** tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="a4a37-137">In hello results pane, select **Questetra BPM Suite**, and then click **Complete** tooadd hello application.</span></span>

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a4a37-138">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="a4a37-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a4a37-139">Bu bölümde Hello amacı olan tooshow nasıl tooconfigure ve Questetra BPM Suite ile Azure AD çoklu oturum açmayı test temel alarak "Britta Simon" adlı bir test kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="a4a37-139">hello objective of this section is tooshow you how tooconfigure and test Azure AD single sign-on with Questetra BPM Suite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a4a37-140">Tek toowork'ın oturum açma, Azure AD hangi hello karşılık gelen kullanıcı Questetra BPM Suite tooan kullanıcı Azure AD'de tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="a4a37-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Questetra BPM Suite tooan user in Azure AD is.</span></span> <span data-ttu-id="a4a37-141">Diğer bir deyişle, bir Azure AD kullanıcısının ve Questetra BPM paketindeki hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="a4a37-141">In other words, a link relationship between an Azure AD user and hello related user in Questetra BPM Suite needs toobe established.</span></span>  
<span data-ttu-id="a4a37-142">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** Questetra BPM paketindeki.</span><span class="sxs-lookup"><span data-stu-id="a4a37-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Questetra BPM Suite.</span></span>

<span data-ttu-id="a4a37-143">tooconfigure ve Questetra BPM Suite ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="a4a37-143">tooconfigure and test Azure AD single sign-on with Questetra BPM Suite, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a4a37-144">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="a4a37-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a4a37-145">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="a4a37-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a4a37-146">**[Questetra BPM Suite test kullanıcısı oluşturma](#creating-a-questetra-bpm-suite-test-user)**  -toohave karşılık gelen, Britta Simon Questetra BPM paketindeki, her bağlı toohello Azure AD gösterimidir.</span><span class="sxs-lookup"><span data-stu-id="a4a37-146">**[Creating a Questetra BPM Suite test user](#creating-a-questetra-bpm-suite-test-user)** - toohave a counterpart of Britta Simon in Questetra BPM Suite that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="a4a37-147">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="a4a37-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a4a37-148">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="a4a37-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a4a37-149">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a4a37-149">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="a4a37-150">Bu bölümde Hello amacı tooenable Azure AD çoklu oturum açma hello Klasik Azure Portalı'nda ve tooconfigure çoklu oturum açma Questetra BPM Suite uygulamanızda ' dir.</span><span class="sxs-lookup"><span data-stu-id="a4a37-150">hello objective of this section is tooenable Azure AD single sign-on in hello Azure classic portal and tooconfigure single sign-on in your Questetra BPM Suite application.</span></span>

<span data-ttu-id="a4a37-151">**Azure AD çoklu oturum açma tooconfigure Questetra BPM Suite ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a4a37-151">**tooconfigure Azure AD single sign-on with Questetra BPM Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="a4a37-152">Hello hello üzerinde Klasik Azure portalı içinde **Questetra BPM Suite** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma özelliğini yapılandırın** tooopen hello **yapılandırma çoklu oturum açma**  iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="a4a37-152">In hello Azure classic portal, on hello **Questetra BPM Suite** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın][8]

2. <span data-ttu-id="a4a37-154">Merhaba üzerinde **nasıl tooQuestetra BPM paketi üzerinde kullanıcılar toosign gibi yaptığınız** sayfasında, **Azure AD çoklu oturum açma**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="a4a37-154">On hello **How would you like users toosign on tooQuestetra BPM Suite** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Azure AD çoklu oturum açma][9]

3. <span data-ttu-id="a4a37-156">Farklı web tarayıcısı penceresinde oturum açın, **Questetra BPM Suite** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="a4a37-156">In a different web browser window, log into your **Questetra BPM Suite** company site as an administrator.</span></span>

4. <span data-ttu-id="a4a37-157">Hello içinde hello üst menüsünde **sistem ayarlarını**.</span><span class="sxs-lookup"><span data-stu-id="a4a37-157">In hello menu on hello top, click **System Settings**.</span></span> 
   
    ![Azure AD çoklu oturum açma][10]

5. <span data-ttu-id="a4a37-159">tooopen hello **SingleSignOnSAML** sayfasında, **SSO (SAML)**.</span><span class="sxs-lookup"><span data-stu-id="a4a37-159">tooopen hello **SingleSignOnSAML** page, click **SSO (SAML)**.</span></span> 
   
    ![Azure AD çoklu oturum açma][11]

6. <span data-ttu-id="a4a37-161">Merhaba hello üzerinde Klasik Azure portalı içinde **uygulama ayarlarını yapılandır** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a4a37-161">In hello Azure classic portal, on hello **Configure App Settings** dialog page, perform hello following steps:</span></span> 
   
    ![Uygulama ayarlarını yapılandırın][13]
   
    <span data-ttu-id="a4a37-163">a.</span><span class="sxs-lookup"><span data-stu-id="a4a37-163">a.</span></span> <span data-ttu-id="a4a37-164">Üzerinde **Questetra BPM Suite** şirket sitede hello SP bilgi bölümü, kopyalama hello **ACS URL**ve hello yapıştırma **oturum üzerinde URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="a4a37-164">On you **Questetra BPM Suite** company site, in hello SP Information section, copy hello **ACS URL**, and then paste it into hello **Sign On URL** textbox.</span></span>
   
    <span data-ttu-id="a4a37-165">b.</span><span class="sxs-lookup"><span data-stu-id="a4a37-165">b.</span></span> <span data-ttu-id="a4a37-166">Üzerinde **Questetra BPM Suite** şirket sitede hello SP bilgi bölümü, kopyalama hello **varlık kimliği**ve hello yapıştırma **veren URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="a4a37-166">On you **Questetra BPM Suite** company site, in hello SP Information section, copy hello **Entity ID**, and then paste it into hello **Issuer URL** textbox.</span></span>
   
    <span data-ttu-id="a4a37-167">c.</span><span class="sxs-lookup"><span data-stu-id="a4a37-167">c.</span></span> <span data-ttu-id="a4a37-168">Üzerinde **Questetra BPM Suite** şirket sitede hello SP bilgi bölümü, kopyalama hello **ACS URL**ve hello yapıştırma **yanıt URL'si** textbox.</span><span class="sxs-lookup"><span data-stu-id="a4a37-168">On you **Questetra BPM Suite** company site, in hello SP Information section, copy hello **ACS URL**, and then paste it into hello **Reply URL** textbox.</span></span>
   
    <span data-ttu-id="a4a37-169">d.</span><span class="sxs-lookup"><span data-stu-id="a4a37-169">d.</span></span> <span data-ttu-id="a4a37-170">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a4a37-170">Click **Next**.</span></span>

7. <span data-ttu-id="a4a37-171">Merhaba üzerinde **çoklu oturum açma sırasında Questetra BPM paketi yapılandırma** sayfasında, **indirme sertifika**ve yerel olarak bilgisayarınızda hello sertifika dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="a4a37-171">On hello **Configure single sign-on at Questetra BPM Suite** page, click **Download certificate**, and then save hello certificate file locally on your computer.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın][14]

8. <span data-ttu-id="a4a37-173">Üzerinde **Questetra BPM Suite** şirket site, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a4a37-173">On you **Questetra BPM Suite** company site, perform hello following steps:</span></span> 
   
    ![Çoklu oturum açmayı yapılandırın][15]
   
    <span data-ttu-id="a4a37-175">a.</span><span class="sxs-lookup"><span data-stu-id="a4a37-175">a.</span></span> <span data-ttu-id="a4a37-176">Seçin **çoklu oturum açmayı etkinleştir**.</span><span class="sxs-lookup"><span data-stu-id="a4a37-176">Select **Enable Single Sign-On**.</span></span>
   
    <span data-ttu-id="a4a37-177">b.</span><span class="sxs-lookup"><span data-stu-id="a4a37-177">b.</span></span> <span data-ttu-id="a4a37-178">Merhaba Hello Klasik Azure portalı, kopyalama **veren URL'si** değer ve hello yapıştırma **varlık kimliği** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="a4a37-178">On hello Azure classic portal, copy hello **Issuer URL** value, and then paste it into hello **Entity ID** textbox.</span></span>
   
    <span data-ttu-id="a4a37-179">c.</span><span class="sxs-lookup"><span data-stu-id="a4a37-179">c.</span></span> <span data-ttu-id="a4a37-180">Merhaba Hello Klasik Azure portalı, kopyalama **çoklu oturum açma hizmet URL'si** değer ve hello yapıştırma **oturum açma sayfası URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="a4a37-180">On hello Azure classic portal, copy hello **Single Sign-On Service URL** value, and then paste it into hello **Sign-in page URL** textbox.</span></span>
   
    <span data-ttu-id="a4a37-181">d.</span><span class="sxs-lookup"><span data-stu-id="a4a37-181">d.</span></span> <span data-ttu-id="a4a37-182">Merhaba Hello Klasik Azure portalı, kopyalama **tek Sign-Out hizmeti URL'si** değer ve hello yapıştırma **oturum kapatma sayfası URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="a4a37-182">On hello Azure classic portal, copy hello **Single Sign-Out Service URL** value, and then paste it into hello **Sign-out page URL** textbox.</span></span>
   
    <span data-ttu-id="a4a37-183">e.</span><span class="sxs-lookup"><span data-stu-id="a4a37-183">e.</span></span> <span data-ttu-id="a4a37-184">Merhaba, **NameID biçimi** metin kutusuna, türü **urn: OASIS: adları: tc: SAML:1.1:nameid-biçimi: emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="a4a37-184">In hello **NameID format** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="a4a37-185">f.</span><span class="sxs-lookup"><span data-stu-id="a4a37-185">f.</span></span> <span data-ttu-id="a4a37-186">Base-64 kodlanmış dosyayı indirilen sertifikanızı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a4a37-186">Create a base-64 encoded file from your downloaded certificate.</span></span> 

    >[!TIP] 
    ><span data-ttu-id="a4a37-187">Daha fazla ayrıntı için bkz: [nasıl tooconvert bir ikili sertifika bir metin dosyasına](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="a4a37-187">For more details, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

    <span data-ttu-id="a4a37-188">g.</span><span class="sxs-lookup"><span data-stu-id="a4a37-188">g.</span></span> <span data-ttu-id="a4a37-189">Base-64 kodlanmış sertifikanızı kopyalama hello panonuza bunu içerik Not Defteri'nde açın ve hello yapıştırma **doğrulama sertifikası** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="a4a37-189">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it into hello **Validation certificate** textbox.</span></span> 

    <span data-ttu-id="a4a37-190">h.</span><span class="sxs-lookup"><span data-stu-id="a4a37-190">h.</span></span> <span data-ttu-id="a4a37-191">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a4a37-191">Click **Save**.</span></span>

1. <span data-ttu-id="a4a37-192">Hello Klasik Azure portalı, hello tek oturum açma yapılandırması onay seçin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="a4a37-192">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    ![Azure AD Connect nedir?][17]

2. <span data-ttu-id="a4a37-194">Merhaba üzerinde **tek oturum açma onay** sayfasında, **tam**.</span><span class="sxs-lookup"><span data-stu-id="a4a37-194">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Connect nedir?][18]


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a4a37-196">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a4a37-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="a4a37-197">Bu bölümde Hello amacı toocreate hello Britta Simon adlı Klasik Azure portalında bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="a4a37-197">hello objective of this section is toocreate a test user in hello Azure classic portal called Britta Simon.</span></span>

<span data-ttu-id="a4a37-198">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a4a37-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a4a37-199">Merhaba, **Klasik Azure portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a4a37-199">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Azure AD test kullanıcısı oluşturma][100] 

2. <span data-ttu-id="a4a37-201">Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.</span><span class="sxs-lookup"><span data-stu-id="a4a37-201">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="a4a37-202">toodisplay hello hello üstte hello menüde kullanıcıların listesini tıklatın **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="a4a37-202">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Azure AD test kullanıcısı oluşturma][101] 

4. <span data-ttu-id="a4a37-204">tooopen hello **Kullanıcı Ekle** hello araç çubuğunda hello altta iletişim tıklatın **Kullanıcı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="a4a37-204">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span> 
   
    ![Azure AD test kullanıcısı oluşturma][102] 

5. <span data-ttu-id="a4a37-206">Merhaba üzerinde **bu kullanıcı hakkında bize** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a4a37-206">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![Azure AD test kullanıcısı oluşturma][103]
   
    <span data-ttu-id="a4a37-208">a.</span><span class="sxs-lookup"><span data-stu-id="a4a37-208">a.</span></span> <span data-ttu-id="a4a37-209">Olarak **kullanıcı türü**seçin **kuruluşunuzdaki yeni kullanıcı**.</span><span class="sxs-lookup"><span data-stu-id="a4a37-209">As **Type Of User**, select **New user in your organization**.</span></span>
   
    <span data-ttu-id="a4a37-210">b.</span><span class="sxs-lookup"><span data-stu-id="a4a37-210">b.</span></span> <span data-ttu-id="a4a37-211">Merhaba kullanıcı adı olarak **textbox**, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a4a37-211">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="a4a37-212">c.</span><span class="sxs-lookup"><span data-stu-id="a4a37-212">c.</span></span> <span data-ttu-id="a4a37-213">İleri'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a4a37-213">Click Next.</span></span>

6. <span data-ttu-id="a4a37-214">Merhaba üzerinde **kullanıcı profili** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a4a37-214">On hello **User Profile** dialog page, perform hello following steps:</span></span> 
   
    ![Azure AD test kullanıcısı oluşturma][104] 
   
    <span data-ttu-id="a4a37-216">a.</span><span class="sxs-lookup"><span data-stu-id="a4a37-216">a.</span></span> <span data-ttu-id="a4a37-217">Merhaba, **ad** metin kutusuna, türü **Britta**.</span><span class="sxs-lookup"><span data-stu-id="a4a37-217">In hello **First Name** textbox, type **Britta**.</span></span> 
   
    <span data-ttu-id="a4a37-218">b.</span><span class="sxs-lookup"><span data-stu-id="a4a37-218">b.</span></span> <span data-ttu-id="a4a37-219">Merhaba, **Soyadı** metin kutusuna, türü, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="a4a37-219">In hello **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="a4a37-220">c.</span><span class="sxs-lookup"><span data-stu-id="a4a37-220">c.</span></span> <span data-ttu-id="a4a37-221">Merhaba, **görünen adı** metin kutusuna, türü **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="a4a37-221">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="a4a37-222">d.</span><span class="sxs-lookup"><span data-stu-id="a4a37-222">d.</span></span> <span data-ttu-id="a4a37-223">Merhaba, **rol** listesinde **kullanıcı**.</span><span class="sxs-lookup"><span data-stu-id="a4a37-223">In hello **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="a4a37-224">e.</span><span class="sxs-lookup"><span data-stu-id="a4a37-224">e.</span></span> <span data-ttu-id="a4a37-225">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a4a37-225">Click **Next**.</span></span>

7. <span data-ttu-id="a4a37-226">Merhaba üzerinde **Get geçici parola** iletişim sayfasında, tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="a4a37-226">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Azure AD test kullanıcısı oluşturma][105]  

8. <span data-ttu-id="a4a37-228">Merhaba üzerinde **Get geçici parola** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a4a37-228">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Azure AD test kullanıcısı oluşturma][106]   
   
    <span data-ttu-id="a4a37-230">a.</span><span class="sxs-lookup"><span data-stu-id="a4a37-230">a.</span></span> <span data-ttu-id="a4a37-231">Merhaba Hello değerini yazmak **yeni parola**.</span><span class="sxs-lookup"><span data-stu-id="a4a37-231">Write down hello value of hello **New Password**.</span></span>
   
    <span data-ttu-id="a4a37-232">b.</span><span class="sxs-lookup"><span data-stu-id="a4a37-232">b.</span></span> <span data-ttu-id="a4a37-233">**Tamamla**’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a4a37-233">Click **Complete**.</span></span>   

### <a name="creating-a-questetra-bpm-suite-test-user"></a><span data-ttu-id="a4a37-234">Questetra BPM Suite test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a4a37-234">Creating a Questetra BPM Suite test user</span></span>
<span data-ttu-id="a4a37-235">Bu bölümde Hello amacı toocreate Britta Simon Questetra BPM paketindeki adlı bir kullanıcı var.</span><span class="sxs-lookup"><span data-stu-id="a4a37-235">hello objective of this section is toocreate a user called Britta Simon in Questetra BPM Suite.</span></span>

<span data-ttu-id="a4a37-236">**toocreate Britta Simon Questetra BPM paketindeki adlı bir kullanıcı hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a4a37-236">**toocreate a user called Britta Simon in Questetra BPM Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="a4a37-237">Yönetici olarak oturum açma tooyour Questetra BPM Suite şirket sitesi.</span><span class="sxs-lookup"><span data-stu-id="a4a37-237">Sign-on tooyour Questetra BPM Suite company site as an administrator.</span></span>
2. <span data-ttu-id="a4a37-238">Çok Git**sistem ayarlarını > kullanıcı listesi > Yeni kullanıcı**.</span><span class="sxs-lookup"><span data-stu-id="a4a37-238">Go too**System Settings > User List > New User**.</span></span> 
3. <span data-ttu-id="a4a37-239">Merhaba yeni kullanıcı iletişim kutusundaki hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a4a37-239">On hello New User dialog, perform hello following steps:</span></span> 
   
    ![Test kullanıcısı oluşturma][300] 
   
    <span data-ttu-id="a4a37-241">a.</span><span class="sxs-lookup"><span data-stu-id="a4a37-241">a.</span></span> <span data-ttu-id="a4a37-242">Merhaba, **adı** metin kutusuna, Azure AD'de Britta'nin kullanıcı adını yazın.</span><span class="sxs-lookup"><span data-stu-id="a4a37-242">In hello **Name** textbox, type Britta's user name in Azure AD.</span></span>
   
    <span data-ttu-id="a4a37-243">b.</span><span class="sxs-lookup"><span data-stu-id="a4a37-243">b.</span></span> <span data-ttu-id="a4a37-244">Merhaba, **e-posta** metin kutusuna, Azure AD'de Britta'nin kullanıcı adını yazın.</span><span class="sxs-lookup"><span data-stu-id="a4a37-244">In hello **Email** textbox, type Britta's user name in Azure AD.</span></span>
   
    <span data-ttu-id="a4a37-245">c.</span><span class="sxs-lookup"><span data-stu-id="a4a37-245">c.</span></span> <span data-ttu-id="a4a37-246">Merhaba, **parola** metin kutusuna, bir parola yazın.</span><span class="sxs-lookup"><span data-stu-id="a4a37-246">In hello **Password** textbox, type a password.</span></span>

4. <span data-ttu-id="a4a37-247">Tıklatın **yeni kullanıcı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="a4a37-247">Click **Add new user**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a4a37-248">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="a4a37-248">Assigning hello Azure AD test user</span></span>
<span data-ttu-id="a4a37-249">Merhaba amacı, bu bölümde, kendi erişim tooQuestetra BPM Suite vererek tooenabling Britta Simon toouse Azure çoklu oturum açma olur.</span><span class="sxs-lookup"><span data-stu-id="a4a37-249">hello objective of this section is tooenabling Britta Simon toouse Azure single sign-on by granting her access tooQuestetra BPM Suite.</span></span>

![Azure AD Connect nedir?][200]

<span data-ttu-id="a4a37-251">**tooassign Britta Simon tooQuestetra BPM Suite hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a4a37-251">**tooassign Britta Simon tooQuestetra BPM Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="a4a37-252">Hello üzerinde Azure Klasik portalı, hello dizin görünümünde tooopen hello uygulamaları Görünüm'e tıklayın **uygulamaları** hello üst menüde.</span><span class="sxs-lookup"><span data-stu-id="a4a37-252">On hello Azure classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Azure AD Connect nedir?][201]
2. <span data-ttu-id="a4a37-254">Merhaba uygulamalar listesinde **Questetra BPM Suite**.</span><span class="sxs-lookup"><span data-stu-id="a4a37-254">In hello applications list, select **Questetra BPM Suite**.</span></span>
   
    ![Azure AD Connect nedir?][205]
3. <span data-ttu-id="a4a37-256">Hello içinde hello üst menüsünde **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="a4a37-256">In hello menu on hello top, click **Users**.</span></span>
   
    ![Azure AD Connect nedir?][202]
4. <span data-ttu-id="a4a37-258">Merhaba kullanıcılar listesinden seçin **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="a4a37-258">In hello Users list, select **Britta Simon**.</span></span>
   
    ![Azure AD Connect nedir?][203]
5. <span data-ttu-id="a4a37-260">Merhaba altta Hello araç çubuğunda **atamak**.</span><span class="sxs-lookup"><span data-stu-id="a4a37-260">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Azure AD Connect nedir?][204]

### <a name="testing-single-sign-on"></a><span data-ttu-id="a4a37-262">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="a4a37-262">Testing Single Sign-On</span></span>
<span data-ttu-id="a4a37-263">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="a4a37-263">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="a4a37-264">Merhaba Questetra BPM Suite hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Questetra BPM paketi uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a4a37-264">When you click hello Questetra BPM Suite tile in hello Access Panel, you should get automatically signed-on tooyour Questetra BPM Suite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a4a37-265">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="a4a37-265">Additional Resources</span></span>
* [<span data-ttu-id="a4a37-266">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="a4a37-266">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a4a37-267">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="a4a37-267">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_01.png


[8]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_06.png
[9]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_02.png
[10]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_03.png
[11]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_04.png
[12]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_05.png
[13]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_06.png
[14]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_07.png
[15]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_08.png
[16]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_09.png
[17]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_10.png
[18]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_08.png


[100]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_09.png 
[101]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_10.png 
[102]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_11.png 
[103]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_12.png 
[104]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_13.png 
[105]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_14.png 
[106]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_15.png 


[200]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_16.png 
[201]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_17.png 
[202]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_18.png
[203]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_19.png
[204]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_20.png
[205]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_12.png

[300]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_11.png 
