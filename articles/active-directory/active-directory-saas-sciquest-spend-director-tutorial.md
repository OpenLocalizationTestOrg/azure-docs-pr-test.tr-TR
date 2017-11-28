---
title: "Öğretici: Azure Active Directory Tümleştirme SciQuest harcamanız Director ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile SciQuest harcamanız Director arasında."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 9fab641b-292e-4bef-91d1-8ccc4f3a0c1f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 47c46f1297054fd96b86c1d8c66e1a55ec151497
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sciquest-spend-director"></a><span data-ttu-id="0ee26-103">Öğretici: Azure Active Directory Tümleştirme SciQuest harcamanız Director ile</span><span class="sxs-lookup"><span data-stu-id="0ee26-103">Tutorial: Azure Active Directory integration with SciQuest Spend Director</span></span>
<span data-ttu-id="0ee26-104">Bu öğreticinin Hello hedefi olan tooshow, nasıl toointegrate SciQuest harcamanız Director Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0ee26-104">hello objective of this tutorial is tooshow you how toointegrate SciQuest Spend Director with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="0ee26-105">SciQuest harcadığı Director Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="0ee26-105">Integrating SciQuest Spend Director with Azure AD provides you with hello following benefits:</span></span> 

* <span data-ttu-id="0ee26-106">Erişim tooSciQuest harcama Director sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="0ee26-106">You can control in Azure AD who has access tooSciQuest Spend Director</span></span> 
* <span data-ttu-id="0ee26-107">Kullanıcıların tooautomatically get açan tooSciQuest (çoklu oturum açma) harcama Director Azure AD hesaplarına ile etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="0ee26-107">You can enable your users tooautomatically get signed-on tooSciQuest Spend Director (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="0ee26-108">Hesaplarınızı bir merkezi konumda - hello Klasik Azure portalı Yönet</span><span class="sxs-lookup"><span data-stu-id="0ee26-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="0ee26-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0ee26-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0ee26-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="0ee26-110">Prerequisites</span></span>
<span data-ttu-id="0ee26-111">tooconfigure SciQuest harcamanız Director ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="0ee26-111">tooconfigure Azure AD integration with SciQuest Spend Director, you need hello following items:</span></span>

* <span data-ttu-id="0ee26-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="0ee26-112">An Azure AD subscription</span></span>
* <span data-ttu-id="0ee26-113">Bir SciQuest harcamanız Director çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="0ee26-113">A SciQuest Spend Director single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0ee26-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="0ee26-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="0ee26-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="0ee26-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="0ee26-116">Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0ee26-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="0ee26-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0ee26-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="0ee26-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="0ee26-118">Scenario Description</span></span>
<span data-ttu-id="0ee26-119">Bu öğreticinin Hello hedefi olan tooenable, tootest Azure AD çoklu oturum açma bir sınama ortamında.</span><span class="sxs-lookup"><span data-stu-id="0ee26-119">hello objective of this tutorial is tooenable you tootest Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="0ee26-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="0ee26-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0ee26-121">Merhaba Galerisi'nden SciQuest harcamanız Director ekleme</span><span class="sxs-lookup"><span data-stu-id="0ee26-121">Adding SciQuest Spend Director from hello gallery</span></span> 
2. <span data-ttu-id="0ee26-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="0ee26-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sciquest-spend-director-from-hello-gallery"></a><span data-ttu-id="0ee26-123">Merhaba Galerisi'nden SciQuest harcamanız Director ekleme</span><span class="sxs-lookup"><span data-stu-id="0ee26-123">Adding SciQuest Spend Director from hello gallery</span></span>
<span data-ttu-id="0ee26-124">Azure AD'ye tooconfigure hello tümleştirme SciQuest harcamanız Director, tooadd SciQuest harcamanız Director hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="0ee26-124">tooconfigure hello integration of SciQuest Spend Director into Azure AD, you need tooadd SciQuest Spend Director from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0ee26-125">**tooadd SciQuest harcamanız Director hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0ee26-125">**tooadd SciQuest Spend Director from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0ee26-126">Merhaba, **Klasik Azure portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0ee26-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="0ee26-128">Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.</span><span class="sxs-lookup"><span data-stu-id="0ee26-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="0ee26-129">Merhaba dizin görünümünde tooopen hello uygulamaları Görüntüle'yi tıklatın **uygulamaları** hello üst menüde.</span><span class="sxs-lookup"><span data-stu-id="0ee26-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Uygulamalar][2]

4. <span data-ttu-id="0ee26-131">Tıklatın **Ekle** hello sayfanın hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="0ee26-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Uygulamalar][3]

5. <span data-ttu-id="0ee26-133">Merhaba üzerinde **neler toodo istediğiniz** iletişim kutusunda, tıklatın **hello Galeriden bir uygulama eklemek**.</span><span class="sxs-lookup"><span data-stu-id="0ee26-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Uygulamalar][4]

6. <span data-ttu-id="0ee26-135">Merhaba arama kutusuna yazın **sciQuest harcamanız director**.</span><span class="sxs-lookup"><span data-stu-id="0ee26-135">In hello search box, type **sciQuest spend director**.</span></span>
   
    ![Uygulamalar][5]

7. <span data-ttu-id="0ee26-137">Merhaba sonuçlar bölmesinde seçin **SciQuest harcamanız Director**ve ardından **tam** tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="0ee26-137">In hello results pane, select **SciQuest Spend Director**, and then click **Complete** tooadd hello application.</span></span>
   
    ![Uygulamalar][6]

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0ee26-139">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="0ee26-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0ee26-140">Bu bölümde Hello amacı olan tooshow nasıl tooconfigure ve Azure AD çoklu oturum açmayı test SciQuest harcamanız Director ile temel alarak "Britta Simon" adlı bir test kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="0ee26-140">hello objective of this section is tooshow you how tooconfigure and test Azure AD single sign-on with SciQuest Spend Director based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0ee26-141">Tek toowork'ın oturum açma, Azure AD hangi hello karşılık gelen kullanıcı SciQuest harcamanız Director tooan kullanıcı Azure AD'de tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="0ee26-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SciQuest Spend Director tooan user in Azure AD is.</span></span> <span data-ttu-id="0ee26-142">Diğer bir deyişle, bir Azure AD kullanıcısının ve SciQuest harcamanız Director hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="0ee26-142">In other words, a link relationship between an Azure AD user and hello related user in SciQuest Spend Director needs toobe established.</span></span>  
<span data-ttu-id="0ee26-143">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcı adı** SciQuest harcamanız Director.</span><span class="sxs-lookup"><span data-stu-id="0ee26-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in SciQuest Spend Director.</span></span>

<span data-ttu-id="0ee26-144">tooconfigure ve SciQuest harcamanız Director ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="0ee26-144">tooconfigure and test Azure AD single sign-on with SciQuest Spend Director, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0ee26-145">**[Azure AD tek tek oturum açma yapılandırma](#configuring-azure-ad-single-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="0ee26-145">**[Configuring Azure AD Single Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0ee26-146">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="0ee26-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0ee26-147">**[SciQuest harcadığı Director test kullanıcısı oluşturma](#creating-a-halogen-software-test-user)**  -toohave karşılık gelen, Britta Simon SciQuest harcamanız Director her bağlantılı toohello Azure AD gösterimidir.</span><span class="sxs-lookup"><span data-stu-id="0ee26-147">**[Creating a SciQuest Spend Director test user](#creating-a-halogen-software-test-user)** - toohave a counterpart of Britta Simon in SciQuest Spend Director that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="0ee26-148">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="0ee26-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0ee26-149">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="0ee26-149">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-single-sign-on"></a><span data-ttu-id="0ee26-150">Azure AD çoklu çoklu oturum açma yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0ee26-150">Configuring Azure AD Single Single Sign-On</span></span>
<span data-ttu-id="0ee26-151">Bu bölümde Hello amacı tooenable Azure AD çoklu oturum açma hello Klasik Azure Portalı'nda ve tooconfigure çoklu oturum açma SciQuest harcamanız Director uygulamanızda ' dir.</span><span class="sxs-lookup"><span data-stu-id="0ee26-151">hello objective of this section is tooenable Azure AD single sign-on in hello Azure classic portal and tooconfigure single sign-on in your SciQuest Spend Director application.</span></span>

<span data-ttu-id="0ee26-152">**Azure AD çoklu oturum açma tooconfigure harcamanız SciQuest Director ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0ee26-152">**tooconfigure Azure AD single sign-on with SciQuest Spend Director, perform hello following steps:**</span></span>

1. <span data-ttu-id="0ee26-153">Hello hello üzerinde Klasik Azure portalı içinde **SciQuest harcamanız Director** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma özelliğini yapılandırın** tooopen hello **yapılandırma çoklu oturum açma**iletişim.</span><span class="sxs-lookup"><span data-stu-id="0ee26-153">In hello Azure classic portal, on hello **SciQuest Spend Director** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın][8]

2. <span data-ttu-id="0ee26-155">Merhaba üzerinde **nasıl tooSciQuest harcama Director üzerinde kullanıcılar toosign gibi yaptığınız** sayfasında, **Azure AD çoklu oturum açma**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="0ee26-155">On hello **How would you like users toosign on tooSciQuest Spend Director** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Azure AD çoklu oturum açma][9]

