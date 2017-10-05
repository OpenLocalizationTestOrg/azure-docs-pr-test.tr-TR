---
title: "Öğretici: Azure Active Directory Tümleştirme ile çalışma alanına Facebook tarafından | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ve Facebook ile çalışma alanına arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 30f2ee64-95d3-44ef-b832-8a0a27e2967c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: jeedes
ms.openlocfilehash: 27e62a00832484667117d8718db9f2fc05e2f4e2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workplace-by-facebook"></a><span data-ttu-id="8d63a-103">Öğretici: Facebook ile çalışma alanına Azure Active Directory Tümleştirme</span><span class="sxs-lookup"><span data-stu-id="8d63a-103">Tutorial: Azure Active Directory integration with Workplace by Facebook</span></span>

<span data-ttu-id="8d63a-104">Bu öğreticide, Azure Active Directory (Azure AD) ile çalışma alanına Facebook ile tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="8d63a-104">In this tutorial, you learn how to integrate Workplace by Facebook with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8d63a-105">Çalışma alanına Facebook ile Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="8d63a-105">Integrating Workplace by Facebook with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8d63a-106">Facebook ile çalışma alanına erişimi olan Azure AD'de kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8d63a-106">You can control in Azure AD who has access to Workplace by Facebook.</span></span>
- <span data-ttu-id="8d63a-107">Otomatik olarak çalışma alanına (çoklu oturum açma) tarafından Facebook kendi Azure AD hesaplarıyla oturum, kullanıcılarınızın etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8d63a-107">You can enable your users to automatically get signed on to Workplace by Facebook (single sign-on) with their Azure AD accounts.</span></span>
- <span data-ttu-id="8d63a-108">Hesaplarınızı tek bir merkezi konumda yönetebilirsiniz: Azure portal.</span><span class="sxs-lookup"><span data-stu-id="8d63a-108">You can manage your accounts in one central location: the Azure portal.</span></span>

