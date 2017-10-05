---
title: "Öğretici: Azure Active Directory Tümleştirme ile TeamSeer | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile TeamSeer arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6ec4806f-fe0f-4ed7-8cfa-32d1c840433f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 2a5e8f6d1443681c43db95da5cef0b7f2ef92291
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamseer"></a><span data-ttu-id="3bbf2-103">Öğretici: Azure Active Directory Tümleştirme TeamSeer ile</span><span class="sxs-lookup"><span data-stu-id="3bbf2-103">Tutorial: Azure Active Directory integration with TeamSeer</span></span>

<span data-ttu-id="3bbf2-104">Bu öğreticide, Azure Active Directory (Azure AD) ile TeamSeer tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-104">In this tutorial, you learn how to integrate TeamSeer with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3bbf2-105">TeamSeer Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="3bbf2-105">Integrating TeamSeer with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3bbf2-106">TeamSeer erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="3bbf2-106">You can control in Azure AD who has access to TeamSeer</span></span>
- <span data-ttu-id="3bbf2-107">Otomatik olarak için TeamSeer (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="3bbf2-107">You can enable your users to automatically get signed-on to TeamSeer (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3bbf2-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="3bbf2-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3bbf2-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3bbf2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3bbf2-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="3bbf2-110">Prerequisites</span></span>

<span data-ttu-id="3bbf2-111">Azure AD tümleştirme TeamSeer ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="3bbf2-111">To configure Azure AD integration with TeamSeer, you need the following items:</span></span>

- <span data-ttu-id="3bbf2-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="3bbf2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3bbf2-113">Bir TeamSeer çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="3bbf2-113">A TeamSeer single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3bbf2-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3bbf2-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="3bbf2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3bbf2-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3bbf2-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3bbf2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3bbf2-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="3bbf2-118">Scenario description</span></span>
<span data-ttu-id="3bbf2-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3bbf2-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="3bbf2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3bbf2-121">Galeriden TeamSeer ekleme</span><span class="sxs-lookup"><span data-stu-id="3bbf2-121">Adding TeamSeer from the gallery</span></span>
2. <span data-ttu-id="3bbf2-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="3bbf2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-teamseer-from-the-gallery"></a><span data-ttu-id="3bbf2-123">Galeriden TeamSeer ekleme</span><span class="sxs-lookup"><span data-stu-id="3bbf2-123">Adding TeamSeer from the gallery</span></span>
<span data-ttu-id="3bbf2-124">Azure ad içinde TeamSeer tümleştirmesini yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden TeamSeer eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-124">To configure the integration of TeamSeer in to Azure AD, you need to add TeamSeer from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3bbf2-125">**Galeriden TeamSeer eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="3bbf2-125">**To add TeamSeer from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3bbf2-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3bbf2-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3bbf2-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="3bbf2-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="3bbf2-133">Arama kutusuna **TeamSeer**.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-133">In the search box, type **TeamSeer**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_search.png)

5. <span data-ttu-id="3bbf2-135">Sonuçlar panelinde seçin **TeamSeer**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-135">In the results panel, select **TeamSeer**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3bbf2-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="3bbf2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3bbf2-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı TeamSeer ile test etme</span><span class="sxs-lookup"><span data-stu-id="3bbf2-138">In this section, you configure and test Azure AD single sign-on with TeamSeer based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3bbf2-139">Tekli çalışmaya oturum için Azure AD TeamSeer karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-139">For single sign-on to work, Azure AD needs to know what the counterpart user in TeamSeer is to a user in Azure AD.</span></span> <span data-ttu-id="3bbf2-140">Diğer bir deyişle, bir Azure AD kullanıcısının TeamSeer ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-140">In other words, a link relationship between an Azure AD user and the related user in TeamSeer needs to be established.</span></span>

<span data-ttu-id="3bbf2-141">TeamSeer içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-141">In TeamSeer, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3bbf2-142">Yapılandırma ve Azure AD çoklu oturum açma TeamSeer ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="3bbf2-142">To configure and test Azure AD single sign-on with TeamSeer, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3bbf2-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3bbf2-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3bbf2-145">**[TeamSeer test kullanıcısı oluşturma](#creating-a-teamseer-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı TeamSeer sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-145">**[Creating a TeamSeer test user](#creating-a-teamseer-test-user)** - to have a counterpart of Britta Simon in TeamSeer that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3bbf2-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3bbf2-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3bbf2-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3bbf2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3bbf2-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma TeamSeer uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TeamSeer application.</span></span>

<span data-ttu-id="3bbf2-150">**Azure AD çoklu oturum açma ile TeamSeer yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="3bbf2-150">**To configure Azure AD single sign-on with TeamSeer, perform the following steps:**</span></span>

1. <span data-ttu-id="3bbf2-151">Azure portalında üzerinde **TeamSeer** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-151">In the Azure portal, on the **TeamSeer** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="3bbf2-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_samlbase.png)

3. <span data-ttu-id="3bbf2-155">Üzerinde **TeamSeer etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="3bbf2-155">On the **TeamSeer Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_url.png)

     <span data-ttu-id="3bbf2-157">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://www.teamseer.com/<companyid>`</span><span class="sxs-lookup"><span data-stu-id="3bbf2-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://www.teamseer.com/<companyid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3bbf2-158">Değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-158">The value is not real.</span></span> <span data-ttu-id="3bbf2-159">Değerin gerçek oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="3bbf2-160">Kişi [TeamSeer istemci destek ekibi](http://pages.theaccessgroup.com/solutions_business-suite_absence-management_contact.html) değeri alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-160">Contact [TeamSeer Client support team](http://pages.theaccessgroup.com/solutions_business-suite_absence-management_contact.html) to get the value.</span></span> 
 