3. <span data-ttu-id="0ee26-157">Merhaba üzerinde **uygulama ayarlarını yapılandır** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="0ee26-157">On hello **Configure App Settings** dialog page, perform hello following steps:</span></span> 
   
    ![Uygulama ayarlarını yapılandırın][10]
   
     <span data-ttu-id="0ee26-159">a.</span><span class="sxs-lookup"><span data-stu-id="0ee26-159">a.</span></span> <span data-ttu-id="0ee26-160">Merhaba, **oturum üzerinde URL'si** metin kutusuna, türü URL'niz, kullanıcıların toosign desen aşağıdaki hello kullanarak tooyour SciQuest harcamanız Director uygulama tarafından kullanılan: *https://.* SciQuest.com/.**</span><span class="sxs-lookup"><span data-stu-id="0ee26-160">In hello **Sign On URL** textbox, type your URL used by your users toosign on tooyour SciQuest Spend Director application using hello following pattern: *https://.*sciquest.com/.**</span></span>
   
     <span data-ttu-id="0ee26-161">b.</span><span class="sxs-lookup"><span data-stu-id="0ee26-161">b.</span></span> <span data-ttu-id="0ee26-162">Merhaba, **yanıt URL'si** metin kutusuna, türü hello aynı değeri, hello yazmış **oturum üzerinde URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="0ee26-162">In hello **Reply URL** textbox, type hello same value you have typed into hello **Sign On URL** textbox.</span></span> 
   
     <span data-ttu-id="0ee26-163">c.</span><span class="sxs-lookup"><span data-stu-id="0ee26-163">c.</span></span> <span data-ttu-id="0ee26-164">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0ee26-164">Click **Next**.</span></span>

