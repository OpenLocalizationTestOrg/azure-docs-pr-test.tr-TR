---
title: "Öğretici: Azure Active Directory Tümleştirme 8 x 8 sanal Office ile | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ve 8 x 8 sanal ofis arasındaki yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b34a6edf-e745-4aec-b0b2-7337473d64c5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: d8dcf0171b93fec15347e810a1b525bd815dbf04
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-8x8-virtual-office"></a><span data-ttu-id="4b337-103">Öğretici: Azure Active Directory Tümleştirme 8 x 8 sanal Office ile</span><span class="sxs-lookup"><span data-stu-id="4b337-103">Tutorial: Azure Active Directory integration with 8x8 Virtual Office</span></span>

<span data-ttu-id="4b337-104">Bu öğreticide, Azure Active Directory (Azure AD) ile 8 x 8 sanal Office tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="4b337-104">In this tutorial, you learn how to integrate 8x8 Virtual Office with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4b337-105">8 x 8 tümleştirme sanal Office Azure AD ile aşağıdaki faydaları sağlar:</span><span class="sxs-lookup"><span data-stu-id="4b337-105">Integrating 8x8 Virtual Office with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4b337-106">8 x 8 sanal ofise erişimi olan Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="4b337-106">You can control in Azure AD who has access to 8x8 Virtual Office</span></span>
- <span data-ttu-id="4b337-107">Azure AD hesaplarına otomatik olarak (çoklu oturum açma) 8 x 8 sanal Office açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="4b337-107">You can enable your users to automatically get signed-on to 8x8 Virtual Office (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4b337-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="4b337-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="4b337-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4b337-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4b337-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="4b337-110">Prerequisites</span></span>

<span data-ttu-id="4b337-111">Azure AD tümleştirme 8 x 8 sanal Office ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="4b337-111">To configure Azure AD integration with 8x8 Virtual Office, you need the following items:</span></span>

- <span data-ttu-id="4b337-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="4b337-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4b337-113">Bir 8 x 8 sanal Office çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="4b337-113">A 8x8 Virtual Office single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4b337-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="4b337-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4b337-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="4b337-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4b337-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="4b337-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4b337-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4b337-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4b337-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="4b337-118">Scenario description</span></span>
<span data-ttu-id="4b337-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="4b337-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4b337-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="4b337-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4b337-121">Galeriden 8 x 8 sanal Office ekleme</span><span class="sxs-lookup"><span data-stu-id="4b337-121">Adding 8x8 Virtual Office from the gallery</span></span>
2. <span data-ttu-id="4b337-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="4b337-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-8x8-virtual-office-from-the-gallery"></a><span data-ttu-id="4b337-123">Galeriden 8 x 8 sanal Office ekleme</span><span class="sxs-lookup"><span data-stu-id="4b337-123">Adding 8x8 Virtual Office from the gallery</span></span>
<span data-ttu-id="4b337-124">Azure AD 8 x 8 sanal Office tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden 8 x 8 sanal Office eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4b337-124">To configure the integration of 8x8 Virtual Office into Azure AD, you need to add 8x8 Virtual Office from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4b337-125">**Galeriden 8 x 8 sanal Office eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="4b337-125">**To add 8x8 Virtual Office from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4b337-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="4b337-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4b337-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="4b337-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4b337-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="4b337-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="4b337-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4b337-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="4b337-133">Arama kutusuna **8 x 8 sanal Office**.</span><span class="sxs-lookup"><span data-stu-id="4b337-133">In the search box, type **8x8 Virtual Office**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_search.png)

