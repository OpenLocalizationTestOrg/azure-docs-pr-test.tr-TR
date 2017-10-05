---
title: "Öğretici: Azure Active Directory Tümleştirme SkyDesk e-posta ile | Microsoft Docs"
description: "Çoklu oturum açma SkyDesk e-posta ile Azure Active Directory arasındaki yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a9d0bbcb-ddb5-473f-a4aa-028ae88ced1a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: 0ffcca4161fc836192fc9c9871a905f36ea76b32
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-skydesk-email"></a><span data-ttu-id="7fc29-103">Öğretici: Azure Active Directory Tümleştirme SkyDesk e-posta ile</span><span class="sxs-lookup"><span data-stu-id="7fc29-103">Tutorial: Azure Active Directory integration with SkyDesk Email</span></span>

<span data-ttu-id="7fc29-104">Bu öğreticide, Azure Active Directory (Azure AD) ile SkyDesk e-posta tümleştirme öğrenin.</span><span class="sxs-lookup"><span data-stu-id="7fc29-104">In this tutorial, you learn how to integrate SkyDesk Email with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7fc29-105">Azure AD ile SkyDesk e-posta tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="7fc29-105">Integrating SkyDesk Email with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7fc29-106">SkyDesk e-posta erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="7fc29-106">You can control in Azure AD who has access to SkyDesk Email</span></span>
- <span data-ttu-id="7fc29-107">Azure AD hesaplarına otomatik olarak SkyDesk e-posta (çoklu oturum açma) açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="7fc29-107">You can enable your users to automatically get signed-on to SkyDesk Email (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7fc29-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="7fc29-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7fc29-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7fc29-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7fc29-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="7fc29-110">Prerequisites</span></span>

<span data-ttu-id="7fc29-111">Azure AD tümleştirme SkyDesk e-posta ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="7fc29-111">To configure Azure AD integration with SkyDesk Email, you need the following items:</span></span>

- <span data-ttu-id="7fc29-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="7fc29-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7fc29-113">Bir SkyDesk e-posta çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="7fc29-113">A SkyDesk Email single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7fc29-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="7fc29-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7fc29-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="7fc29-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7fc29-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="7fc29-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7fc29-117">Bir Azure AD deneme ortam yoksa, burada bir aylık deneme alabilirsiniz [deneme teklifi](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7fc29-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7fc29-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="7fc29-118">Scenario description</span></span>
<span data-ttu-id="7fc29-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="7fc29-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7fc29-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="7fc29-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7fc29-121">Galeriden SkyDesk e-posta ekleme</span><span class="sxs-lookup"><span data-stu-id="7fc29-121">Adding SkyDesk Email from the gallery</span></span>
2. <span data-ttu-id="7fc29-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="7fc29-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-skydesk-email-from-the-gallery"></a><span data-ttu-id="7fc29-123">Galeriden SkyDesk e-posta ekleme</span><span class="sxs-lookup"><span data-stu-id="7fc29-123">Adding SkyDesk Email from the gallery</span></span>
<span data-ttu-id="7fc29-124">Azure AD SkyDesk e-posta tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden SkyDesk e-posta eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="7fc29-124">To configure the integration of SkyDesk Email into Azure AD, you need to add SkyDesk Email from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7fc29-125">**Galeriden SkyDesk e-posta eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7fc29-125">**To add SkyDesk Email from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7fc29-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="7fc29-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7fc29-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="7fc29-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7fc29-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="7fc29-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="7fc29-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7fc29-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="7fc29-133">Arama kutusuna **SkyDesk e-posta**.</span><span class="sxs-lookup"><span data-stu-id="7fc29-133">In the search box, type **SkyDesk Email**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_search.png)

5. <span data-ttu-id="7fc29-135">Sonuçlar panelinde seçin **SkyDesk e-posta**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7fc29-135">In the results panel, select **SkyDesk Email**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7fc29-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="7fc29-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7fc29-138">Bu bölümde, yapılandırmanız ve SkyDesk e-posta ile Azure AD çoklu oturum açmayı test "Britta Simon" adlı bir test kullanıcı tabanlı.</span><span class="sxs-lookup"><span data-stu-id="7fc29-138">In this section, you configure and test Azure AD single sign-on with SkyDesk Email based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7fc29-139">Tekli çalışmaya oturum için Azure AD ne karşılık gelen SkyDesk e-posta içinde bir kullanıcı için Azure AD içinde olduğu bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="7fc29-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SkyDesk Email is to a user in Azure AD.</span></span> <span data-ttu-id="7fc29-140">Diğer bir deyişle, bir Azure AD kullanıcısının SkyDesk e-posta ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7fc29-140">In other words, a link relationship between an Azure AD user and the related user in SkyDesk Email needs to be established.</span></span>

