---
title: "Öğretici: Azure Active Directory Tümleştirme ScaleX kuruluş ile | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile ScaleX kuruluş arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2379a8d-a659-45f1-87db-9ba156d83183
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2017
ms.author: jeedes
ms.openlocfilehash: 0ebed0c2605862426384c0e219e52c9d626b6246
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scalex-enterprise"></a><span data-ttu-id="36fb6-103">Öğretici: Azure Active Directory Tümleştirme ScaleX kuruluş ile</span><span class="sxs-lookup"><span data-stu-id="36fb6-103">Tutorial: Azure Active Directory integration with ScaleX Enterprise</span></span>

<span data-ttu-id="36fb6-104">Bu öğreticide, Azure Active Directory (Azure AD) ile ScaleX Kurumsal tümleştirme öğrenin.</span><span class="sxs-lookup"><span data-stu-id="36fb6-104">In this tutorial, you learn how to integrate ScaleX Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="36fb6-105">Azure AD ile ScaleX Kurumsal tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="36fb6-105">Integrating ScaleX Enterprise with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="36fb6-106">ScaleX Kurumsal erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="36fb6-106">You can control in Azure AD who has access to ScaleX Enterprise</span></span>
- <span data-ttu-id="36fb6-107">Azure AD hesaplarına otomatik olarak ScaleX kuruluş (çoklu oturum açma) açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="36fb6-107">You can enable your users to automatically get signed-on to ScaleX Enterprise (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="36fb6-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="36fb6-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="36fb6-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz.</span><span class="sxs-lookup"><span data-stu-id="36fb6-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="36fb6-110">Uygulama erişimi ve çoklu oturum açma ile nedir [Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="36fb6-110">What is application access and single sign-on with [Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="36fb6-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="36fb6-111">Prerequisites</span></span>

<span data-ttu-id="36fb6-112">Azure AD tümleştirme ScaleX Enterprise ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="36fb6-112">To configure Azure AD integration with ScaleX Enterprise, you need the following items:</span></span>

- <span data-ttu-id="36fb6-113">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="36fb6-113">An Azure AD subscription</span></span>
- <span data-ttu-id="36fb6-114">Bir ScaleX Kurumsal çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="36fb6-114">A ScaleX Enterprise single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="36fb6-115">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="36fb6-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="36fb6-116">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="36fb6-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="36fb6-117">Bu gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="36fb6-117">Do not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="36fb6-118">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="36fb6-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="36fb6-119">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="36fb6-119">Scenario description</span></span>
<span data-ttu-id="36fb6-120">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="36fb6-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="36fb6-121">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="36fb6-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="36fb6-122">Galeriden ScaleX Kurumsal ekleme</span><span class="sxs-lookup"><span data-stu-id="36fb6-122">Adding ScaleX Enterprise from the gallery</span></span>
2. <span data-ttu-id="36fb6-123">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="36fb6-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-scalex-enterprise-from-the-gallery"></a><span data-ttu-id="36fb6-124">Galeriden ScaleX Kurumsal ekleme</span><span class="sxs-lookup"><span data-stu-id="36fb6-124">Adding ScaleX Enterprise from the gallery</span></span>
<span data-ttu-id="36fb6-125">Azure ad ScaleX kuruluşta tümleştirmesini yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden ScaleX Kurumsal eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="36fb6-125">To configure the integration of ScaleX Enterprise in to Azure AD, you need to add ScaleX Enterprise from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="36fb6-126">**Galeriden ScaleX Kurumsal eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="36fb6-126">**To add ScaleX Enterprise from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="36fb6-127">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="36fb6-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="36fb6-129">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="36fb6-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="36fb6-130">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="36fb6-130">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="36fb6-132">Tıklatın **Ekle** iletişim kutusunun üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="36fb6-132">Click **Add** button on the top of the dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="36fb6-134">Arama kutusuna **ScaleX Kurumsal**.</span><span class="sxs-lookup"><span data-stu-id="36fb6-134">In the search box, type **ScaleX Enterprise**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_search.png)

5. <span data-ttu-id="36fb6-136">Sonuçlar panelinde seçin **ScaleX Kurumsal**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="36fb6-136">In the results panel, select **ScaleX Enterprise**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="36fb6-138">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="36fb6-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="36fb6-139">Bu bölümde, yapılandırmanız ve ScaleX kuruluş ile Azure AD çoklu oturum açmayı test "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı</span><span class="sxs-lookup"><span data-stu-id="36fb6-139">In this section, you configure and test Azure AD single sign-on with ScaleX Enterprise based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="36fb6-140">Tekli çalışmaya oturum için Azure AD ne karşılık gelen ScaleX kuruluştaki bir kullanıcı için Azure AD içinde olduğu bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="36fb6-140">For single sign-on to work, Azure AD needs to know what the counterpart user in ScaleX Enterprise is to a user in Azure AD.</span></span> <span data-ttu-id="36fb6-141">Diğer bir deyişle, bir Azure AD kullanıcısının ScaleX Kurumsal ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="36fb6-141">In other words, a link relationship between an Azure AD user and the related user in ScaleX Enterprise needs to be established.</span></span>

<span data-ttu-id="36fb6-142">Bu bağlantı değeri atayarak ilişkisi **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** ScaleX kuruluştaki.</span><span class="sxs-lookup"><span data-stu-id="36fb6-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ScaleX Enterprise.</span></span>

<span data-ttu-id="36fb6-143">Yapılandırma ve Azure AD çoklu oturum açma ScaleX kuruluş ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="36fb6-143">To configure and test Azure AD single sign-on with ScaleX Enterprise, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="36fb6-144">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="36fb6-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="36fb6-145">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="36fb6-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="36fb6-146">**[ScaleX Kurumsal test kullanıcısı oluşturma](#creating-a-scalex-enterprise-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı ScaleX Kurumsal sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="36fb6-146">**[Creating a ScaleX Enterprise test user](#creating-a-scalex-enterprise-test-user)** - to have a counterpart of Britta Simon in ScaleX Enterprise that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="36fb6-147">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="36fb6-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="36fb6-148">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="36fb6-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="36fb6-149">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="36fb6-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="36fb6-150">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma ScaleX Kurumsal uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="36fb6-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ScaleX Enterprise application.</span></span>

<span data-ttu-id="36fb6-151">**Azure AD çoklu oturum açma ScaleX Enterprise ile yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="36fb6-151">**To configure Azure AD single sign-on with ScaleX Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="36fb6-152">Azure portalında üzerinde **ScaleX Kurumsal** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="36fb6-152">In the Azure portal, on the **ScaleX Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="36fb6-154">Üzerinde **çoklu oturum açma** iletişim kutusunda, olarak **modu** seçin **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="36fb6-154">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_samlbase.png)

3. <span data-ttu-id="36fb6-156">Üzerinde **ScaleX kuruluş etki alanı ve URL'leri** bölümünde, uygulamada yapılandırmak istiyorsanız aşağıdaki adımları gerçekleştirin **IDP** modu tarafından başlatılan:</span><span class="sxs-lookup"><span data-stu-id="36fb6-156">On the **ScaleX Enterprise Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_url1.png)

    <span data-ttu-id="36fb6-158">a.</span><span class="sxs-lookup"><span data-stu-id="36fb6-158">a.</span></span> <span data-ttu-id="36fb6-159">İçinde **tanımlayıcısı** metin kutusuna, şu biçimi kullanarak değeri yazın:`https://platform.rescale.com/saml2/<company id>/`</span><span class="sxs-lookup"><span data-stu-id="36fb6-159">In the **Identifier** textbox, type the value using the following pattern: `https://platform.rescale.com/saml2/<company id>/`</span></span>

    <span data-ttu-id="36fb6-160">b.</span><span class="sxs-lookup"><span data-stu-id="36fb6-160">b.</span></span> <span data-ttu-id="36fb6-161">İçinde **yanıt URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://platform.rescale.com/saml2/<company id>/acs/`</span><span class="sxs-lookup"><span data-stu-id="36fb6-161">In the **Reply URL** textbox, type a URL using the following pattern: `https://platform.rescale.com/saml2/<company id>/acs/`</span></span>

4. <span data-ttu-id="36fb6-162">Denetleme **Göster Gelişmiş URL ayarları**, uygulamada yapılandırmak istiyorsanız **SP** modunda başlatılan:</span><span class="sxs-lookup"><span data-stu-id="36fb6-162">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_url2.png)

    <span data-ttu-id="36fb6-164">İçinde **oturum açma URL'si** metin kutusuna, şu biçimi kullanarak değeri yazın:`https://platform.rescale.com/saml2/<company id>/sso/`</span><span class="sxs-lookup"><span data-stu-id="36fb6-164">In the **Sign-on URL** textbox, type the value using the following pattern: `https://platform.rescale.com/saml2/<company id>/sso/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="36fb6-165">Bunlar gerçek değerleri değildir.</span><span class="sxs-lookup"><span data-stu-id="36fb6-165">These are not the real values.</span></span> <span data-ttu-id="36fb6-166">Bu değerler gerçek tanımlayıcısı, yanıt URL'si veya oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="36fb6-166">Update these values with the actual Identifier, Reply URL or Sign-On URL.</span></span> <span data-ttu-id="36fb6-167">Kişi [ScaleX Kurumsal İstemci destek ekibi](http://info.rescale.com/contact_sales) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="36fb6-167">Contact [ScaleX Enterprise Client support team](http://info.rescale.com/contact_sales) to get these values.</span></span> 

5. <span data-ttu-id="36fb6-168">SAML belirteci öznitelikleri yapılandırmanıza özel öznitelik eşlemelerini değiştirmek gerektiren belirli bir biçimde SAML onaylar ScaleX uygulamanızı bekliyor.</span><span class="sxs-lookup"><span data-stu-id="36fb6-168">Your ScaleX application expects the SAML assertions in a specific format, which requires you to modify custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="36fb6-169">Tıklatın **Görünüm ve diğer tüm kullanıcı özniteliklerini düzenleme** özel açmak için onay kutusunu öznitelikleri ayarlar.</span><span class="sxs-lookup"><span data-stu-id="36fb6-169">Click **View and edit all other user attributes** checkbox to open the custom attributes settings.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-scalexenterprise-tutorial/scalex_attributes.png)
    
    <span data-ttu-id="36fb6-171">a.</span><span class="sxs-lookup"><span data-stu-id="36fb6-171">a.</span></span> <span data-ttu-id="36fb6-172">Öznitelik sağ tıklayın **adı** ve Sil'i tıklatın.</span><span class="sxs-lookup"><span data-stu-id="36fb6-172">Right click the attribute **name** and click delete.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-scalexenterprise-tutorial/delete_attribute_name.png)

    <span data-ttu-id="36fb6-174">b.</span><span class="sxs-lookup"><span data-stu-id="36fb6-174">b.</span></span> <span data-ttu-id="36fb6-175">Tıklatın **emailaddress** öznitelik öznitelik Düzenle penceresini açın.</span><span class="sxs-lookup"><span data-stu-id="36fb6-175">Click **emailaddress** attribute to open the Edit Attribute window.</span></span> <span data-ttu-id="36fb6-176">Kendi değerini değiştirmek **user.mail** için **user.userprincipalname** ve Tamam'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="36fb6-176">Change its value from **user.mail** to **user.userprincipalname** and click Ok.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-scalexenterprise-tutorial/edit_email_attribute.png)   
    
5. <span data-ttu-id="36fb6-178">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="36fb6-178">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the Certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_certificate.png) 

