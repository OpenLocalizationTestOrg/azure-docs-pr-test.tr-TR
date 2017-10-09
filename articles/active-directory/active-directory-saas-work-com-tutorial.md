---
title: "Öğretici: Azure Active Directory Tümleştirme ile Work.com | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Work.com arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 98e6739e-eb24-46bd-9dd3-20b489839076
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: dcdc51c884abd78c945b649de99f942d32373cf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workcom"></a><span data-ttu-id="77ccf-103">Öğretici: Azure Active Directory Tümleştirme Work.com ile</span><span class="sxs-lookup"><span data-stu-id="77ccf-103">Tutorial: Azure Active Directory integration with Work.com</span></span>

<span data-ttu-id="77ccf-104">Bu öğreticide, bilgi nasıl toointegrate Work.com Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="77ccf-104">In this tutorial, you learn how toointegrate Work.com with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="77ccf-105">Work.com Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="77ccf-105">Integrating Work.com with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="77ccf-106">Erişim tooWork.com sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="77ccf-106">You can control in Azure AD who has access tooWork.com</span></span>
- <span data-ttu-id="77ccf-107">Kullanıcıların tooautomatically get açan tooWork.com (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="77ccf-107">You can enable your users tooautomatically get signed-on tooWork.com (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="77ccf-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="77ccf-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="77ccf-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="77ccf-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="77ccf-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="77ccf-110">Prerequisites</span></span>

<span data-ttu-id="77ccf-111">tooconfigure Work.com ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="77ccf-111">tooconfigure Azure AD integration with Work.com, you need hello following items:</span></span>

- <span data-ttu-id="77ccf-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="77ccf-112">An Azure AD subscription</span></span>
- <span data-ttu-id="77ccf-113">Bir Work.com çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="77ccf-113">A Work.com single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="77ccf-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="77ccf-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="77ccf-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="77ccf-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="77ccf-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="77ccf-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="77ccf-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="77ccf-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="77ccf-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="77ccf-118">Scenario description</span></span>
<span data-ttu-id="77ccf-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="77ccf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="77ccf-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="77ccf-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="77ccf-121">Merhaba Galerisi'nden Work.com ekleme</span><span class="sxs-lookup"><span data-stu-id="77ccf-121">Add Work.com from hello gallery</span></span>
2. <span data-ttu-id="77ccf-122">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="77ccf-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-workcom-from-hello-gallery"></a><span data-ttu-id="77ccf-123">Merhaba Galerisi'nden Work.com ekleme</span><span class="sxs-lookup"><span data-stu-id="77ccf-123">Add Work.com from hello gallery</span></span>
<span data-ttu-id="77ccf-124">Azure AD'ye tooconfigure hello tümleştirme Work.com, tooadd Work.com hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="77ccf-124">tooconfigure hello integration of Work.com into Azure AD, you need tooadd Work.com from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="77ccf-125">**tooadd Work.com hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="77ccf-125">**tooadd Work.com from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="77ccf-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="77ccf-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="77ccf-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="77ccf-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="77ccf-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="77ccf-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="77ccf-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="77ccf-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="77ccf-133">Merhaba arama kutusuna yazın **Work.com**seçin **Work.com** sonuçları panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="77ccf-133">In hello search box, type **Work.com**, select **Work.com** from results panel then click **Add** button tooadd hello application.</span></span>

    ![Galerisi'nden ekleme](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="77ccf-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="77ccf-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="77ccf-136">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Work.com sınayın.</span><span class="sxs-lookup"><span data-stu-id="77ccf-136">In this section, you configure and test Azure AD single sign-on with Work.com based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="77ccf-137">Tek toowork'ın oturum açma hangi hello karşılık gelen Work.com içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="77ccf-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Work.com is tooa user in Azure AD.</span></span> <span data-ttu-id="77ccf-138">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Work.com hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="77ccf-138">In other words, a link relationship between an Azure AD user and hello related user in Work.com needs toobe established.</span></span>

<span data-ttu-id="77ccf-139">Merhaba hello değeri Work.com içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="77ccf-139">In Work.com, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="77ccf-140">tooconfigure ve Work.com ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="77ccf-140">tooconfigure and test Azure AD single sign-on with Work.com, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="77ccf-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="77ccf-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="77ccf-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="77ccf-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="77ccf-143">**[Work.com test kullanıcısı oluşturma](#create-a-workcom-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Work.com içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="77ccf-143">**[Create a Work.com test user](#create-a-workcom-test-user)** - toohave a counterpart of Britta Simon in Work.com that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="77ccf-144">**[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="77ccf-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="77ccf-145">**[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="77ccf-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="77ccf-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="77ccf-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="77ccf-147">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Work.com uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="77ccf-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Work.com application.</span></span>

>[!NOTE]
><span data-ttu-id="77ccf-148">tooconfigure çoklu oturum açma, toosetup özel bir Work.com etki alanı adı henüz gerekir.</span><span class="sxs-lookup"><span data-stu-id="77ccf-148">tooconfigure single sign-on, you need toosetup a custom Work.com domain name yet.</span></span> <span data-ttu-id="77ccf-149">Toodefine en az bir etki alanına ihtiyacınız adı, etki alanı adınızı test ve kuruluşun tamamına tooyour dağıtın.</span><span class="sxs-lookup"><span data-stu-id="77ccf-149">You need toodefine at least a domain name, test your domain name, and deploy it tooyour entire organization.</span></span>

<span data-ttu-id="77ccf-150">**tooconfigure Azure AD çoklu oturum açma ile Work.com, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="77ccf-150">**tooconfigure Azure AD single sign-on with Work.com, perform hello following steps:**</span></span>

1. <span data-ttu-id="77ccf-151">Hello hello üzerinde Azure portal'ın **Work.com** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="77ccf-151">In hello Azure portal, on hello **Work.com** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="77ccf-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="77ccf-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![SAML tabanlı oturum açma](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_samlbase.png)

3. <span data-ttu-id="77ccf-155">Merhaba üzerinde **Work.com etki alanı ve URL'leri** bölümünde, hello aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="77ccf-155">On hello **Work.com Domain and URLs** section, perform hello following:</span></span>

    ![Work.com etki alanı ve URL'ler bölümü](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_url.png)

    <span data-ttu-id="77ccf-157">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`http://<companyname>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="77ccf-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `http://<companyname>.my.salesforce.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="77ccf-158">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="77ccf-158">This value is not real.</span></span> <span data-ttu-id="77ccf-159">Bu değer ile Merhaba güncelleştirme gerçek oturum açma URL'si.</span><span class="sxs-lookup"><span data-stu-id="77ccf-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="77ccf-160">Kişi [Work.com istemci destek ekibi](https://help.salesforce.com/articleView?id=000159855&type=3) tooget bu değer.</span><span class="sxs-lookup"><span data-stu-id="77ccf-160">Contact [Work.com Client support team](https://help.salesforce.com/articleView?id=000159855&type=3) tooget this value.</span></span> 

4. <span data-ttu-id="77ccf-161">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="77ccf-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![SAML imzalama sertifikası bölümü](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_certificate.png) 

5. <span data-ttu-id="77ccf-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="77ccf-163">Click **Save** button.</span></span>

    ![Kaydet Düğmesi](./media/active-directory-saas-work-com-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="77ccf-165">Merhaba üzerinde **Work.com yapılandırma** 'yi tıklatın **yapılandırma Work.com** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="77ccf-165">On hello **Work.com Configuration** section, click **Configure Work.com** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="77ccf-166">Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="77ccf-166">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Work.com yapılandırma bölümü](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_configure.png) 
7. <span data-ttu-id="77ccf-168">İçinde tooyour Work.com Kiracı yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="77ccf-168">Log in tooyour Work.com tenant as administrator.</span></span>

8. <span data-ttu-id="77ccf-169">Çok Git**Kurulum**.</span><span class="sxs-lookup"><span data-stu-id="77ccf-169">Go too**Setup**.</span></span>
   
    <span data-ttu-id="77ccf-170">![Kurulum](./media/active-directory-saas-work-com-tutorial/ic794108.png "Kurulumu")</span><span class="sxs-lookup"><span data-stu-id="77ccf-170">![Setup](./media/active-directory-saas-work-com-tutorial/ic794108.png "Setup")</span></span>

9. <span data-ttu-id="77ccf-171">Merhaba de hello sol gezinti bölmesindeki **Yönet** 'yi tıklatın **etki alanı yönetimi** tooexpand hello ilgili bölümü ve ardından **My etki alanı** tooopen hello  **Etki alanım** sayfası.</span><span class="sxs-lookup"><span data-stu-id="77ccf-171">On hello left navigation pane, in hello **Administer** section, click **Domain Management** tooexpand hello related section, and then click **My Domain** tooopen hello **My Domain** page.</span></span> 
   
    <span data-ttu-id="77ccf-172">![Etki alanım](./media/active-directory-saas-work-com-tutorial/ic767825.png "etki alanım")</span><span class="sxs-lookup"><span data-stu-id="77ccf-172">![My Domain](./media/active-directory-saas-work-com-tutorial/ic767825.png "My Domain")</span></span>

10. <span data-ttu-id="77ccf-173">etki alanınızın doğru olarak ayarlanmış tooverify alanında olduğundan emin olun "**4 adım dağıtılan tooUsers**" ve gözden geçirin, "**My etki alanı ayarları**".</span><span class="sxs-lookup"><span data-stu-id="77ccf-173">tooverify that your domain has been set up correctly, make sure that it is in “**Step 4 Deployed tooUsers**” and review your “**My Domain Settings**”.</span></span>
   
    <span data-ttu-id="77ccf-174">![Etki alanı dağıtıldı tooUser](./media/active-directory-saas-work-com-tutorial/ic784377.png "etki alanı dağıtılan tooUser")</span><span class="sxs-lookup"><span data-stu-id="77ccf-174">![Domain Deployed tooUser](./media/active-directory-saas-work-com-tutorial/ic784377.png "Domain Deployed tooUser")</span></span>

11. <span data-ttu-id="77ccf-175">İçinde tooyour Work.com Kiracı oturum açın.</span><span class="sxs-lookup"><span data-stu-id="77ccf-175">Log in tooyour Work.com tenant.</span></span>

12. <span data-ttu-id="77ccf-176">Çok Git**Kurulum**.</span><span class="sxs-lookup"><span data-stu-id="77ccf-176">Go too**Setup**.</span></span>
    
    <span data-ttu-id="77ccf-177">![Kurulum](./media/active-directory-saas-work-com-tutorial/ic794108.png "Kurulumu")</span><span class="sxs-lookup"><span data-stu-id="77ccf-177">![Setup](./media/active-directory-saas-work-com-tutorial/ic794108.png "Setup")</span></span>

13. <span data-ttu-id="77ccf-178">Merhaba genişletin **güvenlik denetimleri** menüsüne ve ardından **çoklu oturum açma ayarları**.</span><span class="sxs-lookup"><span data-stu-id="77ccf-178">Expand hello **Security Controls** menu, and then click **Single Sign-On Settings**.</span></span>
    
    <span data-ttu-id="77ccf-179">![Çoklu oturum açma ayarları](./media/active-directory-saas-work-com-tutorial/ic794113.png "tek oturum açma ayarları")</span><span class="sxs-lookup"><span data-stu-id="77ccf-179">![Single Sign-On Settings](./media/active-directory-saas-work-com-tutorial/ic794113.png "Single Sign-On Settings")</span></span>

14. <span data-ttu-id="77ccf-180">Merhaba üzerinde **çoklu oturum açma ayarları** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="77ccf-180">On hello **Single Sign-On Settings** dialog page, perform hello following steps:</span></span>
    
    <span data-ttu-id="77ccf-181">![SAML etkin](./media/active-directory-saas-work-com-tutorial/ic781026.png "SAML etkin")</span><span class="sxs-lookup"><span data-stu-id="77ccf-181">![SAML Enabled](./media/active-directory-saas-work-com-tutorial/ic781026.png "SAML Enabled")</span></span>
    
    <span data-ttu-id="77ccf-182">a.</span><span class="sxs-lookup"><span data-stu-id="77ccf-182">a.</span></span> <span data-ttu-id="77ccf-183">Seçin **SAML etkin**.</span><span class="sxs-lookup"><span data-stu-id="77ccf-183">Select **SAML Enabled**.</span></span>
    
    <span data-ttu-id="77ccf-184">b.</span><span class="sxs-lookup"><span data-stu-id="77ccf-184">b.</span></span> <span data-ttu-id="77ccf-185">**Yeni**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="77ccf-185">Click **New**.</span></span>

15. <span data-ttu-id="77ccf-186">Merhaba, **SAML çoklu oturum açma ayarları** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="77ccf-186">In hello **SAML Single Sign-On Settings** section, perform hello following steps:</span></span>
    
    <span data-ttu-id="77ccf-187">![Oturum açma SAML tek ayar](./media/active-directory-saas-work-com-tutorial/ic794114.png "oturum açma SAML tek ayar")</span><span class="sxs-lookup"><span data-stu-id="77ccf-187">![SAML Single Sign-On Setting](./media/active-directory-saas-work-com-tutorial/ic794114.png "SAML Single Sign-On Setting")</span></span>
    
    <span data-ttu-id="77ccf-188">a.</span><span class="sxs-lookup"><span data-stu-id="77ccf-188">a.</span></span> <span data-ttu-id="77ccf-189">Merhaba, **adı** metin kutusuna, yapılandırmanız için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="77ccf-189">In hello **Name** textbox, type a name for your configuration.</span></span>  
       
    > [!NOTE]
    > <span data-ttu-id="77ccf-190">İçin bir değer sağlama **adı** hello otomatik olarak doldurulması **API adı** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="77ccf-190">Providing a value for **Name** does automatically populate hello **API Name** textbox.</span></span>
    
    <span data-ttu-id="77ccf-191">b.</span><span class="sxs-lookup"><span data-stu-id="77ccf-191">b.</span></span> <span data-ttu-id="77ccf-192">İçinde **veren** metin kutusuna, Yapıştır hello değerini **SAML varlık kimliği** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="77ccf-192">In **Issuer** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="77ccf-193">c.</span><span class="sxs-lookup"><span data-stu-id="77ccf-193">c.</span></span> <span data-ttu-id="77ccf-194">Azure portalından tooupload indirilen hello sertifikayı tıklatın **Gözat**.</span><span class="sxs-lookup"><span data-stu-id="77ccf-194">tooupload hello downloaded certificate from Azure portal, click **Browse**.</span></span>
    
    <span data-ttu-id="77ccf-195">d.</span><span class="sxs-lookup"><span data-stu-id="77ccf-195">d.</span></span> <span data-ttu-id="77ccf-196">Merhaba, **varlık kimliği** metin kutusuna, türü `https://salesforce-work.com`.</span><span class="sxs-lookup"><span data-stu-id="77ccf-196">In hello **Entity Id** textbox, type `https://salesforce-work.com`.</span></span>
    
    <span data-ttu-id="77ccf-197">e.</span><span class="sxs-lookup"><span data-stu-id="77ccf-197">e.</span></span> <span data-ttu-id="77ccf-198">Olarak **SAML kimlik türü**seçin **onaylamayı içeren hello Federasyon kimliği hello kullanıcı nesnesinden**.</span><span class="sxs-lookup"><span data-stu-id="77ccf-198">As **SAML Identity Type**, select **Assertion contains hello Federation ID from hello User object**.</span></span>
    
    <span data-ttu-id="77ccf-199">f.</span><span class="sxs-lookup"><span data-stu-id="77ccf-199">f.</span></span> <span data-ttu-id="77ccf-200">Olarak **SAML kimlik konumu**seçin **kimliktir hello NameIdentfier öğesinde hello konu deyimi**.</span><span class="sxs-lookup"><span data-stu-id="77ccf-200">As **SAML Identity Location**, select **Identity is in hello NameIdentfier element of hello Subject statement**.</span></span>
    
    <span data-ttu-id="77ccf-201">g.</span><span class="sxs-lookup"><span data-stu-id="77ccf-201">g.</span></span> <span data-ttu-id="77ccf-202">İçinde **kimlik sağlayıcısı oturum açma URL'si** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="77ccf-202">In **Identity Provider Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="77ccf-203">h.</span><span class="sxs-lookup"><span data-stu-id="77ccf-203">h.</span></span> <span data-ttu-id="77ccf-204">İçinde **kimlik sağlayıcısı oturum kapatma URL'si** metin kutusuna, Yapıştır hello değerini **Sign-Out URL** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="77ccf-204">In **Identity Provider Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="77ccf-205">ı.</span><span class="sxs-lookup"><span data-stu-id="77ccf-205">i.</span></span> <span data-ttu-id="77ccf-206">Olarak **hizmet sağlayıcısı tarafından başlatılan bağlama isteği**seçin **HTTP Post**.</span><span class="sxs-lookup"><span data-stu-id="77ccf-206">As **Service Provider Initiated Request Binding**, select **HTTP Post**.</span></span>
    
    <span data-ttu-id="77ccf-207">j.</span><span class="sxs-lookup"><span data-stu-id="77ccf-207">j.</span></span> <span data-ttu-id="77ccf-208">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="77ccf-208">Click **Save**.</span></span>

16. <span data-ttu-id="77ccf-209">Merhaba sol gezinti bölmesinde, Work.com Klasik Portalı'nda tıklatın **etki alanı yönetimi** tooexpand hello ilgili bölümü ve ardından **My etki alanı** tooopen hello **My etki alanı**sayfası.</span><span class="sxs-lookup"><span data-stu-id="77ccf-209">In your Work.com classic portal, on hello left navigation pane, click **Domain Management** tooexpand hello related section, and then click **My Domain** tooopen hello **My Domain** page.</span></span> 
    
    <span data-ttu-id="77ccf-210">![Etki alanım](./media/active-directory-saas-work-com-tutorial/ic794115.png "etki alanım")</span><span class="sxs-lookup"><span data-stu-id="77ccf-210">![My Domain](./media/active-directory-saas-work-com-tutorial/ic794115.png "My Domain")</span></span>

17. <span data-ttu-id="77ccf-211">Merhaba üzerinde **My etki alanı** sayfasında hello **oturum açma sayfası markalama** 'yi tıklatın **Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="77ccf-211">On hello **My Domain** page, in hello **Login Page Branding** section, click **Edit**.</span></span>
    
    <span data-ttu-id="77ccf-212">![Oturum açma sayfası markalama](./media/active-directory-saas-work-com-tutorial/ic767826.png "oturum açma sayfası markalama")</span><span class="sxs-lookup"><span data-stu-id="77ccf-212">![Login Page Branding](./media/active-directory-saas-work-com-tutorial/ic767826.png "Login Page Branding")</span></span>

14. <span data-ttu-id="77ccf-213">Merhaba üzerinde **oturum açma sayfası markalama** sayfasında hello **kimlik doğrulama hizmeti** bölümü, hello adını, **SAML SSO ayarları** görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="77ccf-213">On hello **Login Page Branding** page, in hello **Authentication Service** section, hello name of your **SAML SSO Settings** is displayed.</span></span> <span data-ttu-id="77ccf-214">Seçin ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="77ccf-214">Select it, and then click **Save**.</span></span>
    
    <span data-ttu-id="77ccf-215">![Oturum açma sayfası markalama](./media/active-directory-saas-work-com-tutorial/ic784366.png "oturum açma sayfası markalama")</span><span class="sxs-lookup"><span data-stu-id="77ccf-215">![Login Page Branding](./media/active-directory-saas-work-com-tutorial/ic784366.png "Login Page Branding")</span></span>

> [!TIP]
> <span data-ttu-id="77ccf-216">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="77ccf-216">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="77ccf-217">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="77ccf-217">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="77ccf-218">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="77ccf-218">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="77ccf-219">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="77ccf-219">Create an Azure AD test user</span></span>
<span data-ttu-id="77ccf-220">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="77ccf-220">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="77ccf-222">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="77ccf-222">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="77ccf-223">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="77ccf-223">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-work-com-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="77ccf-225">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="77ccf-225">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Kullanıcıların ve grupların tüm kullanıcılar ->](./media/active-directory-saas-work-com-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="77ccf-227">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="77ccf-227">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Ekle](./media/active-directory-saas-work-com-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="77ccf-229">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="77ccf-229">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Kullanıcı iletişim sayfası](./media/active-directory-saas-work-com-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="77ccf-231">a.</span><span class="sxs-lookup"><span data-stu-id="77ccf-231">a.</span></span> <span data-ttu-id="77ccf-232">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="77ccf-232">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="77ccf-233">b.</span><span class="sxs-lookup"><span data-stu-id="77ccf-233">b.</span></span> <span data-ttu-id="77ccf-234">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="77ccf-234">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="77ccf-235">c.</span><span class="sxs-lookup"><span data-stu-id="77ccf-235">c.</span></span> <span data-ttu-id="77ccf-236">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="77ccf-236">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="77ccf-237">d.</span><span class="sxs-lookup"><span data-stu-id="77ccf-237">d.</span></span> <span data-ttu-id="77ccf-238">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="77ccf-238">Click **Create**.</span></span>
 
### <a name="create-a-workcom-test-user"></a><span data-ttu-id="77ccf-239">Work.com test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="77ccf-239">Create a Work.com test user</span></span>
<span data-ttu-id="77ccf-240">Azure Active Directory Kullanıcıları toobe mümkün toosign için bunların sağlanan tooWork.com olması gerekir. Work.com Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="77ccf-240">For Azure Active Directory users toobe able toosign in, they must be provisioned tooWork.com. In hello case of Work.com, provisioning is a manual task.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="77ccf-241">tooconfigure kullanıcı hazırlama, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="77ccf-241">tooconfigure user provisioning, perform hello following steps:</span></span>
1. <span data-ttu-id="77ccf-242">Üzerinde tooyour Work.com şirket site yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="77ccf-242">Sign on tooyour Work.com company site as an administrator.</span></span>

2. <span data-ttu-id="77ccf-243">Çok Git**Kurulum**.</span><span class="sxs-lookup"><span data-stu-id="77ccf-243">Go too**Setup**.</span></span>
   
    <span data-ttu-id="77ccf-244">![Kurulum](./media/active-directory-saas-work-com-tutorial/IC794108.png "Kurulumu")</span><span class="sxs-lookup"><span data-stu-id="77ccf-244">![Setup](./media/active-directory-saas-work-com-tutorial/IC794108.png "Setup")</span></span>
3. <span data-ttu-id="77ccf-245">Çok Git**kullanıcıları yönetme \> kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="77ccf-245">Go too**Manage Users \> Users**.</span></span>
   
    <span data-ttu-id="77ccf-246">![Kullanıcıları yönetme](./media/active-directory-saas-work-com-tutorial/IC784369.png "kullanıcıları yönetme")</span><span class="sxs-lookup"><span data-stu-id="77ccf-246">![Manage Users](./media/active-directory-saas-work-com-tutorial/IC784369.png "Manage Users")</span></span>

4. <span data-ttu-id="77ccf-247">Tıklatın **yeni kullanıcı**.</span><span class="sxs-lookup"><span data-stu-id="77ccf-247">Click **New User**.</span></span>
   
    <span data-ttu-id="77ccf-248">![Tüm kullanıcılar](./media/active-directory-saas-work-com-tutorial/IC794117.png "tüm kullanıcılar")</span><span class="sxs-lookup"><span data-stu-id="77ccf-248">![All Users](./media/active-directory-saas-work-com-tutorial/IC794117.png "All Users")</span></span>

5. <span data-ttu-id="77ccf-249">Geçerli bir Azure özniteliklerini içindeki adımları izleyerek hello Hello kullanıcı Düzenle bölümüne, gerçekleştirmek istediğiniz tooprovision hello AD hesabının ilgili metin kutularına:</span><span class="sxs-lookup"><span data-stu-id="77ccf-249">In hello User Edit section, perform hello following steps, in attributes of a valid Azure AD account you want tooprovision into hello related textboxes:</span></span>
   
    <span data-ttu-id="77ccf-250">![Kullanıcı düzenleme](./media/active-directory-saas-work-com-tutorial/ic794118.png "kullanıcı düzenleme")</span><span class="sxs-lookup"><span data-stu-id="77ccf-250">![User Edit](./media/active-directory-saas-work-com-tutorial/ic794118.png "User Edit")</span></span>
   
    <span data-ttu-id="77ccf-251">a.</span><span class="sxs-lookup"><span data-stu-id="77ccf-251">a.</span></span> <span data-ttu-id="77ccf-252">Merhaba, **ad** metin kutusuna, türü hello **ad** hello kullanıcının **Britta**.</span><span class="sxs-lookup"><span data-stu-id="77ccf-252">In hello **First Name** textbox, type hello **first name** of hello user **Britta**.</span></span>
    
    <span data-ttu-id="77ccf-253">b.</span><span class="sxs-lookup"><span data-stu-id="77ccf-253">b.</span></span> <span data-ttu-id="77ccf-254">Merhaba, **Soyadı** metin kutusuna, türü hello **Soyadı** hello kullanıcının **Simon**.</span><span class="sxs-lookup"><span data-stu-id="77ccf-254">In hello **Last Name** textbox, type hello **last name** of hello user **Simon**.</span></span>
    
    <span data-ttu-id="77ccf-255">c.</span><span class="sxs-lookup"><span data-stu-id="77ccf-255">c.</span></span> <span data-ttu-id="77ccf-256">Merhaba, **diğer** metin kutusuna, türü hello **adı** hello kullanıcının **BrittaS**.</span><span class="sxs-lookup"><span data-stu-id="77ccf-256">In hello **Alias** textbox, type hello **name** of hello user **BrittaS**.</span></span>
    
    <span data-ttu-id="77ccf-257">d.</span><span class="sxs-lookup"><span data-stu-id="77ccf-257">d.</span></span> <span data-ttu-id="77ccf-258">Merhaba, **e-posta** metin kutusuna, türü hello **e-posta adresi** kullanıcının  **Brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="77ccf-258">In hello **Email** textbox, type hello **email address** of user **Brittasimon@contoso.com**.</span></span>
    
    <span data-ttu-id="77ccf-259">e.</span><span class="sxs-lookup"><span data-stu-id="77ccf-259">e.</span></span> <span data-ttu-id="77ccf-260">Merhaba, **kullanıcı adı** metin kutusuna, türü kullanıcının kullanıcı adını ister  **Brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="77ccf-260">In hello **User Name** textbox, type a user name of user like **Brittasimon@contoso.com**.</span></span>
    
    <span data-ttu-id="77ccf-261">f.</span><span class="sxs-lookup"><span data-stu-id="77ccf-261">f.</span></span> <span data-ttu-id="77ccf-262">Merhaba, **takma ad** metin kutusuna, bir **takma ad** kullanıcının **Simon**.</span><span class="sxs-lookup"><span data-stu-id="77ccf-262">In hello **Nick Name** textbox, type a **nick name** of user **Simon**.</span></span>
    
    <span data-ttu-id="77ccf-263">g.</span><span class="sxs-lookup"><span data-stu-id="77ccf-263">g.</span></span> <span data-ttu-id="77ccf-264">Seçin **rol**, **kullanıcı lisansı**, ve **profil**.</span><span class="sxs-lookup"><span data-stu-id="77ccf-264">Select **Role**, **User License**, and **Profile**.</span></span>
    
    <span data-ttu-id="77ccf-265">h.</span><span class="sxs-lookup"><span data-stu-id="77ccf-265">h.</span></span> <span data-ttu-id="77ccf-266">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="77ccf-266">Click **Save**.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="77ccf-267">Hello Azure AD hesap sahibi etkin hale önce bir bağlantı tooconfirm hello hesabı da dahil olmak üzere bir e-posta alırsınız.</span><span class="sxs-lookup"><span data-stu-id="77ccf-267">hello Azure AD account holder will get an email including a link tooconfirm hello account before it becomes active.</span></span>
    > 
    > 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="77ccf-268">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="77ccf-268">Assign hello Azure AD test user</span></span>

<span data-ttu-id="77ccf-269">Bu bölümde, erişim tooWork.com vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="77ccf-269">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWork.com.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="77ccf-271">**tooassign Britta Simon tooWork.com hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="77ccf-271">**tooassign Britta Simon tooWork.com, perform hello following steps:**</span></span>

1. <span data-ttu-id="77ccf-272">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="77ccf-272">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="77ccf-274">Merhaba uygulamalar listesinde **Work.com**.</span><span class="sxs-lookup"><span data-stu-id="77ccf-274">In hello applications list, select **Work.com**.</span></span>

    ![Uygulamanın listesinde Work.com](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_app.png) 

3. <span data-ttu-id="77ccf-276">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="77ccf-276">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="77ccf-278">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="77ccf-278">Click **Add** button.</span></span> <span data-ttu-id="77ccf-279">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="77ccf-279">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="77ccf-281">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="77ccf-281">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="77ccf-282">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="77ccf-282">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="77ccf-283">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="77ccf-283">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="77ccf-284">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="77ccf-284">Test single sign-on</span></span>

<span data-ttu-id="77ccf-285">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="77ccf-285">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="77ccf-286">Merhaba Work.com hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Work.com uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="77ccf-286">When you click hello Work.com tile in hello Access Panel, you should get automatically signed-on tooyour Work.com application.</span></span>
<span data-ttu-id="77ccf-287">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="77ccf-287">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="77ccf-288">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="77ccf-288">Additional resources</span></span>

* [<span data-ttu-id="77ccf-289">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="77ccf-289">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="77ccf-290">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="77ccf-290">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_203.png