5. <span data-ttu-id="4b337-135">Sonuçlar panelinde seçin **8 x 8 sanal Office**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4b337-135">In the results panel, select **8x8 Virtual Office**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4b337-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="4b337-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4b337-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma 8 x 8 sanal Office "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı ile test etme</span><span class="sxs-lookup"><span data-stu-id="4b337-138">In this section, you configure and test Azure AD single sign-on with 8x8 Virtual Office based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4b337-139">Tekli çalışmaya oturum için Azure AD ne karşılık gelen kullanıcı 8 x 8 sanal Office Azure AD'de bir kullanıcıya olduğunu bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="4b337-139">For single sign-on to work, Azure AD needs to know what the counterpart user in 8x8 Virtual Office is to a user in Azure AD.</span></span> <span data-ttu-id="4b337-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve ilgili kullanıcı 8 x 8 arasında bir bağlantı ilişkisi sanal Office kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="4b337-140">In other words, a link relationship between an Azure AD user and the related user in 8x8 Virtual Office needs to be established.</span></span>

<span data-ttu-id="4b337-141">8 x 8 sanal ofisinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="4b337-141">In 8x8 Virtual Office, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="4b337-142">Yapılandırma ve Azure AD çoklu oturum açma 8 x 8 sanal Office ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="4b337-142">To configure and test Azure AD single sign-on with 8x8 Virtual Office, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4b337-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="4b337-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4b337-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="4b337-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4b337-145">**[8 x 8 sanal Office test kullanıcısı oluşturma](#creating-a-8x8-virtual-office-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı 8 x 8 sanal Office sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="4b337-145">**[Creating a 8x8 Virtual Office test user](#creating-a-8x8-virtual-office-test-user)** - to have a counterpart of Britta Simon in 8x8 Virtual Office that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="4b337-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="4b337-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4b337-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="4b337-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4b337-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="4b337-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4b337-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma 8 x 8 sanal Office uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="4b337-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your 8x8 Virtual Office application.</span></span>

<span data-ttu-id="4b337-150">**Azure AD çoklu oturum açma 8 x 8 sanal Office ile yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="4b337-150">**To configure Azure AD single sign-on with 8x8 Virtual Office, perform the following steps:**</span></span>

1. <span data-ttu-id="4b337-151">Azure portalında üzerinde **8 x 8 sanal Office** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="4b337-151">In the Azure portal, on the **8x8 Virtual Office** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="4b337-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="4b337-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_samlbase.png)

3. <span data-ttu-id="4b337-155">Üzerinde **8 x 8 sanal Office etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="4b337-155">On the **8x8 Virtual Office Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_url.png)

    <span data-ttu-id="4b337-157">a.</span><span class="sxs-lookup"><span data-stu-id="4b337-157">a.</span></span> <span data-ttu-id="4b337-158">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:</span><span class="sxs-lookup"><span data-stu-id="4b337-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>

    <span data-ttu-id="4b337-159">| `https://sso.8x8.com/<companyname>` |
    | `https://www.8x8.com/<companyname>` |
    | `https://sso.8x8pilot.com/<companyname>` |</span><span class="sxs-lookup"><span data-stu-id="4b337-159">| `https://sso.8x8.com/<companyname>` |
 | `https://www.8x8.com/<companyname>` |
 | `https://sso.8x8pilot.com/<companyname>` |</span></span>

    <span data-ttu-id="4b337-160">b.</span><span class="sxs-lookup"><span data-stu-id="4b337-160">b.</span></span> <span data-ttu-id="4b337-161">İçinde **yanıt URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:</span><span class="sxs-lookup"><span data-stu-id="4b337-161">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>

    <span data-ttu-id="4b337-162">| `https://<subdomain>.8x8.com/saml2` |
    | `https://<subdomain>.8x8pilot.com/saml2`|</span><span class="sxs-lookup"><span data-stu-id="4b337-162">| `https://<subdomain>.8x8.com/saml2` |
 | `https://<subdomain>.8x8pilot.com/saml2`|</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4b337-163">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="4b337-163">These values are not real.</span></span> <span data-ttu-id="4b337-164">Bu değerler gerçek tanımlayıcısı ve yanıt URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="4b337-164">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="4b337-165">Kişi [8 x 8 sanal Office destek ekibi](https://www.8x8.com/about-us/contact-us) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="4b337-165">Contact [8x8 Virtual Office support team](https://www.8x8.com/about-us/contact-us) to get these values.</span></span>
 


