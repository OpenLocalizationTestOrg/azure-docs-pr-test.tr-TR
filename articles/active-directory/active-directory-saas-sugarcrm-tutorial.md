---
title: "Öğretici: Azure Active Directory Tümleştirme Sugar CRM ile | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Sugar CRM arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3331b9fc-ebc0-4a3a-9f7b-bf20ee35d180
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: c27aef24e859522b8001ecb747906abdca14d87a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sugar-crm"></a><span data-ttu-id="4c69f-103">Öğretici: Sugar CRM Azure Active Directory Tümleştirme</span><span class="sxs-lookup"><span data-stu-id="4c69f-103">Tutorial: Azure Active Directory integration with Sugar CRM</span></span>

<span data-ttu-id="4c69f-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Sugar CRM tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="4c69f-104">In this tutorial, you learn how to integrate Sugar CRM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4c69f-105">Sugar CRM Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="4c69f-105">Integrating Sugar CRM with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4c69f-106">Sugar CRM erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="4c69f-106">You can control in Azure AD who has access to Sugar CRM</span></span>
- <span data-ttu-id="4c69f-107">Azure AD hesaplarına otomatik olarak Sugar CRM'ye (çoklu oturum açma) açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="4c69f-107">You can enable your users to automatically get signed-on to Sugar CRM (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4c69f-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="4c69f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="4c69f-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4c69f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4c69f-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="4c69f-110">Prerequisites</span></span>

<span data-ttu-id="4c69f-111">Azure AD tümleştirme Sugar CRM ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="4c69f-111">To configure Azure AD integration with Sugar CRM, you need the following items:</span></span>

- <span data-ttu-id="4c69f-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="4c69f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4c69f-113">Bir Sugar CRM çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="4c69f-113">A Sugar CRM single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4c69f-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="4c69f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4c69f-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="4c69f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4c69f-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="4c69f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4c69f-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4c69f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4c69f-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="4c69f-118">Scenario description</span></span>
<span data-ttu-id="4c69f-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="4c69f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4c69f-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="4c69f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4c69f-121">Sugar CRM Galeriden ekleme</span><span class="sxs-lookup"><span data-stu-id="4c69f-121">Adding Sugar CRM from the gallery</span></span>
2. <span data-ttu-id="4c69f-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="4c69f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sugar-crm-from-the-gallery"></a><span data-ttu-id="4c69f-123">Sugar CRM Galeriden ekleme</span><span class="sxs-lookup"><span data-stu-id="4c69f-123">Adding Sugar CRM from the gallery</span></span>
<span data-ttu-id="4c69f-124">Azure AD Sugar CRM tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Sugar CRM eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4c69f-124">To configure the integration of Sugar CRM into Azure AD, you need to add Sugar CRM from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4c69f-125">**Sugar CRM Galeriden eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="4c69f-125">**To add Sugar CRM from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4c69f-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="4c69f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4c69f-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="4c69f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4c69f-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="4c69f-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="4c69f-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4c69f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="4c69f-133">Arama kutusuna **Sugar CRM**.</span><span class="sxs-lookup"><span data-stu-id="4c69f-133">In the search box, type **Sugar CRM**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_search.png)

5. <span data-ttu-id="4c69f-135">Sonuçlar panelinde seçin **Sugar CRM**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4c69f-135">In the results panel, select **Sugar CRM**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4c69f-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="4c69f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4c69f-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma Sugar "Britta Simon" adlı bir test kullanıcı tabanlı CRM ile test etme.</span><span class="sxs-lookup"><span data-stu-id="4c69f-138">In this section, you configure and test Azure AD single sign-on with Sugar CRM based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4c69f-139">Tekli çalışmaya oturum için Azure AD ne karşılık gelen Sugar CRM'deki bir kullanıcı için Azure AD içinde olduğu bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="4c69f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Sugar CRM is to a user in Azure AD.</span></span> <span data-ttu-id="4c69f-140">Diğer bir deyişle, bir Azure AD kullanıcısının Sugar CRM ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="4c69f-140">In other words, a link relationship between an Azure AD user and the related user in Sugar CRM needs to be established.</span></span>

<span data-ttu-id="4c69f-141">Sugar CRM değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="4c69f-141">In Sugar CRM, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="4c69f-142">Yapılandırma ve Azure AD çoklu oturum açma Sugar CRM ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="4c69f-142">To configure and test Azure AD single sign-on with Sugar CRM, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4c69f-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="4c69f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4c69f-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="4c69f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4c69f-145">**[Sugar CRM test kullanıcısı oluşturma](#creating-a-sugar-crm-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Sugar CRM sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="4c69f-145">**[Creating a Sugar CRM test user](#creating-a-sugar-crm-test-user)** - to have a counterpart of Britta Simon in Sugar CRM that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="4c69f-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="4c69f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4c69f-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="4c69f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4c69f-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="4c69f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4c69f-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Sugar CRM uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="4c69f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Sugar CRM application.</span></span>

