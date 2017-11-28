---
title: "Öğretici: Azure Active Directory Tümleştirme ile Workfront | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Workfront arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: aab8bd2f-f9dd-42da-a18e-d707865687d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: e7249b9ec769f19cf5aa7d44ff6f58705df4020a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workfront"></a><span data-ttu-id="7697e-103">Öğretici: Azure Active Directory Tümleştirme Workfront ile</span><span class="sxs-lookup"><span data-stu-id="7697e-103">Tutorial: Azure Active Directory integration with Workfront</span></span>

<span data-ttu-id="7697e-104">Bu öğreticide, bilgi nasıl toointegrate Workfront Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7697e-104">In this tutorial, you learn how toointegrate Workfront with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7697e-105">Workfront Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="7697e-105">Integrating Workfront with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7697e-106">Erişim tooWorkfront sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="7697e-106">You can control in Azure AD who has access tooWorkfront</span></span>
- <span data-ttu-id="7697e-107">Kullanıcıların tooautomatically get açan tooWorkfront (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="7697e-107">You can enable your users tooautomatically get signed-on tooWorkfront (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7697e-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="7697e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7697e-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7697e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7697e-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="7697e-110">Prerequisites</span></span>

<span data-ttu-id="7697e-111">tooconfigure Workfront ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="7697e-111">tooconfigure Azure AD integration with Workfront, you need hello following items:</span></span>

- <span data-ttu-id="7697e-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="7697e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7697e-113">Bir Workfront çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="7697e-113">A Workfront single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7697e-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="7697e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7697e-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="7697e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7697e-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="7697e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7697e-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7697e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7697e-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="7697e-118">Scenario description</span></span>
<span data-ttu-id="7697e-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="7697e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7697e-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="7697e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7697e-121">Merhaba Galerisi'nden Workfront ekleme</span><span class="sxs-lookup"><span data-stu-id="7697e-121">Adding Workfront from hello gallery</span></span>
2. <span data-ttu-id="7697e-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="7697e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workfront-from-hello-gallery"></a><span data-ttu-id="7697e-123">Merhaba Galerisi'nden Workfront ekleme</span><span class="sxs-lookup"><span data-stu-id="7697e-123">Adding Workfront from hello gallery</span></span>
<span data-ttu-id="7697e-124">Azure AD'ye tooconfigure hello tümleştirme Workfront, tooadd Workfront hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="7697e-124">tooconfigure hello integration of Workfront into Azure AD, you need tooadd Workfront from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7697e-125">**tooadd Workfront hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7697e-125">**tooadd Workfront from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7697e-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="7697e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7697e-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="7697e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7697e-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="7697e-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="7697e-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7697e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="7697e-133">Merhaba arama kutusuna yazın **Workfront**.</span><span class="sxs-lookup"><span data-stu-id="7697e-133">In hello search box, type **Workfront**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_search.png)

5. <span data-ttu-id="7697e-135">Merhaba Sonuçlar panelinde seçin **Workfront**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="7697e-135">In hello results panel, select **Workfront**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7697e-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="7697e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7697e-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Workfront ile test etme</span><span class="sxs-lookup"><span data-stu-id="7697e-138">In this section, you configure and test Azure AD single sign-on with Workfront based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7697e-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Workfront içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="7697e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Workfront is tooa user in Azure AD.</span></span> <span data-ttu-id="7697e-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Workfront hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="7697e-140">In other words, a link relationship between an Azure AD user and hello related user in Workfront needs toobe established.</span></span>

<span data-ttu-id="7697e-141">Merhaba hello değeri Workfront içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="7697e-141">In Workfront, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7697e-142">tooconfigure ve Workfront ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="7697e-142">tooconfigure and test Azure AD single sign-on with Workfront, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7697e-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="7697e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7697e-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="7697e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7697e-145">**[Workfront test kullanıcısı oluşturma](#creating-a-workfront-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Workfront içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="7697e-145">**[Creating a Workfront test user](#creating-a-workfront-test-user)** - toohave a counterpart of Britta Simon in Workfront that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7697e-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="7697e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7697e-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="7697e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7697e-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="7697e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7697e-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Workfront uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="7697e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Workfront application.</span></span>

<span data-ttu-id="7697e-150">**tooconfigure Azure AD çoklu oturum açma ile Workfront, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7697e-150">**tooconfigure Azure AD single sign-on with Workfront, perform hello following steps:**</span></span>

1. <span data-ttu-id="7697e-151">Hello hello üzerinde Azure portal'ın **Workfront** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="7697e-151">In hello Azure portal, on hello **Workfront** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="7697e-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="7697e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_samlbase.png)

3. <span data-ttu-id="7697e-155">Merhaba üzerinde **Workfront etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="7697e-155">On hello **Workfront Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_url.png)

    <span data-ttu-id="7697e-157">a.</span><span class="sxs-lookup"><span data-stu-id="7697e-157">a.</span></span> <span data-ttu-id="7697e-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.attask-ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="7697e-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.attask-ondemand.com`</span></span>

    <span data-ttu-id="7697e-159">b.</span><span class="sxs-lookup"><span data-stu-id="7697e-159">b.</span></span> <span data-ttu-id="7697e-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.attasksandbox.com/SAML2`</span><span class="sxs-lookup"><span data-stu-id="7697e-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.attasksandbox.com/SAML2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7697e-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="7697e-161">These values are not real.</span></span> <span data-ttu-id="7697e-162">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="7697e-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="7697e-163">Kişi [Workfront istemci destek ekibi](https://www.workfront.com/contact-us/) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="7697e-163">Contact [Workfront Client support team](https://www.workfront.com/contact-us/) tooget these values.</span></span> 
 
4. <span data-ttu-id="7697e-164">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="7697e-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello Certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_certificate.png) 

5. <span data-ttu-id="7697e-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7697e-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-workfront-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7697e-168">Merhaba üzerinde **Workfront yapılandırma** 'yi tıklatın **yapılandırma Workfront** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="7697e-168">On hello **Workfront Configuration** section, click **Configure Workfront** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="7697e-169">Kopya hello **Sign-Out URL ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="7697e-169">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_configure.png) 

7. <span data-ttu-id="7697e-171">Yönetici olarak oturum açma tooyour Workfront şirket sitesi.</span><span class="sxs-lookup"><span data-stu-id="7697e-171">Sign-on tooyour Workfront company site as administrator.</span></span>

8. <span data-ttu-id="7697e-172">Çok Git**tek oturum açma yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="7697e-172">Go too**Single Sign On Configuration**.</span></span>

9. <span data-ttu-id="7697e-173">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda, aşağıdaki adımları hello gerçekleştirmek</span><span class="sxs-lookup"><span data-stu-id="7697e-173">On hello **Single Sign-On** dialog, perform hello following steps</span></span>
    
    ![Çoklu oturum açmayı yapılandırın][23]
   
    <span data-ttu-id="7697e-175">a.</span><span class="sxs-lookup"><span data-stu-id="7697e-175">a.</span></span> <span data-ttu-id="7697e-176">Olarak **türü**seçin **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="7697e-176">As **Type**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="7697e-177">b.</span><span class="sxs-lookup"><span data-stu-id="7697e-177">b.</span></span> <span data-ttu-id="7697e-178">Seçin **hizmet sağlayıcı kimliği**.</span><span class="sxs-lookup"><span data-stu-id="7697e-178">Select **Service Provider ID**.</span></span>
   
    <span data-ttu-id="7697e-179">c.</span><span class="sxs-lookup"><span data-stu-id="7697e-179">c.</span></span> <span data-ttu-id="7697e-180">Yapıştır hello **SAML çoklu oturum açma hizmet URL'si** hello içine **oturum açma portalı URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="7697e-180">Paste hello **SAML Single Sign-On Service URL** into hello **Login Portal URL** textbox.</span></span>
   
    <span data-ttu-id="7697e-181">d.</span><span class="sxs-lookup"><span data-stu-id="7697e-181">d.</span></span> <span data-ttu-id="7697e-182">Yapıştır **tek Sign-Out hizmeti URL'si** hello içine **Sign-Out URL** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="7697e-182">Paste **Single Sign-Out Service URL** into hello **Sign-Out URL** textbox.</span></span>
   
    <span data-ttu-id="7697e-183">e.</span><span class="sxs-lookup"><span data-stu-id="7697e-183">e.</span></span> <span data-ttu-id="7697e-184">Yapıştır **değişiklik parola URL'si** hello içine **değişiklik parola URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="7697e-184">Paste **Change Password URL** into hello **Change Password URL** textbox.</span></span>
   
    <span data-ttu-id="7697e-185">f.</span><span class="sxs-lookup"><span data-stu-id="7697e-185">f.</span></span> <span data-ttu-id="7697e-186">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7697e-186">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="7697e-187">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="7697e-187">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7697e-188">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="7697e-188">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7697e-189">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7697e-189">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7697e-190">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7697e-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="7697e-191">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="7697e-191">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="7697e-193">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7697e-193">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7697e-194">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="7697e-194">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-workfront-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7697e-196">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="7697e-196">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-workfront-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7697e-198">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="7697e-198">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-workfront-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7697e-200">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="7697e-200">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-workfront-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7697e-202">a.</span><span class="sxs-lookup"><span data-stu-id="7697e-202">a.</span></span> <span data-ttu-id="7697e-203">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7697e-203">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7697e-204">b.</span><span class="sxs-lookup"><span data-stu-id="7697e-204">b.</span></span> <span data-ttu-id="7697e-205">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="7697e-205">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7697e-206">c.</span><span class="sxs-lookup"><span data-stu-id="7697e-206">c.</span></span> <span data-ttu-id="7697e-207">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="7697e-207">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7697e-208">d.</span><span class="sxs-lookup"><span data-stu-id="7697e-208">d.</span></span> <span data-ttu-id="7697e-209">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7697e-209">Click **Create**.</span></span>
 
### <a name="creating-a-workfront-test-user"></a><span data-ttu-id="7697e-210">Workfront test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7697e-210">Creating a Workfront test user</span></span>

<span data-ttu-id="7697e-211">Bu bölümde Hello amacı toocreate Britta Simon içinde Workfront adlı bir kullanıcı ' dir.</span><span class="sxs-lookup"><span data-stu-id="7697e-211">hello objective of this section is toocreate a user called Britta Simon in Workfront.</span></span>

<span data-ttu-id="7697e-212">**toocreate Workfront içinde Britta Simon adlı bir kullanıcı hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7697e-212">**toocreate a user called Britta Simon in Workfront, perform hello following steps:**</span></span>

1. <span data-ttu-id="7697e-213">Üzerinde tooyour Workfront şirket site yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="7697e-213">Sign on tooyour Workfront company site as administrator.</span></span>
2. <span data-ttu-id="7697e-214">Hello içinde hello üst menüsünde **kişiler**.</span><span class="sxs-lookup"><span data-stu-id="7697e-214">In hello menu on hello top, click **People**.</span></span>
3. <span data-ttu-id="7697e-215">Tıklatın **yeni bir kişiye**.</span><span class="sxs-lookup"><span data-stu-id="7697e-215">Click **New Person**.</span></span> 
4. <span data-ttu-id="7697e-216">Merhaba yeni bir kişiye iletişim kutusunda hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="7697e-216">On hello New Person dialog, perform hello following steps:</span></span>
   
    ![Bir Workfront test kullanıcısı oluşturma][21] 
   
    <span data-ttu-id="7697e-218">a.</span><span class="sxs-lookup"><span data-stu-id="7697e-218">a.</span></span> <span data-ttu-id="7697e-219">Merhaba, **ad** metin kutusuna, "Britta." yazın</span><span class="sxs-lookup"><span data-stu-id="7697e-219">In hello **First Name** textbox, type "Britta."</span></span>
   
    <span data-ttu-id="7697e-220">b.</span><span class="sxs-lookup"><span data-stu-id="7697e-220">b.</span></span> <span data-ttu-id="7697e-221">Merhaba, **Soyadı** metin kutusuna, "Simon." yazın</span><span class="sxs-lookup"><span data-stu-id="7697e-221">In hello **Last Name** textbox, type "Simon."</span></span>
   
    <span data-ttu-id="7697e-222">c.</span><span class="sxs-lookup"><span data-stu-id="7697e-222">c.</span></span> <span data-ttu-id="7697e-223">Merhaba, **e-posta adresi** metin kutusuna, Azure Active Directory'de Britta Simon'ın e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="7697e-223">In hello **Email Address** textbox, type Britta Simon's email address in Azure Active Directory.</span></span>
   
    <span data-ttu-id="7697e-224">d.</span><span class="sxs-lookup"><span data-stu-id="7697e-224">d.</span></span> <span data-ttu-id="7697e-225">Tıklatın **kişiyi ekler**.</span><span class="sxs-lookup"><span data-stu-id="7697e-225">Click **Add Person**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="7697e-226">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="7697e-226">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="7697e-227">Bu bölümde, erişim tooWorkfront vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="7697e-227">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWorkfront.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="7697e-229">**tooassign Britta Simon tooWorkfront hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7697e-229">**tooassign Britta Simon tooWorkfront, perform hello following steps:**</span></span>

1. <span data-ttu-id="7697e-230">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="7697e-230">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="7697e-232">Merhaba uygulamalar listesinde **Workfront**.</span><span class="sxs-lookup"><span data-stu-id="7697e-232">In hello applications list, select **Workfront**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_app.png) 

3. <span data-ttu-id="7697e-234">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="7697e-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="7697e-236">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7697e-236">Click **Add** button.</span></span> <span data-ttu-id="7697e-237">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="7697e-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="7697e-239">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="7697e-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7697e-240">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="7697e-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7697e-241">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="7697e-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7697e-242">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="7697e-242">Testing single sign-on</span></span>

<span data-ttu-id="7697e-243">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="7697e-243">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="7697e-244">Merhaba Workfront hello erişim paneli parçasında tıkladığınızda, oturum açma sayfasına Workfront uygulamasının almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7697e-244">When you click hello Workfront tile in hello Access Panel, you should get login page of Workfront application.</span></span>
<span data-ttu-id="7697e-245">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7697e-245">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7697e-246">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="7697e-246">Additional resources</span></span>

* [<span data-ttu-id="7697e-247">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="7697e-247">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7697e-248">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="7697e-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_04.png
[21]:./media/active-directory-saas-workfront-tutorial/tutorial_attask_08.png
[23]:./media/active-directory-saas-workfront-tutorial/tutorial_attask_06.png
[100]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_203.png