4. <span data-ttu-id="3bbf2-161">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_certificate.png) 

5. <span data-ttu-id="3bbf2-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-teamseer-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3bbf2-165">Üzerinde **TeamSeer yapılandırma** 'yi tıklatın **yapılandırma TeamSeer** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-165">On the **TeamSeer Configuration** section, click **Configure TeamSeer** to open **Configure sign-on** window.</span></span> <span data-ttu-id="3bbf2-166">Kopya **SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="3bbf2-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_configure.png)

7. <span data-ttu-id="3bbf2-168">Farklı web tarayıcısı penceresinde TeamSeer şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-168">In a different web browser window, log in to your TeamSeer company site as an administrator.</span></span>

8. <span data-ttu-id="3bbf2-169">Git **ik yönetici**.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-169">Go to **HR Admin**.</span></span>
   
    <span data-ttu-id="3bbf2-170">![HR yönetici](./media/active-directory-saas-teamseer-tutorial/ic789634.png "ik yönetici")</span><span class="sxs-lookup"><span data-stu-id="3bbf2-170">![HR Admin](./media/active-directory-saas-teamseer-tutorial/ic789634.png "HR Admin")</span></span>

9. <span data-ttu-id="3bbf2-171">Tıklatın **Kurulum**.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-171">Click **Setup**.</span></span>
   
    <span data-ttu-id="3bbf2-172">![Kurulum](./media/active-directory-saas-teamseer-tutorial/ic789635.png "Kurulumu")</span><span class="sxs-lookup"><span data-stu-id="3bbf2-172">![Setup](./media/active-directory-saas-teamseer-tutorial/ic789635.png "Setup")</span></span>

10. <span data-ttu-id="3bbf2-173">Tıklatın **SAML sağlayıcı ayrıntılarını ayarlama**.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-173">Click **Set up SAML provider details**.</span></span>
   
    <span data-ttu-id="3bbf2-174">![SAML ayarları](./media/active-directory-saas-teamseer-tutorial/ic789636.png "SAML ayarları")</span><span class="sxs-lookup"><span data-stu-id="3bbf2-174">![SAML Settings](./media/active-directory-saas-teamseer-tutorial/ic789636.png "SAML Settings")</span></span>