<span data-ttu-id="7fc29-141">Değeri SkyDesk postada atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="7fc29-141">In SkyDesk Email, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="7fc29-142">Yapılandırma ve Azure AD çoklu oturum açma SkyDesk e-posta ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="7fc29-142">To configure and test Azure AD single sign-on with SkyDesk Email, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7fc29-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="7fc29-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7fc29-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="7fc29-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7fc29-145">**[SkyDesk e-posta test kullanıcısı oluşturma](#creating-a-skydesk-email-test-user)**  - Britta Simon, karşılık gelen SkyDesk kullanıcı Azure AD gösterimini bağlantılı e-posta olmayacağını.</span><span class="sxs-lookup"><span data-stu-id="7fc29-145">**[Creating a SkyDesk Email test user](#creating-a-skydesk-email-test-user)** - to have a counterpart of Britta Simon in SkyDesk Email that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7fc29-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="7fc29-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7fc29-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="7fc29-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7fc29-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="7fc29-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7fc29-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma SkyDesk e-posta uygulamanızı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="7fc29-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SkyDesk Email application.</span></span>

<span data-ttu-id="7fc29-150">**Azure AD çoklu oturum açma SkyDesk e-posta ile yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7fc29-150">**To configure Azure AD single sign-on with SkyDesk Email, perform the following steps:**</span></span>

1. <span data-ttu-id="7fc29-151">Azure portalında üzerinde **SkyDesk e-posta** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="7fc29-151">In the Azure portal, on the **SkyDesk Email** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="7fc29-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="7fc29-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_samlbase.png)

3. <span data-ttu-id="7fc29-155">Üzerinde **SkyDesk e-posta etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="7fc29-155">On the **SkyDesk Email Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_url.png)

    <span data-ttu-id="7fc29-157">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://mail.skydesk.jp/portal/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="7fc29-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://mail.skydesk.jp/portal/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7fc29-158">Değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="7fc29-158">The value is not real.</span></span> <span data-ttu-id="7fc29-159">Değerin gerçek oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="7fc29-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="7fc29-160">Kişi [SkyDesk e-posta istemcisi destek ekibi](https://www.skydesk.sg/support/) değeri alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="7fc29-160">Contact [SkyDesk Email Client support team](https://www.skydesk.sg/support/) to get the value.</span></span> 
 
4. <span data-ttu-id="7fc29-161">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="7fc29-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_certificate.png) 

5. <span data-ttu-id="7fc29-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7fc29-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7fc29-165">Üzerinde **SkyDesk e-posta Yapılandırması** 'yi tıklatın **SkyDesk e-posta Yapılandırma** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="7fc29-165">On the **SkyDesk Email Configuration** section, click **Configure SkyDesk Email** to open **Configure sign-on** window.</span></span> <span data-ttu-id="7fc29-166">Kopya **Sign-Out URL ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="7fc29-166">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_configure.png) 

