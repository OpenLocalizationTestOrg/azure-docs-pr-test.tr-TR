---
title: "Öğretici: Azure Active Directory Tümleştirme ArcGIS Online ile | Microsoft Docs"
description: "Azure Active Directory ArcGIS Online arasında tek oturum açma yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a9e132a4-29e7-48bf-beb9-4148e617c8a9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: df72270ca6443b456c079b22425f1660aa522389
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-arcgis-online"></a><span data-ttu-id="4e049-103">Öğretici: Azure Active Directory Tümleştirme ArcGIS Online ile</span><span class="sxs-lookup"><span data-stu-id="4e049-103">Tutorial: Azure Active Directory integration with ArcGIS Online</span></span>

<span data-ttu-id="4e049-104">Bu öğreticide, Azure Active Directory (Azure AD) ile ArcGIS çevrimiçi tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="4e049-104">In this tutorial, you learn how to integrate ArcGIS Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4e049-105">ArcGIS çevrimiçi Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="4e049-105">Integrating ArcGIS Online with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4e049-106">ArcGIS çevrimiçi erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="4e049-106">You can control in Azure AD who has access to ArcGIS Online</span></span>
- <span data-ttu-id="4e049-107">Azure AD hesaplarına otomatik olarak ArcGIS Online'a (çoklu oturum açma) açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="4e049-107">You can enable your users to automatically get signed-on to ArcGIS Online (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4e049-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="4e049-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="4e049-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4e049-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

To enable single sign-on with ArcGIS Online, it must be configured to use Azure Active Directory as an identity provider. This guide provides information and tips on how to perform this configuration in ArcGIS Online.

>[!Note]: 
>This embedded guide is brand new in the new Azure portal, and we’d love to hear your thoughts. Use the Feedback ? button at the top of the portal to provide feedback. The older guide for using the [Azure classic portal](https://manage.windowsazure.com) to configure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="4e049-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="4e049-110">Prerequisites</span></span>

<span data-ttu-id="4e049-111">Azure AD tümleştirme ArcGIS Online ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="4e049-111">To configure Azure AD integration with ArcGIS Online, you need the following items:</span></span>

- <span data-ttu-id="4e049-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="4e049-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4e049-113">Bir ArcGIS çevrimiçi çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="4e049-113">A ArcGIS Online single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4e049-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="4e049-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4e049-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="4e049-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4e049-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="4e049-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4e049-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4e049-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4e049-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="4e049-118">Scenario description</span></span>
<span data-ttu-id="4e049-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="4e049-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4e049-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="4e049-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4e049-121">ArcGIS çevrimiçi galeriden ekleme</span><span class="sxs-lookup"><span data-stu-id="4e049-121">Adding ArcGIS Online from the gallery</span></span>
2. <span data-ttu-id="4e049-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="4e049-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-arcgis-online-from-the-gallery"></a><span data-ttu-id="4e049-123">ArcGIS çevrimiçi galeriden ekleme</span><span class="sxs-lookup"><span data-stu-id="4e049-123">Adding ArcGIS Online from the gallery</span></span>
<span data-ttu-id="4e049-124">Azure AD ArcGIS Online tümleştirilmesi yapılandırmak için ArcGIS çevrimiçi galeriden yönetilen SaaS uygulamaları listenize eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4e049-124">To configure the integration of ArcGIS Online into Azure AD, you need to add ArcGIS Online from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4e049-125">**ArcGIS çevrimiçi Galeriden eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="4e049-125">**To add ArcGIS Online from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4e049-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="4e049-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4e049-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="4e049-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4e049-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="4e049-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="4e049-131">Tıklatın **yeni uygulama** yeni bir uygulama eklemek için iletişim kutusunun üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4e049-131">Click **New application** button on the top of the dialog to add new application.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="4e049-133">Arama kutusuna **ArcGIS çevrimiçi**.</span><span class="sxs-lookup"><span data-stu-id="4e049-133">In the search box, type **ArcGIS Online**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_search.png)