<span data-ttu-id="8d63a-109">Azure AD ile hizmet (SaaS) uygulaması tümleştirme olarak yazılım hakkında daha fazla ayrıntı için bkz: [uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8d63a-109">For more details about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8d63a-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="8d63a-110">Prerequisites</span></span>

<span data-ttu-id="8d63a-111">Facebook ile çalışma alanına ile Azure AD tümleştirme yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="8d63a-111">To configure Azure AD integration with Workplace by Facebook, you need the following items:</span></span>

- <span data-ttu-id="8d63a-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="8d63a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8d63a-113">Abonelik çalışma alanına Facebook çoklu oturum açma (SSO) tarafından etkin</span><span class="sxs-lookup"><span data-stu-id="8d63a-113">A Workplace by Facebook single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="8d63a-114">Bu öğreticide adımları test etmek için aşağıdaki önerileri uygulayın:</span><span class="sxs-lookup"><span data-stu-id="8d63a-114">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="8d63a-115">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="8d63a-115">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8d63a-116">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8d63a-116">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8d63a-117">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="8d63a-117">Scenario description</span></span>
<span data-ttu-id="8d63a-118">Bu öğreticide, Azure AD SSO bir test ortamında test.</span><span class="sxs-lookup"><span data-stu-id="8d63a-118">In this tutorial, you test Azure AD SSO in a test environment.</span></span> <span data-ttu-id="8d63a-119">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="8d63a-119">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8d63a-120">Facebook ile çalışma alanına Galeriden ekleyin.</span><span class="sxs-lookup"><span data-stu-id="8d63a-120">Add Workplace by Facebook from the gallery.</span></span>
2. <span data-ttu-id="8d63a-121">Yapılandırma ve Azure AD çoklu oturum açmayı sınayın.</span><span class="sxs-lookup"><span data-stu-id="8d63a-121">Configure and test Azure AD single sign-on.</span></span>

## <a name="add-workplace-by-facebook-from-the-gallery"></a><span data-ttu-id="8d63a-122">Galeriden Facebook ile çalışma alanına ekleyin</span><span class="sxs-lookup"><span data-stu-id="8d63a-122">Add Workplace by Facebook from the gallery</span></span>
<span data-ttu-id="8d63a-123">Azure AD çalışma alanına Facebook ile tümleştirilmesi yapılandırmak için çalışma alanına Facebook tarafından Galeriden yönetilen SaaS uygulamaları listenize ekleyin.</span><span class="sxs-lookup"><span data-stu-id="8d63a-123">To configure the integration of Workplace by Facebook into Azure AD, add Workplace by Facebook from the gallery to your list of managed SaaS apps.</span></span>

1. <span data-ttu-id="8d63a-124">İçinde [Azure portal](https://portal.azure.com), sol bölmede seçin **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8d63a-124">In the [Azure portal](https://portal.azure.com), in the left pane, select **Azure Active Directory**.</span></span> 

    ![Azure Active Directory düğmesi][1]

2. <span data-ttu-id="8d63a-126">Gözat **kurumsal uygulamalar** > **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="8d63a-126">Browse to **Enterprise applications** > **All applications**.</span></span>

    ![Kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="8d63a-128">Yeni bir uygulama eklemek için seçin **yeni uygulama** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="8d63a-128">To add the new application, select **New application** on the top of the dialog box.</span></span>

    ![Yeni Uygulama düğmesi][3]

4. <span data-ttu-id="8d63a-130">Arama kutusuna **Facebook ile çalışma alanına**seçip **Facebook ile çalışma alanına** sonuçlarından.</span><span class="sxs-lookup"><span data-stu-id="8d63a-130">In the search box, type **Workplace by Facebook**, and select **Workplace by Facebook** from results.</span></span> <span data-ttu-id="8d63a-131">Ardından **Ekle**, bir uygulama eklemek için.</span><span class="sxs-lookup"><span data-stu-id="8d63a-131">Then select **Add**, to add the application.</span></span>

    ![Sonuçlar listesinde Facebook ile çalışma](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_search.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="8d63a-133">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="8d63a-133">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="8d63a-134">Bu bölümde, yapılandırma ve Azure AD çalışma alanına "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Facebook tarafından SSO'su test etme</span><span class="sxs-lookup"><span data-stu-id="8d63a-134">In this section, you configure and test Azure AD SSO with Workplace by Facebook, based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8d63a-135">Çalışmak SSO için Azure AD ne karşılık gelen çalışma Facebook tarafından bir kullanıcı için Azure AD içinde olduğu bilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="8d63a-135">For SSO to work, Azure AD needs to know what the counterpart user in Workplace by Facebook is to a user in Azure AD.</span></span> <span data-ttu-id="8d63a-136">Diğer bir deyişle, bir Azure AD kullanıcısının çalışma Facebook ile ilgili kullanıcı arasında bağlantılı bir ilişkisi kurulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8d63a-136">In other words, a linked relationship between an Azure AD user and the related user in Workplace by Facebook should be established.</span></span>

<span data-ttu-id="8d63a-137">Bu ilişkiyi değerini atayarak kurmak **kullanıcı adı** değeri olarak Azure AD'de **kullanıcı adı** Facebook ile çalışma.</span><span class="sxs-lookup"><span data-stu-id="8d63a-137">Establish this relationship by assigning the value of the **user name** in Azure AD as the value of the **Username** in Workplace by Facebook.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="8d63a-138">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="8d63a-138">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="8d63a-139">Bu bölümde, Azure portalında Azure AD SSO'yu etkinleştirmek ve SSO Facebook uygulama tarafından çalışma alanınızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="8d63a-139">In this section, you enable Azure AD SSO in the Azure portal, and you configure SSO in your Workplace by Facebook application.</span></span>

1. <span data-ttu-id="8d63a-140">Azure portalında üzerinde **Facebook ile çalışma alanına** uygulama tümleştirmesi sayfasında, **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="8d63a-140">In the Azure portal, on the **Workplace by Facebook** application integration page, select **Single sign-on**.</span></span>

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. <span data-ttu-id="8d63a-142">İçinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** SSO'yu etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="8d63a-142">In the **Single sign-on** dialog box, select **Mode** as **SAML-based Sign-on** to enable SSO.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_samlbase.png)

3. <span data-ttu-id="8d63a-144">İçinde **Facebook etki alanı ve URL'ler ile çalışma alanına** bölümünde, aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="8d63a-144">In the **Workplace by Facebook Domain and URLs** section, do the following:</span></span>

    <span data-ttu-id="8d63a-145">a.</span><span class="sxs-lookup"><span data-stu-id="8d63a-145">a.</span></span> <span data-ttu-id="8d63a-146">İçinde **oturum açma URL'si** metin kutusunda, aşağıdaki desen kullanan bir URL yazın:`https://<company subdomain>.facebook.com`</span><span class="sxs-lookup"><span data-stu-id="8d63a-146">In the **Sign-on URL** text box, type a URL that uses the following pattern: `https://<company subdomain>.facebook.com`</span></span>

    <span data-ttu-id="8d63a-147">b.</span><span class="sxs-lookup"><span data-stu-id="8d63a-147">b.</span></span> <span data-ttu-id="8d63a-148">İçinde **tanımlayıcısı** metin kutusunda, aşağıdaki desen kullanan bir URL yazın:`https://www.facebook.com/company/<scim company id>`</span><span class="sxs-lookup"><span data-stu-id="8d63a-148">In the **Identifier** text box, type a URL that uses the following pattern: `https://www.facebook.com/company/<scim company id>`</span></span>

    > [!NOTE]
    > <span data-ttu-id="8d63a-149">Bu yalnızca bir örnek değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="8d63a-149">These values are an example only.</span></span> <span data-ttu-id="8d63a-150">Bu değerleri tanımlayıcısı ve gerçek oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="8d63a-150">Update these values with the actual sign-on URL and identifier.</span></span> <span data-ttu-id="8d63a-151">Kişi [Facebook istemcisini destek ekibi ile çalışma alanına](https://workplace.fb.com/faq/) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="8d63a-151">Contact the [Workplace by Facebook Client support team](https://workplace.fb.com/faq/) to get these values.</span></span> 

4. <span data-ttu-id="8d63a-152">İçinde **SAML imzalama sertifikası** bölümünde, select **sertifika (Base64)**ve ardından sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="8d63a-152">In the **SAML Signing Certificate** section, select **Certificate (Base64)**, and then save the certificate file on your computer.</span></span>

    ![Sertifika indirme bağlantısı](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_certificate.png) 

5. <span data-ttu-id="8d63a-154">**Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="8d63a-154">Select **Save**.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8d63a-156">İçinde **Facebook yapılandırmaya göre çalışma alanına** bölümünde, select **yapılandırma çalışma Facebook tarafından** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="8d63a-156">In the **Workplace by Facebook Configuration** section, select **Configure Workplace by Facebook** to open the **Configure sign-on** window.</span></span> <span data-ttu-id="8d63a-157">Kopya **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru** bölümü.</span><span class="sxs-lookup"><span data-stu-id="8d63a-157">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference** section.</span></span>

    ![Facebook yapılandırma ile çalışma](./media/active-directory-saas-facebook-at-work-tutorial/config.png) 

7. <span data-ttu-id="8d63a-159">Farklı web tarayıcısı penceresinde işyeriniz Facebook şirket site tarafından bir yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="8d63a-159">In a different web browser window, sign in to your Workplace by Facebook company site as an administrator.</span></span>
  
   > [!NOTE] 
   > <span data-ttu-id="8d63a-160">SAML kimlik doğrulama işleminin bir parçası olarak, çalışma alanına sorgu dizeleri kadar 2,5 kilobayt boyutunda Azure AD'ye parametreleri geçirmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8d63a-160">As part of the SAML authentication process, Workplace can use query strings of up to 2.5 kilobytes in size in order to pass parameters to Azure AD.</span></span>

8. <span data-ttu-id="8d63a-161">İçinde **şirket Pano**gidin **kimlik doğrulaması** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="8d63a-161">In the **Company Dashboard**, go to the **Authentication** tab.</span></span>

9. <span data-ttu-id="8d63a-162">Altında **SAML kimlik doğrulaması**seçin **yalnızca SSO** aşağı açılan listeden.</span><span class="sxs-lookup"><span data-stu-id="8d63a-162">Under **SAML Authentication**, select **SSO Only** from the drop-down list.</span></span>

10. <span data-ttu-id="8d63a-163">Kopyalanan değerleri girin **Facebook yapılandırmaya göre çalışma alanına** bölümüne karşılık gelen alanlara Azure portalının:</span><span class="sxs-lookup"><span data-stu-id="8d63a-163">Enter the values copied from the **Workplace by Facebook Configuration** section of the Azure portal into the corresponding fields:</span></span>

    *   <span data-ttu-id="8d63a-164">İçinde **SAML URL** metin kutusunda, değerini yapıştırın **çoklu oturum açma hizmet URL'si**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="8d63a-164">In the **SAML URL** text box, paste the value of **Single Sign-On Service URL**, which you have copied from the Azure portal.</span></span>
    *   <span data-ttu-id="8d63a-165">İçinde **SAML veren URL'si** metin kutusunda, değerini yapıştırın **SAML varlık kimliği**, hangi Azure portalından kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="8d63a-165">In the **SAML Issuer URL** text box, paste the value of **SAML Entity ID**, which you have copied from the Azure portal.</span></span>
    *   <span data-ttu-id="8d63a-166">İçinde **SAML oturum kapatma yeniden yönlendir (isteğe bağlı)**, değerini yapıştırın **Sign-Out URL**, hangi Azure portalından kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="8d63a-166">In **SAML Logout Redirect (optional)**, paste the value of **Sign-Out URL**, which you have copied from the Azure portal.</span></span>
    *   <span data-ttu-id="8d63a-167">Açık, **base-64 kodlamalı sertifika** Not Defteri'nde, Azure portalından indirdiğiniz.</span><span class="sxs-lookup"><span data-stu-id="8d63a-167">Open your **base-64 encoded certificate** in Notepad, downloaded from the Azure portal.</span></span> <span data-ttu-id="8d63a-168">İçeriğini, panoya kopyalayın ve yapıştırın kendisine **SAML sertifika** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="8d63a-168">Copy the content of it into your clipboard, and then paste it to the **SAML Certificate** text box.</span></span>

11. <span data-ttu-id="8d63a-169">Hedef kitle URL girmeniz gerekebilir alıcı URL'si ve ACS (onaylama tüketici hizmeti) URL'si altında listelenen **SAML Yapılandırması** bölümü.</span><span class="sxs-lookup"><span data-stu-id="8d63a-169">You might need to enter the audience URL, recipient URL, and ACS (Assertion Consumer Service) URL, listed under the **SAML Configuration** section.</span></span>

12. <span data-ttu-id="8d63a-170">Bölümün sonuna kaydırın ve seçin **Test SSO**.</span><span class="sxs-lookup"><span data-stu-id="8d63a-170">Scroll to the bottom of the section, and select **Test SSO**.</span></span> <span data-ttu-id="8d63a-171">Açılır pencere sahip Azure AD oturum açma sayfası görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="8d63a-171">A pop-up window appears, with the Azure AD sign-in page.</span></span> <span data-ttu-id="8d63a-172">Kimlik doğrulaması için kimlik bilgilerinizi normal olarak girin.</span><span class="sxs-lookup"><span data-stu-id="8d63a-172">To authenticate, enter your credentials as normal.</span></span> <span data-ttu-id="8d63a-173">Azure AD geri döndürülen e-posta adresi ile oturum açmış kullanıcının iş yeri hesabını aynı olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="8d63a-173">Ensure the email address returned back from Azure AD is the same as the Workplace account you are logged in with.</span></span>

13. <span data-ttu-id="8d63a-174">Test başarıyla tamamlandı, seçin ve sayfanın alt kısmına kaydırın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="8d63a-174">If the test has finished successfully, scroll to the bottom of the page and select **Save**.</span></span>

14. <span data-ttu-id="8d63a-175">Çalışma alanına kullanan herkesin artık kimlik doğrulaması için Azure AD oturum açma sayfası sunulur.</span><span class="sxs-lookup"><span data-stu-id="8d63a-175">Anyone using Workplace is now presented with Azure AD sign-in page for authentication.</span></span>

<span data-ttu-id="8d63a-176">SAML oturum açma kapatma sırasında Azure AD oturum kapatma sayfasını işaret etmek için kullanılan URL'si yapılandırın seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8d63a-176">You can choose to configure a SAML sign out URL, which can be used to point at the Azure AD sign-out page.</span></span> <span data-ttu-id="8d63a-177">Bu ayar etkin ve yapılandırılmış olduğunda, kullanıcı artık çalışma alanına oturum kapatma sayfasına yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="8d63a-177">When this setting is enabled and configured, the user is no longer directed to the Workplace sign-out page.</span></span> <span data-ttu-id="8d63a-178">Bunun yerine, kullanıcı SAML oturum kapatma yeniden yönlendirme ayarında eklenmiş olan URL'ye yeniden yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="8d63a-178">Instead, the user is redirected to the URL that was added in the SAML sign-out redirect setting.</span></span>


> [!TIP]
> <span data-ttu-id="8d63a-179">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken.</span><span class="sxs-lookup"><span data-stu-id="8d63a-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app.</span></span> <span data-ttu-id="8d63a-180">Bu uygulamadan ekledikten sonra **Active Directory** > **kurumsal uygulamalar** bölüm, yalnızca select **çoklu oturum açma** sekmesini tıklatın ve erişim Belge aracılığıyla katıştırılmış **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="8d63a-180">After adding this app from the **Active Directory** > **Enterprise Applications** section, simply select the **Single Sign-On** tab, and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8d63a-181">Daha fazla bilgiyi embedded belgeler özelliği hakkında [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="8d63a-181">You can read more about the embedded documentation feature in the [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>

### <a name="configure-reauthentication-frequency"></a><span data-ttu-id="8d63a-182">Yeniden kimlik doğrulamanın sıklığını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="8d63a-182">Configure reauthentication frequency</span></span>

<span data-ttu-id="8d63a-183">Bir SAML denetimi için üç gün, günde bir hafta, iki hafta, bir ay istemek için çalışma alanına yapılandırabilirsiniz ya da hiç.</span><span class="sxs-lookup"><span data-stu-id="8d63a-183">You can configure Workplace to prompt for a SAML check every day, three days, one week, two weeks, one month, or never.</span></span>

> [!NOTE] 
><span data-ttu-id="8d63a-184">Mobil uygulamalar üzerinde SAML denetimi için en düşük değer için bir hafta ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="8d63a-184">The minimum value for the SAML check on mobile applications is set to one week.</span></span>

<span data-ttu-id="8d63a-185">Ayrıca, tüm kullanıcılar için sıfırlama SAML zorlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8d63a-185">You can also force a SAML reset for all users.</span></span> <span data-ttu-id="8d63a-186">Bunu yapmak için kullanın **şimdi gerektiren SAML kimlik doğrulaması tüm kullanıcılar için** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="8d63a-186">To do this, use the **Require SAML authentication for all users now** button.</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="8d63a-187">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="8d63a-187">Create an Azure AD test user</span></span>
<span data-ttu-id="8d63a-188">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="8d63a-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

1. <span data-ttu-id="8d63a-190">İçinde **Azure portal**, sol bölmede seçin **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8d63a-190">In the **Azure portal**, in the left pane, select **Azure Active Directory**.</span></span>

    ![Azure Active Directory düğmesi](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8d63a-192">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar**seçip **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="8d63a-192">To display the list of users, go to **Users and groups**, and select **All users**.</span></span>
    
    !["Kullanıcılar ve Gruplar" ve "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8d63a-194">Açmak için **kullanıcı** iletişim kutusunda **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="8d63a-194">To open the **User** dialog box, select **Add**.</span></span>
 
    ![Ekle düğmesi](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8d63a-196">İçinde **kullanıcı** iletişim kutusunda, aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="8d63a-196">In the **User** dialog box, do the following:</span></span>
 
    ![Kullanıcı iletişim kutusu](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8d63a-198">a.</span><span class="sxs-lookup"><span data-stu-id="8d63a-198">a.</span></span> <span data-ttu-id="8d63a-199">İçinde **adı** metin kutusunda, **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8d63a-199">In the **Name** text box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8d63a-200">b.</span><span class="sxs-lookup"><span data-stu-id="8d63a-200">b.</span></span> <span data-ttu-id="8d63a-201">İçinde **kullanıcı adı** metin kutusunda, **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="8d63a-201">In the **User name** text box, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8d63a-202">c.</span><span class="sxs-lookup"><span data-stu-id="8d63a-202">c.</span></span> <span data-ttu-id="8d63a-203">Seçin **Göster parola**ve not edin.</span><span class="sxs-lookup"><span data-stu-id="8d63a-203">Select **Show Password**, and write it down.</span></span>

    <span data-ttu-id="8d63a-204">d.</span><span class="sxs-lookup"><span data-stu-id="8d63a-204">d.</span></span> <span data-ttu-id="8d63a-205">**Oluştur**’u seçin.</span><span class="sxs-lookup"><span data-stu-id="8d63a-205">Select **Create**.</span></span>
 
### <a name="create-a-workplace-by-facebook-test-user"></a><span data-ttu-id="8d63a-206">Facebook test kullanıcı tarafından bir çalışma alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="8d63a-206">Create a Workplace by Facebook test user</span></span>

<span data-ttu-id="8d63a-207">Bu bölümde, Britta Simon adlı bir kullanıcı tarafından Facebook çalışma alanında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="8d63a-207">In this section, a user called Britta Simon is created in Workplace by Facebook.</span></span> <span data-ttu-id="8d63a-208">Çalışma alanına Facebook tarafından yalnızca zaman sağlama, varsayılan olarak etkin olduğu destekler.</span><span class="sxs-lookup"><span data-stu-id="8d63a-208">Workplace by Facebook supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="8d63a-209">Bu bölümdeki hiçbir şey yoktur.</span><span class="sxs-lookup"><span data-stu-id="8d63a-209">There is no action for you in this section.</span></span> <span data-ttu-id="8d63a-210">Bir kullanıcı çalışma Facebook tarafından yoksa, çalışma alanına erişmeye çalıştığında yeni bir Facebook tarafından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="8d63a-210">If a user doesn't exist in Workplace by Facebook, a new one is created when you attempt to access Workplace by Facebook.</span></span>

>[!Note]
><span data-ttu-id="8d63a-211">Bir kullanıcı el ile oluşturmanız gerekiyorsa, kişi [Facebook istemcisini destek ekibi ile çalışma alanına](https://workplace.fb.com/faq/).</span><span class="sxs-lookup"><span data-stu-id="8d63a-211">If you need to create a user manually, contact the [Workplace by Facebook Client support team](https://workplace.fb.com/faq/).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="8d63a-212">Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="8d63a-212">Assign the Azure AD test user</span></span>

<span data-ttu-id="8d63a-213">Bu bölümde, Facebook ile çalışma alanına erişim vererek Azure SSO kullanılacak Britta Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="8d63a-213">In this section, you enable Britta Simon to use Azure SSO by granting access to Workplace by Facebook.</span></span>

![Kullanıcı atama][200] 

1. <span data-ttu-id="8d63a-215">Azure portalında uygulamaları görünümünü açın.</span><span class="sxs-lookup"><span data-stu-id="8d63a-215">In the Azure portal, open the applications view.</span></span> <span data-ttu-id="8d63a-216">Dizin görünümüne gidin, Git **kurumsal uygulamalar**ve ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="8d63a-216">Go to the directory view, go to **Enterprise applications**, and then select **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="8d63a-218">Uygulamalar listesinde **Facebook ile çalışma alanına**.</span><span class="sxs-lookup"><span data-stu-id="8d63a-218">In the applications list, select **Workplace by Facebook**.</span></span>

    ![Uygulamalar listesinde Facebook bağlantısıyla çalışma](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_app.png) 

3. <span data-ttu-id="8d63a-220">Soldaki menüde seçin **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="8d63a-220">In the menu on the left, select **Users and groups**.</span></span>

    !["Kullanıcılar ve Gruplar" bağlantı][202] 

4. <span data-ttu-id="8d63a-222">**Add (Ekle)** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="8d63a-222">Select **Add**.</span></span> <span data-ttu-id="8d63a-223">Ardından **eklemek atama** bölmesinde, **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="8d63a-223">Then, in the **Add Assignment** pane, select **Users and groups**.</span></span>

    ![Ekleme atama bölmesi][203]

5. <span data-ttu-id="8d63a-225">İçinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="8d63a-225">In the **Users and groups** dialog box, select **Britta Simon** in the users list.</span></span>

6. <span data-ttu-id="8d63a-226">İçinde **kullanıcılar ve gruplar** iletişim kutusunda **seçin**.</span><span class="sxs-lookup"><span data-stu-id="8d63a-226">In the **Users and groups** dialog box, select **Select**.</span></span>

7. <span data-ttu-id="8d63a-227">İçinde **eklemek atama** iletişim kutusunda **atamak**.</span><span class="sxs-lookup"><span data-stu-id="8d63a-227">In the **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="8d63a-228">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="8d63a-228">Test single sign-on</span></span>

<span data-ttu-id="8d63a-229">SSO ayarlarınızı test etmek isterseniz, erişim paneli açın.</span><span class="sxs-lookup"><span data-stu-id="8d63a-229">If you want to test your SSO settings, open the Access Panel.</span></span>
<span data-ttu-id="8d63a-230">Daha fazla bilgi için bkz. [Erişim Paneli'ne Giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8d63a-230">For more information, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="8d63a-231">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8d63a-231">Next steps</span></span>

* <span data-ttu-id="8d63a-232">Bkz: [SaaS uygulamaları Azure Active Directory ile tümleştirme hakkında öğreticiler listesi](active-directory-saas-tutorial-list.md).</span><span class="sxs-lookup"><span data-stu-id="8d63a-232">See the [list of tutorials on how to integrate SaaS Apps with Azure Active Directory](active-directory-saas-tutorial-list.md).</span></span>
* <span data-ttu-id="8d63a-233">Okuma [uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8d63a-233">Read [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>
* <span data-ttu-id="8d63a-234">Nasıl yapılır hakkında daha fazla bilgi [kullanıcı sağlamayı Yapılandır](active-directory-saas-facebook-at-work-provisioning-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="8d63a-234">Learn more about how to [configure user provisioning](active-directory-saas-facebook-at-work-provisioning-tutorial.md).</span></span>



<!--Image references-->

[1]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_203.png

