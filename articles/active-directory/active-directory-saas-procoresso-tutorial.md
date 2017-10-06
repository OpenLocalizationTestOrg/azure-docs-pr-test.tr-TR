---
title: "Öğretici: Azure Active Directory Tümleştirme Procore SSO | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Procore SSO arasında."
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
ms.openlocfilehash: bb918617f18ba3f44ddde469e6fc411977752f15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-procore-sso"></a><span data-ttu-id="984c7-103">Öğretici: Azure Active Directory Tümleştirme Procore SSO</span><span class="sxs-lookup"><span data-stu-id="984c7-103">Tutorial: Azure Active Directory integration with Procore SSO</span></span>

<span data-ttu-id="984c7-104">Bu öğreticide, bilgi nasıl toointegrate Procore SSO Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="984c7-104">In this tutorial, you learn how toointegrate Procore SSO with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="984c7-105">Procore SSO Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="984c7-105">Integrating Procore SSO with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="984c7-106">Erişim tooProcore SSO sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="984c7-106">You can control in Azure AD who has access tooProcore SSO</span></span>
- <span data-ttu-id="984c7-107">Kullanıcıların tooautomatically get açan tooProcore SSO (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="984c7-107">You can enable your users tooautomatically get signed-on tooProcore SSO (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="984c7-108">Bir merkezi konumda - hello Azure Yönetim Portalı hesaplarınızı yönetebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="984c7-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="984c7-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="984c7-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

tooenable single sign-on with Procore SSO, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Procore SSO.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="984c7-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="984c7-110">Prerequisites</span></span>

<span data-ttu-id="984c7-111">tooconfigure Procore SSO ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="984c7-111">tooconfigure Azure AD integration with Procore SSO, you need hello following items:</span></span>

- <span data-ttu-id="984c7-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="984c7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="984c7-113">Bir Procore SSO çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="984c7-113">A Procore SSO single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="984c7-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="984c7-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="984c7-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="984c7-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="984c7-116">Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="984c7-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="984c7-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="984c7-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="984c7-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="984c7-118">Scenario description</span></span>
<span data-ttu-id="984c7-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="984c7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="984c7-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="984c7-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="984c7-121">Merhaba Galerisi'nden Procore SSO ekleme</span><span class="sxs-lookup"><span data-stu-id="984c7-121">Adding Procore SSO from hello gallery</span></span>
2. <span data-ttu-id="984c7-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="984c7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-procore-sso-from-hello-gallery"></a><span data-ttu-id="984c7-123">Merhaba Galerisi'nden Procore SSO ekleme</span><span class="sxs-lookup"><span data-stu-id="984c7-123">Adding Procore SSO from hello gallery</span></span>
<span data-ttu-id="984c7-124">Azure AD'ye tooconfigure hello tümleştirme Procore sso'nun tooadd Procore SSO hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="984c7-124">tooconfigure hello integration of Procore SSO into Azure AD, you need tooadd Procore SSO from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="984c7-125">**tooadd hello galerisinden Procore SSO hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="984c7-125">**tooadd Procore SSO from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="984c7-126">Merhaba,  **[Azure Yönetim Portalı](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="984c7-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="984c7-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="984c7-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="984c7-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="984c7-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="984c7-131">Tıklatın **Ekle** hello iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="984c7-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="984c7-133">Merhaba arama kutusuna yazın **Procore SSO**.</span><span class="sxs-lookup"><span data-stu-id="984c7-133">In hello search box, type **Procore SSO**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_search.png)

5. <span data-ttu-id="984c7-135">Merhaba Sonuçlar panelinde seçin **Procore SSO**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="984c7-135">In hello results panel, select **Procore SSO**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="984c7-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="984c7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="984c7-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma Procore "Britta Simon" adlı bir test kullanıcı tabanlı SSO ile test etme.</span><span class="sxs-lookup"><span data-stu-id="984c7-138">In this section, you configure and test Azure AD single sign-on with Procore SSO based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="984c7-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Procore SSO tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="984c7-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Procore SSO is tooa user in Azure AD.</span></span> <span data-ttu-id="984c7-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve Procore SSO hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="984c7-140">In other words, a link relationship between an Azure AD user and hello related user in Procore SSO needs toobe established.</span></span>

<span data-ttu-id="984c7-141">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** Procore sso.</span><span class="sxs-lookup"><span data-stu-id="984c7-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Procore SSO.</span></span>

<span data-ttu-id="984c7-142">tooconfigure ve Procore SSO ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="984c7-142">tooconfigure and test Azure AD single sign-on with Procore SSO, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="984c7-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="984c7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="984c7-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="984c7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="984c7-145">**[Procore SSO test kullanıcısı oluşturma](#creating-a-procore-sso-test-user)**  -toohave karşılık gelen her bağlantılı toohello Azure AD gösterimidir Procore SSO Britta Simon biri.</span><span class="sxs-lookup"><span data-stu-id="984c7-145">**[Creating a Procore SSO test user](#creating-a-procore-sso-test-user)** - toohave a counterpart of Britta Simon in Procore SSO that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="984c7-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="984c7-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="984c7-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="984c7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="984c7-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="984c7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="984c7-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure Yönetim Portalı'nda etkinleştirin ve çoklu oturum açma Procore SSO uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="984c7-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Procore SSO application.</span></span>

<span data-ttu-id="984c7-150">**tooconfigure Azure AD çoklu oturum açma Procore SSO hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="984c7-150">**tooconfigure Azure AD single sign-on with Procore SSO, perform hello following steps:**</span></span>

1. <span data-ttu-id="984c7-151">Merhaba üzerinde hello Azure Yönetim Portalı'nda **Procore SSO** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="984c7-151">In hello Azure Management portal, on hello **Procore SSO** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="984c7-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="984c7-153">On hello **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_samlbase.png)

3. <span data-ttu-id="984c7-155">Merhaba üzerinde **Procore SSO etki alanı ve URL'leri** bölümünde, hello uygulama zaten Azure ile önceden tümleştirilmiş gibi hello kullanıcının tooperform herhangi bir adımı yok.</span><span class="sxs-lookup"><span data-stu-id="984c7-155">On hello **Procore SSO Domain and URLs** section, hello user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_url.png)

4. <span data-ttu-id="984c7-157">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello XML dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="984c7-157">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_certificate.png) 

5. <span data-ttu-id="984c7-159">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="984c7-159">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-procoresso-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="984c7-161">Merhaba üzerinde **Procore SSO yapılandırma** 'yi tıklatın **yapılandırma Procore SSO** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="984c7-161">On hello **Procore SSO Configuration** section, click **Configure Procore SSO** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="984c7-162">Kopya hello **SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="984c7-162">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_configure.png) 

7. <span data-ttu-id="984c7-164">tooconfigure çoklu oturum açma üzerinde **Procore SSO** tarafı, yönetici olarak oturum açma tooyour procore şirket site.</span><span class="sxs-lookup"><span data-stu-id="984c7-164">tooconfigure single sign-on on **Procore SSO** side, login tooyour procore company site as an administrator.</span></span>

8. <span data-ttu-id="984c7-165">Merhaba araç kutusu açılır, aşağı, tıklayın **yönetici** tooopen hello SSO Ayarları sayfası.</span><span class="sxs-lookup"><span data-stu-id="984c7-165">From hello toolbox drop down, click on **Admin** tooopen hello SSO settings page.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-procoresso-tutorial/procore_tool_admin.png)

9. <span data-ttu-id="984c7-167">Merhaba kutuları olarak Yapıştır hello değerleri aşağıdaki - açıklanan</span><span class="sxs-lookup"><span data-stu-id="984c7-167">Paste hello values in hello boxes as described below-</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-procoresso-tutorial/procore_setting_admin.png)    

    <span data-ttu-id="984c7-169">a.</span><span class="sxs-lookup"><span data-stu-id="984c7-169">a.</span></span> <span data-ttu-id="984c7-170">Merhaba, **tek oturum üzerinde veren URL'si** kutusunda, SAML varlık kimliği kopyalanan hello Azure portal ' hello yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="984c7-170">In hello **Single Sign On Issuer URL** box, paste hello SAML Entity ID copied from hello Azure portal.</span></span>

    <span data-ttu-id="984c7-171">b.</span><span class="sxs-lookup"><span data-stu-id="984c7-171">b.</span></span> <span data-ttu-id="984c7-172">Merhaba, **hedef URL üzerinde SAML oturum** kutusunda, SAML çoklu oturum açma hizmet URL'si kopyalanan hello Azure portal ' hello yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="984c7-172">In hello **SAML Sign On Target URL** box, paste hello SAML Single Sign-On Service URL copied from hello Azure portal.</span></span>

    <span data-ttu-id="984c7-173">c.</span><span class="sxs-lookup"><span data-stu-id="984c7-173">c.</span></span> <span data-ttu-id="984c7-174">Şimdi hello açmak **meta veri XML** hello Azure portal ve kopyalama hello sertifikası adlı hello etiketinde yukarıda indirilen **X509Certificate**.</span><span class="sxs-lookup"><span data-stu-id="984c7-174">Now open hello **Metadata XML** downloaded above from hello Azure portal and copy hello certficate in hello tag named **X509Certificate**.</span></span> <span data-ttu-id="984c7-175">Yapıştır hello kopyaladığınız değeri hello **çoklu oturum açma x509 sertifika** kutusu.</span><span class="sxs-lookup"><span data-stu-id="984c7-175">Paste hello copied value into hello **Single Sign On x509 Certificate** box.</span></span>