5. <span data-ttu-id="4e049-135">Sonuçlar panelinde seçin **ArcGIS çevrimiçi**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4e049-135">In the results panel, select **ArcGIS Online**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4e049-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="4e049-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4e049-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma ArcGIS "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Online ile test etme</span><span class="sxs-lookup"><span data-stu-id="4e049-138">In this section, you configure and test Azure AD single sign-on with ArcGIS Online based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4e049-139">Tekli çalışmaya oturum için Azure AD ne karşılık gelen ArcGIS çevrimiçi bir kullanıcı için Azure AD içinde olduğu bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="4e049-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ArcGIS Online is to a user in Azure AD.</span></span> <span data-ttu-id="4e049-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve ilgili kullanıcı ArcGIS çevrimiçi arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="4e049-140">In other words, a link relationship between an Azure AD user and the related user in ArcGIS Online needs to be established.</span></span>

<span data-ttu-id="4e049-141">Bu bağlantı değeri atayarak ilişkisi **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** ArcGIS çevrimiçi.</span><span class="sxs-lookup"><span data-stu-id="4e049-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ArcGIS Online.</span></span>

<span data-ttu-id="4e049-142">Yapılandırma ve Azure AD çoklu oturum açma ArcGIS Online ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="4e049-142">To configure and test Azure AD single sign-on with ArcGIS Online, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4e049-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="4e049-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4e049-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="4e049-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4e049-145">**[ArcGIS çevrimiçi bir test kullanıcısı oluşturma](#creating-an-arcgis-online-test-user)**  - ArcGIS kullanıcı Azure AD gösterimini bağlantılı çevrimiçi Britta Simon, karşılık gelen sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="4e049-145">**[Creating an ArcGIS Online test user](#creating-an-arcgis-online-test-user)** - to have a counterpart of Britta Simon in ArcGIS Online that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="4e049-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="4e049-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4e049-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="4e049-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4e049-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="4e049-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4e049-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma ArcGIS çevrimiçi uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="4e049-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ArcGIS Online application.</span></span>

<span data-ttu-id="4e049-150">**Azure AD çoklu oturum açma ArcGIS Online ile yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="4e049-150">**To configure Azure AD single sign-on with ArcGIS Online, perform the following steps:**</span></span>

1. <span data-ttu-id="4e049-151">Azure portalında üzerinde **ArcGIS çevrimiçi** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="4e049-151">In the Azure portal, on the **ArcGIS Online** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="4e049-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="4e049-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_samlbase.png)

3. <span data-ttu-id="4e049-155">Üzerinde **ArcGIS çevrimiçi etki alanı ve URL'leri** bölümünde, aşağıdaki adımı gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="4e049-155">On the **ArcGIS Online Domain and URLs** section, perform the following step:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_url.png)

    <span data-ttu-id="4e049-157">İçinde **oturum açma URL'si** metin kutusuna, şu biçimi kullanarak değeri yazın:`https://<company>.maps.arcgis.com`</span><span class="sxs-lookup"><span data-stu-id="4e049-157">In the **Sign-on URL** textbox, type the value using the following pattern: `https://<company>.maps.arcgis.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4e049-158">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="4e049-158">This value is not the real.</span></span> <span data-ttu-id="4e049-159">Bu değer gerçek oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="4e049-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="4e049-160">Kişi [ArcGIS çevrimiçi istemci destek ekibi](http://support.esri.com/) bu değeri alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="4e049-160">Contact [ArcGIS Online Client support team](http://support.esri.com/) to get this value.</span></span> 

4. <span data-ttu-id="4e049-161">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve XML dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="4e049-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_certificate.png) 

5. <span data-ttu-id="4e049-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4e049-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-arcgis-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4e049-165">Farklı web tarayıcısı penceresinde ArcGIS şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="4e049-165">In a different web browser window, log into your ArcGIS company site as an administrator.</span></span>

