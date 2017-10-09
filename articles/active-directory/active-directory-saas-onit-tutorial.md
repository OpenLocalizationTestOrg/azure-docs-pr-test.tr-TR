---
title: "Öğretici: Azure Active Directory Tümleştirme ile Onit | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Onit arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: bc479a28-8fcd-493f-ac53-681975a5149c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jeedes
ms.openlocfilehash: 9e12449e5bf7f169b3cadfaa12438ac5d52ed8f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-onit"></a><span data-ttu-id="1b9ef-103">Öğretici: Azure Active Directory Tümleştirme Onit ile</span><span class="sxs-lookup"><span data-stu-id="1b9ef-103">Tutorial: Azure Active Directory integration with Onit</span></span>

<span data-ttu-id="1b9ef-104">Bu öğreticide, bilgi nasıl toointegrate Onit Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1b9ef-104">In this tutorial, you learn how toointegrate Onit with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1b9ef-105">Onit Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="1b9ef-105">Integrating Onit with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1b9ef-106">Erişim tooOnit sahip Azure AD'de kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-106">You can control in Azure AD who has access tooOnit.</span></span>
- <span data-ttu-id="1b9ef-107">Kullanıcıların tooautomatically get açan tooOnit (çoklu oturum açma) Azure AD hesaplarına ile etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-107">You can enable your users tooautomatically get signed-on tooOnit (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="1b9ef-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="1b9ef-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1b9ef-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1b9ef-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="1b9ef-110">Prerequisites</span></span>

<span data-ttu-id="1b9ef-111">tooconfigure Onit ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="1b9ef-111">tooconfigure Azure AD integration with Onit, you need hello following items:</span></span>

- <span data-ttu-id="1b9ef-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="1b9ef-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1b9ef-113">Bir Onit çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="1b9ef-113">An Onit single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1b9ef-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1b9ef-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="1b9ef-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1b9ef-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1b9ef-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1b9ef-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1b9ef-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="1b9ef-118">Scenario description</span></span>

<span data-ttu-id="1b9ef-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1b9ef-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="1b9ef-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1b9ef-121">Merhaba Galerisi'nden Onit ekleme</span><span class="sxs-lookup"><span data-stu-id="1b9ef-121">Adding Onit from hello gallery</span></span>
2. <span data-ttu-id="1b9ef-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="1b9ef-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-onit-from-hello-gallery"></a><span data-ttu-id="1b9ef-123">Merhaba Galerisi'nden Onit ekleme</span><span class="sxs-lookup"><span data-stu-id="1b9ef-123">Adding Onit from hello gallery</span></span>
<span data-ttu-id="1b9ef-124">Azure AD'ye tooconfigure hello tümleştirme Onit, tooadd Onit hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-124">tooconfigure hello integration of Onit into Azure AD, you need tooadd Onit from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1b9ef-125">**tooadd Onit hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="1b9ef-125">**tooadd Onit from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1b9ef-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory düğmesi][1]

2. <span data-ttu-id="1b9ef-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1b9ef-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-129">Then go too**All applications**.</span></span>

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="1b9ef-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Merhaba yeni uygulama düğmesi][3]

4. <span data-ttu-id="1b9ef-133">Merhaba arama kutusuna yazın **Onit**seçin **Onit** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-133">In hello search box, type **Onit**, select **Onit** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Merhaba sonuçları listesinde Onit](./media/active-directory-saas-onit-tutorial/tutorial_onit_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="1b9ef-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="1b9ef-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="1b9ef-136">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Onit ile test etme</span><span class="sxs-lookup"><span data-stu-id="1b9ef-136">In this section, you configure and test Azure AD single sign-on with Onit based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1b9ef-137">Tek toowork'ın oturum açma hangi hello karşılık gelen Onit içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Onit is tooa user in Azure AD.</span></span> <span data-ttu-id="1b9ef-138">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Onit hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-138">In other words, a link relationship between an Azure AD user and hello related user in Onit needs toobe established.</span></span>

