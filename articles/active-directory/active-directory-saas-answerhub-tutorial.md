---
title: "Öğretici: Azure Active Directory Tümleştirme ile AnswerHub | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile AnswerHub arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 818b91d7-01df-4b36-9706-f167c710a73c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 3a1c9cc5d7a2ebe28e9fb7e0e6ed8e3d393873ae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-answerhub"></a><span data-ttu-id="79eb4-103">Öğretici: Azure Active Directory Tümleştirme AnswerHub ile</span><span class="sxs-lookup"><span data-stu-id="79eb4-103">Tutorial: Azure Active Directory integration with AnswerHub</span></span>

<span data-ttu-id="79eb4-104">Bu öğreticide, Azure Active Directory (Azure AD) ile AnswerHub tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="79eb4-104">In this tutorial, you learn how to integrate AnswerHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="79eb4-105">AnswerHub Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="79eb4-105">Integrating AnswerHub with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="79eb4-106">AnswerHub erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="79eb4-106">You can control in Azure AD who has access to AnswerHub</span></span>
- <span data-ttu-id="79eb4-107">Otomatik olarak için AnswerHub (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="79eb4-107">You can enable your users to automatically get signed-on to AnswerHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="79eb4-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="79eb4-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="79eb4-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="79eb4-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="79eb4-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="79eb4-110">Prerequisites</span></span>

<span data-ttu-id="79eb4-111">Azure AD tümleştirme AnswerHub ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="79eb4-111">To configure Azure AD integration with AnswerHub, you need the following items:</span></span>

- <span data-ttu-id="79eb4-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="79eb4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="79eb4-113">Bir AnswerHub çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="79eb4-113">An AnswerHub single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="79eb4-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="79eb4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="79eb4-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="79eb4-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="79eb4-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="79eb4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="79eb4-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="79eb4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="79eb4-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="79eb4-118">Scenario description</span></span>
<span data-ttu-id="79eb4-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="79eb4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="79eb4-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="79eb4-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="79eb4-121">Galeriden AnswerHub ekleme</span><span class="sxs-lookup"><span data-stu-id="79eb4-121">Adding AnswerHub from the gallery</span></span>
2. <span data-ttu-id="79eb4-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="79eb4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-answerhub-from-the-gallery"></a><span data-ttu-id="79eb4-123">Galeriden AnswerHub ekleme</span><span class="sxs-lookup"><span data-stu-id="79eb4-123">Adding AnswerHub from the gallery</span></span>
<span data-ttu-id="79eb4-124">Azure AD AnswerHub tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden AnswerHub eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="79eb4-124">To configure the integration of AnswerHub into Azure AD, you need to add AnswerHub from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="79eb4-125">**Galeriden AnswerHub eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="79eb4-125">**To add AnswerHub from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="79eb4-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="79eb4-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="79eb4-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="79eb4-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="79eb4-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="79eb4-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="79eb4-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="79eb4-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="79eb4-133">Arama kutusuna **AnswerHub**.</span><span class="sxs-lookup"><span data-stu-id="79eb4-133">In the search box, type **AnswerHub**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_search.png)

5. <span data-ttu-id="79eb4-135">Sonuçlar panelinde seçin **AnswerHub**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="79eb4-135">In the results panel, select **AnswerHub**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="79eb4-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="79eb4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="79eb4-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı AnswerHub sınayın.</span><span class="sxs-lookup"><span data-stu-id="79eb4-138">In this section, you configure and test Azure AD single sign-on with AnswerHub based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="79eb4-139">Tekli çalışmaya oturum için Azure AD AnswerHub karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="79eb4-139">For single sign-on to work, Azure AD needs to know what the counterpart user in AnswerHub is to a user in Azure AD.</span></span> <span data-ttu-id="79eb4-140">Diğer bir deyişle, bir Azure AD kullanıcısının AnswerHub ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="79eb4-140">In other words, a link relationship between an Azure AD user and the related user in AnswerHub needs to be established.</span></span>

