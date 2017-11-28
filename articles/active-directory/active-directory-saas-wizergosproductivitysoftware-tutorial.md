---
title: "Öğretici: Azure Active Directory Tümleştirme Wizergos üretkenlik ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Wizergos üretkenlik arasında."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: acc04396-13c5-4c24-ab9a-30fbc9234ebd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/20/2017
ms.author: jeedes
ms.openlocfilehash: cdd186c38c426dde404ed8bb84700faf9c8c1a46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wizergos-productivity-software"></a><span data-ttu-id="35ac2-103">Öğretici: Azure Active Directory Tümleştirme ile Wizergos üretkenlik</span><span class="sxs-lookup"><span data-stu-id="35ac2-103">Tutorial: Azure Active Directory integration with Wizergos Productivity Software</span></span>
<span data-ttu-id="35ac2-104">Bu öğreticinin Hello hedefi olan tooshow, nasıl toointegrate Wizergos üretkenlik Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="35ac2-104">hello objective of this tutorial is tooshow you how toointegrate Wizergos Productivity Software  with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="35ac2-105">Wizergos üretkenlik Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="35ac2-105">Integrating Wizergos Productivity Software with Azure AD provides you with hello following benefits:</span></span>

* <span data-ttu-id="35ac2-106">Erişim tooWizergos üretkenlik sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="35ac2-106">You can control in Azure AD who has access tooWizergos Productivity Software</span></span>
* <span data-ttu-id="35ac2-107">Azure AD hesaplarına, kullanıcıların tooautomatically get açan tooWizergos üretkenlik çoklu oturum açma (SSO) etkinleştir</span><span class="sxs-lookup"><span data-stu-id="35ac2-107">You can enable your users tooautomatically get signed-on tooWizergos Productivity Software single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="35ac2-108">Hesaplarınızı bir merkezi konumda - hello Klasik Azure portalı Yönet</span><span class="sxs-lookup"><span data-stu-id="35ac2-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="35ac2-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="35ac2-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="35ac2-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="35ac2-110">Prerequisites</span></span>
<span data-ttu-id="35ac2-111">tooconfigure Wizergos üretkenlik ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="35ac2-111">tooconfigure Azure AD integration with Wizergos Productivity Software, you need hello following items:</span></span>

* <span data-ttu-id="35ac2-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="35ac2-112">An Azure AD subscription</span></span>
* <span data-ttu-id="35ac2-113">Abonelik Wizergos üretkenlik yazılım SSO etkin</span><span class="sxs-lookup"><span data-stu-id="35ac2-113">A Wizergos Productivity Software SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="35ac2-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="35ac2-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="35ac2-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="35ac2-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="35ac2-116">Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="35ac2-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="35ac2-117">Bir Azure AD deneme ortam yoksa, alabileceğiniz bir [bir aylık deneme](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="35ac2-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="35ac2-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="35ac2-118">Scenario description</span></span>
<span data-ttu-id="35ac2-119">Bu öğreticinin Hello hedefi olan tooenable, tootest Azure AD SSO bir sınama ortamında.</span><span class="sxs-lookup"><span data-stu-id="35ac2-119">hello objective of this tutorial is tooenable you tootest Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="35ac2-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="35ac2-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="35ac2-121">Merhaba Galerisi'nden Wizergos üretkenlik ekleme</span><span class="sxs-lookup"><span data-stu-id="35ac2-121">Adding Wizergos Productivity Software from hello gallery</span></span>
2. <span data-ttu-id="35ac2-122">Yapılandırma ve Azure AD SSO test etme</span><span class="sxs-lookup"><span data-stu-id="35ac2-122">Configuring and testing Azure AD SSO</span></span>