<span data-ttu-id="1b9ef-139">Merhaba hello değeri Onit içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-139">In Onit, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="1b9ef-140">tooconfigure ve Onit ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="1b9ef-140">tooconfigure and test Azure AD single sign-on with Onit, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1b9ef-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1b9ef-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1b9ef-143">**[Bir Onit test kullanıcısı oluşturma](#create-an-onit-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Onit içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-143">**[Create an Onit test user](#create-an-onit-test-user)** - toohave a counterpart of Britta Simon in Onit that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1b9ef-144">**[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1b9ef-145">**[Test çoklu oturum açma](#test-single-sign-on)**  tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-145">**[Test single sign-on](#test-single-sign-on)** tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="1b9ef-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="1b9ef-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="1b9ef-147">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Onit uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Onit application.</span></span>

<span data-ttu-id="1b9ef-148">**tooconfigure Azure AD çoklu oturum açma ile Onit, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="1b9ef-148">**tooconfigure Azure AD single sign-on with Onit, perform hello following steps:**</span></span>

1. <span data-ttu-id="1b9ef-149">Hello hello üzerinde Azure portal'ın **Onit** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-149">In hello Azure portal, on hello **Onit** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. <span data-ttu-id="1b9ef-151">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-onit-tutorial/tutorial_onit_samlbase.png)

3. <span data-ttu-id="1b9ef-153">Merhaba üzerinde **Onit etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="1b9ef-153">On hello **Onit Domain and URLs** section, perform hello following steps:</span></span>

    ![Onit etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-onit-tutorial/tutorial_onit_url.png)

    <span data-ttu-id="1b9ef-155">a.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-155">a.</span></span> <span data-ttu-id="1b9ef-156">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<sub-domain>.onit.com`</span><span class="sxs-lookup"><span data-stu-id="1b9ef-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<sub-domain>.onit.com`</span></span>

    <span data-ttu-id="1b9ef-157">b.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-157">b.</span></span> <span data-ttu-id="1b9ef-158">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<sub-domain>.onit.com`</span><span class="sxs-lookup"><span data-stu-id="1b9ef-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<sub-domain>.onit.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1b9ef-159">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-159">These values are not real.</span></span> <span data-ttu-id="1b9ef-160">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="1b9ef-161">Kişi [Onit istemci destek ekibi](https://www.onit.com/support) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-161">Contact [Onit Client support team](https://www.onit.com/support) tooget these values.</span></span> 
 
4. <span data-ttu-id="1b9ef-162">Merhaba üzerinde **SAML imzalama sertifikası** bölümü, kopyalama hello **parmak İZİ** sertifika değeri.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-162">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-onit-tutorial/tutorial_onit_certificate.png) 

5. <span data-ttu-id="1b9ef-164">Onit uygulama hello SAML onaylar belirli bir biçimde bekler.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-164">Onit application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="1b9ef-165">Lütfen bu uygulama için talep aşağıdaki hello yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-165">Please configure hello following claims for this application.</span></span> <span data-ttu-id="1b9ef-166">Hello başlangıç değerleri bu özniteliklerin yönetebilirsiniz **"Atrribute"** hello uygulama sekmesinde.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-166">You can manage hello values of these attributes from hello **"Atrribute"** tab of hello application.</span></span> <span data-ttu-id="1b9ef-167">Ekran aşağıdaki hello bunun bir örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-167">hello following screenshot shows an example for this.</span></span> 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-onit-tutorial/tutorial_onit_attribute.png) 

6. <span data-ttu-id="1b9ef-169">Merhaba, **kullanıcı öznitelikleri** hello bölüm **çoklu oturum açma** iletişim kutusunda, SAML belirteci özniteliği hello görüntüde gösterildiği gibi yapılandırmak ve hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="1b9ef-169">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="1b9ef-170">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="1b9ef-170">Attribute Name</span></span> | <span data-ttu-id="1b9ef-171">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="1b9ef-171">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="1b9ef-172">E-posta</span><span class="sxs-lookup"><span data-stu-id="1b9ef-172">email</span></span> | <span data-ttu-id="1b9ef-173">User.Mail</span><span class="sxs-lookup"><span data-stu-id="1b9ef-173">user.mail</span></span> |
    
    <span data-ttu-id="1b9ef-174">a.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-174">a.</span></span> <span data-ttu-id="1b9ef-175">Tıklatın **Ekle özniteliği** tooopen hello **özniteliği eklemek** iletişim.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-175">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-onit-tutorial/tutorial_attribute_04.png)

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-onit-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="1b9ef-178">b.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-178">b.</span></span> <span data-ttu-id="1b9ef-179">Merhaba, **adı** metin kutusuna, ilgili satır için gösterilen türü hello öznitelik adı.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-179">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="1b9ef-180">c.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-180">c.</span></span> <span data-ttu-id="1b9ef-181">Merhaba gelen **değeri** listesinde, ilgili satır için gösterilen türü hello öznitelik değeri.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-181">From hello **Value** list, type hello attribute value shown for that row.</span></span>

    <span data-ttu-id="1b9ef-182">d.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-182">d.</span></span> <span data-ttu-id="1b9ef-183">Merhaba bırakın **Namespace** boş.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-183">Leave hello **Namespace** blank.</span></span>
    
    <span data-ttu-id="1b9ef-184">e.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-184">e.</span></span> <span data-ttu-id="1b9ef-185">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-185">Click **Ok**.</span></span>

