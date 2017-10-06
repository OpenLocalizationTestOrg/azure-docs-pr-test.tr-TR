---
title: "Öğretici: SAP HANA Azure Active Directory Tümleştirme | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve SAP HANA arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: cef4a146-f4b0-4e94-82de-f5227a4b462c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 5ff6bfde0b1d7ab14025a4bc45199f9f826affd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana"></a><span data-ttu-id="8fc6f-103">Öğretici: SAP HANA Azure Active Directory Tümleştirme</span><span class="sxs-lookup"><span data-stu-id="8fc6f-103">Tutorial: Azure Active Directory integration with SAP HANA</span></span>

<span data-ttu-id="8fc6f-104">Bu öğreticide, nasıl toointegrate SAP öğrenin HANA Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8fc6f-104">In this tutorial, you learn how toointegrate SAP HANA with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8fc6f-105">SAP HANA Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="8fc6f-105">Integrating SAP HANA with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8fc6f-106">Erişim tooSAP HANA sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="8fc6f-106">You can control in Azure AD who has access tooSAP HANA</span></span>
- <span data-ttu-id="8fc6f-107">Kullanıcıların tooautomatically get açan tooSAP HANA (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="8fc6f-107">You can enable your users tooautomatically get signed-on tooSAP HANA (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8fc6f-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="8fc6f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8fc6f-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8fc6f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8fc6f-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="8fc6f-110">Prerequisites</span></span>

<span data-ttu-id="8fc6f-111">SAP HANA ile Azure AD tümleştirme tooconfigure, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="8fc6f-111">tooconfigure Azure AD integration with SAP HANA, you need hello following items:</span></span>

- <span data-ttu-id="8fc6f-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="8fc6f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8fc6f-113">Bir SAP HANA çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="8fc6f-113">A SAP HANA single sign-on enabled subscription</span></span>
- <span data-ttu-id="8fc6f-114">Çalışan HANA örneği üzerinde herhangi bir ortak Iaas, şirket içi ya da Azure VM'ler veya Azure SAP büyük örnekleri</span><span class="sxs-lookup"><span data-stu-id="8fc6f-114">A running HANA Instance either on any public IaaS, on-premises, Azure VMs or SAP Large Instances in Azure</span></span>
- <span data-ttu-id="8fc6f-115">Merhaba XSA Yönetim Web arabirimi yanı sıra HANA Studio hello HANA örnek üzerinde yüklü.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-115">hello XSA Administration Web Interface as well as HANA Studio installed on hello HANA instance.</span></span>

> [!NOTE]
> <span data-ttu-id="8fc6f-116">tootest hello bu öğreticideki adımlar, bir üretim ortamında, SAP HANA kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-116">tootest hello steps in this tutorial, we do not recommend using a production environment of SAP HANA.</span></span> <span data-ttu-id="8fc6f-117">Merhaba tümleştirme ilk geliştirme veya hazırlama ortamı hello uygulamasının ve kullanım hello üretim ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-117">Test hello integration first in development or staging environment of hello application and then use hello production environment.</span></span>

<span data-ttu-id="8fc6f-118">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="8fc6f-118">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8fc6f-119">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-119">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8fc6f-120">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8fc6f-120">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8fc6f-121">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="8fc6f-121">Scenario description</span></span>
<span data-ttu-id="8fc6f-122">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-122">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8fc6f-123">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="8fc6f-123">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8fc6f-124">SAP HANA hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="8fc6f-124">Adding SAP HANA from hello gallery</span></span>
2. <span data-ttu-id="8fc6f-125">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="8fc6f-125">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-hana-from-hello-gallery"></a><span data-ttu-id="8fc6f-126">SAP HANA hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="8fc6f-126">Adding SAP HANA from hello gallery</span></span>
<span data-ttu-id="8fc6f-127">Azure AD'ye tooconfigure hello tümleştirme, SAP HANA tooadd SAP HANA hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-127">tooconfigure hello integration of SAP HANA into Azure AD, you need tooadd SAP HANA from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8fc6f-128">**SAP HANA hello galerisinden tooadd hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="8fc6f-128">**tooadd SAP HANA from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8fc6f-129">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-129">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory düğmesi][1]

2. <span data-ttu-id="8fc6f-131">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-131">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8fc6f-132">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-132">Then go too**All applications**.</span></span>

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="8fc6f-134">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-134">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Merhaba yeni uygulama düğmesi][3]

4. <span data-ttu-id="8fc6f-136">Merhaba arama kutusuna yazın **SAP HANA**seçin **SAP HANA** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-136">In hello search box, type **SAP HANA**, select **SAP HANA** from result panel then click **Add** button tooadd hello application.</span></span> 

    ![Merhaba yeni uygulama](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8fc6f-138">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="8fc6f-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8fc6f-139">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı SAP HANA ile test etme</span><span class="sxs-lookup"><span data-stu-id="8fc6f-139">In this section, you configure and test Azure AD single sign-on with SAP HANA based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8fc6f-140">Tek toowork'ın oturum açma hangi hello karşılık gelen SAP HANA içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SAP HANA is tooa user in Azure AD.</span></span> <span data-ttu-id="8fc6f-141">Diğer bir deyişle, bir Azure AD kullanıcısının ve SAP HANA hello ilgili kullanıcı arasındaki bağlantıyı ilişki kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-141">In other words, a link relationship between an Azure AD user and hello related user in SAP HANA needs toobe established.</span></span>

<span data-ttu-id="8fc6f-142">SAP HANA içinde hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-142">In SAP HANA, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8fc6f-143">tooconfigure ve SAP HANA ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="8fc6f-143">tooconfigure and test Azure AD single sign-on with SAP HANA, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8fc6f-144">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8fc6f-145">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8fc6f-146">**[SAP HANA test kullanıcısı oluşturma](#creating-a-sap-hana-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir SAP HANA içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-146">**[Creating a SAP HANA test user](#creating-a-sap-hana-test-user)** - toohave a counterpart of Britta Simon in SAP HANA that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8fc6f-147">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8fc6f-148">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8fc6f-149">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="8fc6f-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8fc6f-150">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma, SAP HANA uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SAP HANA application.</span></span>

<span data-ttu-id="8fc6f-151">**tooconfigure Azure AD çoklu oturum açma SAP HANA ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="8fc6f-151">**tooconfigure Azure AD single sign-on with SAP HANA, perform hello following steps:**</span></span>

1. <span data-ttu-id="8fc6f-152">Hello hello üzerinde Azure portal'ın **SAP HANA** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-152">In hello Azure portal, on hello **SAP HANA** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="8fc6f-154">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_samlbase.png)

3. <span data-ttu-id="8fc6f-156">Merhaba üzerinde **SAP HANA etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="8fc6f-156">On hello **SAP HANA Domain and URLs** section, perform hello following steps:</span></span>

    ![Etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_url.png)

    <span data-ttu-id="8fc6f-158">a.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-158">a.</span></span> <span data-ttu-id="8fc6f-159">Merhaba, **tanımlayıcısı** metin kutusuna, türü olarak:`HA100`</span><span class="sxs-lookup"><span data-stu-id="8fc6f-159">In hello **Identifier** textbox, type as: `HA100`</span></span> 

    <span data-ttu-id="8fc6f-160">b.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-160">b.</span></span> <span data-ttu-id="8fc6f-161">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<Customer-SAP-instance-url>/sap/hana/xs/saml/login.xscfunc`</span><span class="sxs-lookup"><span data-stu-id="8fc6f-161">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<Customer-SAP-instance-url>/sap/hana/xs/saml/login.xscfunc`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8fc6f-162">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-162">These values are not real.</span></span> <span data-ttu-id="8fc6f-163">Bu değerleri hello gerçek tanımlayıcısı ve yanıt URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-163">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="8fc6f-164">Kişi [SAP HANA istemci destek ekibi](https://cloudplatform.sap.com/contact.html) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-164">Contact [SAP HANA Client support team](https://cloudplatform.sap.com/contact.html) tooget these values.</span></span> 

4. <span data-ttu-id="8fc6f-165">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_certificate.png) 

    >[!Note]
    ><span data-ttu-id="8fc6f-167">Sertifika etkin değilse, ardından active hello tıklayarak "Yapma yeni sertifika etkin" onay kutusunu hello Azure AD kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-167">If certificate is not active then make it active by clicking hello “Make new certificate active” checkbox in hello Azure AD.</span></span> 

5. <span data-ttu-id="8fc6f-168">SAP HANA uygulama hello SAML onaylar belirli bir biçimde bekler.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-168">SAP HANA application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="8fc6f-169">Ekran aşağıdaki hello bunun bir örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-169">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="8fc6f-170">Burada size hello eşledikten **kullanıcı tanımlayıcısı** ile **ExtractMailPrefix()** işlevinin **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-170">Here we have mapped hello **User Identifier** with **ExtractMailPrefix()** function of **user.mail**.</span></span> <span data-ttu-id="8fc6f-171">Bu e-posta benzersiz kullanıcı kimliği hello hello kullanıcının hello önek değeri verir</span><span class="sxs-lookup"><span data-stu-id="8fc6f-171">This gives hello prefix value of email of hello user which is hello unique User ID.</span></span> <span data-ttu-id="8fc6f-172">Bu toohello SAP HANA uygulama her başarılı yanıt olarak gönderilir.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-172">This is sent toohello SAP HANA application in every successful response.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-saphana-tutorial/attribute.png)

6. <span data-ttu-id="8fc6f-174">Merhaba, **kullanıcı öznitelikleri** hello bölüm **çoklu oturum açma** iletişim:</span><span class="sxs-lookup"><span data-stu-id="8fc6f-174">In hello **User Attributes** section on hello **Single sign-on** dialog:</span></span>

    <span data-ttu-id="8fc6f-175">a.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-175">a.</span></span> <span data-ttu-id="8fc6f-176">Merhaba, **kullanıcı tanımlayıcısı** açılır listesinden, **ExtractMailPrefix**.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-176">In hello **User Identifier** dropdown list, select **ExtractMailPrefix**.</span></span>
    
    <span data-ttu-id="8fc6f-177">b.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-177">b.</span></span> <span data-ttu-id="8fc6f-178">Merhaba, **posta** açılır listesinden, **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-178">In hello **Mail** dropdown list, select **user.mail**.</span></span>

7. <span data-ttu-id="8fc6f-179">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-179">Click **Save** button.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-saphana-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="8fc6f-181">tooconfigure çoklu oturum açma üzerinde **SAP HANA** tarafı, oturum açma tooyour **HANA XSA Web Konsolu** toohello giderek ilgili HTTPS uç noktası.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-181">tooconfigure single sign-on on **SAP HANA** side, login tooyour **HANA XSA Web Console**  by browsing toohello respective HTTPS-endpoint.</span></span>

    > [!Note]
    > <span data-ttu-id="8fc6f-182">Merhaba varsayılan yapılandırmasında bir kimliği doğrulanmış SAP HANA veritabanına kullanıcı toocomplete hello oturum açma işleminin hello kimlik bilgileri gerektiren hello isteği tooa oturum açma ekranı hello URL yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-182">In hello default configuration, hello URL redirects hello request tooa logon screen, which requires hello credentials of an authenticated SAP HANA database user toocomplete hello logon process.</span></span> <span data-ttu-id="8fc6f-183">oturum açan hello kullanıcı hello ayrıcalıkları gerekli tooperform SAML yönetim görevlerini olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-183">hello user who logs on must have hello privileges required tooperform SAML administration tasks.</span></span>

9. <span data-ttu-id="8fc6f-184">Hello XSA Web arabirimi, çok gidin**SAML kimlik sağlayıcısı** tıklatıp buradan hello **"+"** -düğmesini hello bölmesinin Merhaba ekranında toodisplay hello kimlik sağlayıcısı bilgisi Ekle üzerinde ve gerçekleştirin Aşağıdaki adımları hello:</span><span class="sxs-lookup"><span data-stu-id="8fc6f-184">In hello XSA Web Interface, navigate too**SAML Identity Provider** and from there, click hello **“+”** -button on hello bottom of hello screen toodisplay hello Add Identity Provider Info pane and perform hello following steps:</span></span>

    ![Kimlik sağlayıcısı ekleyin](./media/active-directory-saas-saphana-tutorial/sap1.png)

    <span data-ttu-id="8fc6f-186">a.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-186">a.</span></span> <span data-ttu-id="8fc6f-187">Merhaba, **kimlik sağlayıcısı bilgisi Ekle** bölmesinde, Yapıştır hello hello hello Azure Portalı'ndan indirilen meta veri XML içeriğini **meta veri** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-187">In hello **Add Identity Provider Info** pane, paste hello contents of hello Metadata XML, which you have downloaded from Azure portal into hello **Metadata** textbox.</span></span>

    ![Kimlik sağlayıcı ayarları ekleme](./media/active-directory-saas-saphana-tutorial/sap2.png)

    <span data-ttu-id="8fc6f-189">b.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-189">b.</span></span> <span data-ttu-id="8fc6f-190">Merhaba hello XML belgesinin içeriğini geçerliyse, işlem ayrıştırma hello hello gerekli bilgileri tooinsert hello ayıklar. **konu, varlık kimliği ve sertifikayı veren** hello genel veri alanlarında ekran alanı ve hello URL alanlarında hello Hedef ekran alanı, örneğin,  **taban URL ve SingleSignOn URL (*)**.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-190">If hello contents of hello XML document are valid, hello parsing process extracts hello information required tooinsert into hello **Subject, Entity ID, and Issuer** fields in hello General Data screen area, and hello URL fields in hello Destination screen area, for example, **Base URL and SingleSignOn URL (*)**.</span></span>

    ![Kimlik sağlayıcı ayarları ekleme](./media/active-directory-saas-saphana-tutorial/sap3.png)

    <span data-ttu-id="8fc6f-192">c.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-192">c.</span></span> <span data-ttu-id="8fc6f-193">Merhaba adı kutusuna hello genel veri alanı ekranında, hello yeni SAML SSO kimlik sağlayıcısı için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-193">In hello Name box of hello General Data screen area, enter a name for hello new SAML SSO identity provider.</span></span>

    > [!Note]
    > <span data-ttu-id="8fc6f-194">Merhaba SAML IDP Hello adı zorunludur ve benzersiz olmalıdır; SAML SAP HANA XS uygulamaları toouse hello kimlik doğrulama yöntemi olarak Örneğin, Itanium tabanlı sistemler için hello kimlik doğrulaması ekran alanı hello XS yapı Yönetim Aracı'nda seçerseniz hello görüntülenir, kullanılabilir SAML IDPs listesinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-194">hello name of hello SAML IDP is mandatory and must be unique; it appears in hello list of available SAML IDPs that is displayed, if you select SAML as hello authentication method for SAP HANA XS applications toouse, for example, in hello Authentication screen area of hello XS Artifact Administration tool.</span></span>

10. <span data-ttu-id="8fc6f-195">Merhaba yeni SAML kimlik sağlayıcısı Hello ayrıntılarını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-195">Save hello details of hello new SAML identity provider.</span></span> <span data-ttu-id="8fc6f-196">Seçin **kaydetmek** toosave hello hello SAML kimlik sağlayıcısı ayrıntılarını ve hello yeni SAML IDP toohello listesi bilinen SAML IDPs ekleyin.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-196">Choose **Save** toosave hello details of hello SAML identity provider and add hello new SAML IDP toohello list of known SAML IDPs.</span></span>

    ![Kaydet düğmesi](./media/active-directory-saas-saphana-tutorial/sap4.png)

11. <span data-ttu-id="8fc6f-198">Merhaba hello sistem özelliklerini içinde HANA Studio'da **yapılandırma** sekmesinde, yalnızca ayarlarına göre filtre **saml** ve hello ayarlamak **assertion_timeout** gelen**10 sn** çok**120 saniye**.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-198">In HANA Studio within hello system properties of hello **Configuration** tab, just filter settings by **saml** and adjust hello **assertion_timeout** from **10 sec** too**120 sec**.</span></span>

    ![assertion_timeout ayarı](./media/active-directory-saas-saphana-tutorial/sap7.png)

> [!TIP]
> <span data-ttu-id="8fc6f-200">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="8fc6f-200">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8fc6f-201">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-201">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8fc6f-202">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8fc6f-202">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8fc6f-203">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="8fc6f-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="8fc6f-204">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-204">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="8fc6f-206">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="8fc6f-206">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8fc6f-207">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-207">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-saphana-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8fc6f-209">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-209">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-saphana-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8fc6f-211">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-211">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Merhaba Ekle düğmesi](./media/active-directory-saas-saphana-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8fc6f-213">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="8fc6f-213">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-saphana-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8fc6f-215">a.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-215">a.</span></span> <span data-ttu-id="8fc6f-216">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-216">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8fc6f-217">b.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-217">b.</span></span> <span data-ttu-id="8fc6f-218">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-218">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8fc6f-219">c.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-219">c.</span></span> <span data-ttu-id="8fc6f-220">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-220">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8fc6f-221">d.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-221">d.</span></span> <span data-ttu-id="8fc6f-222">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-222">Click **Create**.</span></span>
 
### <a name="creating-a-sap-hana-test-user"></a><span data-ttu-id="8fc6f-223">SAP HANA test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="8fc6f-223">Creating a SAP HANA test user</span></span>

<span data-ttu-id="8fc6f-224">tooenable Azure AD kullanıcıların toolog tooSAP HANA'da, bunlar SAP HANA sağlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-224">tooenable Azure AD users toolog in tooSAP HANA, they must be provisioned into SAP HANA.</span></span>
<span data-ttu-id="8fc6f-225">SAP HANA tam zamanı sağlama, varsayılan olarak etkin olduğu destekler.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-225">SAP HANA supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="8fc6f-226">Bir kullanıcı toocreate el ile gerekiyorsa, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="8fc6f-226">If you need toocreate a user manually, perform hello following steps:</span></span>

>[!Note]
><span data-ttu-id="8fc6f-227">Merhaba kullanıcı tarafından kullanılan hello Dış kimlik doğrulama değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-227">You can change hello external authentication used by hello user.</span></span>
<span data-ttu-id="8fc6f-228">Dış kullanıcılar, örneğin Kerberos sistem bir dış sistem kullanılarak doğrulanır.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-228">External users are authenticated using an external system, for example a Kerberos system.</span></span> <span data-ttu-id="8fc6f-229">Dış kimlikler hakkında ayrıntılı bilgi için kişi, [etki alanı yöneticisi](https://cloudplatform.sap.com/contact.html).</span><span class="sxs-lookup"><span data-stu-id="8fc6f-229">For detailed information about external identities, contact your [domain administrator](https://cloudplatform.sap.com/contact.html).</span></span>

1. <span data-ttu-id="8fc6f-230">Açık hello [SAP HANA Studio](https://help.sap.com/viewer/a2a49126a5c546a9864aae22c05c3d0e/2.0.01/en-us) bir Yöneticiyseniz ve etkinleştir DB kullanıcı SAML SSO için hello gibi.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-230">Open hello [SAP HANA Studio](https://help.sap.com/viewer/a2a49126a5c546a9864aae22c05c3d0e/2.0.01/en-us) as an administrator and enable hello DB-User for SAML SSO.</span></span>

    ![Kullanıcı oluştur](./media/active-directory-saas-saphana-tutorial/sap5.png)

2. <span data-ttu-id="8fc6f-232">Değer çizgilerinin hello görünmez onay kutusunu toohello sol üst **SAML** ve hello Yapılandır bağlantısını izleyin.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-232">Tick hello invisible checkbox toohello left of **SAML** and follow hello Configure link.</span></span>

3. <span data-ttu-id="8fc6f-233">Tıklatın **Ekle** tooadd SAML IDP hello ve tıklayın **Tamam** hello uygun SAML IDP seçme.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-233">Click **Add** tooadd hello SAML IDP and click **OK** selecting hello appropriate SAML IDP.</span></span>

4. <span data-ttu-id="8fc6f-234">Merhaba eklemek **Dış kimlik** (örneğin.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-234">Add hello **External Identity** (ex.</span></span> <span data-ttu-id="8fc6f-235">Burada BrittaSimon) veya seçin **"Tüm"** tıklatıp **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-235">BrittaSimon here) or choose **"Any"** and click **OK**.</span></span>

    >[!Note]
    ><span data-ttu-id="8fc6f-236">"Tüm" onay kutusu işaretli sonra HANA hello kullanıcı adı gerekiyor tooexactly eşleşme hello hello UPN hello etki alanı soneki önce hello kullanıcı adını (yani BrittaSimon@contoso.com HANA BrittaSimon olur).</span><span class="sxs-lookup"><span data-stu-id="8fc6f-236">If "ANY" check-box is not checked, then hello user name in HANA needs tooexactly match hello name of hello user in hello UPN before hello domain suffix (i.e. BrittaSimon@contoso.com would become BrittaSimon in HANA).</span></span>

5. <span data-ttu-id="8fc6f-237">Test amacıyla, tüm Ata **"XS"** rolleri toohello kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-237">For testing purposes, assign all **"XS"** roles toohello user.</span></span>

    ![rol atama](./media/active-directory-saas-saphana-tutorial/sap6.png)

    > [!TIP]
    > <span data-ttu-id="8fc6f-239">Bu, kullanım örnekleri için yalnızca uygun izinleri vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-239">You should give those permissions appropriate for your use cases, only.</span></span>

6. <span data-ttu-id="8fc6f-240">Merhaba kullanıcı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-240">Save hello user.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8fc6f-241">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="8fc6f-241">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8fc6f-242">Bu bölümde, erişim tooSAP HANA vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-242">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSAP HANA.</span></span>

![Merhaba kullanıcı rolü atayın][200] 

<span data-ttu-id="8fc6f-244">**tooassign Britta Simon tooSAP HANA, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="8fc6f-244">**tooassign Britta Simon tooSAP HANA, perform hello following steps:**</span></span>

1. <span data-ttu-id="8fc6f-245">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-245">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="8fc6f-247">Merhaba uygulamalar listesinde **SAP HANA**.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-247">In hello applications list, select **SAP HANA**.</span></span>

    ![Kullanıcı atama](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_app.png) 

3. <span data-ttu-id="8fc6f-249">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-249">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202] 

4. <span data-ttu-id="8fc6f-251">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-251">Click **Add** button.</span></span> <span data-ttu-id="8fc6f-252">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Merhaba eklemek atama bölmesi][203]

5. <span data-ttu-id="8fc6f-254">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-254">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8fc6f-255">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8fc6f-256">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8fc6f-257">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="8fc6f-257">Testing single sign-on</span></span>

<span data-ttu-id="8fc6f-258">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-258">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8fc6f-259">Merhaba SAP HANA hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour SAP HANA uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8fc6f-259">When you click hello SAP HANA tile in hello Access Panel, you should get automatically signed-on tooyour SAP HANA application.</span></span>
<span data-ttu-id="8fc6f-260">Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8fc6f-260">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8fc6f-261">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="8fc6f-261">Additional resources</span></span>

* [<span data-ttu-id="8fc6f-262">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="8fc6f-262">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8fc6f-263">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="8fc6f-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_203.png