7. <span data-ttu-id="4e049-166">Tıklatın **ayarları düzenleme**.</span><span class="sxs-lookup"><span data-stu-id="4e049-166">Click **EDIT SETTINGS**.</span></span>

    <span data-ttu-id="4e049-167">![Ayarları Düzenle](./media/active-directory-saas-arcgis-tutorial/ic784742.png "ayarlarını Düzenle")</span><span class="sxs-lookup"><span data-stu-id="4e049-167">![Edit Settings](./media/active-directory-saas-arcgis-tutorial/ic784742.png "Edit Settings")</span></span>

8. <span data-ttu-id="4e049-168">Tıklatın **güvenlik**.</span><span class="sxs-lookup"><span data-stu-id="4e049-168">Click **Security**.</span></span>

    <span data-ttu-id="4e049-169">![Güvenlik](./media/active-directory-saas-arcgis-tutorial/ic784743.png "güvenlik")</span><span class="sxs-lookup"><span data-stu-id="4e049-169">![Security](./media/active-directory-saas-arcgis-tutorial/ic784743.png "Security")</span></span>

9. <span data-ttu-id="4e049-170">Altında **Kurumsal oturum açma bilgileri**, tıklatın **AYARLANMIŞ kimlik sağlayıcı**.</span><span class="sxs-lookup"><span data-stu-id="4e049-170">Under **Enterprise Logins**, click **SET IDENTITY PROVIDER**.</span></span>

    <span data-ttu-id="4e049-171">![Kurumsal oturum açma bilgileri](./media/active-directory-saas-arcgis-tutorial/ic784744.png "Kurumsal oturum açmalar")</span><span class="sxs-lookup"><span data-stu-id="4e049-171">![Enterprise Logins](./media/active-directory-saas-arcgis-tutorial/ic784744.png "Enterprise Logins")</span></span>

10. <span data-ttu-id="4e049-172">Üzerinde **ayarlanmış kimlik sağlayıcı** yapılandırma sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="4e049-172">On the **Set Identity Provider** configuration page, perform the following steps:</span></span>
   
    <span data-ttu-id="4e049-173">![Kimlik sağlayıcısı ayarlamak](./media/active-directory-saas-arcgis-tutorial/ic784745.png "ayarlamak kimlik sağlayıcısı")</span><span class="sxs-lookup"><span data-stu-id="4e049-173">![Set Identity Provider](./media/active-directory-saas-arcgis-tutorial/ic784745.png "Set Identity Provider")</span></span>
   
    <span data-ttu-id="4e049-174">a.</span><span class="sxs-lookup"><span data-stu-id="4e049-174">a.</span></span> <span data-ttu-id="4e049-175">İçinde **adı** metin kutusuna, kuruluşunuzun adını yazın.</span><span class="sxs-lookup"><span data-stu-id="4e049-175">In the **Name** textbox, type your organization’s name.</span></span>

    <span data-ttu-id="4e049-176">b.</span><span class="sxs-lookup"><span data-stu-id="4e049-176">b.</span></span> <span data-ttu-id="4e049-177">İçin **Kurumsal kimlik sağlayıcısı meta verileri sağlanan kullanarak**seçin **dosya**.</span><span class="sxs-lookup"><span data-stu-id="4e049-177">For **Metadata for the Enterprise Identity Provider will be supplied using**, select **A File**.</span></span>

    <span data-ttu-id="4e049-178">c.</span><span class="sxs-lookup"><span data-stu-id="4e049-178">c.</span></span> <span data-ttu-id="4e049-179">İndirilen meta veri dosyanızı karşıya yüklemek için tıklayın **dosya**.</span><span class="sxs-lookup"><span data-stu-id="4e049-179">To upload your downloaded metadata file, click **Choose file**.</span></span>

    <span data-ttu-id="4e049-180">d.</span><span class="sxs-lookup"><span data-stu-id="4e049-180">d.</span></span> <span data-ttu-id="4e049-181">Tıklatın **KÜMESİ kimlik SAĞLAYICISI**.</span><span class="sxs-lookup"><span data-stu-id="4e049-181">Click **SET IDENTITY PROVIDER**.</span></span>

