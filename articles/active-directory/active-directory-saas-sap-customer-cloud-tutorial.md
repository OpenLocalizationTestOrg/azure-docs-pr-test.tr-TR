---
title: "Öğretici: Müşteri için SAP bulut Azure Active Directory Tümleştirmesi | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve müşteri için SAP bulut arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 90154dab-eba2-4563-bcf0-f2acc797ea97
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 0525ea81122458ab3ac24a5bdb0b5f628405dd05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-cloud-for-customer"></a><span data-ttu-id="53798-103">Öğretici: Müşteri için SAP bulut Azure Active Directory Tümleştirmesi</span><span class="sxs-lookup"><span data-stu-id="53798-103">Tutorial: Azure Active Directory integration with SAP Cloud for Customer</span></span>

<span data-ttu-id="53798-104">Bu öğreticide, nasıl toointegrate SAP öğrenmek için Azure Active Directory (Azure AD) ile müşteri bulut.</span><span class="sxs-lookup"><span data-stu-id="53798-104">In this tutorial, you learn how toointegrate SAP Cloud for Customer with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="53798-105">Azure AD ile müşteri için SAP bulut tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="53798-105">Integrating SAP Cloud for Customer with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="53798-106">Müşteri için erişim tooSAP bulut olan Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="53798-106">You can control in Azure AD who has access tooSAP Cloud for Customer</span></span>
- <span data-ttu-id="53798-107">Azure AD hesaplarına (çoklu oturum açma) müşteri için kullanıcılar tooautomatically get açan tooSAP bulut etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="53798-107">You can enable your users tooautomatically get signed-on tooSAP Cloud for Customer (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="53798-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="53798-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="53798-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="53798-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="53798-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="53798-110">Prerequisites</span></span>

<span data-ttu-id="53798-111">tooconfigure müşteri için SAP bulut ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="53798-111">tooconfigure Azure AD integration with SAP Cloud for Customer, you need hello following items:</span></span>

- <span data-ttu-id="53798-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="53798-112">An Azure AD subscription</span></span>
- <span data-ttu-id="53798-113">SAP Bulutu müşteri çoklu oturum açma için abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="53798-113">A SAP Cloud for Customer single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="53798-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="53798-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="53798-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="53798-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="53798-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="53798-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="53798-117">Bir Azure AD deneme ortam yoksa, burada bir aylık deneme elde edebilirsiniz: [deneme teklifi](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="53798-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="53798-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="53798-118">Scenario description</span></span>
<span data-ttu-id="53798-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="53798-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="53798-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="53798-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="53798-121">SAP bulut müşteri için hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="53798-121">Adding SAP Cloud for Customer from hello gallery</span></span>
2. <span data-ttu-id="53798-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="53798-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-cloud-for-customer-from-hello-gallery"></a><span data-ttu-id="53798-123">SAP bulut müşteri için hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="53798-123">Adding SAP Cloud for Customer from hello gallery</span></span>
<span data-ttu-id="53798-124">Azure AD'ye müşteri için tooconfigure hello tümleştirme SAP bulutun tooadd SAP bulut hello galeri tooyour listesinden yönetilen SaaS uygulamaları için müşteri gerekir.</span><span class="sxs-lookup"><span data-stu-id="53798-124">tooconfigure hello integration of SAP Cloud for Customer into Azure AD, you need tooadd SAP Cloud for Customer from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="53798-125">**tooadd hello galerisinden müşteri için SAP bulut hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="53798-125">**tooadd SAP Cloud for Customer from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="53798-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="53798-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="53798-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="53798-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="53798-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="53798-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="53798-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="53798-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="53798-133">Merhaba arama kutusuna yazın **müşteri için SAP bulut**.</span><span class="sxs-lookup"><span data-stu-id="53798-133">In hello search box, type **SAP Cloud for Customer**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_search.png)

5. <span data-ttu-id="53798-135">Merhaba Sonuçlar panelinde seçin **müşteri için SAP bulut**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="53798-135">In hello results panel, select **SAP Cloud for Customer**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="53798-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="53798-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="53798-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma SAP bulut ile "Britta Simon" adlı bir test kullanıcıya bağlı müşteri için test etme.</span><span class="sxs-lookup"><span data-stu-id="53798-138">In this section, you configure and test Azure AD single sign-on with SAP Cloud for Customer based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="53798-139">Tek toowork'ın oturum açma hangi hello karşılık gelen müşteri için SAP bulutta tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="53798-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SAP Cloud for Customer is tooa user in Azure AD.</span></span> <span data-ttu-id="53798-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve müşteri için SAP bulutta hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="53798-140">In other words, a link relationship between an Azure AD user and hello related user in SAP Cloud for Customer needs toobe established.</span></span>

<span data-ttu-id="53798-141">Merhaba hello değeri müşteri SAP buluta atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="53798-141">In SAP Cloud for Customer, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="53798-142">tooconfigure ve Azure AD çoklu oturum açma ile test SAP bulut müşteri için yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="53798-142">tooconfigure and test Azure AD single sign-on with SAP Cloud for Customer, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="53798-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="53798-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="53798-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="53798-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="53798-145">**[Müşteri test kullanıcısı için bir SAP bulut oluşturma](#creating-a-sap-cloud-for-customer-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir müşteri için SAP bulutta, karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="53798-145">**[Creating a SAP Cloud for Customer test user](#creating-a-sap-cloud-for-customer-test-user)** - toohave a counterpart of Britta Simon in SAP Cloud for Customer that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="53798-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="53798-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="53798-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="53798-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="53798-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="53798-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="53798-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve SAP bulut müşteri uygulaması için çoklu oturum açmayı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="53798-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SAP Cloud for Customer application.</span></span>

<span data-ttu-id="53798-150">**Müşteri, SAP bulut ile Azure AD çoklu oturum açma tooconfigure hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="53798-150">**tooconfigure Azure AD single sign-on with SAP Cloud for Customer, perform hello following steps:**</span></span>

1. <span data-ttu-id="53798-151">Merhaba hello üzerinde Azure portal'ın **müşteri için SAP bulut** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="53798-151">In hello Azure portal, on hello **SAP Cloud for Customer** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="53798-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="53798-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_samlbase.png)

3. <span data-ttu-id="53798-155">Merhaba üzerinde **müşteri etki alanı ve URL'ler için SAP bulut** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="53798-155">On hello **SAP Cloud for Customer Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_url.png)

    <span data-ttu-id="53798-157">a.</span><span class="sxs-lookup"><span data-stu-id="53798-157">a.</span></span> <span data-ttu-id="53798-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<server name>.crm.ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="53798-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<server name>.crm.ondemand.com`</span></span>

    <span data-ttu-id="53798-159">b.</span><span class="sxs-lookup"><span data-stu-id="53798-159">b.</span></span> <span data-ttu-id="53798-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<server name>.crm.ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="53798-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<server name>.crm.ondemand.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="53798-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="53798-161">These values are not real.</span></span> <span data-ttu-id="53798-162">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="53798-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="53798-163">Kişi [müşteri istemci destek ekibi için SAP bulut](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="53798-163">Contact [SAP Cloud for Customer Client support team](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) tooget these values.</span></span> 

4. <span data-ttu-id="53798-164">Merhaba üzerinde **kullanıcı öznitelikleri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="53798-164">On hello **User Attributes** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_attribute.png)

    <span data-ttu-id="53798-166">a.</span><span class="sxs-lookup"><span data-stu-id="53798-166">a.</span></span> <span data-ttu-id="53798-167">İçinde **kullanıcı tanımlayıcısı** listesi, select hello **ExtractMailPrefix()** işlevi.</span><span class="sxs-lookup"><span data-stu-id="53798-167">In **User Identifier** list, select hello **ExtractMailPrefix()** function.</span></span>

    <span data-ttu-id="53798-168">b.</span><span class="sxs-lookup"><span data-stu-id="53798-168">b.</span></span> <span data-ttu-id="53798-169">Merhaba gelen **posta** listesi, uygulamanız için kullanmak istediğiniz toouse select hello kullanıcı özniteliği.</span><span class="sxs-lookup"><span data-stu-id="53798-169">From hello **Mail** list, select hello user attribute you want toouse for your implementation.</span></span>
    <span data-ttu-id="53798-170">Örneğin, toouse hello benzersiz kullanıcı tanımlayıcısı olarak EmployeeID istiyorsanız ve hello ExtensionAttribute2 hello öznitelik değeri depoladığınız ardından user.extensionattribute2 seçin.</span><span class="sxs-lookup"><span data-stu-id="53798-170">For example, if you want toouse hello EmployeeID as unique user identifier and you have stored hello attribute value in hello ExtensionAttribute2, then select user.extensionattribute2.</span></span>  

5. <span data-ttu-id="53798-171">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="53798-171">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_certificate.png) 

6. <span data-ttu-id="53798-173">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="53798-173">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="53798-175">Merhaba üzerinde **müşteri yapılandırması için SAP bulut** 'yi tıklatın **müşteri için SAP bulut yapılandırma** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="53798-175">On hello **SAP Cloud for Customer Configuration** section, click **Configure SAP Cloud for Customer** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="53798-176">Kopya hello **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="53798-176">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_configure.png) 

8. <span data-ttu-id="53798-178">tooget yapılandırılmış, SSO hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="53798-178">tooget SSO configured, perform hello following steps:</span></span>
   
    <span data-ttu-id="53798-179">a.</span><span class="sxs-lookup"><span data-stu-id="53798-179">a.</span></span> <span data-ttu-id="53798-180">Müşteri portalı yönetici haklarıyla oturum açma SAP buluta.</span><span class="sxs-lookup"><span data-stu-id="53798-180">Login into SAP Cloud for Customer portal with administrator rights.</span></span>
   
    <span data-ttu-id="53798-181">b.</span><span class="sxs-lookup"><span data-stu-id="53798-181">b.</span></span> <span data-ttu-id="53798-182">Toohello gidin **uygulama ve kullanıcı yönetimi görevinin** hello tıklatıp **kimlik sağlayıcısı** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="53798-182">Navigate toohello **Application and User Management Common Task** and click hello **Identity Provider** tab.</span></span>
   
    <span data-ttu-id="53798-183">c.</span><span class="sxs-lookup"><span data-stu-id="53798-183">c.</span></span> <span data-ttu-id="53798-184">Tıklatın **yeni kimlik sağlayıcısı** ve select hello meta veri XML dosyası hello Azure portal ' indirilir.</span><span class="sxs-lookup"><span data-stu-id="53798-184">Click **New Identity Provider** and select hello metadata XML file you have downloaded from hello Azure portal.</span></span> <span data-ttu-id="53798-185">Merhaba meta verileri içe aktararak hello sistem otomatik olarak hello gerekli imza sertifikası ve şifreleme sertifikası karşıya yükleme.</span><span class="sxs-lookup"><span data-stu-id="53798-185">By importing hello metadata, hello system automatically uploads hello required signature certificate and encryption certificate.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_54.png)
   
    <span data-ttu-id="53798-187">d.</span><span class="sxs-lookup"><span data-stu-id="53798-187">d.</span></span> <span data-ttu-id="53798-188">Azure Active Directory hello SAML isteği onaylama tüketici hizmeti URL'si öğesinde hello gerektirir, bu nedenle hello seçin **onaylama tüketici hizmeti URL'si dahil** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="53798-188">Azure Active Directory requires hello element Assertion Consumer Service URL in hello SAML request, so select hello **Include Assertion Consumer Service URL** checkbox.</span></span>
   
    <span data-ttu-id="53798-189">e.</span><span class="sxs-lookup"><span data-stu-id="53798-189">e.</span></span> <span data-ttu-id="53798-190">Tıklatın **çoklu oturum açmayı etkinleştirme**.</span><span class="sxs-lookup"><span data-stu-id="53798-190">Click **Activate Single Sign-On**.</span></span>
   
    <span data-ttu-id="53798-191">f.</span><span class="sxs-lookup"><span data-stu-id="53798-191">f.</span></span> <span data-ttu-id="53798-192">Yaptığınız değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="53798-192">Save your changes.</span></span>
   
    <span data-ttu-id="53798-193">g.</span><span class="sxs-lookup"><span data-stu-id="53798-193">g.</span></span> <span data-ttu-id="53798-194">Merhaba tıklatın **My sistem** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="53798-194">Click hello **My System** tab.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_52.png)
   
    <span data-ttu-id="53798-196">h.</span><span class="sxs-lookup"><span data-stu-id="53798-196">h.</span></span> <span data-ttu-id="53798-197">İçinde **Azure AD oturum açma URL'si** metin kutusuna, Yapıştır **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="53798-197">In **Azure AD Sign On URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_53.png)
   
    <span data-ttu-id="53798-199">ı.</span><span class="sxs-lookup"><span data-stu-id="53798-199">i.</span></span> <span data-ttu-id="53798-200">Kullanıcı kimliği ve parola veya SSO ile Merhaba seçerek oturum açma arasında Hello çalışan el ile seçip seçemeyeceğini belirtin **el ile kimlik sağlayıcısı seçimi**.</span><span class="sxs-lookup"><span data-stu-id="53798-200">Specify whether hello employee can manually choose between logging on with user ID and password or SSO by selecting hello **Manual Identity Provider Selection**.</span></span>
   
    <span data-ttu-id="53798-201">j.</span><span class="sxs-lookup"><span data-stu-id="53798-201">j.</span></span> <span data-ttu-id="53798-202">Merhaba, **SSO URL** bölümünde, çalışanların toosign toohello sistemde tarafından kullanılması gereken hello URL'sini belirtin.</span><span class="sxs-lookup"><span data-stu-id="53798-202">In hello **SSO URL** section, specify hello URL that should be used by your employees toosign on toohello system.</span></span> 
    <span data-ttu-id="53798-203">Merhaba, **URL gönderilen tooEmployee** listesinde, aşağıdaki seçenekleri şu hello arasında seçim yapabilir:</span><span class="sxs-lookup"><span data-stu-id="53798-203">In hello **URL Sent tooEmployee** list, you can choose between hello following options:</span></span>
   
    <span data-ttu-id="53798-204">**SSO olmayan URL'si**</span><span class="sxs-lookup"><span data-stu-id="53798-204">**Non-SSO URL**</span></span>
   
    <span data-ttu-id="53798-205">Merhaba sistemi yalnızca hello normal sistem URL toohello çalışan gönderir.</span><span class="sxs-lookup"><span data-stu-id="53798-205">hello system sends only hello normal system URL toohello employee.</span></span> <span data-ttu-id="53798-206">Hello çalışan olamaz SSO kullanarak oturum açın ve parolayı kullanın veya gerekir bunun yerine sertifika.</span><span class="sxs-lookup"><span data-stu-id="53798-206">hello employee cannot log on using SSO, and must use password or certificate instead.</span></span>
   
    <span data-ttu-id="53798-207">**SSO URL'Sİ**</span><span class="sxs-lookup"><span data-stu-id="53798-207">**SSO URL**</span></span> 
   
    <span data-ttu-id="53798-208">Merhaba sistemi yalnızca hello SSO URL toohello çalışan gönderir.</span><span class="sxs-lookup"><span data-stu-id="53798-208">hello system sends only hello SSO URL toohello employee.</span></span> <span data-ttu-id="53798-209">Merhaba çalışan SSO kullanarak oturum açabilir.</span><span class="sxs-lookup"><span data-stu-id="53798-209">hello employee can log on using SSO.</span></span> <span data-ttu-id="53798-210">Kimlik doğrulama isteği IDP hello yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="53798-210">Authentication request is redirected through hello IdP.</span></span>
   
    <span data-ttu-id="53798-211">**Otomatik Seçim**</span><span class="sxs-lookup"><span data-stu-id="53798-211">**Automatic Selection**</span></span>
   
    <span data-ttu-id="53798-212">SSO etkin değilse, hello sistem hello normal sistem URL toohello çalışan gönderir.</span><span class="sxs-lookup"><span data-stu-id="53798-212">If SSO is not active, hello system sends hello normal system URL toohello employee.</span></span> <span data-ttu-id="53798-213">SSO etkin değilse, hello sistem hello çalışan bir parolaya sahip olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="53798-213">If SSO is active, hello system checks whether hello employee has a password.</span></span> <span data-ttu-id="53798-214">Bir parola kullanılabilir durumdaysa, SSO URL'si ve olmayan SSO URL'si toohello çalışan gönderilir.</span><span class="sxs-lookup"><span data-stu-id="53798-214">If a password is available, both SSO URL and Non-SSO URL are sent toohello employee.</span></span> <span data-ttu-id="53798-215">Bununla birlikte, Hello çalışan parolası yoksa, yalnızca hello SSO URL toohello çalışan gönderilir.</span><span class="sxs-lookup"><span data-stu-id="53798-215">However, if hello employee has no password, only hello SSO URL is sent toohello employee.</span></span>
   
    <span data-ttu-id="53798-216">k.</span><span class="sxs-lookup"><span data-stu-id="53798-216">k.</span></span> <span data-ttu-id="53798-217">Yaptığınız değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="53798-217">Save your changes.</span></span>

> [!TIP]
> <span data-ttu-id="53798-218">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="53798-218">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="53798-219">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="53798-219">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="53798-220">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="53798-220">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="53798-221">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="53798-221">Creating an Azure AD test user</span></span>
<span data-ttu-id="53798-222">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="53798-222">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="53798-224">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="53798-224">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="53798-225">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="53798-225">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="53798-227">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="53798-227">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="53798-229">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="53798-229">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="53798-231">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="53798-231">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="53798-233">a.</span><span class="sxs-lookup"><span data-stu-id="53798-233">a.</span></span> <span data-ttu-id="53798-234">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="53798-234">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="53798-235">b.</span><span class="sxs-lookup"><span data-stu-id="53798-235">b.</span></span> <span data-ttu-id="53798-236">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="53798-236">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="53798-237">c.</span><span class="sxs-lookup"><span data-stu-id="53798-237">c.</span></span> <span data-ttu-id="53798-238">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="53798-238">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="53798-239">d.</span><span class="sxs-lookup"><span data-stu-id="53798-239">d.</span></span> <span data-ttu-id="53798-240">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="53798-240">Click **Create**.</span></span>
 
### <a name="creating-a-sap-cloud-for-customer-test-user"></a><span data-ttu-id="53798-241">Müşteri test kullanıcısı için bir SAP bulut oluşturma</span><span class="sxs-lookup"><span data-stu-id="53798-241">Creating a SAP Cloud for Customer test user</span></span>

<span data-ttu-id="53798-242">Bu bölümde, Britta Simon SAP bulutta müşteri için adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="53798-242">In this section, you create a user called Britta Simon in SAP Cloud for Customer.</span></span> <span data-ttu-id="53798-243">Lütfen çalışmak [müşteri destek ekibi için SAP bulut](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) hello SAP bulut müşteri platform için tooadd hello kullanıcılar.</span><span class="sxs-lookup"><span data-stu-id="53798-243">Please work with [SAP Cloud for Customer support team](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) tooadd hello users in hello SAP Cloud for Customer platform.</span></span> 

> [!NOTE]
> <span data-ttu-id="53798-244">Lütfen NameID değeri hello SAP bulut müşteri platform için hello kullanıcıadı alanıyla eşleşmelidir emin olun.</span><span class="sxs-lookup"><span data-stu-id="53798-244">Please make sure that NameID value should match with hello username field in hello SAP Cloud for Customer platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="53798-245">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="53798-245">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="53798-246">Bu bölümde, müşteri için erişim tooSAP bulut vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="53798-246">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSAP Cloud for Customer.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="53798-248">**tooassign Britta Simon tooSAP müşteri için bulut hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="53798-248">**tooassign Britta Simon tooSAP Cloud for Customer, perform hello following steps:**</span></span>

1. <span data-ttu-id="53798-249">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="53798-249">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="53798-251">Merhaba uygulamalar listesinde **müşteri için SAP bulut**.</span><span class="sxs-lookup"><span data-stu-id="53798-251">In hello applications list, select **SAP Cloud for Customer**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_app.png) 

3. <span data-ttu-id="53798-253">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="53798-253">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="53798-255">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="53798-255">Click **Add** button.</span></span> <span data-ttu-id="53798-256">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="53798-256">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="53798-258">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="53798-258">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="53798-259">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="53798-259">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="53798-260">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="53798-260">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="53798-261">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="53798-261">Testing single sign-on</span></span>

<span data-ttu-id="53798-262">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="53798-262">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="53798-263">Merhaba SAP bulut hello erişim paneli müşteri parçasında tıkladığınızda, müşteri uygulaması için otomatik olarak imzalanmış üzerinde SAP bulut tooyour almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="53798-263">When you click hello SAP Cloud for Customer tile in hello Access Panel, you should get automatically signed-on tooyour SAP Cloud for Customer application.</span></span>
<span data-ttu-id="53798-264">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="53798-264">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="53798-265">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="53798-265">Additional resources</span></span>

* [<span data-ttu-id="53798-266">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="53798-266">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="53798-267">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="53798-267">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_203.png