## <a name="adding-wizergos-productivity-software-from-hello-gallery"></a><span data-ttu-id="35ac2-123">Merhaba Galerisi'nden Wizergos üretkenlik ekleme</span><span class="sxs-lookup"><span data-stu-id="35ac2-123">Adding Wizergos Productivity Software from hello gallery</span></span>
<span data-ttu-id="35ac2-124">Azure AD'ye tooconfigure hello tümleştirme Wizergos üretkenlik yazılımın tooadd Wizergos üretkenlik hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="35ac2-124">tooconfigure hello integration of Wizergos Productivity Software into Azure AD, you need tooadd Wizergos Productivity Software from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="35ac2-125">**tooadd Wizergos üretkenlik hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="35ac2-125">**tooadd Wizergos Productivity Software from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="35ac2-126">Merhaba, **Klasik Azure portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="35ac2-126">In hello **Azure classic Portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="35ac2-128">Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.</span><span class="sxs-lookup"><span data-stu-id="35ac2-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="35ac2-129">Merhaba dizin görünümünde tooopen hello uygulamaları Görüntüle'yi tıklatın **uygulamaları** hello üst menüde.</span><span class="sxs-lookup"><span data-stu-id="35ac2-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Uygulamalar][2]
4. <span data-ttu-id="35ac2-131">Tıklatın **Ekle** hello sayfanın hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="35ac2-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Uygulamalar][3]
5. <span data-ttu-id="35ac2-133">Merhaba üzerinde **neler toodo istediğiniz** iletişim kutusunda, tıklatın **hello Galeriden bir uygulama eklemek**.</span><span class="sxs-lookup"><span data-stu-id="35ac2-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Uygulamalar][4]
6. <span data-ttu-id="35ac2-135">Merhaba arama kutusuna yazın **Wizergos üretkenlik**.</span><span class="sxs-lookup"><span data-stu-id="35ac2-135">In hello search box, type **Wizergos Productivity Software**.</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_01.png)
7. <span data-ttu-id="35ac2-137">Merhaba Sonuçlar panelinde seçin **Wizergos üretkenlik**ve ardından **tam** tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="35ac2-137">In hello results panel, select **Wizergos Productivity Software**, and then click **Complete** tooadd hello application.</span></span>
   
    ![Merhaba Galerisi'nde Hello uygulama seçme](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_001.png)

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="35ac2-139">Yapılandırma ve Azure AD SSO test etme</span><span class="sxs-lookup"><span data-stu-id="35ac2-139">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="35ac2-140">Bu bölümde Hello amacı olan tooshow nasıl tooconfigure ve test Wizergos üretkenlik ile Azure AD SSO temel alarak "Britta Simon" adlı bir test kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="35ac2-140">hello objective of this section is tooshow you how tooconfigure and test Azure AD SSO with Wizergos Productivity Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="35ac2-141">SSO toowork için Azure AD hangi hello karşılık gelen kullanıcı Wizergos üretkenlik tooan kullanıcı Azure AD'de tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="35ac2-141">For SSO toowork, Azure AD needs tooknow what hello counterpart user in Wizergos Productivity Software tooan user in Azure AD is.</span></span> <span data-ttu-id="35ac2-142">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Wizergos üretkenlik hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="35ac2-142">In other words, a link relationship between an Azure AD user and hello related user in Wizergos Productivity Software needs toobe established.</span></span>

<span data-ttu-id="35ac2-143">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcı adı** Wizergos üretkenlik yazılım.</span><span class="sxs-lookup"><span data-stu-id="35ac2-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Wizergos Productivity Software.</span></span>

<span data-ttu-id="35ac2-144">tooconfigure ve BynWizergos üretkenlik Softwareder ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="35ac2-144">tooconfigure and test Azure AD single sign-on with BynWizergos Productivity Softwareder, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="35ac2-145">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="35ac2-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="35ac2-146">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="35ac2-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="35ac2-147">**[Wizergos üretkenlik test kullanıcısı oluşturma](#creating-a-wizergos-productivity-software-test-user)**  -toohave karşılık gelen, Britta Simon Wizergos üretkenlik yazılımında, her bağlı toohello Azure AD gösterimidir.</span><span class="sxs-lookup"><span data-stu-id="35ac2-147">**[Creating a Wizergos Productivity Software test user](#creating-a-wizergos-productivity-software-test-user)** - toohave a counterpart of Britta Simon in Wizergos Productivity Software that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="35ac2-148">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="35ac2-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="35ac2-149">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="35ac2-149">**[Testing single sign-on](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-sso"></a><span data-ttu-id="35ac2-150">Azure AD SSO yapılandırma</span><span class="sxs-lookup"><span data-stu-id="35ac2-150">Configuring Azure AD SSO</span></span>
<span data-ttu-id="35ac2-151">Bu bölümde, Azure AD çoklu oturum açma hello Klasik portalında etkinleştirin ve çoklu oturum açma Wizergos üretkenlik uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="35ac2-151">In this section, you enable Azure AD single sign-on in hello classic portal and configure single sign-on in your Wizergos Productivity Software application.</span></span>

<span data-ttu-id="35ac2-152">**Azure AD çoklu oturum açma tooconfigure Wizergos üretkenlik ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="35ac2-152">**tooconfigure Azure AD single sign-on with Wizergos Productivity Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="35ac2-153">Merhaba üzerinde hello Klasik Portalı'nda **Wizergos üretkenlik** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma özelliğini yapılandırın** tooopen hello **yapılandırma çoklu oturum açma**iletişim.</span><span class="sxs-lookup"><span data-stu-id="35ac2-153">In hello classic portal, on hello **Wizergos Productivity Software** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın][6] 
2. <span data-ttu-id="35ac2-155">Merhaba üzerinde **nasıl tooWizergos üretkenlik üzerinde kullanıcılar toosign gibi yaptığınız** sayfasında, **Azure AD çoklu oturum açma**ve ardından **sonraki**:</span><span class="sxs-lookup"><span data-stu-id="35ac2-155">On hello **How would you like users toosign on tooWizergos Productivity Software** page, select **Azure AD Single Sign-On**, and then click **Next**:</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_03.png)
3. <span data-ttu-id="35ac2-157">Merhaba üzerinde **uygulama ayarlarını yapılandır** iletişim sayfasında, tıklatın **sonraki**:</span><span class="sxs-lookup"><span data-stu-id="35ac2-157">On hello **Configure App Settings** dialog page, click **Next**:</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_04.png)
4. <span data-ttu-id="35ac2-159">Merhaba üzerinde **çoklu oturum açma sırasında Wizergos üretkenlik yapılandırma** sayfasında, **indirme sertifika**ve ardından hello dosyayı bilgisayarınıza kaydedin:</span><span class="sxs-lookup"><span data-stu-id="35ac2-159">On hello **Configure single sign-on at Wizergos Productivity Software** page, click **Download certificate**, and then save hello file on your computer:</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_05.png)
5. <span data-ttu-id="35ac2-161">Bir farklı web tarayıcısı penceresinde, bir yönetici olarak oturum açma tooyour Wizergos üretkenlik Kiracı.</span><span class="sxs-lookup"><span data-stu-id="35ac2-161">In a different web browser window, sign-on tooyour Wizergos Productivity Software tenant as an administrator.</span></span>
6. <span data-ttu-id="35ac2-162">Merhaba hamburger menüsünden seçin **yönetici**.</span><span class="sxs-lookup"><span data-stu-id="35ac2-162">From hello hamburger menu, select **Admin**.</span></span>
   
    ![Çoklu oturum açma üzerinde uygulama tarafı yapılandırma](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_000.png)
