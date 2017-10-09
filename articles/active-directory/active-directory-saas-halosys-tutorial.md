---
title: "Öğretici: Azure Active Directory Tümleştirme ile Halosys | Microsoft Docs"
description: "Azure Active Directory tooenable ile toouse Halosys nasıl tek oturum açma, otomatik sağlama ve daha fazlasını öğrenin!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 42a0eb7c-5cb7-44a9-b00b-b0e7df4b63e8
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 18043ed1b6f7ab45c59cfd36252bef1621618e51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-halosys"></a><span data-ttu-id="0b8da-103">Öğretici: Azure Active Directory Tümleştirme Halosys ile</span><span class="sxs-lookup"><span data-stu-id="0b8da-103">Tutorial: Azure Active Directory integration with Halosys</span></span>

<span data-ttu-id="0b8da-104">Bu öğreticide, bilgi nasıl toointegrate Halosys Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0b8da-104">In this tutorial, you learn how toointegrate Halosys with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0b8da-105">Halosys Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="0b8da-105">Integrating Halosys with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0b8da-106">Erişim tooHalosys sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="0b8da-106">You can control in Azure AD who has access tooHalosys</span></span>
- <span data-ttu-id="0b8da-107">Kullanıcıların tooautomatically get açan tooHalosys (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="0b8da-107">You can enable your users tooautomatically get signed-on tooHalosys (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0b8da-108">Hesaplarınızı bir merkezi konumda - hello Klasik Azure portalı Yönet</span><span class="sxs-lookup"><span data-stu-id="0b8da-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="0b8da-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0b8da-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0b8da-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="0b8da-110">Prerequisites</span></span>

<span data-ttu-id="0b8da-111">tooconfigure Halosys ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="0b8da-111">tooconfigure Azure AD integration with Halosys, you need hello following items:</span></span>

- <span data-ttu-id="0b8da-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="0b8da-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0b8da-113">Bir Halosys çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="0b8da-113">A Halosys single-sign on enabled subscription</span></span>


> [!NOTE] 
> <span data-ttu-id="0b8da-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="0b8da-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="0b8da-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="0b8da-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0b8da-116">Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0b8da-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="0b8da-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0b8da-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="0b8da-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="0b8da-118">Scenario description</span></span>
<span data-ttu-id="0b8da-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="0b8da-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="0b8da-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="0b8da-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0b8da-121">Merhaba Galerisi'nden Halosys ekleme</span><span class="sxs-lookup"><span data-stu-id="0b8da-121">Adding Halosys from hello gallery</span></span>
2. <span data-ttu-id="0b8da-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="0b8da-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-halosys-from-hello-gallery"></a><span data-ttu-id="0b8da-123">Merhaba Galerisi'nden Halosys ekleme</span><span class="sxs-lookup"><span data-stu-id="0b8da-123">Adding Halosys from hello gallery</span></span>
<span data-ttu-id="0b8da-124">Azure AD'ye tooconfigure hello tümleştirme Halosys, tooadd Halosys hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="0b8da-124">tooconfigure hello integration of Halosys into Azure AD, you need tooadd Halosys from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0b8da-125">**tooadd Halosys hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0b8da-125">**tooadd Halosys from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0b8da-126">Merhaba, **Klasik Azure portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0b8da-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>

    ![Active Directory][1]
2. <span data-ttu-id="0b8da-128">Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.</span><span class="sxs-lookup"><span data-stu-id="0b8da-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="0b8da-129">Merhaba dizin görünümünde tooopen hello uygulamaları Görüntüle'yi tıklatın **uygulamaları** hello üst menüde.</span><span class="sxs-lookup"><span data-stu-id="0b8da-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>

    ![Uygulamalar][2]

4. <span data-ttu-id="0b8da-131">Tıklatın **Ekle** hello sayfanın hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="0b8da-131">Click **Add** at hello bottom of hello page.</span></span>

    ![Uygulamalar][3]

5. <span data-ttu-id="0b8da-133">Merhaba üzerinde **neler toodo istediğiniz** iletişim kutusunda, tıklatın **hello Galeriden bir uygulama eklemek**.</span><span class="sxs-lookup"><span data-stu-id="0b8da-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>

    ![Uygulamalar][4]

6. <span data-ttu-id="0b8da-135">Merhaba arama kutusuna yazın **Halosys**.</span><span class="sxs-lookup"><span data-stu-id="0b8da-135">In hello search box, type **Halosys**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_01.png)
    
7. <span data-ttu-id="0b8da-137">Merhaba sonuçlar bölmesinde seçin **Halosys**ve ardından **tam** tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="0b8da-137">In hello results pane, select **Halosys**, and then click **Complete** tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_011.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0b8da-139">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="0b8da-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0b8da-140">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Halosys sınayın.</span><span class="sxs-lookup"><span data-stu-id="0b8da-140">In this section, you configure and test Azure AD single sign-on with Halosys based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0b8da-141">Tek toowork'ın oturum açma hangi hello karşılık gelen Halosys içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="0b8da-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Halosys is tooa user in Azure AD.</span></span> <span data-ttu-id="0b8da-142">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Halosys hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="0b8da-142">In other words, a link relationship between an Azure AD user and hello related user in Halosys needs toobe established.</span></span>

<span data-ttu-id="0b8da-143">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** Halosys içinde.</span><span class="sxs-lookup"><span data-stu-id="0b8da-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Halosys.</span></span>

<span data-ttu-id="0b8da-144">tooconfigure ve Halosys ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="0b8da-144">tooconfigure and test Azure AD single sign-on with Halosys, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0b8da-145">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="0b8da-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0b8da-146">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="0b8da-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0b8da-147">**[Halosys test kullanıcısı oluşturma](#creating-a-halosys-test-user)**  -toohave karşılık gelen her bağlantılı toohello Azure AD gösterimidir Halosys içinde Britta Simon biri.</span><span class="sxs-lookup"><span data-stu-id="0b8da-147">**[Creating a Halosys test user](#creating-a-halosys-test-user)** - toohave a counterpart of Britta Simon in Halosys that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="0b8da-148">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="0b8da-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0b8da-149">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="0b8da-149">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0b8da-150">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0b8da-150">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0b8da-151">Bu bölümde, Azure AD çoklu oturum açma hello Klasik portalında etkinleştirin ve çoklu oturum açma Halosys uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="0b8da-151">In this section, you enable Azure AD single sign-on in hello classic portal and configure single sign-on in your Halosys application.</span></span>


<span data-ttu-id="0b8da-152">**tooconfigure Azure AD çoklu oturum açma ile Halosys, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0b8da-152">**tooconfigure Azure AD single sign-on with Halosys, perform hello following steps:**</span></span>

1. <span data-ttu-id="0b8da-153">Merhaba üzerinde hello Klasik Portalı'nda **Halosys** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma özelliğini yapılandırın** tooopen hello **yapılandırma çoklu oturum açma** iletişim.</span><span class="sxs-lookup"><span data-stu-id="0b8da-153">In hello classic portal, on hello **Halosys** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
     
    ![Çoklu oturum açmayı yapılandırın][6] 

2. <span data-ttu-id="0b8da-155">Merhaba üzerinde **nasıl tooHalosys üzerinde kullanıcılar toosign gibi yaptığınız** sayfasında, **Azure AD çoklu oturum açma**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="0b8da-155">On hello **How would you like users toosign on tooHalosys** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_03.png) 

