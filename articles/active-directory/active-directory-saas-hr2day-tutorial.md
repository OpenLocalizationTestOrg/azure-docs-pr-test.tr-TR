---
title: "Öğretici: Azure Active Directory Tümleştirme ile Merces tarafından HR2day | Microsoft Docs"
description: "Çoklu oturum açma HR2day Merces tarafından Azure Active Directory arasındaki yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 853d08c9-27b1-48d4-b8e7-3705140eb67f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/24/2017
ms.author: jeedes
ms.openlocfilehash: 77e2fcf9c306259286b15767f3a992510d6d79d8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hr2day-by-merces"></a><span data-ttu-id="c23a3-103">Öğretici: Azure Active Directory Tümleştirme Merces tarafından HR2day ile</span><span class="sxs-lookup"><span data-stu-id="c23a3-103">Tutorial: Azure Active Directory integration with HR2day by Merces</span></span>

<span data-ttu-id="c23a3-104">Bu öğreticide, Azure Active Directory (Azure AD) ile HR2day Merces tarafından tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="c23a3-104">In this tutorial, you learn how to integrate HR2day by Merces with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c23a3-105">HR2day Merces tarafından Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="c23a3-105">Integrating HR2day by Merces with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c23a3-106">HR2day Merces tarafından erişimi, Azure AD'de kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c23a3-106">You can control in Azure AD who has access to HR2day by Merces.</span></span>
- <span data-ttu-id="c23a3-107">Otomatik olarak HR2day için Merces tarafından kendi Azure AD hesaplarıyla oturum, kullanıcılarınızın etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c23a3-107">You can enable your users to automatically get signed in to HR2day by Merces with their Azure AD accounts.</span></span>
- <span data-ttu-id="c23a3-108">Hesaplarınızı bir merkezi konumda--Azure portalında yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="c23a3-108">You can manage your accounts in one central location--the Azure portal.</span></span>

