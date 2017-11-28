---
title: "Öğretici: Azure Active Directory Tümleştirme ile DigiCert | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile DigiCert arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 646f3129-aa67-4875-9073-1d0b6a3173d9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: 2ceb3c0833edcd4ecd875c5e8006961ed7216c66
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-digicert"></a><span data-ttu-id="ab3ac-103">Öğretici: Azure Active Directory Tümleştirme DigiCert ile</span><span class="sxs-lookup"><span data-stu-id="ab3ac-103">Tutorial: Azure Active Directory integration with DigiCert</span></span>

<span data-ttu-id="ab3ac-104">Bu öğreticide, Azure Active Directory (Azure AD) ile DigiCert tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-104">In this tutorial, you learn how to integrate DigiCert with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ab3ac-105">DigiCert Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="ab3ac-105">Integrating DigiCert with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ab3ac-106">DigiCert erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="ab3ac-106">You can control in Azure AD who has access to DigiCert</span></span>
- <span data-ttu-id="ab3ac-107">Otomatik olarak için DigiCert (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="ab3ac-107">You can enable your users to automatically get signed-on to DigiCert (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ab3ac-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="ab3ac-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ab3ac-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ab3ac-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ab3ac-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ab3ac-110">Prerequisites</span></span>

<span data-ttu-id="ab3ac-111">Azure AD tümleştirme DigiCert ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="ab3ac-111">To configure Azure AD integration with DigiCert, you need the following items:</span></span>

- <span data-ttu-id="ab3ac-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="ab3ac-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ab3ac-113">Bir DigiCert çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="ab3ac-113">A DigiCert single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ab3ac-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ab3ac-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="ab3ac-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ab3ac-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ab3ac-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ab3ac-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ab3ac-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="ab3ac-118">Scenario description</span></span>
<span data-ttu-id="ab3ac-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ab3ac-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="ab3ac-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ab3ac-121">Galeriden DigiCert ekleme</span><span class="sxs-lookup"><span data-stu-id="ab3ac-121">Adding DigiCert from the gallery</span></span>
2. <span data-ttu-id="ab3ac-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="ab3ac-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-digicert-from-the-gallery"></a><span data-ttu-id="ab3ac-123">Galeriden DigiCert ekleme</span><span class="sxs-lookup"><span data-stu-id="ab3ac-123">Adding DigiCert from the gallery</span></span>
<span data-ttu-id="ab3ac-124">Azure AD DigiCert tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden DigiCert eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-124">To configure the integration of DigiCert into Azure AD, you need to add DigiCert from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ab3ac-125">**Galeriden DigiCert eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ab3ac-125">**To add DigiCert from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ab3ac-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ab3ac-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ab3ac-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="ab3ac-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="ab3ac-133">Arama kutusuna **DigiCert**.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-133">In the search box, type **DigiCert**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_search.png)

5. <span data-ttu-id="ab3ac-135">Sonuçlar panelinde seçin **DigiCert**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-135">In the results panel, select **DigiCert**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ab3ac-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="ab3ac-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ab3ac-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı DigiCert ile test etme</span><span class="sxs-lookup"><span data-stu-id="ab3ac-138">In this section, you configure and test Azure AD single sign-on with DigiCert based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ab3ac-139">Tekli çalışmaya oturum için Azure AD DigiCert karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-139">For single sign-on to work, Azure AD needs to know what the counterpart user in DigiCert is to a user in Azure AD.</span></span> <span data-ttu-id="ab3ac-140">Diğer bir deyişle, bir Azure AD kullanıcısının DigiCert ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-140">In other words, a link relationship between an Azure AD user and the related user in DigiCert needs to be established.</span></span>

<span data-ttu-id="ab3ac-141">DigiCert içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-141">In DigiCert, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ab3ac-142">Yapılandırma ve Azure AD çoklu oturum açma DigiCert ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="ab3ac-142">To configure and test Azure AD single sign-on with DigiCert, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ab3ac-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ab3ac-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ab3ac-145">**[DigiCert test kullanıcısı oluşturma](#creating-a-digicert-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı DigiCert sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-145">**[Creating a DigiCert test user](#creating-a-digicert-test-user)** - to have a counterpart of Britta Simon in DigiCert that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ab3ac-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ab3ac-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ab3ac-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ab3ac-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ab3ac-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma DigiCert uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your DigiCert application.</span></span>

<span data-ttu-id="ab3ac-150">**Azure AD çoklu oturum açma ile DigiCert yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ab3ac-150">**To configure Azure AD single sign-on with DigiCert, perform the following steps:**</span></span>

1. <span data-ttu-id="ab3ac-151">Azure portalında üzerinde **DigiCert** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-151">In the Azure portal, on the **DigiCert** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="ab3ac-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_samlbase.png)

3. <span data-ttu-id="ab3ac-155">Üzerinde **DigiCert etki alanı ve URL'leri** bölümü, kullanıcı gerekmez uygulama zaten Azure ile önceden tümleştirilmiş gibi tüm adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-155">On the **DigiCert Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_url.png)

4. <span data-ttu-id="ab3ac-157">DigiCert uygulaması SAML onaylar belirli bir biçimde bekliyor.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-157">DigiCert application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="ab3ac-158">Bu uygulama için aşağıdaki talep yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-158">Configure the following claims for this application.</span></span> <span data-ttu-id="ab3ac-159">Bu öznitelik değerlerini yönetebilirsiniz "**kullanıcı öznitelikleri**" uygulama tümleştirmesi sayfasında bölüm.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-159">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="ab3ac-160">Aşağıdaki ekran görüntüsünde, bu yapılandırma için bir örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-160">The following screenshot shows an example for this configuration.</span></span> 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_attributes.png)
    
5. <span data-ttu-id="ab3ac-162">İçinde **kullanıcı öznitelikleri** bölümünde **çoklu oturum açma** iletişim kutusunda, SAML belirteci özniteliği görüntüde gösterildiği gibi yapılandırın ve aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="ab3ac-162">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="ab3ac-163">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="ab3ac-163">Attribute Name</span></span> | <span data-ttu-id="ab3ac-164">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="ab3ac-164">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="ab3ac-165">Şirket</span><span class="sxs-lookup"><span data-stu-id="ab3ac-165">company</span></span> | <span data-ttu-id="ab3ac-166">< companycode ></span><span class="sxs-lookup"><span data-stu-id="ab3ac-166">< companycode ></span></span> |
    | <span data-ttu-id="ab3ac-167">digicertrole</span><span class="sxs-lookup"><span data-stu-id="ab3ac-167">digicertrole</span></span> | <span data-ttu-id="ab3ac-168">CanAccessCertCentral</span><span class="sxs-lookup"><span data-stu-id="ab3ac-168">CanAccessCertCentral</span></span> |

    > [!Note]
    > <span data-ttu-id="ab3ac-169">Değeri **şirket** özniteliği gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-169">The value of **company** attribute is not real.</span></span> <span data-ttu-id="ab3ac-170">Bu değer ile gerçek şirket kodunu güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-170">Update this value with actual company code.</span></span> <span data-ttu-id="ab3ac-171">Değeri alınacak **şirket** özniteliği kişi [DigiCert destek ekibi](mailto:support@digicert.com).</span><span class="sxs-lookup"><span data-stu-id="ab3ac-171">To get the value of **company** attribute contact [DigiCert support team](mailto:support@digicert.com).</span></span>

    <span data-ttu-id="ab3ac-172">a.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-172">a.</span></span> <span data-ttu-id="ab3ac-173">Tıklatın **Ekle özniteliği** açmak için **özniteliği eklemek** iletişim.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-173">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-digicert-tutorial/tutorial_attribute_04.png)

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-digicert-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="ab3ac-176">b.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-176">b.</span></span> <span data-ttu-id="ab3ac-177">İçinde **adı** metin kutusuna, ilgili satır için gösterilen öznitelik adı yazın.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-177">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="ab3ac-178">c.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-178">c.</span></span> <span data-ttu-id="ab3ac-179">Gelen **değeri** listesinde, ilgili satır için gösterilen öznitelik değeri yazın.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-179">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="ab3ac-180">d.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-180">d.</span></span> <span data-ttu-id="ab3ac-181">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-181">Click **Ok**.</span></span> 