<span data-ttu-id="4c69f-150">**Azure AD çoklu oturum açma Sugar CRM ile yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="4c69f-150">**To configure Azure AD single sign-on with Sugar CRM, perform the following steps:**</span></span>

1. <span data-ttu-id="4c69f-151">Azure portalında üzerinde **Sugar CRM** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="4c69f-151">In the Azure portal, on the **Sugar CRM** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="4c69f-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="4c69f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_samlbase.png)

3. <span data-ttu-id="4c69f-155">Üzerinde **Sugar CRM etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="4c69f-155">On the **Sugar CRM Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_url.png)

    <span data-ttu-id="4c69f-157">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:</span><span class="sxs-lookup"><span data-stu-id="4c69f-157">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.sugarondemand.com` |
    | `https://<companyname>.trial.sugarcrm` |

    > [!NOTE] 
    > <span data-ttu-id="4c69f-158">Değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="4c69f-158">The value is not real.</span></span> <span data-ttu-id="4c69f-159">Değerin gerçek oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="4c69f-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="4c69f-160">Kişi [Sugar CRM istemci destek ekibi](https://support.sugarcrm.com/) değeri alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="4c69f-160">Contact [Sugar CRM Client support team](https://support.sugarcrm.com/) to get the value.</span></span> 
 
4. <span data-ttu-id="4c69f-161">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="4c69f-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_certificate.png) 

5. <span data-ttu-id="4c69f-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4c69f-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4c69f-165">Üzerinde **Sugar CRM Yapılandırma** 'yi tıklatın **yapılandırma Sugar CRM** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="4c69f-165">On the **Sugar CRM Configuration** section, click **Configure Sugar CRM** to open **Configure sign-on** window.</span></span> <span data-ttu-id="4c69f-166">Kopya **Sign-Out URL ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="4c69f-166">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_configure.png) 

7. <span data-ttu-id="4c69f-168">Farklı web tarayıcısı penceresinde Sugar CRM şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="4c69f-168">In a different web browser window, log in to your Sugar CRM company site as an administrator.</span></span>

8. <span data-ttu-id="4c69f-169">Git **yönetici**.</span><span class="sxs-lookup"><span data-stu-id="4c69f-169">Go to **Admin**.</span></span>
   
    <span data-ttu-id="4c69f-170">![Yönetici](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "yönetici")</span><span class="sxs-lookup"><span data-stu-id="4c69f-170">![Admin](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "Admin")</span></span>

9. <span data-ttu-id="4c69f-171">İçinde **Yönetim** 'yi tıklatın **parola yönetimi**.</span><span class="sxs-lookup"><span data-stu-id="4c69f-171">In the **Administration** section, click **Password Management**.</span></span>
   
    <span data-ttu-id="4c69f-172">![Yönetim](./media/active-directory-saas-sugarcrm-tutorial/ic795889.png "Yönetim")</span><span class="sxs-lookup"><span data-stu-id="4c69f-172">![Administration](./media/active-directory-saas-sugarcrm-tutorial/ic795889.png "Administration")</span></span>

10. <span data-ttu-id="4c69f-173">Seçin **SAML kimlik doğrulamasını etkinleştirme**.</span><span class="sxs-lookup"><span data-stu-id="4c69f-173">Select **Enable SAML Authentication**.</span></span>
   
    <span data-ttu-id="4c69f-174">![Yönetim](./media/active-directory-saas-sugarcrm-tutorial/ic795890.png "Yönetim")</span><span class="sxs-lookup"><span data-stu-id="4c69f-174">![Administration](./media/active-directory-saas-sugarcrm-tutorial/ic795890.png "Administration")</span></span>