<span data-ttu-id="79eb4-141">AnswerHub içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="79eb4-141">In AnswerHub, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="79eb4-142">Yapılandırma ve Azure AD çoklu oturum açma AnswerHub ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="79eb4-142">To configure and test Azure AD single sign-on with AnswerHub, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="79eb4-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="79eb4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="79eb4-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="79eb4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="79eb4-145">**[Bir AnswerHub test kullanıcısı oluşturma](#creating-an-answerhub-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı AnswerHub sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="79eb4-145">**[Creating an AnswerHub test user](#creating-an-answerhub-test-user)** - to have a counterpart of Britta Simon in AnswerHub that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="79eb4-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="79eb4-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="79eb4-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="79eb4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="79eb4-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="79eb4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="79eb4-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma AnswerHub uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="79eb4-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your AnswerHub application.</span></span>

<span data-ttu-id="79eb4-150">**Azure AD çoklu oturum açma ile AnswerHub yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="79eb4-150">**To configure Azure AD single sign-on with AnswerHub, perform the following steps:**</span></span>

1. <span data-ttu-id="79eb4-151">Azure portalında üzerinde **AnswerHub** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="79eb4-151">In the Azure portal, on the **AnswerHub** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="79eb4-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="79eb4-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_samlbase.png)