3. <span data-ttu-id="0b8da-157">Merhaba üzerinde **uygulama ayarlarını yapılandır** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="0b8da-157">On hello **Configure App Settings** dialog page, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_04.png) 

    <span data-ttu-id="0b8da-159">a.</span><span class="sxs-lookup"><span data-stu-id="0b8da-159">a.</span></span> <span data-ttu-id="0b8da-160">Merhaba, **oturum üzerinde URL'si** metin kutusuna, desen aşağıdaki hello kullanarak, kullanıcılar toosign üzerinde tooyour Halosys uygulamanız tarafından kullanılan türü hello URL: `https://<company-name>.Halosys.com/client-api/api`.</span><span class="sxs-lookup"><span data-stu-id="0b8da-160">In hello **Sign On URL** textbox, type hello URL used by your users toosign-on tooyour Halosys application using hello following pattern: `https://<company-name>.Halosys.com/client-api/api`.</span></span>

    <span data-ttu-id="0b8da-161">b.In hello **tanımlayıcı URL'si** metin kutusuna, türü hello hello desen aşağıdaki URL'de: `https://<company-name>.Halosys.com`.</span><span class="sxs-lookup"><span data-stu-id="0b8da-161">b.In hello **Identifier URL** textbox, type hello URL in hello following pattern: `https://<company-name>.Halosys.com`.</span></span> 
         
4. <span data-ttu-id="0b8da-162">Merhaba üzerinde **çoklu oturum açma sırasında Halosys yapılandırma** sayfasında, **karşıdan meta veri**ve hello dosyayı bilgisayarınıza kaydedin:</span><span class="sxs-lookup"><span data-stu-id="0b8da-162">On hello **Configure single sign-on at Halosys** page, click **Download metadata**, and then save hello file on your computer:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_05.png)
   