> [!TIP]
> <span data-ttu-id="4e049-182">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="4e049-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="4e049-183">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="4e049-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4e049-184">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4e049-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4e049-185">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="4e049-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="4e049-186">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="4e049-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="4e049-188">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="4e049-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4e049-189">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="4e049-189">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-arcgis-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4e049-191">Git **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar** kullanıcıların listesini görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="4e049-191">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-arcgis-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4e049-193">İletişim kutusunun üstündeki **Ekle** açmak için **kullanıcı** iletişim.</span><span class="sxs-lookup"><span data-stu-id="4e049-193">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-arcgis-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4e049-195">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="4e049-195">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-arcgis-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4e049-197">a.</span><span class="sxs-lookup"><span data-stu-id="4e049-197">a.</span></span> <span data-ttu-id="4e049-198">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4e049-198">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4e049-199">b.</span><span class="sxs-lookup"><span data-stu-id="4e049-199">b.</span></span> <span data-ttu-id="4e049-200">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** Britta Simon biri.</span><span class="sxs-lookup"><span data-stu-id="4e049-200">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="4e049-201">c.</span><span class="sxs-lookup"><span data-stu-id="4e049-201">c.</span></span> <span data-ttu-id="4e049-202">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="4e049-202">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="4e049-203">d.</span><span class="sxs-lookup"><span data-stu-id="4e049-203">d.</span></span> <span data-ttu-id="4e049-204">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4e049-204">Click **Create**.</span></span>
 
### <a name="creating-an-arcgis-online-test-user"></a><span data-ttu-id="4e049-205">ArcGIS çevrimiçi bir test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="4e049-205">Creating an ArcGIS Online test user</span></span>

<span data-ttu-id="4e049-206">Azure AD kullanıcıların ArcGIS çevrimiçi oturum etkinleştirmek için bunlar ArcGIS çevrimiçi sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="4e049-206">In order to enable Azure AD users to log into ArcGIS Online, they must be provisioned into ArcGIS Online.</span></span>  
<span data-ttu-id="4e049-207">ArcGIS söz konusu olduğunda, sağlama el ile bir görev çevrimiçidir.</span><span class="sxs-lookup"><span data-stu-id="4e049-207">In the case of ArcGIS Online, provisioning is a manual task.</span></span>

<span data-ttu-id="4e049-208">**Bir kullanıcı hesabı sağlamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="4e049-208">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="4e049-209">Oturum, **ArcGIS** Kiracı.</span><span class="sxs-lookup"><span data-stu-id="4e049-209">Log in to your **ArcGIS** tenant.</span></span>

2. <span data-ttu-id="4e049-210">Tıklatın **üye davet et**.</span><span class="sxs-lookup"><span data-stu-id="4e049-210">Click **INVITE MEMBERS**.</span></span>
   
    <span data-ttu-id="4e049-211">![Üye davet](./media/active-directory-saas-arcgis-tutorial/ic784747.png "üye davet")</span><span class="sxs-lookup"><span data-stu-id="4e049-211">![Invite Members](./media/active-directory-saas-arcgis-tutorial/ic784747.png "Invite Members")</span></span>

3. <span data-ttu-id="4e049-212">Seçin **üye otomatik olarak bir e-posta göndermeden eklemek**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="4e049-212">Select **Add members automatically without sending an email**, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="4e049-213">![Üyeler otomatik olarak Ekle](./media/active-directory-saas-arcgis-tutorial/ic784748.png "üyeleri otomatik olarak Ekle")</span><span class="sxs-lookup"><span data-stu-id="4e049-213">![Add Members Automatically](./media/active-directory-saas-arcgis-tutorial/ic784748.png "Add Members Automatically")</span></span>