7. <span data-ttu-id="35ac2-164">Sol taraftaki menüsünde Yönetim sayfasında seçin **kimlik doğrulaması** ve tıklayın **Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="35ac2-164">In Admin page on left hand menu select **AUTHENTICATION** and click on **Azure AD**.</span></span>
   
    ![Çoklu oturum açma üzerinde uygulama tarafı yapılandırma](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_002.png)
8. <span data-ttu-id="35ac2-166">Aşağıdaki adımları hello gerçekleştirmek **kimlik doğrulaması** bölümü.</span><span class="sxs-lookup"><span data-stu-id="35ac2-166">Perform hello following steps on **AUTHENTICATION** section.</span></span>
   
    ![Çoklu oturum açma üzerinde uygulama tarafı yapılandırma](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_003.png)
  1. <span data-ttu-id="35ac2-168">Tıklatın **karşıya** düğmesini tooupload hello Azure AD'den sertifika indirilir.</span><span class="sxs-lookup"><span data-stu-id="35ac2-168">Click **UPLOAD** button tooupload hello downloaded certificate from Azure AD.</span></span> 
  2. <span data-ttu-id="35ac2-169">Merhaba, **veren URL'si** textbox put hello değerini **veren URL'si** Azure AD Uygulama Yapılandırma Sihirbazı'ndan.</span><span class="sxs-lookup"><span data-stu-id="35ac2-169">In hello **Issuer URL** textbox put hello value of **Issuer URL** from Azure AD application configuration wizard.</span></span>
  3. <span data-ttu-id="35ac2-170">Merhaba, **çoklu oturum açma URL'si** textbox put hello değerini **çoklu oturum açma hizmet URL'si** Azure AD Uygulama Yapılandırma Sihirbazı'ndan.</span><span class="sxs-lookup"><span data-stu-id="35ac2-170">In hello **Single Sign-On URL** textbox put hello value of **Single Sign-on Service URL** from Azure AD application configuration wizard.</span></span>
  4. <span data-ttu-id="35ac2-171">Merhaba, **tek Sign-Out URL** textbox put hello değerini **tek Sign-out hizmeti URL'si** Azure AD Uygulama Yapılandırma Sihirbazı'ndan.</span><span class="sxs-lookup"><span data-stu-id="35ac2-171">In hello **Single Sign-Out URL** textbox put hello value of **Single Sign-out Service URL** from Azure AD application configuration wizard.</span></span>
  5. <span data-ttu-id="35ac2-172">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="35ac2-172">Click **Save** button.</span></span>
