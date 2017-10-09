---
title: "Öğretici: Azure Active Directory Tümleştirme ile Merces tarafından HR2day | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile HR2day Merces tarafından arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 853d08c9-27b1-48d4-b8e7-3705140eb67f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/24/2017
ms.author: jeedes
ms.openlocfilehash: 257233767e1fddbaf115878cb0455acf61b2f5f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hr2day-by-merces"></a><span data-ttu-id="a8b73-103">Öğretici: Azure Active Directory Tümleştirme Merces tarafından HR2day ile</span><span class="sxs-lookup"><span data-stu-id="a8b73-103">Tutorial: Azure Active Directory integration with HR2day by Merces</span></span>

<span data-ttu-id="a8b73-104">Bu öğreticide, bilgi nasıl toointegrate HR2day tarafından Azure Active Directory (Azure AD) ile Merces.</span><span class="sxs-lookup"><span data-stu-id="a8b73-104">In this tutorial, you learn how toointegrate HR2day by Merces with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a8b73-105">HR2day Merces tarafından Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="a8b73-105">Integrating HR2day by Merces with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a8b73-106">Merces tarafından erişim tooHR2day sahip Azure AD'de kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a8b73-106">You can control in Azure AD who has access tooHR2day by Merces.</span></span>
- <span data-ttu-id="a8b73-107">Kullanıcılarınızın tooautomatically imzalı tooHR2day içinde Merces tarafından kendi Azure AD hesapları ile etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a8b73-107">You can enable your users tooautomatically get signed in tooHR2day by Merces with their Azure AD accounts.</span></span>
- <span data-ttu-id="a8b73-108">Hesaplarınızı bir merkezi konumda--hello Azure portalında yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="a8b73-108">You can manage your accounts in one central location--hello Azure portal.</span></span>