3. <span data-ttu-id="79eb4-155">Üzerinde **AnswerHub etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="79eb4-155">On the **AnswerHub Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_url.png)

    <span data-ttu-id="79eb4-157">a.</span><span class="sxs-lookup"><span data-stu-id="79eb4-157">a.</span></span> <span data-ttu-id="79eb4-158">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<company>.answerhub.com`</span><span class="sxs-lookup"><span data-stu-id="79eb4-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company>.answerhub.com`</span></span>

    <span data-ttu-id="79eb4-159">b.</span><span class="sxs-lookup"><span data-stu-id="79eb4-159">b.</span></span> <span data-ttu-id="79eb4-160">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<company>.answerhub.com`</span><span class="sxs-lookup"><span data-stu-id="79eb4-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<company>.answerhub.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="79eb4-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="79eb4-161">These values are not real.</span></span> <span data-ttu-id="79eb4-162">Bu değerler gerçek oturum açma URL'si ve tanımlayıcı ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="79eb4-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="79eb4-163">Kişi [AnswerHub istemci destek ekibi](mailto:success@answerhub.com) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="79eb4-163">Contact [AnswerHub Client support team](mailto:success@answerhub.com) to get these values.</span></span> 
 
4. <span data-ttu-id="79eb4-164">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="79eb4-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_certificate.png) 

5. <span data-ttu-id="79eb4-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="79eb4-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-answerhub-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="79eb4-168">Üzerinde **AnswerHub yapılandırma** 'yi tıklatın **yapılandırma AnswerHub** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="79eb4-168">On the **AnswerHub Configuration** section, click **Configure AnswerHub** to open **Configure sign-on** window.</span></span> <span data-ttu-id="79eb4-169">Kopya **Sign-Out URL ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="79eb4-169">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_configure.png) 

7. <span data-ttu-id="79eb4-171">Farklı web tarayıcısı penceresinde AnswerHub şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="79eb4-171">In a different web browser window, log into your AnswerHub company site as an administrator.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="79eb4-172">AnswerHub yapılandırmada yardıma gereksinim duyarsanız başvurun [AnswerHub'in destek ekibi](mailto:success@answerhub.com.).</span><span class="sxs-lookup"><span data-stu-id="79eb4-172">If you need help configuring AnswerHub, contact [AnswerHub's support team](mailto:success@answerhub.com.).</span></span>
   
8. <span data-ttu-id="79eb4-173">Git **Yönetim**.</span><span class="sxs-lookup"><span data-stu-id="79eb4-173">Go to **Administration**.</span></span>

9. <span data-ttu-id="79eb4-174">Tıklatın **kullanıcı ve grup** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="79eb4-174">Click the **User and Group** tab.</span></span>

10. <span data-ttu-id="79eb4-175">Sol taraftaki gezinti bölmesinde de **sosyal ayarları** 'yi tıklatın **SAML Kurulumu**.</span><span class="sxs-lookup"><span data-stu-id="79eb4-175">In the navigation pane on the left side, in the **Social Settings** section, click **SAML Setup**.</span></span>

11. <span data-ttu-id="79eb4-176">Tıklatın **IDP Config** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="79eb4-176">Click **IDP Config** tab.</span></span>

12. <span data-ttu-id="79eb4-177">Üzerinde **IDP Config** sekmesinde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="79eb4-177">On the **IDP Config** tab, perform the following steps:</span></span>

     <span data-ttu-id="79eb4-178">![SAML Kurulumu](./media/active-directory-saas-answerhub-tutorial/ic785172.png "SAML Kurulumu")</span><span class="sxs-lookup"><span data-stu-id="79eb4-178">![SAML Setup](./media/active-directory-saas-answerhub-tutorial/ic785172.png "SAML Setup")</span></span>  
  
     <span data-ttu-id="79eb4-179">a.</span><span class="sxs-lookup"><span data-stu-id="79eb4-179">a.</span></span> <span data-ttu-id="79eb4-180">İçinde **IDP oturum açma URL'si** metin kutusuna, Yapıştır **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="79eb4-180">In **IDP Login URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
  
     <span data-ttu-id="79eb4-181">b.</span><span class="sxs-lookup"><span data-stu-id="79eb4-181">b.</span></span> <span data-ttu-id="79eb4-182">İçinde **IDP oturum kapatma URL'si** metin kutusuna, Yapıştır **Sign-Out URL** Azure portalından kopyaladığınız değeri.</span><span class="sxs-lookup"><span data-stu-id="79eb4-182">In **IDP Logout URL** textbox, paste **Sign-Out URL** value which you have copied from Azure portal.</span></span>
     
     <span data-ttu-id="79eb4-183">c.</span><span class="sxs-lookup"><span data-stu-id="79eb4-183">c.</span></span> <span data-ttu-id="79eb4-184">İçinde **IDP ad tanımlayıcısı biçimi** metin kutusu, kullanıcı tanımlayıcısı olarak seçili Azure Portalı'nda aynı değeri girin **kullanıcı öznitelikleri** bölümü.</span><span class="sxs-lookup"><span data-stu-id="79eb4-184">In **IDP Name Identifier Format** textbox, enter the user Identifier value same as selected in Azure portal in **User Attributes** section.</span></span>
  
     <span data-ttu-id="79eb4-185">d.</span><span class="sxs-lookup"><span data-stu-id="79eb4-185">d.</span></span> <span data-ttu-id="79eb4-186">Tıklatın **anahtarlar ve Sertifikalar**.</span><span class="sxs-lookup"><span data-stu-id="79eb4-186">Click **Keys and Certificates**.</span></span>

13. <span data-ttu-id="79eb4-187">Anahtarlar ve sertifikalar sekmesinde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="79eb4-187">On the Keys and Certificates tab, perform the following steps:</span></span>
    
     <span data-ttu-id="79eb4-188">![Anahtarlar ve Sertifikalar](./media/active-directory-saas-answerhub-tutorial/ic785173.png "anahtarlar ve sertifikalar")</span><span class="sxs-lookup"><span data-stu-id="79eb4-188">![Keys and Certificates](./media/active-directory-saas-answerhub-tutorial/ic785173.png "Keys and Certificates")</span></span>  
 
     <span data-ttu-id="79eb4-189">a.</span><span class="sxs-lookup"><span data-stu-id="79eb4-189">a.</span></span> <span data-ttu-id="79eb4-190">Not Defteri'nde, Azure Portalı'ndan indirilen, base-64 kodlanmış sertifika açmak içeriğini, panoya kopyalayın ve yapıştırın kendisine **IDP ortak anahtarı (x 509 biçimi)** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="79eb4-190">Open your base-64 encoded certificate which you have downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **IDP Public Key (x509 Format)** textbox.</span></span>
  
     <span data-ttu-id="79eb4-191">b.</span><span class="sxs-lookup"><span data-stu-id="79eb4-191">b.</span></span> <span data-ttu-id="79eb4-192">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="79eb4-192">Click **Save**.</span></span>

14. <span data-ttu-id="79eb4-193">Üzerinde **IDP Config** sekmesini tıklatın, **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="79eb4-193">On the **IDP Config** tab, click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="79eb4-194">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="79eb4-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="79eb4-195">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="79eb4-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="79eb4-196">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="79eb4-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="79eb4-197">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="79eb4-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="79eb4-198">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="79eb4-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="79eb4-200">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="79eb4-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="79eb4-201">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="79eb4-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-answerhub-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="79eb4-203">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="79eb4-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-answerhub-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="79eb4-205">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="79eb4-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-answerhub-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="79eb4-207">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="79eb4-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-answerhub-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="79eb4-209">a.</span><span class="sxs-lookup"><span data-stu-id="79eb4-209">a.</span></span> <span data-ttu-id="79eb4-210">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="79eb4-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="79eb4-211">b.</span><span class="sxs-lookup"><span data-stu-id="79eb4-211">b.</span></span> <span data-ttu-id="79eb4-212">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="79eb4-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="79eb4-213">c.</span><span class="sxs-lookup"><span data-stu-id="79eb4-213">c.</span></span> <span data-ttu-id="79eb4-214">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="79eb4-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="79eb4-215">d.</span><span class="sxs-lookup"><span data-stu-id="79eb4-215">d.</span></span> <span data-ttu-id="79eb4-216">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="79eb4-216">Click **Create**.</span></span>
 
### <a name="creating-an-answerhub-test-user"></a><span data-ttu-id="79eb4-217">Bir AnswerHub test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="79eb4-217">Creating an AnswerHub test user</span></span>

<span data-ttu-id="79eb4-218">Azure AD kullanıcıları için AnswerHub oturum açmak etkinleştirmek için bunların AnswerHub sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="79eb4-218">To enable Azure AD users to log in to AnswerHub, they must be provisioned into AnswerHub.</span></span>  
<span data-ttu-id="79eb4-219">AnswerHub söz konusu olduğunda, sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="79eb4-219">In the case of AnswerHub, provisioning is a manual task.</span></span>

<span data-ttu-id="79eb4-220">**Bir kullanıcı hesabı sağlamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="79eb4-220">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="79eb4-221">Oturum, **AnswerHub** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="79eb4-221">Log in to your **AnswerHub** company site as administrator.</span></span>

2. <span data-ttu-id="79eb4-222">Git **Yönetim**.</span><span class="sxs-lookup"><span data-stu-id="79eb4-222">Go to **Administration**.</span></span>

3. <span data-ttu-id="79eb4-223">Tıklatın **kullanıcıları ve grupları** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="79eb4-223">Click the **Users & Groups** tab.</span></span>

4. <span data-ttu-id="79eb4-224">Sol taraftaki gezinti bölmesinde de **kullanıcıları yönetme** 'yi tıklatın **oluşturma veya içeri aktarma kullanıcı**.</span><span class="sxs-lookup"><span data-stu-id="79eb4-224">In the navigation pane on the left side, in the **Manage Users** section, click **Create or import users**.</span></span>
   
   <span data-ttu-id="79eb4-225">![Kullanıcıları ve grupları](./media/active-directory-saas-answerhub-tutorial/ic785175.png "kullanıcıları ve grupları")</span><span class="sxs-lookup"><span data-stu-id="79eb4-225">![Users & Groups](./media/active-directory-saas-answerhub-tutorial/ic785175.png "Users & Groups")</span></span>

5. <span data-ttu-id="79eb4-226">Tür **e-posta adresi**, **kullanıcıadı** ve **parola** ilgili metin kutularına sağlamak ve ardından istediğiniz geçerli bir Azure Active Directory hesap **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="79eb4-226">Type the **Email address**, **Username** and **Password** of a valid Azure Active Directory account you want to provision into the related textboxes, and then click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="79eb4-227">API sağlama AAD kullanıcı hesaplarına AnswerHub tarafından sağlanan veya herhangi diğer AnswerHub kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="79eb4-227">You can use any other AnswerHub user account creation tools or APIs provided by AnswerHub to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="79eb4-228">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="79eb4-228">Assigning the Azure AD test user</span></span>

<span data-ttu-id="79eb4-229">Bu bölümde, Britta AnswerHub için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="79eb4-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to AnswerHub.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="79eb4-231">**AnswerHub için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="79eb4-231">**To assign Britta Simon to AnswerHub, perform the following steps:**</span></span>

1. <span data-ttu-id="79eb4-232">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="79eb4-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="79eb4-234">Uygulamalar listesinde **AnswerHub**.</span><span class="sxs-lookup"><span data-stu-id="79eb4-234">In the applications list, select **AnswerHub**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_app.png) 

3. <span data-ttu-id="79eb4-236">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="79eb4-236">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="79eb4-238">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="79eb4-238">Click **Add** button.</span></span> <span data-ttu-id="79eb4-239">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="79eb4-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="79eb4-241">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="79eb4-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="79eb4-242">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="79eb4-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="79eb4-243">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="79eb4-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="79eb4-244">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="79eb4-244">Testing single sign-on</span></span>

<span data-ttu-id="79eb4-245">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="79eb4-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="79eb4-246">Erişim paneli AnswerHub parçasında tıklattığınızda, otomatik olarak AnswerHub uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="79eb4-246">When you click the AnswerHub tile in the Access Panel, you should get automatically signed-on to your AnswerHub application.</span></span>
<span data-ttu-id="79eb4-247">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="79eb4-247">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="79eb4-248">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="79eb4-248">Additional resources</span></span>

* [<span data-ttu-id="79eb4-249">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="79eb4-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="79eb4-250">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="79eb4-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_203.png