7. <span data-ttu-id="7fc29-168">İçinde SSO'yu etkinleştirmek için **SkyDesk e-posta**, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="7fc29-168">To enable SSO in **SkyDesk Email**, perform the following steps:</span></span>

    <span data-ttu-id="7fc29-169">a.</span><span class="sxs-lookup"><span data-stu-id="7fc29-169">a.</span></span> <span data-ttu-id="7fc29-170">SkyDesk e-posta hesabınız yönetici olarak oturum.</span><span class="sxs-lookup"><span data-stu-id="7fc29-170">Sign-on to your SkyDesk Email account as administrator.</span></span>

    <span data-ttu-id="7fc29-171">b.</span><span class="sxs-lookup"><span data-stu-id="7fc29-171">b.</span></span> <span data-ttu-id="7fc29-172">Üstteki menüde tıklatın **Kurulum**seçip **Org**.</span><span class="sxs-lookup"><span data-stu-id="7fc29-172">In the menu on the top, click **Setup**, and select **Org**.</span></span> 
    
      ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_51.png)
  
    <span data-ttu-id="7fc29-174">c.</span><span class="sxs-lookup"><span data-stu-id="7fc29-174">c.</span></span> <span data-ttu-id="7fc29-175">Tıklayın **etki alanları** sol panelindeki.</span><span class="sxs-lookup"><span data-stu-id="7fc29-175">Click on **Domains** from the left panel.</span></span>
    
      ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_53.png)

    <span data-ttu-id="7fc29-177">d.</span><span class="sxs-lookup"><span data-stu-id="7fc29-177">d.</span></span> <span data-ttu-id="7fc29-178">Tıklayın **etki alanı ekleme**.</span><span class="sxs-lookup"><span data-stu-id="7fc29-178">Click on **Add Domain**.</span></span>
    
      ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_54.png)

    <span data-ttu-id="7fc29-180">e.</span><span class="sxs-lookup"><span data-stu-id="7fc29-180">e.</span></span> <span data-ttu-id="7fc29-181">Etki alanı adınızı girin ve ardından etki alanını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="7fc29-181">Enter your Domain name, and then verify the Domain.</span></span>
    
      ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_55.png)

    <span data-ttu-id="7fc29-183">f.</span><span class="sxs-lookup"><span data-stu-id="7fc29-183">f.</span></span> <span data-ttu-id="7fc29-184">Tıklayın **SAML kimlik doğrulaması** sol panelindeki.</span><span class="sxs-lookup"><span data-stu-id="7fc29-184">Click on **SAML Authentication** from the left panel.</span></span>
    
      ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_52.png)

8. <span data-ttu-id="7fc29-186">Üzerinde **SAML kimlik doğrulaması** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="7fc29-186">On the **SAML Authentication** dialog page, perform the following steps:</span></span>
   
      ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_56.png)
   
    >[!NOTE]
    ><span data-ttu-id="7fc29-188">SAML tabanlı kimlik doğrulaması kullanmak için ya da olmalıdır **etki alanını doğruladıysanız** veya **portalı URL'si** kurulumu.</span><span class="sxs-lookup"><span data-stu-id="7fc29-188">To use SAML based authentication, you should either have **verified domain** or **portal URL** setup.</span></span> <span data-ttu-id="7fc29-189">Portal ayarlayabilirsiniz URL benzersiz bir ad ile.</span><span class="sxs-lookup"><span data-stu-id="7fc29-189">You can set the portal URL with the unique name.</span></span>
    > 
    > 
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_57.png)

    <span data-ttu-id="7fc29-191">a.</span><span class="sxs-lookup"><span data-stu-id="7fc29-191">a.</span></span> <span data-ttu-id="7fc29-192">İçinde **oturum açma URL'si** metin değerini yapıştırın **SAML çoklu oturum açma hizmet URL'si**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="7fc29-192">In the **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="7fc29-193">b.</span><span class="sxs-lookup"><span data-stu-id="7fc29-193">b.</span></span> <span data-ttu-id="7fc29-194">İçinde **oturum kapatma** URL textbox değeri yapıştırın **Sign-Out URL**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="7fc29-194">In the **Logout** URL textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="7fc29-195">c.</span><span class="sxs-lookup"><span data-stu-id="7fc29-195">c.</span></span> <span data-ttu-id="7fc29-196">**Değiştirme parola URL'si** isteğe bağlı olduğu kadar boş bırakın.</span><span class="sxs-lookup"><span data-stu-id="7fc29-196">**Change Password URL** is optional so leave it blank.</span></span>

    <span data-ttu-id="7fc29-197">d.</span><span class="sxs-lookup"><span data-stu-id="7fc29-197">d.</span></span> <span data-ttu-id="7fc29-198">Tıklayın **anahtarı dosyadan al** Azure Portalı'ndan indirilen sertifikanızı seçin ve ardından **açık** sertifikayı karşıya yüklemek için.</span><span class="sxs-lookup"><span data-stu-id="7fc29-198">Click on **Get Key From File** to select your downloaded certificate from Azure portal, and then click **Open** to upload the certificate.</span></span>

    <span data-ttu-id="7fc29-199">e.</span><span class="sxs-lookup"><span data-stu-id="7fc29-199">e.</span></span> <span data-ttu-id="7fc29-200">Olarak **algoritması**seçin **RSA**.</span><span class="sxs-lookup"><span data-stu-id="7fc29-200">As **Algorithm**, select **RSA**.</span></span>

    <span data-ttu-id="7fc29-201">f.</span><span class="sxs-lookup"><span data-stu-id="7fc29-201">f.</span></span> <span data-ttu-id="7fc29-202">Tıklatın **Tamam** değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="7fc29-202">Click **Ok** to save the changes.</span></span>

