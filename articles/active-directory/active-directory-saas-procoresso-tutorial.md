---
title: "Öğretici: Azure Active Directory Tümleştirme Procore SSO | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Procore SSO arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9818edd3-48c0-411d-b05a-3ec805eafb2e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jeedes
ms.openlocfilehash: 042a41eaa6bb21670b4c12068f1b017222f64b99
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-procore-sso"></a><span data-ttu-id="13e60-103">Öğretici: Azure Active Directory Tümleştirme Procore SSO</span><span class="sxs-lookup"><span data-stu-id="13e60-103">Tutorial: Azure Active Directory integration with Procore SSO</span></span>

<span data-ttu-id="13e60-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Procore SSO tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="13e60-104">In this tutorial, you learn how to integrate Procore SSO with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="13e60-105">Procore SSO Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="13e60-105">Integrating Procore SSO with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="13e60-106">Procore SSO erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="13e60-106">You can control in Azure AD who has access to Procore SSO</span></span>
- <span data-ttu-id="13e60-107">Azure AD hesaplarına otomatik olarak için Procore SSO (çoklu oturum açma) açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="13e60-107">You can enable your users to automatically get signed-on to Procore SSO (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="13e60-108">Hesaplarınızı bir merkezi konumda - Azure Yönetim Portalı'nı yönetme</span><span class="sxs-lookup"><span data-stu-id="13e60-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="13e60-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="13e60-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

To enable single sign-on with Procore SSO, it must be configured to use Azure Active Directory as an identity provider. This guide provides information and tips on how to perform this configuration in Procore SSO.

>[!Note]: 
>This embedded guide is brand new in the new Azure portal, and we’d love to hear your thoughts. Use the Feedback ? button at the top of the portal to provide feedback. The older guide for using the [Azure classic portal](https://manage.windowsazure.com) to configure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="13e60-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="13e60-110">Prerequisites</span></span>

<span data-ttu-id="13e60-111">Azure AD tümleştirme Procore SSO'su yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="13e60-111">To configure Azure AD integration with Procore SSO, you need the following items:</span></span>

- <span data-ttu-id="13e60-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="13e60-112">An Azure AD subscription</span></span>
- <span data-ttu-id="13e60-113">Bir Procore SSO çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="13e60-113">A Procore SSO single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="13e60-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="13e60-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="13e60-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="13e60-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="13e60-116">Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="13e60-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="13e60-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="13e60-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="13e60-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="13e60-118">Scenario description</span></span>
<span data-ttu-id="13e60-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="13e60-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="13e60-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="13e60-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="13e60-121">Galeriden Procore SSO ekleme</span><span class="sxs-lookup"><span data-stu-id="13e60-121">Adding Procore SSO from the gallery</span></span>
2. <span data-ttu-id="13e60-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="13e60-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-procore-sso-from-the-gallery"></a><span data-ttu-id="13e60-123">Galeriden Procore SSO ekleme</span><span class="sxs-lookup"><span data-stu-id="13e60-123">Adding Procore SSO from the gallery</span></span>
<span data-ttu-id="13e60-124">Azure AD Procore SSO tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Procore SSO eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="13e60-124">To configure the integration of Procore SSO into Azure AD, you need to add Procore SSO from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="13e60-125">**Galeriden Procore SSO eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="13e60-125">**To add Procore SSO from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="13e60-126">İçinde  **[Azure Yönetim Portalı](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="13e60-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="13e60-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="13e60-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="13e60-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="13e60-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="13e60-131">Tıklatın **Ekle** iletişim kutusunun üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="13e60-131">Click **Add** button on the top of the dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="13e60-133">Arama kutusuna **Procore SSO**.</span><span class="sxs-lookup"><span data-stu-id="13e60-133">In the search box, type **Procore SSO**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_search.png)

5. <span data-ttu-id="13e60-135">Sonuçlar panelinde seçin **Procore SSO**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="13e60-135">In the results panel, select **Procore SSO**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="13e60-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="13e60-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="13e60-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma Procore "Britta Simon" adlı bir test kullanıcı tabanlı SSO ile test etme.</span><span class="sxs-lookup"><span data-stu-id="13e60-138">In this section, you configure and test Azure AD single sign-on with Procore SSO based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="13e60-139">Tekli çalışmaya oturum için Azure AD ne karşılık gelen Procore SSO bir kullanıcı için Azure AD içinde olduğu bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="13e60-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Procore SSO is to a user in Azure AD.</span></span> <span data-ttu-id="13e60-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve ilgili kullanıcı Procore SSO arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="13e60-140">In other words, a link relationship between an Azure AD user and the related user in Procore SSO needs to be established.</span></span>

<span data-ttu-id="13e60-141">Bu bağlantı değeri atayarak ilişkisi **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** Procore sso.</span><span class="sxs-lookup"><span data-stu-id="13e60-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Procore SSO.</span></span>

<span data-ttu-id="13e60-142">Yapılandırmak ve Azure AD çoklu oturum açma Procore SSO sınamak için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="13e60-142">To configure and test Azure AD single sign-on with Procore SSO, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="13e60-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="13e60-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="13e60-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="13e60-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="13e60-145">**[Procore SSO test kullanıcısı oluşturma](#creating-a-procore-sso-test-user)**  - Britta Simon, karşılık gelen her, Azure AD gösterimine bağlı Procore SSO sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="13e60-145">**[Creating a Procore SSO test user](#creating-a-procore-sso-test-user)** - to have a counterpart of Britta Simon in Procore SSO that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="13e60-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="13e60-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="13e60-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="13e60-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="13e60-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="13e60-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="13e60-149">Bu bölümde, Azure AD çoklu oturum açma Azure Yönetim Portalı'nda etkinleştirin ve çoklu oturum açma Procore SSO uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="13e60-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Procore SSO application.</span></span>

<span data-ttu-id="13e60-150">**Azure AD çoklu oturum açma Procore SSO'su yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="13e60-150">**To configure Azure AD single sign-on with Procore SSO, perform the following steps:**</span></span>

1. <span data-ttu-id="13e60-151">Azure Yönetim Portalı'nda üzerinde **Procore SSO** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="13e60-151">In the Azure Management portal, on the **Procore SSO** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="13e60-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="13e60-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_samlbase.png)

3. <span data-ttu-id="13e60-155">Üzerinde **Procore SSO etki alanı ve URL'leri** bölümü, kullanıcı gerekmez uygulama zaten Azure ile önceden tümleştirilmiş gibi tüm adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="13e60-155">On the **Procore SSO Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_url.png)

4. <span data-ttu-id="13e60-157">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve XML dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="13e60-157">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_certificate.png) 

5. <span data-ttu-id="13e60-159">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="13e60-159">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-procoresso-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="13e60-161">Üzerinde **Procore SSO yapılandırma** 'yi tıklatın **yapılandırma Procore SSO** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="13e60-161">On the **Procore SSO Configuration** section, click **Configure Procore SSO** to open **Configure sign-on** window.</span></span> <span data-ttu-id="13e60-162">Kopya **SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="13e60-162">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_configure.png) 

7. <span data-ttu-id="13e60-164">Çoklu oturum açma yapılandırmak için **Procore SSO** tarafı, procore şirket siteniz bir yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="13e60-164">To configure single sign-on on **Procore SSO** side, login to your procore company site as an administrator.</span></span>

8. <span data-ttu-id="13e60-165">Araç kutusu açılır, aşağı, tıklayın **yönetici** SSO ayarları sayfasını açın.</span><span class="sxs-lookup"><span data-stu-id="13e60-165">From the toolbox drop down, click on **Admin** to open the SSO settings page.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-procoresso-tutorial/procore_tool_admin.png)

9. <span data-ttu-id="13e60-167">Aşağıdaki - açıklandığı gibi değerler kutularına yapıştırın</span><span class="sxs-lookup"><span data-stu-id="13e60-167">Paste the values in the boxes as described below-</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-procoresso-tutorial/procore_setting_admin.png)    

    <span data-ttu-id="13e60-169">a.</span><span class="sxs-lookup"><span data-stu-id="13e60-169">a.</span></span> <span data-ttu-id="13e60-170">İçinde **tek oturum üzerinde veren URL'si** kutusu, SAML varlık kimliği kopyalanan Azure portalından Yapıştır.</span><span class="sxs-lookup"><span data-stu-id="13e60-170">In the **Single Sign On Issuer URL** box, paste the SAML Entity ID copied from the Azure portal.</span></span>

    <span data-ttu-id="13e60-171">b.</span><span class="sxs-lookup"><span data-stu-id="13e60-171">b.</span></span> <span data-ttu-id="13e60-172">İçinde **hedef URL üzerinde SAML oturum** kutusu, SAML çoklu oturum açma hizmet URL'si kopyalanan Azure portalından Yapıştır.</span><span class="sxs-lookup"><span data-stu-id="13e60-172">In the **SAML Sign On Target URL** box, paste the SAML Single Sign-On Service URL copied from the Azure portal.</span></span>

    <span data-ttu-id="13e60-173">c.</span><span class="sxs-lookup"><span data-stu-id="13e60-173">c.</span></span> <span data-ttu-id="13e60-174">Şimdi açmak **meta veri XML** yukarıda Azure portalından indirdiğiniz ve sertifikası adlı etiketinde kopyalama **X509Certificate**.</span><span class="sxs-lookup"><span data-stu-id="13e60-174">Now open the **Metadata XML** downloaded above from the Azure portal and copy the certficate in the tag named **X509Certificate**.</span></span> <span data-ttu-id="13e60-175">Kopyalanan değeri içine yapıştırabilirsiniz **çoklu oturum açma x509 sertifika** kutusu.</span><span class="sxs-lookup"><span data-stu-id="13e60-175">Paste the copied value into the **Single Sign On x509 Certificate** box.</span></span>

10. <span data-ttu-id="13e60-176">Tıklayın **değişiklikleri kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="13e60-176">Click on **Save Changes**.</span></span>

11. <span data-ttu-id="13e60-177">Bu ayarları sonra göndermesi gerekir. **etki alanı adı** (örneğin **contoso.com**) için Procore uygulamasına, oturum açtığınız aracılığıyla [Procore destek ekibi](https://support.procore.com/) ve bunlar Bu etki alanı için Federasyon SSO etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="13e60-177">After these settings, you needs to send the **domain name** (e.g **contoso.com**) through which you are logging into Procore to the [Procore Support team](https://support.procore.com/) and they will activate federated SSO for that domain.</span></span>

<!--### Next steps

To ensure users can sign-in to Procore SSO after it has been configured to use Azure Active Directory, review the following tasks and topics:

- User accounts must be pre-provisioned into Procore SSO prior to sign-in. To set this up, see Provisioning.
 
- Users must be assigned access to Procore SSO in Azure AD to sign-in. To assign users, see Users.
 
- To configure access polices for Procore SSO users, see Access Policies.
 
- For additional information on deploying single sign-on to users, see [this article](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="13e60-178">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="13e60-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="13e60-179">Bu bölümün amacı, Britta Simon adlı Azure Yönetim Portalı'nda bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="13e60-179">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="13e60-181">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="13e60-181">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="13e60-182">İçinde **Azure Yönetim Portalı**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="13e60-182">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-procoresso-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="13e60-184">Git **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar** kullanıcıların listesini görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="13e60-184">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-procoresso-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="13e60-186">İletişim kutusunun üstündeki **Ekle** açmak için **kullanıcı** iletişim.</span><span class="sxs-lookup"><span data-stu-id="13e60-186">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-procoresso-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="13e60-188">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="13e60-188">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-procoresso-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="13e60-190">a.</span><span class="sxs-lookup"><span data-stu-id="13e60-190">a.</span></span> <span data-ttu-id="13e60-191">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="13e60-191">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="13e60-192">b.</span><span class="sxs-lookup"><span data-stu-id="13e60-192">b.</span></span> <span data-ttu-id="13e60-193">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="13e60-193">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="13e60-194">c.</span><span class="sxs-lookup"><span data-stu-id="13e60-194">c.</span></span> <span data-ttu-id="13e60-195">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="13e60-195">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="13e60-196">d.</span><span class="sxs-lookup"><span data-stu-id="13e60-196">d.</span></span> <span data-ttu-id="13e60-197">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="13e60-197">Click **Create**.</span></span>
 
### <a name="creating-a-procore-sso-test-user"></a><span data-ttu-id="13e60-198">Procore SSO test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="13e60-198">Creating a Procore SSO test user</span></span>

<span data-ttu-id="13e60-199">Lütfen izleyin kendi tarafında Procore test kullanıcısı oluşturmak için aşağıdaki adımları.</span><span class="sxs-lookup"><span data-stu-id="13e60-199">Please follow the below steps to create a Procore test user on their side.</span></span>

1. <span data-ttu-id="13e60-200">Procore şirket siteniz bir yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="13e60-200">Login to your procore company site as an administrator.</span></span>  

2. <span data-ttu-id="13e60-201">Araç kutusu açılır, aşağı, tıklayın **Directory** şirket dizin sayfasını açın.</span><span class="sxs-lookup"><span data-stu-id="13e60-201">From the toolbox drop down, click on **Directory** to open the company directory page.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-procoresso-tutorial/Procore_sso_directory.png)

3. <span data-ttu-id="13e60-203">Tıklayın **bir kişi Ekle** formunu açmak ve girmek için seçenek seçenekler - gerçekleştirin</span><span class="sxs-lookup"><span data-stu-id="13e60-203">Click on **Add a Person** option to open the form and enter perform following options -</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-procoresso-tutorial/Procore_user_add.png)

    <span data-ttu-id="13e60-205">a.</span><span class="sxs-lookup"><span data-stu-id="13e60-205">a.</span></span> <span data-ttu-id="13e60-206">İçinde **ad** metin kutusuna, türü kullanıcının ilk adını gibi **Britta**.</span><span class="sxs-lookup"><span data-stu-id="13e60-206">In the **First Name** textbox, type user's first name like **Britta**.</span></span>

    <span data-ttu-id="13e60-207">b.</span><span class="sxs-lookup"><span data-stu-id="13e60-207">b.</span></span> <span data-ttu-id="13e60-208">İçinde **Soyadı** metin kutusuna, türü kullanıcının soyadını gibi **Simon**.</span><span class="sxs-lookup"><span data-stu-id="13e60-208">In the **Last name** textbox, type user's last name like **Simon**.</span></span>

    <span data-ttu-id="13e60-209">c.</span><span class="sxs-lookup"><span data-stu-id="13e60-209">c.</span></span> <span data-ttu-id="13e60-210">İçinde **e-posta adresi** türü kullanıcının e-posta adresi metin kutusuna, ister  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="13e60-210">In the **Email Address** textbox, type user's email address like **BrittaSimon@contoso.com**.</span></span>

    <span data-ttu-id="13e60-211">d.</span><span class="sxs-lookup"><span data-stu-id="13e60-211">d.</span></span> <span data-ttu-id="13e60-212">Seçin **izin şablonu** olarak **izin şablonu daha sonra uygulamak**.</span><span class="sxs-lookup"><span data-stu-id="13e60-212">Select **Permission Template** as **Apply Permission Template Later**.</span></span>

    <span data-ttu-id="13e60-213">e.</span><span class="sxs-lookup"><span data-stu-id="13e60-213">e.</span></span> <span data-ttu-id="13e60-214">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="13e60-214">Click **Create**.</span></span>

4. <span data-ttu-id="13e60-215">Kontrol edin ve yeni eklenen kişi ayrıntılarını güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="13e60-215">Check and update the details for the newly added contact.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-procoresso-tutorial/Procore_user_check.png)