4. <span data-ttu-id="4b337-166">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (ham)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="4b337-166">On the **SAML Signing Certificate** section, click **Certificate (Raw)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_certificate.png) 

5. <span data-ttu-id="4b337-168">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4b337-168">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4b337-170">Üzerinde **8 x 8 sanal Office yapılandırma** 'yi tıklatın **yapılandırma 8 x 8 sanal Office** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="4b337-170">On the **8x8 Virtual Office Configuration** section, click **Configure 8x8 Virtual Office** to open **Configure sign-on** window.</span></span> <span data-ttu-id="4b337-171">Kopya **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="4b337-171">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_configure.png) 

7. <span data-ttu-id="4b337-173">8 x 8 sanal Office kiracınız yönetici olarak oturum.</span><span class="sxs-lookup"><span data-stu-id="4b337-173">Sign-on to your 8x8 Virtual Office tenant as an administrator.</span></span>

8. <span data-ttu-id="4b337-174">Seçin **sanal Office hesap Mgr** uygulama panelindeki.</span><span class="sxs-lookup"><span data-stu-id="4b337-174">Select **Virtual Office Account Mgr** on Application Panel.</span></span>
   
    ![Uygulama tarafında yapılandırma](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_001.png)

9. <span data-ttu-id="4b337-176">Seçin **iş** yönetmek tıklatıp hesap **oturum** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4b337-176">Select **Business** account to manage and click **Sign In** button.</span></span>
   
    ![Uygulama tarafında yapılandırma](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_002.png)

10. <span data-ttu-id="4b337-178">Tıklatın **hesapları** menü listesi sekmesindedir.</span><span class="sxs-lookup"><span data-stu-id="4b337-178">Click **Accounts** tab in the menu list.</span></span>
   
    ![Uygulama tarafında yapılandırma](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_003.png)

11. <span data-ttu-id="4b337-180">Tıklatın **çoklu oturum açma** hesaplar listesinde.</span><span class="sxs-lookup"><span data-stu-id="4b337-180">Click **Single Sign On** in the list of Accounts.</span></span>
   
    ![Uygulama tarafında yapılandırma](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_004.png)

12. <span data-ttu-id="4b337-182">Seçin **çoklu oturum açma** kimlik doğrulama yöntemi ve tıklatın altında **SAML**.</span><span class="sxs-lookup"><span data-stu-id="4b337-182">Select **Single Sign On** under Authentication method and click **SAML**.</span></span>
    
    ![Uygulama tarafında yapılandırma](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_005.png)

13. <span data-ttu-id="4b337-184">Kopya **SAML SSO URL**, **tek oturum kapatma hizmeti URL'si** ve **veren URL'si** için Azure AD'den **URL'de oturum**, **oturum kapatma URL'si**  ve **veren URL'si** 8 x 8 sanal Office.</span><span class="sxs-lookup"><span data-stu-id="4b337-184">Copy **SAML SSO URL**, **Single Sing Out Service URL** and **Issuer URL** from Azure AD to **Sign In URL**, **Sign Out URL** and **Issuer URL** in 8x8 Virtual Office.</span></span> 
    
    ![Uygulama tarafında yapılandırma](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_006.png)
    
