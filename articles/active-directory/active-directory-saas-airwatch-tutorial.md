---
title: "Öğretici: Azure Active Directory Tümleştirme ile AirWatch | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile AirWatch arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 96a3bb1c-96c6-40dc-8ea0-060b0c2a62e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 1996ec97e7c0d94c5606ca43bb5956548f1f3712
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-airwatch"></a><span data-ttu-id="991d7-103">Öğretici: Azure Active Directory Tümleştirme AirWatch ile</span><span class="sxs-lookup"><span data-stu-id="991d7-103">Tutorial: Azure Active Directory integration with AirWatch</span></span>

<span data-ttu-id="991d7-104">Bu öğreticide, Azure Active Directory (Azure AD) ile AirWatch tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="991d7-104">In this tutorial, you learn how to integrate AirWatch with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="991d7-105">AirWatch Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="991d7-105">Integrating AirWatch with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="991d7-106">AirWatch erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="991d7-106">You can control in Azure AD who has access to AirWatch</span></span>
- <span data-ttu-id="991d7-107">Otomatik olarak için AirWatch (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="991d7-107">You can enable your users to automatically get signed-on to AirWatch (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="991d7-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="991d7-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="991d7-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="991d7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="991d7-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="991d7-110">Prerequisites</span></span>

<span data-ttu-id="991d7-111">Azure AD tümleştirme AirWatch ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="991d7-111">To configure Azure AD integration with AirWatch, you need the following items:</span></span>

- <span data-ttu-id="991d7-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="991d7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="991d7-113">Bir AirWatch çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="991d7-113">An AirWatch single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="991d7-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="991d7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="991d7-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="991d7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="991d7-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="991d7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="991d7-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="991d7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="991d7-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="991d7-118">Scenario description</span></span>
<span data-ttu-id="991d7-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="991d7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="991d7-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="991d7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="991d7-121">Galeriden AirWatch ekleme</span><span class="sxs-lookup"><span data-stu-id="991d7-121">Adding AirWatch from the gallery</span></span>
2. <span data-ttu-id="991d7-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="991d7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-airwatch-from-the-gallery"></a><span data-ttu-id="991d7-123">Galeriden AirWatch ekleme</span><span class="sxs-lookup"><span data-stu-id="991d7-123">Adding AirWatch from the gallery</span></span>
<span data-ttu-id="991d7-124">Azure AD AirWatch tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden AirWatch eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="991d7-124">To configure the integration of AirWatch into Azure AD, you need to add AirWatch from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="991d7-125">**Galeriden AirWatch eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="991d7-125">**To add AirWatch from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="991d7-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="991d7-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="991d7-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="991d7-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="991d7-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="991d7-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="991d7-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="991d7-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="991d7-133">Arama kutusuna **AirWatch**.</span><span class="sxs-lookup"><span data-stu-id="991d7-133">In the search box, type **AirWatch**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_search.png)

5. <span data-ttu-id="991d7-135">Sonuçlar panelinde seçin **AirWatch**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="991d7-135">In the results panel, select **AirWatch**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="991d7-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="991d7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="991d7-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı AirWatch ile test etme</span><span class="sxs-lookup"><span data-stu-id="991d7-138">In this section, you configure and test Azure AD single sign-on with AirWatch based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="991d7-139">Tekli çalışmaya oturum için Azure AD AirWatch karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="991d7-139">For single sign-on to work, Azure AD needs to know what the counterpart user in AirWatch is to a user in Azure AD.</span></span> <span data-ttu-id="991d7-140">Diğer bir deyişle, bir Azure AD kullanıcısının AirWatch ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="991d7-140">In other words, a link relationship between an Azure AD user and the related user in AirWatch needs to be established.</span></span>

<span data-ttu-id="991d7-141">Bu bağlantı değeri atayarak ilişkisi **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** AirWatch içinde.</span><span class="sxs-lookup"><span data-stu-id="991d7-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in AirWatch.</span></span>

<span data-ttu-id="991d7-142">Yapılandırma ve Azure AD çoklu oturum açma AirWatch ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="991d7-142">To configure and test Azure AD single sign-on with AirWatch, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="991d7-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="991d7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="991d7-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="991d7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="991d7-145">**[AirWatch test kullanıcısı oluşturma](#creating-a-airwatch-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı AirWatch sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="991d7-145">**[Creating a AirWatch test user](#creating-a-airwatch-test-user)** - to have a counterpart of Britta Simon in AirWatch that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="991d7-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="991d7-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="991d7-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="991d7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="991d7-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="991d7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="991d7-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma AirWatch uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="991d7-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your AirWatch application.</span></span>

<span data-ttu-id="991d7-150">**Azure AD çoklu oturum açma ile AirWatch yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="991d7-150">**To configure Azure AD single sign-on with AirWatch, perform the following steps:**</span></span>

1. <span data-ttu-id="991d7-151">Azure portalında üzerinde **AirWatch** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="991d7-151">In the Azure portal, on the **AirWatch** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="991d7-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="991d7-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_samlbase.png)

3. <span data-ttu-id="991d7-155">Üzerinde **AirWatch etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="991d7-155">On the **AirWatch Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_url.png)

    <span data-ttu-id="991d7-157">a.</span><span class="sxs-lookup"><span data-stu-id="991d7-157">a.</span></span> <span data-ttu-id="991d7-158">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<subdomain>.awmdm.com/AirWatch/Login?gid=companycode`</span><span class="sxs-lookup"><span data-stu-id="991d7-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.awmdm.com/AirWatch/Login?gid=companycode`</span></span>

    <span data-ttu-id="991d7-159">b.</span><span class="sxs-lookup"><span data-stu-id="991d7-159">b.</span></span> <span data-ttu-id="991d7-160">İçinde **tanımlayıcısı** metin değeri olarak yazın`AirWatch`</span><span class="sxs-lookup"><span data-stu-id="991d7-160">In the **Identifier** textbox, type the value as `AirWatch`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="991d7-161">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="991d7-161">This value is not the real.</span></span> <span data-ttu-id="991d7-162">Bu değer gerçek oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="991d7-162">Update this value with the actual Sign-on URL.</span></span> <span data-ttu-id="991d7-163">Kişi [AirWatch istemci destek ekibi](http://www.air-watch.com/company/contact-us/) bu değeri alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="991d7-163">Contact [AirWatch Client support team](http://www.air-watch.com/company/contact-us/) to get this value.</span></span> 
 
4. <span data-ttu-id="991d7-164">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve XML dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="991d7-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_certificate.png) 

5. <span data-ttu-id="991d7-166">Üzerinde **AirWatch yapılandırma** 'yi tıklatın **yapılandırma AirWatch** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="991d7-166">On the **AirWatch Configuration** section, click **Configure AirWatch** to open **Configure sign-on** window.</span></span> <span data-ttu-id="991d7-167">Kopya **SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="991d7-167">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_configure.png) 

6. <span data-ttu-id="991d7-169">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="991d7-169">Click **Save** button.</span></span>

    <span data-ttu-id="991d7-170">![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-airwatch-tutorial/tutorial_general_400.png)
<CS></span><span class="sxs-lookup"><span data-stu-id="991d7-170">![Configure Single Sign-On](./media/active-directory-saas-airwatch-tutorial/tutorial_general_400.png)
<CS></span></span>
7. <span data-ttu-id="991d7-171">Farklı web tarayıcısı penceresinde AirWatch şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="991d7-171">In a different web browser window, log in to your AirWatch company site as an administrator.</span></span>

8. <span data-ttu-id="991d7-172">Sol gezinti bölmesinde **hesapları**ve ardından **Yöneticiler**.</span><span class="sxs-lookup"><span data-stu-id="991d7-172">In the left navigation pane, click **Accounts**, and then click **Administrators**.</span></span>
   
   <span data-ttu-id="991d7-173">![Yöneticiler](./media/active-directory-saas-airwatch-tutorial/ic791920.png "yöneticileri")</span><span class="sxs-lookup"><span data-stu-id="991d7-173">![Administrators](./media/active-directory-saas-airwatch-tutorial/ic791920.png "Administrators")</span></span>

9. <span data-ttu-id="991d7-174">Genişletme **ayarları** menüsüne ve ardından **Dizin Hizmetleri**.</span><span class="sxs-lookup"><span data-stu-id="991d7-174">Expand the **Settings** menu, and then click **Directory Services**.</span></span>
   
   <span data-ttu-id="991d7-175">![Ayarları](./media/active-directory-saas-airwatch-tutorial/ic791921.png "ayarları")</span><span class="sxs-lookup"><span data-stu-id="991d7-175">![Settings](./media/active-directory-saas-airwatch-tutorial/ic791921.png "Settings")</span></span>

10. <span data-ttu-id="991d7-176">Tıklatın **kullanıcı** sekmesinde **temel DN** metin kutusuna, etki alanı adınızı yazın ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="991d7-176">Click the **User** tab, in the **Base DN** textbox, type your domain name, and then click **Save**.</span></span>
   
   <span data-ttu-id="991d7-177">![Kullanıcı](./media/active-directory-saas-airwatch-tutorial/ic791922.png "kullanıcı")</span><span class="sxs-lookup"><span data-stu-id="991d7-177">![User](./media/active-directory-saas-airwatch-tutorial/ic791922.png "User")</span></span>

11. <span data-ttu-id="991d7-178">Tıklatın **Server** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="991d7-178">Click the **Server** tab.</span></span>
   
   <span data-ttu-id="991d7-179">![Sunucu](./media/active-directory-saas-airwatch-tutorial/ic791923.png "sunucu")</span><span class="sxs-lookup"><span data-stu-id="991d7-179">![Server](./media/active-directory-saas-airwatch-tutorial/ic791923.png "Server")</span></span>

12. <span data-ttu-id="991d7-180">Aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="991d7-180">Perform the following steps:</span></span>
    
    <span data-ttu-id="991d7-181">![Karşıya yükleme](./media/active-directory-saas-airwatch-tutorial/ic791924.png "karşıya yükle")</span><span class="sxs-lookup"><span data-stu-id="991d7-181">![Upload](./media/active-directory-saas-airwatch-tutorial/ic791924.png "Upload")</span></span>   
    
    <span data-ttu-id="991d7-182">a.</span><span class="sxs-lookup"><span data-stu-id="991d7-182">a.</span></span> <span data-ttu-id="991d7-183">Olarak **Directory türü**seçin **hiçbiri**.</span><span class="sxs-lookup"><span data-stu-id="991d7-183">As **Directory Type**, select **None**.</span></span>

    <span data-ttu-id="991d7-184">b.</span><span class="sxs-lookup"><span data-stu-id="991d7-184">b.</span></span> <span data-ttu-id="991d7-185">Seçin **SAML kimlik doğrulaması için kullanmak**.</span><span class="sxs-lookup"><span data-stu-id="991d7-185">Select **Use SAML For Authentication**.</span></span>

    <span data-ttu-id="991d7-186">c.</span><span class="sxs-lookup"><span data-stu-id="991d7-186">c.</span></span> <span data-ttu-id="991d7-187">İndirilen sertifika karşıya yüklemek için tıklayın **karşıya**.</span><span class="sxs-lookup"><span data-stu-id="991d7-187">To upload the downloaded certificate, click **Upload**.</span></span>

13. <span data-ttu-id="991d7-188">İçinde **isteği** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="991d7-188">In the **Request** section, perform the following steps:</span></span>
    
    <span data-ttu-id="991d7-189">![İstek](./media/active-directory-saas-airwatch-tutorial/ic791925.png "isteği")</span><span class="sxs-lookup"><span data-stu-id="991d7-189">![Request](./media/active-directory-saas-airwatch-tutorial/ic791925.png "Request")</span></span>  

    <span data-ttu-id="991d7-190">a.</span><span class="sxs-lookup"><span data-stu-id="991d7-190">a.</span></span> <span data-ttu-id="991d7-191">Olarak **bağlama türü isteği**seçin **POST**.</span><span class="sxs-lookup"><span data-stu-id="991d7-191">As **Request Binding Type**, select **POST**.</span></span>

    <span data-ttu-id="991d7-192">b.</span><span class="sxs-lookup"><span data-stu-id="991d7-192">b.</span></span> <span data-ttu-id="991d7-193">Azure portalında üzerinde **çoklu oturum açma sırasında Airwatch yapılandırma** iletişim sayfası, kopya **SAML çoklu oturum açma hizmet URL'si** değer ve ardından yapıştırın **kimlik sağlayıcısı çoklu oturum açma URL** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="991d7-193">In the Azure portal, on the **Configure single sign-on at Airwatch** dialog page, copy the **SAML Single Sign-On Service URL** value, and then paste it into the **Identity Provider Single Sign On URL** textbox.</span></span>

    <span data-ttu-id="991d7-194">c.</span><span class="sxs-lookup"><span data-stu-id="991d7-194">c.</span></span> <span data-ttu-id="991d7-195">Olarak **NameID biçimi**seçin **e-posta adresi**.</span><span class="sxs-lookup"><span data-stu-id="991d7-195">As **NameID Format**, select **Email Address**.</span></span>

    <span data-ttu-id="991d7-196">d.</span><span class="sxs-lookup"><span data-stu-id="991d7-196">d.</span></span> <span data-ttu-id="991d7-197">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="991d7-197">Click **Save**.</span></span>

14. <span data-ttu-id="991d7-198">Tıklatın **kullanıcı** yeniden sekmesinde.</span><span class="sxs-lookup"><span data-stu-id="991d7-198">Click the **User** tab again.</span></span>
    
    <span data-ttu-id="991d7-199">![Kullanıcı](./media/active-directory-saas-airwatch-tutorial/ic791926.png "kullanıcı")</span><span class="sxs-lookup"><span data-stu-id="991d7-199">![User](./media/active-directory-saas-airwatch-tutorial/ic791926.png "User")</span></span>

15. <span data-ttu-id="991d7-200">İçinde **özniteliği** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="991d7-200">In the **Attribute** section, perform the following steps:</span></span>
    
    <span data-ttu-id="991d7-201">![Öznitelik](./media/active-directory-saas-airwatch-tutorial/ic791927.png "özniteliği")</span><span class="sxs-lookup"><span data-stu-id="991d7-201">![Attribute](./media/active-directory-saas-airwatch-tutorial/ic791927.png "Attribute")</span></span>

    <span data-ttu-id="991d7-202">a.</span><span class="sxs-lookup"><span data-stu-id="991d7-202">a.</span></span> <span data-ttu-id="991d7-203">İçinde **nesne tanımlayıcısı** metin kutusuna, türü **http://schemas.microsoft.com/identity/claims/objectidentifier**.</span><span class="sxs-lookup"><span data-stu-id="991d7-203">In the **Object Identifier** textbox, type **http://schemas.microsoft.com/identity/claims/objectidentifier**.</span></span>

    <span data-ttu-id="991d7-204">b.</span><span class="sxs-lookup"><span data-stu-id="991d7-204">b.</span></span> <span data-ttu-id="991d7-205">İçinde **kullanıcıadı** metin kutusuna, türü **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="991d7-205">In the **Username** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>

    <span data-ttu-id="991d7-206">c.</span><span class="sxs-lookup"><span data-stu-id="991d7-206">c.</span></span> <span data-ttu-id="991d7-207">İçinde **görünen adı** metin kutusuna, türü **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span><span class="sxs-lookup"><span data-stu-id="991d7-207">In the **Display Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>

    <span data-ttu-id="991d7-208">d.</span><span class="sxs-lookup"><span data-stu-id="991d7-208">d.</span></span> <span data-ttu-id="991d7-209">İçinde **ad** metin kutusuna, türü **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span><span class="sxs-lookup"><span data-stu-id="991d7-209">In the **First Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>

    <span data-ttu-id="991d7-210">e.</span><span class="sxs-lookup"><span data-stu-id="991d7-210">e.</span></span> <span data-ttu-id="991d7-211">İçinde **Soyadı** metin kutusuna, türü **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span><span class="sxs-lookup"><span data-stu-id="991d7-211">In the **Last Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span></span>

    <span data-ttu-id="991d7-212">f.</span><span class="sxs-lookup"><span data-stu-id="991d7-212">f.</span></span> <span data-ttu-id="991d7-213">İçinde **e-posta** metin kutusuna, türü **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="991d7-213">In the **Email** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>

    <span data-ttu-id="991d7-214">g.</span><span class="sxs-lookup"><span data-stu-id="991d7-214">g.</span></span> <span data-ttu-id="991d7-215">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="991d7-215">Click **Save**.</span></span>

<CE>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="991d7-216">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="991d7-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="991d7-217">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="991d7-217">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="991d7-219">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="991d7-219">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="991d7-220">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="991d7-220">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-airwatch-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="991d7-222">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="991d7-222">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-airwatch-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="991d7-224">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="991d7-224">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-airwatch-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="991d7-226">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="991d7-226">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-airwatch-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="991d7-228">a.</span><span class="sxs-lookup"><span data-stu-id="991d7-228">a.</span></span> <span data-ttu-id="991d7-229">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="991d7-229">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="991d7-230">b.</span><span class="sxs-lookup"><span data-stu-id="991d7-230">b.</span></span> <span data-ttu-id="991d7-231">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** Britta Simon biri.</span><span class="sxs-lookup"><span data-stu-id="991d7-231">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="991d7-232">c.</span><span class="sxs-lookup"><span data-stu-id="991d7-232">c.</span></span> <span data-ttu-id="991d7-233">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="991d7-233">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="991d7-234">d.</span><span class="sxs-lookup"><span data-stu-id="991d7-234">d.</span></span> <span data-ttu-id="991d7-235">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="991d7-235">Click **Create**.</span></span>
 
### <a name="creating-a-airwatch-test-user"></a><span data-ttu-id="991d7-236">AirWatch test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="991d7-236">Creating a AirWatch test user</span></span>

<span data-ttu-id="991d7-237">AirWatch için oturum açmak Azure AD kullanıcıları etkinleştirmek için bunlar içinde AirWatch için hazırlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="991d7-237">To enable Azure AD users to log in to AirWatch, they must be provisioned in to AirWatch.</span></span>

* <span data-ttu-id="991d7-238">AirWatch, sağlama el ile bir görev olduğunda.</span><span class="sxs-lookup"><span data-stu-id="991d7-238">When AirWatch, provisioning is a manual task.</span></span>

<span data-ttu-id="991d7-239">**Bir kullanıcı hesabı sağlamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="991d7-239">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="991d7-240">Oturum, **AirWatch** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="991d7-240">Log in to your **AirWatch** company site as administrator.</span></span>
2. <span data-ttu-id="991d7-241">Sol taraftaki gezinti bölmesinde tıklayın **hesapları**ve ardından **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="991d7-241">In the navigation pane on the left side, click **Accounts**, and then click **Users**.</span></span>
   
   <span data-ttu-id="991d7-242">![Kullanıcıların](./media/active-directory-saas-airwatch-tutorial/ic791929.png "kullanıcılar")</span><span class="sxs-lookup"><span data-stu-id="991d7-242">![Users](./media/active-directory-saas-airwatch-tutorial/ic791929.png "Users")</span></span>
3. <span data-ttu-id="991d7-243">İçinde **kullanıcılar** menüsünde tıklatın **liste görünümü**ve ardından **Ekle \> Kullanıcı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="991d7-243">In the **Users** menu, click **List View**, and then click **Add \> Add User**.</span></span>
   
   <span data-ttu-id="991d7-244">![Kullanıcı ekleme](./media/active-directory-saas-airwatch-tutorial/ic791930.png "kullanıcı ekleme")</span><span class="sxs-lookup"><span data-stu-id="991d7-244">![Add User](./media/active-directory-saas-airwatch-tutorial/ic791930.png "Add User")</span></span>
4. <span data-ttu-id="991d7-245">Üzerinde **Ekle / Düzenle kullanıcı** iletişim kutusunda, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="991d7-245">On the **Add / Edit User** dialog, perform the following steps:</span></span>

   <span data-ttu-id="991d7-246">![Kullanıcı ekleme](./media/active-directory-saas-airwatch-tutorial/ic791931.png "kullanıcı ekleme")</span><span class="sxs-lookup"><span data-stu-id="991d7-246">![Add User](./media/active-directory-saas-airwatch-tutorial/ic791931.png "Add User")</span></span>   
   1. <span data-ttu-id="991d7-247">Tür **kullanıcıadı**, **parola**, **parolayı onaylayın**, **ad**, **Soyadı**,  **E-posta adresi** istediğiniz ilgili metin kutularına sağlamayı geçerli bir Azure Active Directory hesabı.</span><span class="sxs-lookup"><span data-stu-id="991d7-247">Type the **Username**, **Password**, **Confirm Password**, **First Name**, **Last Name**, **Email Address** of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>
   2. <span data-ttu-id="991d7-248">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="991d7-248">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="991d7-249">API sağlama AAD kullanıcı hesaplarına AirWatch tarafından sağlanan veya herhangi diğer AirWatch kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="991d7-249">You can use any other AirWatch user account creation tools or APIs provided by AirWatch to provision AAD user accounts.</span></span>
>  

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="991d7-250">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="991d7-250">Assigning the Azure AD test user</span></span>

<span data-ttu-id="991d7-251">Bu bölümde, Britta AirWatch için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="991d7-251">In this section, you enable Britta Simon to use Azure single sign-on by granting access to AirWatch.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="991d7-253">**AirWatch için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="991d7-253">**To assign Britta Simon to AirWatch, perform the following steps:**</span></span>

1. <span data-ttu-id="991d7-254">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="991d7-254">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="991d7-256">Uygulamalar listesinde **AirWatch**.</span><span class="sxs-lookup"><span data-stu-id="991d7-256">In the applications list, select **AirWatch**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_app.png) 

3. <span data-ttu-id="991d7-258">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="991d7-258">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="991d7-260">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="991d7-260">Click **Add** button.</span></span> <span data-ttu-id="991d7-261">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="991d7-261">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="991d7-263">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="991d7-263">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="991d7-264">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="991d7-264">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="991d7-265">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="991d7-265">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="991d7-266">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="991d7-266">Testing single sign-on</span></span>

<span data-ttu-id="991d7-267">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="991d7-267">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="991d7-268">Çoklu oturum açma ayarlarınızı test etmek isterseniz, erişim paneli açın.</span><span class="sxs-lookup"><span data-stu-id="991d7-268">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="991d7-269">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="991d7-269">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="991d7-270">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="991d7-270">Additional resources</span></span>

* [<span data-ttu-id="991d7-271">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="991d7-271">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="991d7-272">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="991d7-272">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_203.png