6. <span data-ttu-id="36fb6-180">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="36fb6-180">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="36fb6-182">Üzerinde **ScaleX Kurumsal yapılandırma** 'yi tıklatın **ScaleX Kurumsal yapılandırma** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="36fb6-182">On the **ScaleX Enterprise Configuration** section, click **Configure ScaleX Enterprise** to open **Configure sign-on** window.</span></span> <span data-ttu-id="36fb6-183">Kopya **SAML varlık kimliği** ve **SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="36fb6-183">Copy the **SAML Entity ID** and **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_configure.png) 

8. <span data-ttu-id="36fb6-185">Çoklu oturum açma yapılandırmak için **ScaleX Kurumsal** tarafı, ScaleX Kurumsal şirket Web sitesinin yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="36fb6-185">To configure single sign-on on **ScaleX Enterprise** side, login to the ScaleX Enterprise company website as an administrator.</span></span>

9. <span data-ttu-id="36fb6-186">Menüsünü seçin ve sağ üst **Contoso Yönetim**.</span><span class="sxs-lookup"><span data-stu-id="36fb6-186">Click the menu in the upper right and select **Contoso Administration**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="36fb6-187">Contoso yalnızca bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="36fb6-187">Contoso is just an example.</span></span> <span data-ttu-id="36fb6-188">Bu, gerçek şirket adınızı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="36fb6-188">This should be your actual Company Name.</span></span> 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-scalexenterprise-tutorial/Test_Admin.png) 

