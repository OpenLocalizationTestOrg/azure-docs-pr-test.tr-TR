---
title: "Öğretici: Azure Active Directory Tümleştirme ile RunMyProcess | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile RunMyProcess arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d31f7395-048b-4a61-9505-5acf9fc68d9b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: f02acda015aeb8d131d8e3ef88bf50c4e8e94750
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-runmyprocess"></a><span data-ttu-id="6256f-103">Öğretici: Azure Active Directory Tümleştirme RunMyProcess ile</span><span class="sxs-lookup"><span data-stu-id="6256f-103">Tutorial: Azure Active Directory integration with RunMyProcess</span></span>

<span data-ttu-id="6256f-104">Bu öğreticide, bilgi nasıl toointegrate RunMyProcess Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6256f-104">In this tutorial, you learn how toointegrate RunMyProcess with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6256f-105">RunMyProcess Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="6256f-105">Integrating RunMyProcess with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6256f-106">Erişim tooRunMyProcess sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="6256f-106">You can control in Azure AD who has access tooRunMyProcess</span></span>
- <span data-ttu-id="6256f-107">Kullanıcıların tooautomatically get açan tooRunMyProcess (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="6256f-107">You can enable your users tooautomatically get signed-on tooRunMyProcess (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6256f-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="6256f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="6256f-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6256f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6256f-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="6256f-110">Prerequisites</span></span>

<span data-ttu-id="6256f-111">tooconfigure RunMyProcess ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="6256f-111">tooconfigure Azure AD integration with RunMyProcess, you need hello following items:</span></span>

- <span data-ttu-id="6256f-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="6256f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6256f-113">Bir RunMyProcess çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="6256f-113">A RunMyProcess single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6256f-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="6256f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6256f-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="6256f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6256f-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="6256f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6256f-117">Bir Azure AD deneme ortam yoksa, burada bir aylık deneme elde edebilirsiniz:[deneme teklifi](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6256f-117">If you don't have an Azure AD trial environment, you can get a one-month trial here:[Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6256f-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="6256f-118">Scenario description</span></span>
<span data-ttu-id="6256f-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="6256f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6256f-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="6256f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6256f-121">Merhaba Galerisi'nden RunMyProcess ekleme</span><span class="sxs-lookup"><span data-stu-id="6256f-121">Adding RunMyProcess from hello gallery</span></span>
2. <span data-ttu-id="6256f-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="6256f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-runmyprocess-from-hello-gallery"></a><span data-ttu-id="6256f-123">Merhaba Galerisi'nden RunMyProcess ekleme</span><span class="sxs-lookup"><span data-stu-id="6256f-123">Adding RunMyProcess from hello gallery</span></span>
<span data-ttu-id="6256f-124">Azure AD'ye tooconfigure hello tümleştirme RunMyProcess, tooadd RunMyProcess hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="6256f-124">tooconfigure hello integration of RunMyProcess into Azure AD, you need tooadd RunMyProcess from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6256f-125">**tooadd RunMyProcess hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6256f-125">**tooadd RunMyProcess from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6256f-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="6256f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6256f-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="6256f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6256f-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="6256f-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="6256f-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="6256f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="6256f-133">Merhaba arama kutusuna yazın **RunMyProcess**.</span><span class="sxs-lookup"><span data-stu-id="6256f-133">In hello search box, type **RunMyProcess**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_search.png)

5. <span data-ttu-id="6256f-135">Merhaba Sonuçlar panelinde seçin **RunMyProcess**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="6256f-135">In hello results panel, select **RunMyProcess**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6256f-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="6256f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6256f-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı RunMyProcess sınayın.</span><span class="sxs-lookup"><span data-stu-id="6256f-138">In this section, you configure and test Azure AD single sign-on with RunMyProcess based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6256f-139">Tek toowork'ın oturum açma hangi hello karşılık gelen RunMyProcess içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="6256f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in RunMyProcess is tooa user in Azure AD.</span></span> <span data-ttu-id="6256f-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı RunMyProcess hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="6256f-140">In other words, a link relationship between an Azure AD user and hello related user in RunMyProcess needs toobe established.</span></span>

<span data-ttu-id="6256f-141">Merhaba hello değeri RunMyProcess içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="6256f-141">In RunMyProcess, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="6256f-142">tooconfigure ve RunMyProcess ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="6256f-142">tooconfigure and test Azure AD single sign-on with RunMyProcess, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6256f-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="6256f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6256f-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="6256f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6256f-145">**[RunMyProcess test kullanıcısı oluşturma](#creating-a-runmyprocess-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir RunMyProcess içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="6256f-145">**[Creating a RunMyProcess test user](#creating-a-runmyprocess-test-user)** - toohave a counterpart of Britta Simon in RunMyProcess that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6256f-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="6256f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6256f-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="6256f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6256f-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="6256f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6256f-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma RunMyProcess uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="6256f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your RunMyProcess application.</span></span>

<span data-ttu-id="6256f-150">**tooconfigure Azure AD çoklu oturum açma ile RunMyProcess, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6256f-150">**tooconfigure Azure AD single sign-on with RunMyProcess, perform hello following steps:**</span></span>

1. <span data-ttu-id="6256f-151">Hello hello üzerinde Azure portal'ın **RunMyProcess** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="6256f-151">In hello Azure portal, on hello **RunMyProcess** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="6256f-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="6256f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_samlbase.png)

3. <span data-ttu-id="6256f-155">Merhaba üzerinde **RunMyProcess etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="6256f-155">On hello **RunMyProcess Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_url.png)

    <span data-ttu-id="6256f-157">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://live.runmyprocess.com/live/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="6256f-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://live.runmyprocess.com/live/<tenant id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6256f-158">Merhaba değeri gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="6256f-158">hello value is not real.</span></span> <span data-ttu-id="6256f-159">Güncelleştirme hello değerle hello gerçek oturum açma URL'si.</span><span class="sxs-lookup"><span data-stu-id="6256f-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="6256f-160">Kişi [RunMyProcess istemci destek ekibi](mailto:support@runmyprocess.com) tooget hello değeri.</span><span class="sxs-lookup"><span data-stu-id="6256f-160">Contact [RunMyProcess Client support team](mailto:support@runmyprocess.com) tooget hello value.</span></span> 

4. <span data-ttu-id="6256f-161">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="6256f-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_certificate.png) 

5. <span data-ttu-id="6256f-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="6256f-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6256f-165">Merhaba üzerinde **RunMyProcess yapılandırma** 'yi tıklatın **yapılandırma RunMyProcess** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="6256f-165">On hello **RunMyProcess Configuration** section, click **Configure RunMyProcess** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="6256f-166">Kopya hello **Sign-Out URL ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="6256f-166">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_configure.png) 

7. <span data-ttu-id="6256f-168">Bir farklı web tarayıcısı penceresinde, bir yönetici olarak oturum açma tooyour RunMyProcess Kiracı.</span><span class="sxs-lookup"><span data-stu-id="6256f-168">In a different web browser window, sign-on tooyour RunMyProcess tenant as an administrator.</span></span>

8. <span data-ttu-id="6256f-169">Sol gezinti panelinde tıklatın **hesap** seçip **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="6256f-169">In left navigation panel, click **Account** and select **Configuration**.</span></span>
   
    ![Çoklu oturum açma uygulama tarafında yapılandırma](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_001.png)

9. <span data-ttu-id="6256f-171">Çok Git**kimlik doğrulama yöntemini** bölümünde ve aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="6256f-171">Go too**Authentication method** section and perform below steps:</span></span>
   
    ![Çoklu oturum açma uygulama tarafında yapılandırma](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_002.png)

    <span data-ttu-id="6256f-173">a.</span><span class="sxs-lookup"><span data-stu-id="6256f-173">a.</span></span> <span data-ttu-id="6256f-174">Olarak **yöntemi**seçin **Samlv2 SSO'su**.</span><span class="sxs-lookup"><span data-stu-id="6256f-174">As **Method**, select **SSO with Samlv2**.</span></span> 

    <span data-ttu-id="6256f-175">b.</span><span class="sxs-lookup"><span data-stu-id="6256f-175">b.</span></span> <span data-ttu-id="6256f-176">Merhaba, **SSO yeniden yönlendirme** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="6256f-176">In hello **SSO redirect** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="6256f-177">c.</span><span class="sxs-lookup"><span data-stu-id="6256f-177">c.</span></span> <span data-ttu-id="6256f-178">Merhaba, **oturumu kapatıp yeniden yönlendirme** metin kutusuna, Yapıştır hello değerini **Sign-Out URL**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="6256f-178">In hello **Logout redirect** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="6256f-179">d.</span><span class="sxs-lookup"><span data-stu-id="6256f-179">d.</span></span> <span data-ttu-id="6256f-180">Merhaba, **ad kimliği biçimi** metin kutusuna, tür hello değeri **ad tanımlayıcısı biçimi** olarak **urn: OASIS: adları: tc: SAML:1.1:nameid-biçimi: emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="6256f-180">In hello **Name Id Format** textbox, type hello value of **Name Identifier Format** as **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="6256f-181">e.</span><span class="sxs-lookup"><span data-stu-id="6256f-181">e.</span></span> <span data-ttu-id="6256f-182">Merhaba hello indirilen sertifika dosyasının içeriğini kopyalayın ve hello yapıştırma **sertifika** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="6256f-182">Copy hello content of hello downloaded certificate file and then paste it into hello **Certificate** textbox.</span></span> 
 
    <span data-ttu-id="6256f-183">f.</span><span class="sxs-lookup"><span data-stu-id="6256f-183">f.</span></span> <span data-ttu-id="6256f-184">Tıklatın **kaydetmek** simgesi.</span><span class="sxs-lookup"><span data-stu-id="6256f-184">Click **Save** icon.</span></span>

> [!TIP]
> <span data-ttu-id="6256f-185">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="6256f-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6256f-186">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="6256f-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6256f-187">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6256f-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6256f-188">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6256f-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="6256f-189">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="6256f-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="6256f-191">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6256f-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6256f-192">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="6256f-192">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6256f-194">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="6256f-194">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6256f-196">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="6256f-196">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6256f-198">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="6256f-198">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6256f-200">a.</span><span class="sxs-lookup"><span data-stu-id="6256f-200">a.</span></span> <span data-ttu-id="6256f-201">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6256f-201">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6256f-202">b.</span><span class="sxs-lookup"><span data-stu-id="6256f-202">b.</span></span> <span data-ttu-id="6256f-203">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="6256f-203">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6256f-204">c.</span><span class="sxs-lookup"><span data-stu-id="6256f-204">c.</span></span> <span data-ttu-id="6256f-205">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="6256f-205">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="6256f-206">d.</span><span class="sxs-lookup"><span data-stu-id="6256f-206">d.</span></span> <span data-ttu-id="6256f-207">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6256f-207">Click **Create**.</span></span>
 
### <a name="creating-a-runmyprocess-test-user"></a><span data-ttu-id="6256f-208">RunMyProcess test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6256f-208">Creating a RunMyProcess test user</span></span>

<span data-ttu-id="6256f-209">TooRunMyProcess içinde sipariş tooenable Azure AD kullanıcıların toolog bunların RunMyProcess sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="6256f-209">In order tooenable Azure AD users toolog in tooRunMyProcess, they must be provisioned into RunMyProcess.</span></span> <span data-ttu-id="6256f-210">RunMyProcess Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="6256f-210">In hello case of RunMyProcess, provisioning is a manual task.</span></span>

<span data-ttu-id="6256f-211">**bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6256f-211">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="6256f-212">İçinde tooyour RunMyProcess şirket site yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="6256f-212">Log in tooyour RunMyProcess company site as an administrator.</span></span>

2. <span data-ttu-id="6256f-213">Tıklatın **hesap** seçip **kullanıcılar** sol gezinti panelinde, ardından **yeni kullanıcı**.</span><span class="sxs-lookup"><span data-stu-id="6256f-213">Click **Account** and select **Users** in left navigation panel, then click **New User**.</span></span>
   
    <span data-ttu-id="6256f-214">![Yeni kullanıcı](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_003.png "yeni kullanıcı")</span><span class="sxs-lookup"><span data-stu-id="6256f-214">![New User](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_003.png "New User")</span></span>

3. <span data-ttu-id="6256f-215">Merhaba, **kullanıcı ayarları** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="6256f-215">In hello **User Settings** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="6256f-216">![Profil](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_004.png "profili")</span><span class="sxs-lookup"><span data-stu-id="6256f-216">![Profile](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_004.png "Profile")</span></span> 
  
    <span data-ttu-id="6256f-217">a.</span><span class="sxs-lookup"><span data-stu-id="6256f-217">a.</span></span> <span data-ttu-id="6256f-218">Türü hello **adı** ve **e-posta** geçerli bir Azure hello tooprovision istediğiniz AD hesabının ilgili metin kutuları.</span><span class="sxs-lookup"><span data-stu-id="6256f-218">Type hello **Name** and **E-mail** of a valid Azure AD account you want tooprovision into hello related textboxes.</span></span> 

    <span data-ttu-id="6256f-219">b.</span><span class="sxs-lookup"><span data-stu-id="6256f-219">b.</span></span> <span data-ttu-id="6256f-220">Seçin bir **IDE dil**, **dil**, ve **profil**.</span><span class="sxs-lookup"><span data-stu-id="6256f-220">Select an **IDE language**, **Language**, and **Profile**.</span></span> 

    <span data-ttu-id="6256f-221">c.</span><span class="sxs-lookup"><span data-stu-id="6256f-221">c.</span></span> <span data-ttu-id="6256f-222">Seçin **Gönder hesap oluşturma e-posta toome**.</span><span class="sxs-lookup"><span data-stu-id="6256f-222">Select **Send account creation e-mail toome**.</span></span> 

    <span data-ttu-id="6256f-223">d.</span><span class="sxs-lookup"><span data-stu-id="6256f-223">d.</span></span> <span data-ttu-id="6256f-224">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6256f-224">Click **Save**.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="6256f-225">API, kullanıcı hesaplarını RunMyProcess tooprovision Azure Active Directory tarafından sağlanan veya herhangi diğer RunMyProcess kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6256f-225">You can use any other RunMyProcess user account creation tools or APIs provided by RunMyProcess tooprovision Azure Active Directory user accounts.</span></span> 
    > 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="6256f-226">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="6256f-226">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="6256f-227">Bu bölümde, erişim tooRunMyProcess vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="6256f-227">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRunMyProcess.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="6256f-229">**tooassign Britta Simon tooRunMyProcess hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6256f-229">**tooassign Britta Simon tooRunMyProcess, perform hello following steps:**</span></span>

1. <span data-ttu-id="6256f-230">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="6256f-230">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="6256f-232">Merhaba uygulamalar listesinde **RunMyProcess**.</span><span class="sxs-lookup"><span data-stu-id="6256f-232">In hello applications list, select **RunMyProcess**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_app.png) 

3. <span data-ttu-id="6256f-234">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="6256f-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="6256f-236">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="6256f-236">Click **Add** button.</span></span> <span data-ttu-id="6256f-237">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="6256f-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="6256f-239">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="6256f-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6256f-240">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="6256f-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6256f-241">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="6256f-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6256f-242">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="6256f-242">Testing single sign-on</span></span>

<span data-ttu-id="6256f-243">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD SSO yapılandırmayı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="6256f-243">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="6256f-244">Hello erişim paneli RunMyProcess döşeme hello tıkladığınızda, otomatik olarak oturum açma RunMyProcess uygulama tooyour almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6256f-244">When you click hello RunMyProcess tile in hello Access Panel, you should get automatically signed-on tooyour RunMyProcess application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6256f-245">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="6256f-245">Additional resources</span></span>

* [<span data-ttu-id="6256f-246">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="6256f-246">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6256f-247">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="6256f-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_203.png