11. <span data-ttu-id="3bbf2-175">SAML sağlayıcısı Ayrıntılar bölümünde aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="3bbf2-175">In the SAML provider details section, perform the following steps:</span></span>
   
    <span data-ttu-id="3bbf2-176">![SAML ayarları](./media/active-directory-saas-teamseer-tutorial/ic789637.png "SAML ayarları")</span><span class="sxs-lookup"><span data-stu-id="3bbf2-176">![SAML Settings](./media/active-directory-saas-teamseer-tutorial/ic789637.png "SAML Settings")</span></span>   

    <span data-ttu-id="3bbf2-177">a.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-177">a.</span></span> <span data-ttu-id="3bbf2-178">Yapıştır **çoklu oturum açma hizmet URL'si** için değer **URL** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-178">Paste the **Single Sign-On Service URL** value in to the **URL** textbox.</span></span>
          
    <span data-ttu-id="3bbf2-179">b.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-179">b.</span></span> <span data-ttu-id="3bbf2-180">Base-64 kodlanmış sertifikanızı Not Defteri'nde açın, içinde içeriğini panonuza kopyalayın ve yapıştırın kendisine **IDP ortak sertifika** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-180">Open your base-64 encoded certificate in notepad, copy the content of it in to your clipboard, and then paste it to the **IdP Public Certificate** textbox.</span></span>

12. <span data-ttu-id="3bbf2-181">SAML sağlayıcısı yapılandırmasını tamamlamak için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="3bbf2-181">To complete the SAML provider configuration, perform the following steps:</span></span>
    
    <span data-ttu-id="3bbf2-182">![SAML ayarları](./media/active-directory-saas-teamseer-tutorial/ic789638.png "SAML ayarları")</span><span class="sxs-lookup"><span data-stu-id="3bbf2-182">![SAML Settings](./media/active-directory-saas-teamseer-tutorial/ic789638.png "SAML Settings")</span></span> 

    <span data-ttu-id="3bbf2-183">a.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-183">a.</span></span> <span data-ttu-id="3bbf2-184">İçinde **Test e-posta adresleri**, test kullanıcının e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-184">In the **Test Email Addresses**, type the test user’s email address.</span></span> 
  
    <span data-ttu-id="3bbf2-185">b.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-185">b.</span></span> <span data-ttu-id="3bbf2-186">İçinde **veren** metin kutusuna, hizmet sağlayıcısı veren URL'sini yazın.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-186">In the **Issuer** textbox, type the Issuer URL of the service provider.</span></span> 
  
    <span data-ttu-id="3bbf2-187">c.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-187">c.</span></span> <span data-ttu-id="3bbf2-188">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-188">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="3bbf2-189">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="3bbf2-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3bbf2-190">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3bbf2-191">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3bbf2-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3bbf2-192">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="3bbf2-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="3bbf2-193">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="3bbf2-195">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="3bbf2-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3bbf2-196">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-teamseer-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3bbf2-198">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-teamseer-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3bbf2-200">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-teamseer-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3bbf2-202">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="3bbf2-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-teamseer-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3bbf2-204">a.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-204">a.</span></span> <span data-ttu-id="3bbf2-205">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3bbf2-206">b.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-206">b.</span></span> <span data-ttu-id="3bbf2-207">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3bbf2-208">c.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-208">c.</span></span> <span data-ttu-id="3bbf2-209">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3bbf2-210">d.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-210">d.</span></span> <span data-ttu-id="3bbf2-211">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-211">Click **Create**.</span></span>
 
### <a name="creating-a-teamseer-test-user"></a><span data-ttu-id="3bbf2-212">TeamSeer test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="3bbf2-212">Creating a TeamSeer test user</span></span>

<span data-ttu-id="3bbf2-213">TeamSeer için oturum açmak Azure AD kullanıcıları etkinleştirmek için bunlar içinde ShiftPlanning için hazırlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-213">To enable Azure AD users to log in to TeamSeer, they must be provisioned in to ShiftPlanning.</span></span> <span data-ttu-id="3bbf2-214">TeamSeer söz konusu olduğunda, sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-214">In the case of TeamSeer, provisioning is a manual task.</span></span>

