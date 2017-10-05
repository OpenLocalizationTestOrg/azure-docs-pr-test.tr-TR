---
title: "Öğretici: Azure Active Directory Tümleştirme ile ön | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ve ön arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 88270b6d-2571-434a-b139-b6ccc3a2b19f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: d936bc50a66ac2a3c17038ff08351edf9902c99f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-front"></a><span data-ttu-id="c2438-103">Öğretici: Azure Active Directory Tümleştirme ön ile</span><span class="sxs-lookup"><span data-stu-id="c2438-103">Tutorial: Azure Active Directory integration with Front</span></span>

<span data-ttu-id="c2438-104">Bu öğreticide, Azure Active Directory (Azure AD) ile ön tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="c2438-104">In this tutorial, you learn how to integrate Front with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c2438-105">Ön Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="c2438-105">Integrating Front with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c2438-106">Ön erişimi, Azure AD'de kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c2438-106">You can control in Azure AD who has access to Front.</span></span>
- <span data-ttu-id="c2438-107">Otomatik olarak öne (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c2438-107">You can enable your users to automatically get signed-on to Front (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="c2438-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="c2438-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="c2438-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c2438-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c2438-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="c2438-110">Prerequisites</span></span>

<span data-ttu-id="c2438-111">Azure AD tümleştirme ön ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="c2438-111">To configure Azure AD integration with Front, you need the following items:</span></span>

- <span data-ttu-id="c2438-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="c2438-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c2438-113">Bir ön çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="c2438-113">A Front single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c2438-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="c2438-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c2438-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="c2438-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c2438-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="c2438-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c2438-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c2438-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c2438-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="c2438-118">Scenario description</span></span>
<span data-ttu-id="c2438-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="c2438-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c2438-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="c2438-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c2438-121">Galeriden ön ekleme</span><span class="sxs-lookup"><span data-stu-id="c2438-121">Adding Front from the gallery</span></span>
2. <span data-ttu-id="c2438-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="c2438-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-front-from-the-gallery"></a><span data-ttu-id="c2438-123">Galeriden ön ekleme</span><span class="sxs-lookup"><span data-stu-id="c2438-123">Adding Front from the gallery</span></span>
<span data-ttu-id="c2438-124">Azure AD Önden tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden ön eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c2438-124">To configure the integration of Front into Azure AD, you need to add Front from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c2438-125">**Galeriden ön eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c2438-125">**To add Front from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c2438-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="c2438-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory düğmesi][1]

