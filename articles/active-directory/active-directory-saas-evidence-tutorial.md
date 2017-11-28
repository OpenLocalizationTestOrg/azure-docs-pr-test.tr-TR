---
title: "Öğretici: Azure Active Directory Tümleştirme ile Evidence.com | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Evidence.com arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: f9a7cb7c-ff67-40dc-872c-1fa35f9dd03b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: eed98c15dca8a6a77f0b5d407bb40ee0037fccad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-evidencecom"></a><span data-ttu-id="6a3cb-103">Öğretici: Azure Active Directory Tümleştirme Evidence.com ile</span><span class="sxs-lookup"><span data-stu-id="6a3cb-103">Tutorial: Azure Active Directory integration with Evidence.com</span></span>

<span data-ttu-id="6a3cb-104">Bu öğreticide, bilgi nasıl toointegrate Evidence.com Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6a3cb-104">In this tutorial, you learn how toointegrate Evidence.com with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6a3cb-105">Evidence.com Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="6a3cb-105">Integrating Evidence.com with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6a3cb-106">Erişim tooEvidence.com sahip Azure AD'de kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-106">You can control in Azure AD who has access tooEvidence.com.</span></span>
- <span data-ttu-id="6a3cb-107">Kullanıcıların tooautomatically get açan tooEvidence.com (çoklu oturum açma) Azure AD hesaplarına ile etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-107">You can enable your users tooautomatically get signed-on tooEvidence.com (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="6a3cb-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="6a3cb-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6a3cb-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6a3cb-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="6a3cb-110">Prerequisites</span></span>

<span data-ttu-id="6a3cb-111">tooconfigure Evidence.com ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="6a3cb-111">tooconfigure Azure AD integration with Evidence.com, you need hello following items:</span></span>

- <span data-ttu-id="6a3cb-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="6a3cb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6a3cb-113">Bir Evidence.com çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="6a3cb-113">A Evidence.com single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6a3cb-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6a3cb-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="6a3cb-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6a3cb-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6a3cb-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6a3cb-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6a3cb-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="6a3cb-118">Scenario description</span></span>
<span data-ttu-id="6a3cb-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6a3cb-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="6a3cb-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6a3cb-121">Merhaba Galerisi'nden Evidence.com ekleme</span><span class="sxs-lookup"><span data-stu-id="6a3cb-121">Adding Evidence.com from hello gallery</span></span>
2. <span data-ttu-id="6a3cb-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="6a3cb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-evidencecom-from-hello-gallery"></a><span data-ttu-id="6a3cb-123">Merhaba Galerisi'nden Evidence.com ekleme</span><span class="sxs-lookup"><span data-stu-id="6a3cb-123">Adding Evidence.com from hello gallery</span></span>
<span data-ttu-id="6a3cb-124">Azure AD'ye tooconfigure hello tümleştirme Evidence.com, tooadd Evidence.com hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-124">tooconfigure hello integration of Evidence.com into Azure AD, you need tooadd Evidence.com from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6a3cb-125">**tooadd Evidence.com hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6a3cb-125">**tooadd Evidence.com from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6a3cb-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory düğmesi][1]

2. <span data-ttu-id="6a3cb-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6a3cb-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-129">Then go too**All applications**.</span></span>

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="6a3cb-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Merhaba yeni uygulama düğmesi][3]

4. <span data-ttu-id="6a3cb-133">Merhaba arama kutusuna yazın **Evidence.com**seçin **Evidence.com** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-133">In hello search box, type **Evidence.com**, select **Evidence.com** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Merhaba sonuçları listesinde Evidence.com](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="6a3cb-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="6a3cb-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="6a3cb-136">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Evidence.com sınayın.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-136">In this section, you configure and test Azure AD single sign-on with Evidence.com based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6a3cb-137">Tek toowork'ın oturum açma hangi hello karşılık gelen Evidence.com içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Evidence.com is tooa user in Azure AD.</span></span> <span data-ttu-id="6a3cb-138">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Evidence.com hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-138">In other words, a link relationship between an Azure AD user and hello related user in Evidence.com needs toobe established.</span></span>