5. <span data-ttu-id="0b8da-164">tooget uygulamanız için yapılandırılmış SSO Halosys Destek ekibine başvurun ve ile Merhaba aşağıdakileri sağlar:</span><span class="sxs-lookup"><span data-stu-id="0b8da-164">tooget SSO configured for your application, contact Halosys support team and provide them with hello following:</span></span>

    <span data-ttu-id="0b8da-165">• hello indirilen **meta veri dosyası**</span><span class="sxs-lookup"><span data-stu-id="0b8da-165">• hello downloaded **metadata file**</span></span>
    
    <span data-ttu-id="0b8da-166">• hello **SAML SSO URL'si**</span><span class="sxs-lookup"><span data-stu-id="0b8da-166">• hello **SAML SSO URL**</span></span>
    

6. <span data-ttu-id="0b8da-167">Merhaba Klasik portalında hello tek oturum açma yapılandırması onay seçin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="0b8da-167">In hello classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span>
    
    ![Azure AD çoklu oturum açma][10]

7. <span data-ttu-id="0b8da-169">Merhaba üzerinde **tek oturum açma onay** sayfasında, **tam**.</span><span class="sxs-lookup"><span data-stu-id="0b8da-169">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
 
    ![Azure AD çoklu oturum açma][11]


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0b8da-171">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="0b8da-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="0b8da-172">Bu bölümde, bir test kullanıcısı Britta Simon adlı hello Klasik portalda oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0b8da-172">In this section, you create a test user in hello classic portal called Britta Simon.</span></span>


![Azure AD Kullanıcı oluşturma][20]

<span data-ttu-id="0b8da-174">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0b8da-174">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0b8da-175">Merhaba, **Klasik Azure portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0b8da-175">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-Halosys-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="0b8da-177">Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.</span><span class="sxs-lookup"><span data-stu-id="0b8da-177">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="0b8da-178">toodisplay hello hello üstte hello menüde kullanıcıların listesini tıklatın **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="0b8da-178">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-Halosys-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0b8da-180">tooopen hello **Kullanıcı Ekle** hello araç çubuğunda hello altta iletişim tıklatın **Kullanıcı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="0b8da-180">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-Halosys-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="0b8da-182">Merhaba üzerinde **bu kullanıcı hakkında bize** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin: ![bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-Halosys-tutorial/create_aaduser_05.png)</span><span class="sxs-lookup"><span data-stu-id="0b8da-182">On hello **Tell us about this user** dialog page, perform hello following steps:  ![Creating an Azure AD test user](./media/active-directory-saas-Halosys-tutorial/create_aaduser_05.png)</span></span> 

    <span data-ttu-id="0b8da-183">a.</span><span class="sxs-lookup"><span data-stu-id="0b8da-183">a.</span></span> <span data-ttu-id="0b8da-184">Kullanıcı türü olarak, kuruluşunuzdaki yeni kullanıcı seçin.</span><span class="sxs-lookup"><span data-stu-id="0b8da-184">As Type Of User, select New user in your organization.</span></span>

    <span data-ttu-id="0b8da-185">b.</span><span class="sxs-lookup"><span data-stu-id="0b8da-185">b.</span></span> <span data-ttu-id="0b8da-186">Merhaba kullanıcı adı olarak **textbox**, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0b8da-186">In hello User Name **textbox**, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0b8da-187">c.</span><span class="sxs-lookup"><span data-stu-id="0b8da-187">c.</span></span> <span data-ttu-id="0b8da-188">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0b8da-188">Click **Next**.</span></span>

6.  <span data-ttu-id="0b8da-189">Merhaba üzerinde **kullanıcı profili** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin: ![bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-Halosys-tutorial/create_aaduser_06.png)</span><span class="sxs-lookup"><span data-stu-id="0b8da-189">On hello **User Profile** dialog page, perform hello following steps: ![Creating an Azure AD test user](./media/active-directory-saas-Halosys-tutorial/create_aaduser_06.png)</span></span> 

    <span data-ttu-id="0b8da-190">a.</span><span class="sxs-lookup"><span data-stu-id="0b8da-190">a.</span></span> <span data-ttu-id="0b8da-191">Merhaba, **ad** metin kutusuna, türü **Britta**.</span><span class="sxs-lookup"><span data-stu-id="0b8da-191">In hello **First Name** textbox, type **Britta**.</span></span>  

    <span data-ttu-id="0b8da-192">b.</span><span class="sxs-lookup"><span data-stu-id="0b8da-192">b.</span></span> <span data-ttu-id="0b8da-193">Merhaba, **Soyadı** metin kutusuna, türü, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="0b8da-193">In hello **Last Name** textbox, type, **Simon**.</span></span>

    <span data-ttu-id="0b8da-194">c.</span><span class="sxs-lookup"><span data-stu-id="0b8da-194">c.</span></span> <span data-ttu-id="0b8da-195">Merhaba, **görünen adı** metin kutusuna, türü **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="0b8da-195">In hello **Display Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="0b8da-196">d.</span><span class="sxs-lookup"><span data-stu-id="0b8da-196">d.</span></span> <span data-ttu-id="0b8da-197">Merhaba, **rol** listesinde **kullanıcı**.</span><span class="sxs-lookup"><span data-stu-id="0b8da-197">In hello **Role** list, select **User**.</span></span>

    <span data-ttu-id="0b8da-198">e.</span><span class="sxs-lookup"><span data-stu-id="0b8da-198">e.</span></span> <span data-ttu-id="0b8da-199">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0b8da-199">Click **Next**.</span></span>