2. <span data-ttu-id="c2438-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="c2438-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c2438-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="c2438-129">Then go to **All applications**.</span></span>

    ![Kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="c2438-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c2438-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Yeni Uygulama düğmesi][3]

4. <span data-ttu-id="c2438-133">Arama kutusuna **ön**seçin **ön** sonuç panelinden ardından **Ekle** uygulama eklemek için düğmeyi.</span><span class="sxs-lookup"><span data-stu-id="c2438-133">In the search box, type **Front**, select **Front** from result panel then click **Add** button to add the application.</span></span>

    ![Sonuçlar listesinde ön](./media/active-directory-saas-front-tutorial/tutorial_front_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="c2438-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="c2438-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="c2438-136">Bu bölümde, yapılandırmak ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı ön sınayın.</span><span class="sxs-lookup"><span data-stu-id="c2438-136">In this section, you configure and test Azure AD single sign-on with Front based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c2438-137">Tekli çalışmaya oturum için Azure AD ne karşılık gelen önde bir kullanıcı için Azure AD içinde olduğu bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="c2438-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Front is to a user in Azure AD.</span></span> <span data-ttu-id="c2438-138">Diğer bir deyişle, bir Azure AD kullanıcısının ve önde ilgili kullanıcı arasındaki bağlantıyı ilişki kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c2438-138">In other words, a link relationship between an Azure AD user and the related user in Front needs to be established.</span></span>

<span data-ttu-id="c2438-139">Önde, değeri atamak **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="c2438-139">In Front, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c2438-140">Yapılandırma ve Azure AD çoklu oturum açma ile ön test etmek için aşağıdaki yapı taşları tamamlanması gerekir:</span><span class="sxs-lookup"><span data-stu-id="c2438-140">To configure and test Azure AD single sign-on with Front, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c2438-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="c2438-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c2438-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="c2438-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c2438-143">**[Ön test kullanıcısı oluşturma](#create-a-front-test-user)**  - kullanıcı Azure AD gösterimini bağlantılı bir karşılık gelen Britta Simon, önde sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="c2438-143">**[Create a Front test user](#create-a-front-test-user)** - to have a counterpart of Britta Simon in Front that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c2438-144">**[Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="c2438-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c2438-145">**[Test çoklu oturum açma](#test-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="c2438-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="c2438-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="c2438-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="c2438-147">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma ön uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="c2438-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Front application.</span></span>

<span data-ttu-id="c2438-148">**Azure AD çoklu oturum açma ile ön yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c2438-148">**To configure Azure AD single sign-on with Front, perform the following steps:**</span></span>

1. <span data-ttu-id="c2438-149">Azure portalında üzerinde **ön** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="c2438-149">In the Azure portal, on the **Front** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. <span data-ttu-id="c2438-151">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="c2438-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-front-tutorial/tutorial_front_samlbase.png)

3. <span data-ttu-id="c2438-153">Üzerinde **ön etki alanı ve URL'leri** uygulamada yapılandırmak istiyorsanız, bölüm **IDP** modu tarafından başlatılan:</span><span class="sxs-lookup"><span data-stu-id="c2438-153">On the **Front Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-front-tutorial/tutorial_front_url1.png)

    <span data-ttu-id="c2438-155">a.</span><span class="sxs-lookup"><span data-stu-id="c2438-155">a.</span></span> <span data-ttu-id="c2438-156">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<companyname>.frontapp.com`</span><span class="sxs-lookup"><span data-stu-id="c2438-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.frontapp.com`</span></span>

    <span data-ttu-id="c2438-157">b.</span><span class="sxs-lookup"><span data-stu-id="c2438-157">b.</span></span> <span data-ttu-id="c2438-158">İçinde **yanıt URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<companyname>.frontapp.com/sso/saml/callback`</span><span class="sxs-lookup"><span data-stu-id="c2438-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.frontapp.com/sso/saml/callback`</span></span>

4. <span data-ttu-id="c2438-159">Denetleme **Göster Gelişmiş URL ayarları**, uygulamada yapılandırmak istiyorsanız **SP** modunda başlatılan:</span><span class="sxs-lookup"><span data-stu-id="c2438-159">Check **Show advanced URL settings**, If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-front-tutorial/tutorial_front_url2.png)

    <span data-ttu-id="c2438-161">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<companyname>.frontapp.com`</span><span class="sxs-lookup"><span data-stu-id="c2438-161">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.frontapp.com`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="c2438-162">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="c2438-162">These values are not real.</span></span> <span data-ttu-id="c2438-163">Gerçek tanımlayıcısı, yanıt URL'si ve oturum açma URL'si daha sonra öğreticide veya kişi açıklanacak olan bu değerleri güncelleştirmek [ön istemci destek ekibi](mailto:support@frontapp.com) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="c2438-163">Update these values with the actual Identifier, Reply URL, and Sign-On URL which are explained later in tutorial or contact [Front Client support team](mailto:support@frontapp.com) to get these values.</span></span> 

5. <span data-ttu-id="c2438-164">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="c2438-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-front-tutorial/tutorial_front_certificate.png) 

6. <span data-ttu-id="c2438-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c2438-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-front-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="c2438-168">Üzerinde **ön yapılandırma** 'yi tıklatın **yapılandırma ön** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="c2438-168">On the **Front Configuration** section, click **Configure Front** to open **Configure sign-on** window.</span></span> <span data-ttu-id="c2438-169">Kopya **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="c2438-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-front-tutorial/tutorial_front_configure.png) 

8. <span data-ttu-id="c2438-171">Ön kiracınız yönetici olarak oturum.</span><span class="sxs-lookup"><span data-stu-id="c2438-171">Sign-on to your Front tenant as an administrator.</span></span>

9. <span data-ttu-id="c2438-172">Git **ayarları (dişli simgesine sol kenar) > Tercihler**.</span><span class="sxs-lookup"><span data-stu-id="c2438-172">Go to **Settings (cog icon at the bottom of the left sidebar) > Preferences**.</span></span>
   
    ![Çoklu oturum açma üzerinde uygulama tarafı yapılandırma](./media/active-directory-saas-front-tutorial/tutorial_front_000.png)

10. <span data-ttu-id="c2438-174">Tıklatın **çoklu oturum açma** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="c2438-174">Click **Single Sign On** link.</span></span>
   
    ![Çoklu oturum açma üzerinde uygulama tarafı yapılandırma](./media/active-directory-saas-front-tutorial/tutorial_front_001.png)

11. <span data-ttu-id="c2438-176">Seçin **SAML** aşağı açılan listesinde **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="c2438-176">Select **SAML** in the drop-down list of **Single Sign On**.</span></span>
   
    ![Çoklu oturum açma üzerinde uygulama tarafı yapılandırma](./media/active-directory-saas-front-tutorial/tutorial_front_002.png)

12. <span data-ttu-id="c2438-178">İçinde **giriş noktası** textbox değeri put **çoklu oturum açma hizmet URL'si** Azure AD Uygulama Yapılandırma Sihirbazı'ndan.</span><span class="sxs-lookup"><span data-stu-id="c2438-178">In the **Entry Point** textbox put the value of **Single Sign-on Service URL** from Azure AD application configuration wizard.</span></span>
    
    ![Çoklu oturum açma üzerinde uygulama tarafı yapılandırma](./media/active-directory-saas-front-tutorial/tutorial_front_003.png)

13. <span data-ttu-id="c2438-180">İndirilen açmak **Certificate(Base64)** dosyasını Not Defteri'nde, içeriğini, panoya kopyalayın ve yapıştırın kendisine **imzalama sertifikası** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="c2438-180">Open your downloaded **Certificate(Base64)** file in notepad, copy the content of it into your clipboard, and then paste it to the **Signing certificate** textbox.</span></span>
    
    ![Çoklu oturum açma üzerinde uygulama tarafı yapılandırma](./media/active-directory-saas-front-tutorial/tutorial_front_004.png)

14. <span data-ttu-id="c2438-182">Üzerinde **hizmet sağlayıcı ayarları** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="c2438-182">On the **Service provider settings** section, perform the following steps:</span></span>

    ![Çoklu oturum açma üzerinde uygulama tarafı yapılandırma](./media/active-directory-saas-front-tutorial/tutorial_front_005.png)

    <span data-ttu-id="c2438-184">a.</span><span class="sxs-lookup"><span data-stu-id="c2438-184">a.</span></span> <span data-ttu-id="c2438-185">Değerini kopyalayın **varlık kimliği** ve yapıştırın **tanımlayıcısı** metin kutusuna **ön etki alanı ve URL'leri** Azure portalı bölümünde.</span><span class="sxs-lookup"><span data-stu-id="c2438-185">Copy the value of **Entity ID** and paste it into the **Identifier** textbox in **Front Domain and URLs** section in Azure portal.</span></span>

    <span data-ttu-id="c2438-186">b.</span><span class="sxs-lookup"><span data-stu-id="c2438-186">b.</span></span> <span data-ttu-id="c2438-187">Değerini kopyalayın **ACS URL** ve yapıştırın **oturum açma URL'si** metin kutusuna **ön etki alanı ve URL'leri** Azure portalı bölümünde.</span><span class="sxs-lookup"><span data-stu-id="c2438-187">Copy the value of **ACS URL** and paste it into the **Sign-on URL** textbox in **Front Domain and URLs** section in Azure portal.</span></span>
    
15. <span data-ttu-id="c2438-188">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c2438-188">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="c2438-189">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="c2438-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c2438-190">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="c2438-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c2438-191">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c2438-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="c2438-192">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c2438-192">Create an Azure AD test user</span></span>

<span data-ttu-id="c2438-193">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="c2438-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="c2438-195">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c2438-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c2438-196">Sol bölmede, Azure portal'ı tıklatın **Azure Active Directory** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c2438-196">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory düğmesi](./media/active-directory-saas-front-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="c2438-198">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="c2438-198">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["Kullanıcılar ve Gruplar" ve "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-front-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="c2438-200">Açmak için **kullanıcı** iletişim kutusu, tıklatın **Ekle** en üstündeki **tüm kullanıcılar** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="c2438-200">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Ekle düğmesi](./media/active-directory-saas-front-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="c2438-202">İçinde **kullanıcı** iletişim kutusunda, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="c2438-202">In the **User** dialog box, perform the following steps:</span></span>

    ![Kullanıcı iletişim kutusu](./media/active-directory-saas-front-tutorial/create_aaduser_04.png)

    <span data-ttu-id="c2438-204">a.</span><span class="sxs-lookup"><span data-stu-id="c2438-204">a.</span></span> <span data-ttu-id="c2438-205">İçinde **adı** kutusuna **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c2438-205">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c2438-206">b.</span><span class="sxs-lookup"><span data-stu-id="c2438-206">b.</span></span> <span data-ttu-id="c2438-207">İçinde **kullanıcı adı** kullanıcı Britta Simon e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="c2438-207">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="c2438-208">c.</span><span class="sxs-lookup"><span data-stu-id="c2438-208">c.</span></span> <span data-ttu-id="c2438-209">Seçin **Göster parola** onay kutusunu işaretleyin ve ardından görüntülenen değer aşağı yazma **parola** kutusu.</span><span class="sxs-lookup"><span data-stu-id="c2438-209">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="c2438-210">d.</span><span class="sxs-lookup"><span data-stu-id="c2438-210">d.</span></span> <span data-ttu-id="c2438-211">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c2438-211">Click **Create**.</span></span>
 
### <a name="create-a-front-test-user"></a><span data-ttu-id="c2438-212">Ön test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c2438-212">Create a Front test user</span></span>

<span data-ttu-id="c2438-213">Bu bölümde, Britta Simon önde adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c2438-213">In this section, you create a user called Britta Simon in Front.</span></span> <span data-ttu-id="c2438-214">Çalışmak [ön istemci destek ekibi](mailto:support@frontapp.com) ön platform kullanıcıları eklemek için.</span><span class="sxs-lookup"><span data-stu-id="c2438-214">Work with [Front Client support team](mailto:support@frontapp.com) to add the users in the Front platform.</span></span> <span data-ttu-id="c2438-215">Kullanıcıların oluşturulan ve çoklu oturum açma kullanmadan önce etkinleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="c2438-215">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="c2438-216">Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="c2438-216">Assign the Azure AD test user</span></span>

<span data-ttu-id="c2438-217">Bu bölümde, Britta öne erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="c2438-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Front.</span></span>

![Kullanıcı rolü atayın][200] 

<span data-ttu-id="c2438-219">**Öne Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c2438-219">**To assign Britta Simon to Front, perform the following steps:**</span></span>

1. <span data-ttu-id="c2438-220">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="c2438-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="c2438-222">Uygulamalar listesinde **ön**.</span><span class="sxs-lookup"><span data-stu-id="c2438-222">In the applications list, select **Front**.</span></span>

    ![Uygulamalar listesinde ön bağlantı](./media/active-directory-saas-front-tutorial/tutorial_front_app.png)  

3. <span data-ttu-id="c2438-224">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="c2438-224">In the menu on the left, click **Users and groups**.</span></span>

    !["Kullanıcılar ve Gruplar" bağlantı][202]

4. <span data-ttu-id="c2438-226">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c2438-226">Click **Add** button.</span></span> <span data-ttu-id="c2438-227">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="c2438-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Ekleme atama bölmesi][203]

5. <span data-ttu-id="c2438-229">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="c2438-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c2438-230">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="c2438-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c2438-231">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="c2438-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="c2438-232">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="c2438-232">Test single sign-on</span></span>

<span data-ttu-id="c2438-233">Bu bölümün amacı, Azure AD erişim paneli kullanarak SSOconfiguration test etmektir.</span><span class="sxs-lookup"><span data-stu-id="c2438-233">The objective of this section is to test your Azure AD SSOconfiguration using the Access Panel.</span></span>

<span data-ttu-id="c2438-234">Erişim paneli ön parçasında tıklattığınızda, otomatik olarak ön uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="c2438-234">When you click the Front tile in the Access Panel, you should get automatically signed-on to your Front application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c2438-235">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="c2438-235">Additional resources</span></span>

* [<span data-ttu-id="c2438-236">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="c2438-236">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c2438-237">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="c2438-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-front-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-front-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-front-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-front-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-front-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-front-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-front-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-front-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-front-tutorial/tutorial_general_203.png