4. <span data-ttu-id="4e049-214">Üzerinde **üyeleri** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="4e049-214">On the **Members** dialog page, perform the following steps:</span></span>
   
     <span data-ttu-id="4e049-215">![Ekleme ve gözden](./media/active-directory-saas-arcgis-tutorial/ic784749.png "ekleme ve gözden geçirme")</span><span class="sxs-lookup"><span data-stu-id="4e049-215">![Add and review](./media/active-directory-saas-arcgis-tutorial/ic784749.png "Add and review")</span></span>
    
     <span data-ttu-id="4e049-216">a.</span><span class="sxs-lookup"><span data-stu-id="4e049-216">a.</span></span> <span data-ttu-id="4e049-217">Girin **e-posta**, **ad**, ve **Soyadı** sağlamak istediğiniz geçerli bir AAD hesabının.</span><span class="sxs-lookup"><span data-stu-id="4e049-217">Enter the **Email**, **First Name**, and **Last Name** of a valid AAD account you want to provision.</span></span>
  
     <span data-ttu-id="4e049-218">b.</span><span class="sxs-lookup"><span data-stu-id="4e049-218">b.</span></span> <span data-ttu-id="4e049-219">Tıklatın **ekleme ve gözden geçirme**.</span><span class="sxs-lookup"><span data-stu-id="4e049-219">Click **ADD AND REVIEW**.</span></span>
5. <span data-ttu-id="4e049-220">Girdiğiniz ve ardından verileri gözden **ADD MEMBERS**.</span><span class="sxs-lookup"><span data-stu-id="4e049-220">Review the data you have entered, and then click **ADD MEMBERS**.</span></span>
   
    <span data-ttu-id="4e049-221">![Üye Ekle](./media/active-directory-saas-arcgis-tutorial/ic784750.png "Üye Ekle")</span><span class="sxs-lookup"><span data-stu-id="4e049-221">![Add member](./media/active-directory-saas-arcgis-tutorial/ic784750.png "Add member")</span></span>
        
    > [!NOTE]
    > <span data-ttu-id="4e049-222">Azure Active Directory hesap sahibi bir e-posta alır ve onu etkinleştirilmeden önce kendi hesabı onaylamak için bağlantıyı izleyin.</span><span class="sxs-lookup"><span data-stu-id="4e049-222">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="4e049-223">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="4e049-223">Assigning the Azure AD test user</span></span>

<span data-ttu-id="4e049-224">Bu bölümde, Britta ArcGIS Online'a erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="4e049-224">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ArcGIS Online.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="4e049-226">**Britta Simon ArcGIS Online'a atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="4e049-226">**To assign Britta Simon to ArcGIS Online, perform the following steps:**</span></span>

1. <span data-ttu-id="4e049-227">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="4e049-227">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="4e049-229">Uygulamalar listesinde **ArcGIS çevrimiçi**.</span><span class="sxs-lookup"><span data-stu-id="4e049-229">In the applications list, select **ArcGIS Online**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_app.png) 

3. <span data-ttu-id="4e049-231">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="4e049-231">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="4e049-233">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4e049-233">Click **Add** button.</span></span> <span data-ttu-id="4e049-234">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="4e049-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="4e049-236">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="4e049-236">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="4e049-237">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="4e049-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4e049-238">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="4e049-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4e049-239">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="4e049-239">Testing single sign-on</span></span>

<span data-ttu-id="4e049-240">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="4e049-240">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="4e049-241">Erişim panelinde ArcGIS çevrimiçi kutucuğa tıkladığınızda, otomatik olarak ArcGIS çevrimiçi uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="4e049-241">When you click the ArcGIS Online tile in the Access Panel, you should get automatically signed-on to your ArcGIS Online application.</span></span>
<span data-ttu-id="4e049-242">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4e049-242">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4e049-243">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="4e049-243">Additional resources</span></span>

* [<span data-ttu-id="4e049-244">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="4e049-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4e049-245">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="4e049-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_203.png

