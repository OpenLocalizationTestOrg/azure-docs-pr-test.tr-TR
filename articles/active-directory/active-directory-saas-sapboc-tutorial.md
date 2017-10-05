---
title: "Öğretici: SAP Business nesnesi bulut Azure Active Directory Tümleştirme | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ve SAP Business nesnesi bulut arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 6c5e44f0-4e52-463f-b879-834d80a55cdf
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jeedes
ms.openlocfilehash: 6d517c5e302ac36e5bba2053998c75f8f4d42683
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-business-object-cloud"></a><span data-ttu-id="dda91-103">Öğretici: SAP Business nesnesi bulut Azure Active Directory Tümleştirme</span><span class="sxs-lookup"><span data-stu-id="dda91-103">Tutorial: Azure Active Directory integration with SAP Business Object Cloud</span></span>

<span data-ttu-id="dda91-104">Bu öğreticide, SAP Business nesnesi bulut Azure Active Directory (Azure AD) ile tümleştirme öğrenin.</span><span class="sxs-lookup"><span data-stu-id="dda91-104">In this tutorial, you learn how to integrate SAP Business Object Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dda91-105">SAP Business nesnesi bulut Azure AD ile tümleştirdiğinizde aşağıdaki yararları alın:</span><span class="sxs-lookup"><span data-stu-id="dda91-105">You get the following benefits when you integrate SAP Business Object Cloud with Azure AD:</span></span>

- <span data-ttu-id="dda91-106">Azure AD'de SAP Business nesnesi buluta kimlerin erişimi olduğunu kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dda91-106">In Azure AD, you can control who has access to SAP Business Object Cloud.</span></span>
- <span data-ttu-id="dda91-107">Otomatik olarak SAP Business nesnesi bulut kullanıcılarınıza, çoklu oturum açma ve bir kullanıcının Azure AD hesabı kullanarak oturum.</span><span class="sxs-lookup"><span data-stu-id="dda91-107">You can automatically sign in your users to SAP Business Object Cloud by using single sign-on and a user's Azure AD account.</span></span>
- <span data-ttu-id="dda91-108">Hesaplarınızı tek, merkezi bir konumda, Azure portalında yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="dda91-108">You can manage your accounts in one, central location, the Azure portal.</span></span>

