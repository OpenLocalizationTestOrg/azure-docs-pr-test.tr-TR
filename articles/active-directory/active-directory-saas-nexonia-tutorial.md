---
title: "Öğretici: Azure Active Directory Tümleştirme ile Nexonia | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Nexonia arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a93b771a-9bc3-444a-bdc0-457f8bb7e780
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/1/2017
ms.author: jeedes
ms.openlocfilehash: 3778804084a7989414260bae5654cf76e9ccca6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-nexonia"></a><span data-ttu-id="7abf1-103">Öğretici: Azure Active Directory Tümleştirme Nexonia ile</span><span class="sxs-lookup"><span data-stu-id="7abf1-103">Tutorial: Azure Active Directory integration with Nexonia</span></span>

<span data-ttu-id="7abf1-104">Bu öğreticide, bilgi nasıl toointegrate Nexonia Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7abf1-104">In this tutorial, you learn how toointegrate Nexonia with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7abf1-105">Nexonia Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="7abf1-105">Integrating Nexonia with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7abf1-106">Erişim tooNexonia sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="7abf1-106">You can control in Azure AD who has access tooNexonia</span></span>
- <span data-ttu-id="7abf1-107">Kullanıcıların tooautomatically get açan tooNexonia (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="7abf1-107">You can enable your users tooautomatically get signed-on tooNexonia (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7abf1-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="7abf1-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7abf1-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz.</span><span class="sxs-lookup"><span data-stu-id="7abf1-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="7abf1-110">[Uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7abf1-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7abf1-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="7abf1-111">Prerequisites</span></span>

<span data-ttu-id="7abf1-112">tooconfigure Nexonia ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="7abf1-112">tooconfigure Azure AD integration with Nexonia, you need hello following items:</span></span>

- <span data-ttu-id="7abf1-113">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="7abf1-113">An Azure AD subscription</span></span>
- <span data-ttu-id="7abf1-114">Bir Nexonia çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="7abf1-114">A Nexonia single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7abf1-115">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="7abf1-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7abf1-116">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="7abf1-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7abf1-117">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="7abf1-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7abf1-118">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7abf1-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7abf1-119">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="7abf1-119">Scenario description</span></span>
<span data-ttu-id="7abf1-120">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="7abf1-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7abf1-121">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="7abf1-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7abf1-122">Merhaba Galerisi'nden Nexonia ekleme</span><span class="sxs-lookup"><span data-stu-id="7abf1-122">Adding Nexonia from hello gallery</span></span>
2. <span data-ttu-id="7abf1-123">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="7abf1-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-nexonia-from-hello-gallery"></a><span data-ttu-id="7abf1-124">Merhaba Galerisi'nden Nexonia ekleme</span><span class="sxs-lookup"><span data-stu-id="7abf1-124">Adding Nexonia from hello gallery</span></span>
<span data-ttu-id="7abf1-125">Azure AD'ye tooconfigure hello tümleştirme Nexonia, tooadd Nexonia hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="7abf1-125">tooconfigure hello integration of Nexonia into Azure AD, you need tooadd Nexonia from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7abf1-126">**tooadd Nexonia hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7abf1-126">**tooadd Nexonia from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7abf1-127">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="7abf1-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7abf1-129">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="7abf1-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7abf1-130">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="7abf1-130">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="7abf1-132">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7abf1-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="7abf1-134">Merhaba arama kutusuna yazın **Nexonia**.</span><span class="sxs-lookup"><span data-stu-id="7abf1-134">In hello search box, type **Nexonia**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_search.png)

5. <span data-ttu-id="7abf1-136">Merhaba Sonuçlar panelinde seçin **Nexonia**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="7abf1-136">In hello results panel, select **Nexonia**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7abf1-138">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="7abf1-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7abf1-139">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Nexonia ile test etme</span><span class="sxs-lookup"><span data-stu-id="7abf1-139">In this section, you configure and test Azure AD single sign-on with Nexonia based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7abf1-140">Tek toowork'ın oturum açma hangi hello karşılık gelen Nexonia içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="7abf1-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Nexonia is tooa user in Azure AD.</span></span> <span data-ttu-id="7abf1-141">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Nexonia hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="7abf1-141">In other words, a link relationship between an Azure AD user and hello related user in Nexonia needs toobe established.</span></span>

<span data-ttu-id="7abf1-142">Merhaba hello değeri Nexonia içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="7abf1-142">In Nexonia, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7abf1-143">tooconfigure ve Nexonia ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="7abf1-143">tooconfigure and test Azure AD single sign-on with Nexonia, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7abf1-144">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="7abf1-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7abf1-145">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="7abf1-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7abf1-146">**[Nexonia test kullanıcısı oluşturma](#creating-a-nexonia-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Nexonia içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="7abf1-146">**[Creating a Nexonia test user](#creating-a-nexonia-test-user)** - toohave a counterpart of Britta Simon in Nexonia that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7abf1-147">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="7abf1-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7abf1-148">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="7abf1-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7abf1-149">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="7abf1-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7abf1-150">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Nexonia uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="7abf1-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Nexonia application.</span></span>

>[!Note]
><span data-ttu-id="7abf1-151">Merhaba tümleştirme sırasında sorunlarla sonra bu [bağlantı](https://docs.microsoft.com/azure/active-directory/application-sign-in-problem-federated-sso-gallery?WT.mc_id=UI_AAD_Enterprise_Apps_SupportOrTroubleshooting) sorun giderme kılavuzu için.</span><span class="sxs-lookup"><span data-stu-id="7abf1-151">If you have issues in hello integration then refer this [link](https://docs.microsoft.com/azure/active-directory/application-sign-in-problem-federated-sso-gallery?WT.mc_id=UI_AAD_Enterprise_Apps_SupportOrTroubleshooting) for troubleshooting guide.</span></span> <span data-ttu-id="7abf1-152">Merhaba çözüm hala bulunamadı, Azure portalından hello destek isteği yükseltin.</span><span class="sxs-lookup"><span data-stu-id="7abf1-152">If you still have not found hello solution, then raise hello support request from Azure portal.</span></span>

<span data-ttu-id="7abf1-153">**tooconfigure Azure AD çoklu oturum açma ile Nexonia, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7abf1-153">**tooconfigure Azure AD single sign-on with Nexonia, perform hello following steps:**</span></span>

1. <span data-ttu-id="7abf1-154">Hello hello üzerinde Azure portal'ın **Nexonia** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="7abf1-154">In hello Azure portal, on hello **Nexonia** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="7abf1-156">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="7abf1-156">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_samlbase.png)

3. <span data-ttu-id="7abf1-158">Merhaba üzerinde **Nexonia etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="7abf1-158">On hello **Nexonia Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_url.png)

    <span data-ttu-id="7abf1-160">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://system.nexonia.com/assistant/saml.do?orgCode=<organizationcode>`</span><span class="sxs-lookup"><span data-stu-id="7abf1-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://system.nexonia.com/assistant/saml.do?orgCode=<organizationcode>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7abf1-161">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="7abf1-161">This value is not real.</span></span> <span data-ttu-id="7abf1-162">Bu değer hello gerçek yanıt URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="7abf1-162">Update this value with hello actual Reply URL.</span></span> <span data-ttu-id="7abf1-163">Kişi [Nexonia destek ekibi](https://nexonia.zendesk.com/hc/requests/new) tooget bu değer.</span><span class="sxs-lookup"><span data-stu-id="7abf1-163">Contact [Nexonia support team](https://nexonia.zendesk.com/hc/requests/new) tooget this value.</span></span> 


4. <span data-ttu-id="7abf1-164">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="7abf1-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_certificate.png) 

5. <span data-ttu-id="7abf1-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7abf1-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-nexonia-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7abf1-168">Merhaba üzerinde **Nexonia yapılandırma** 'yi tıklatın **yapılandırma Nexonia** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="7abf1-168">On hello **Nexonia Configuration** section, click **Configure Nexonia** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="7abf1-169">Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="7abf1-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_configure.png) 

7. <span data-ttu-id="7abf1-171">tooget SSO yapılandırılmış uygulamanızın, kişi [Nexonia destek ekibi](https://nexonia.zendesk.com/hc/requests/new) ve ile Merhaba aşağıdakileri sağlar:</span><span class="sxs-lookup"><span data-stu-id="7abf1-171">tooget SSO configured for your application, contact [Nexonia support team](https://nexonia.zendesk.com/hc/requests/new) and provide them with hello following:</span></span>

    <span data-ttu-id="7abf1-172">• hello indirilen **sertifika**</span><span class="sxs-lookup"><span data-stu-id="7abf1-172">• hello downloaded **certificate**</span></span>

    <span data-ttu-id="7abf1-173">• hello **SAML varlık kimliği**</span><span class="sxs-lookup"><span data-stu-id="7abf1-173">• hello **SAML Entity ID**</span></span>

    <span data-ttu-id="7abf1-174">• hello **SAML çoklu oturum açma hizmet URL'si**</span><span class="sxs-lookup"><span data-stu-id="7abf1-174">• hello **SAML Single Sign-On Service URL**</span></span>

    <span data-ttu-id="7abf1-175">• hello **Sign-Out URL'si**</span><span class="sxs-lookup"><span data-stu-id="7abf1-175">• hello **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="7abf1-176">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="7abf1-176">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7abf1-177">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="7abf1-177">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7abf1-178">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7abf1-178">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7abf1-179">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7abf1-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="7abf1-180">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="7abf1-180">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="7abf1-182">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7abf1-182">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7abf1-183">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="7abf1-183">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-nexonia-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7abf1-185">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="7abf1-185">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-nexonia-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7abf1-187">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="7abf1-187">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-nexonia-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7abf1-189">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="7abf1-189">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-nexonia-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7abf1-191">a.</span><span class="sxs-lookup"><span data-stu-id="7abf1-191">a.</span></span> <span data-ttu-id="7abf1-192">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7abf1-192">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7abf1-193">b.</span><span class="sxs-lookup"><span data-stu-id="7abf1-193">b.</span></span> <span data-ttu-id="7abf1-194">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="7abf1-194">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7abf1-195">c.</span><span class="sxs-lookup"><span data-stu-id="7abf1-195">c.</span></span> <span data-ttu-id="7abf1-196">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="7abf1-196">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7abf1-197">d.</span><span class="sxs-lookup"><span data-stu-id="7abf1-197">d.</span></span> <span data-ttu-id="7abf1-198">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7abf1-198">Click **Create**.</span></span>
 
### <a name="creating-a-nexonia-test-user"></a><span data-ttu-id="7abf1-199">Nexonia test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7abf1-199">Creating a Nexonia test user</span></span>

<span data-ttu-id="7abf1-200">Bu bölümde, Nexonia içinde Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7abf1-200">In this section, you create a user called Britta Simon in Nexonia.</span></span> <span data-ttu-id="7abf1-201">Çalışmak [Nexonia destek ekibi](https://nexonia.zendesk.com/hc/requests/new) tooadd hello kullanıcılar hello Nexonia Platform.</span><span class="sxs-lookup"><span data-stu-id="7abf1-201">Work with [Nexonia support team](https://nexonia.zendesk.com/hc/requests/new) tooadd hello users in hello Nexonia platform.</span></span> <span data-ttu-id="7abf1-202">Kullanıcıların oluşturulan ve çoklu oturum açma kullanmadan önce etkinleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="7abf1-202">Users must be created and activated before you use single sign-on.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="7abf1-203">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="7abf1-203">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="7abf1-204">Bu bölümde, erişim tooNexonia vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="7abf1-204">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNexonia.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="7abf1-206">**tooassign Britta Simon tooNexonia hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7abf1-206">**tooassign Britta Simon tooNexonia, perform hello following steps:**</span></span>

1. <span data-ttu-id="7abf1-207">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="7abf1-207">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="7abf1-209">Merhaba uygulamalar listesinde **Nexonia**.</span><span class="sxs-lookup"><span data-stu-id="7abf1-209">In hello applications list, select **Nexonia**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_app.png) 

3. <span data-ttu-id="7abf1-211">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="7abf1-211">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="7abf1-213">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7abf1-213">Click **Add** button.</span></span> <span data-ttu-id="7abf1-214">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="7abf1-214">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="7abf1-216">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="7abf1-216">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7abf1-217">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="7abf1-217">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7abf1-218">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="7abf1-218">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7abf1-219">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="7abf1-219">Testing single sign-on</span></span>

<span data-ttu-id="7abf1-220">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="7abf1-220">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="7abf1-221">Merhaba Nexonia hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Nexonia uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7abf1-221">When you click hello Nexonia tile in hello Access Panel, you should get automatically signed-on tooyour Nexonia application.</span></span>
<span data-ttu-id="7abf1-222">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="7abf1-222">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7abf1-223">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="7abf1-223">Additional resources</span></span>

* [<span data-ttu-id="7abf1-224">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="7abf1-224">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7abf1-225">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="7abf1-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_203.png

