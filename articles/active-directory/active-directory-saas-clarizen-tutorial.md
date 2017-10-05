---
title: "Öğretici: Azure Active Directory Tümleştirme ile Clarizen | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Clarizen arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 574c6877bddac8be7d6d541bfabbdc10f6be3101
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clarizen"></a><span data-ttu-id="e3dbe-103">Öğretici: Azure Active Directory Tümleştirme Clarizen ile</span><span class="sxs-lookup"><span data-stu-id="e3dbe-103">Tutorial: Azure Active Directory integration with Clarizen</span></span>

<span data-ttu-id="e3dbe-104">Bu öğreticide, Azure Active Directory (Azure AD) tümleştirme ile Clarizen öğrenin.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-104">In this tutorial, you learn how to integrate Azure Active Directory (Azure AD) with Clarizen.</span></span> <span data-ttu-id="e3dbe-105">Bu tümleştirme, aşağıdaki avantajları sunar:</span><span class="sxs-lookup"><span data-stu-id="e3dbe-105">This integration gives you the following benefits:</span></span>

- <span data-ttu-id="e3dbe-106">Clarizen erişebilen Azure AD'de, denetleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-106">You can control, in Azure AD, who has access to Clarizen.</span></span>
- <span data-ttu-id="e3dbe-107">Kullanıcılarınız için Clarizen (çoklu oturum açma) ile Azure AD hesaplarına otomatik olarak oturum açmanız etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-107">You can enable your users to be automatically signed in to Clarizen (single sign-on) with their Azure AD accounts.</span></span>
- <span data-ttu-id="e3dbe-108">Hesaplarınızı bir merkezi konumda, Azure portalında yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-108">You can manage your accounts in one central location, the Azure portal.</span></span>

<span data-ttu-id="e3dbe-109">Bu öğretici senaryoda iki ana görevden oluşur:</span><span class="sxs-lookup"><span data-stu-id="e3dbe-109">The scenario in this tutorial consists of two main tasks:</span></span>

1. <span data-ttu-id="e3dbe-110">Clarizen Galeriden ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-110">Add Clarizen from the gallery.</span></span>
2. <span data-ttu-id="e3dbe-111">Yapılandırma ve Azure AD çoklu oturum açmayı sınayın.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-111">Configure and test Azure AD single sign-on.</span></span>

<span data-ttu-id="e3dbe-112">Azure AD ile hizmet (SaaS) uygulaması tümleştirme olarak yazılım hakkında daha fazla bilgi istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e3dbe-112">If you want more details about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e3dbe-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e3dbe-113">Prerequisites</span></span>
<span data-ttu-id="e3dbe-114">Azure AD tümleştirme Clarizen ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="e3dbe-114">To configure Azure AD integration with Clarizen, you need the following items:</span></span>

- <span data-ttu-id="e3dbe-115">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="e3dbe-115">An Azure AD subscription</span></span>
- <span data-ttu-id="e3dbe-116">Çoklu oturum açma için etkinleştirilen Clarizen abonelik</span><span class="sxs-lookup"><span data-stu-id="e3dbe-116">A Clarizen subscription that's enabled for single sign-on</span></span>

<span data-ttu-id="e3dbe-117">Bu öğreticide adımları test etmek için aşağıdaki önerileri uygulayın:</span><span class="sxs-lookup"><span data-stu-id="e3dbe-117">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="e3dbe-118">Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-118">Test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e3dbe-119">Bu gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-119">Don't use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="e3dbe-120">Bir Azure AD test ortamı yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e3dbe-120">If you don't have an Azure AD test environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="add-clarizen-from-the-gallery"></a><span data-ttu-id="e3dbe-121">Galeriden Clarizen Ekle</span><span class="sxs-lookup"><span data-stu-id="e3dbe-121">Add Clarizen from the gallery</span></span>
<span data-ttu-id="e3dbe-122">Azure AD Clarizen tümleştirilmesi yapılandırmak için Clarizen Galeriden yönetilen SaaS uygulamaları listenize ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-122">To configure the integration of Clarizen into Azure AD, add Clarizen from the gallery to your list of managed SaaS apps.</span></span>