11. <span data-ttu-id="4c69f-175">İçinde **SAML kimlik doğrulaması** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="4c69f-175">In the **SAML Authentication** section, perform the following steps:</span></span>
   
    <span data-ttu-id="4c69f-176">![SAML kimlik doğrulaması](./media/active-directory-saas-sugarcrm-tutorial/ic795891.png "SAML kimlik doğrulaması")</span><span class="sxs-lookup"><span data-stu-id="4c69f-176">![SAML Authentication](./media/active-directory-saas-sugarcrm-tutorial/ic795891.png "SAML Authentication")</span></span>  
 
    <span data-ttu-id="4c69f-177">a.</span><span class="sxs-lookup"><span data-stu-id="4c69f-177">a.</span></span> <span data-ttu-id="4c69f-178">İçinde **oturum açma URL'si** metin değerini yapıştırın **SAML çoklu oturum açma hizmet URL'si**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="4c69f-178">In the **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="4c69f-179">b.</span><span class="sxs-lookup"><span data-stu-id="4c69f-179">b.</span></span> <span data-ttu-id="4c69f-180">İçinde **SLO URL** metin değerini yapıştırın **Sign-Out URL**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="4c69f-180">In the **SLO URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="4c69f-181">c.</span><span class="sxs-lookup"><span data-stu-id="4c69f-181">c.</span></span> <span data-ttu-id="4c69f-182">Base-64 kodlanmış sertifikanızı Not Defteri'nde açın, içeriğini, panoya kopyalayın ve sonra tüm sertifika içine yapıştırabilirsiniz **X.509 sertifikası** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="4c69f-182">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste the entire Certificate into **X.509 Certificate** textbox.</span></span>
  
    <span data-ttu-id="4c69f-183">d.</span><span class="sxs-lookup"><span data-stu-id="4c69f-183">d.</span></span> <span data-ttu-id="4c69f-184">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4c69f-184">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="4c69f-185">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="4c69f-185">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="4c69f-186">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="4c69f-186">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4c69f-187">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4c69f-187">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4c69f-188">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="4c69f-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="4c69f-189">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="4c69f-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="4c69f-191">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="4c69f-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4c69f-192">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="4c69f-192">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4c69f-194">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="4c69f-194">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4c69f-196">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="4c69f-196">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4c69f-198">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="4c69f-198">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4c69f-200">a.</span><span class="sxs-lookup"><span data-stu-id="4c69f-200">a.</span></span> <span data-ttu-id="4c69f-201">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4c69f-201">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4c69f-202">b.</span><span class="sxs-lookup"><span data-stu-id="4c69f-202">b.</span></span> <span data-ttu-id="4c69f-203">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="4c69f-203">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4c69f-204">c.</span><span class="sxs-lookup"><span data-stu-id="4c69f-204">c.</span></span> <span data-ttu-id="4c69f-205">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="4c69f-205">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="4c69f-206">d.</span><span class="sxs-lookup"><span data-stu-id="4c69f-206">d.</span></span> <span data-ttu-id="4c69f-207">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4c69f-207">Click **Create**.</span></span>
 
### <a name="creating-a-sugar-crm-test-user"></a><span data-ttu-id="4c69f-208">Sugar CRM test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="4c69f-208">Creating a Sugar CRM test user</span></span>

<span data-ttu-id="4c69f-209">Sugar CRM oturum açmak Azure AD kullanıcıları etkinleştirmek için bunlar Sugar CRM sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="4c69f-209">In order to enable Azure AD users to log in to Sugar CRM, they must be provisioned to Sugar CRM.</span></span>

<span data-ttu-id="4c69f-210">Sugar söz konusu olduğunda, sağlama el ile bir görev olduğundan, CRM.</span><span class="sxs-lookup"><span data-stu-id="4c69f-210">In the case of Sugar CRM, provisioning is a manual task.</span></span>

<span data-ttu-id="4c69f-211">**Bir kullanıcı hesabı sağlamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="4c69f-211">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="4c69f-212">Oturum, **Sugar CRM** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="4c69f-212">Log in to your **Sugar CRM** company site as administrator.</span></span>

2. <span data-ttu-id="4c69f-213">Git **yönetici**.</span><span class="sxs-lookup"><span data-stu-id="4c69f-213">Go to **Admin**.</span></span>
   
    <span data-ttu-id="4c69f-214">![Yönetici](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "yönetici")</span><span class="sxs-lookup"><span data-stu-id="4c69f-214">![Admin](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "Admin")</span></span>

3. <span data-ttu-id="4c69f-215">İçinde **Yönetim** 'yi tıklatın **kullanıcı yönetimi**.</span><span class="sxs-lookup"><span data-stu-id="4c69f-215">In the **Administration** section, click **User Management**.</span></span>
   
    <span data-ttu-id="4c69f-216">![Yönetim](./media/active-directory-saas-sugarcrm-tutorial/ic795893.png "Yönetim")</span><span class="sxs-lookup"><span data-stu-id="4c69f-216">![Administration](./media/active-directory-saas-sugarcrm-tutorial/ic795893.png "Administration")</span></span>