7. <span data-ttu-id="0b8da-200">Merhaba üzerinde **Get geçici parola** iletişim sayfasında, tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="0b8da-200">On hello **Get temporary password** dialog page, click **create**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-Halosys-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="0b8da-202">Merhaba üzerinde **Get geçici parola** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="0b8da-202">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-Halosys-tutorial/create_aaduser_08.png) 

    <span data-ttu-id="0b8da-204">a.</span><span class="sxs-lookup"><span data-stu-id="0b8da-204">a.</span></span> <span data-ttu-id="0b8da-205">Merhaba Hello değerini yazmak **yeni parola**.</span><span class="sxs-lookup"><span data-stu-id="0b8da-205">Write down hello value of hello **New Password**.</span></span>

    <span data-ttu-id="0b8da-206">b.</span><span class="sxs-lookup"><span data-stu-id="0b8da-206">b.</span></span> <span data-ttu-id="0b8da-207">**Tamamla**’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0b8da-207">Click **Complete**.</span></span>   



### <a name="creating-a-halosys-test-user"></a><span data-ttu-id="0b8da-208">Halosys test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="0b8da-208">Creating a Halosys test user</span></span>

<span data-ttu-id="0b8da-209">Bu bölümde, Halosys içinde Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0b8da-209">In this section, you create a user called Britta Simon in Halosys.</span></span> <span data-ttu-id="0b8da-210">Lütfen destek ekibi tooadd hello kullanıcılar hello Halosys Platform Halosys ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="0b8da-210">Please work with Halosys support team tooadd hello users in hello Halosys platform.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0b8da-211">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="0b8da-211">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0b8da-212">Bu bölümde, kendi erişim tooHalosys vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="0b8da-212">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooHalosys.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="0b8da-214">**tooassign Britta Simon tooHalosys hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0b8da-214">**tooassign Britta Simon tooHalosys, perform hello following steps:**</span></span>

1. <span data-ttu-id="0b8da-215">Merhaba Klasik portalında hello dizin görünümünde tooopen hello uygulamaları Görüntüle'yi tıklatın **uygulamaları** hello üst menüde.</span><span class="sxs-lookup"><span data-stu-id="0b8da-215">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="0b8da-217">Merhaba uygulamalar listesinde **Halosys**.</span><span class="sxs-lookup"><span data-stu-id="0b8da-217">In hello applications list, select **Halosys**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_50.png) 

3. <span data-ttu-id="0b8da-219">Hello içinde hello üst menüsünde **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="0b8da-219">In hello menu on hello top, click **Users**.</span></span>

    ![Kullanıcı atama][203]

4. <span data-ttu-id="0b8da-221">Merhaba kullanıcılar listesinden seçin **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="0b8da-221">In hello Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="0b8da-222">Merhaba altta Hello araç çubuğunda **atamak**.</span><span class="sxs-lookup"><span data-stu-id="0b8da-222">In hello toolbar on hello bottom, click **Assign**.</span></span>

    ![Kullanıcı atama][205]


### <a name="testing-single-sign-on"></a><span data-ttu-id="0b8da-224">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="0b8da-224">Testing single sign-on</span></span>

<span data-ttu-id="0b8da-225">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="0b8da-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="0b8da-226">Hello erişim paneli Halosys döşeme hello tıkladığınızda, otomatik olarak oturum açma Halosys uygulama tooyour almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0b8da-226">When you click hello Halosys tile in hello Access Panel, you should get automatically signed-on tooyour Halosys application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="0b8da-227">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="0b8da-227">Additional resources</span></span>

* [<span data-ttu-id="0b8da-228">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="0b8da-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0b8da-229">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="0b8da-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_205.png