<span data-ttu-id="c23a3-109">Azure AD SaaS uygulama tümleştirmesi hakkında daha fazla bilgi için bkz: [uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c23a3-109">For more information about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c23a3-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="c23a3-110">Prerequisites</span></span>

<span data-ttu-id="c23a3-111">Azure AD tümleştirme Merces tarafından HR2day yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="c23a3-111">To configure Azure AD integration with HR2day by Merces, you need the following items:</span></span>

- <span data-ttu-id="c23a3-112">Bir Azure AD abonelik.</span><span class="sxs-lookup"><span data-stu-id="c23a3-112">An Azure AD subscription.</span></span>
- <span data-ttu-id="c23a3-113">Bir HR2day Merces çoklu oturum açma tarafından abonelik etkin.</span><span class="sxs-lookup"><span data-stu-id="c23a3-113">An HR2day by Merces single sign-on enabled subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="c23a3-114">Bu öğreticide adımları test etmek için bir üretim ortamında kullanmanızı öneririz yok.</span><span class="sxs-lookup"><span data-stu-id="c23a3-114">We don't recommend using a production environment to test the steps in this tutorial.</span></span>

<span data-ttu-id="c23a3-115">Bu öğreticide adımları test etmek için aşağıdaki önerileri uygulayın:</span><span class="sxs-lookup"><span data-stu-id="c23a3-115">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="c23a3-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="c23a3-116">Don't use your production environment unless it's necessary.</span></span>
- <span data-ttu-id="c23a3-117">Alma bir [bir aylık ücretsiz deneme Azure ad](https://azure.microsoft.com/pricing/free-trial/) , zaten yoksa.</span><span class="sxs-lookup"><span data-stu-id="c23a3-117">Get a [one-month free trial of Azure AD](https://azure.microsoft.com/pricing/free-trial/) if you don't already have it.</span></span>  

## <a name="scenario-description"></a><span data-ttu-id="c23a3-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="c23a3-118">Scenario description</span></span>
<span data-ttu-id="c23a3-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="c23a3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c23a3-120">Burada özetlenen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="c23a3-120">The scenario that's outlined here consists of two main building blocks:</span></span>

1. <span data-ttu-id="c23a3-121">Galeriden HR2day Merces tarafından ekleniyor.</span><span class="sxs-lookup"><span data-stu-id="c23a3-121">Adding HR2day by Merces from the gallery.</span></span>
2. <span data-ttu-id="c23a3-122">Yapılandırma ve Azure AD sınama çoklu oturum açmayı.</span><span class="sxs-lookup"><span data-stu-id="c23a3-122">Configuring and testing Azure AD single sign-on.</span></span>

## <a name="add-hr2day-by-merces-from-the-gallery"></a><span data-ttu-id="c23a3-123">Galeriden Merces tarafından HR2day Ekle</span><span class="sxs-lookup"><span data-stu-id="c23a3-123">Add HR2day by Merces from the gallery</span></span>
<span data-ttu-id="c23a3-124">Azure AD tarafından Merces HR2day tümleştirilmesi yapılandırmak için HR2day Merces tarafından Galeriden yönetilen SaaS uygulamaları listenize ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c23a3-124">To configure the integration of HR2day by Merces into Azure AD, add HR2day by Merces from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c23a3-125">**Galeriden Merces tarafından HR2day eklemek için aşağıdaki adımları uygulayın:**</span><span class="sxs-lookup"><span data-stu-id="c23a3-125">**To add HR2day by Merces from the gallery, take the following steps:**</span></span>

1. <span data-ttu-id="c23a3-126">İçinde [Azure portal](https://portal.azure.com), sol gezinti bölmesinde seçin **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="c23a3-126">In the [Azure portal](https://portal.azure.com), on the left navigation pane, select the **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c23a3-128">Git **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="c23a3-128">Go to **Enterprise applications**.</span></span> <span data-ttu-id="c23a3-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="c23a3-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="c23a3-131">Yeni bir uygulama eklemek için seçin **yeni uygulama** iletişim kutusunun üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c23a3-131">To add a new application, select the **New application** button on the top of the dialog box.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="c23a3-133">Arama kutusuna **HR2day Merces tarafından**.</span><span class="sxs-lookup"><span data-stu-id="c23a3-133">In the search box, type **HR2day by Merces**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_search.png)

5. <span data-ttu-id="c23a3-135">Sonuçlar panelinde seçin **Merces tarafından HR2day**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c23a3-135">In the results panel, select **HR2day by Merces**, and then select the **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="c23a3-137">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="c23a3-137">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="c23a3-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Merces tarafından HR2day ile test etme</span><span class="sxs-lookup"><span data-stu-id="c23a3-138">In this section, you configure and test Azure AD single sign-on with HR2day by Merces based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c23a3-139">Tekli çalışmaya oturum için Azure AD için bir kullanıcı Azure AD'de HR2day Merces tarafından karşılık gelen kullanıcı olan bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="c23a3-139">For single sign-on to work, Azure AD needs to know who the counterpart user in HR2day by Merces is to a user in Azure AD.</span></span> <span data-ttu-id="c23a3-140">Diğer bir deyişle, Merces tarafından HR2day içinde bir Azure AD kullanıcısının ve ilgili kullanıcı arasında bir bağlantı oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c23a3-140">In other words, you need to establish a link between an Azure AD user and the related user in HR2day by Merces.</span></span>

<span data-ttu-id="c23a3-141">Merces tarafından HR2day içinde atamak **kullanıcı adı** için Azure AD'de **kullanıcıadı** ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="c23a3-141">In HR2day by Merces, assign the **user name** in Azure AD to  **Username** to establish the relationship.</span></span>

<span data-ttu-id="c23a3-142">Yapılandırma ve Azure AD çoklu oturum açma Merces tarafından HR2day ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="c23a3-142">To configure and test Azure AD single sign-on with HR2day by Merces, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c23a3-143">[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on): Bu özelliği kullanmak etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="c23a3-143">[Configure Azure AD single sign-on](#configuring-azure-ad-single-sign-on): Enable your users to use this feature.</span></span>
2. <span data-ttu-id="c23a3-144">[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user): Test Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="c23a3-144">[Create an Azure AD test user](#creating-an-azure-ad-test-user): Test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c23a3-145">[Merces test kullanıcı tarafından bir HR2day oluşturma](#creating-an-hr2day-by-merces-test-user): Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Merces tarafından HR2day oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c23a3-145">[Create an HR2day by Merces test user](#creating-an-hr2day-by-merces-test-user): Create a counterpart of Britta Simon in HR2day by Merces that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c23a3-146">[Azure AD test kullanıcısı atayın](#assigning-the-azure-ad-test-user): Azure AD çoklu oturum açma kullanmak için Britta Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="c23a3-146">[Assign the Azure AD test user](#assigning-the-azure-ad-test-user): Enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c23a3-147">[Test çoklu oturum açma](#testing-single-sign-on): yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="c23a3-147">[Test single sign-on](#testing-single-sign-on): Verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="c23a3-148">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="c23a3-148">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="c23a3-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma, HR2day Merces uygulama tarafından yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="c23a3-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your HR2day by Merces application.</span></span>

<span data-ttu-id="c23a3-150">**Azure AD çoklu oturum açma Merces tarafından HR2day yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c23a3-150">**To configure Azure AD single sign-on with HR2day by Merces, take the following steps:**</span></span>

1. <span data-ttu-id="c23a3-151">Azure portalında üzerinde **Merces tarafından HR2day** uygulama tümleştirmesi sayfasında, **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="c23a3-151">In the Azure portal, on the **HR2day by Merces** application integration page, select **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="c23a3-153">Çoklu oturum açma, etkinleştirmek için **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="c23a3-153">To enable single sign-on, in the **Single sign-on** dialog box, select **Mode** as **SAML-based Sign-on**.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_samlbase.png)

3. <span data-ttu-id="c23a3-155">İçinde **HR2day Merces etki alanı ve URL'leri** bölümünde, aşağıdaki adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="c23a3-155">In the **HR2day by Merces Domain and URLs** section, take the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_url.png)

    <span data-ttu-id="c23a3-157">a.</span><span class="sxs-lookup"><span data-stu-id="c23a3-157">a.</span></span> <span data-ttu-id="c23a3-158">İçinde **oturum açma URL'si** kutusuna şu biçimi kullanarak bir URL yazın: `https://<tenantname>.force.com/<instancename>`.</span><span class="sxs-lookup"><span data-stu-id="c23a3-158">In the **Sign-on URL** box, type a URL by using the following pattern: `https://<tenantname>.force.com/<instancename>`.</span></span>

    <span data-ttu-id="c23a3-159">b.</span><span class="sxs-lookup"><span data-stu-id="c23a3-159">b.</span></span> <span data-ttu-id="c23a3-160">İçinde **tanımlayıcısı** kutusuna şu biçimi kullanarak bir URL yazın: `https://hr2day.force.com/<companyname>`.</span><span class="sxs-lookup"><span data-stu-id="c23a3-160">In the **Identifier** box, type a URL by using the following pattern: `https://hr2day.force.com/<companyname>`.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c23a3-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="c23a3-161">These values are not real.</span></span> <span data-ttu-id="c23a3-162">Bu değerleri tanımlayıcısı ve gerçek oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="c23a3-162">Update these values with the actual sign-on URL and identifier.</span></span> <span data-ttu-id="c23a3-163">Kişi [HR2day Merces istemci destek ekibi tarafından](mailto:servicedesk@merces.nl) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="c23a3-163">Contact the [HR2day by Merces client support team](mailto:servicedesk@merces.nl) to get these values.</span></span> 
 


4. <span data-ttu-id="c23a3-164">Üzerinde **SAML imzalama sertifikası** bölümünde, select **Certificate(Base64)**ve ardından sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="c23a3-164">On the **SAML Signing Certificate** section, select **Certificate(Base64)**, and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_certificate.png) 

5. <span data-ttu-id="c23a3-166">Bu bölümde, kullanıcıların kendi hesabıyla Merces tarafından HR2day için Azure AD içinde kimlik doğrulaması sağlamak açıklar.</span><span class="sxs-lookup"><span data-stu-id="c23a3-166">This section describes how to enable users to authenticate to HR2day by Merces with their account in Azure AD.</span></span> <span data-ttu-id="c23a3-167">Bunlar SAML protokolünü temel Federasyon kullanarak yapın.</span><span class="sxs-lookup"><span data-stu-id="c23a3-167">They do this by using federation that's based on the SAML protocol.</span></span>

    <span data-ttu-id="c23a3-168">Merces uygulama tarafından HR2day SAML onaylar, SAML belirteci özel öznitelik eşlemelerini eklemenizi gerektirir belirli bir biçimde bekliyor.</span><span class="sxs-lookup"><span data-stu-id="c23a3-168">Your HR2day by Merces application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token.</span></span> <span data-ttu-id="c23a3-169">Aşağıdaki ekran görüntüsü, bunun bir örneğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="c23a3-169">The following screenshot shows an example of this.</span></span> 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2day_00.png)
    
    > [!NOTE] 
    <span data-ttu-id="c23a3-171">SAML onayı yapılandırmadan önce başvurmalıdır [HR2day Merces istemci destek ekibi tarafından](mailto:servicedesk@merces.nl) ve kiracınız için benzersiz tanımlayıcı özniteliği değeri isteyin.</span><span class="sxs-lookup"><span data-stu-id="c23a3-171">Before you can configure the SAML assertion, you must contact the [HR2day by Merces Client support team](mailto:servicedesk@merces.nl) and request the value of the unique identifier attribute for your tenant.</span></span> <span data-ttu-id="c23a3-172">Sonraki bölümde yer alan adımları tamamlamak için bu değeri gerekir.</span><span class="sxs-lookup"><span data-stu-id="c23a3-172">You need this value to complete the steps in the next section.</span></span> 

6. <span data-ttu-id="c23a3-173">İçinde **çoklu oturum açma** iletişim kutusunda **kullanıcı öznitelikleri** bölümünde, aşağıdaki görüntüde gösterildiği gibi SAML belirteci özniteliği yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="c23a3-173">In the **Single sign-on** dialog box, in the **User Attributes** section, configure the SAML token attribute as shown in the following image.</span></span> <span data-ttu-id="c23a3-174">Ardından aşağıdaki adımları uygulayın.</span><span class="sxs-lookup"><span data-stu-id="c23a3-174">Then take the following steps.</span></span>
    
      | <span data-ttu-id="c23a3-175">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="c23a3-175">Attribute name</span></span>    |   <span data-ttu-id="c23a3-176">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="c23a3-176">Attribute value</span></span> |  
    | ------------------- | -------------------- |    
    | <span data-ttu-id="c23a3-177">ATTR_LOGINCLAIM</span><span class="sxs-lookup"><span data-stu-id="c23a3-177">ATTR_LOGINCLAIM</span></span> | <span data-ttu-id="c23a3-178">Birleştirme ([posta] "102938475Z", "@"</span><span class="sxs-lookup"><span data-stu-id="c23a3-178">join([mail],"102938475Z","@"</span></span> |
    
      <span data-ttu-id="c23a3-179">a.</span><span class="sxs-lookup"><span data-stu-id="c23a3-179">a.</span></span> <span data-ttu-id="c23a3-180">Açmak için **özniteliği eklemek** iletişim kutusunda **Ekle özniteliği**.</span><span class="sxs-lookup"><span data-stu-id="c23a3-180">To open the **Add Attribute** dialog, select **Add attribute**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hr2day-tutorial/tutorial_attribute_04.png)

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hr2day-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="c23a3-183">b.</span><span class="sxs-lookup"><span data-stu-id="c23a3-183">b.</span></span> <span data-ttu-id="c23a3-184">İçinde **adı** kutusuna **ATTR_LOGINCLAIM**.</span><span class="sxs-lookup"><span data-stu-id="c23a3-184">In the **Name** box, type **ATTR_LOGINCLAIM**.</span></span>

    <span data-ttu-id="c23a3-185">c.</span><span class="sxs-lookup"><span data-stu-id="c23a3-185">c.</span></span> <span data-ttu-id="c23a3-186">Gelen **değeri** listesinde **Join()**.</span><span class="sxs-lookup"><span data-stu-id="c23a3-186">From the **Value** list, select **Join()**.</span></span>

    <span data-ttu-id="c23a3-187">d.</span><span class="sxs-lookup"><span data-stu-id="c23a3-187">d.</span></span> <span data-ttu-id="c23a3-188">Gelen **Dize1** listesinde **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="c23a3-188">From the **String1** list, select **user.mail**.</span></span>

    <span data-ttu-id="c23a3-189">e.</span><span class="sxs-lookup"><span data-stu-id="c23a3-189">e.</span></span> <span data-ttu-id="c23a3-190">İçin **dize2**, HR2day ekibiniz tarafından sunulan benzersiz bir tanımlayıcı yazın.</span><span class="sxs-lookup"><span data-stu-id="c23a3-190">For **String2**, type the unique identifier that's provided by your HR2day team.</span></span>

    <span data-ttu-id="c23a3-191">f.</span><span class="sxs-lookup"><span data-stu-id="c23a3-191">f.</span></span> <span data-ttu-id="c23a3-192">İçinde **ayırıcı** kutusuna  **@** .</span><span class="sxs-lookup"><span data-stu-id="c23a3-192">In the **Separator** box, type **@**.</span></span>
    
    <span data-ttu-id="c23a3-193">g.</span><span class="sxs-lookup"><span data-stu-id="c23a3-193">g.</span></span> <span data-ttu-id="c23a3-194">Seçin **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="c23a3-194">Select **Ok**.</span></span>

7. <span data-ttu-id="c23a3-195">**Kaydet** düğmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="c23a3-195">Select the **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hr2day-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="c23a3-197">İçinde **Merces yapılandırma tarafından HR2day** bölümünde, select **yapılandırma HR2day Merces tarafından** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="c23a3-197">In the **HR2day by Merces Configuration** section, select **Configure HR2day by Merces** to open the **Configure sign-on** window.</span></span> <span data-ttu-id="c23a3-198">Kopya **Sign-Out URL**, **SAML varlık kimliği**, ve **SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru** bölümü.</span><span class="sxs-lookup"><span data-stu-id="c23a3-198">Copy the **Sign-Out URL**, **SAML Entity ID**, and **SAML Single Sign-On Service URL** from the **Quick Reference** section.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_configure.png) 

9. <span data-ttu-id="c23a3-200">Uygulamanız için SSO yapılandırmak için ilgili kişi [HR2day Merces istemci destek ekibi tarafından](mailTo:servicedesk@merces.nl).</span><span class="sxs-lookup"><span data-stu-id="c23a3-200">To configure SSO  for your application, contact the [HR2day by Merces client support team](mailTo:servicedesk@merces.nl).</span></span> <span data-ttu-id="c23a3-201">İndirilen attach **Certificate(Base64)** e-postanıza dosya.</span><span class="sxs-lookup"><span data-stu-id="c23a3-201">Attach the downloaded **Certificate(Base64)** file to your email.</span></span> <span data-ttu-id="c23a3-202">Ayrıca sağlamak **Sign-Out URL**, **SAML varlık kimliği**, ve **SAML çoklu oturum açma hizmet URL'si** böylece SSO tümleştirmesi için yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="c23a3-202">Also provide the **Sign-Out URL**, **SAML Entity ID**, and **SAML Single Sign-On Service URL** so that they can be configured for SSO integration.</span></span>

    > [!NOTE]
    ><span data-ttu-id="c23a3-203">Bu tümleştirme desenle ayarlanacak varlık kimliği gerektiğini Merces ekibine Bahsediyor **https://hr2day.force.com/INSTANCENAME**.</span><span class="sxs-lookup"><span data-stu-id="c23a3-203">Mention to the Merces team that this integration needs the Entity ID to be set with the pattern **https://hr2day.force.com/INSTANCENAME**.</span></span>

    > [!TIP]
    ><span data-ttu-id="c23a3-204">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="c23a3-204">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c23a3-205">Bu uygulamadan ekledikten sonra **Active Directory** > **kurumsal uygulamalar** bölümünde, select **çoklu oturum açma** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="c23a3-205">After you add this app from the **Active Directory** > **Enterprise Applications** section, select the **Single Sign-On** tab.</span></span> <span data-ttu-id="c23a3-206">Katıştırılmış belgeleri aracılığıyla erişim **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="c23a3-206">Then access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c23a3-207">Daha fazla bilgiyi embedded belgeler özelliği hakkında [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="c23a3-207">You can read more about the embedded documentation feature in the [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="c23a3-208">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c23a3-208">Create an Azure AD test user</span></span>
<span data-ttu-id="c23a3-209">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="c23a3-209">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="c23a3-211">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları uygulayın:**</span><span class="sxs-lookup"><span data-stu-id="c23a3-211">**To create a test user in Azure AD, take the following steps:**</span></span>

1. <span data-ttu-id="c23a3-212">İçinde **Azure portal**, sol gezinti bölmesinde seçin **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="c23a3-212">In the **Azure portal**, on the left navigation pane, select the **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-hr2day-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c23a3-214">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="c23a3-214">To display the list of users, go to **Users and groups**, and then select **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-hr2day-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c23a3-216">Açmak için **kullanıcı** iletişim kutusunda **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="c23a3-216">To open the **User** dialog box, select **Add** on the top of the dialog box.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-hr2day-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c23a3-218">İçinde **kullanıcı** iletişim kutusunda, aşağıdaki adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="c23a3-218">In the **User** dialog box, take the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-hr2day-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c23a3-220">a.</span><span class="sxs-lookup"><span data-stu-id="c23a3-220">a.</span></span> <span data-ttu-id="c23a3-221">İçinde **adı** kutusuna **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c23a3-221">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c23a3-222">b.</span><span class="sxs-lookup"><span data-stu-id="c23a3-222">b.</span></span> <span data-ttu-id="c23a3-223">İçinde **kullanıcı adı** kutusuna **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="c23a3-223">In the **User name** box, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c23a3-224">c.</span><span class="sxs-lookup"><span data-stu-id="c23a3-224">c.</span></span> <span data-ttu-id="c23a3-225">Seçin **Göster parola**ve ardından parolayı not alın.</span><span class="sxs-lookup"><span data-stu-id="c23a3-225">Select **Show Password**, and then write down the password.</span></span>

    <span data-ttu-id="c23a3-226">d.</span><span class="sxs-lookup"><span data-stu-id="c23a3-226">d.</span></span> <span data-ttu-id="c23a3-227">**Oluştur**’u seçin.</span><span class="sxs-lookup"><span data-stu-id="c23a3-227">Select **Create**.</span></span>
 
### <a name="create-an-hr2day-by-merces-test-user"></a><span data-ttu-id="c23a3-228">Bir HR2day tarafından Merces test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c23a3-228">Create an HR2day by Merces test user</span></span>

<span data-ttu-id="c23a3-229">Bu bölümün amacı Britta Simon içinde HR2day tarafından Merces adlı bir kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="c23a3-229">The objective of this section is to create a user called Britta Simon in HR2day by Merces.</span></span> <span data-ttu-id="c23a3-230">HR2day hesap kullanıcılar eklemek için çalışmak [HR2day Merces istemci destek ekibi tarafından](mailto:servicedesk@merces.nl).</span><span class="sxs-lookup"><span data-stu-id="c23a3-230">To add the users in the HR2day account, work with the [HR2day by Merces client support team](mailto:servicedesk@merces.nl).</span></span> 

> [!NOTE]
> <span data-ttu-id="c23a3-231">Bir kullanıcı el ile oluşturmanız gerekiyorsa, kişi [HR2day Merces istemci destek ekibi tarafından](mailto:servicedesk@merces.nl).</span><span class="sxs-lookup"><span data-stu-id="c23a3-231">If you need to create a user manually, contact the [HR2day by Merces client support team](mailto:servicedesk@merces.nl).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="c23a3-232">Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="c23a3-232">Assign the Azure AD test user</span></span>

<span data-ttu-id="c23a3-233">Bu bölümde, Britta Merces tarafından HR2day için kendi erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="c23a3-233">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to HR2day by Merces.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="c23a3-235">**HR2day Merces tarafından Britta Simon atamak için aşağıdaki adımları uygulayın:**</span><span class="sxs-lookup"><span data-stu-id="c23a3-235">**To assign Britta Simon to HR2day by Merces, take the following steps:**</span></span>

1. <span data-ttu-id="c23a3-236">Azure portalında uygulamaları görünümü açmak için dizin görünümüne gidin ve ardından Git **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="c23a3-236">In the Azure portal, open the applications view, go to the directory view, and then go to **Enterprise applications**.</span></span> <span data-ttu-id="c23a3-237">Ardından, **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="c23a3-237">Next, select **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="c23a3-239">Uygulamalar listesinde **HR2day Merces tarafından**.</span><span class="sxs-lookup"><span data-stu-id="c23a3-239">In the applications list, select **HR2day by Merces**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_app.png) 

3. <span data-ttu-id="c23a3-241">Soldaki menüde seçin **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="c23a3-241">In the menu on the left, select **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="c23a3-243">Seçin **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c23a3-243">Select the **Add** button.</span></span> <span data-ttu-id="c23a3-244">Ardından **eklemek atama** iletişim kutusunda **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="c23a3-244">Then, in the **Add Assignment** dialog box, select **Users and groups**.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="c23a3-246">İçinde **kullanıcılar ve gruplar** iletişim kutusunda **kullanıcılar** listesinde **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="c23a3-246">In the **Users and groups** dialog box, in the **Users** list, select **Britta Simon**.</span></span>

6. <span data-ttu-id="c23a3-247">Tıklatın **seçin** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c23a3-247">Click the **Select** button.</span></span>

7. <span data-ttu-id="c23a3-248">İçinde **eklemek atama** iletişim kutusunda **atamak**.</span><span class="sxs-lookup"><span data-stu-id="c23a3-248">In the **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="c23a3-249">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="c23a3-249">Test single sign-on</span></span>

<span data-ttu-id="c23a3-250">Bu bölümün amacı erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="c23a3-250">The objective of this section is to test your Azure AD single sign-on configuration by using the Access Panel.</span></span>  

<span data-ttu-id="c23a3-251">Erişim paneli Merces parçasında tarafından HR2day seçtiğinizde, otomatik olarak, HR2day Merces uygulama tarafından oturum.</span><span class="sxs-lookup"><span data-stu-id="c23a3-251">When you select the HR2day by Merces tile in the Access Panel, you automatically get signed in  to your HR2day by Merces application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c23a3-252">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="c23a3-252">Additional resources</span></span>

* [<span data-ttu-id="c23a3-253">Azure Active Directory ile SaaS uygulamalarını tümleştirme ilgili öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="c23a3-253">List of tutorials about how to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c23a3-254">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="c23a3-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_203.png