4. <span data-ttu-id="0ee26-165">Merhaba üzerinde **çoklu oturum açma SciQuest harcamanız Director yapılandırma** sayfasında, **karşıdan meta veri**ve hello meta veri dosyası, bilgisayarınıza yerel olarak kaydedin.</span><span class="sxs-lookup"><span data-stu-id="0ee26-165">On hello **Configure single sign-on at SciQuest Spend Director** page, click **Download metadata**, and then save hello metadata file locally on your computer.</span></span>
   
    ![Azure AD Connect nedir?][11]

5. <span data-ttu-id="0ee26-167">SciQuest destek tooenable hello yukarıdaki indirilen meta verileri kullanarak bu kimlik doğrulama yöntemini başvurun.</span><span class="sxs-lookup"><span data-stu-id="0ee26-167">Contact SciQuest support tooenable this authentication method using hello above downloaded metadata.</span></span>

6. <span data-ttu-id="0ee26-168">Hello Klasik Azure portalı, hello tek oturum açma yapılandırması onay seçin ve ardından **tam** tooclose hello **tek oturum yapılandırma üzerinde aktar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="0ee26-168">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span> 
   
    ![Azure AD Connect nedir?][15]

7. <span data-ttu-id="0ee26-170">Merhaba üzerinde **tek oturum açma onay** sayfasında, **tam**.</span><span class="sxs-lookup"><span data-stu-id="0ee26-170">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0ee26-171">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="0ee26-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="0ee26-172">Bu bölümde Hello amacı toocreate hello Britta Simon adlı Klasik Azure portalında bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="0ee26-172">hello objective of this section is toocreate a test user in hello Azure classic portal called Britta Simon.</span></span>

<span data-ttu-id="0ee26-173">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0ee26-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0ee26-174">Merhaba, **Klasik Azure portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0ee26-174">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Azure AD Connect nedir?][100] 

2. <span data-ttu-id="0ee26-176">Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.</span><span class="sxs-lookup"><span data-stu-id="0ee26-176">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="0ee26-177">toodisplay hello hello üstte hello menüde kullanıcıların listesini tıklatın **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="0ee26-177">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Azure AD Connect nedir?][101] 

4. <span data-ttu-id="0ee26-179">tooopen hello **Kullanıcı Ekle** hello araç çubuğunda hello altta iletişim tıklatın **Kullanıcı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="0ee26-179">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span> 
   
    ![Azure AD Connect nedir?][102] 