7. <span data-ttu-id="1b9ef-186">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-186">Click **Save** button.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-onit-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="1b9ef-188">Merhaba üzerinde **Onit yapılandırma** 'yi tıklatın **yapılandırma Onit** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-188">On hello **Onit Configuration** section, click **Configure Onit** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="1b9ef-189">Kopya hello **Sign-Out URL, SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="1b9ef-189">Copy hello **Sign-Out URL, SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Onit yapılandırma](./media/active-directory-saas-onit-tutorial/tutorial_onit_configure.png)

9. <span data-ttu-id="1b9ef-191">Farklı web tarayıcısı penceresinde Onit şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-191">In a different web browser window, log into your Onit company site as an administrator.</span></span>

10. <span data-ttu-id="1b9ef-192">Hello içinde hello üst menüsünde **Yönetim**.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-192">In hello menu on hello top, click **Administration**.</span></span>
   
   <span data-ttu-id="1b9ef-193">![Yönetim](./media/active-directory-saas-onit-tutorial/IC791174.png "Yönetim")</span><span class="sxs-lookup"><span data-stu-id="1b9ef-193">![Administration](./media/active-directory-saas-onit-tutorial/IC791174.png "Administration")</span></span>
11. <span data-ttu-id="1b9ef-194">Tıklatın **düzenleme Corporation**.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-194">Click **Edit Corporation**.</span></span>
   
   <span data-ttu-id="1b9ef-195">![Düzen Corporation](./media/active-directory-saas-onit-tutorial/IC791175.png "düzenleme Corporation")</span><span class="sxs-lookup"><span data-stu-id="1b9ef-195">![Edit Corporation](./media/active-directory-saas-onit-tutorial/IC791175.png "Edit Corporation")</span></span>
   
12. <span data-ttu-id="1b9ef-196">Merhaba tıklatın **güvenlik** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-196">Click hello **Security** tab.</span></span>
    
    <span data-ttu-id="1b9ef-197">![Düzen şirket bilgileri](./media/active-directory-saas-onit-tutorial/IC791176.png "düzenleme şirket bilgileri")</span><span class="sxs-lookup"><span data-stu-id="1b9ef-197">![Edit Company Information](./media/active-directory-saas-onit-tutorial/IC791176.png "Edit Company Information")</span></span>