9. <span data-ttu-id="35ac2-173">Merhaba Klasik portalında hello tek oturum açma yapılandırması onay seçin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="35ac2-173">In hello classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD çoklu oturum açma][10]
10. <span data-ttu-id="35ac2-175">Merhaba üzerinde **tek oturum açma onay** sayfasında, **tam**.</span><span class="sxs-lookup"><span data-stu-id="35ac2-175">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
    
    ![Azure AD çoklu oturum açma][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="35ac2-177">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="35ac2-177">Create an Azure AD test user</span></span>
<span data-ttu-id="35ac2-178">Bu bölümde Hello amacı toocreate bir test kullanıcısı Britta Simon adlı hello Klasik Portalı'nda ' dir.</span><span class="sxs-lookup"><span data-stu-id="35ac2-178">hello objective of this section is toocreate a test user in hello classic portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][20]

<span data-ttu-id="35ac2-180">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="35ac2-180">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="35ac2-181">Merhaba, **Klasik Azure portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="35ac2-181">In hello **Azure classic Portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_09.png)
2. <span data-ttu-id="35ac2-183">Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.</span><span class="sxs-lookup"><span data-stu-id="35ac2-183">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="35ac2-184">toodisplay hello hello üstte hello menüde kullanıcıların listesini tıklatın **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="35ac2-184">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_03.png)
4. <span data-ttu-id="35ac2-186">tooopen hello **Kullanıcı Ekle** hello araç çubuğunda hello altta iletişim tıklatın **Kullanıcı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="35ac2-186">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_04.png)
5. <span data-ttu-id="35ac2-188">Merhaba üzerinde **bu kullanıcı hakkında bize** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="35ac2-188">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="35ac2-190">Kullanıcı türü olarak, kuruluşunuzdaki yeni kullanıcı seçin.</span><span class="sxs-lookup"><span data-stu-id="35ac2-190">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="35ac2-191">Merhaba kullanıcı adı olarak **textbox**, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="35ac2-191">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="35ac2-192">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="35ac2-192">Click **Next**.</span></span>
6. <span data-ttu-id="35ac2-193">Merhaba üzerinde **kullanıcı profili** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="35ac2-193">On hello **User Profile** dialog page, perform hello following steps:</span></span>
   
   ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_06.png)
  1. <span data-ttu-id="35ac2-195">Merhaba, **ad** metin kutusuna, türü **Britta**.</span><span class="sxs-lookup"><span data-stu-id="35ac2-195">In hello **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="35ac2-196">Merhaba, **Soyadı** metin kutusuna, türü, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="35ac2-196">In hello **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="35ac2-197">Merhaba, **görünen adı** metin kutusuna, türü **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="35ac2-197">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="35ac2-198">Merhaba, **rol** listesinde **kullanıcı**.</span><span class="sxs-lookup"><span data-stu-id="35ac2-198">In hello **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="35ac2-199">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="35ac2-199">Click **Next**.</span></span>
