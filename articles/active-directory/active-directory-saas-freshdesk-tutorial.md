---
title: "Öğretici: Azure Active Directory Tümleştirme ile FreshDesk | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile FreshDesk arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2a3e5aa-7b5a-4fe4-9285-45dbe6e8efcc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 577a5eb6d9b1bc03030a2b47f63d375869c903bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshdesk"></a><span data-ttu-id="e5db6-103">Öğretici: Azure Active Directory Tümleştirme FreshDesk ile</span><span class="sxs-lookup"><span data-stu-id="e5db6-103">Tutorial: Azure Active Directory integration with FreshDesk</span></span>

<span data-ttu-id="e5db6-104">Bu öğreticide, bilgi nasıl toointegrate FreshDesk Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e5db6-104">In this tutorial, you learn how toointegrate FreshDesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e5db6-105">FreshDesk Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="e5db6-105">Integrating FreshDesk with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e5db6-106">Erişim tooFreshDesk sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="e5db6-106">You can control in Azure AD who has access tooFreshDesk</span></span>
- <span data-ttu-id="e5db6-107">Kullanıcıların tooautomatically get açan tooFreshDesk (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="e5db6-107">You can enable your users tooautomatically get signed-on tooFreshDesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e5db6-108">Bir merkezi konumda - hello Azure Yönetim Portalı hesaplarınızı yönetebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="e5db6-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="e5db6-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e5db6-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e5db6-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e5db6-110">Prerequisites</span></span>

<span data-ttu-id="e5db6-111">tooconfigure FreshDesk ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="e5db6-111">tooconfigure Azure AD integration with FreshDesk, you need hello following items:</span></span>

- <span data-ttu-id="e5db6-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="e5db6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e5db6-113">Bir FreshDesk çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="e5db6-113">A FreshDesk single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e5db6-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="e5db6-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e5db6-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="e5db6-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e5db6-116">Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e5db6-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="e5db6-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e5db6-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e5db6-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="e5db6-118">Scenario description</span></span>
<span data-ttu-id="e5db6-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="e5db6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e5db6-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="e5db6-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e5db6-121">Merhaba Galerisi'nden FreshDesk ekleme</span><span class="sxs-lookup"><span data-stu-id="e5db6-121">Adding FreshDesk from hello gallery</span></span>
2. <span data-ttu-id="e5db6-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="e5db6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-freshdesk-from-hello-gallery"></a><span data-ttu-id="e5db6-123">Merhaba Galerisi'nden FreshDesk ekleme</span><span class="sxs-lookup"><span data-stu-id="e5db6-123">Adding FreshDesk from hello gallery</span></span>
<span data-ttu-id="e5db6-124">Azure AD'ye tooconfigure hello tümleştirme FreshDesk, tooadd FreshDesk hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="e5db6-124">tooconfigure hello integration of FreshDesk into Azure AD, you need tooadd FreshDesk from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e5db6-125">**tooadd FreshDesk hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e5db6-125">**tooadd FreshDesk from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e5db6-126">Merhaba,  **[Azure Yönetim Portalı](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="e5db6-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e5db6-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="e5db6-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e5db6-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="e5db6-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="e5db6-131">Tıklatın **Ekle** hello iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e5db6-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="e5db6-133">Merhaba arama kutusuna yazın **FreshDesk**.</span><span class="sxs-lookup"><span data-stu-id="e5db6-133">In hello search box, type **FreshDesk**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_search.png)

5. <span data-ttu-id="e5db6-135">Merhaba Sonuçlar panelinde seçin **FreshDesk**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="e5db6-135">In hello results panel, select **FreshDesk**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e5db6-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="e5db6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e5db6-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı FreshDesk sınayın.</span><span class="sxs-lookup"><span data-stu-id="e5db6-138">In this section, you configure and test Azure AD single sign-on with FreshDesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e5db6-139">Tek toowork'ın oturum açma hangi hello karşılık gelen FreshDesk içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="e5db6-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in FreshDesk is tooa user in Azure AD.</span></span> <span data-ttu-id="e5db6-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı FreshDesk hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="e5db6-140">In other words, a link relationship between an Azure AD user and hello related user in FreshDesk needs toobe established.</span></span>

<span data-ttu-id="e5db6-141">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** FreshDesk içinde.</span><span class="sxs-lookup"><span data-stu-id="e5db6-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in FreshDesk.</span></span>

<span data-ttu-id="e5db6-142">tooconfigure ve FreshDesk ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="e5db6-142">tooconfigure and test Azure AD single sign-on with FreshDesk, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e5db6-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="e5db6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e5db6-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="e5db6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e5db6-145">**[FreshDesk test kullanıcısı oluşturma](#creating-a-freshdesk-test-user)**  -toohave karşılık gelen her bağlantılı toohello Azure AD gösterimidir FreshDesk içinde Britta Simon biri.</span><span class="sxs-lookup"><span data-stu-id="e5db6-145">**[Creating a FreshDesk test user](#creating-a-freshdesk-test-user)** - toohave a counterpart of Britta Simon in FreshDesk that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="e5db6-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="e5db6-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e5db6-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="e5db6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e5db6-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e5db6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e5db6-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure Yönetim Portalı'nda etkinleştirin ve çoklu oturum açma FreshDesk uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="e5db6-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your FreshDesk application.</span></span>

<span data-ttu-id="e5db6-150">**tooconfigure Azure AD çoklu oturum açma ile FreshDesk, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e5db6-150">**tooconfigure Azure AD single sign-on with FreshDesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="e5db6-151">Merhaba üzerinde hello Azure Yönetim Portalı'nda **FreshDesk** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="e5db6-151">In hello Azure Management portal, on hello **FreshDesk** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="e5db6-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda, olarak **modu** seçin **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="e5db6-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_samlbase.png)

3. <span data-ttu-id="e5db6-155">Merhaba üzerinde **FreshDesk etki alanı ve URL'leri** bölümünde, lütfen hello girin **oturum açma URL'si** olarak: `https://<tenant-name>.freshdesk.com` veya başka bir değer Freshdesk önerdiği.</span><span class="sxs-lookup"><span data-stu-id="e5db6-155">On hello **FreshDesk Domain and URLs** section, please enter hello **Sign-on URL** as: `https://<tenant-name>.freshdesk.com` or any other value Freshdesk has suggested.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_url.png)

    > [!NOTE] 
    > <span data-ttu-id="e5db6-157">Lütfen bu gerçek değer olmadığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="e5db6-157">Please note that this is not the real value.</span></span> <span data-ttu-id="e5db6-158">Değerin gerçek oturum açma URL'si ile güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e5db6-158">You have to update the value with the actual Sign-on URL.</span></span> <span data-ttu-id="e5db6-159">Kişi [FreshDesk istemci destek ekibi](https://freshdesk.com/helpdesk-software?utm_source=Google-AdWords&utm_medium=Search-IND-Brand&utm_campaign=Search-IND-Brand&utm_term=freshdesk&device=c&gclid=COSH2_LH7NICFVUDvAodBPgBZg) bu değeri alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="e5db6-159">Contact [FreshDesk Client support team](https://freshdesk.com/helpdesk-software?utm_source=Google-AdWords&utm_medium=Search-IND-Brand&utm_campaign=Search-IND-Brand&utm_term=freshdesk&device=c&gclid=COSH2_LH7NICFVUDvAodBPgBZg) to get this value.</span></span>  