1. <span data-ttu-id="e3dbe-123">İçinde [Azure portal](https://portal.azure.com), sol bölmede **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-123">In the [Azure portal](https://portal.azure.com), in the left pane, click the **Azure Active Directory** icon.</span></span>

    ![Azure Active Directory simgesi][1]

2. <span data-ttu-id="e3dbe-125">Tıklatın **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-125">Click **Enterprise applications**.</span></span> <span data-ttu-id="e3dbe-126">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-126">Then click **All applications**.</span></span>

    !["Kurumsal uygulamalar" ve "Tüm uygulamalar" ı tıklatarak][2]

3. <span data-ttu-id="e3dbe-128">Tıklatın **Ekle** iletişim kutusunun üstündeki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-128">Click the **Add** button at the top of the dialog box.</span></span>

    !["Ekle" düğmesi][3]

4. <span data-ttu-id="e3dbe-130">Arama kutusuna **Clarizen**.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-130">In the search box, type **Clarizen**.</span></span>

    ![Arama kutusuna "Clarizen" yazın](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_000.png)

5. <span data-ttu-id="e3dbe-132">Sonuçlar bölmesinde seçin **Clarizen**ve ardından **Ekle** uygulama eklemek için.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-132">In the results pane, select **Clarizen**, and then click **Add** to add the application.</span></span>

    ![Sonuçlar bölmesinde Clarizen seçme](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_0001.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="e3dbe-134">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="e3dbe-134">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="e3dbe-135">Aşağıdaki bölümlerde, yapılandırma ve test kullanıcı Britta Simon tabanlı Clarizen ile Azure AD çoklu oturum açma sınayın.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-135">In the following sections, you configure and test Azure AD single sign-on with Clarizen based on the test user Britta Simon.</span></span>

<span data-ttu-id="e3dbe-136">Tekli çalışmaya oturum için Azure AD Clarizen karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-136">For single sign-on to work, Azure AD needs to know what the counterpart user in Clarizen is to a user in Azure AD.</span></span> <span data-ttu-id="e3dbe-137">Diğer bir deyişle, bir Azure AD kullanıcısının Clarizen ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-137">In other words, a link relationship between an Azure AD user and the related user in Clarizen needs to be established.</span></span> <span data-ttu-id="e3dbe-138">Değerini atayarak bu bağlantı ilişkisini kurmak **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** Clarizen içinde.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-138">You establish this link relationship by assigning the value of **user name** in Azure AD as the value of **Username** in Clarizen.</span></span>

<span data-ttu-id="e3dbe-139">Yapılandırma ve Azure AD çoklu oturum açma Clarizen ile test etmek için aşağıdaki yapı taşları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="e3dbe-139">To configure and test Azure AD single sign-on with Clarizen, complete the following building blocks:</span></span>

1. <span data-ttu-id="e3dbe-140">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-140">**[Configure Azure AD single sign-on](#configure-azure-ad-single-sign-on)** to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e3dbe-141">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e3dbe-142">**[Clarizen test kullanıcısı oluşturma](#create-a-clarizen-test-user)**  Britta Simon, karşılık gelen her, Azure AD gösterimine bağlı Clarizen sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-142">**[Create a Clarizen test user](#create-a-clarizen-test-user)** to have a counterpart of Britta Simon in Clarizen that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="e3dbe-143">**[Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  Britta Azure AD çoklu oturum açma kullanmak Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e3dbe-144">**[Test çoklu oturum açma](#test-single-sign-on)**  yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-144">**[Test single sign-on](#test-single-sign-on)** to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="e3dbe-145">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="e3dbe-145">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="e3dbe-146">Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Clarizen uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-146">Enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Clarizen application.</span></span>

1. <span data-ttu-id="e3dbe-147">Azure portalında üzerinde **Clarizen** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-147">In the Azure portal, on the **Clarizen** application integration page, click **Single sign-on**.</span></span>

    !["Çoklu oturum açma" a tıklayarak][4]

2. <span data-ttu-id="e3dbe-149">İçinde **çoklu oturum açma** iletişim kutusu için **modu**seçin **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-149">In the **Single sign-on** dialog box, for **Mode**, select **SAML-based Sign-on** to enable single sign-on.</span></span>

    !["SAML tabanlı oturum açma" seçme](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_01.png)

3. <span data-ttu-id="e3dbe-151">İçinde **Clarizen etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e3dbe-151">In the **Clarizen Domain and URLs** section, perform the following steps:</span></span>

    ![Tanımlayıcı ve yanıt URL'si için kutuları](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_02.png)

    <span data-ttu-id="e3dbe-153">a.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-153">a.</span></span> <span data-ttu-id="e3dbe-154">İçinde **tanımlayıcısı** değeri olarak yazın: **Clarizen**</span><span class="sxs-lookup"><span data-stu-id="e3dbe-154">In the **Identifier** box, type the value as: **Clarizen**</span></span>

    <span data-ttu-id="e3dbe-155">b.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-155">b.</span></span> <span data-ttu-id="e3dbe-156">İçinde **yanıt URL'si** kutusunda, bir URL şu biçimi kullanarak girin: **https://<company name>.clarizen.com/Clarizen/Pages/Integrations/SAML/SamlResponse.aspx**</span><span class="sxs-lookup"><span data-stu-id="e3dbe-156">In the **Reply URL** box, type a URL by using the following pattern: **https://<company name>.clarizen.com/Clarizen/Pages/Integrations/SAML/SamlResponse.aspx**</span></span>

    > [!NOTE]
    > <span data-ttu-id="e3dbe-157">Bunlar gerçek değerleri değildir.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-157">These are not the real values.</span></span> <span data-ttu-id="e3dbe-158">Gerçek tanımlayıcı kullanın ve URL yanıt gerekmez.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-158">You have to use the actual identifier and reply URL.</span></span> <span data-ttu-id="e3dbe-159">Burada tanımlayıcı olarak benzersiz bir dize değerini kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-159">Here we suggest that you use the unique value of a string as the identifier.</span></span> <span data-ttu-id="e3dbe-160">Gerçek değerleri almak için başvurun [Clarizen destek ekibi](https://success.clarizen.com/hc/en-us/requests/new).</span><span class="sxs-lookup"><span data-stu-id="e3dbe-160">To get the actual values, contact the [Clarizen support team](https://success.clarizen.com/hc/en-us/requests/new).</span></span>

4. <span data-ttu-id="e3dbe-161">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **yeni sertifika oluştur**.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-161">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    !["Yeni Sertifika Oluştur" a tıklayarak](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_03.png)  

5. <span data-ttu-id="e3dbe-163">İçinde **yeni sertifika oluştur** iletişim kutusunda, takvim simgesini tıklatın ve bir süre sonu tarihi seçin.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-163">In the **Create New Certificate** dialog box, click the calendar icon and select an expiry date.</span></span> <span data-ttu-id="e3dbe-164">Daha sonra **Kaydet**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-164">Then click **Save**.</span></span>

    ![Seçme ve sona erme tarihi kaydetme](./media/active-directory-saas-clarizen-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="e3dbe-166">İçinde **SAML imzalama sertifikası** bölümünde, select **yeni sertifika etkin hale getirin**ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-166">In the **SAML Signing Certificate** section, select **Make new certificate active**, and then click **Save**.</span></span>

    ![Yeni sertifika etkin hale getirme için onay kutusunu işaretleyerek](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_04.png)

7. <span data-ttu-id="e3dbe-168">İçinde **geçiş sertifikası** iletişim kutusu, tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-168">In the **Rollover certificate** dialog box, click **OK**.</span></span>

    ![Sertifikayı etkinleştirmek istediğinizi onaylamak için "Tamam" a tıklayarak](./media/active-directory-saas-clarizen-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="e3dbe-170">İçinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-170">In the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    !["Yüklemeyi başlatmak için sertifika (Base64)" a tıklayarak](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_05.png)

9. <span data-ttu-id="e3dbe-172">İçinde **Clarizen yapılandırma** 'yi tıklatın **yapılandırma Clarizen** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-172">In the **Clarizen Configuration** section, click **Configure Clarizen** to open the **Configure sign-on** window.</span></span>

    !["Clarizen Yapılandır" a tıklayarak](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_06.png)

    !["Oturum açma yapılandırma" penceresinde, dosyaları ve URL'leri dahil](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_07.png)

10. <span data-ttu-id="e3dbe-175">Farklı web tarayıcısı penceresinde Clarizen şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-175">In a different web browser window, sign in to your Clarizen company site as an administrator.</span></span>

11. <span data-ttu-id="e3dbe-176">Kullanıcı adınıza tıklayın ve ardından **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-176">Click your username, and then click **Settings**.</span></span>

    <span data-ttu-id="e3dbe-177">![Kullanıcı adınızı "Ayarlar"'ı tıklatarak](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_001.png "ayarları")</span><span class="sxs-lookup"><span data-stu-id="e3dbe-177">![Clicking "Settings" under your username](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_001.png "Settings")</span></span>

12. <span data-ttu-id="e3dbe-178">Tıklatın **genel ayarları** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-178">Click the **Global Settings** tab.</span></span> <span data-ttu-id="e3dbe-179">Ardından yanına **şirket dışı kimlik doğrulaması**, tıklatın **Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-179">Then, next to **Federated Authentication**, click **edit**.</span></span>

    <span data-ttu-id="e3dbe-180">!["Genel ayarları" sekmesini](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_002.png "genel ayarları")</span><span class="sxs-lookup"><span data-stu-id="e3dbe-180">!["Global Settings" tab](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_002.png "Global Settings")</span></span>

13. <span data-ttu-id="e3dbe-181">İçinde **şirket dışı kimlik doğrulaması** iletişim kutusunda, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e3dbe-181">In the **Federated Authentication** dialog box, perform the following steps:</span></span>

    <span data-ttu-id="e3dbe-182">!["Federe kimlik doğrulaması" iletişim kutusu](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_003.png "şirket dışı kimlik doğrulaması")</span><span class="sxs-lookup"><span data-stu-id="e3dbe-182">!["Federated Authentication" dialog box](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_003.png "Federated Authentication")</span></span>

    <span data-ttu-id="e3dbe-183">a.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-183">a.</span></span> <span data-ttu-id="e3dbe-184">Seçin **etkinleştir federe kimlik doğrulaması**.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-184">Select **Enable Federated Authentication**.</span></span>

    <span data-ttu-id="e3dbe-185">b.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-185">b.</span></span> <span data-ttu-id="e3dbe-186">Tıklatın **karşıya** indirilen sertifikanızı karşıya yüklemek için.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-186">Click **Upload** to upload your downloaded certificate.</span></span>

    <span data-ttu-id="e3dbe-187">c.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-187">c.</span></span> <span data-ttu-id="e3dbe-188">İçinde **oturum açma URL'si** kutusunda, değeri girin **SAML çoklu oturum açma hizmet URL'si** Azure AD uygulama yapılandırma penceresinden.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-188">In the **Sign-in URL** box, enter the value of **SAML Single Sign-On Service URL** from the Azure AD application configuration window.</span></span>

    <span data-ttu-id="e3dbe-189">d.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-189">d.</span></span> <span data-ttu-id="e3dbe-190">İçinde **Sign-out URL** kutusunda, değeri girin **Sign-Out URL** Azure AD uygulama yapılandırma penceresinden.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-190">In the **Sign-out URL** box, enter the value of **Sign-Out URL** from the Azure AD application configuration window.</span></span>

    <span data-ttu-id="e3dbe-191">e.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-191">e.</span></span> <span data-ttu-id="e3dbe-192">Seçin **POST kullanmak**.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-192">Select **Use POST**.</span></span>

    <span data-ttu-id="e3dbe-193">f.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-193">f.</span></span> <span data-ttu-id="e3dbe-194">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-194">Click **Save**.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="e3dbe-195">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e3dbe-195">Create an Azure AD test user</span></span>
<span data-ttu-id="e3dbe-196">Azure portalında Britta Simon adlı bir test kullanıcısı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-196">In the Azure portal, create a test user called Britta Simon.</span></span>

![Azure AD test kullanıcı adı ve e-posta adresi][100]

1. <span data-ttu-id="e3dbe-198">Sol bölmede, Azure portal'ı tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-198">In the Azure portal, in the left pane, click the **Azure Active Directory** icon.</span></span>

    ![Azure Active Directory simgesi](./media/active-directory-saas-clarizen-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="e3dbe-200">Tıklatın **kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar** kullanıcıların listesini görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-200">Click **Users and groups**, and then click **All users** to display the list of users.</span></span>

    !["Kullanıcılar ve Gruplar" ve "Tüm kullanıcılar"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="e3dbe-202">İletişim kutusunun üstündeki **Ekle** açmak için **kullanıcı** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-202">At the top of the dialog box, click **Add** to open the **User** dialog box.</span></span>

    !["Ekle" düğmesi](./media/active-directory-saas-clarizen-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="e3dbe-204">İçinde **kullanıcı** iletişim kutusunda, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e3dbe-204">In the **User** dialog box, perform the following steps:</span></span>

    !["Kullanıcı" iletişim kutusu adı, e-posta adresi ve parola ile doldurulur](./media/active-directory-saas-clarizen-tutorial/create_aaduser_04.png)

    <span data-ttu-id="e3dbe-206">a.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-206">a.</span></span> <span data-ttu-id="e3dbe-207">İçinde **adı** kutusuna **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-207">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e3dbe-208">b.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-208">b.</span></span> <span data-ttu-id="e3dbe-209">İçinde **kullanıcı adı** Britta Simon hesabın e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-209">In the **User name** box, type the email address of the Britta Simon account.</span></span>

    <span data-ttu-id="e3dbe-210">c.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-210">c.</span></span> <span data-ttu-id="e3dbe-211">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-211">Select **Show Password** and write down the value of **Password**.</span></span>

    <span data-ttu-id="e3dbe-212">d.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-212">d.</span></span> <span data-ttu-id="e3dbe-213">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-213">Click **Create**.</span></span>

### <a name="create-a-clarizen-test-user"></a><span data-ttu-id="e3dbe-214">Clarizen test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e3dbe-214">Create a Clarizen test user</span></span>
<span data-ttu-id="e3dbe-215">Azure AD için Clarizen oturum açmalarını etkinleştirmek için kullanıcı hesapları hazırlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-215">To enable Azure AD users to sign in to Clarizen, you must provision user accounts.</span></span> <span data-ttu-id="e3dbe-216">Clarizen söz konusu olduğunda, sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-216">In the case of Clarizen, provisioning is a manual task.</span></span>

1. <span data-ttu-id="e3dbe-217">Clarizen şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-217">Sign in to your Clarizen company site as an administrator.</span></span>

2. <span data-ttu-id="e3dbe-218">Tıklatın **kişiler**.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-218">Click **People**.</span></span>

    <span data-ttu-id="e3dbe-219">!["Kişiler" tıklatarak](./media/active-directory-saas-clarizen-tutorial/create_aaduser_001.png "kişiler")</span><span class="sxs-lookup"><span data-stu-id="e3dbe-219">![Clicking "People"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_001.png "People")</span></span>

3. <span data-ttu-id="e3dbe-220">Tıklatın **davet kullanıcı**.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-220">Click **Invite User**.</span></span>

    <span data-ttu-id="e3dbe-221">!["Kullanıcı davet" düğmesine](./media/active-directory-saas-clarizen-tutorial/create_aaduser_002.png "kullanıcıları davet et")</span><span class="sxs-lookup"><span data-stu-id="e3dbe-221">!["Invite User" button](./media/active-directory-saas-clarizen-tutorial/create_aaduser_002.png "Invite Users")</span></span>

4. <span data-ttu-id="e3dbe-222">İçinde **kişileri davet** iletişim kutusunda, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e3dbe-222">In the **Invite People** dialog box, perform the following steps:</span></span>

    <span data-ttu-id="e3dbe-223">!["Kişileri davet edin" iletişim kutusu](./media/active-directory-saas-clarizen-tutorial/create_aaduser_003.png "kişileri davet edin")</span><span class="sxs-lookup"><span data-stu-id="e3dbe-223">!["Invite People" dialog box](./media/active-directory-saas-clarizen-tutorial/create_aaduser_003.png "Invite People")</span></span>

    <span data-ttu-id="e3dbe-224">a.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-224">a.</span></span> <span data-ttu-id="e3dbe-225">İçinde **e-posta** Britta Simon hesabın e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-225">In the **Email** box, type the email address of the Britta Simon account.</span></span>

    <span data-ttu-id="e3dbe-226">b.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-226">b.</span></span> <span data-ttu-id="e3dbe-227">Tıklatın **davet**.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-227">Click **Invite**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e3dbe-228">Azure Active Directory hesap sahibi bir e-posta alır ve onu etkinleştirilmeden önce kendi hesabı onaylamak için bağlantıyı izleyin.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-228">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="e3dbe-229">Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="e3dbe-229">Assign the Azure AD test user</span></span>
<span data-ttu-id="e3dbe-230">Britta Clarizen için kendi erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-230">Enable Britta Simon to use Azure single sign-on by granting her access to Clarizen.</span></span>

![Atanan test kullanıcısı][200]

1. <span data-ttu-id="e3dbe-232">Azure portal, Aç uygulamaları görüntülemek, dizin görüntülemek için Gözat'ı tıklatın **kurumsal uygulamalar**ve ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-232">In the Azure portal, open the applications view, browse to the directory view, click **Enterprise applications**, and then click **All applications**.</span></span>

    !["Kurumsal uygulamalar" ve "Tüm uygulamalar" ı tıklatarak][201]

2. <span data-ttu-id="e3dbe-234">Uygulamalar listesinde **Clarizen**.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-234">In the applications list, select **Clarizen**.</span></span>

    ![Listede Clarizen seçme](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_50.png)

3. <span data-ttu-id="e3dbe-236">Sol bölmede **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-236">In the left pane, click **Users and groups**.</span></span>

    !["Kullanıcılar ve Gruplar" a tıklayarak][202]

4. <span data-ttu-id="e3dbe-238">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-238">Click the **Add** button.</span></span> <span data-ttu-id="e3dbe-239">Ardından **eklemek atama** iletişim kutusunda **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-239">Then, in the **Add Assignment** dialog box, select **Users and groups**.</span></span>

    !["Ekle" düğmesi ve "Atama Ekle" iletişim kutusu][203]

5. <span data-ttu-id="e3dbe-241">İçinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcılar listesinde.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-241">In the **Users and groups** dialog box, select **Britta Simon** in the list of users.</span></span>

6. <span data-ttu-id="e3dbe-242">İçinde **kullanıcılar ve gruplar** iletişim kutusu, tıklatın **seçin** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-242">In the **Users and groups** dialog box, click the **Select** button.</span></span>

7. <span data-ttu-id="e3dbe-243">İçinde **eklemek atama** iletişim kutusu, tıklatın **atamak** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-243">In the **Add Assignment** dialog box, click the **Assign** button.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="e3dbe-244">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="e3dbe-244">Test single sign-on</span></span>
<span data-ttu-id="e3dbe-245">Azure AD çoklu oturum açma yapılandırmanızı erişim paneli kullanarak sınayın.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-245">Test your Azure AD single sign-on configuration by using the Access Panel.</span></span>

<span data-ttu-id="e3dbe-246">Erişim paneli Clarizen parçasında tıklattığınızda, otomatik olarak Clarizen uygulamanıza oturum açmanız.</span><span class="sxs-lookup"><span data-stu-id="e3dbe-246">When you click the Clarizen tile in the Access Panel, you should be automatically signed in to your Clarizen application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e3dbe-247">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="e3dbe-247">Additional resources</span></span>

* [<span data-ttu-id="e3dbe-248">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="e3dbe-248">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e3dbe-249">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="e3dbe-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_203.png