<span data-ttu-id="6a3cb-139">Merhaba hello değeri Evidence.com içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-139">In Evidence.com, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="6a3cb-140">tooconfigure ve Evidence.com ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="6a3cb-140">tooconfigure and test Azure AD single sign-on with Evidence.com, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6a3cb-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6a3cb-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6a3cb-143">**[Evidence.com test kullanıcısı oluşturma](#create-a-evidencecom-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Evidence.com içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-143">**[Create a Evidence.com test user](#create-a-evidencecom-test-user)** - toohave a counterpart of Britta Simon in Evidence.com that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6a3cb-144">**[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6a3cb-145">**[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="6a3cb-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="6a3cb-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="6a3cb-147">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Evidence.com uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Evidence.com application.</span></span>

<span data-ttu-id="6a3cb-148">**tooconfigure Azure AD çoklu oturum açma ile Evidence.com, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6a3cb-148">**tooconfigure Azure AD single sign-on with Evidence.com, perform hello following steps:**</span></span>

1. <span data-ttu-id="6a3cb-149">Hello hello üzerinde Azure portal'ın **Evidence.com** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-149">In hello Azure portal, on hello **Evidence.com** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. <span data-ttu-id="6a3cb-151">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_samlbase.png)

3. <span data-ttu-id="6a3cb-153">Merhaba üzerinde **Evidence.com etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="6a3cb-153">On hello **Evidence.com Domain and URLs** section, perform hello following steps:</span></span>

    ![Evidence.com etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_url.png)

    <span data-ttu-id="6a3cb-155">a.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-155">a.</span></span> <span data-ttu-id="6a3cb-156">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<yourtenant>.evidence.com`</span><span class="sxs-lookup"><span data-stu-id="6a3cb-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<yourtenant>.evidence.com`</span></span>

    <span data-ttu-id="6a3cb-157">b.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-157">b.</span></span> <span data-ttu-id="6a3cb-158">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<yourtenant>.evidence.com`</span><span class="sxs-lookup"><span data-stu-id="6a3cb-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<yourtenant>.evidence.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6a3cb-159">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-159">These values are not real.</span></span> <span data-ttu-id="6a3cb-160">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="6a3cb-161">Kişi [Evidence.com istemci destek ekibi](https://communities.taser.com/support/SupportContactUs?typ=LE) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-161">Contact [Evidence.com Client support team](https://communities.taser.com/support/SupportContactUs?typ=LE) tooget these values.</span></span> 

4. <span data-ttu-id="6a3cb-162">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-162">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_certificate.png) 

5. <span data-ttu-id="6a3cb-164">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-164">Click **Save** button.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-evidence-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6a3cb-166">Merhaba üzerinde **Evidence.com yapılandırma** 'yi tıklatın **yapılandırma Evidence.com** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-166">On hello **Evidence.com Configuration** section, click **Configure Evidence.com** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="6a3cb-167">Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="6a3cb-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Evidence.com yapılandırma](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_configure.png) 

7. <span data-ttu-id="6a3cb-169">Oturum açma tooyour Evidence.com ayrı bir web tarayıcısı penceresinde, Kiracı yönetici olarak ve çok gidin**yönetici** sekmesi</span><span class="sxs-lookup"><span data-stu-id="6a3cb-169">In a separate web browser window, login tooyour Evidence.com tenant as an administrator and navigate too**Admin** Tab</span></span>

8. <span data-ttu-id="6a3cb-170">Tıklayın **Teşkilatı çoklu oturum açma**</span><span class="sxs-lookup"><span data-stu-id="6a3cb-170">Click on **Agency Single Sign On**</span></span>

9. <span data-ttu-id="6a3cb-171">Seçin **SAML temel çoklu oturum açma**</span><span class="sxs-lookup"><span data-stu-id="6a3cb-171">Select **SAML Based Single Sign On**</span></span>

10. <span data-ttu-id="6a3cb-172">Kopya hello **SAML varlık kimliği**, **SAML çoklu oturum açma hizmet URL'si** ve **Sign-Out URL** hello Azure portal ve Evidence.com karşılık gelen alanlara toohello gösterilen değerleri.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-172">Copy hello **SAML Entity ID**, **SAML Single Sign-On Service URL** and **Sign-Out URL** values shown in hello Azure portal and toohello corresponding fields in Evidence.com.</span></span>

11. <span data-ttu-id="6a3cb-173">İndirilen Certificate(Base64) dosyanızı kopyalama hello panonuza bunu içerik Not Defteri'nde açın ve toohello yapıştırın **güvenlik sertifikası** kutusu.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-173">Open your downloaded Certificate(Base64) file in notepad, copy hello content of it into your clipboard, and then paste it toohello **Security Certificate** box.</span></span> 

12. <span data-ttu-id="6a3cb-174">Merhaba yapılandırma Evidence.com kaydedin.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-174">Save hello configuration in Evidence.com.</span></span>

> [!TIP]
> <span data-ttu-id="6a3cb-175">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="6a3cb-175">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6a3cb-176">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-176">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6a3cb-177">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6a3cb-177">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="6a3cb-178">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6a3cb-178">Create an Azure AD test user</span></span>

<span data-ttu-id="6a3cb-179">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-179">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="6a3cb-181">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6a3cb-181">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6a3cb-182">Merhaba hello sol bölmede Azure portal hello tıklatın **Azure Active Directory** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-182">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-evidence-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="6a3cb-184">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-184">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-evidence-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="6a3cb-186">tooopen hello **kullanıcı** iletişim kutusu, tıklatın **Ekle** hello hello üstündeki **tüm kullanıcılar** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-186">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Merhaba Ekle düğmesi](./media/active-directory-saas-evidence-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="6a3cb-188">Merhaba, **kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="6a3cb-188">In hello **User** dialog box, perform hello following steps:</span></span>

    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-evidence-tutorial/create_aaduser_04.png)

    <span data-ttu-id="6a3cb-190">a.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-190">a.</span></span> <span data-ttu-id="6a3cb-191">Merhaba, **adı** kutusuna **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-191">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6a3cb-192">b.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-192">b.</span></span> <span data-ttu-id="6a3cb-193">Merhaba, **kullanıcı adı** kutusuna, kullanıcının Britta Simon hello e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-193">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="6a3cb-194">c.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-194">c.</span></span> <span data-ttu-id="6a3cb-195">Select hello **Göster parola** onay kutusunu işaretleyin ve ardından hello görüntülenen hello değerini aşağı yazma **parola** kutusu.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-195">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="6a3cb-196">d.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-196">d.</span></span> <span data-ttu-id="6a3cb-197">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-197">Click **Create**.</span></span>
 
### <a name="create-a-evidencecom-test-user"></a><span data-ttu-id="6a3cb-198">Evidence.com test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6a3cb-198">Create a Evidence.com test user</span></span>

<span data-ttu-id="6a3cb-199">Azure AD kullanıcıların toobe mümkün toosign için hello Evidence.com uygulama içinde erişim sağlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-199">For Azure AD users toobe able toosign in, they must be provisioned for access inside hello Evidence.com application.</span></span> <span data-ttu-id="6a3cb-200">Bu bölümde nasıl Evidence.com içinde toocreate Azure AD kullanıcı hesapları açıklanmaktadır</span><span class="sxs-lookup"><span data-stu-id="6a3cb-200">This section describes how toocreate Azure AD user accounts inside Evidence.com</span></span>

<span data-ttu-id="6a3cb-201">**tooprovision Evidence.com bir kullanıcı hesabı:**</span><span class="sxs-lookup"><span data-stu-id="6a3cb-201">**tooprovision a user account in Evidence.com:**</span></span>

1. <span data-ttu-id="6a3cb-202">Bir web tarayıcısı penceresinde Evidence.com şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-202">In a web browser window, log into your Evidence.com company site as an administrator.</span></span>

2. <span data-ttu-id="6a3cb-203">Çok gidin**yönetici** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-203">Navigate too**Admin** tab.</span></span>

3. <span data-ttu-id="6a3cb-204">Tıklayın **kullanıcı ekleme**.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-204">Click on **Add User**.</span></span>

4. <span data-ttu-id="6a3cb-205">Merhaba tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-205">Click hello **Add** button.</span></span>

5. <span data-ttu-id="6a3cb-206">Merhaba **e-posta adresi** kullanıcı toogive istediğiniz Azure AD içinde hello kullanıcılar hello kullanıcı adı eşleşmelidir hello eklenen erişim.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-206">hello **Email Address** of hello added user must match hello username of hello users in Azure AD who you wish toogive access.</span></span> <span data-ttu-id="6a3cb-207">Merhaba kullanıcı adı ve e-posta adresi değil Merhaba, aynı değeri, kuruluşunuzda hello kullanabilirsiniz **Evidence.com > öznitelikler > çoklu oturum açma** gönderilen hello Azure portal toochange hello nameidenitifer bölümü tooEvidence.com toobe hello e-posta adresi.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-207">If hello username and email address are not hello same value in your organization, you can use hello **Evidence.com > Attributes > Single Sign-On** section of hello Azure portal toochange hello nameidenitifer sent tooEvidence.com toobe hello email address.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="6a3cb-208">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="6a3cb-208">Assign hello Azure AD test user</span></span>

<span data-ttu-id="6a3cb-209">Bu bölümde, erişim tooEvidence.com vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-209">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooEvidence.com.</span></span>

![Merhaba kullanıcı rolü atayın][200] 

<span data-ttu-id="6a3cb-211">**tooassign Britta Simon tooEvidence.com hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6a3cb-211">**tooassign Britta Simon tooEvidence.com, perform hello following steps:**</span></span>

1. <span data-ttu-id="6a3cb-212">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-212">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="6a3cb-214">Merhaba uygulamalar listesinde **Evidence.com**.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-214">In hello applications list, select **Evidence.com**.</span></span>

    ![Merhaba Evidence.com bağlantı hello uygulamalar listesinde](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_app.png)  

3. <span data-ttu-id="6a3cb-216">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-216">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202]

4. <span data-ttu-id="6a3cb-218">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-218">Click **Add** button.</span></span> <span data-ttu-id="6a3cb-219">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Merhaba eklemek atama bölmesi][203]

5. <span data-ttu-id="6a3cb-221">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-221">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6a3cb-222">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6a3cb-223">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="6a3cb-224">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="6a3cb-224">Test single sign-on</span></span>

<span data-ttu-id="6a3cb-225">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="6a3cb-226">Merhaba Evidence.com hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Evidence.com uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6a3cb-226">When you click hello Evidence.com tile in hello Access Panel, you should get automatically signed-on tooyour Evidence.com application.</span></span>
<span data-ttu-id="6a3cb-227">Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6a3cb-227">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="6a3cb-228">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="6a3cb-228">Additional resources</span></span>

* [<span data-ttu-id="6a3cb-229">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="6a3cb-229">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6a3cb-230">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="6a3cb-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_203.png