10. <span data-ttu-id="984c7-176">Tıklayın **değişiklikleri kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="984c7-176">Click on **Save Changes**.</span></span>

11. <span data-ttu-id="984c7-177">Bu ayarları sonra toosend hello ihtiyaç duyduğu **etki alanı adı** (örneğin **contoso.com**) hangi Procore toohello günlüğü aracılığıyla [Procore destek ekibi](https://support.procore.com/) ve bunlar Bu etki alanı için Federasyon SSO etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="984c7-177">After these settings, you needs toosend hello **domain name** (e.g **contoso.com**) through which you are logging into Procore toohello [Procore Support team](https://support.procore.com/) and they will activate federated SSO for that domain.</span></span>

<!--### Next steps

tooensure users can sign-in tooProcore SSO after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Procore SSO prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooProcore SSO in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Procore SSO users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="984c7-178">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="984c7-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="984c7-179">Bu bölümde Hello amacı toocreate Britta Simon adlı hello Azure Yönetim Portalı'nda bir sınama kullanıcısı ' dir.</span><span class="sxs-lookup"><span data-stu-id="984c7-179">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="984c7-181">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="984c7-181">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="984c7-182">Merhaba, **Azure Yönetim Portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="984c7-182">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-procoresso-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="984c7-184">Çok Git**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar** toodisplay hello kullanıcılar listesi.</span><span class="sxs-lookup"><span data-stu-id="984c7-184">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-procoresso-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="984c7-186">Merhaba hello iletişim üstündeki **Ekle** tooopen hello **kullanıcı** iletişim.</span><span class="sxs-lookup"><span data-stu-id="984c7-186">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-procoresso-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="984c7-188">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="984c7-188">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-procoresso-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="984c7-190">a.</span><span class="sxs-lookup"><span data-stu-id="984c7-190">a.</span></span> <span data-ttu-id="984c7-191">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="984c7-191">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="984c7-192">b.</span><span class="sxs-lookup"><span data-stu-id="984c7-192">b.</span></span> <span data-ttu-id="984c7-193">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="984c7-193">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="984c7-194">c.</span><span class="sxs-lookup"><span data-stu-id="984c7-194">c.</span></span> <span data-ttu-id="984c7-195">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="984c7-195">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="984c7-196">d.</span><span class="sxs-lookup"><span data-stu-id="984c7-196">d.</span></span> <span data-ttu-id="984c7-197">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="984c7-197">Click **Create**.</span></span>
 
### <a name="creating-a-procore-sso-test-user"></a><span data-ttu-id="984c7-198">Procore SSO test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="984c7-198">Creating a Procore SSO test user</span></span>

<span data-ttu-id="984c7-199">Lütfen başlangıç adımları toocreate Procore test kullanıcısı aşağıda kendi tarafında izleyin.</span><span class="sxs-lookup"><span data-stu-id="984c7-199">Please follow hello below steps toocreate a Procore test user on their side.</span></span>

1. <span data-ttu-id="984c7-200">Yönetici olarak oturum açma tooyour procore şirket sitesi.</span><span class="sxs-lookup"><span data-stu-id="984c7-200">Login tooyour procore company site as an administrator.</span></span>  

2. <span data-ttu-id="984c7-201">Merhaba araç kutusu açılır, aşağı, tıklayın **Directory** tooopen hello şirket dizin sayfası.</span><span class="sxs-lookup"><span data-stu-id="984c7-201">From hello toolbox drop down, click on **Directory** tooopen hello company directory page.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-procoresso-tutorial/Procore_sso_directory.png)