<span data-ttu-id="3bbf2-215">**Bir kullanıcı hesabı sağlamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="3bbf2-215">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="3bbf2-216">Oturum, **TeamSeer** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-216">Log in to your **TeamSeer** company site as an administrator.</span></span>

2. <span data-ttu-id="3bbf2-217">Aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="3bbf2-217">Perform the following steps:</span></span>
   
    <span data-ttu-id="3bbf2-218">![HR yönetici](./media/active-directory-saas-teamseer-tutorial/ic789640.png "ik yönetici")</span><span class="sxs-lookup"><span data-stu-id="3bbf2-218">![HR Admin](./media/active-directory-saas-teamseer-tutorial/ic789640.png "HR Admin")</span></span>  
 
    <span data-ttu-id="3bbf2-219">a.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-219">a.</span></span> <span data-ttu-id="3bbf2-220">Git **ik yönetici \> kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-220">Go to **HR Admin \> Users**.</span></span>
  
    <span data-ttu-id="3bbf2-221">b.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-221">b.</span></span> <span data-ttu-id="3bbf2-222">Tıklatın **yeni kullanıcı Sihirbazı'nı çalıştırın**.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-222">Click **Run the New User wizard**.</span></span>

3. <span data-ttu-id="3bbf2-223">İçinde **kullanıcı ayrıntıları** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="3bbf2-223">In the **User Details** section, perform the following steps:</span></span>
   
    <span data-ttu-id="3bbf2-224">![Kullanıcı ayrıntılarını](./media/active-directory-saas-teamseer-tutorial/ic789641.png "kullanıcı ayrıntıları")</span><span class="sxs-lookup"><span data-stu-id="3bbf2-224">![User Details](./media/active-directory-saas-teamseer-tutorial/ic789641.png "User Details")</span></span>

    <span data-ttu-id="3bbf2-225">a.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-225">a.</span></span> <span data-ttu-id="3bbf2-226">Tür **ad**, **Soyadı**, **kullanıcı adı (e-posta adresi)** sağlamak için ilgili metin kutularına, geçerli bir AAD hesabının.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-226">Type the **First Name**, **Surname**, **User name (Email address)** of a valid AAD account you want to provision in to the related textboxes.</span></span>
  
    <span data-ttu-id="3bbf2-227">b.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-227">b.</span></span> <span data-ttu-id="3bbf2-228">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-228">Click **Next**.</span></span>

4. <span data-ttu-id="3bbf2-229">İzleyin ekran yeni bir kullanıcı eklemek için yönergeler tıklatıp **son**.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-229">Follow the on-screen instructions for adding a new user, and click **Finish**.</span></span>

>[!NOTE]
><span data-ttu-id="3bbf2-230">API Azure AD kullanıcı hesaplarını sağlamak için TeamSeer tarafından sağlanan veya herhangi diğer TeamSeer kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-230">You can use any other TeamSeer user account creation tools or APIs provided by TeamSeer to provision Azure AD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3bbf2-231">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="3bbf2-231">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3bbf2-232">Bu bölümde, Britta TeamSeer için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TeamSeer.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="3bbf2-234">**TeamSeer için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="3bbf2-234">**To assign Britta Simon to TeamSeer, perform the following steps:**</span></span>

1. <span data-ttu-id="3bbf2-235">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="3bbf2-237">Uygulamalar listesinde **TeamSeer**.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-237">In the applications list, select **TeamSeer**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_app.png) 

3. <span data-ttu-id="3bbf2-239">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-239">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="3bbf2-241">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-241">Click **Add** button.</span></span> <span data-ttu-id="3bbf2-242">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="3bbf2-244">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3bbf2-245">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3bbf2-246">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3bbf2-247">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="3bbf2-247">Testing single sign-on</span></span>

<span data-ttu-id="3bbf2-248">Çoklu oturum açma ayarlarınızı test etmek isterseniz, erişim paneli açın.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-248">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="3bbf2-249">Erişim paneli hakkında daha fazla ayrıntı için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3bbf2-249">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3bbf2-250">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="3bbf2-250">Additional resources</span></span>

* [<span data-ttu-id="3bbf2-251">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="3bbf2-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3bbf2-252">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="3bbf2-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_203.png