4. <span data-ttu-id="e5db6-160">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika** ve hello sertifika bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e5db6-160">On hello **SAML Signing Certificate** section, click **Certificate** and then save hello certificate on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_certificate.png) 

5. <span data-ttu-id="e5db6-162">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e5db6-162">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-freshdesk-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e5db6-164">Merhaba üzerinde **FreshDesk yapılandırma** 'yi tıklatın **yapılandırma FreshDesk** tooopen yapılandırma oturum açma penceresi.</span><span class="sxs-lookup"><span data-stu-id="e5db6-164">On hello **FreshDesk Configuration** section, click **Configure FreshDesk** tooopen Configure sign-on window.</span></span> <span data-ttu-id="e5db6-165">Hello hello SAML çoklu oturum açma hizmet URL'si ve Sign-Out URL'sini kopyalayın **hızlı başvuru** bölümü.</span><span class="sxs-lookup"><span data-stu-id="e5db6-165">Copy hello SAML Single Sign-On Service URL and Sign-Out URL from hello **Quick Reference** section.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_configure.png)

7. <span data-ttu-id="e5db6-167">Farklı web tarayıcısı penceresinde Freshdesk şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="e5db6-167">In a different web browser window, log into your Freshdesk company site as an administrator.</span></span>

8. <span data-ttu-id="e5db6-168">Hello içinde hello üst menüsünde **yönetici**.</span><span class="sxs-lookup"><span data-stu-id="e5db6-168">In hello menu on hello top, click **Admin**.</span></span>
   
   <span data-ttu-id="e5db6-169">![Yönetici](./media/active-directory-saas-freshdesk-tutorial/IC776768.png "yönetici")</span><span class="sxs-lookup"><span data-stu-id="e5db6-169">![Admin](./media/active-directory-saas-freshdesk-tutorial/IC776768.png "Admin")</span></span>