7. <span data-ttu-id="35ac2-200">Merhaba üzerinde **Get geçici parola** iletişim sayfasında, tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="35ac2-200">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_07.png)
8. <span data-ttu-id="35ac2-202">Merhaba üzerinde **Get geçici parola** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="35ac2-202">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_08.png)
  1. <span data-ttu-id="35ac2-204">Merhaba Hello değerini yazmak **yeni parola**.</span><span class="sxs-lookup"><span data-stu-id="35ac2-204">Write down hello value of hello **New Password**.</span></span>
  2. <span data-ttu-id="35ac2-205">**Tamamla**’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="35ac2-205">Click **Complete**.</span></span>   

### <a name="create-a-wizergos-productivity-software-test-user"></a><span data-ttu-id="35ac2-206">Wizergos üretkenlik test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="35ac2-206">Create a Wizergos Productivity Software test user</span></span>
<span data-ttu-id="35ac2-207">Bu bölümde, Britta Simon Wizergos üretkenlik adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="35ac2-207">In this section, you create a user called Britta Simon in Wizergos Productivity Software.</span></span> <span data-ttu-id="35ac2-208">Lütfen Wizergos üretkenlik destek ekibi ile çalışmak [ support@wizergos.com ](emailTo:support@wizergos.com) tooadd hello kullanıcılar hello Wizergos üretkenlik Platform.</span><span class="sxs-lookup"><span data-stu-id="35ac2-208">Please work with Wizergos Productivity Software support team via [support@wizergos.com](emailTo:support@wizergos.com) tooadd hello users in hello Wizergos Productivity Software platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="35ac2-209">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="35ac2-209">Assign hello Azure AD test user</span></span>
<span data-ttu-id="35ac2-210">Bu bölümde Hello amacı kendi erişim tooWizergos üretkenlik vererek tooenabling Britta Simon toouse Azure SSO olur.</span><span class="sxs-lookup"><span data-stu-id="35ac2-210">hello objective of this section is tooenabling Britta Simon toouse Azure SSO by granting her access tooWizergos Productivity Software.</span></span>

  ![Kullanıcı atama][200]

<span data-ttu-id="35ac2-212">**tooassign Britta Simon tooWizergos üretkenlik, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="35ac2-212">**tooassign Britta Simon tooWizergos Productivity Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="35ac2-213">Merhaba Klasik portalında hello dizin görünümünde tooopen hello uygulamaları Görüntüle'yi tıklatın **uygulamaları** hello üst menüde.</span><span class="sxs-lookup"><span data-stu-id="35ac2-213">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Kullanıcı atama][201]
2. <span data-ttu-id="35ac2-215">Merhaba uygulamalar listesinde **Wizergos üretkenlik**.</span><span class="sxs-lookup"><span data-stu-id="35ac2-215">In hello applications list, select **Wizergos Productivity Software**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_50.png)
3. <span data-ttu-id="35ac2-217">Hello içinde hello üst menüsünde **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="35ac2-217">In hello menu on hello top, click **Users**.</span></span>
   
    ![Kullanıcı atama][203]
4. <span data-ttu-id="35ac2-219">Merhaba kullanıcılar listesinden seçin **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="35ac2-219">In hello Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="35ac2-220">Merhaba altta Hello araç çubuğunda **atamak**.</span><span class="sxs-lookup"><span data-stu-id="35ac2-220">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Kullanıcı atama][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="35ac2-222">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="35ac2-222">Test single sign-on</span></span>
<span data-ttu-id="35ac2-223">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD SSO yapılandırmayı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="35ac2-223">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="35ac2-224">Merhaba Wizergos üretkenlik hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Wizergos üretkenlik uygulaması almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="35ac2-224">When you click hello Wizergos Productivity Software tile in hello Access Panel, you should get automatically signed-on tooyour Wizergos Productivity Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="35ac2-225">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="35ac2-225">Additional resources</span></span>
* [<span data-ttu-id="35ac2-226">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="35ac2-226">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="35ac2-227">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="35ac2-227">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_205.png