4. <span data-ttu-id="4c69f-217">Git **kullanıcılar \> yeni bir kullanıcı oluşturmak**.</span><span class="sxs-lookup"><span data-stu-id="4c69f-217">Go to **Users \> Create New User**.</span></span>
   
    <span data-ttu-id="4c69f-218">![Yeni kullanıcı oluşturmak](./media/active-directory-saas-sugarcrm-tutorial/ic795894.png "yeni kullanıcı oluşturun")</span><span class="sxs-lookup"><span data-stu-id="4c69f-218">![Create New User](./media/active-directory-saas-sugarcrm-tutorial/ic795894.png "Create New User")</span></span>

5. <span data-ttu-id="4c69f-219">Üzerinde **kullanıcı profili** sekmesinde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="4c69f-219">On the **User Profile** tab, perform the following steps:</span></span>
   
    <span data-ttu-id="4c69f-220">![Yeni kullanıcı](./media/active-directory-saas-sugarcrm-tutorial/ic795895.png "yeni kullanıcı")</span><span class="sxs-lookup"><span data-stu-id="4c69f-220">![New User](./media/active-directory-saas-sugarcrm-tutorial/ic795895.png "New User")</span></span>

    <span data-ttu-id="4c69f-221">a.</span><span class="sxs-lookup"><span data-stu-id="4c69f-221">a.</span></span> <span data-ttu-id="4c69f-222">Tür **kullanıcı adı**, **Soyadı**, ve **e-posta adresi** ilgili metin kutularına halinde geçerli bir Azure Active Directory kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="4c69f-222">Type the **user name**, **last name**, and **email address** of a valid Azure Active Directory user into the related textboxes.</span></span>
  
6. <span data-ttu-id="4c69f-223">Olarak **durum**seçin **etkin**.</span><span class="sxs-lookup"><span data-stu-id="4c69f-223">As **Status**, select **Active**.</span></span>

7. <span data-ttu-id="4c69f-224">Parola sekmesinde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="4c69f-224">On the Password tab, perform the following steps:</span></span>
   
    <span data-ttu-id="4c69f-225">![Yeni kullanıcı](./media/active-directory-saas-sugarcrm-tutorial/ic795896.png "yeni kullanıcı")</span><span class="sxs-lookup"><span data-stu-id="4c69f-225">![New User](./media/active-directory-saas-sugarcrm-tutorial/ic795896.png "New User")</span></span>

    <span data-ttu-id="4c69f-226">a.</span><span class="sxs-lookup"><span data-stu-id="4c69f-226">a.</span></span> <span data-ttu-id="4c69f-227">Parolayı ilgili metin kutusuna yazın.</span><span class="sxs-lookup"><span data-stu-id="4c69f-227">Type the password into the related textbox.</span></span>

    <span data-ttu-id="4c69f-228">b.</span><span class="sxs-lookup"><span data-stu-id="4c69f-228">b.</span></span> <span data-ttu-id="4c69f-229">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4c69f-229">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="4c69f-230">API sağlama AAD kullanıcı hesaplarına Sugar CRM tarafından sağlanan veya herhangi diğer Sugar CRM kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4c69f-230">You can use any other Sugar CRM user account creation tools or APIs provided by Sugar CRM to provision AAD user accounts.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="4c69f-231">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="4c69f-231">Assigning the Azure AD test user</span></span>

<span data-ttu-id="4c69f-232">Bu bölümde, Britta Sugar CRM'ye erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="4c69f-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Sugar CRM.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="4c69f-234">**Sugar CRM Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="4c69f-234">**To assign Britta Simon to Sugar CRM, perform the following steps:**</span></span>

1. <span data-ttu-id="4c69f-235">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="4c69f-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="4c69f-237">Uygulamalar listesinde **Sugar CRM**.</span><span class="sxs-lookup"><span data-stu-id="4c69f-237">In the applications list, select **Sugar CRM**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_app.png) 

3. <span data-ttu-id="4c69f-239">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="4c69f-239">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="4c69f-241">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4c69f-241">Click **Add** button.</span></span> <span data-ttu-id="4c69f-242">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="4c69f-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="4c69f-244">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="4c69f-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="4c69f-245">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="4c69f-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4c69f-246">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="4c69f-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4c69f-247">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="4c69f-247">Testing single sign-on</span></span>

<span data-ttu-id="4c69f-248">Bu bölümün amacı erişim paneli kullanılarak Azure AD çoklu oturum açma yapılandırmanızı test etmektir.</span><span class="sxs-lookup"><span data-stu-id="4c69f-248">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="4c69f-249">Erişim paneli Sugar CRM parçasında tıklattığınızda, otomatik olarak Sugar CRM uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="4c69f-249">When you click the Sugar CRM tile in the Access Panel, you should get automatically signed-on to your Sugar CRM application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4c69f-250">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="4c69f-250">Additional resources</span></span>

* [<span data-ttu-id="4c69f-251">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="4c69f-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4c69f-252">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="4c69f-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_203.png