3. <span data-ttu-id="984c7-203">Tıklayın **bir kişi Ekle** seçeneği tooopen hello form ve girin seçenekler - gerçekleştirin</span><span class="sxs-lookup"><span data-stu-id="984c7-203">Click on **Add a Person** option tooopen hello form and enter perform following options -</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-procoresso-tutorial/Procore_user_add.png)

    <span data-ttu-id="984c7-205">a.</span><span class="sxs-lookup"><span data-stu-id="984c7-205">a.</span></span> <span data-ttu-id="984c7-206">Merhaba, **ad** metin kutusuna, türü kullanıcının ilk adını gibi **Britta**.</span><span class="sxs-lookup"><span data-stu-id="984c7-206">In hello **First Name** textbox, type user's first name like **Britta**.</span></span>

    <span data-ttu-id="984c7-207">b.</span><span class="sxs-lookup"><span data-stu-id="984c7-207">b.</span></span> <span data-ttu-id="984c7-208">Merhaba, **Soyadı** metin kutusuna, türü kullanıcının soyadını gibi **Simon**.</span><span class="sxs-lookup"><span data-stu-id="984c7-208">In hello **Last name** textbox, type user's last name like **Simon**.</span></span>

    <span data-ttu-id="984c7-209">c.</span><span class="sxs-lookup"><span data-stu-id="984c7-209">c.</span></span> <span data-ttu-id="984c7-210">Merhaba, **e-posta adresi** türü kullanıcının e-posta adresi metin kutusuna, ister  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="984c7-210">In hello **Email Address** textbox, type user's email address like **BrittaSimon@contoso.com**.</span></span>

    <span data-ttu-id="984c7-211">d.</span><span class="sxs-lookup"><span data-stu-id="984c7-211">d.</span></span> <span data-ttu-id="984c7-212">Seçin **izin şablonu** olarak **izin şablonu daha sonra uygulamak**.</span><span class="sxs-lookup"><span data-stu-id="984c7-212">Select **Permission Template** as **Apply Permission Template Later**.</span></span>

    <span data-ttu-id="984c7-213">e.</span><span class="sxs-lookup"><span data-stu-id="984c7-213">e.</span></span> <span data-ttu-id="984c7-214">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="984c7-214">Click **Create**.</span></span>

