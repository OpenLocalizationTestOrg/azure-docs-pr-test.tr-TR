---
title: "Öğretici: Azure Active Directory Tümleştirme ile Citrix GoToMeeting | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve Citrix GoToMeeting arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7d7897f6-b88e-4dd5-8f3a-e612337b1413
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 46a5da7504806202a5ec29f73c504e772c61bc2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-citrix-gotomeeting"></a><span data-ttu-id="24441-103">Öğretici: Citrix GoToMeeting Azure Active Directory Tümleştirme</span><span class="sxs-lookup"><span data-stu-id="24441-103">Tutorial: Azure Active Directory integration with Citrix GoToMeeting</span></span>

<span data-ttu-id="24441-104">Bu öğreticide, bilgi nasıl toointegrate Citrix GoToMeeting Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="24441-104">In this tutorial, you learn how toointegrate Citrix GoToMeeting with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="24441-105">Citrix GoToMeeting Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="24441-105">Integrating Citrix GoToMeeting with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="24441-106">Erişim tooCitrix GoToMeeting sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="24441-106">You can control in Azure AD who has access tooCitrix GoToMeeting</span></span>
- <span data-ttu-id="24441-107">Kullanıcıların tooautomatically get açan tooCitrix GoToMeeting (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="24441-107">You can enable your users tooautomatically get signed-on tooCitrix GoToMeeting (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="24441-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="24441-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="24441-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="24441-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="24441-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="24441-110">Prerequisites</span></span>

<span data-ttu-id="24441-111">tooconfigure Citrix GoToMeeting ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="24441-111">tooconfigure Azure AD integration with Citrix GoToMeeting, you need hello following items:</span></span>

- <span data-ttu-id="24441-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="24441-112">An Azure AD subscription</span></span>
- <span data-ttu-id="24441-113">Bir Citrix GoToMeeting çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="24441-113">A Citrix GoToMeeting single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="24441-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="24441-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="24441-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="24441-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="24441-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="24441-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="24441-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="24441-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="24441-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="24441-118">Scenario description</span></span>
<span data-ttu-id="24441-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="24441-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="24441-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="24441-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="24441-121">Citrix GoToMeeting hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="24441-121">Adding Citrix GoToMeeting from hello gallery</span></span>
2. <span data-ttu-id="24441-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="24441-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-citrix-gotomeeting-from-hello-gallery"></a><span data-ttu-id="24441-123">Citrix GoToMeeting hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="24441-123">Adding Citrix GoToMeeting from hello gallery</span></span>
<span data-ttu-id="24441-124">Azure AD'ye tooconfigure hello tümleştirme Citrix GoToMeeting, tooadd Citrix GoToMeeting hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="24441-124">tooconfigure hello integration of Citrix GoToMeeting into Azure AD, you need tooadd Citrix GoToMeeting from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="24441-125">**tooadd Citrix GoToMeeting hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="24441-125">**tooadd Citrix GoToMeeting from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="24441-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="24441-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="24441-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="24441-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="24441-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="24441-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="24441-131">Tıklatın **yeni uygulama** hello iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="24441-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="24441-133">Merhaba arama kutusuna yazın **Citrix GoToMeeting**.</span><span class="sxs-lookup"><span data-stu-id="24441-133">In hello search box, type **Citrix GoToMeeting**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_search.png)

5. <span data-ttu-id="24441-135">Merhaba Sonuçlar panelinde seçin **Citrix GoToMeeting**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="24441-135">In hello results panel, select **Citrix GoToMeeting**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="24441-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="24441-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="24441-138">Bu bölümde, yapılandırmanız ve Citrix GoToMeeting ile Azure AD çoklu oturum açmayı test "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı</span><span class="sxs-lookup"><span data-stu-id="24441-138">In this section, you configure and test Azure AD single sign-on with Citrix GoToMeeting based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="24441-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Citrix GoToMeeting içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="24441-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Citrix GoToMeeting is tooa user in Azure AD.</span></span> <span data-ttu-id="24441-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve Citrix GoToMeeting hello ilgili kullanıcı arasındaki bağlantıyı ilişki kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="24441-140">In other words, a link relationship between an Azure AD user and hello related user in Citrix GoToMeeting needs toobe established.</span></span>

<span data-ttu-id="24441-141">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** Citrix GoToMeeting içinde.</span><span class="sxs-lookup"><span data-stu-id="24441-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Citrix GoToMeeting.</span></span>

<span data-ttu-id="24441-142">tooconfigure ve Citrix GoToMeeting ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="24441-142">tooconfigure and test Azure AD single sign-on with Citrix GoToMeeting, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="24441-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="24441-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="24441-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="24441-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="24441-145">**[Citrix GoToMeeting test kullanıcısı oluşturma](#creating-a-citrix-gotomeeting-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Citrix GoToMeeting içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="24441-145">**[Creating a Citrix GoToMeeting test user](#creating-a-citrix-gotomeeting-test-user)** - toohave a counterpart of Britta Simon in Citrix GoToMeeting that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="24441-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="24441-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="24441-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="24441-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="24441-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="24441-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="24441-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Citrix GoToMeeting uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="24441-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Citrix GoToMeeting application.</span></span>

<span data-ttu-id="24441-150">**tooconfigure Azure AD çoklu oturum açma Citrix GoToMeeting ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="24441-150">**tooconfigure Azure AD single sign-on with Citrix GoToMeeting, perform hello following steps:**</span></span>

1. <span data-ttu-id="24441-151">Hello hello üzerinde Azure portal'ın **Citrix GoToMeeting** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="24441-151">In hello Azure portal, on hello **Citrix GoToMeeting** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="24441-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="24441-153">On hello **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_samlbase.png)

3. <span data-ttu-id="24441-155">Merhaba üzerinde **Citrix GoToMeeting etki alanı ve URL'leri** bölümünde, gerek tooperform herhangi bir adımı.</span><span class="sxs-lookup"><span data-stu-id="24441-155">On hello **Citrix GoToMeeting Domain and URLs** section, no need tooperform any steps.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_url.png)


3. <span data-ttu-id="24441-157">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="24441-157">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_certificate.png) 

4. <span data-ttu-id="24441-159">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="24441-159">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_400.png)
    
5. <span data-ttu-id="24441-161">Hello Citrix GoToMeeting SAML yapılandırma bölümü, oturum açma yapılandırma Citrix GoToMeeting SAML tooopen yapılandırma penceresi'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="24441-161">On hello Citrix GoToMeeting SAML Configuration section, click Configure Citrix GoToMeeting SAML tooopen Configure sign-on window.</span></span> <span data-ttu-id="24441-162">Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="24441-162">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

6. <span data-ttu-id="24441-163">Farklı bir tarayıcı penceresinde tooyour içinde oturum [Citrix kuruluş Merkezi](https://account.citrixonline.com/organization/administration/).</span><span class="sxs-lookup"><span data-stu-id="24441-163">In a different browser window, log in tooyour [Citrix Organization Center](https://account.citrixonline.com/organization/administration/).</span></span>

7. <span data-ttu-id="24441-164">Merhaba tıklatın **kimlik sağlayıcısı** sekmesini tıklatın ve ardından hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="24441-164">Click hello **Identity Provider** tab, and then perform hello following steps:</span></span>  
   
    <span data-ttu-id="24441-165">![SAML Kurulumu](./media/active-directory-saas-citrix-gotomeeting-tutorial/IC6892321.png "SAML Kurulumu")</span><span class="sxs-lookup"><span data-stu-id="24441-165">![SAML setup](./media/active-directory-saas-citrix-gotomeeting-tutorial/IC6892321.png "SAML setup")</span></span>
   
    <span data-ttu-id="24441-166">a.</span><span class="sxs-lookup"><span data-stu-id="24441-166">a.</span></span> <span data-ttu-id="24441-167">Seçin **el ile**</span><span class="sxs-lookup"><span data-stu-id="24441-167">Select **Manual**</span></span>

    <span data-ttu-id="24441-168">b.</span><span class="sxs-lookup"><span data-stu-id="24441-168">b.</span></span> <span data-ttu-id="24441-169">Merhaba hello üzerinde Azure portal'ın **çoklu oturum açma sırasında Citrix GoToMeeting yapılandırma** iletişim sayfası, kopyalama hello **SAML çoklu oturum açma hizmet URL'si** değer ve hello yapıştırma **oturum açma sayfası URL** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="24441-169">In hello Azure portal, on hello **Configure single sign-on at Citrix GoToMeeting** dialog page, copy hello **SAML Single Sign-On Service URL** value, and then paste it into hello **Sign-in page URL** textbox.</span></span> 

    <span data-ttu-id="24441-170">c.</span><span class="sxs-lookup"><span data-stu-id="24441-170">c.</span></span> <span data-ttu-id="24441-171">Merhaba hello üzerinde Azure portal'ın **çoklu oturum açma sırasında Citrix GoToMeeting yapılandırma** iletişim sayfası, kopyalama hello **Sign-Out URL** değer ve hello yapıştırma **oturum kapatma sayfası URL'si**metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="24441-171">In hello Azure portal, on hello **Configure single sign-on at Citrix GoToMeeting** dialog page, copy hello **Sign-Out URL** value, and then paste it into hello **Sign-out page URL** textbox.</span></span>

    <span data-ttu-id="24441-172">d.</span><span class="sxs-lookup"><span data-stu-id="24441-172">d.</span></span> <span data-ttu-id="24441-173">Merhaba hello üzerinde Azure portal'ın **çoklu oturum açma sırasında Citrix GoToMeeting yapılandırma** iletişim sayfası, kopyalama hello **SAML varlık kimliği** değer ve hello yapıştırma **kimlik sağlayıcısı varlık kimliği**  metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="24441-173">In hello Azure portal, on hello **Configure single sign-on at Citrix GoToMeeting** dialog page, copy hello **SAML Entity ID** value, and then paste it into hello **Identity Provider Entity ID** textbox.</span></span>

    <span data-ttu-id="24441-174">e.</span><span class="sxs-lookup"><span data-stu-id="24441-174">e.</span></span> <span data-ttu-id="24441-175">tooupload indirilen sertifikanızı tıklatın **sertifikasını karşıya yükle**.</span><span class="sxs-lookup"><span data-stu-id="24441-175">tooupload your downloaded certificate, click **Upload Certificate**.</span></span>

    <span data-ttu-id="24441-176">f.</span><span class="sxs-lookup"><span data-stu-id="24441-176">f.</span></span> <span data-ttu-id="24441-177">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="24441-177">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="24441-178">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="24441-178">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="24441-179">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="24441-179">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="24441-180">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="24441-180">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="24441-181">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="24441-181">Creating an Azure AD test user</span></span>
<span data-ttu-id="24441-182">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="24441-182">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="24441-184">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="24441-184">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="24441-185">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="24441-185">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="24441-187">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="24441-187">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="24441-189">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="24441-189">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="24441-191">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="24441-191">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="24441-193">a.</span><span class="sxs-lookup"><span data-stu-id="24441-193">a.</span></span> <span data-ttu-id="24441-194">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="24441-194">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="24441-195">b.</span><span class="sxs-lookup"><span data-stu-id="24441-195">b.</span></span> <span data-ttu-id="24441-196">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="24441-196">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="24441-197">c.</span><span class="sxs-lookup"><span data-stu-id="24441-197">c.</span></span> <span data-ttu-id="24441-198">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="24441-198">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="24441-199">d.</span><span class="sxs-lookup"><span data-stu-id="24441-199">d.</span></span> <span data-ttu-id="24441-200">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="24441-200">Click **Create**.</span></span>
 
### <a name="creating-a-citrix-gotomeeting-test-user"></a><span data-ttu-id="24441-201">Citrix GoToMeeting test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="24441-201">Creating a Citrix GoToMeeting test user</span></span>

<span data-ttu-id="24441-202">Bu bölümde, bir kullanıcı Britta Simon olarak adlandırılır ve Citrix GoToMeeting oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="24441-202">In this section, a user called Britta Simon is created in Citrix GoToMeeting.</span></span> <span data-ttu-id="24441-203">Citrix GoToMeeting tam zamanı sağlama, varsayılan olarak etkin olduğu destekler.</span><span class="sxs-lookup"><span data-stu-id="24441-203">Citrix GoToMeeting supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="24441-204">Bu bölümde, eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="24441-204">There is no action item for you in this section.</span></span> <span data-ttu-id="24441-205">Bir kullanıcı zaten Citrix GoToMeeting yoksa, tooaccess Citrix GoToMeeting çalıştığında yeni bir tane oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="24441-205">If a user doesn't already exist in Citrix GoToMeeting, a new one is created when you attempt tooaccess Citrix GoToMeeting.</span></span>

>[!Note]
><span data-ttu-id="24441-206">El ile bir kullanıcıyla iletişim toocreate gerekiyorsa [Citrix GoToMeeting destek ekibi](https://care.citrixonline.com/gotomeeting)</span><span class="sxs-lookup"><span data-stu-id="24441-206">If you need toocreate a user manually, Contact [Citrix GoToMeeting support team](https://care.citrixonline.com/gotomeeting)</span></span> 


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="24441-207">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="24441-207">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="24441-208">Bu bölümde, erişim tooCitrix GoToMeeting vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="24441-208">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCitrix GoToMeeting.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="24441-210">**tooassign Britta Simon tooCitrix GoToMeeting, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="24441-210">**tooassign Britta Simon tooCitrix GoToMeeting, perform hello following steps:**</span></span>

1. <span data-ttu-id="24441-211">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="24441-211">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="24441-213">Merhaba uygulamalar listesinde **Citrix GoToMeeting**.</span><span class="sxs-lookup"><span data-stu-id="24441-213">In hello applications list, select **Citrix GoToMeeting**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_app.png) 

3. <span data-ttu-id="24441-215">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="24441-215">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="24441-217">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="24441-217">Click **Add** button.</span></span> <span data-ttu-id="24441-218">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="24441-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="24441-220">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="24441-220">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="24441-221">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="24441-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="24441-222">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="24441-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="24441-223">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="24441-223">Testing single sign-on</span></span>

<span data-ttu-id="24441-224">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="24441-224">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="24441-225">Çoklu oturum açma ayarlarınızı tootest istiyorsanız hello erişim paneli açın.</span><span class="sxs-lookup"><span data-stu-id="24441-225">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="24441-226">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="24441-226">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="24441-227">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="24441-227">Additional resources</span></span>

* [<span data-ttu-id="24441-228">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="24441-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="24441-229">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="24441-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="24441-230">Kullanıcı sağlamayı Yapılandır</span><span class="sxs-lookup"><span data-stu-id="24441-230">Configure User Provisioning</span></span>](active-directory-saas-citrixgotomeeting-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_203.png

