---
title: "Öğretici: Azure Active Directory Tümleştirme MOVEit Transfer - Azure AD Tümleştirmesi ile | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory MOVEit Transfer - Azure AD tümleştirme arasındaki yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8ff7102d-be73-4888-ae81-d8e3d01dd534
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: d35aceb9be2d0ff49f86a00cc84f5deb198d88f0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moveit-transfer---azure-ad-integration"></a><span data-ttu-id="50894-103">Öğretici: Azure Active Directory Tümleştirme ile MOVEit Transfer - Azure AD tümleştirme</span><span class="sxs-lookup"><span data-stu-id="50894-103">Tutorial: Azure Active Directory integration with MOVEit Transfer - Azure AD integration</span></span>

<span data-ttu-id="50894-104">Bu öğreticide, MOVEit Transfer - Azure Active Directory (Azure AD) ile Azure AD tümleştirme tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="50894-104">In this tutorial, you learn how to integrate MOVEit Transfer - Azure AD integration with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="50894-105">MOVEit Transfer - Azure AD tümleştirme Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="50894-105">Integrating MOVEit Transfer - Azure AD integration with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="50894-106">MOVEit Transfer - Azure AD tümleştirme erişimi, Azure AD'de kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="50894-106">You can control in Azure AD who has access to MOVEit Transfer - Azure AD integration.</span></span>
- <span data-ttu-id="50894-107">Otomatik olarak MOVEit aktarımı - Azure AD hesaplarına ile Azure AD tümleştirme (çoklu oturum açma) açan kullanıcılarınıza etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="50894-107">You can enable your users to automatically get signed-on to MOVEit Transfer - Azure AD integration (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="50894-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="50894-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="50894-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="50894-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="50894-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="50894-110">Prerequisites</span></span>

<span data-ttu-id="50894-111">Azure AD tümleştirme MOVEit Transfer - Azure AD tümleştirme yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="50894-111">To configure Azure AD integration with MOVEit Transfer - Azure AD integration, you need the following items:</span></span>

- <span data-ttu-id="50894-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="50894-112">An Azure AD subscription</span></span>
- <span data-ttu-id="50894-113">MOVEit Transfer - Azure AD tümleştirme çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="50894-113">A MOVEit Transfer - Azure AD integration single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="50894-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="50894-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="50894-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="50894-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="50894-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="50894-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="50894-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="50894-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="50894-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="50894-118">Scenario description</span></span>
<span data-ttu-id="50894-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="50894-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="50894-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="50894-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="50894-121">MOVEit Transfer - Azure AD tümleştirme galerisinden ekleme</span><span class="sxs-lookup"><span data-stu-id="50894-121">Adding MOVEit Transfer - Azure AD integration from the gallery</span></span>
2. <span data-ttu-id="50894-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="50894-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-moveit-transfer---azure-ad-integration-from-the-gallery"></a><span data-ttu-id="50894-123">MOVEit Transfer - Azure AD tümleştirme galerisinden ekleme</span><span class="sxs-lookup"><span data-stu-id="50894-123">Adding MOVEit Transfer - Azure AD integration from the gallery</span></span>
<span data-ttu-id="50894-124">MOVEit Transfer - Azure AD, Azure AD tümleştirmeye tümleştirmesini yapılandırma MOVEit Transfer - Azure AD tümleştirme galerisinden listenize yönetilen SaaS uygulamalarının eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="50894-124">To configure the integration of MOVEit Transfer - Azure AD integration into Azure AD, you need to add MOVEit Transfer - Azure AD integration from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="50894-125">**Azure AD tümleştirme Galerisi'nden MOVEit Transfer - eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="50894-125">**To add MOVEit Transfer - Azure AD integration from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="50894-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="50894-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory düğmesi][1]

2. <span data-ttu-id="50894-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="50894-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="50894-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="50894-129">Then go to **All applications**.</span></span>

    ![Kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="50894-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="50894-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Yeni Uygulama düğmesi][3]

4. <span data-ttu-id="50894-133">Arama kutusuna yazın **MOVEit Transfer - Azure AD tümleştirme**seçin **MOVEit Transfer - Azure AD tümleştirme** sonuç panelinden ardından **Ekle** Ekle düğmesi uygulama.</span><span class="sxs-lookup"><span data-stu-id="50894-133">In the search box, type **MOVEit Transfer - Azure AD integration**, select **MOVEit Transfer - Azure AD integration** from result panel then click **Add** button to add the application.</span></span>

    ![MOVEit Transfer - Azure AD tümleştirme sonuçlar listesinde](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="50894-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="50894-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="50894-136">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma MOVEit Transfer - "Britta Simon" adlı bir test kullanıcı tabanlı Azure AD Tümleştirmesi ile test etme.</span><span class="sxs-lookup"><span data-stu-id="50894-136">In this section, you configure and test Azure AD single sign-on with MOVEit Transfer - Azure AD integration based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="50894-137">Tekli çalışmaya oturum için Azure AD ne karşılık gelen MOVEit transfer - Azure AD tümleştirme bir kullanıcı için Azure AD içinde olduğu bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="50894-137">For single sign-on to work, Azure AD needs to know what the counterpart user in MOVEit Transfer - Azure AD integration is to a user in Azure AD.</span></span> <span data-ttu-id="50894-138">Diğer bir deyişle, bir Azure AD kullanıcısının ve ilgili kullanıcı MOVEit transfer - arasında bir bağlantı ilişkisi Azure AD tümleştirme kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="50894-138">In other words, a link relationship between an Azure AD user and the related user in MOVEit Transfer - Azure AD integration needs to be established.</span></span>

<span data-ttu-id="50894-139">Değeri MOVEit Transfer - Azure AD tümleştirme atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="50894-139">In MOVEit Transfer - Azure AD integration, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="50894-140">Yapılandırmak ve Azure AD çoklu oturum açma ile MOVEit Transfer - sınamak için Azure AD tümleştirme, aşağıdaki yapı taşları tamamlanması gerekir:</span><span class="sxs-lookup"><span data-stu-id="50894-140">To configure and test Azure AD single sign-on with MOVEit Transfer - Azure AD integration, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="50894-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="50894-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="50894-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="50894-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="50894-143">**[MOVEit Transfer - Azure AD tümleştirme test kullanıcısı oluşturma](#create-a-moveit-transfer---azure-ad-integration-test-user)**  - Britta Simon, karşılık gelen MOVEit Transfer - kullanıcı Azure AD gösterimini bağlı Azure AD tümleştirme sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="50894-143">**[Create a MOVEit Transfer - Azure AD integration test user](#create-a-moveit-transfer---azure-ad-integration-test-user)** - to have a counterpart of Britta Simon in MOVEit Transfer - Azure AD integration that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="50894-144">**[Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="50894-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="50894-145">**[Test çoklu oturum açma](#test-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="50894-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="50894-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="50894-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="50894-147">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma, MOVEit Transfer - Azure AD tümleştirme uygulaması yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="50894-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your MOVEit Transfer - Azure AD integration application.</span></span>

<span data-ttu-id="50894-148">**Azure AD çoklu oturum açma MOVEit Transfer - Azure AD tümleştirme yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="50894-148">**To configure Azure AD single sign-on with MOVEit Transfer - Azure AD integration, perform the following steps:**</span></span>

1. <span data-ttu-id="50894-149">Azure portalında üzerinde **MOVEit Transfer - Azure AD tümleştirme** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="50894-149">In the Azure portal, on the **MOVEit Transfer - Azure AD integration** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. <span data-ttu-id="50894-151">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="50894-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_samlbase.png)

3. <span data-ttu-id="50894-153">Üzerinde **MOVEit aktarım - Azure AD tümleştirme etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="50894-153">On the **MOVEit Transfer - Azure AD integration Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_url.png)

    <span data-ttu-id="50894-155">a.</span><span class="sxs-lookup"><span data-stu-id="50894-155">a.</span></span> <span data-ttu-id="50894-156">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://contoso.com`</span><span class="sxs-lookup"><span data-stu-id="50894-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://contoso.com`</span></span>

    <span data-ttu-id="50894-157">b.</span><span class="sxs-lookup"><span data-stu-id="50894-157">b.</span></span> <span data-ttu-id="50894-158">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://contoso.com/<tenatid>`</span><span class="sxs-lookup"><span data-stu-id="50894-158">In the **Identifier** textbox, type a URL using the following pattern: `https://contoso.com/<tenatid>`</span></span>

    <span data-ttu-id="50894-159">c.</span><span class="sxs-lookup"><span data-stu-id="50894-159">c.</span></span> <span data-ttu-id="50894-160">İçinde **yanıt URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://contoso.com/<tenatid>/SAML/SSO/HTTP-Post`</span><span class="sxs-lookup"><span data-stu-id="50894-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://contoso.com/<tenatid>/SAML/SSO/HTTP-Post`</span></span>    
     
    > [!NOTE] 
    > <span data-ttu-id="50894-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="50894-161">These values are not real.</span></span> <span data-ttu-id="50894-162">Bu değerler, gerçek tanımlayıcı, yanıt URL'si ve oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="50894-162">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="50894-163">Bu değerleri daha sonra da başvurabilir **servis sağlayıcı meta verileri URL'sini** bölüm veya kişi [MOVEit Transfer - Azure AD tümleştirme istemci destek ekibi](https://community.ipswitch.com/s/support) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="50894-163">You can refer these values later in **Service Provider Metadata URL** section or contact [MOVEit Transfer - Azure AD integration Client support team](https://community.ipswitch.com/s/support) to get these values.</span></span>

4. <span data-ttu-id="50894-164">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="50894-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Sertifika indirme bağlantısı](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_certificate.png) 

5. <span data-ttu-id="50894-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="50894-166">Click **Save** button.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="50894-168">MOVEit aktarımı Kiracı yönetici olarak oturum açma.</span><span class="sxs-lookup"><span data-stu-id="50894-168">Sign on to your MOVEit Transfer tenant as an administrator.</span></span>

7. <span data-ttu-id="50894-169">Sol gezinti bölmesinde tıklatın **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="50894-169">On the left navigation pane, click **Settings**.</span></span>

    ![Ayarları bölümü üzerinde uygulama yan](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_000.png)

8. <span data-ttu-id="50894-171">Tıklatın **tek oturum açma** altındaki bağlantı **kullanıcı kimlik doğrulama -> güvenlik ilkelerini**.</span><span class="sxs-lookup"><span data-stu-id="50894-171">Click **Single Signon** link, which is under **Security Policies -> User Auth**.</span></span>

    ![Güvenlik ilkeleri üzerinde uygulama yan](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_001.png)

9. <span data-ttu-id="50894-173">Meta veri belgesi indirmek için meta veri URL'sini bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="50894-173">Click the Metadata URL link to download the metadata document.</span></span>

    ![Hizmet sağlayıcısı meta veri URL'si](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_002.png)
    
    * <span data-ttu-id="50894-175">Doğrulayın **Entityıd** eşleşen **tanımlayıcısı** içinde **MOVEit aktarım - Azure AD tümleştirme etki alanı ve URL'leri** bölümü.</span><span class="sxs-lookup"><span data-stu-id="50894-175">Verify **entityID** matches **Identifier** in the **MOVEit Transfer - Azure AD integration Domain and URLs** section .</span></span>
    * <span data-ttu-id="50894-176">Doğrulayın **AssertionConsumerService** konumu URL ile eşleşip **yanıt URL'si** içinde **MOVEit aktarım - Azure AD tümleştirme etki alanı ve URL'leri** bölümü.</span><span class="sxs-lookup"><span data-stu-id="50894-176">Verify **AssertionConsumerService** Location URL matches **REPLY URL** in the **MOVEit Transfer - Azure AD integration Domain and URLs** section.</span></span>
    
    ![Çoklu oturum açma üzerinde uygulama tarafı yapılandırma](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_007.png)

10. <span data-ttu-id="50894-178">Tıklatın **kimlik sağlayıcı Ekle** yeni bir Federasyon kimlik sağlayıcısı eklemek için düğmeyi.</span><span class="sxs-lookup"><span data-stu-id="50894-178">Click **Add Identity Provider** button to add a new Federated Identity Provider.</span></span>

    ![Kimlik sağlayıcısı ekleyin](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_003.png)

11. <span data-ttu-id="50894-180">Tıklatın **Gözat...**  Azure Portalı'ndan indirilen meta veri dosyası seçmek için ardından **kimlik sağlayıcı Ekle** indirilen dosya karşıya yüklemek için.</span><span class="sxs-lookup"><span data-stu-id="50894-180">Click **Browse...** to select the metadata file which you downloaded from Azure portal, then click **Add Identity Provider** to upload the downloaded file.</span></span>

    ![SAML kimlik sağlayıcısı](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_004.png)

12. <span data-ttu-id="50894-182">Seçin "**Evet**" olarak **etkin** içinde **Federasyon kimlik sağlayıcı ayarları Düzenle...**  sayfasında ve tıklayın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="50894-182">Select "**Yes**" as **Enabled** in the **Edit Federated Identity Provider Settings...** page and click **Save**.</span></span>

    ![Federe kimlik sağlayıcı ayarları](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_005.png)

13. <span data-ttu-id="50894-184">İçinde **federe kimlik sağlayıcısı kullanıcı ayarlarını Düzenle** sayfasında, aşağıdaki eylemleri gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="50894-184">In the **Edit Federated Identity Provider User Settings** page, perform the following actions:</span></span>
    
    ![Federe kimlik sağlayıcı ayarları Düzenle](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_006.png)
    
    <span data-ttu-id="50894-186">a.</span><span class="sxs-lookup"><span data-stu-id="50894-186">a.</span></span> <span data-ttu-id="50894-187">Seçin **SAML NameID** olarak **oturum açma adı**.</span><span class="sxs-lookup"><span data-stu-id="50894-187">Select **SAML NameID** as **Login name**.</span></span>
    
    <span data-ttu-id="50894-188">b.</span><span class="sxs-lookup"><span data-stu-id="50894-188">b.</span></span> <span data-ttu-id="50894-189">Seçin **diğer** olarak **tam adı** ve **öznitelik adı** textbox değeri koyun: `http://schemas.microsoft.com/identity/claims/displayname`.</span><span class="sxs-lookup"><span data-stu-id="50894-189">Select **Other** as **Full name** and in the **Attribute name** textbox put the value: `http://schemas.microsoft.com/identity/claims/displayname`.</span></span>
    
    <span data-ttu-id="50894-190">c.</span><span class="sxs-lookup"><span data-stu-id="50894-190">c.</span></span> <span data-ttu-id="50894-191">Seçin **diğer** olarak **e-posta** ve **öznitelik adı** textbox değeri koyun: `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="50894-191">Select **Other** as **Email** and in the **Attribute name** textbox put the value: `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
    
    <span data-ttu-id="50894-192">d.</span><span class="sxs-lookup"><span data-stu-id="50894-192">d.</span></span> <span data-ttu-id="50894-193">Seçin **Evet** olarak **oturum açma hesabı otomatik olarak oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="50894-193">Select **Yes** as **Auto-create account on signon**.</span></span>
    
    <span data-ttu-id="50894-194">e.</span><span class="sxs-lookup"><span data-stu-id="50894-194">e.</span></span> <span data-ttu-id="50894-195">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="50894-195">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="50894-196">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="50894-196">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="50894-197">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="50894-197">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="50894-198">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="50894-198">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="50894-199">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="50894-199">Create an Azure AD test user</span></span>

<span data-ttu-id="50894-200">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="50894-200">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="50894-202">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="50894-202">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="50894-203">Sol bölmede, Azure portal'ı tıklatın **Azure Active Directory** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="50894-203">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory düğmesi](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="50894-205">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="50894-205">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["Kullanıcılar ve Gruplar" ve "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="50894-207">Açmak için **kullanıcı** iletişim kutusu, tıklatın **Ekle** en üstündeki **tüm kullanıcılar** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="50894-207">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Ekle düğmesi](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="50894-209">İçinde **kullanıcı** iletişim kutusunda, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="50894-209">In the **User** dialog box, perform the following steps:</span></span>

    ![Kullanıcı iletişim kutusu](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_04.png)

    <span data-ttu-id="50894-211">a.</span><span class="sxs-lookup"><span data-stu-id="50894-211">a.</span></span> <span data-ttu-id="50894-212">İçinde **adı** kutusuna **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="50894-212">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="50894-213">b.</span><span class="sxs-lookup"><span data-stu-id="50894-213">b.</span></span> <span data-ttu-id="50894-214">İçinde **kullanıcı adı** kullanıcı Britta Simon e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="50894-214">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="50894-215">c.</span><span class="sxs-lookup"><span data-stu-id="50894-215">c.</span></span> <span data-ttu-id="50894-216">Seçin **Göster parola** onay kutusunu işaretleyin ve ardından görüntülenen değer aşağı yazma **parola** kutusu.</span><span class="sxs-lookup"><span data-stu-id="50894-216">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="50894-217">d.</span><span class="sxs-lookup"><span data-stu-id="50894-217">d.</span></span> <span data-ttu-id="50894-218">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="50894-218">Click **Create**.</span></span>
 
### <a name="create-a-moveit-transfer---azure-ad-integration-test-user"></a><span data-ttu-id="50894-219">MOVEit Transfer - Azure AD tümleştirme test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="50894-219">Create a MOVEit Transfer - Azure AD integration test user</span></span>

<span data-ttu-id="50894-220">Bu bölümün amacı Britta Simon MOVEit Transfer - Azure AD tümleştirme adlı bir kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="50894-220">The objective of this section is to create a user called Britta Simon in MOVEit Transfer - Azure AD integration.</span></span> <span data-ttu-id="50894-221">MOVEit Transfer - Azure AD tümleştirme yalnızca zaman sağlama, hangi etkinleştirdiğiniz destekler.</span><span class="sxs-lookup"><span data-stu-id="50894-221">MOVEit Transfer - Azure AD integration supports just-in-time provisioning, which you have enabled.</span></span> <span data-ttu-id="50894-222">Bu bölümde, eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="50894-222">There is no action item for you in this section.</span></span> <span data-ttu-id="50894-223">Yeni bir kullanıcı MOVEit Transfer - henüz yoksa Azure AD tümleştirme erişme denemesi sırasında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="50894-223">A new user is created during an attempt to access MOVEit Transfer - Azure AD integration if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="50894-224">Bir kullanıcı el ile oluşturmanız gerekiyorsa, başvurmanız gerekir [MOVEit Transfer - Azure AD tümleştirme istemci destek ekibi](https://community.ipswitch.com/s/support).</span><span class="sxs-lookup"><span data-stu-id="50894-224">If you need to create a user manually, you need to contact the [MOVEit Transfer - Azure AD integration Client support team](https://community.ipswitch.com/s/support).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="50894-225">Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="50894-225">Assign the Azure AD test user</span></span>

<span data-ttu-id="50894-226">Bu bölümde, Britta MOVEit Transfer - Azure AD tümleştirme erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="50894-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to MOVEit Transfer - Azure AD integration.</span></span>

![Kullanıcı rolü atayın][200] 

<span data-ttu-id="50894-228">**Britta Simon MOVEit Transfer - Azure AD tümleştirme atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="50894-228">**To assign Britta Simon to MOVEit Transfer - Azure AD integration, perform the following steps:**</span></span>

1. <span data-ttu-id="50894-229">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="50894-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="50894-231">Uygulamalar listesinde **MOVEit Transfer - Azure AD tümleştirme**.</span><span class="sxs-lookup"><span data-stu-id="50894-231">In the applications list, select **MOVEit Transfer - Azure AD integration**.</span></span>

    ![MOVEit Transfer - Azure AD tümleştirme uygulamalar listesinde bağlantı](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_app.png)  

3. <span data-ttu-id="50894-233">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="50894-233">In the menu on the left, click **Users and groups**.</span></span>

    !["Kullanıcılar ve Gruplar" bağlantı][202]

4. <span data-ttu-id="50894-235">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="50894-235">Click **Add** button.</span></span> <span data-ttu-id="50894-236">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="50894-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Ekleme atama bölmesi][203]

5. <span data-ttu-id="50894-238">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="50894-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="50894-239">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="50894-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="50894-240">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="50894-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="50894-241">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="50894-241">Test single sign-on</span></span>

<span data-ttu-id="50894-242">Bu bölümün amacı erişim paneli kullanılarak Azure AD SSO yapılandırmanızı test etmektir.</span><span class="sxs-lookup"><span data-stu-id="50894-242">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="50894-243">MOVEit Transfer - tıklattığınızda Azure AD tümleştirme kutucuğunu erişim panelinde, otomatik olarak imzalanmış-, MOVEit Transfer - Azure AD tümleştirme uygulaması için.</span><span class="sxs-lookup"><span data-stu-id="50894-243">When you click the MOVEit Transfer - Azure AD integration tile in the Access Panel, you should get automatically signed-on to your MOVEit Transfer - Azure AD integration application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="50894-244">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="50894-244">Additional resources</span></span>

* [<span data-ttu-id="50894-245">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="50894-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="50894-246">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="50894-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_203.png