4. <span data-ttu-id="984c7-215">Denetleyin ve hello kişi yeni eklenen için güncelleştirme hello ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="984c7-215">Check and update hello details for hello newly added contact.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-procoresso-tutorial/Procore_user_check.png)

5. <span data-ttu-id="984c7-217">Tıklayın **Kaydet ve Gönder daveti** (posta yoluyla bir davet gerekliyse) veya **kaydetmek** (doğrudan Kaydet) toocomplete hello kullanıcı kaydı.</span><span class="sxs-lookup"><span data-stu-id="984c7-217">Click on **Save and Send Invitiation** (if an invite through mail is required) or **Save** (Save directly) toocomplete hello user registration.</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-procoresso-tutorial/Procore_user_save.png)    

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="984c7-219">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="984c7-219">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="984c7-220">Bu bölümde, kendi erişim tooProcore SSO vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="984c7-220">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooProcore SSO.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="984c7-222">**tooassign Britta Simon tooProcore SSO hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="984c7-222">**tooassign Britta Simon tooProcore SSO, perform hello following steps:**</span></span>

1. <span data-ttu-id="984c7-223">Hello uygulamaları görünümü, Hello Azure Yönetim Portalı'nda açın ve ardından toohello dizin görünümüne gidin ve çok gidin**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="984c7-223">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="984c7-225">Merhaba uygulamalar listesinde **Procore SSO**.</span><span class="sxs-lookup"><span data-stu-id="984c7-225">In hello applications list, select **Procore SSO**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_app.png) 

3. <span data-ttu-id="984c7-227">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="984c7-227">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="984c7-229">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="984c7-229">Click **Add** button.</span></span> <span data-ttu-id="984c7-230">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="984c7-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="984c7-232">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="984c7-232">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="984c7-233">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="984c7-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="984c7-234">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="984c7-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="984c7-235">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="984c7-235">Testing single sign-on</span></span>

<span data-ttu-id="984c7-236">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="984c7-236">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="984c7-237">Çoklu oturum açma ayarlarınızı test etmek isterseniz, erişim paneli açın.</span><span class="sxs-lookup"><span data-stu-id="984c7-237">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="984c7-238">Erişim paneli hakkında daha fazla ayrıntı için bkz: [erişim Paneli'ne giriş](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="984c7-238">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> <span data-ttu-id="984c7-239">Merhaba Procore SSO hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Procore SSO uygulaması almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="984c7-239">When you click hello Procore SSO tile in hello Access Panel, you should get automatically signed-on tooyour Procore SSO application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="984c7-240">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="984c7-240">Additional resources</span></span>

* [<span data-ttu-id="984c7-241">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="984c7-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="984c7-242">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="984c7-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



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