> [!TIP]
> <span data-ttu-id="7fc29-203">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="7fc29-203">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7fc29-204">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="7fc29-204">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7fc29-205">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7fc29-205">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7fc29-206">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7fc29-206">Creating an Azure AD test user</span></span>
<span data-ttu-id="7fc29-207">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="7fc29-207">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="7fc29-209">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7fc29-209">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7fc29-210">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="7fc29-210">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7fc29-212">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="7fc29-212">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7fc29-214">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="7fc29-214">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7fc29-216">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="7fc29-216">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7fc29-218">a.</span><span class="sxs-lookup"><span data-stu-id="7fc29-218">a.</span></span> <span data-ttu-id="7fc29-219">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7fc29-219">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7fc29-220">b.</span><span class="sxs-lookup"><span data-stu-id="7fc29-220">b.</span></span> <span data-ttu-id="7fc29-221">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="7fc29-221">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7fc29-222">c.</span><span class="sxs-lookup"><span data-stu-id="7fc29-222">c.</span></span> <span data-ttu-id="7fc29-223">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="7fc29-223">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7fc29-224">d.</span><span class="sxs-lookup"><span data-stu-id="7fc29-224">d.</span></span> <span data-ttu-id="7fc29-225">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7fc29-225">Click **Create**.</span></span>
 
### <a name="creating-a-skydesk-email-test-user"></a><span data-ttu-id="7fc29-226">SkyDesk e-posta test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7fc29-226">Creating a SkyDesk Email test user</span></span>

<span data-ttu-id="7fc29-227">Bu bölümde, Britta Simon SkyDesk e-postayla adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7fc29-227">In this section, you create a user called Britta Simon in SkyDesk Email.</span></span>

1. <span data-ttu-id="7fc29-228">Tıklayın **kullanıcı erişimini** sol panel SkyDesk e-posta ve kullanıcı adınızı girin.</span><span class="sxs-lookup"><span data-stu-id="7fc29-228">Click on **User Access** from the left panel in SkyDesk Email and then enter your username.</span></span> 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_58.png)

>[!NOTE] 
><span data-ttu-id="7fc29-230">Toplu kullanıcılar oluşturmanız gerekiyorsa, başvurmanız gerekir [SkyDesk e-posta istemcisi destek ekibi](https://www.skydesk.sg/support/).</span><span class="sxs-lookup"><span data-stu-id="7fc29-230">If you need to create bulk users, you need to contact the [SkyDesk Email Client support team](https://www.skydesk.sg/support/).</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7fc29-231">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="7fc29-231">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7fc29-232">Bu bölümde, Britta SkyDesk e-postasına erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="7fc29-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SkyDesk Email.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="7fc29-234">**SkyDesk e-posta Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7fc29-234">**To assign Britta Simon to SkyDesk Email, perform the following steps:**</span></span>

1. <span data-ttu-id="7fc29-235">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="7fc29-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="7fc29-237">Uygulamalar listesinde **SkyDesk e-posta**.</span><span class="sxs-lookup"><span data-stu-id="7fc29-237">In the applications list, select **SkyDesk Email**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_app.png) 

3. <span data-ttu-id="7fc29-239">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="7fc29-239">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="7fc29-241">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7fc29-241">Click **Add** button.</span></span> <span data-ttu-id="7fc29-242">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="7fc29-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="7fc29-244">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="7fc29-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7fc29-245">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="7fc29-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7fc29-246">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="7fc29-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7fc29-247">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="7fc29-247">Testing single sign-on</span></span>

<span data-ttu-id="7fc29-248">Bu bölümün amacı erişim paneli kullanılarak Azure AD SSO yapılandırmanızı test etmektir.</span><span class="sxs-lookup"><span data-stu-id="7fc29-248">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="7fc29-249">Erişim paneli SkyDesk e-posta parçasında tıklattığınızda, otomatik olarak SkyDesk e-posta uygulamanızı açan.</span><span class="sxs-lookup"><span data-stu-id="7fc29-249">When you click the SkyDesk Email tile in the Access Panel, you should get automatically signed-on to your SkyDesk Email application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7fc29-250">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="7fc29-250">Additional resources</span></span>

* [<span data-ttu-id="7fc29-251">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="7fc29-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7fc29-252">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="7fc29-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_203.png