14. <span data-ttu-id="4b337-186">Tıklatın **tarayıcı** Azure AD'den indirilen sertifikayı karşıya yüklemek için düğmesine tıklayın ve **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4b337-186">Click **Browser** button to upload the certificate which you downloaded from Azure AD, and click the **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="4b337-187">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="4b337-187">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="4b337-188">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="4b337-188">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4b337-189">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4b337-189">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4b337-190">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="4b337-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="4b337-191">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="4b337-191">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="4b337-193">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="4b337-193">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4b337-194">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="4b337-194">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4b337-196">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="4b337-196">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4b337-198">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="4b337-198">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4b337-200">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="4b337-200">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4b337-202">a.</span><span class="sxs-lookup"><span data-stu-id="4b337-202">a.</span></span> <span data-ttu-id="4b337-203">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4b337-203">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4b337-204">b.</span><span class="sxs-lookup"><span data-stu-id="4b337-204">b.</span></span> <span data-ttu-id="4b337-205">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="4b337-205">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4b337-206">c.</span><span class="sxs-lookup"><span data-stu-id="4b337-206">c.</span></span> <span data-ttu-id="4b337-207">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="4b337-207">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="4b337-208">d.</span><span class="sxs-lookup"><span data-stu-id="4b337-208">d.</span></span> <span data-ttu-id="4b337-209">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4b337-209">Click **Create**.</span></span>
 
### <a name="creating-a-8x8-virtual-office-test-user"></a><span data-ttu-id="4b337-210">8 x 8 sanal Office test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="4b337-210">Creating a 8x8 Virtual Office test user</span></span>

<span data-ttu-id="4b337-211">Bu bölümün amacı Britta Simon 8 x 8 sanal ofisinde adlı bir kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="4b337-211">The objective of this section is to create a user called Britta Simon in 8x8 Virtual Office.</span></span> <span data-ttu-id="4b337-212">8 x 8 sanal Office henüz zaman sağlama, varsayılan olarak etkin olduğu destekler.</span><span class="sxs-lookup"><span data-stu-id="4b337-212">8x8 Virtual Office supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="4b337-213">Bu bölümde, eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="4b337-213">There is no action item for you in this section.</span></span> <span data-ttu-id="4b337-214">Yeni bir kullanıcı henüz yoksa 8 x 8 sanal Office erişme denemesi sırasında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="4b337-214">A new user is created during an attempt to access 8x8 Virtual Office if it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="4b337-215">Bir kullanıcı el ile oluşturmanız gerekiyorsa, başvurmanız gerekir [8 x 8 sanal Office destek ekibi](https://www.8x8.com/about-us/contact-us).</span><span class="sxs-lookup"><span data-stu-id="4b337-215">If you need to create a user manually, you need to contact the [8x8 Virtual Office support team](https://www.8x8.com/about-us/contact-us).</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="4b337-216">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="4b337-216">Assigning the Azure AD test user</span></span>

<span data-ttu-id="4b337-217">Bu bölümde, Britta 8 x 8 sanal ofise erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="4b337-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to 8x8 Virtual Office.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="4b337-219">**8 x 8 sanal ofise Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="4b337-219">**To assign Britta Simon to 8x8 Virtual Office, perform the following steps:**</span></span>

1. <span data-ttu-id="4b337-220">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="4b337-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="4b337-222">Uygulamalar listesinde **8 x 8 sanal Office**.</span><span class="sxs-lookup"><span data-stu-id="4b337-222">In the applications list, select **8x8 Virtual Office**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_app.png) 

3. <span data-ttu-id="4b337-224">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="4b337-224">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="4b337-226">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4b337-226">Click **Add** button.</span></span> <span data-ttu-id="4b337-227">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="4b337-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="4b337-229">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="4b337-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="4b337-230">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="4b337-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4b337-231">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="4b337-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4b337-232">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="4b337-232">Testing single sign-on</span></span>

<span data-ttu-id="4b337-233">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="4b337-233">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="4b337-234">Erişim paneli 8 x 8 sanal Office parçasında tıklattığınızda, otomatik olarak 8 x 8 sanal Office uygulamanızda açan.</span><span class="sxs-lookup"><span data-stu-id="4b337-234">When you click the 8x8 Virtual Office tile in the Access Panel, you should get automatically signed-on to your 8x8 Virtual Office application.</span></span>
<span data-ttu-id="4b337-235">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="4b337-235">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md)</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4b337-236">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="4b337-236">Additional resources</span></span>

* [<span data-ttu-id="4b337-237">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="4b337-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4b337-238">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="4b337-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_203.png