13. <span data-ttu-id="1b9ef-198">Merhaba üzerinde **güvenlik** sekmesinde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="1b9ef-198">On hello **Security** tab, perform hello following steps:</span></span>

    <span data-ttu-id="1b9ef-199">![Çoklu oturum açma](./media/active-directory-saas-onit-tutorial/IC791177.png "çoklu oturum açma")</span><span class="sxs-lookup"><span data-stu-id="1b9ef-199">![Single Sign-On](./media/active-directory-saas-onit-tutorial/IC791177.png "Single Sign-On")</span></span>

    <span data-ttu-id="1b9ef-200">a.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-200">a.</span></span> <span data-ttu-id="1b9ef-201">Olarak **kimlik doğrulama stratejisi**seçin **çoklu oturum açma ve parola**.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-201">As **Authentication Strategy**, select **Single Sign On and Password**.</span></span>
    
    <span data-ttu-id="1b9ef-202">b.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-202">b.</span></span> <span data-ttu-id="1b9ef-203">İçinde **IDP hedef URL** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-203">In **Idp Target URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="1b9ef-204">c.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-204">c.</span></span> <span data-ttu-id="1b9ef-205">İçinde **IDP oturum kapatma URL'si** metin kutusuna, Yapıştır hello değerini **Sign-Out URL**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-205">In **Idp logout URL** textbox, paste hello value of  **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="1b9ef-206">d.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-206">d.</span></span> <span data-ttu-id="1b9ef-207">İçinde **IDP sertifika parmak izi (SHA1)** metin kutusuna, Yapıştır hello **parmak izi** Azure portalından kopyaladığınız sertifika değeri.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-207">In **Idp Cert Fingerprint (SHA1)** textbox, paste hello  **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span>

> [!TIP]
> <span data-ttu-id="1b9ef-208">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="1b9ef-208">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1b9ef-209">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-209">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1b9ef-210">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1b9ef-210">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="1b9ef-211">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="1b9ef-211">Create an Azure AD test user</span></span>

<span data-ttu-id="1b9ef-212">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-212">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="1b9ef-214">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="1b9ef-214">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1b9ef-215">Merhaba hello sol bölmede Azure portal hello tıklatın **Azure Active Directory** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-215">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-onit-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="1b9ef-217">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-217">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-onit-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="1b9ef-219">tooopen hello **kullanıcı** iletişim kutusu, tıklatın **Ekle** hello hello üstündeki **tüm kullanıcılar** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-219">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Merhaba Ekle düğmesi](./media/active-directory-saas-onit-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="1b9ef-221">Merhaba, **kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="1b9ef-221">In hello **User** dialog box, perform hello following steps:</span></span>

    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-onit-tutorial/create_aaduser_04.png)

    <span data-ttu-id="1b9ef-223">a.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-223">a.</span></span> <span data-ttu-id="1b9ef-224">Merhaba, **adı** kutusuna **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-224">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1b9ef-225">b.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-225">b.</span></span> <span data-ttu-id="1b9ef-226">Merhaba, **kullanıcı adı** kutusuna, kullanıcının Britta Simon hello e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-226">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="1b9ef-227">c.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-227">c.</span></span> <span data-ttu-id="1b9ef-228">Select hello **Göster parola** onay kutusunu işaretleyin ve ardından hello görüntülenen hello değerini aşağı yazma **parola** kutusu.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-228">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="1b9ef-229">d.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-229">d.</span></span> <span data-ttu-id="1b9ef-230">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-230">Click **Create**.</span></span>
 
### <a name="create-an-onit-test-user"></a><span data-ttu-id="1b9ef-231">Bir Onit test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="1b9ef-231">Create an Onit test user</span></span>

<span data-ttu-id="1b9ef-232">Onit içine sipariş tooenable Azure AD kullanıcıların toolog bunların Onit sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-232">In order tooenable Azure AD users toolog into Onit, they must be provisioned into Onit.</span></span>  

<span data-ttu-id="1b9ef-233">Onit Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-233">In hello case of Onit, provisioning is a manual task.</span></span>