9. <span data-ttu-id="e5db6-170">Merhaba, **genel ayarları** sekmesini tıklatın, **güvenlik**.</span><span class="sxs-lookup"><span data-stu-id="e5db6-170">In hello **General Settings** tab, click **Security**.</span></span>
   
   <span data-ttu-id="e5db6-171">![Güvenlik](./media/active-directory-saas-freshdesk-tutorial/IC776769.png "güvenlik")</span><span class="sxs-lookup"><span data-stu-id="e5db6-171">![Security](./media/active-directory-saas-freshdesk-tutorial/IC776769.png "Security")</span></span>

10. <span data-ttu-id="e5db6-172">Merhaba, **güvenlik** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e5db6-172">In hello **Security** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="e5db6-173">![Çoklu oturum açmayı](./media/active-directory-saas-freshdesk-tutorial/IC776770.png "çoklu oturum açmayı")</span><span class="sxs-lookup"><span data-stu-id="e5db6-173">![Single Sign On](./media/active-directory-saas-freshdesk-tutorial/IC776770.png "Single Sign On")</span></span>
   
    <span data-ttu-id="e5db6-174">a.</span><span class="sxs-lookup"><span data-stu-id="e5db6-174">a.</span></span> <span data-ttu-id="e5db6-175">İçin **çoklu oturum açma (SSO)**seçin **üzerinde**.</span><span class="sxs-lookup"><span data-stu-id="e5db6-175">For **Single Sign On (SSO)**, select **On**.</span></span>

    <span data-ttu-id="e5db6-176">b.</span><span class="sxs-lookup"><span data-stu-id="e5db6-176">b.</span></span> <span data-ttu-id="e5db6-177">Seçin **SAML SSO**.</span><span class="sxs-lookup"><span data-stu-id="e5db6-177">Select **SAML SSO**.</span></span>

    <span data-ttu-id="e5db6-178">c.</span><span class="sxs-lookup"><span data-stu-id="e5db6-178">c.</span></span> <span data-ttu-id="e5db6-179">Türü hello **SAML çoklu oturum açma hizmet URL'si** hello Azure portalından kopyalandığından **SAML oturum açma URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="e5db6-179">Type hello **SAML Single Sign-On Service URL** you copied from Azure portal into hello **SAML Login URL** textbox.</span></span>

    <span data-ttu-id="e5db6-180">d.</span><span class="sxs-lookup"><span data-stu-id="e5db6-180">d.</span></span> <span data-ttu-id="e5db6-181">Türü hello **Sign-Out URL** hello Azure portalından kopyalandığından **oturum kapatma URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="e5db6-181">Type hello **Sign-Out URL**  you copied from Azure portal into hello **Logout URL** textbox.</span></span>

    <span data-ttu-id="e5db6-182">e.</span><span class="sxs-lookup"><span data-stu-id="e5db6-182">e.</span></span> <span data-ttu-id="e5db6-183">Kopya hello **parmak izi** değer Azure Portalı'ndan indirilen hello sertifikasından ve hello yapıştırma **güvenlik sertifika parmak izi** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="e5db6-183">Copy hello **Thumbprint** value from hello downloaded certificate from Azure portal and paste it into hello **Security Certificate Fingerprint** textbox.</span></span>  
 
    >[!TIP]
    ><span data-ttu-id="e5db6-184">Daha fazla ayrıntı için bkz: [nasıl tooretrieve bir sertifikanın parmak izi değeri](http://youtu.be/YKQF266SAxI).</span><span class="sxs-lookup"><span data-stu-id="e5db6-184">For more details, see [How tooretrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span> 
    
    <span data-ttu-id="e5db6-185">f.</span><span class="sxs-lookup"><span data-stu-id="e5db6-185">f.</span></span> <span data-ttu-id="e5db6-186">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e5db6-186">Click **Save**.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e5db6-187">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e5db6-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="e5db6-188">Bu bölümde Hello amacı toocreate Britta Simon adlı hello Azure Yönetim Portalı'nda bir sınama kullanıcısı ' dir.</span><span class="sxs-lookup"><span data-stu-id="e5db6-188">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="e5db6-190">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e5db6-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e5db6-191">Merhaba, **Azure Yönetim Portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="e5db6-191">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e5db6-193">Çok Git**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar** toodisplay hello kullanıcılar listesi.</span><span class="sxs-lookup"><span data-stu-id="e5db6-193">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e5db6-195">Merhaba hello iletişim üstündeki **Ekle** tooopen hello **kullanıcı** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e5db6-195">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e5db6-197">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e5db6-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e5db6-199">a.</span><span class="sxs-lookup"><span data-stu-id="e5db6-199">a.</span></span> <span data-ttu-id="e5db6-200">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e5db6-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e5db6-201">b.</span><span class="sxs-lookup"><span data-stu-id="e5db6-201">b.</span></span> <span data-ttu-id="e5db6-202">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="e5db6-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e5db6-203">c.</span><span class="sxs-lookup"><span data-stu-id="e5db6-203">c.</span></span> <span data-ttu-id="e5db6-204">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="e5db6-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e5db6-205">d.</span><span class="sxs-lookup"><span data-stu-id="e5db6-205">d.</span></span> <span data-ttu-id="e5db6-206">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e5db6-206">Click **Create**.</span></span>
 
### <a name="creating-a-freshdesk-test-user"></a><span data-ttu-id="e5db6-207">FreshDesk test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e5db6-207">Creating a FreshDesk test user</span></span>

<span data-ttu-id="e5db6-208">FreshDesk içine sipariş tooenable Azure AD kullanıcıların toolog bunların FreshDesk sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e5db6-208">In order tooenable Azure AD users toolog into FreshDesk, they must be provisioned into FreshDesk.</span></span>  
<span data-ttu-id="e5db6-209">FreshDesk Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="e5db6-209">In hello case of FreshDesk, provisioning is a manual task.</span></span>

<span data-ttu-id="e5db6-210">**bir kullanıcı hesapları tooprovision gerçekleştirmek hello adımları izleyin:**</span><span class="sxs-lookup"><span data-stu-id="e5db6-210">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="e5db6-211">İçinde tooyour oturum **Freshdesk** Kiracı.</span><span class="sxs-lookup"><span data-stu-id="e5db6-211">Log in tooyour **Freshdesk** tenant.</span></span>
2. <span data-ttu-id="e5db6-212">Hello içinde hello üst menüsünde **yönetici**.</span><span class="sxs-lookup"><span data-stu-id="e5db6-212">In hello menu on hello top, click **Admin**.</span></span>
   
   <span data-ttu-id="e5db6-213">![Yönetici](./media/active-directory-saas-freshdesk-tutorial/IC776772.png "yönetici")</span><span class="sxs-lookup"><span data-stu-id="e5db6-213">![Admin](./media/active-directory-saas-freshdesk-tutorial/IC776772.png "Admin")</span></span>

3. <span data-ttu-id="e5db6-214">Merhaba, **genel ayarları** sekmesini tıklatın, **aracıları**.</span><span class="sxs-lookup"><span data-stu-id="e5db6-214">In hello **General Settings** tab, click **Agents**.</span></span>
   
   <span data-ttu-id="e5db6-215">![Aracıları](./media/active-directory-saas-freshdesk-tutorial/IC776773.png "aracıları")</span><span class="sxs-lookup"><span data-stu-id="e5db6-215">![Agents](./media/active-directory-saas-freshdesk-tutorial/IC776773.png "Agents")</span></span>

4. <span data-ttu-id="e5db6-216">Tıklatın **yeni aracı**.</span><span class="sxs-lookup"><span data-stu-id="e5db6-216">Click **New Agent**.</span></span>
   
    <span data-ttu-id="e5db6-217">![Yeni aracı](./media/active-directory-saas-freshdesk-tutorial/IC776774.png "yeni aracı")</span><span class="sxs-lookup"><span data-stu-id="e5db6-217">![New Agent](./media/active-directory-saas-freshdesk-tutorial/IC776774.png "New Agent")</span></span>

5. <span data-ttu-id="e5db6-218">Merhaba aracı bilgileri iletişim kutusunda hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e5db6-218">On hello Agent Information dialog, perform hello following steps:</span></span>
   
   <span data-ttu-id="e5db6-219">![Aracı bilgilerini](./media/active-directory-saas-freshdesk-tutorial/IC776775.png "aracısı bilgileri")</span><span class="sxs-lookup"><span data-stu-id="e5db6-219">![Agent Information](./media/active-directory-saas-freshdesk-tutorial/IC776775.png "Agent Information")</span></span>
   
   <span data-ttu-id="e5db6-220">a.</span><span class="sxs-lookup"><span data-stu-id="e5db6-220">a.</span></span> <span data-ttu-id="e5db6-221">Merhaba, **tam adı** metin kutusuna, tür hello tooprovision istediğiniz hello Azure AD hesabının adını.</span><span class="sxs-lookup"><span data-stu-id="e5db6-221">In hello **Full Name** textbox, type hello name of hello Azure AD account you want tooprovision.</span></span>

   <span data-ttu-id="e5db6-222">b.</span><span class="sxs-lookup"><span data-stu-id="e5db6-222">b.</span></span> <span data-ttu-id="e5db6-223">Merhaba, **e-posta** metin kutusuna, türü hello Azure AD e-posta adresini istediğiniz hello Azure AD hesabının tooprovision.</span><span class="sxs-lookup"><span data-stu-id="e5db6-223">In hello **Email** textbox, type hello Azure AD email address of hello Azure AD account you want tooprovision.</span></span>

   <span data-ttu-id="e5db6-224">c.</span><span class="sxs-lookup"><span data-stu-id="e5db6-224">c.</span></span> <span data-ttu-id="e5db6-225">Merhaba, **başlık** metin kutusuna, tooprovision istediğiniz hello Azure AD hesabının türü hello başlığı.</span><span class="sxs-lookup"><span data-stu-id="e5db6-225">In hello **Title** textbox, type hello title of hello Azure AD account you want tooprovision.</span></span>

   <span data-ttu-id="e5db6-226">d.</span><span class="sxs-lookup"><span data-stu-id="e5db6-226">d.</span></span> <span data-ttu-id="e5db6-227">Seçin **aracıları rolü**ve ardından **atamak**.</span><span class="sxs-lookup"><span data-stu-id="e5db6-227">Select **Agents role**, and then click **Assign**.</span></span>
       
   <span data-ttu-id="e5db6-228">e.</span><span class="sxs-lookup"><span data-stu-id="e5db6-228">e.</span></span> <span data-ttu-id="e5db6-229">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e5db6-229">Click **Save**.</span></span>     
   
    >[!NOTE]
    ><span data-ttu-id="e5db6-230">Hello Azure AD hesap sahibi etkinleştirilmeden önce bir bağlantı tooconfirm hello hesabını içeren bir e-posta alırsınız.</span><span class="sxs-lookup"><span data-stu-id="e5db6-230">hello Azure AD account holder will get an email that includes a link tooconfirm hello account before it is activated.</span></span> 
    > 
    
    >[!NOTE]
    ><span data-ttu-id="e5db6-231">API AAD kullanıcı hesaplarının Freshdesk tooprovision tarafından sağlanan veya herhangi diğer Freshdesk kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e5db6-231">You can use any other Freshdesk user account creation tools or APIs provided by Freshdesk tooprovision AAD user accounts.</span></span> <span data-ttu-id="e5db6-232">tooFreshDesk.</span><span class="sxs-lookup"><span data-stu-id="e5db6-232">tooFreshDesk.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e5db6-233">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="e5db6-233">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e5db6-234">Bu bölümde, kendi erişim tooBox vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="e5db6-234">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooBox.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="e5db6-236">**tooassign Britta Simon tooFreshDesk hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e5db6-236">**tooassign Britta Simon tooFreshDesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="e5db6-237">Hello uygulamaları görünümü, Hello Azure Yönetim Portalı'nda açın ve ardından toohello dizin görünümüne gidin ve çok gidin**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="e5db6-237">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="e5db6-239">Merhaba uygulamalar listesinde **FreshDesk**.</span><span class="sxs-lookup"><span data-stu-id="e5db6-239">In hello applications list, select **FreshDesk**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_app.png) 

3. <span data-ttu-id="e5db6-241">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="e5db6-241">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="e5db6-243">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e5db6-243">Click **Add** button.</span></span> <span data-ttu-id="e5db6-244">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e5db6-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="e5db6-246">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="e5db6-246">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e5db6-247">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e5db6-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e5db6-248">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e5db6-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e5db6-249">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="e5db6-249">Testing single sign-on</span></span>

<span data-ttu-id="e5db6-250">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="e5db6-250">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="e5db6-251">Merhaba FreshDesk hello erişim paneli parçasında tıkladığınızda, oturum açma sayfası tooget açan tooyour FreshDesk uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e5db6-251">When you click hello FreshDesk tile in hello Access Panel, you should get login page tooget signed-on tooyour FreshDesk application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e5db6-252">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="e5db6-252">Additional resources</span></span>

* [<span data-ttu-id="e5db6-253">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="e5db6-253">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e5db6-254">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="e5db6-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_203.png