6. <span data-ttu-id="ab3ac-182">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-182">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_certificate.png) 

7. <span data-ttu-id="ab3ac-184">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-184">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-digicert-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="ab3ac-186">Çoklu oturum açma yapılandırmak için **DigiCert** yan, indirilen göndermek için ihtiyacınız **meta veri XML** için [DigiCert destek ekibi](mailto:support@digicert.com).</span><span class="sxs-lookup"><span data-stu-id="ab3ac-186">To configure single sign-on on **DigiCert** side, you need to send the downloaded **Metadata XML** to [DigiCert support team](mailto:support@digicert.com).</span></span> <span data-ttu-id="ab3ac-187">Bunlar, her iki tarafta da ayarlamanızı SAML SSO bağlantı sağlamak için bu ayarı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-187">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="ab3ac-188">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="ab3ac-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ab3ac-189">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ab3ac-190">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ab3ac-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ab3ac-191">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ab3ac-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="ab3ac-192">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="ab3ac-194">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ab3ac-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ab3ac-195">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-digicert-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ab3ac-197">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-digicert-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ab3ac-199">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-digicert-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ab3ac-201">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="ab3ac-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-digicert-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ab3ac-203">a.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-203">a.</span></span> <span data-ttu-id="ab3ac-204">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ab3ac-205">b.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-205">b.</span></span> <span data-ttu-id="ab3ac-206">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ab3ac-207">c.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-207">c.</span></span> <span data-ttu-id="ab3ac-208">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ab3ac-209">d.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-209">d.</span></span> <span data-ttu-id="ab3ac-210">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-210">Click **Create**.</span></span>
 