<span data-ttu-id="1b9ef-234">**tooconfigure kullanıcı hazırlama, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="1b9ef-234">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="1b9ef-235">Tooyour üzerinde oturum **Onit** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-235">Sign on tooyour **Onit** company site as an administrator.</span></span>
2. <span data-ttu-id="1b9ef-236">Tıklatın **kullanıcı ekleme**.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-236">Click **Add User**.</span></span>
   
   <span data-ttu-id="1b9ef-237">![Yönetim](./media/active-directory-saas-onit-tutorial/IC791180.png "Yönetim")</span><span class="sxs-lookup"><span data-stu-id="1b9ef-237">![Administration](./media/active-directory-saas-onit-tutorial/IC791180.png "Administration")</span></span>
3. <span data-ttu-id="1b9ef-238">Merhaba üzerinde **Kullanıcı Ekle** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="1b9ef-238">On hello **Add User** dialog page, perform hello following steps:</span></span>
   
   <span data-ttu-id="1b9ef-239">![Kullanıcı ekleme](./media/active-directory-saas-onit-tutorial/IC791181.png "kullanıcı ekleme")</span><span class="sxs-lookup"><span data-stu-id="1b9ef-239">![Add User](./media/active-directory-saas-onit-tutorial/IC791181.png "Add User")</span></span>
   
  1. <span data-ttu-id="1b9ef-240">Türü hello **adı** ve hello **e-posta adresi** geçerli bir Azure hello tooprovision istediğiniz AD hesabının ilgili metin kutuları.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-240">Type hello **Name** and hello **Email Address** of a valid Azure AD account you want tooprovision into hello related textboxes.</span></span>
  2. <span data-ttu-id="1b9ef-241">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-241">Click **Create**.</span></span>    
   
 > [!NOTE]
 > <span data-ttu-id="1b9ef-242">Hello Azure Active Directory hesap sahibi bir e-posta alır ve onu etkinleştirilmeden önce bir bağlantı tooconfirm hesaplarında izler.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-242">hello Azure Active Directory account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="1b9ef-243">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="1b9ef-243">Assign hello Azure AD test user</span></span>

<span data-ttu-id="1b9ef-244">Bu bölümde, erişim tooOnit vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-244">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooOnit.</span></span>

![Merhaba kullanıcı rolü atayın][200] 

<span data-ttu-id="1b9ef-246">**tooassign Britta Simon tooOnit hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="1b9ef-246">**tooassign Britta Simon tooOnit, perform hello following steps:**</span></span>

1. <span data-ttu-id="1b9ef-247">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-247">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="1b9ef-249">Merhaba uygulamalar listesinde **Onit**.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-249">In hello applications list, select **Onit**.</span></span>

    ![Merhaba Onit bağlantı hello uygulamalar listesinde](./media/active-directory-saas-onit-tutorial/tutorial_onit_app.png)  

3. <span data-ttu-id="1b9ef-251">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-251">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202]

4. <span data-ttu-id="1b9ef-253">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-253">Click **Add** button.</span></span> <span data-ttu-id="1b9ef-254">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Merhaba eklemek atama bölmesi][203]

5. <span data-ttu-id="1b9ef-256">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-256">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1b9ef-257">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1b9ef-258">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="1b9ef-259">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="1b9ef-259">Test single sign-on</span></span>

<span data-ttu-id="1b9ef-260">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-260">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1b9ef-261">Merhaba Onit hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Onit uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1b9ef-261">When you click hello Onit tile in hello Access Panel, you should get automatically signed-on tooyour Onit application.</span></span>
<span data-ttu-id="1b9ef-262">Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1b9ef-262">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="1b9ef-263">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="1b9ef-263">Additional resources</span></span>

* [<span data-ttu-id="1b9ef-264">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="1b9ef-264">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1b9ef-265">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="1b9ef-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-onit-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-onit-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-onit-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-onit-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-onit-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-onit-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-onit-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-onit-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-onit-tutorial/tutorial_general_203.png

