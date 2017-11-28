---
title: "Öğretici: Azure Active Directory Tümleştirme ile TargetProcess | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile TargetProcess arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 7cb91628-e758-480d-a233-7a3caaaff50d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 05c574e2c18d7f73edc6c094093a6e59d46b8e6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-targetprocess"></a><span data-ttu-id="b168a-103">Öğretici: Azure Active Directory Tümleştirme TargetProcess ile</span><span class="sxs-lookup"><span data-stu-id="b168a-103">Tutorial: Azure Active Directory integration with TargetProcess</span></span>

<span data-ttu-id="b168a-104">Bu öğreticide, bilgi nasıl toointegrate TargetProcess Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b168a-104">In this tutorial, you learn how toointegrate TargetProcess with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b168a-105">TargetProcess Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="b168a-105">Integrating TargetProcess with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b168a-106">Erişim tooTargetProcess sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="b168a-106">You can control in Azure AD who has access tooTargetProcess</span></span>
- <span data-ttu-id="b168a-107">Kullanıcıların tooautomatically get açan tooTargetProcess (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="b168a-107">You can enable your users tooautomatically get signed-on tooTargetProcess (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b168a-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="b168a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b168a-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b168a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b168a-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="b168a-110">Prerequisites</span></span>

<span data-ttu-id="b168a-111">tooconfigure TargetProcess ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="b168a-111">tooconfigure Azure AD integration with TargetProcess, you need hello following items:</span></span>

- <span data-ttu-id="b168a-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="b168a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b168a-113">Bir TargetProcess çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="b168a-113">A TargetProcess single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b168a-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="b168a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b168a-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="b168a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b168a-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="b168a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b168a-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b168a-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b168a-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="b168a-118">Scenario description</span></span>
<span data-ttu-id="b168a-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="b168a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b168a-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="b168a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b168a-121">Merhaba Galerisi'nden TargetProcess ekleme</span><span class="sxs-lookup"><span data-stu-id="b168a-121">Add TargetProcess from hello gallery</span></span>
2. <span data-ttu-id="b168a-122">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="b168a-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-targetprocess-from-hello-gallery"></a><span data-ttu-id="b168a-123">Merhaba Galerisi'nden TargetProcess ekleme</span><span class="sxs-lookup"><span data-stu-id="b168a-123">Add TargetProcess from hello gallery</span></span>
<span data-ttu-id="b168a-124">Azure AD'ye tooconfigure hello tümleştirme TargetProcess, tooadd TargetProcess hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="b168a-124">tooconfigure hello integration of TargetProcess into Azure AD, you need tooadd TargetProcess from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b168a-125">**tooadd TargetProcess hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="b168a-125">**tooadd TargetProcess from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b168a-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="b168a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b168a-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="b168a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b168a-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="b168a-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="b168a-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="b168a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="b168a-133">Merhaba arama kutusuna yazın **TargetProcess**seçin **TargetProcess** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="b168a-133">In hello search box, type **TargetProcess**, select **TargetProcess**  from result panel then click **Add** button tooadd hello application.</span></span>

    ![Galeriden Ekle TargetProcess](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="b168a-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="b168a-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="b168a-136">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı TargetProcess sınayın.</span><span class="sxs-lookup"><span data-stu-id="b168a-136">In this section, you configure and test Azure AD single sign-on with TargetProcess based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b168a-137">Tek toowork'ın oturum açma hangi hello karşılık gelen TargetProcess içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="b168a-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TargetProcess is tooa user in Azure AD.</span></span> <span data-ttu-id="b168a-138">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı TargetProcess hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="b168a-138">In other words, a link relationship between an Azure AD user and hello related user in TargetProcess needs toobe established.</span></span>

<span data-ttu-id="b168a-139">Merhaba hello değeri TargetProcess içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="b168a-139">In TargetProcess, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="b168a-140">tooconfigure ve TargetProcess ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="b168a-140">tooconfigure and test Azure AD single sign-on with TargetProcess, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b168a-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="b168a-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b168a-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="b168a-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b168a-143">**[TargetProcess test kullanıcısı oluşturma](#create-a-targetprocess-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir TargetProcess içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="b168a-143">**[Create a TargetProcess test user](#create-a-targetprocess-test-user)** - toohave a counterpart of Britta Simon in TargetProcess that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b168a-144">**[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="b168a-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b168a-145">**[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="b168a-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="b168a-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="b168a-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="b168a-147">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma TargetProcess uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="b168a-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TargetProcess application.</span></span>

<span data-ttu-id="b168a-148">**tooconfigure Azure AD çoklu oturum açma ile TargetProcess, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="b168a-148">**tooconfigure Azure AD single sign-on with TargetProcess, perform hello following steps:**</span></span>

1. <span data-ttu-id="b168a-149">Hello hello üzerinde Azure portal'ın **TargetProcess** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="b168a-149">In hello Azure portal, on hello **TargetProcess** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="b168a-151">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="b168a-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![SAML tabanlı oturum açma](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_samlbase.png)

3. <span data-ttu-id="b168a-153">Merhaba üzerinde **TargetProcess etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="b168a-153">On hello **TargetProcess Domain and URLs** section, perform hello following steps:</span></span>

    ![TargetProcess etki alanı ve URL'ler bölümü](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_url.png)

    <span data-ttu-id="b168a-155">a.</span><span class="sxs-lookup"><span data-stu-id="b168a-155">a.</span></span> <span data-ttu-id="b168a-156">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.tpondemand.com/`</span><span class="sxs-lookup"><span data-stu-id="b168a-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.tpondemand.com/`</span></span>

    <span data-ttu-id="b168a-157">b.</span><span class="sxs-lookup"><span data-stu-id="b168a-157">b.</span></span> <span data-ttu-id="b168a-158">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.tpondemand.com/`</span><span class="sxs-lookup"><span data-stu-id="b168a-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.tpondemand.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b168a-159">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="b168a-159">These values are not real.</span></span> <span data-ttu-id="b168a-160">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="b168a-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="b168a-161">Kişi [TargetProcess istemci destek ekibi](mailto:support@targetprocess.com) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="b168a-161">Contact [TargetProcess Client support team](mailto:support@targetprocess.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="b168a-162">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="b168a-162">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![SAML imzalama sertifikası bölümü](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_certificate.png) 

5. <span data-ttu-id="b168a-164">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="b168a-164">Click **Save** button.</span></span>

    ![Kaydet düğmesi](./media/active-directory-saas-target-process-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b168a-166">Merhaba üzerinde **TargetProcess yapılandırma** 'yi tıklatın **yapılandırma TargetProcess** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="b168a-166">On hello **TargetProcess Configuration** section, click **Configure TargetProcess** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="b168a-167">Kopya hello **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="b168a-167">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![TargetProcess yapılandırma bölümü](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_configure.png) 

7. <span data-ttu-id="b168a-169">Oturum açma TargetProcess uygulama yönetici olarak tooyour.</span><span class="sxs-lookup"><span data-stu-id="b168a-169">Sign-on tooyour TargetProcess application as an administrator.</span></span>

8. <span data-ttu-id="b168a-170">Hello içinde hello üst menüsünde **Kurulum**.</span><span class="sxs-lookup"><span data-stu-id="b168a-170">In hello menu on hello top, click **Setup**.</span></span>
   
    ![Kurulum](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_05.png)

9. <span data-ttu-id="b168a-172">Tıklatın **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="b168a-172">Click **Settings**.</span></span>
   
    ![Ayarlar](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_06.png) 

10. <span data-ttu-id="b168a-174">Tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="b168a-174">Click **Single Sign-on**.</span></span>
   
    ![Çoklu oturum açma'ı tıklatın](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_07.png) 

11. <span data-ttu-id="b168a-176">Merhaba çoklu oturum açma ayarları iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="b168a-176">On hello Single Sign-on settings dialog, perform hello following steps:</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_08.png)
    
    <span data-ttu-id="b168a-178">a.</span><span class="sxs-lookup"><span data-stu-id="b168a-178">a.</span></span> <span data-ttu-id="b168a-179">Tıklatın **çoklu oturum açmayı etkinleştir**.</span><span class="sxs-lookup"><span data-stu-id="b168a-179">Click **Enable Single Sign-on**.</span></span>
    
    <span data-ttu-id="b168a-180">b.</span><span class="sxs-lookup"><span data-stu-id="b168a-180">b.</span></span> <span data-ttu-id="b168a-181">İçinde **oturum açma URL'si** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="b168a-181">In **Sign-on URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="b168a-182">c.</span><span class="sxs-lookup"><span data-stu-id="b168a-182">c.</span></span> <span data-ttu-id="b168a-183">İndirilen sertifikanızı kopyalama Merhaba içeriğine Not Defteri'nde açın ve hello yapıştırma **sertifika** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="b168a-183">Open your downloaded certificate in notepad, copy hello content, and then paste it into hello **Certificate** textbox.</span></span>
    
    <span data-ttu-id="b168a-184">d.</span><span class="sxs-lookup"><span data-stu-id="b168a-184">d.</span></span> <span data-ttu-id="b168a-185">tıklatın **JIT etkinleştirme sağlama**.</span><span class="sxs-lookup"><span data-stu-id="b168a-185">click **Enable JIT Provisioning**.</span></span>

    <span data-ttu-id="b168a-186">e.</span><span class="sxs-lookup"><span data-stu-id="b168a-186">e.</span></span> <span data-ttu-id="b168a-187">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b168a-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="b168a-188">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="b168a-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b168a-189">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="b168a-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b168a-190">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b168a-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b168a-191">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="b168a-191">Create an Azure AD test user</span></span>
<span data-ttu-id="b168a-192">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="b168a-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="b168a-194">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="b168a-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b168a-195">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="b168a-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-target-process-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b168a-197">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="b168a-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Kullanıcıların toodisplay hello listesi](./media/active-directory-saas-target-process-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b168a-199">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="b168a-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Ekle düğmesi](./media/active-directory-saas-target-process-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b168a-201">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="b168a-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Kullanıcı bölümü](./media/active-directory-saas-target-process-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b168a-203">a.</span><span class="sxs-lookup"><span data-stu-id="b168a-203">a.</span></span> <span data-ttu-id="b168a-204">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b168a-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b168a-205">b.</span><span class="sxs-lookup"><span data-stu-id="b168a-205">b.</span></span> <span data-ttu-id="b168a-206">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="b168a-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b168a-207">c.</span><span class="sxs-lookup"><span data-stu-id="b168a-207">c.</span></span> <span data-ttu-id="b168a-208">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="b168a-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b168a-209">d.</span><span class="sxs-lookup"><span data-stu-id="b168a-209">d.</span></span> <span data-ttu-id="b168a-210">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b168a-210">Click **Create**.</span></span>
 
### <a name="create-a-targetprocess-test-user"></a><span data-ttu-id="b168a-211">TargetProcess test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="b168a-211">Create a TargetProcess test user</span></span>

<span data-ttu-id="b168a-212">Bu bölümde Hello amacı toocreate Britta Simon içinde TargetProcess adlı bir kullanıcı ' dir.</span><span class="sxs-lookup"><span data-stu-id="b168a-212">hello objective of this section is toocreate a user called Britta Simon in TargetProcess.</span></span>

<span data-ttu-id="b168a-213">Yalnızca zaman sağlama TargetProcess destekler.</span><span class="sxs-lookup"><span data-stu-id="b168a-213">TargetProcess supports just-in-time provisioning.</span></span> <span data-ttu-id="b168a-214">İçinde zaten etkinleştirdiğiniz [yapılandırma Azure AD çoklu oturum açma](#configuring-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="b168a-214">You have already enabled it in [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

<span data-ttu-id="b168a-215">Bu bölümde, eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="b168a-215">There is no action item for you in this section.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="b168a-216">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="b168a-216">Assign hello Azure AD test user</span></span>

<span data-ttu-id="b168a-217">Bu bölümde, erişim tooTargetProcess vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="b168a-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTargetProcess.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="b168a-219">**tooassign Britta Simon tooTargetProcess hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="b168a-219">**tooassign Britta Simon tooTargetProcess, perform hello following steps:**</span></span>

1. <span data-ttu-id="b168a-220">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="b168a-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="b168a-222">Merhaba uygulamalar listesinde **TargetProcess**.</span><span class="sxs-lookup"><span data-stu-id="b168a-222">In hello applications list, select **TargetProcess**.</span></span>

    ![Uygulama listesinde TargetProcess](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_app.png) 

3. <span data-ttu-id="b168a-224">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="b168a-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="b168a-226">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="b168a-226">Click **Add** button.</span></span> <span data-ttu-id="b168a-227">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="b168a-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="b168a-229">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="b168a-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b168a-230">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="b168a-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b168a-231">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="b168a-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="b168a-232">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="b168a-232">Test single sign-on</span></span>

<span data-ttu-id="b168a-233">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="b168a-233">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b168a-234">Hello erişim paneli TargetProcess döşeme hello tıkladığınızda, otomatik olarak oturum açma TargetProcess uygulama tooyour almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b168a-234">When you click hello TargetProcess tile in hello Access Panel, you should get automatically signed-on tooyour TargetProcess application.</span></span> <span data-ttu-id="b168a-235">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b168a-235">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b168a-236">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="b168a-236">Additional resources</span></span>

* [<span data-ttu-id="b168a-237">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="b168a-237">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b168a-238">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="b168a-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_203.png