10. <span data-ttu-id="36fb6-190">Seçin **tümleştirmeler** seçin ve üstteki menüden **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="36fb6-190">Select **Integrations** from the top menu and select **Single Sign-On**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-scalexenterprise-tutorial/admin_sso.png) 

11. <span data-ttu-id="36fb6-192">Form aşağıdaki gibi tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="36fb6-192">Complete the form as follows:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-scalexenterprise-tutorial/scalex_admin_save.png) 
    
    <span data-ttu-id="36fb6-194">a.</span><span class="sxs-lookup"><span data-stu-id="36fb6-194">a.</span></span> <span data-ttu-id="36fb6-195">Seçin **"SSO ile doğrulanabilir herhangi bir kullanıcı oluşturun."**</span><span class="sxs-lookup"><span data-stu-id="36fb6-195">Select **“Create any user who can authenticate with SSO.”**</span></span>

    <span data-ttu-id="36fb6-196">b.</span><span class="sxs-lookup"><span data-stu-id="36fb6-196">b.</span></span> <span data-ttu-id="36fb6-197">**Hizmet sağlayıcısı saml**: değer Yapıştır ***urn: OASIS: adları: tc: SAML:2.0:nameid-biçimi: kalıcı***</span><span class="sxs-lookup"><span data-stu-id="36fb6-197">**Service Provider saml**: Paste the value ***urn:oasis:names:tc:SAML:2.0:nameid-format:persistent***</span></span>

    <span data-ttu-id="36fb6-198">c.</span><span class="sxs-lookup"><span data-stu-id="36fb6-198">c.</span></span> <span data-ttu-id="36fb6-199">**ACS yanıt kimlik sağlayıcısı e-posta alanının adı**: değer yapıştırın`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span><span class="sxs-lookup"><span data-stu-id="36fb6-199">**Name of Identity Provider email field in ACS response**: Paste the value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span></span>

    <span data-ttu-id="36fb6-200">d.</span><span class="sxs-lookup"><span data-stu-id="36fb6-200">d.</span></span> <span data-ttu-id="36fb6-201">**Kimlik sağlayıcısı EntityDescriptor varlık Tanıtıcısı:** Yapıştır **SAML varlık kimliği** değer Azure Portalı'ndan kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="36fb6-201">**Identity Provider EntityDescriptor Entity ID:** Paste the **SAML Entity ID** value copied from the Azure portal.</span></span>

    <span data-ttu-id="36fb6-202">e.</span><span class="sxs-lookup"><span data-stu-id="36fb6-202">e.</span></span> <span data-ttu-id="36fb6-203">**Kimlik sağlayıcısı SingleSignOnService URL'si:** Yapıştır **SAML çoklu oturum açma hizmet URL'si** Azure portalından.</span><span class="sxs-lookup"><span data-stu-id="36fb6-203">**Identity Provider SingleSignOnService URL:** Paste the **SAML Single Sign-On Service URL** from the Azure portal.</span></span>

    <span data-ttu-id="36fb6-204">f.</span><span class="sxs-lookup"><span data-stu-id="36fb6-204">f.</span></span> <span data-ttu-id="36fb6-205">**Kimlik sağlayıcısı ortak X509 sertifikası:** açık X509 sertifika Not Defteri'nde Azure indirilir ve içeriği bu kutuya yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="36fb6-205">**Identity Provider public X509 certificate:** Open the X509 certificate downloaded from the Azure in notepad and paste the contents in this box.</span></span> <span data-ttu-id="36fb6-206">Sertifika içeriği ortadaki hiçbir satır sonlarını emin olun.</span><span class="sxs-lookup"><span data-stu-id="36fb6-206">Ensure there are no line breaks in the middle of the certificate contents.</span></span>
    
    <span data-ttu-id="36fb6-207">g.</span><span class="sxs-lookup"><span data-stu-id="36fb6-207">g.</span></span> <span data-ttu-id="36fb6-208">Aşağıdaki onay kutularını kontrol edin: **etkin, NameID şifrelemek ve oturum AuthnRequests.**</span><span class="sxs-lookup"><span data-stu-id="36fb6-208">Check the following checkboxes: **Enabled, Encrypt NameID and Sign AuthnRequests.**</span></span>

    <span data-ttu-id="36fb6-209">h.</span><span class="sxs-lookup"><span data-stu-id="36fb6-209">h.</span></span> <span data-ttu-id="36fb6-210">Tıklatın **güncelleştirme SSO ayarlarını** ayarları kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="36fb6-210">Click **Update SSO Settings** to save the settings.</span></span>

> [!TIP]
> <span data-ttu-id="36fb6-211">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="36fb6-211">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="36fb6-212">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="36fb6-212">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="36fb6-213">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="36fb6-213">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="36fb6-214">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="36fb6-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="36fb6-215">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="36fb6-215">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="36fb6-217">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="36fb6-217">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="36fb6-218">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="36fb6-218">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="36fb6-220">Git **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar** kullanıcıların listesini görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="36fb6-220">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="36fb6-222">İletişim kutusunun üstündeki **Ekle** açmak için **kullanıcı** iletişim.</span><span class="sxs-lookup"><span data-stu-id="36fb6-222">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="36fb6-224">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="36fb6-224">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="36fb6-226">a.</span><span class="sxs-lookup"><span data-stu-id="36fb6-226">a.</span></span> <span data-ttu-id="36fb6-227">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="36fb6-227">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="36fb6-228">b.</span><span class="sxs-lookup"><span data-stu-id="36fb6-228">b.</span></span> <span data-ttu-id="36fb6-229">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="36fb6-229">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="36fb6-230">c.</span><span class="sxs-lookup"><span data-stu-id="36fb6-230">c.</span></span> <span data-ttu-id="36fb6-231">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="36fb6-231">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="36fb6-232">d.</span><span class="sxs-lookup"><span data-stu-id="36fb6-232">d.</span></span> <span data-ttu-id="36fb6-233">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="36fb6-233">Click **Create**.</span></span>
 
### <a name="creating-a-scalex-enterprise-test-user"></a><span data-ttu-id="36fb6-234">ScaleX Kurumsal test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="36fb6-234">Creating a ScaleX Enterprise test user</span></span>

<span data-ttu-id="36fb6-235">ScaleX Kurumsal oturum açmak Azure AD kullanıcıları etkinleştirmek için bunlar içinde ScaleX kuruluş sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="36fb6-235">To enable Azure AD users to log in to ScaleX Enterprise, they must be provisioned in to ScaleX Enterprise.</span></span> <span data-ttu-id="36fb6-236">ScaleX Kurumsal durumunda sağlama otomatik bir görevdir ve el ile yapılan hiçbir adım gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="36fb6-236">In the case of ScaleX Enterprise, provisioning is an automatic task and no manual steps are required.</span></span> <span data-ttu-id="36fb6-237">SSO kimlik bilgileriyle kimlik doğrulamasını başarıyla herhangi bir kullanıcı otomatik olarak ScaleX tarafında sağlanacak.</span><span class="sxs-lookup"><span data-stu-id="36fb6-237">Any user who can successfully authenticate with SSO credentials will be automatically provisioned on the ScaleX side.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="36fb6-238">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="36fb6-238">Assigning the Azure AD test user</span></span>

<span data-ttu-id="36fb6-239">Bu bölümde, Britta ScaleX kuruluş için kullanıcı erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="36fb6-239">In this section, you enable Britta Simon to use Azure single sign-on by granting user access to ScaleX Enterprise.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="36fb6-241">**Britta Simon ScaleX kuruluş atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="36fb6-241">**To assign Britta Simon to ScaleX Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="36fb6-242">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="36fb6-242">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="36fb6-244">Uygulamalar listesinde **ScaleX Kurumsal**.</span><span class="sxs-lookup"><span data-stu-id="36fb6-244">In the applications list, select **ScaleX Enterprise**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_app.png) 

3. <span data-ttu-id="36fb6-246">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="36fb6-246">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="36fb6-248">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="36fb6-248">Click **Add** button.</span></span> <span data-ttu-id="36fb6-249">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="36fb6-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="36fb6-251">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="36fb6-251">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="36fb6-252">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="36fb6-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="36fb6-253">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="36fb6-253">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="testing-single-sign-on"></a><span data-ttu-id="36fb6-254">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="36fb6-254">Testing single sign-on</span></span>

<span data-ttu-id="36fb6-255">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="36fb6-255">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="36fb6-256">Erişim panelinde ScaleX Kurumsal kutucuğuna tıklayın, otomatik olarak imzalanmış ScaleX Kurumsal uygulamanıza açma.</span><span class="sxs-lookup"><span data-stu-id="36fb6-256">Click the ScaleX Enterprise tile in the Access Panel, you will get automatically signed-on to your ScaleX Enterprise application.</span></span> <span data-ttu-id="36fb6-257">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="36fb6-257">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="36fb6-258">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="36fb6-258">Additional resources</span></span>

* [<span data-ttu-id="36fb6-259">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="36fb6-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="36fb6-260">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="36fb6-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_203.png