### <a name="creating-a-digicert-test-user"></a><span data-ttu-id="ab3ac-211">DigiCert test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ab3ac-211">Creating a DigiCert test user</span></span>

<span data-ttu-id="ab3ac-212">Bu bölümde, DigiCert içinde Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-212">In this section, you create a user called Britta Simon in DigiCert.</span></span> <span data-ttu-id="ab3ac-213">Lütfen çalışmak [DigiCert destek ekibi](mailto:support@digicert.com) DigiCert içinde kullanıcıları eklemek için.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-213">Please work with [DigiCert support team](mailto:support@digicert.com) to add the users in DigiCert.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ab3ac-214">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="ab3ac-214">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ab3ac-215">Bu bölümde, Britta DigiCert için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-215">In this section, you enable Britta Simon to use Azure single sign-on by granting access to DigiCert.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="ab3ac-217">**DigiCert için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ab3ac-217">**To assign Britta Simon to DigiCert, perform the following steps:**</span></span>

1. <span data-ttu-id="ab3ac-218">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-218">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="ab3ac-220">Uygulamalar listesinde **DigiCert**.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-220">In the applications list, select **DigiCert**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_app.png) 

3. <span data-ttu-id="ab3ac-222">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-222">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="ab3ac-224">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-224">Click **Add** button.</span></span> <span data-ttu-id="ab3ac-225">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-225">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="ab3ac-227">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-227">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ab3ac-228">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-228">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ab3ac-229">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-229">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ab3ac-230">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="ab3ac-230">Testing single sign-on</span></span>

<span data-ttu-id="ab3ac-231">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-231">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ab3ac-232">Erişim paneli DigiCert parçasında tıklattığınızda, otomatik olarak DeigiCert uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="ab3ac-232">When you click the DigiCert tile in the Access Panel, you should get automatically signed-on to your DeigiCert application.</span></span>
<span data-ttu-id="ab3ac-233">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ab3ac-233">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ab3ac-234">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="ab3ac-234">Additional resources</span></span>

* [<span data-ttu-id="ab3ac-235">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="ab3ac-235">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ab3ac-236">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="ab3ac-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_203.png