<span data-ttu-id="a8b73-109">Azure AD SaaS uygulama tümleştirmesi hakkında daha fazla bilgi için bkz: [uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a8b73-109">For more information about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a8b73-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="a8b73-110">Prerequisites</span></span>

<span data-ttu-id="a8b73-111">tooconfigure HR2day Merces tarafından ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="a8b73-111">tooconfigure Azure AD integration with HR2day by Merces, you need hello following items:</span></span>

- <span data-ttu-id="a8b73-112">Bir Azure AD abonelik.</span><span class="sxs-lookup"><span data-stu-id="a8b73-112">An Azure AD subscription.</span></span>
- <span data-ttu-id="a8b73-113">Bir HR2day Merces çoklu oturum açma tarafından abonelik etkin.</span><span class="sxs-lookup"><span data-stu-id="a8b73-113">An HR2day by Merces single sign-on enabled subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="a8b73-114">Bir üretim ortamında tootest hello kullanarak bu öğreticideki adımlar öneririz yok.</span><span class="sxs-lookup"><span data-stu-id="a8b73-114">We don't recommend using a production environment tootest hello steps in this tutorial.</span></span>

<span data-ttu-id="a8b73-115">Bu öğreticide tootest hello adımları bu önerileri izleyin:</span><span class="sxs-lookup"><span data-stu-id="a8b73-115">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="a8b73-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="a8b73-116">Don't use your production environment unless it's necessary.</span></span>
- <span data-ttu-id="a8b73-117">Alma bir [bir aylık ücretsiz deneme Azure ad](https://azure.microsoft.com/pricing/free-trial/) , zaten yoksa.</span><span class="sxs-lookup"><span data-stu-id="a8b73-117">Get a [one-month free trial of Azure AD](https://azure.microsoft.com/pricing/free-trial/) if you don't already have it.</span></span>  

## <a name="scenario-description"></a><span data-ttu-id="a8b73-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="a8b73-118">Scenario description</span></span>
<span data-ttu-id="a8b73-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="a8b73-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a8b73-120">Burada özetlenen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="a8b73-120">hello scenario that's outlined here consists of two main building blocks:</span></span>

1. <span data-ttu-id="a8b73-121">HR2day Merces tarafından hello Galerisi'nden ekleniyor.</span><span class="sxs-lookup"><span data-stu-id="a8b73-121">Adding HR2day by Merces from hello gallery.</span></span>
2. <span data-ttu-id="a8b73-122">Yapılandırma ve Azure AD sınama çoklu oturum açmayı.</span><span class="sxs-lookup"><span data-stu-id="a8b73-122">Configuring and testing Azure AD single sign-on.</span></span>

## <a name="add-hr2day-by-merces-from-hello-gallery"></a><span data-ttu-id="a8b73-123">Merhaba Galerisi'nden Merces tarafından HR2day ekleme</span><span class="sxs-lookup"><span data-stu-id="a8b73-123">Add HR2day by Merces from hello gallery</span></span>
<span data-ttu-id="a8b73-124">Azure AD'ye HR2day Merces tarafından tooconfigure hello tümleştirilmesi hello galeri tooyour listesinden yönetilen SaaS uygulamaları Merces tarafından HR2day ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a8b73-124">tooconfigure hello integration of HR2day by Merces into Azure AD, add HR2day by Merces from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a8b73-125">**tooadd HR2day Merces hello galerisinden tarafından hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a8b73-125">**tooadd HR2day by Merces from hello gallery, take hello following steps:**</span></span>

1. <span data-ttu-id="a8b73-126">Merhaba, [Azure portal](https://portal.azure.com), üzerinde sol gezinti bölmesinde Merhaba, seçin hello **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="a8b73-126">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, select hello **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a8b73-128">Çok Git**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="a8b73-128">Go too**Enterprise applications**.</span></span> <span data-ttu-id="a8b73-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="a8b73-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="a8b73-131">tooadd yeni bir uygulama seçin hello **yeni uygulama** hello hello iletişim kutusunun üstündeki düğmesinde.</span><span class="sxs-lookup"><span data-stu-id="a8b73-131">tooadd a new application, select hello **New application** button on hello top of hello dialog box.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="a8b73-133">Merhaba arama kutusuna yazın **HR2day Merces tarafından**.</span><span class="sxs-lookup"><span data-stu-id="a8b73-133">In hello search box, type **HR2day by Merces**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_search.png)

5. <span data-ttu-id="a8b73-135">Merhaba Sonuçlar panelinde seçin **HR2day Merces tarafından**ve ardından hello **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="a8b73-135">In hello results panel, select **HR2day by Merces**, and then select hello **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="a8b73-137">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="a8b73-137">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="a8b73-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Merces tarafından HR2day ile test etme</span><span class="sxs-lookup"><span data-stu-id="a8b73-138">In this section, you configure and test Azure AD single sign-on with HR2day by Merces based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a8b73-139">Tek toowork'ın oturum açma Azure AD hello karşılık gelen Merces tarafından HR2day içinde tooa kullanıcı Azure AD içinde olduğu tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="a8b73-139">For single sign-on toowork, Azure AD needs tooknow who hello counterpart user in HR2day by Merces is tooa user in Azure AD.</span></span> <span data-ttu-id="a8b73-140">Diğer bir deyişle, tooestablish bir Azure AD kullanıcı ve ilgili kullanıcı HR2day Merces tarafından hello arasında bir bağlantı gerekir.</span><span class="sxs-lookup"><span data-stu-id="a8b73-140">In other words, you need tooestablish a link between an Azure AD user and hello related user in HR2day by Merces.</span></span>

<span data-ttu-id="a8b73-141">Merhaba Merces tarafından HR2day içinde atamak **kullanıcı adı** Azure AD'de çok **kullanıcıadı** tooestablish hello ilişki.</span><span class="sxs-lookup"><span data-stu-id="a8b73-141">In HR2day by Merces, assign hello **user name** in Azure AD too **Username** tooestablish hello relationship.</span></span>

<span data-ttu-id="a8b73-142">tooconfigure ve HR2day Merces tarafından ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="a8b73-142">tooconfigure and test Azure AD single sign-on with HR2day by Merces, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a8b73-143">[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on): Bu özellik, kullanıcıların toouse etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="a8b73-143">[Configure Azure AD single sign-on](#configuring-azure-ad-single-sign-on): Enable your users toouse this feature.</span></span>
2. <span data-ttu-id="a8b73-144">[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user): Test Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="a8b73-144">[Create an Azure AD test user](#creating-an-azure-ad-test-user): Test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a8b73-145">[Merces test kullanıcı tarafından bir HR2day oluşturma](#creating-an-hr2day-by-merces-test-user): Britta Simon, karşılık gelen kullanıcı bağlantılı toohello Azure AD gösterimidir Merces tarafından HR2day oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a8b73-145">[Create an HR2day by Merces test user](#creating-an-hr2day-by-merces-test-user): Create a counterpart of Britta Simon in HR2day by Merces that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a8b73-146">[Hello Azure AD test kullanıcısı atayın](#assigning-the-azure-ad-test-user): Azure AD çoklu oturum açmayı etkinleştir Britta Simon toouse.</span><span class="sxs-lookup"><span data-stu-id="a8b73-146">[Assign hello Azure AD test user](#assigning-the-azure-ad-test-user): Enable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a8b73-147">[Test çoklu oturum açma](#testing-single-sign-on): hello yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="a8b73-147">[Test single sign-on](#testing-single-sign-on): Verify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="a8b73-148">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="a8b73-148">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="a8b73-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma, HR2day Merces uygulama tarafından yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="a8b73-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your HR2day by Merces application.</span></span>

<span data-ttu-id="a8b73-150">**tooconfigure Azure AD çoklu oturum açma HR2day Merces tarafından ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a8b73-150">**tooconfigure Azure AD single sign-on with HR2day by Merces, take hello following steps:**</span></span>

1. <span data-ttu-id="a8b73-151">Merhaba hello üzerinde Azure portal'ın **Merces tarafından HR2day** uygulama tümleştirmesi sayfasında, **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="a8b73-151">In hello Azure portal, on hello **HR2day by Merces** application integration page, select **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="a8b73-153">tooenable çoklu oturum açma, hello içinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="a8b73-153">tooenable single sign-on, in hello **Single sign-on** dialog box, select **Mode** as **SAML-based Sign-on**.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_samlbase.png)

3. <span data-ttu-id="a8b73-155">Merhaba, **HR2day Merces etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a8b73-155">In hello **HR2day by Merces Domain and URLs** section, take hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_url.png)

    <span data-ttu-id="a8b73-157">a.</span><span class="sxs-lookup"><span data-stu-id="a8b73-157">a.</span></span> <span data-ttu-id="a8b73-158">Merhaba, **oturum açma URL'si** kutusuna bir URL deseni takip hello kullanarak yazın: `https://<tenantname>.force.com/<instancename>`.</span><span class="sxs-lookup"><span data-stu-id="a8b73-158">In hello **Sign-on URL** box, type a URL by using hello following pattern: `https://<tenantname>.force.com/<instancename>`.</span></span>

    <span data-ttu-id="a8b73-159">b.</span><span class="sxs-lookup"><span data-stu-id="a8b73-159">b.</span></span> <span data-ttu-id="a8b73-160">Merhaba, **tanımlayıcısı** kutusuna bir URL deseni takip hello kullanarak yazın: `https://hr2day.force.com/<companyname>`.</span><span class="sxs-lookup"><span data-stu-id="a8b73-160">In hello **Identifier** box, type a URL by using hello following pattern: `https://hr2day.force.com/<companyname>`.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a8b73-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="a8b73-161">These values are not real.</span></span> <span data-ttu-id="a8b73-162">Bu değerler, oturum açma hello gerçek URL ve tanımlayıcıdır ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="a8b73-162">Update these values with hello actual sign-on URL and identifier.</span></span> <span data-ttu-id="a8b73-163">Kişi hello [Merces istemci destek ekibi tarafından HR2day](mailto:servicedesk@merces.nl) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="a8b73-163">Contact hello [HR2day by Merces client support team](mailto:servicedesk@merces.nl) tooget these values.</span></span> 
 


4. <span data-ttu-id="a8b73-164">Merhaba üzerinde **SAML imzalama sertifikası** bölümünde, select **Certificate(Base64)**ve ardından hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="a8b73-164">On hello **SAML Signing Certificate** section, select **Certificate(Base64)**, and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_certificate.png) 

5. <span data-ttu-id="a8b73-166">Bu bölümde açıklanmıştır nasıl Itanium tabanlı sistemler için tooenable kullanıcılar tooauthenticate tooHR2day Merces tarafından Azure AD'de hesabıyla.</span><span class="sxs-lookup"><span data-stu-id="a8b73-166">This section describes how tooenable users tooauthenticate tooHR2day by Merces with their account in Azure AD.</span></span> <span data-ttu-id="a8b73-167">SAML Protokolü hello üzerinde temel Federasyon kullanarak bunu.</span><span class="sxs-lookup"><span data-stu-id="a8b73-167">They do this by using federation that's based on hello SAML protocol.</span></span>

    <span data-ttu-id="a8b73-168">Merces uygulama tarafından HR2day hello SAML onaylar tooadd özel öznitelik eşlemelerini tooyour SAML belirteci gerektiren belirli bir biçimde, bekliyor.</span><span class="sxs-lookup"><span data-stu-id="a8b73-168">Your HR2day by Merces application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token.</span></span> <span data-ttu-id="a8b73-169">Aşağıdaki ekran görüntüsü hello bunun bir örneğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="a8b73-169">hello following screenshot shows an example of this.</span></span> 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2day_00.png)
    
    > [!NOTE] 
    <span data-ttu-id="a8b73-171">Merhaba SAML onayı yapılandırmadan önce hello başvurmalıdır [HR2day Merces istemci destek ekibi tarafından](mailto:servicedesk@merces.nl) ve kiracınız için hello benzersiz tanımlayıcı özniteliği hello değerini isteyin.</span><span class="sxs-lookup"><span data-stu-id="a8b73-171">Before you can configure hello SAML assertion, you must contact hello [HR2day by Merces Client support team](mailto:servicedesk@merces.nl) and request hello value of hello unique identifier attribute for your tenant.</span></span> <span data-ttu-id="a8b73-172">Bu değer toocomplete hello adımları hello sonraki bölümde gerekir.</span><span class="sxs-lookup"><span data-stu-id="a8b73-172">You need this value toocomplete hello steps in hello next section.</span></span> 

6. <span data-ttu-id="a8b73-173">Merhaba, **çoklu oturum açma** iletişim kutusunda hello **kullanıcı öznitelikleri** bölümünde, hello SAML belirteci özniteliği hello görüntü aşağıdaki gösterildiği gibi yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="a8b73-173">In hello **Single sign-on** dialog box, in hello **User Attributes** section, configure hello SAML token attribute as shown in hello following image.</span></span> <span data-ttu-id="a8b73-174">Ardından hello aşağıdaki adımları uygulayın.</span><span class="sxs-lookup"><span data-stu-id="a8b73-174">Then take hello following steps.</span></span>
    
      | <span data-ttu-id="a8b73-175">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="a8b73-175">Attribute name</span></span>    |   <span data-ttu-id="a8b73-176">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="a8b73-176">Attribute value</span></span> |  
    | ------------------- | -------------------- |    
    | <span data-ttu-id="a8b73-177">ATTR_LOGINCLAIM</span><span class="sxs-lookup"><span data-stu-id="a8b73-177">ATTR_LOGINCLAIM</span></span> | <span data-ttu-id="a8b73-178">Birleştirme ([posta] "102938475Z", "@"</span><span class="sxs-lookup"><span data-stu-id="a8b73-178">join([mail],"102938475Z","@"</span></span> |
    
      <span data-ttu-id="a8b73-179">a.</span><span class="sxs-lookup"><span data-stu-id="a8b73-179">a.</span></span> <span data-ttu-id="a8b73-180">tooopen hello **özniteliği eklemek** iletişim kutusunda **Ekle özniteliği**.</span><span class="sxs-lookup"><span data-stu-id="a8b73-180">tooopen hello **Add Attribute** dialog, select **Add attribute**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hr2day-tutorial/tutorial_attribute_04.png)

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hr2day-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="a8b73-183">b.</span><span class="sxs-lookup"><span data-stu-id="a8b73-183">b.</span></span> <span data-ttu-id="a8b73-184">Merhaba, **adı** kutusuna **ATTR_LOGINCLAIM**.</span><span class="sxs-lookup"><span data-stu-id="a8b73-184">In hello **Name** box, type **ATTR_LOGINCLAIM**.</span></span>

    <span data-ttu-id="a8b73-185">c.</span><span class="sxs-lookup"><span data-stu-id="a8b73-185">c.</span></span> <span data-ttu-id="a8b73-186">Merhaba gelen **değeri** listesinde **Join()**.</span><span class="sxs-lookup"><span data-stu-id="a8b73-186">From hello **Value** list, select **Join()**.</span></span>

    <span data-ttu-id="a8b73-187">d.</span><span class="sxs-lookup"><span data-stu-id="a8b73-187">d.</span></span> <span data-ttu-id="a8b73-188">Merhaba gelen **Dize1** listesinde **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="a8b73-188">From hello **String1** list, select **user.mail**.</span></span>

    <span data-ttu-id="a8b73-189">e.</span><span class="sxs-lookup"><span data-stu-id="a8b73-189">e.</span></span> <span data-ttu-id="a8b73-190">İçin **dize2**, HR2day ekibiniz tarafından sunulan benzersiz bir tanımlayıcı hello yazın.</span><span class="sxs-lookup"><span data-stu-id="a8b73-190">For **String2**, type hello unique identifier that's provided by your HR2day team.</span></span>

    <span data-ttu-id="a8b73-191">f.</span><span class="sxs-lookup"><span data-stu-id="a8b73-191">f.</span></span> <span data-ttu-id="a8b73-192">Merhaba, **ayırıcı** kutusuna  **@** .</span><span class="sxs-lookup"><span data-stu-id="a8b73-192">In hello **Separator** box, type **@**.</span></span>
    
    <span data-ttu-id="a8b73-193">g.</span><span class="sxs-lookup"><span data-stu-id="a8b73-193">g.</span></span> <span data-ttu-id="a8b73-194">Seçin **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="a8b73-194">Select **Ok**.</span></span>

7. <span data-ttu-id="a8b73-195">Select hello **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a8b73-195">Select hello **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hr2day-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="a8b73-197">Merhaba, **HR2day Merces yapılandırma tarafından** bölümünde, select **yapılandırma HR2day Merces tarafından** tooopen hello **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="a8b73-197">In hello **HR2day by Merces Configuration** section, select **Configure HR2day by Merces** tooopen hello **Configure sign-on** window.</span></span> <span data-ttu-id="a8b73-198">Kopya hello **Sign-Out URL**, **SAML varlık kimliği**, ve **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru** bölümü.</span><span class="sxs-lookup"><span data-stu-id="a8b73-198">Copy hello **Sign-Out URL**, **SAML Entity ID**, and **SAML Single Sign-On Service URL** from hello **Quick Reference** section.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_configure.png) 

9. <span data-ttu-id="a8b73-200">Uygulama, kişi hello için SSO tooconfigure [HR2day Merces istemci destek ekibi tarafından](mailTo:servicedesk@merces.nl).</span><span class="sxs-lookup"><span data-stu-id="a8b73-200">tooconfigure SSO  for your application, contact hello [HR2day by Merces client support team](mailTo:servicedesk@merces.nl).</span></span> <span data-ttu-id="a8b73-201">İndirilen hello attach **Certificate(Base64)** dosya tooyour e-posta.</span><span class="sxs-lookup"><span data-stu-id="a8b73-201">Attach hello downloaded **Certificate(Base64)** file tooyour email.</span></span> <span data-ttu-id="a8b73-202">Ayrıca hello sağlamak **Sign-Out URL**, **SAML varlık kimliği**, ve **SAML çoklu oturum açma hizmet URL'si** böylece SSO tümleştirmesi için yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="a8b73-202">Also provide hello **Sign-Out URL**, **SAML Entity ID**, and **SAML Single Sign-On Service URL** so that they can be configured for SSO integration.</span></span>

    > [!NOTE]
    ><span data-ttu-id="a8b73-203">Bu tümleştirme hello desenle ayarlamak varlık kimliği toobe hello gereken toohello Merces takım Bahsediyor **https://hr2day.force.com/INSTANCENAME**.</span><span class="sxs-lookup"><span data-stu-id="a8b73-203">Mention toohello Merces team that this integration needs hello Entity ID toobe set with hello pattern **https://hr2day.force.com/INSTANCENAME**.</span></span>

    > [!TIP]
    ><span data-ttu-id="a8b73-204">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="a8b73-204">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a8b73-205">Bu uygulamayı hello ekledikten sonra **Active Directory** > **kurumsal uygulamalar** bölümü, select hello **çoklu oturum açma** sekmesi. Ardından hello aracılığıyla belgelere erişimi hello katıştırılmış **yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="a8b73-205">After you add this app from hello **Active Directory** > **Enterprise Applications** section, select hello **Single Sign-On** tab. Then access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a8b73-206">Daha fazla bilgiyi hello hello embedded belgeler özelliği hakkında [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="a8b73-206">You can read more about hello embedded documentation feature in hello [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="a8b73-207">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a8b73-207">Create an Azure AD test user</span></span>
<span data-ttu-id="a8b73-208">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="a8b73-208">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="a8b73-210">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a8b73-210">**toocreate a test user in Azure AD, take hello following steps:**</span></span>

1. <span data-ttu-id="a8b73-211">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, seçin hello **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="a8b73-211">In hello **Azure portal**, on hello left navigation pane, select hello **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-hr2day-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a8b73-213">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="a8b73-213">toodisplay hello list of users, go too**Users and groups**, and then select **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-hr2day-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a8b73-215">tooopen hello **kullanıcı** iletişim kutusunda **Ekle** hello iletişim kutusunun hello üstte.</span><span class="sxs-lookup"><span data-stu-id="a8b73-215">tooopen hello **User** dialog box, select **Add** on hello top of hello dialog box.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-hr2day-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a8b73-217">Merhaba, **kullanıcı** iletişim kutusunda, aşağıdaki adımları gerçekleştirin hello:</span><span class="sxs-lookup"><span data-stu-id="a8b73-217">In hello **User** dialog box, take hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-hr2day-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a8b73-219">a.</span><span class="sxs-lookup"><span data-stu-id="a8b73-219">a.</span></span> <span data-ttu-id="a8b73-220">Merhaba, **adı** kutusuna **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a8b73-220">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a8b73-221">b.</span><span class="sxs-lookup"><span data-stu-id="a8b73-221">b.</span></span> <span data-ttu-id="a8b73-222">Merhaba, **kullanıcı adı** kutusu, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="a8b73-222">In hello **User name** box, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a8b73-223">c.</span><span class="sxs-lookup"><span data-stu-id="a8b73-223">c.</span></span> <span data-ttu-id="a8b73-224">Seçin **Göster parola**ve ardından hello parolayı not alın.</span><span class="sxs-lookup"><span data-stu-id="a8b73-224">Select **Show Password**, and then write down hello password.</span></span>

    <span data-ttu-id="a8b73-225">d.</span><span class="sxs-lookup"><span data-stu-id="a8b73-225">d.</span></span> <span data-ttu-id="a8b73-226">**Oluştur**’u seçin.</span><span class="sxs-lookup"><span data-stu-id="a8b73-226">Select **Create**.</span></span>
 
### <a name="create-an-hr2day-by-merces-test-user"></a><span data-ttu-id="a8b73-227">Bir HR2day tarafından Merces test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a8b73-227">Create an HR2day by Merces test user</span></span>

<span data-ttu-id="a8b73-228">Bu bölümde Hello amacı toocreate Britta Simon içinde HR2day tarafından Merces adlı bir kullanıcı var.</span><span class="sxs-lookup"><span data-stu-id="a8b73-228">hello objective of this section is toocreate a user called Britta Simon in HR2day by Merces.</span></span> <span data-ttu-id="a8b73-229">Merhaba HR2day hesabındaki tooadd hello kullanıcıların çalışması ile Merhaba [HR2day Merces istemci destek ekibi tarafından](mailto:servicedesk@merces.nl).</span><span class="sxs-lookup"><span data-stu-id="a8b73-229">tooadd hello users in hello HR2day account, work with hello [HR2day by Merces client support team](mailto:servicedesk@merces.nl).</span></span> 

> [!NOTE]
> <span data-ttu-id="a8b73-230">Bir kullanıcı toocreate el ile gerekiyorsa hello başvurun [HR2day Merces istemci destek ekibi tarafından](mailto:servicedesk@merces.nl).</span><span class="sxs-lookup"><span data-stu-id="a8b73-230">If you need toocreate a user manually, contact hello [HR2day by Merces client support team](mailto:servicedesk@merces.nl).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="a8b73-231">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="a8b73-231">Assign hello Azure AD test user</span></span>

<span data-ttu-id="a8b73-232">Bu bölümde, kendi erişim tooHR2day Merces tarafından vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="a8b73-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooHR2day by Merces.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="a8b73-234">**tooassign Britta Simon tooHR2day Merces tarafından hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a8b73-234">**tooassign Britta Simon tooHR2day by Merces, take hello following steps:**</span></span>

1. <span data-ttu-id="a8b73-235">Hello Azure portal, açık hello uygulamaları görüntülemek, toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="a8b73-235">In hello Azure portal, open hello applications view, go toohello directory view, and then go too**Enterprise applications**.</span></span> <span data-ttu-id="a8b73-236">Ardından, **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="a8b73-236">Next, select **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="a8b73-238">Merhaba uygulamalar listesinde **HR2day Merces tarafından**.</span><span class="sxs-lookup"><span data-stu-id="a8b73-238">In hello applications list, select **HR2day by Merces**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_app.png) 

3. <span data-ttu-id="a8b73-240">Merhaba soldaki Hello menüde seçin **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="a8b73-240">In hello menu on hello left, select **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="a8b73-242">Select hello **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a8b73-242">Select hello **Add** button.</span></span> <span data-ttu-id="a8b73-243">Ardından hello **eklemek atama** iletişim kutusunda **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="a8b73-243">Then, in hello **Add Assignment** dialog box, select **Users and groups**.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="a8b73-245">Merhaba, **kullanıcılar ve gruplar** iletişim kutusunda hello **kullanıcılar** listesinde **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="a8b73-245">In hello **Users and groups** dialog box, in hello **Users** list, select **Britta Simon**.</span></span>

6. <span data-ttu-id="a8b73-246">Merhaba tıklatın **seçin** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a8b73-246">Click hello **Select** button.</span></span>

7. <span data-ttu-id="a8b73-247">Merhaba, **eklemek atama** iletişim kutusunda **atamak**.</span><span class="sxs-lookup"><span data-stu-id="a8b73-247">In hello **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="a8b73-248">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="a8b73-248">Test single sign-on</span></span>

<span data-ttu-id="a8b73-249">Merhaba, bu bölümün amacı olan tootest kullanarak Azure AD çoklu oturum açma yapılandırmanızı hello erişim paneli.</span><span class="sxs-lookup"><span data-stu-id="a8b73-249">hello objective of this section is tootest your Azure AD single sign-on configuration by using hello Access Panel.</span></span>  

<span data-ttu-id="a8b73-250">Merhaba erişim paneli Merces parçasında tarafından hello HR2day seçtiğinizde otomatik olarak tooyour HR2day Merces uygulama tarafından oturumunuz.</span><span class="sxs-lookup"><span data-stu-id="a8b73-250">When you select hello HR2day by Merces tile in hello Access Panel, you automatically get signed in  tooyour HR2day by Merces application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a8b73-251">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="a8b73-251">Additional resources</span></span>

* [<span data-ttu-id="a8b73-252">İlgili öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="a8b73-252">List of tutorials about how tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a8b73-253">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="a8b73-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_203.png