5. <span data-ttu-id="0ee26-181">Merhaba üzerinde **bu kullanıcı hakkında bize** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="0ee26-181">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![Azure AD Connect nedir?][103] 
   
    <span data-ttu-id="0ee26-183">a.</span><span class="sxs-lookup"><span data-stu-id="0ee26-183">a.</span></span> <span data-ttu-id="0ee26-184">Olarak **kullanıcı türü**seçin **kuruluşunuzdaki yeni kullanıcı**.</span><span class="sxs-lookup"><span data-stu-id="0ee26-184">As **Type Of User**, select **New user in your organization**.</span></span>
   
    <span data-ttu-id="0ee26-185">b.</span><span class="sxs-lookup"><span data-stu-id="0ee26-185">b.</span></span> <span data-ttu-id="0ee26-186">Merhaba kullanıcı adı olarak **textbox**, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0ee26-186">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="0ee26-187">c.</span><span class="sxs-lookup"><span data-stu-id="0ee26-187">c.</span></span> <span data-ttu-id="0ee26-188">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0ee26-188">Click **Next**.</span></span>

6. <span data-ttu-id="0ee26-189">Merhaba üzerinde **kullanıcı profili** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="0ee26-189">On hello **User Profile** dialog page, perform hello following steps:</span></span> 
   
    ![Azure AD Connect nedir?][104] 
   
    <span data-ttu-id="0ee26-191">a.</span><span class="sxs-lookup"><span data-stu-id="0ee26-191">a.</span></span> <span data-ttu-id="0ee26-192">Merhaba, **ad** metin kutusuna, türü **Britta**.</span><span class="sxs-lookup"><span data-stu-id="0ee26-192">In hello **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="0ee26-193">b.</span><span class="sxs-lookup"><span data-stu-id="0ee26-193">b.</span></span> <span data-ttu-id="0ee26-194">Merhaba, **Soyadı** txtbox, türü, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="0ee26-194">In hello **Last Name** txtbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="0ee26-195">c.</span><span class="sxs-lookup"><span data-stu-id="0ee26-195">c.</span></span> <span data-ttu-id="0ee26-196">Merhaba, **görünen adı** metin kutusuna, türü **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="0ee26-196">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="0ee26-197">d.</span><span class="sxs-lookup"><span data-stu-id="0ee26-197">d.</span></span> <span data-ttu-id="0ee26-198">Merhaba, **rol** listesinde **kullanıcı**.</span><span class="sxs-lookup"><span data-stu-id="0ee26-198">In hello **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="0ee26-199">e.</span><span class="sxs-lookup"><span data-stu-id="0ee26-199">e.</span></span> <span data-ttu-id="0ee26-200">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0ee26-200">Click **Next**.</span></span>

7. <span data-ttu-id="0ee26-201">Merhaba üzerinde **Get geçici parola** iletişim sayfasında, tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="0ee26-201">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Azure AD Connect nedir?][105]  

8. <span data-ttu-id="0ee26-203">Merhaba üzerinde **Get geçici parola** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="0ee26-203">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Azure AD Connect nedir?][106]   
   
    <span data-ttu-id="0ee26-205">a.</span><span class="sxs-lookup"><span data-stu-id="0ee26-205">a.</span></span> <span data-ttu-id="0ee26-206">Merhaba Hello değerini yazmak **yeni parola**.</span><span class="sxs-lookup"><span data-stu-id="0ee26-206">Write down hello value of hello **New Password**.</span></span>
   
    <span data-ttu-id="0ee26-207">b.</span><span class="sxs-lookup"><span data-stu-id="0ee26-207">b.</span></span> <span data-ttu-id="0ee26-208">**Tamamla**’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0ee26-208">Click **Complete**.</span></span>   

### <a name="creating-a-sciquest-spend-director-test-user"></a><span data-ttu-id="0ee26-209">SciQuest harcadığı Director test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="0ee26-209">Creating a SciQuest Spend Director test user</span></span>
<span data-ttu-id="0ee26-210">Bu bölümde Hello amacı toocreate Britta Simon SciQuest harcamanız Director uygulamasında adlı bir kullanıcı var.</span><span class="sxs-lookup"><span data-stu-id="0ee26-210">hello objective of this section is toocreate a user called Britta Simon in SciQuest Spend Director.</span></span>

<span data-ttu-id="0ee26-211">Oluşturulan, test hesap tooget hakkında hello ayrıntılarla sağlayacağını ve toocontact SciQuest harcamanız Director destek ekibinize gerekir.</span><span class="sxs-lookup"><span data-stu-id="0ee26-211">You need toocontact your SciQuest Spend Director support team and provide them with hello details about your test account tooget it created.</span></span>

