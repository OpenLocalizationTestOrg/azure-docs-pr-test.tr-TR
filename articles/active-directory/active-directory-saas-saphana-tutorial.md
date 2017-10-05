---
title: "Öğretici: SAP HANA Azure Active Directory Tümleştirme | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ve SAP HANA arasında yapılandırmayı öğrenin."
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
ms.openlocfilehash: a7e73f6ee763d1005ad85935cf2d8f6b24ecf116
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana"></a><span data-ttu-id="58bdb-103">Öğretici: SAP HANA Azure Active Directory Tümleştirme</span><span class="sxs-lookup"><span data-stu-id="58bdb-103">Tutorial: Azure Active Directory integration with SAP HANA</span></span>

<span data-ttu-id="58bdb-104">Bu öğreticide, Azure Active Directory (Azure AD) ile SAP HANA tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="58bdb-104">In this tutorial, you learn how to integrate SAP HANA with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="58bdb-105">SAP HANA Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="58bdb-105">Integrating SAP HANA with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="58bdb-106">SAP HANA erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="58bdb-106">You can control in Azure AD who has access to SAP HANA</span></span>
- <span data-ttu-id="58bdb-107">Azure AD hesaplarına otomatik olarak (çoklu oturum açma) için SAP HANA açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="58bdb-107">You can enable your users to automatically get signed-on to SAP HANA (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="58bdb-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="58bdb-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="58bdb-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="58bdb-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="58bdb-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="58bdb-110">Prerequisites</span></span>

<span data-ttu-id="58bdb-111">SAP HANA ile Azure AD tümleştirme yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="58bdb-111">To configure Azure AD integration with SAP HANA, you need the following items:</span></span>

- <span data-ttu-id="58bdb-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="58bdb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="58bdb-113">Bir SAP HANA çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="58bdb-113">A SAP HANA single sign-on enabled subscription</span></span>
- <span data-ttu-id="58bdb-114">Çalışan HANA örneği üzerinde herhangi bir ortak Iaas, şirket içi ya da Azure VM'ler veya Azure SAP büyük örnekleri</span><span class="sxs-lookup"><span data-stu-id="58bdb-114">A running HANA Instance either on any public IaaS, on-premises, Azure VMs or SAP Large Instances in Azure</span></span>
- <span data-ttu-id="58bdb-115">XSA Yönetim Web arabirimi yanı sıra HANA Studio HANA örnek üzerinde yüklü.</span><span class="sxs-lookup"><span data-stu-id="58bdb-115">The XSA Administration Web Interface as well as HANA Studio installed on the HANA instance.</span></span>

> [!NOTE]
> <span data-ttu-id="58bdb-116">Bu öğreticide adımları test etmek için bir üretim ortamında, SAP HANA kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="58bdb-116">To test the steps in this tutorial, we do not recommend using a production environment of SAP HANA.</span></span> <span data-ttu-id="58bdb-117">Geliştirme veya uygulamanın hazırlama ortamında tümleştirme önce test ve üretim ortamına kullanın.</span><span class="sxs-lookup"><span data-stu-id="58bdb-117">Test the integration first in development or staging environment of the application and then use the production environment.</span></span>

<span data-ttu-id="58bdb-118">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="58bdb-118">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="58bdb-119">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="58bdb-119">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="58bdb-120">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="58bdb-120">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="58bdb-121">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="58bdb-121">Scenario description</span></span>
<span data-ttu-id="58bdb-122">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="58bdb-122">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="58bdb-123">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="58bdb-123">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="58bdb-124">SAP HANA Galeriden ekleme</span><span class="sxs-lookup"><span data-stu-id="58bdb-124">Adding SAP HANA from the gallery</span></span>
2. <span data-ttu-id="58bdb-125">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="58bdb-125">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-hana-from-the-gallery"></a><span data-ttu-id="58bdb-126">SAP HANA Galeriden ekleme</span><span class="sxs-lookup"><span data-stu-id="58bdb-126">Adding SAP HANA from the gallery</span></span>
<span data-ttu-id="58bdb-127">SAP HANA tümleştirme Azure AD'ye yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden SAP HANA eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="58bdb-127">To configure the integration of SAP HANA into Azure AD, you need to add SAP HANA from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="58bdb-128">**SAP HANA Galeriden eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="58bdb-128">**To add SAP HANA from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="58bdb-129">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="58bdb-129">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory düğmesi][1]

2. <span data-ttu-id="58bdb-131">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="58bdb-131">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="58bdb-132">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="58bdb-132">Then go to **All applications**.</span></span>

    ![Kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="58bdb-134">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="58bdb-134">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Yeni Uygulama düğmesi][3]

4. <span data-ttu-id="58bdb-136">Arama kutusuna **SAP HANA**seçin **SAP HANA** sonuç panelinden ardından **Ekle** uygulama eklemek için düğmeyi.</span><span class="sxs-lookup"><span data-stu-id="58bdb-136">In the search box, type **SAP HANA**, select **SAP HANA** from result panel then click **Add** button to add the application.</span></span> 

    ![Yeni uygulama](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="58bdb-138">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="58bdb-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="58bdb-139">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı SAP HANA ile test etme</span><span class="sxs-lookup"><span data-stu-id="58bdb-139">In this section, you configure and test Azure AD single sign-on with SAP HANA based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="58bdb-140">Tekli çalışmaya oturum için Azure AD SAP HANA karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="58bdb-140">For single sign-on to work, Azure AD needs to know what the counterpart user in SAP HANA is to a user in Azure AD.</span></span> <span data-ttu-id="58bdb-141">Diğer bir deyişle, bir Azure AD kullanıcısının SAP HANA ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="58bdb-141">In other words, a link relationship between an Azure AD user and the related user in SAP HANA needs to be established.</span></span>

<span data-ttu-id="58bdb-142">SAP HANA içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="58bdb-142">In SAP HANA, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="58bdb-143">Yapılandırma ve Azure AD çoklu oturum açma SAP HANA ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="58bdb-143">To configure and test Azure AD single sign-on with SAP HANA, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="58bdb-144">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="58bdb-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="58bdb-145">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="58bdb-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="58bdb-146">**[SAP HANA test kullanıcısı oluşturma](#creating-a-sap-hana-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı SAP HANA sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="58bdb-146">**[Creating a SAP HANA test user](#creating-a-sap-hana-test-user)** - to have a counterpart of Britta Simon in SAP HANA that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="58bdb-147">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="58bdb-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="58bdb-148">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="58bdb-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="58bdb-149">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="58bdb-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="58bdb-150">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma, SAP HANA uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="58bdb-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SAP HANA application.</span></span>

<span data-ttu-id="58bdb-151">**Azure AD çoklu oturum açma ile SAP HANA yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="58bdb-151">**To configure Azure AD single sign-on with SAP HANA, perform the following steps:**</span></span>

1. <span data-ttu-id="58bdb-152">Azure portalında üzerinde **SAP HANA** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="58bdb-152">In the Azure portal, on the **SAP HANA** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="58bdb-154">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="58bdb-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_samlbase.png)

3. <span data-ttu-id="58bdb-156">Üzerinde **SAP HANA etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="58bdb-156">On the **SAP HANA Domain and URLs** section, perform the following steps:</span></span>

    ![Etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_url.png)

    <span data-ttu-id="58bdb-158">a.</span><span class="sxs-lookup"><span data-stu-id="58bdb-158">a.</span></span> <span data-ttu-id="58bdb-159">İçinde **tanımlayıcısı** metin kutusuna, türü olarak:`HA100`</span><span class="sxs-lookup"><span data-stu-id="58bdb-159">In the **Identifier** textbox, type as: `HA100`</span></span> 

    <span data-ttu-id="58bdb-160">b.</span><span class="sxs-lookup"><span data-stu-id="58bdb-160">b.</span></span> <span data-ttu-id="58bdb-161">İçinde **yanıt URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<Customer-SAP-instance-url>/sap/hana/xs/saml/login.xscfunc`</span><span class="sxs-lookup"><span data-stu-id="58bdb-161">In the **Reply URL** textbox, type a URL using the following pattern: `https://<Customer-SAP-instance-url>/sap/hana/xs/saml/login.xscfunc`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="58bdb-162">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="58bdb-162">These values are not real.</span></span> <span data-ttu-id="58bdb-163">Bu değerler gerçek tanımlayıcısı ve yanıt URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="58bdb-163">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="58bdb-164">Kişi [SAP HANA istemci destek ekibi](https://cloudplatform.sap.com/contact.html) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="58bdb-164">Contact [SAP HANA Client support team](https://cloudplatform.sap.com/contact.html) to get these values.</span></span> 

4. <span data-ttu-id="58bdb-165">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="58bdb-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Sertifika indirme bağlantısı](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_certificate.png) 

    >[!Note]
    ><span data-ttu-id="58bdb-167">Sertifika etkin değilse, ardından onu Azure AD içinde "Yeni sertifikayı etkinleştirmek" onay kutusunu tıklatarak etkin hale getirin.</span><span class="sxs-lookup"><span data-stu-id="58bdb-167">If certificate is not active then make it active by clicking the “Make new certificate active” checkbox in the Azure AD.</span></span> 

5. <span data-ttu-id="58bdb-168">SAP HANA uygulaması SAML onaylar belirli bir biçimde bekliyor.</span><span class="sxs-lookup"><span data-stu-id="58bdb-168">SAP HANA application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="58bdb-169">Aşağıdaki ekran görüntüsünde bunun bir örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="58bdb-169">The following screenshot shows an example for this.</span></span> <span data-ttu-id="58bdb-170">Biz burada eşledikten **kullanıcı tanımlayıcısı** ile **ExtractMailPrefix()** işlevinin **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="58bdb-170">Here we have mapped the **User Identifier** with **ExtractMailPrefix()** function of **user.mail**.</span></span> <span data-ttu-id="58bdb-171">Bu e-posta benzersiz kullanıcı kimliği olan kullanıcının önek değeri verir</span><span class="sxs-lookup"><span data-stu-id="58bdb-171">This gives the prefix value of email of the user which is the unique User ID.</span></span> <span data-ttu-id="58bdb-172">Bu, her başarılı yanıt SAP HANA uygulamaya gönderilir.</span><span class="sxs-lookup"><span data-stu-id="58bdb-172">This is sent to the SAP HANA application in every successful response.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-saphana-tutorial/attribute.png)

6. <span data-ttu-id="58bdb-174">İçinde **kullanıcı öznitelikleri** bölümünde **çoklu oturum açma** iletişim:</span><span class="sxs-lookup"><span data-stu-id="58bdb-174">In the **User Attributes** section on the **Single sign-on** dialog:</span></span>

    <span data-ttu-id="58bdb-175">a.</span><span class="sxs-lookup"><span data-stu-id="58bdb-175">a.</span></span> <span data-ttu-id="58bdb-176">İçinde **kullanıcı tanımlayıcısı** açılır listesinden, **ExtractMailPrefix**.</span><span class="sxs-lookup"><span data-stu-id="58bdb-176">In the **User Identifier** dropdown list, select **ExtractMailPrefix**.</span></span>
    
    <span data-ttu-id="58bdb-177">b.</span><span class="sxs-lookup"><span data-stu-id="58bdb-177">b.</span></span> <span data-ttu-id="58bdb-178">İçinde **posta** açılır listesinden, **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="58bdb-178">In the **Mail** dropdown list, select **user.mail**.</span></span>

7. <span data-ttu-id="58bdb-179">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="58bdb-179">Click **Save** button.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-saphana-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="58bdb-181">Çoklu oturum açma yapılandırmak için **SAP HANA** tarafı, oturum açma için sizin **HANA XSA Web Konsolu** ilgili HTTPS uç noktasına giderek.</span><span class="sxs-lookup"><span data-stu-id="58bdb-181">To configure single sign-on on **SAP HANA** side, login to your **HANA XSA Web Console**  by browsing to the respective HTTPS-endpoint.</span></span>

    > [!Note]
    > <span data-ttu-id="58bdb-182">Varsayılan yapılandırmasında, istek oturum açma işlemini tamamlamak için kimliği doğrulanmış bir SAP HANA veritabanına kullanıcı kimlik bilgileri gerektiren bir oturum açma ekranına yeniden yönlendirildiği URL.</span><span class="sxs-lookup"><span data-stu-id="58bdb-182">In the default configuration, the URL redirects the request to a logon screen, which requires the credentials of an authenticated SAP HANA database user to complete the logon process.</span></span> <span data-ttu-id="58bdb-183">Oturum açan kullanıcının SAML yönetim görevlerini gerçekleştirmek için gereken izinleri olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="58bdb-183">The user who logs on must have the privileges required to perform SAML administration tasks.</span></span>

9. <span data-ttu-id="58bdb-184">XSA Web arabirimi gidin **SAML kimlik sağlayıcısı** buradan tıklatıp **"+"** -kimlik sağlayıcısı bilgisi Ekle bölmesinde görüntülemek ve aşağıdakileri yapmak için ekranın düğmesine adımlar:</span><span class="sxs-lookup"><span data-stu-id="58bdb-184">In the XSA Web Interface, navigate to **SAML Identity Provider** and from there, click the **“+”** -button on the bottom of the screen to display the Add Identity Provider Info pane and perform the following steps:</span></span>

    ![Kimlik sağlayıcısı ekleyin](./media/active-directory-saas-saphana-tutorial/sap1.png)

    <span data-ttu-id="58bdb-186">a.</span><span class="sxs-lookup"><span data-stu-id="58bdb-186">a.</span></span> <span data-ttu-id="58bdb-187">İçinde **kimlik sağlayıcısı bilgisi Ekle** bölmesinde, Azure portalından indirmiş meta veri XML içeriğini yapıştırın **meta veri** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="58bdb-187">In the **Add Identity Provider Info** pane, paste the contents of the Metadata XML, which you have downloaded from Azure portal into the **Metadata** textbox.</span></span>

    ![Kimlik sağlayıcı ayarları ekleme](./media/active-directory-saas-saphana-tutorial/sap2.png)

    <span data-ttu-id="58bdb-189">b.</span><span class="sxs-lookup"><span data-stu-id="58bdb-189">b.</span></span> <span data-ttu-id="58bdb-190">XML belgesinin içeriğini geçerliyse, ayrıştırma işlemi eklemek için gereken bilgileri ayıklar **konu, varlık kimliği ve sertifikayı veren** genel veri ekran alanının alanlar ve hedef ekranında URL alanlar alan, örneğin,  **taban URL ve SingleSignOn URL (*)**.</span><span class="sxs-lookup"><span data-stu-id="58bdb-190">If the contents of the XML document are valid, the parsing process extracts the information required to insert into the **Subject, Entity ID, and Issuer** fields in the General Data screen area, and the URL fields in the Destination screen area, for example, **Base URL and SingleSignOn URL (*)**.</span></span>

    ![Kimlik sağlayıcı ayarları ekleme](./media/active-directory-saas-saphana-tutorial/sap3.png)

    <span data-ttu-id="58bdb-192">c.</span><span class="sxs-lookup"><span data-stu-id="58bdb-192">c.</span></span> <span data-ttu-id="58bdb-193">Genel veri ekran alanının adı kutusuna yeni SAML SSO kimlik sağlayıcısı için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="58bdb-193">In the Name box of the General Data screen area, enter a name for the new SAML SSO identity provider.</span></span>

    > [!Note]
    > <span data-ttu-id="58bdb-194">SAML IDP adı zorunludur ve benzersiz olmalıdır; Örneğin, kimlik doğrulama ekran bölümünde XS yapı Yönetim Aracı'nı kullanmak SAP HANA XS uygulamalar için kimlik doğrulama yöntemi olarak SAML seçerseniz görüntülenir, kullanılabilir SAML IDPs listesinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="58bdb-194">The name of the SAML IDP is mandatory and must be unique; it appears in the list of available SAML IDPs that is displayed, if you select SAML as the authentication method for SAP HANA XS applications to use, for example, in the Authentication screen area of the XS Artifact Administration tool.</span></span>

10. <span data-ttu-id="58bdb-195">Yeni SAML kimlik sağlayıcısı ayrıntılarını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="58bdb-195">Save the details of the new SAML identity provider.</span></span> <span data-ttu-id="58bdb-196">Seçin **kaydetmek** SAML kimlik sağlayıcısı ayrıntılarını kaydetmek ve yeni SAML IDP bilinen SAML IDPs listesine eklemek için.</span><span class="sxs-lookup"><span data-stu-id="58bdb-196">Choose **Save** to save the details of the SAML identity provider and add the new SAML IDP to the list of known SAML IDPs.</span></span>

    ![Kaydet düğmesi](./media/active-directory-saas-saphana-tutorial/sap4.png)

11. <span data-ttu-id="58bdb-198">Sistem özelliklerini içinde HANA Studio'da **yapılandırma** sekmesinde, yalnızca ayarlarına göre filtre **saml** ve ayarlama **assertion_timeout** gelen **10 sn**  için **120 saniye**.</span><span class="sxs-lookup"><span data-stu-id="58bdb-198">In HANA Studio within the system properties of the **Configuration** tab, just filter settings by **saml** and adjust the **assertion_timeout** from **10 sec** to **120 sec**.</span></span>

    ![assertion_timeout ayarı](./media/active-directory-saas-saphana-tutorial/sap7.png)

> [!TIP]
> <span data-ttu-id="58bdb-200">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="58bdb-200">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="58bdb-201">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="58bdb-201">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="58bdb-202">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="58bdb-202">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="58bdb-203">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="58bdb-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="58bdb-204">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="58bdb-204">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="58bdb-206">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="58bdb-206">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="58bdb-207">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="58bdb-207">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure Active Directory düğmesi](./media/active-directory-saas-saphana-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="58bdb-209">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="58bdb-209">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    !["Kullanıcılar ve Gruplar" ve "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-saphana-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="58bdb-211">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="58bdb-211">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Ekle düğmesi](./media/active-directory-saas-saphana-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="58bdb-213">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="58bdb-213">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Kullanıcı iletişim kutusu](./media/active-directory-saas-saphana-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="58bdb-215">a.</span><span class="sxs-lookup"><span data-stu-id="58bdb-215">a.</span></span> <span data-ttu-id="58bdb-216">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="58bdb-216">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="58bdb-217">b.</span><span class="sxs-lookup"><span data-stu-id="58bdb-217">b.</span></span> <span data-ttu-id="58bdb-218">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="58bdb-218">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="58bdb-219">c.</span><span class="sxs-lookup"><span data-stu-id="58bdb-219">c.</span></span> <span data-ttu-id="58bdb-220">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="58bdb-220">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="58bdb-221">d.</span><span class="sxs-lookup"><span data-stu-id="58bdb-221">d.</span></span> <span data-ttu-id="58bdb-222">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="58bdb-222">Click **Create**.</span></span>
 
### <a name="creating-a-sap-hana-test-user"></a><span data-ttu-id="58bdb-223">SAP HANA test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="58bdb-223">Creating a SAP HANA test user</span></span>

<span data-ttu-id="58bdb-224">SAP HANA oturum açmak Azure AD kullanıcıları etkinleştirmek için bunların SAP HANA sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="58bdb-224">To enable Azure AD users to log in to SAP HANA, they must be provisioned into SAP HANA.</span></span>
<span data-ttu-id="58bdb-225">SAP HANA tam zamanı sağlama, varsayılan olarak etkin olduğu destekler.</span><span class="sxs-lookup"><span data-stu-id="58bdb-225">SAP HANA supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="58bdb-226">Bir kullanıcı el ile oluşturmanız gerekiyorsa, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="58bdb-226">If you need to create a user manually, perform the following steps:</span></span>

>[!Note]
><span data-ttu-id="58bdb-227">Kullanıcı tarafından kullanılan dış kimlik doğrulama değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="58bdb-227">You can change the external authentication used by the user.</span></span>
<span data-ttu-id="58bdb-228">Dış kullanıcılar, örneğin Kerberos sistem bir dış sistem kullanılarak doğrulanır.</span><span class="sxs-lookup"><span data-stu-id="58bdb-228">External users are authenticated using an external system, for example a Kerberos system.</span></span> <span data-ttu-id="58bdb-229">Dış kimlikler hakkında ayrıntılı bilgi için kişi, [etki alanı yöneticisi](https://cloudplatform.sap.com/contact.html).</span><span class="sxs-lookup"><span data-stu-id="58bdb-229">For detailed information about external identities, contact your [domain administrator](https://cloudplatform.sap.com/contact.html).</span></span>

1. <span data-ttu-id="58bdb-230">Açık [SAP HANA Studio](https://help.sap.com/viewer/a2a49126a5c546a9864aae22c05c3d0e/2.0.01/en-us) bir Yöneticiyseniz ve etkinleştir DB kullanıcı SAML SSO olarak.</span><span class="sxs-lookup"><span data-stu-id="58bdb-230">Open the [SAP HANA Studio](https://help.sap.com/viewer/a2a49126a5c546a9864aae22c05c3d0e/2.0.01/en-us) as an administrator and enable the DB-User for SAML SSO.</span></span>

    ![Kullanıcı oluştur](./media/active-directory-saas-saphana-tutorial/sap5.png)

2. <span data-ttu-id="58bdb-232">Görünmez onay kutusunun solundaki değer **SAML** ve aşağıdaki Yapılandır bağlantısını izleyin.</span><span class="sxs-lookup"><span data-stu-id="58bdb-232">Tick the invisible checkbox to the left of **SAML** and follow the Configure link.</span></span>

3. <span data-ttu-id="58bdb-233">Tıklatın **Ekle** SAML IDP eklenecek ve tıklatın **Tamam** uygun SAML IDP seçme.</span><span class="sxs-lookup"><span data-stu-id="58bdb-233">Click **Add** to add the SAML IDP and click **OK** selecting the appropriate SAML IDP.</span></span>

4. <span data-ttu-id="58bdb-234">Ekleme **Dış kimlik** (örneğin.</span><span class="sxs-lookup"><span data-stu-id="58bdb-234">Add the **External Identity** (ex.</span></span> <span data-ttu-id="58bdb-235">Burada BrittaSimon) veya seçin **"Tüm"** tıklatıp **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="58bdb-235">BrittaSimon here) or choose **"Any"** and click **OK**.</span></span>

    >[!Note]
    ><span data-ttu-id="58bdb-236">"Tüm" onay kutusu işaretli sonra HANA kullanıcı adı tam etki alanı soneki önce UPN kullanıcı adı ile eşleşmesi gerekir (yani BrittaSimon@contoso.com HANA BrittaSimon olur).</span><span class="sxs-lookup"><span data-stu-id="58bdb-236">If "ANY" check-box is not checked, then the user name in HANA needs to exactly match the name of the user in the UPN before the domain suffix (i.e. BrittaSimon@contoso.com would become BrittaSimon in HANA).</span></span>

5. <span data-ttu-id="58bdb-237">Test amacıyla, tüm Ata **"XS"** kullanıcı rolleri.</span><span class="sxs-lookup"><span data-stu-id="58bdb-237">For testing purposes, assign all **"XS"** roles to the user.</span></span>

    ![rol atama](./media/active-directory-saas-saphana-tutorial/sap6.png)

    > [!TIP]
    > <span data-ttu-id="58bdb-239">Bu, kullanım örnekleri için yalnızca uygun izinleri vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="58bdb-239">You should give those permissions appropriate for your use cases, only.</span></span>

6. <span data-ttu-id="58bdb-240">Kullanıcı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="58bdb-240">Save the user.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="58bdb-241">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="58bdb-241">Assigning the Azure AD test user</span></span>

<span data-ttu-id="58bdb-242">Bu bölümde, SAP HANA erişim vererek, Azure çoklu oturum açma kullanılacak Britta Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="58bdb-242">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SAP HANA.</span></span>

![Kullanıcı rolü atayın][200] 

<span data-ttu-id="58bdb-244">**SAP HANA Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="58bdb-244">**To assign Britta Simon to SAP HANA, perform the following steps:**</span></span>

1. <span data-ttu-id="58bdb-245">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="58bdb-245">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="58bdb-247">Uygulamalar listesinde **SAP HANA**.</span><span class="sxs-lookup"><span data-stu-id="58bdb-247">In the applications list, select **SAP HANA**.</span></span>

    ![Kullanıcı atama](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_app.png) 

3. <span data-ttu-id="58bdb-249">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="58bdb-249">In the menu on the left, click **Users and groups**.</span></span>

    !["Kullanıcılar ve Gruplar" bağlantı][202] 

4. <span data-ttu-id="58bdb-251">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="58bdb-251">Click **Add** button.</span></span> <span data-ttu-id="58bdb-252">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="58bdb-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Ekleme atama bölmesi][203]

5. <span data-ttu-id="58bdb-254">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="58bdb-254">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="58bdb-255">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="58bdb-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="58bdb-256">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="58bdb-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="58bdb-257">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="58bdb-257">Testing single sign-on</span></span>

<span data-ttu-id="58bdb-258">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="58bdb-258">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="58bdb-259">Erişim paneli SAP HANA parçasında tıklattığınızda, otomatik olarak SAP HANA uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="58bdb-259">When you click the SAP HANA tile in the Access Panel, you should get automatically signed-on to your SAP HANA application.</span></span>
<span data-ttu-id="58bdb-260">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="58bdb-260">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="58bdb-261">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="58bdb-261">Additional resources</span></span>

* [<span data-ttu-id="58bdb-262">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="58bdb-262">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="58bdb-263">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="58bdb-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



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