5. <span data-ttu-id="13e60-217">Tıklayın **Kaydet ve Gönder daveti** (posta yoluyla bir davet gerekliyse) veya **kaydetmek** (kullanıcı kayıt işlemini tamamlamak için doğrudan Kaydet).</span><span class="sxs-lookup"><span data-stu-id="13e60-217">Click on **Save and Send Invitiation** (if an invite through mail is required) or **Save** (Save directly) to complete the user registration.</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-procoresso-tutorial/Procore_user_save.png)    

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="13e60-219">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="13e60-219">Assigning the Azure AD test user</span></span>

<span data-ttu-id="13e60-220">Bu bölümde, Britta Procore SSO kendi erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="13e60-220">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Procore SSO.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="13e60-222">**Britta Simon Procore SSO atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="13e60-222">**To assign Britta Simon to Procore SSO, perform the following steps:**</span></span>

1. <span data-ttu-id="13e60-223">Azure Yönetim Portalı'nda uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="13e60-223">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="13e60-225">Uygulamalar listesinde **Procore SSO**.</span><span class="sxs-lookup"><span data-stu-id="13e60-225">In the applications list, select **Procore SSO**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_app.png) 

3. <span data-ttu-id="13e60-227">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="13e60-227">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="13e60-229">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="13e60-229">Click **Add** button.</span></span> <span data-ttu-id="13e60-230">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="13e60-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="13e60-232">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="13e60-232">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="13e60-233">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="13e60-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="13e60-234">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="13e60-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="13e60-235">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="13e60-235">Testing single sign-on</span></span>

<span data-ttu-id="13e60-236">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="13e60-236">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="13e60-237">Çoklu oturum açma ayarlarınızı test etmek isterseniz, erişim paneli açın.</span><span class="sxs-lookup"><span data-stu-id="13e60-237">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="13e60-238">Erişim paneli hakkında daha fazla ayrıntı için bkz: [erişim Paneli'ne giriş](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="13e60-238">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> <span data-ttu-id="13e60-239">Erişim paneli Procore SSO parçasında tıklattığınızda, otomatik olarak Procore SSO uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="13e60-239">When you click the Procore SSO tile in the Access Panel, you should get automatically signed-on to your Procore SSO application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="13e60-240">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="13e60-240">Additional resources</span></span>

* [<span data-ttu-id="13e60-241">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="13e60-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="13e60-242">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="13e60-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_203.png