<span data-ttu-id="0ee26-212">Alternatif olarak, yalnızca zaman da kullanabilirsiniz sağlama, SciQuest harcamanız Director tarafından desteklenen tek bir oturum açma özelliği.</span><span class="sxs-lookup"><span data-stu-id="0ee26-212">Alternatively, you can also leverage just-in-time provisioning, a single sign-on feature that is supported by SciQuest Spend Director.</span></span>  
<span data-ttu-id="0ee26-213">Yalnızca zaman sağlama etkinse, yoksa kullanıcılar otomatik olarak SciQuest harcamanız Director tarafından bir tek oturum açma girişimi sırasında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="0ee26-213">If just-in-time provisioning is enabled, users are automatically created by SciQuest Spend Director during a single sign-on attempt if they don't exist.</span></span> <span data-ttu-id="0ee26-214">Bu özellik hello ihtiyacını ortadan kaldıran toomanually tek oturum açma karşılık gelen kullanıcılar oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0ee26-214">This feature eliminates hello need toomanually create single sign-on counterpart users.</span></span>

<span data-ttu-id="0ee26-215">yalnızca zaman tooget sağlama etkin, SciQuest harcamanız Director destek ekibinize olduğunuz toocontact gerekir.</span><span class="sxs-lookup"><span data-stu-id="0ee26-215">tooget just-in-time provisioning enabled, you need toocontact your your SciQuest Spend Director support team.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0ee26-216">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="0ee26-216">Assigning hello Azure AD test user</span></span>
<span data-ttu-id="0ee26-217">Bu bölümde Hello amacı kendi erişim tooSciQuest harcama Director vererek tooenabling Britta Simon toouse Azure çoklu oturum açma olur.</span><span class="sxs-lookup"><span data-stu-id="0ee26-217">hello objective of this section is tooenabling Britta Simon toouse Azure single sign-on by granting her access tooSciQuest Spend Director.</span></span>

![Azure AD Connect nedir?][200]

<span data-ttu-id="0ee26-219">**tooassign Britta Simon tooSciQuest harcama Director hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0ee26-219">**tooassign Britta Simon tooSciQuest Spend Director, perform hello following steps:**</span></span>

1. <span data-ttu-id="0ee26-220">Hello üzerinde Azure Klasik portalı, hello dizin görünümünde tooopen hello uygulamaları Görünüm'e tıklayın **uygulamaları** hello üst menüde.</span><span class="sxs-lookup"><span data-stu-id="0ee26-220">On hello Azure classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Azure AD Connect nedir?][201]

2. <span data-ttu-id="0ee26-222">Merhaba uygulamalar listesinde **SciQuest harcamanız Director**.</span><span class="sxs-lookup"><span data-stu-id="0ee26-222">In hello applications list, select **SciQuest Spend Director**.</span></span>
   
    ![Azure AD Connect nedir?][202]

3. <span data-ttu-id="0ee26-224">Hello içinde hello üst menüsünde **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="0ee26-224">In hello menu on hello top, click **Users**.</span></span>
   
    ![Azure AD Connect nedir?][203]

4. <span data-ttu-id="0ee26-226">Merhaba kullanıcılar listesinden seçin **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="0ee26-226">In hello Users list, select **Britta Simon**.</span></span>
   
    ![Azure AD Connect nedir?][204]

5. <span data-ttu-id="0ee26-228">Merhaba altta Hello araç çubuğunda **atamak**.</span><span class="sxs-lookup"><span data-stu-id="0ee26-228">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Azure AD Connect nedir?][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="0ee26-230">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="0ee26-230">Testing Single Sign-On</span></span>
<span data-ttu-id="0ee26-231">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="0ee26-231">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="0ee26-232">Merhaba SciQuest harcamanız Director hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour SciQuest harcamanız Director uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0ee26-232">When you click hello SciQuest Spend Director tile in hello Access Panel, you should get automatically signed-on tooyour SciQuest Spend Director application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0ee26-233">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="0ee26-233">Additional Resources</span></span>
* [<span data-ttu-id="0ee26-234">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="0ee26-234">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0ee26-235">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="0ee26-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_01.png
[6]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_05.png
[8]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_06.png
[9]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_07.png
[10]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_08.png
[11]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_03.png
[15]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_04.png

[100]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_09.png 
[101]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_10.png 
[102]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_11.png 
[103]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_12.png 
[104]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_13.png 
[105]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_14.png 
[106]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_15.png 
[200]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_16.png 
[201]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_17.png 
[202]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_06.png
[203]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_18.png
[204]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_19.png
[205]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_20.png

