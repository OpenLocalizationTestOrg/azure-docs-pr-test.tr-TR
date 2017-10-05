---
title: "Öğretici: Azure Active Directory Tümleştirmesi algısına Amerika Birleşik Devletleri (Non-UltiPro) ile | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile algısına Amerika Birleşik Devletleri (Non-UltiPro) arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: b4a8f026-cb5f-41eb-9680-68eddc33565e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 8e2f9f979f8b94e0c043d4db6e93bd7a53c3dd27
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-perception-united-states-non-ultipro"></a><span data-ttu-id="266ba-103">Öğretici: Azure Active Directory Tümleştirmesi algısına Amerika Birleşik Devletleri (Non-UltiPro) ile</span><span class="sxs-lookup"><span data-stu-id="266ba-103">Tutorial: Azure Active Directory integration with Perception United States (Non-UltiPro)</span></span>

<span data-ttu-id="266ba-104">Bu öğreticide, Azure Active Directory (Azure AD) ile algısına Amerika Birleşik Devletleri (Non-UltiPro) tümleştirme öğrenin.</span><span class="sxs-lookup"><span data-stu-id="266ba-104">In this tutorial, you learn how to integrate Perception United States (Non-UltiPro) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="266ba-105">Algısına Amerika Birleşik Devletleri (Non-UltiPro) Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="266ba-105">Integrating Perception United States (Non-UltiPro) with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="266ba-106">Erişimi algısına Amerika Birleşik Devletleri (Non-UltiPro) için Azure AD'de kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="266ba-106">You can control in Azure AD who has access to Perception United States (Non-UltiPro).</span></span>
- <span data-ttu-id="266ba-107">Otomatik olarak algısına Amerika Birleşik Devletleri (Non-UltiPro) (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="266ba-107">You can enable your users to automatically get signed-on to Perception United States (Non-UltiPro) (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="266ba-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="266ba-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="266ba-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="266ba-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="266ba-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="266ba-110">Prerequisites</span></span>

<span data-ttu-id="266ba-111">Azure AD tümleştirmesi algısına Amerika Birleşik Devletleri (Non-UltiPro) yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="266ba-111">To configure Azure AD integration with Perception United States (Non-UltiPro), you need the following items:</span></span>

- <span data-ttu-id="266ba-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="266ba-112">An Azure AD subscription</span></span>
- <span data-ttu-id="266ba-113">Bir algısına Amerika Birleşik Devletleri (Non-UltiPro) çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="266ba-113">A Perception United States (Non-UltiPro) single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="266ba-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="266ba-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="266ba-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="266ba-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="266ba-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="266ba-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="266ba-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="266ba-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="266ba-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="266ba-118">Scenario description</span></span>
<span data-ttu-id="266ba-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="266ba-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="266ba-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="266ba-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="266ba-121">Galeriden algısına Amerika Birleşik Devletleri (Non-UltiPro) ekleme</span><span class="sxs-lookup"><span data-stu-id="266ba-121">Adding Perception United States (Non-UltiPro) from the gallery</span></span>
2. <span data-ttu-id="266ba-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="266ba-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-perception-united-states-non-ultipro-from-the-gallery"></a><span data-ttu-id="266ba-123">Galeriden algısına Amerika Birleşik Devletleri (Non-UltiPro) ekleme</span><span class="sxs-lookup"><span data-stu-id="266ba-123">Adding Perception United States (Non-UltiPro) from the gallery</span></span>
<span data-ttu-id="266ba-124">Azure AD ile tümleştirme, algısına Amerika Birleşik Devletleri (Non-UltiPro) yapılandırmak için algısına Amerika Birleşik Devletleri (Non-UltiPro) eklemeniz Galeriden yönetilen SaaS uygulamaları listenize gerekir.</span><span class="sxs-lookup"><span data-stu-id="266ba-124">To configure the integration of Perception United States (Non-UltiPro) into Azure AD, you need to add Perception United States (Non-UltiPro) from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="266ba-125">**Galeriden algısına Amerika Birleşik Devletleri (Non-UltiPro) eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="266ba-125">**To add Perception United States (Non-UltiPro) from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="266ba-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="266ba-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory düğmesi][1]

2. <span data-ttu-id="266ba-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="266ba-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="266ba-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="266ba-129">Then go to **All applications**.</span></span>

    ![Kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="266ba-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="266ba-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Yeni Uygulama düğmesi][3]

4. <span data-ttu-id="266ba-133">Arama kutusuna **algısına Amerika Birleşik Devletleri (Non-UltiPro)**seçin **algısına Amerika Birleşik Devletleri (Non-UltiPro)** sonuç panelinden ardından **Ekle** uygulama eklemek için düğmeyi.</span><span class="sxs-lookup"><span data-stu-id="266ba-133">In the search box, type **Perception United States (Non-UltiPro)**, select **Perception United States (Non-UltiPro)** from result panel then click **Add** button to add the application.</span></span>

    ![Sonuçlar listesinde algısına Amerika Birleşik Devletleri (Non-UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="266ba-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="266ba-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="266ba-136">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma ile algısına "Britta Simon" adlı bir test kullanıcı tabanlı ABD (UltiPro olmayan) test etme.</span><span class="sxs-lookup"><span data-stu-id="266ba-136">In this section, you configure and test Azure AD single sign-on with Perception United States (Non-UltiPro) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="266ba-137">Tekli çalışmaya oturum için Azure AD ne karşılık gelen algısına Amerika Birleşik Devletleri (Non-UltiPro) içinde bir kullanıcı için Azure AD içinde olduğu bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="266ba-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Perception United States (Non-UltiPro) is to a user in Azure AD.</span></span> <span data-ttu-id="266ba-138">Diğer bir deyişle, bir Azure AD kullanıcısının ve ilgili kullanıcı içinde algısına Amerika Birleşik Devletleri (Non-UltiPro) arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="266ba-138">In other words, a link relationship between an Azure AD user and the related user in Perception United States (Non-UltiPro) needs to be established.</span></span>

<span data-ttu-id="266ba-139">Değeri algısına Amerika Birleşik Devletleri (UltiPro olmayan), Ata **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="266ba-139">In Perception United States (Non-UltiPro), assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="266ba-140">Yapılandırma ve Azure AD çoklu oturum açma algısına Amerika Birleşik Devletleri (Non-UltiPro) ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="266ba-140">To configure and test Azure AD single sign-on with Perception United States (Non-UltiPro), you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="266ba-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="266ba-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="266ba-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="266ba-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="266ba-143">**[Algısına Amerika Birleşik Devletleri (Non-UltiPro) test kullanıcısı oluşturma](#create-a-perception-united-states-non-ultipro-test-user)**  - Britta Simon, karşılık gelen içinde algısına kullanıcı Azure AD gösterimini bağlantılı ABD (UltiPro olmayan) sahip.</span><span class="sxs-lookup"><span data-stu-id="266ba-143">**[Create a Perception United States (Non-UltiPro) test user](#create-a-perception-united-states-non-ultipro-test-user)** - to have a counterpart of Britta Simon in Perception United States (Non-UltiPro) that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="266ba-144">**[Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="266ba-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="266ba-145">**[Test çoklu oturum açma](#test-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="266ba-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="266ba-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="266ba-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="266ba-147">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma algısına Amerika Birleşik Devletleri (Non-UltiPro) uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="266ba-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Perception United States (Non-UltiPro) application.</span></span>

<span data-ttu-id="266ba-148">**Azure AD çoklu oturum açma algısına Amerika Birleşik Devletleri (Non-UltiPro) yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="266ba-148">**To configure Azure AD single sign-on with Perception United States (Non-UltiPro), perform the following steps:**</span></span>

1. <span data-ttu-id="266ba-149">Azure portalında üzerinde **algısına Amerika Birleşik Devletleri (Non-UltiPro)** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="266ba-149">In the Azure portal, on the **Perception United States (Non-UltiPro)** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. <span data-ttu-id="266ba-151">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="266ba-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_samlbase.png)

3. <span data-ttu-id="266ba-153">Üzerinde **algısına Amerika Birleşik Devletleri (UltiPro olmayan) etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="266ba-153">On the **Perception United States (Non-UltiPro) Domain and URLs** section, perform the following steps:</span></span>

    ![Algısına Amerika Birleşik Devletleri (UltiPro olmayan) etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_url.png)

    <span data-ttu-id="266ba-155">a.</span><span class="sxs-lookup"><span data-stu-id="266ba-155">a.</span></span> <span data-ttu-id="266ba-156">İçinde **tanımlayıcısı** metin kutusuna, URL'yi yazın:`https://perception.kanjoya.com/sp`</span><span class="sxs-lookup"><span data-stu-id="266ba-156">In the **Identifier** textbox, type the URL: `https://perception.kanjoya.com/sp`</span></span>

    <span data-ttu-id="266ba-157">b.</span><span class="sxs-lookup"><span data-stu-id="266ba-157">b.</span></span> <span data-ttu-id="266ba-158">İçinde **yanıt URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://perception.kanjoya.com/sso?idp=<entity_id>`</span><span class="sxs-lookup"><span data-stu-id="266ba-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://perception.kanjoya.com/sso?idp=<entity_id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="266ba-159">Değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="266ba-159">The value is not real.</span></span> <span data-ttu-id="266ba-160">Değer, gerçek yanıt, öğreticide daha sonra açıklanan URL ile güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="266ba-160">You will update the value with the actual Reply URL, which is explained later in the tutorial.</span></span>
 
4. <span data-ttu-id="266ba-161">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="266ba-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Sertifika indirme bağlantısı](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_certificate.png) 

5. <span data-ttu-id="266ba-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="266ba-163">Click **Save** button.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="266ba-165">Üzerinde **algısına Amerika Birleşik Devletleri (Non-UltiPro) yapılandırma** 'yi tıklatın **yapılandırma algısına Amerika Birleşik Devletleri (Non-UltiPro)** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="266ba-165">On the **Perception United States (Non-UltiPro) Configuration** section, click **Configure Perception United States (Non-UltiPro)** to open **Configure sign-on** window.</span></span> <span data-ttu-id="266ba-166">Kopya **SAML varlık kimliği** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="266ba-166">Copy the **SAML Entity ID** from the **Quick Reference section.**</span></span>

    <span data-ttu-id="266ba-167">a.</span><span class="sxs-lookup"><span data-stu-id="266ba-167">a.</span></span> <span data-ttu-id="266ba-168">**Algısına Amerika Birleşik Devletleri (Non-UltiPro)** uygulama gerektirir **SAML varlık kimliği** uri ile kodlanan olması için kopyaladığınız değeri.</span><span class="sxs-lookup"><span data-stu-id="266ba-168">The **Perception United States (Non-UltiPro)** application requires the **SAML Entity ID** value, which you have copied, to be uri encoded.</span></span> <span data-ttu-id="266ba-169">Uri ile kodlanan değerini almak için aşağıdaki bağlantıyı kullanın:**http://www.url-encode-decode.com/**.</span><span class="sxs-lookup"><span data-stu-id="266ba-169">To get the uri encoded value, use the following link:**http://www.url-encode-decode.com/**.</span></span>

    <span data-ttu-id="266ba-170">b.</span><span class="sxs-lookup"><span data-stu-id="266ba-170">b.</span></span> <span data-ttu-id="266ba-171">URI edindikten sonra kodlanmış değeriyle birleştiğinde ile **yanıt URL'si** aşağıdaki - belirtildiği gibi</span><span class="sxs-lookup"><span data-stu-id="266ba-171">After getting the uri encoded value combine it with the **Reply URL** as mentioned below-</span></span>

    `https://perception.kanjoya.com/sso?idp=<URI encooded entity_id>`
    
    <span data-ttu-id="266ba-172">c.</span><span class="sxs-lookup"><span data-stu-id="266ba-172">c.</span></span> <span data-ttu-id="266ba-173">Yukarıdaki değeri yapıştırın **yanıt URL'si** metin kutusuna **algısına Amerika Birleşik Devletleri (UltiPro olmayan) etki alanı ve URL'leri** bölümü.</span><span class="sxs-lookup"><span data-stu-id="266ba-173">Paste the above value in the **Reply URL** textbox in **Perception United States (Non-UltiPro) Domain and URLs** section.</span></span>

    ![Algısına Amerika Birleşik Devletleri (UltiPro olmayan) yapılandırma](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_configure.png) 

7. <span data-ttu-id="266ba-175">Başka bir tarayıcı penceresinde algısına Amerika Birleşik Devletleri (Non-UltiPro) şirket sitenize yönetici olarak oturum açma.</span><span class="sxs-lookup"><span data-stu-id="266ba-175">In another browser window, sign on to your Perception United States (Non-UltiPro) company site as an administrator.</span></span>

8. <span data-ttu-id="266ba-176">Ana araç çubuğunda tıklatın **hesap ayarlarını**.</span><span class="sxs-lookup"><span data-stu-id="266ba-176">In the main toolbar, click **Account Settings**.</span></span>

    ![Algısına Amerika Birleşik Devletleri (Non-UltiPro) kullanıcı](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_user.png)

9. <span data-ttu-id="266ba-178">Üzerinde **hesap ayarlarını** sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="266ba-178">On the **Account Settings** page, perform the following steps:</span></span>

    ![Algısına Amerika Birleşik Devletleri (Non-UltiPro) kullanıcı](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_account.png)

    <span data-ttu-id="266ba-180">a.</span><span class="sxs-lookup"><span data-stu-id="266ba-180">a.</span></span> <span data-ttu-id="266ba-181">İçinde **şirket adı** metin kutusuna, adı **şirket**.</span><span class="sxs-lookup"><span data-stu-id="266ba-181">In the **Company Name** textbox, type the name of the **Company**.</span></span>
    
    <span data-ttu-id="266ba-182">b.</span><span class="sxs-lookup"><span data-stu-id="266ba-182">b.</span></span> <span data-ttu-id="266ba-183">İçinde **hesap adı** metin kutusuna, adı **hesap**.</span><span class="sxs-lookup"><span data-stu-id="266ba-183">In the **Account Name** textbox, type the name of the **Account**.</span></span>

    <span data-ttu-id="266ba-184">c.</span><span class="sxs-lookup"><span data-stu-id="266ba-184">c.</span></span> <span data-ttu-id="266ba-185">İçinde **varsayılan yanıt-e-posta** metin kutusunda, geçerli **e-posta**.</span><span class="sxs-lookup"><span data-stu-id="266ba-185">In **Default Reply-To Email** text box, type the valid **Email**.</span></span>

    <span data-ttu-id="266ba-186">d.</span><span class="sxs-lookup"><span data-stu-id="266ba-186">d.</span></span> <span data-ttu-id="266ba-187">Seçin **SSO kimlik sağlayıcısı** olarak **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="266ba-187">Select **SSO Identity Provider** as **SAML 2.0**.</span></span>

10. <span data-ttu-id="266ba-188">Üzerinde **SSO yapılandırma** sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="266ba-188">On the **SSO Configuration** page, perform the following steps:</span></span>

    ![Algısına Amerika Birleşik Devletleri (UltiPro olmayan) SSOConfig](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_ssoconfig.png)

    <span data-ttu-id="266ba-190">a.</span><span class="sxs-lookup"><span data-stu-id="266ba-190">a.</span></span> <span data-ttu-id="266ba-191">Seçin **SAML NameID türü** olarak **e-posta**.</span><span class="sxs-lookup"><span data-stu-id="266ba-191">Select **SAML NameID Type** as **EMAIL**.</span></span>

    <span data-ttu-id="266ba-192">b.</span><span class="sxs-lookup"><span data-stu-id="266ba-192">b.</span></span> <span data-ttu-id="266ba-193">İçinde **SSO yapılandırma adı** metin kutusuna, adını yazın, **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="266ba-193">In the **SSO Configuration Name** textbox, type the name of your **Configuration**.</span></span>
    
    <span data-ttu-id="266ba-194">c.</span><span class="sxs-lookup"><span data-stu-id="266ba-194">c.</span></span> <span data-ttu-id="266ba-195">İçinde **kimlik sağlayıcı adı** metin değerini yapıştırın **SAML varlık kimliği**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="266ba-195">In **Identity Provider Name** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="266ba-196">d.</span><span class="sxs-lookup"><span data-stu-id="266ba-196">d.</span></span> <span data-ttu-id="266ba-197">İçinde **SAML etki alanı metin kutusu**, etki alanı gibi girin  **@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="266ba-197">In **SAML Domain textbox**, enter the domain like **@contoso.com**.</span></span>

    <span data-ttu-id="266ba-198">e.</span><span class="sxs-lookup"><span data-stu-id="266ba-198">e.</span></span> <span data-ttu-id="266ba-199">Tıklayın **yeniden karşıya** karşıya yüklemek için **meta veri XML** dosya.</span><span class="sxs-lookup"><span data-stu-id="266ba-199">Click on **Upload Again** to upload the **Metadata XML** file.</span></span>

    <span data-ttu-id="266ba-200">f.</span><span class="sxs-lookup"><span data-stu-id="266ba-200">f.</span></span> <span data-ttu-id="266ba-201">Tıklatın **güncelleştirme**.</span><span class="sxs-lookup"><span data-stu-id="266ba-201">Click **Update**.</span></span>


> [!TIP]
> <span data-ttu-id="266ba-202">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="266ba-202">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="266ba-203">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="266ba-203">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="266ba-204">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="266ba-204">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="266ba-205">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="266ba-205">Create an Azure AD test user</span></span>

<span data-ttu-id="266ba-206">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="266ba-206">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="266ba-208">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="266ba-208">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="266ba-209">Sol bölmede, Azure portal'ı tıklatın **Azure Active Directory** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="266ba-209">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory düğmesi](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="266ba-211">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="266ba-211">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["Kullanıcılar ve Gruplar" ve "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="266ba-213">Açmak için **kullanıcı** iletişim kutusu, tıklatın **Ekle** en üstündeki **tüm kullanıcılar** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="266ba-213">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Ekle düğmesi](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="266ba-215">İçinde **kullanıcı** iletişim kutusunda, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="266ba-215">In the **User** dialog box, perform the following steps:</span></span>

    ![Kullanıcı iletişim kutusu](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_04.png)

    <span data-ttu-id="266ba-217">a.</span><span class="sxs-lookup"><span data-stu-id="266ba-217">a.</span></span> <span data-ttu-id="266ba-218">İçinde **adı** kutusuna **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="266ba-218">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="266ba-219">b.</span><span class="sxs-lookup"><span data-stu-id="266ba-219">b.</span></span> <span data-ttu-id="266ba-220">İçinde **kullanıcı adı** kullanıcı Britta Simon e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="266ba-220">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="266ba-221">c.</span><span class="sxs-lookup"><span data-stu-id="266ba-221">c.</span></span> <span data-ttu-id="266ba-222">Seçin **Göster parola** onay kutusunu işaretleyin ve ardından görüntülenen değer aşağı yazma **parola** kutusu.</span><span class="sxs-lookup"><span data-stu-id="266ba-222">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="266ba-223">d.</span><span class="sxs-lookup"><span data-stu-id="266ba-223">d.</span></span> <span data-ttu-id="266ba-224">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="266ba-224">Click **Create**.</span></span>
  
### <a name="create-a-perception-united-states-non-ultipro-test-user"></a><span data-ttu-id="266ba-225">Algısına Amerika Birleşik Devletleri (Non-UltiPro) test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="266ba-225">Create a Perception United States (Non-UltiPro) test user</span></span>

<span data-ttu-id="266ba-226">Bu bölümde, Britta Simon algısına Amerika Birleşik Devletleri (Non-UltiPro) adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="266ba-226">In this section, you create a user called Britta Simon in Perception United States (Non-UltiPro).</span></span> <span data-ttu-id="266ba-227">Çalışmak [algısına Amerika Birleşik Devletleri (Non-UltiPro) destek ekibi](http://www.ultimatesoftware.com/Contact/ContactUs) algısına Amerika Birleşik Devletleri (Non-UltiPro) platform kullanıcıları eklemek için.</span><span class="sxs-lookup"><span data-stu-id="266ba-227">Work with [Perception United States (Non-UltiPro) support team](http://www.ultimatesoftware.com/Contact/ContactUs) to add the users in the Perception United States (Non-UltiPro) platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="266ba-228">Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="266ba-228">Assign the Azure AD test user</span></span>

<span data-ttu-id="266ba-229">Bu bölümde, Britta algısına Amerika Birleşik Devletleri (Non-UltiPro) erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="266ba-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Perception United States (Non-UltiPro).</span></span>

![Kullanıcı rolü atayın][200] 

<span data-ttu-id="266ba-231">**Britta Simon algısına Amerika Birleşik Devletleri (Non-UltiPro) atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="266ba-231">**To assign Britta Simon to Perception United States (Non-UltiPro), perform the following steps:**</span></span>

1. <span data-ttu-id="266ba-232">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="266ba-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="266ba-234">Uygulamalar listesinde **algısına Amerika Birleşik Devletleri (Non-UltiPro)**.</span><span class="sxs-lookup"><span data-stu-id="266ba-234">In the applications list, select **Perception United States (Non-UltiPro)**.</span></span>

    ![Uygulamalar listesinde algısına Amerika Birleşik Devletleri (Non-UltiPro) bağlantısı](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_app.png)  

3. <span data-ttu-id="266ba-236">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="266ba-236">In the menu on the left, click **Users and groups**.</span></span>

    !["Kullanıcılar ve Gruplar" bağlantı][202]

4. <span data-ttu-id="266ba-238">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="266ba-238">Click **Add** button.</span></span> <span data-ttu-id="266ba-239">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="266ba-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Ekleme atama bölmesi][203]

5. <span data-ttu-id="266ba-241">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="266ba-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="266ba-242">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="266ba-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="266ba-243">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="266ba-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="266ba-244">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="266ba-244">Test single sign-on</span></span>

<span data-ttu-id="266ba-245">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="266ba-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="266ba-246">Erişim paneli algısına Amerika Birleşik Devletleri (Non-UltiPro) parçasında tıklattığınızda, otomatik olarak algısına Amerika Birleşik Devletleri (Non-UltiPro) uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="266ba-246">When you click the Perception United States (Non-UltiPro) tile in the Access Panel, you should get automatically signed-on to your Perception United States (Non-UltiPro) application.</span></span>
<span data-ttu-id="266ba-247">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="266ba-247">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="266ba-248">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="266ba-248">Additional resources</span></span>

* [<span data-ttu-id="266ba-249">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="266ba-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="266ba-250">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="266ba-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_203.png