<span data-ttu-id="dda91-109">Azure AD ile hizmet (SaaS) uygulaması tümleştirme olarak yazılım hakkında daha fazla bilgi edinmek için [uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="dda91-109">To learn more about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dda91-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="dda91-110">Prerequisites</span></span>

<span data-ttu-id="dda91-111">SAP Business nesnesi bulut ile Azure AD tümleştirmeyi ayarlamak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="dda91-111">To set up Azure AD integration with SAP Business Object Cloud, you need the following items:</span></span>

- <span data-ttu-id="dda91-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="dda91-112">An Azure AD subscription</span></span>
- <span data-ttu-id="dda91-113">SAP Business nesnesi olan bir buluta, tekli açık oturum</span><span class="sxs-lookup"><span data-stu-id="dda91-113">An SAP Business Object Cloud, with single sign-on turned on</span></span>

> [!NOTE]
> <span data-ttu-id="dda91-114">Bu öğreticide adımları test ederseniz, bunları bir üretim ortamında sınamanızı yok öneririz.</span><span class="sxs-lookup"><span data-stu-id="dda91-114">If you test the steps in this tutorial, we recommend that you don't test them in a production environment.</span></span>

<span data-ttu-id="dda91-115">Bu öğreticide adımları test etmek için öneriler:</span><span class="sxs-lookup"><span data-stu-id="dda91-115">Recommendations for testing the steps in this tutorial:</span></span>

- <span data-ttu-id="dda91-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="dda91-116">Do not use your production environment, unless it's necessary.</span></span>
- <span data-ttu-id="dda91-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık ücretsiz deneme sürümü alma](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dda91-117">If you don't have an Azure AD trial environment, you can [get a one-month free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dda91-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="dda91-118">Scenario description</span></span>
<span data-ttu-id="dda91-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="dda91-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="dda91-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="dda91-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dda91-121">SAP Business nesnesi bulut Galeriden ekleyin.</span><span class="sxs-lookup"><span data-stu-id="dda91-121">Add SAP Business Object Cloud from the gallery.</span></span>
2. <span data-ttu-id="dda91-122">Ayarlama ve Azure AD çoklu oturum açmayı test edin.</span><span class="sxs-lookup"><span data-stu-id="dda91-122">Set up and test Azure AD single sign-on.</span></span>

## <a name="add-sap-business-object-cloud-from-the-gallery"></a><span data-ttu-id="dda91-123">SAP Business nesnesi bulut Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="dda91-123">Add SAP Business Object Cloud from the gallery</span></span>
<span data-ttu-id="dda91-124">Galeride SAP Business nesnesi bulut Azure AD ile tümleştirmeyi ayarlamak için SAP Business nesnesi bulut yönetilen SaaS uygulamaları listenize ekleyin.</span><span class="sxs-lookup"><span data-stu-id="dda91-124">To set up the integration of SAP Business Object Cloud with Azure AD, in the gallery, add SAP Business Object Cloud to your list of managed SaaS apps.</span></span>

<span data-ttu-id="dda91-125">SAP Business nesnesi bulut Galeriden eklemek için:</span><span class="sxs-lookup"><span data-stu-id="dda91-125">To add SAP Business Object Cloud from the gallery:</span></span>

1. <span data-ttu-id="dda91-126">İçinde [Azure portal](https://portal.azure.com), soldaki menüde seçin **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="dda91-126">In the [Azure portal](https://portal.azure.com), in the left menu, select **Azure Active Directory**.</span></span> 

    ![Azure Active Directory düğmesi][1]

2. <span data-ttu-id="dda91-128">Seçin **kurumsal uygulamalar**ve ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="dda91-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Kurumsal uygulamalar sayfası][2]
    
3. <span data-ttu-id="dda91-130">Yeni bir uygulama eklemek için seçin **yeni uygulama**.</span><span class="sxs-lookup"><span data-stu-id="dda91-130">To add a new application, select **New application**.</span></span>

    ![Yeni Uygulama düğmesi][3]

4. <span data-ttu-id="dda91-132">Arama kutusuna **SAP Business nesnesi bulut**.</span><span class="sxs-lookup"><span data-stu-id="dda91-132">In the search box, enter **SAP Business Object Cloud**.</span></span>

    ![Arama kutusu](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_search.png)

5. <span data-ttu-id="dda91-134">Sonuçlar panelinde seçin **SAP Business nesnesi bulut**ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="dda91-134">In the results panel, select **SAP Business Object Cloud**, and then select **Add**.</span></span>

    ![SAP Business nesnesi bulut sonuçlar listesinde](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_addfromgallery.png)

##  <a name="set-up-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="dda91-136">Ayarlama ve Azure AD çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="dda91-136">Set up and test Azure AD single sign-on</span></span>

<span data-ttu-id="dda91-137">Bu bölümde, ayarladığınız ve SAP Business nesnesi bulut ile Azure AD çoklu oturum açmayı test adlı bir test kullanıcı tabanlı *Britta Simon*.</span><span class="sxs-lookup"><span data-stu-id="dda91-137">In this section, you set up and test Azure AD single sign-on with SAP Business Object Cloud based on a test user named *Britta Simon*.</span></span>

<span data-ttu-id="dda91-138">Tekli çalışmaya oturum için Azure AD SAP Business nesnesi bulutta Azure AD karşılık gelen kullanıcı bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="dda91-138">For single sign-on to work, Azure AD needs to know the Azure AD counterpart user in SAP Business Object Cloud.</span></span> <span data-ttu-id="dda91-139">Bir Azure AD kullanıcısının ve SAP Business nesnesi bulutta ilgili kullanıcı arasındaki bağlantıyı ilişkisi kurulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="dda91-139">A link relationship between an Azure AD user and the related user in SAP Business Object Cloud must be established.</span></span>

<span data-ttu-id="dda91-140">İçin SAP Business nesnesi bulutta bağlantı ilişkisi oluşturmak için **kullanıcıadı**, değeri atayın **kullanıcı adı** Azure AD'de.</span><span class="sxs-lookup"><span data-stu-id="dda91-140">To establish the link relationship, in SAP Business Object Cloud, for **Username**, assign the value of the **user name** in Azure AD.</span></span>

<span data-ttu-id="dda91-141">Yapılandırma ve Azure AD çoklu oturum açma SAP Business nesnesi bulut ile test etmek için aşağıdaki görevleri tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="dda91-141">To configure and test Azure AD single sign-on with SAP Business Object Cloud, complete the following tasks:</span></span>

1. <span data-ttu-id="dda91-142">[Azure AD çoklu oturum açmayı ayarlama](#set-up-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="dda91-142">[Set up Azure AD single sign-on](#set-up-azure-ad-single-sign-on).</span></span> <span data-ttu-id="dda91-143">Bir kullanıcı bu özelliği kullanmak için ayarlar.</span><span class="sxs-lookup"><span data-stu-id="dda91-143">Sets up a user to use this feature.</span></span>
2. <span data-ttu-id="dda91-144">[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user).</span><span class="sxs-lookup"><span data-stu-id="dda91-144">[Create an Azure AD test user](#create-an-azure-ad-test-user).</span></span> <span data-ttu-id="dda91-145">Testleri Azure AD çoklu oturum açma Britta Simon kullanıcıyla.</span><span class="sxs-lookup"><span data-stu-id="dda91-145">Tests Azure AD single sign-on with the user Britta Simon.</span></span>
3. <span data-ttu-id="dda91-146">[SAP Business nesnesi bulut test kullanıcısı oluşturma](#create-an-sap-business-object-cloud-test-user).</span><span class="sxs-lookup"><span data-stu-id="dda91-146">[Create an SAP Business Object Cloud test user](#create-an-sap-business-object-cloud-test-user).</span></span> <span data-ttu-id="dda91-147">Karşılık gelen Britta Simon, kullanıcının Azure AD gösterimini bağlı SAP Business nesnesi bulut oluşturur.</span><span class="sxs-lookup"><span data-stu-id="dda91-147">Creates a counterpart of Britta Simon in SAP Business Object Cloud that is linked to the Azure AD representation of the user.</span></span>
4. <span data-ttu-id="dda91-148">[Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user).</span><span class="sxs-lookup"><span data-stu-id="dda91-148">[Assign the Azure AD test user](#assign-the-azure-ad-test-user).</span></span> <span data-ttu-id="dda91-149">Çoklu oturum açmayı Britta Azure AD kullanılacak Simon ayarlar.</span><span class="sxs-lookup"><span data-stu-id="dda91-149">Sets up Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="dda91-150">[Test çoklu oturum açma](#test-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="dda91-150">[Test single sign-on](#test-single-sign-on).</span></span> <span data-ttu-id="dda91-151">Yapılandırma çalıştığını doğrular.</span><span class="sxs-lookup"><span data-stu-id="dda91-151">Verifies that the configuration works.</span></span>

### <a name="set-up-azure-ad-single-sign-on"></a><span data-ttu-id="dda91-152">Azure AD çoklu oturum açmayı ayarlayın</span><span class="sxs-lookup"><span data-stu-id="dda91-152">Set up Azure AD single sign-on</span></span>

<span data-ttu-id="dda91-153">Bu bölümde, üzerinde Azure AD çoklu Azure portalında oturum açın.</span><span class="sxs-lookup"><span data-stu-id="dda91-153">In this section, you turn on Azure AD single sign-on in the Azure portal.</span></span> <span data-ttu-id="dda91-154">Sonra tek oturum açma SAP Business nesnesi bulut uygulamanızda ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="dda91-154">Then, you set up single sign-on in your SAP Business Object Cloud application.</span></span>

<span data-ttu-id="dda91-155">Azure AD çoklu oturum açma SAP Business nesnesi bulut ile ayarlamak için:</span><span class="sxs-lookup"><span data-stu-id="dda91-155">To set up Azure AD single sign-on with SAP Business Object Cloud:</span></span>

1. <span data-ttu-id="dda91-156">Azure portalında üzerinde **SAP Business nesnesi bulut** uygulama tümleştirmesi sayfasında, **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="dda91-156">In the Azure portal, on the **SAP Business Object Cloud** application integration page, select **Single sign-on**.</span></span>

    ![Çoklu oturum açma seçin][4]

2. <span data-ttu-id="dda91-158">Üzerinde **çoklu oturum açma** sayfası için **modu**seçin **SAML tabanlı oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="dda91-158">On the **Single sign-on** page, for **Mode**, select **SAML-based Sign-on**.</span></span>
 
    ![SAML tabanlı oturum açma seçin](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_samlbase.png)

3. <span data-ttu-id="dda91-160">Altında **SAP Business nesnesi bulut etki alanı ve URL'leri**, aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="dda91-160">Under **SAP Business Object Cloud Domain and URLs**, complete the following steps:</span></span>

    1. <span data-ttu-id="dda91-161">İçinde **oturum açma URL'si** kutusunda, aşağıdaki desen bir URL girin:</span><span class="sxs-lookup"><span data-stu-id="dda91-161">In the **Sign-on URL** box, enter a URL that has the following pattern:</span></span> 
    | |
    |-|-|
    | `https://<sub-domain>.sapanalytics.cloud/` |
    | `https://<sub-domain>.sapbusinessobjects.cloud/` |

    2. <span data-ttu-id="dda91-162">İçinde **tanımlayıcısı** kutusunda, aşağıdaki desen bir URL girin:</span><span class="sxs-lookup"><span data-stu-id="dda91-162">In the **Identifier** box, enter a URL that has the following pattern:</span></span>
    | |
    |-|-|
    | `<sub-domain>.sapbusinessobjects.cloud` |
    | `<sub-domain>.sapanalytics.cloud` |

    ![SAP Business nesnesi bulut etki alanı ve URL'leri sayfa URL'leri](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_url.png)
 
    > [!NOTE] 
    > <span data-ttu-id="dda91-164">Bu URL'leri yalnızca tanıtım değerler.</span><span class="sxs-lookup"><span data-stu-id="dda91-164">The values in these URLs are for demonstration only.</span></span> <span data-ttu-id="dda91-165">Değerlerini tanımlayıcı URL'sini ve gerçek oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="dda91-165">Update the values with the actual sign-on URL and identifier URL.</span></span> <span data-ttu-id="dda91-166">Oturum açma URL'si almak için başvurun [SAP Business nesnesi bulut istemci destek ekibi](https://www.sap.com/product/analytics/cloud-analytics.support.html).</span><span class="sxs-lookup"><span data-stu-id="dda91-166">To get the sign-on URL, contact the [SAP Business Object Cloud Client support team](https://www.sap.com/product/analytics/cloud-analytics.support.html).</span></span> <span data-ttu-id="dda91-167">Yönetici konsolundan SAP Business nesnesi bulut meta verileri yükleyerek tanımlayıcı URL'sini alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dda91-167">You can get the identifier URL by downloading the SAP Business Object Cloud metadata from the admin console.</span></span> <span data-ttu-id="dda91-168">Bu öğreticinin ilerleyen bölümlerinde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="dda91-168">This is explained later in the tutorial.</span></span> 

4. <span data-ttu-id="dda91-169">Altında **SAML imzalama sertifikası**seçin **meta veri XML**.</span><span class="sxs-lookup"><span data-stu-id="dda91-169">Under **SAML Signing Certificate**, select **Metadata XML**.</span></span> <span data-ttu-id="dda91-170">Ardından, meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="dda91-170">Then, save the metadata file on your computer.</span></span>

    ![Meta veri XML seçin](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_certificate.png) 

5. <span data-ttu-id="dda91-172">**Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="dda91-172">Select **Save**.</span></span>

    ![Kaydet'i seçin](./media/active-directory-saas-sapboc-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="dda91-174">Farklı web tarayıcısı penceresinde SAP Business nesnesi bulut şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="dda91-174">In a different web browser window, sign in to your SAP Business Object Cloud company site as an administrator.</span></span>

7. <span data-ttu-id="dda91-175">Seçin **menü** > **sistem** > **Yönetim**.</span><span class="sxs-lookup"><span data-stu-id="dda91-175">Select **Menu** > **System** > **Administration**.</span></span>
    
    ![Menüsünü, sonra sistem ve yönetim seçin](./media/active-directory-saas-sapboc-tutorial/config1.png)

8. <span data-ttu-id="dda91-177">Üzerinde **güvenlik** sekmesine **Düzenle** (Kalem) simgesi.</span><span class="sxs-lookup"><span data-stu-id="dda91-177">On the **Security** tab, select the **Edit** (pen) icon.</span></span>
    
    ![Güvenlik sekmesinde Düzenle simgesine seçin](./media/active-directory-saas-sapboc-tutorial/config2.png)  

9. <span data-ttu-id="dda91-179">İçin **kimlik doğrulama yöntemini**seçin **SAML çoklu oturum açma (SSO)**.</span><span class="sxs-lookup"><span data-stu-id="dda91-179">For **Authentication Method**, select **SAML Single Sign-On (SSO)**.</span></span>

    ![SAML çoklu oturum açma kimlik doğrulama yöntemini seçin](./media/active-directory-saas-sapboc-tutorial/config3.png)  

10. <span data-ttu-id="dda91-181">Hizmet sağlayıcısı meta verileri (1. adım) yüklemek üzere seçin **karşıdan**.</span><span class="sxs-lookup"><span data-stu-id="dda91-181">To download the service provider metadata (Step 1), select **Download**.</span></span> <span data-ttu-id="dda91-182">Meta veri dosyasını bulun ve kopyalama **Entityıd** değeri.</span><span class="sxs-lookup"><span data-stu-id="dda91-182">In the metadata file, find and copy the **entityID** value.</span></span> <span data-ttu-id="dda91-183">Azure portalında altında **SAP Business nesnesi bulut etki alanı ve URL'leri**, değeri yapıştırın **tanımlayıcısı** kutusu.</span><span class="sxs-lookup"><span data-stu-id="dda91-183">In the Azure portal, under **SAP Business Object Cloud Domain and URLs**, paste the value in the **Identifier** box.</span></span>

    ![Kopyalama ve yapıştırma Entityıd değeri](./media/active-directory-saas-sapboc-tutorial/config4.png)  

11. <span data-ttu-id="dda91-185">Hizmet sağlayıcısı meta verileri (2. adım) altında Azure portalından indirdiğiniz dosyayı karşıya yükleme için **karşıya kimlik sağlayıcısı meta verileri**seçin **karşıya**.</span><span class="sxs-lookup"><span data-stu-id="dda91-185">To upload the service provider metadata (Step 2) in the file that you downloaded from the Azure portal, under **Upload Identity Provider metadata**, select **Upload**.</span></span>  

    ![Karşıya yükleme karşıya kimlik sağlayıcısı meta verileri altında seçin](./media/active-directory-saas-sapboc-tutorial/config5.png)

12. <span data-ttu-id="dda91-187">İçinde **kullanıcı özniteliği** listesinde, uygulamanız için kullanmak istediğiniz kullanıcı özniteliği (adım 3) seçin.</span><span class="sxs-lookup"><span data-stu-id="dda91-187">In the **User Attribute** list, select the user attribute (Step 3) that you want to use for your implementation.</span></span> <span data-ttu-id="dda91-188">Bu kullanıcı özniteliği kimlik sağlayıcısı eşler.</span><span class="sxs-lookup"><span data-stu-id="dda91-188">This user attribute maps to the identity provider.</span></span> <span data-ttu-id="dda91-189">Özel bir öznitelik kullanıcının sayfasında girmek için **özel SAML eşleme** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="dda91-189">To enter a custom attribute on the user's page, use the **Custom SAML Mapping** option.</span></span> <span data-ttu-id="dda91-190">Ya da her ikisini seçebilirsiniz **e-posta** veya **kullanıcı kimliği** kullanıcı özniteliği olarak.</span><span class="sxs-lookup"><span data-stu-id="dda91-190">Or, you can select either **Email** or **USER ID** as the user attribute.</span></span> <span data-ttu-id="dda91-191">Bizim örneğimizde, biz seçili **e-posta** biz kullanıcı tanımlayıcısı talebi eşlenen çünkü **userprincipalname** özniteliğini **kullanıcı öznitelikleri** Azure portalı bölümünde.</span><span class="sxs-lookup"><span data-stu-id="dda91-191">In our example, we selected **Email** because we mapped the user identifier claim with the **userprincipalname** attribute in the **User Attributes** section in the Azure portal.</span></span> <span data-ttu-id="dda91-192">Bu, her başarılı SAML yanıt SAP Business nesnesi bulut uygulamaya gönderilen bir benzersiz kullanıcı e-posta, sağlar.</span><span class="sxs-lookup"><span data-stu-id="dda91-192">This provides a unique user email, which is sent to the SAP Business Object Cloud application in every successful SAML response.</span></span>

    ![Kullanıcı özniteliğini seçin](./media/active-directory-saas-sapboc-tutorial/config6.png)

13. <span data-ttu-id="dda91-194">Kimlik sağlayıcısı (4. adım), hesabı doğrulamak için **oturum açma kimlik bilgileri (e-posta)** kutusuna, kullanıcının e-posta adresi girin.</span><span class="sxs-lookup"><span data-stu-id="dda91-194">To verify the account with the identity provider (Step 4), in the **Login Credential (Email)** box, enter the user's email address.</span></span> <span data-ttu-id="dda91-195">Ardından, seçin **hesabı doğrula**.</span><span class="sxs-lookup"><span data-stu-id="dda91-195">Then, select **Verify Account**.</span></span> <span data-ttu-id="dda91-196">Sistem kullanıcı hesabı ile oturum açma kimlik bilgilerini ekler.</span><span class="sxs-lookup"><span data-stu-id="dda91-196">The system adds sign-in credentials to the user account.</span></span>

    ![E-posta girin ve Doğrula hesabı seçin](./media/active-directory-saas-sapboc-tutorial/config7.png)

14. <span data-ttu-id="dda91-198">Seçin **kaydetmek** simgesi.</span><span class="sxs-lookup"><span data-stu-id="dda91-198">Select the **Save** icon.</span></span>

    ![Kaydet simgesine](./media/active-directory-saas-sapboc-tutorial/save.png)

> [!TIP]
> <span data-ttu-id="dda91-200">Bu yönergelerde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulamanızı ayarlama yaparken!</span><span class="sxs-lookup"><span data-stu-id="dda91-200">You can read a concise version of these instructions in the [Azure portal](https://portal.azure.com), while you are setting up your app!</span></span> <span data-ttu-id="dda91-201">Seçerek uygulama ekledikten sonra **Active Directory** > **kurumsal uygulamalar**seçin **çoklu oturum açma** sekmesi. Katıştırılmış belgelerde erişebilirsiniz **yapılandırma** bölümünde, sayfanın sonundaki.</span><span class="sxs-lookup"><span data-stu-id="dda91-201">After you add the app by selecting **Active Directory** > **Enterprise Applications**, select the **Single Sign-On** tab. You can access the embedded documentation in the **Configuration** section, at the bottom of the page.</span></span> <span data-ttu-id="dda91-202">Daha fazla bilgi için bkz: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="dda91-202">For more information, see [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="dda91-203">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="dda91-203">Create an Azure AD test user</span></span>
<span data-ttu-id="dda91-204">Bu bölümde, Azure portalında Britta Simon adlı bir test kullanıcısı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="dda91-204">In this section, you create a test user named Britta Simon in the Azure portal.</span></span>

<span data-ttu-id="dda91-205">Azure AD'de bir test kullanıcı oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="dda91-205">To create a test user in Azure AD:</span></span>

1. <span data-ttu-id="dda91-206">Azure portalında soldaki menüde seçin **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="dda91-206">In the Azure portal, in the left menu, select **Azure Active Directory**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sapboc-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="dda91-208">Kullanıcıların listesini görüntülemek için seçin **kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="dda91-208">To display the list of users, select **Users and groups**, and then select **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sapboc-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="dda91-210">Açmak için **kullanıcı** iletişim kutusunda **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="dda91-210">To open the **User** dialog box, select **Add**.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sapboc-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="dda91-212">İçinde **kullanıcı** iletişim kutusunda, aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="dda91-212">In the **User** dialog box, complete the following steps:</span></span>
 
    1. <span data-ttu-id="dda91-213">İçinde **adı** kutusuna **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dda91-213">In the **Name** box, enter **BrittaSimon**.</span></span>

    2. <span data-ttu-id="dda91-214">İçinde **kullanıcı adı** kutusuna, Britta Simon kullanıcının e-posta adresi girin.</span><span class="sxs-lookup"><span data-stu-id="dda91-214">In the **User name** box, enter the email address of the user Britta Simon.</span></span>

    3. <span data-ttu-id="dda91-215">Seçin **Göster parola** onay kutusunu işaretleyin ve ardından görüntülenen değer aşağı yazma **parola** kutusu.</span><span class="sxs-lookup"><span data-stu-id="dda91-215">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    4. <span data-ttu-id="dda91-216">**Oluştur**’u seçin.</span><span class="sxs-lookup"><span data-stu-id="dda91-216">Select **Create**.</span></span>

        ![Kullanıcı iletişim kutusu](./media/active-directory-saas-sapboc-tutorial/create_aaduser_04.png) 

    ![Azure AD Kullanıcı oluşturma][100]

### <a name="create-an-sap-business-object-cloud-test-user"></a><span data-ttu-id="dda91-219">SAP Business nesnesi bulut test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="dda91-219">Create an SAP Business Object Cloud test user</span></span>

<span data-ttu-id="dda91-220">Bunlar SAP Business nesnesi buluta oturum açabilmeniz için önce azure AD kullanıcıları SAP Business nesnesi bulutta sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="dda91-220">Azure AD users must be provisioned in SAP Business Object Cloud before they can sign in to SAP Business Object Cloud.</span></span> <span data-ttu-id="dda91-221">SAP Business nesnesi bulutta sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="dda91-221">In SAP Business Object Cloud, provisioning is a manual task.</span></span>

<span data-ttu-id="dda91-222">Bir kullanıcı hesabı sağlamak için:</span><span class="sxs-lookup"><span data-stu-id="dda91-222">To provision a user account:</span></span>

1. <span data-ttu-id="dda91-223">SAP Business nesnesi bulut şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="dda91-223">Sign in to your SAP Business Object Cloud company site as an administrator.</span></span>

2. <span data-ttu-id="dda91-224">Seçin **menü** > **güvenlik** > **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="dda91-224">Select **Menu** > **Security** > **Users**.</span></span>

    ![Çalışanı ekleyin](./media/active-directory-saas-sapboc-tutorial/user1.png)

3. <span data-ttu-id="dda91-226">Üzerinde **kullanıcılar** seçin sayfasında, yeni kullanıcı ayrıntıları eklemek için  **+** .</span><span class="sxs-lookup"><span data-stu-id="dda91-226">On the **Users** page, to add new user details, select **+**.</span></span> 

    ![Kullanıcılar Sayfası Ekle](./media/active-directory-saas-sapboc-tutorial/user4.png)

    <span data-ttu-id="dda91-228">Ardından, aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="dda91-228">Then, complete the following steps:</span></span>

    1. <span data-ttu-id="dda91-229">İçinde **kullanıcı kimliği** kutusuna, kullanıcının kullanıcı kimliği gibi girin **Britta**.</span><span class="sxs-lookup"><span data-stu-id="dda91-229">In the **USER ID** box, enter the user ID of the user, like **Britta**.</span></span>

    2. <span data-ttu-id="dda91-230">İçinde **ad** kutusuna, kullanıcının ilk adını gibi girin **Britta**.</span><span class="sxs-lookup"><span data-stu-id="dda91-230">In the **FIRST NAME** box, enter the first name of the user, like **Britta**.</span></span>

    3. <span data-ttu-id="dda91-231">İçinde **SOYADI** kutusuna, kullanıcının soyadını gibi girin **Simon**.</span><span class="sxs-lookup"><span data-stu-id="dda91-231">In the **LAST NAME** box, enter the last name of the user, like **Simon**.</span></span>

    4. <span data-ttu-id="dda91-232">İçinde **GÖRÜNEN adı** kutusuna, kullanıcının tam adını gibi girin **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="dda91-232">In the **DISPLAY NAME** box, enter the full name of the user, like **Britta Simon**.</span></span>

    5. <span data-ttu-id="dda91-233">İçinde **e-posta** kutusuna, kullanıcının e-posta adresi gibi girin  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="dda91-233">In the **E-MAIL** box, enter the email address of the user, like **brittasimon@contoso.com**.</span></span>

    6. <span data-ttu-id="dda91-234">Üzerinde **Rollerini Seç** sayfasında, kullanıcı için uygun rolü seçin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="dda91-234">On the **Select Roles** page, select the appropriate role for the user, and then select **OK**.</span></span>

      ![Rol seç](./media/active-directory-saas-sapboc-tutorial/user3.png)

    7. <span data-ttu-id="dda91-236">Seçin **kaydetmek** simgesi.</span><span class="sxs-lookup"><span data-stu-id="dda91-236">Select the **Save** icon.</span></span>    


### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="dda91-237">Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="dda91-237">Assign the Azure AD test user</span></span>

<span data-ttu-id="dda91-238">Bu bölümde, SAP Business nesnesi bulut için kullanıcı hesabı erişimi verilmesi tarafından Azure AD çoklu oturum açma kullanılacak Britta Simon kullanıcı izin verin.</span><span class="sxs-lookup"><span data-stu-id="dda91-238">In this section, you allow the user Britta Simon to use Azure AD single sign-on by granting the user account access to SAP Business Object Cloud.</span></span>

<span data-ttu-id="dda91-239">SAP Business nesnesi buluta Britta Simon atamak için:</span><span class="sxs-lookup"><span data-stu-id="dda91-239">To assign Britta Simon to SAP Business Object Cloud:</span></span>

1. <span data-ttu-id="dda91-240">Azure Portalı'ndaki uygulamaları görünümünü açın ve dizin görünümüne gidin.</span><span class="sxs-lookup"><span data-stu-id="dda91-240">In the Azure portal, open the applications view, and then go to the directory view.</span></span> <span data-ttu-id="dda91-241">Seçin **kurumsal uygulamalar**ve ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="dda91-241">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="dda91-243">Uygulamalar listesinde **SAP Business nesnesi bulut**.</span><span class="sxs-lookup"><span data-stu-id="dda91-243">In the applications list, select **SAP Business Object Cloud**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_app.png) 

3. <span data-ttu-id="dda91-245">Soldaki menüde seçin **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="dda91-245">In the left menu, select **Users and groups**.</span></span>

    ![Kullanıcıları ve grupları seçin][202] 

4. <span data-ttu-id="dda91-247">**Add (Ekle)** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="dda91-247">Select **Add**.</span></span> <span data-ttu-id="dda91-248">Ardından **eklemek atama** sayfasında, **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="dda91-248">Then, on the **Add Assignment** page, select **Users and groups**.</span></span>

    ![Atama Ekle sayfası][203]

5. <span data-ttu-id="dda91-250">Üzerinde **kullanıcılar ve gruplar** sayfasında, kullanıcıların, seçim listesinde **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="dda91-250">On the **Users and groups** page, in the list of users, select **Britta Simon**.</span></span>

6. <span data-ttu-id="dda91-251">Üzerinde **kullanıcılar ve gruplar** sayfasında, **seçin**.</span><span class="sxs-lookup"><span data-stu-id="dda91-251">On the **Users and groups** page, select **Select**.</span></span>

7. <span data-ttu-id="dda91-252">Üzerinde **eklemek atama** sayfasında, **atamak**.</span><span class="sxs-lookup"><span data-stu-id="dda91-252">On the **Add Assignment** page, select **Assign**.</span></span>

![Kullanıcı rolü atayın][200] 
    
### <a name="test-single-sign-on"></a><span data-ttu-id="dda91-254">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="dda91-254">Test single sign-on</span></span>

<span data-ttu-id="dda91-255">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test.</span><span class="sxs-lookup"><span data-stu-id="dda91-255">In this section, you test your Azure AD single sign-on configuration by using the access panel.</span></span>

<span data-ttu-id="dda91-256">SAP Business nesnesi bulut döşeme erişim panelinde seçtiğinizde, otomatik olarak SAP Business nesnesi bulut uygulamanıza oturum açmanız.</span><span class="sxs-lookup"><span data-stu-id="dda91-256">When you select the SAP Business Object Cloud tile in the access panel, you should be automatically signed in to your SAP Business Object Cloud application.</span></span>

<span data-ttu-id="dda91-257">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="dda91-257">For more information about the access panel, see [Introduction to the access panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="dda91-258">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="dda91-258">Additional resources</span></span>

* [<span data-ttu-id="dda91-259">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="dda91-259">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="dda91-260">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="dda91-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_203.png

