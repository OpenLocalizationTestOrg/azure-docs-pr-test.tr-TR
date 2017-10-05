---
title: "Öğretici: Azure Active Directory Tümleştirme SilkRoad yaşam Suite ile | Microsoft Docs"
description: "Çoklu oturum açma SilkRoad yaşam Suite ile Azure Active Directory arasındaki yapılandırmayı öğrenin."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 3cd92319-7964-41eb-8712-444f5c8b4d15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/10/2017
ms.author: jeedes
ms.openlocfilehash: ecf4e31ecea00d003fc47ea4cebb781ca58957f7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-silkroad-life-suite"></a><span data-ttu-id="8bd32-103">Öğretici: Azure Active Directory Tümleştirme SilkRoad yaşam Suite ile</span><span class="sxs-lookup"><span data-stu-id="8bd32-103">Tutorial: Azure Active Directory integration with SilkRoad Life Suite</span></span>
<span data-ttu-id="8bd32-104">Bu öğreticinin amacı SilkRoad yaşam Suite Azure Active Directory (Azure AD) ile tümleştirme Göster sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="8bd32-104">The objective of this tutorial is to show you how to integrate SilkRoad Life Suite with Azure Active Directory (Azure AD).</span></span> 

<span data-ttu-id="8bd32-105">SilkRoad yaşam Suite Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="8bd32-105">Integrating SilkRoad Life Suite with Azure AD provides you with the following benefits:</span></span> 

* <span data-ttu-id="8bd32-106">SilkRoad yaşam Suite erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="8bd32-106">You can control in Azure AD who has access to SilkRoad Life Suite</span></span> 
* <span data-ttu-id="8bd32-107">Otomatik olarak SilkRoad yaşam Suite çoklu oturum açma (SSO) ile Azure AD hesaplarına için açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="8bd32-107">You can enable your users to automatically get signed-on to SilkRoad Life Suite single sign-on (SSO) with their Azure AD accounts</span></span>

<span data-ttu-id="8bd32-108">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8bd32-108">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8bd32-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="8bd32-109">Prerequisites</span></span>
<span data-ttu-id="8bd32-110">Azure AD tümleştirme SilkRoad yaşam paketiyle yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="8bd32-110">To configure Azure AD integration with SilkRoad Life Suite, you need the following items:</span></span>

* <span data-ttu-id="8bd32-111">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="8bd32-111">An Azure AD subscription</span></span>
* <span data-ttu-id="8bd32-112">Abonelik SilkRoad yaşam Suite SSO etkin</span><span class="sxs-lookup"><span data-stu-id="8bd32-112">A SilkRoad Life Suite SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="8bd32-113">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="8bd32-113">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="8bd32-114">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="8bd32-114">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="8bd32-115">Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8bd32-115">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="8bd32-116">Bir Azure AD deneme ortam yoksa, alabileceğiniz bir [bir aylık deneme](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8bd32-116">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="8bd32-117">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="8bd32-117">Scenario Description</span></span>
<span data-ttu-id="8bd32-118">Bu öğreticinin amacı, Azure AD SSO bir test ortamında test etmenizi hale getirmektir.</span><span class="sxs-lookup"><span data-stu-id="8bd32-118">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="8bd32-119">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="8bd32-119">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8bd32-120">Galeriden SilkRoad yaşam paketi ekleme</span><span class="sxs-lookup"><span data-stu-id="8bd32-120">Adding SilkRoad Life Suite from the gallery</span></span> 
2. <span data-ttu-id="8bd32-121">Yapılandırma ve Azure AD SSO test etme</span><span class="sxs-lookup"><span data-stu-id="8bd32-121">Configuring and testing Azure AD SSO</span></span>

## <a name="add-silkroad-life-suite-from-the-gallery"></a><span data-ttu-id="8bd32-122">Galeriden SilkRoad yaşam paketi ekleme</span><span class="sxs-lookup"><span data-stu-id="8bd32-122">Add SilkRoad Life Suite from the gallery</span></span>
<span data-ttu-id="8bd32-123">Azure AD SilkRoad yaşam Suite tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden SilkRoad yaşam paketi eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8bd32-123">To configure the integration of SilkRoad Life Suite into Azure AD, you need to add SilkRoad Life Suite from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8bd32-124">**Galeriden SilkRoad yaşam paketi eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="8bd32-124">**To add SilkRoad Life Suite from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8bd32-125">İçinde **Klasik Azure portalı**, sol gezinti bölmesinde tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8bd32-125">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="8bd32-127">Gelen **Directory** listesinde, directory tümleştirmesini etkinleştirmek istediğiniz dizini seçin.</span><span class="sxs-lookup"><span data-stu-id="8bd32-127">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="8bd32-128">Dizin görünümünde uygulamaları görünümü açmak için **uygulamaları** üst menüde.</span><span class="sxs-lookup"><span data-stu-id="8bd32-128">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Uygulamalar][2]

4. <span data-ttu-id="8bd32-130">Tıklatın **Ekle** sayfanın sonundaki.</span><span class="sxs-lookup"><span data-stu-id="8bd32-130">Click **Add** at the bottom of the page.</span></span>
   
    ![Uygulamalar][3]

5. <span data-ttu-id="8bd32-132">Üzerinde **ne yapmak istiyorsunuz** iletişim kutusunda, tıklatın **Galeriden bir uygulama eklemek**.</span><span class="sxs-lookup"><span data-stu-id="8bd32-132">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Uygulamalar][4]

6. <span data-ttu-id="8bd32-134">Arama kutusuna **SilkRoad yaşam Suite**.</span><span class="sxs-lookup"><span data-stu-id="8bd32-134">In the search box, type **SilkRoad Life Suite**.</span></span>
   
    ![Uygulamalar][5]

7. <span data-ttu-id="8bd32-136">Sonuçlar bölmesinde seçin **SilkRoad yaşam Suite**ve ardından **tam** uygulama eklemek için.</span><span class="sxs-lookup"><span data-stu-id="8bd32-136">In the results pane, select **SilkRoad Life Suite**, and then click **Complete** to add the application.</span></span>
   
    ![Uygulamalar][50]

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="8bd32-138">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="8bd32-138">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="8bd32-139">Bu bölümün amacı, size nasıl yapılandırılacağı ve SilkRoad yaşam "Britta Simon" adlı bir test kullanıcı tabanlı Suite ile Azure AD SSO test göstermektir.</span><span class="sxs-lookup"><span data-stu-id="8bd32-139">The objective of this section is to show you how to configure and test Azure AD SSO with SilkRoad Life Suite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8bd32-140">Çalışmak SSO için Azure AD Azure AD'de bir kullanıcıya karşılık gelen kullanıcı SilkRoad yaşam paketindeki nedir bilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="8bd32-140">For SSO to work, Azure AD needs to know what the counterpart user in SilkRoad Life Suite to an user in Azure AD is.</span></span> <span data-ttu-id="8bd32-141">Diğer bir deyişle, bir Azure AD kullanıcısının SilkRoad yaşam paketindeki ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8bd32-141">In other words, a link relationship between an Azure AD user and the related user in SilkRoad Life Suite needs to be established.</span></span>

<span data-ttu-id="8bd32-142">Bu bağlantı değeri atayarak ilişkisi **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** SilkRoad yaşam paketindeki.</span><span class="sxs-lookup"><span data-stu-id="8bd32-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SilkRoad Life Suite.</span></span>

<span data-ttu-id="8bd32-143">Yapılandırma ve Azure AD çoklu oturum açma SilkRoad yaşam Suite ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="8bd32-143">To configure and test Azure AD single sign-on with SilkRoad Life Suite, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8bd32-144">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="8bd32-144">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8bd32-145">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="8bd32-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8bd32-146">**[SilkRoad yaşam Suite test kullanıcısı oluşturma](#creating-a-silkroad-life-suite-test-user)**  - Britta Simon, karşılık gelen her, Azure AD gösterimine bağlı SilkRoad yaşam Suite sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="8bd32-146">**[Creating a SilkRoad Life Suite test user](#creating-a-silkroad-life-suite-test-user)** - to have a counterpart of Britta Simon in SilkRoad Life Suite that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="8bd32-147">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="8bd32-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8bd32-148">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="8bd32-148">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="8bd32-149">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="8bd32-149">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="8bd32-150">Bu bölümün amacı, Klasik Azure portalında Azure AD SSO'yu etkinleştirmek ve SSO SilkRoad yaşam Suite Uygulamanızı yapılandırmak için ' dir.</span><span class="sxs-lookup"><span data-stu-id="8bd32-150">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure SSO in your SilkRoad Life Suite application.</span></span>

<span data-ttu-id="8bd32-151">**Azure AD çoklu oturum açma SilkRoad yaşam paketiyle yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="8bd32-151">**To configure Azure AD single sign-on with SilkRoad Life Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="8bd32-152">SilkRoad şirket sitenize yönetici olarak oturum.</span><span class="sxs-lookup"><span data-stu-id="8bd32-152">Sign-on to your SilkRoad company site as administrator.</span></span> 

  >[!NOTE] 
  > <span data-ttu-id="8bd32-153">Microsoft Azure AD ile Federasyon yapılandırma SilkRoad yaşam Suite kimlik doğrulaması uygulamaya erişim elde etmek için lütfen SilkRoad desteği veya SilkRoad Hizmetleri temsilcinize başvurun.</span><span class="sxs-lookup"><span data-stu-id="8bd32-153">To obtain access to the SilkRoad Life Suite Authentication application for configuring federation with Microsoft Azure AD, please contact SilkRoad Support or your SilkRoad Services representative.</span></span>
  > 

2. <span data-ttu-id="8bd32-154">Git **hizmet sağlayıcısı**ve ardından **Federasyon ayrıntıları**.</span><span class="sxs-lookup"><span data-stu-id="8bd32-154">Go to **Service Provider**, and then click **Federation Details**.</span></span> 
   
    ![Azure AD çoklu oturum açma][10] 

3. <span data-ttu-id="8bd32-156">Tıklatın **karşıdan Federasyon meta verileri**ve meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="8bd32-156">Click **Download Federation Metadata**, and then save the metadata file on your computer.</span></span>
   
    ![Azure AD çoklu oturum açma][11] 

4. <span data-ttu-id="8bd32-158">Azure Klasik portalında üzerinde **SilkRoad yaşam Suite** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma özelliğini yapılandırın** açmak için **yapılandırma çoklu oturum açma** iletişim.</span><span class="sxs-lookup"><span data-stu-id="8bd32-158">In the Azure classic portal, on the **SilkRoad Life Suite** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın][6] 

5. <span data-ttu-id="8bd32-160">Üzerinde **SilkRoad yaşam paketine oturum açmasını nasıl istiyorsunuz** sayfasında, **Azure AD çoklu oturum açma**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="8bd32-160">On the **How would you like users to sign on to SilkRoad Life Suite** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Azure AD çoklu oturum açma][7] 

6. <span data-ttu-id="8bd32-162">Üzerinde **uygulama ayarlarını yapılandır** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="8bd32-162">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Azure AD çoklu oturum açma][8]   
 1. <span data-ttu-id="8bd32-164">İçinde **oturum üzerinde URL'si** metin kutusuna, türü URL'yi, kullanıcılarınıza oturum açma SilkRoad yaşam Suite sitenize tarafından kullanılan (örn: *https://defcompanytest-test-redcarpet.silkroad-eng.com/Authentication/*).</span><span class="sxs-lookup"><span data-stu-id="8bd32-164">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your SilkRoad Life Suite site (e.g.: *https://defcompanytest-test-redcarpet.silkroad-eng.com/Authentication/*).</span></span>  
 2. <span data-ttu-id="8bd32-165">İndirilen açmak **Silkroad** meta veri dosyası.</span><span class="sxs-lookup"><span data-stu-id="8bd32-165">Open the downloaded **Silkroad** metadata file.</span></span> 
 3. <span data-ttu-id="8bd32-166">Bulun **AssertionConsumerService** etiketi ve ardından kopyalama **konumu** özniteliği.</span><span class="sxs-lookup"><span data-stu-id="8bd32-166">Locate the **AssertionConsumerService** tag, and then copy the **Location** attribute.</span></span>         
   
    ![Azure AD çoklu oturum açma][21] 
 4. <span data-ttu-id="8bd32-168">Değeri içine yapıştırabilirsiniz **yanıt URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="8bd32-168">Paste the value into the **Reply URL** textbox.</span></span>  
 5. <span data-ttu-id="8bd32-169">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8bd32-169">Click **Next**.</span></span>

6. <span data-ttu-id="8bd32-170">Üzerinde **çoklu oturum açma SilkRoad yaşam Suite yapılandırma** sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="8bd32-170">On the **Configure single sign-on at SilkRoad Life Suite** page, perform the following steps:</span></span>
   
    ![Azure AD çoklu oturum açma][9]  
 1. <span data-ttu-id="8bd32-172">İndirme sertifikası'nı tıklatın ve ardından dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="8bd32-172">Click Download certificate, and then save the file on your computer.</span></span>  
 2. <span data-ttu-id="8bd32-173">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8bd32-173">Click **Next**.</span></span>

7. <span data-ttu-id="8bd32-174">İçinde **SilkRoad** uygulama tıklatın **kimlik doğrulaması kaynakları**.</span><span class="sxs-lookup"><span data-stu-id="8bd32-174">In your **SilkRoad** application, click **Authentication Sources**.</span></span>
   
    ![Azure AD çoklu oturum açma][12] 

8. <span data-ttu-id="8bd32-176">Tıklatın **kimlik doğrulaması kaynağı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="8bd32-176">Click **Add Authentication Source**.</span></span> 
   
    ![Azure AD çoklu oturum açma][13] 

9. <span data-ttu-id="8bd32-178">İçinde **kimlik doğrulaması kaynağı Ekle** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="8bd32-178">In the **Add Authentication Source** section, perform the following steps:</span></span> 
   
    ![Azure AD çoklu oturum açma][14]  
 1. <span data-ttu-id="8bd32-180">Altında **seçeneği 2 - meta veri dosyası**, tıklatın **Gözat** indirilen meta veri dosyasını karşıya yüklemek için.</span><span class="sxs-lookup"><span data-stu-id="8bd32-180">Under **Option 2 - Metadata File**, click **Browse** to upload the downloaded metadata file.</span></span>  
 2. <span data-ttu-id="8bd32-181">Tıklatın **kimlik dosya verilerini kullanarak sağlayıcısı oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="8bd32-181">Click **Create Identity Provider using File Data**.</span></span>

10. <span data-ttu-id="8bd32-182">İçinde **kimlik doğrulaması kaynakları** 'yi tıklatın **Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="8bd32-182">In the **Authentication Sources** section, click **Edit**.</span></span> 
    
     ![Azure AD çoklu oturum açma][15] 

11. <span data-ttu-id="8bd32-184">Üzerinde **kimlik doğrulaması kaynağını Düzenle** iletişim kutusunda, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="8bd32-184">On the **Edit Authentication Source** dialog, perform the following steps:</span></span> 
    
     ![Azure AD çoklu oturum açma][16] 
 1. <span data-ttu-id="8bd32-186">Olarak **etkin**seçin **Evet**.</span><span class="sxs-lookup"><span data-stu-id="8bd32-186">As **Enabled**, select **Yes**.</span></span>   
 2. <span data-ttu-id="8bd32-187">İçinde **IDP açıklama** metin kutusuna, yapılandırmanız için bir açıklama yazın (örneğin: *Azure AD SSO*).</span><span class="sxs-lookup"><span data-stu-id="8bd32-187">In the **IdP Description** textbox, type a description for your configuration (e.g.: *Azure AD SSO*).</span></span>  
 3. <span data-ttu-id="8bd32-188">İçinde **IDP adı** metin kutusuna, yapılandırmanızda özgü adını yazın (örneğin: *Azure SP*).</span><span class="sxs-lookup"><span data-stu-id="8bd32-188">In the **IdP Name** textbox, type a name that is specific to your configuration (e.g.: *Azure SP*).</span></span>  
 4. <span data-ttu-id="8bd32-189">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8bd32-189">Click **Save**.</span></span>

12. <span data-ttu-id="8bd32-190">Diğer tüm kimlik doğrulaması kaynakları devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="8bd32-190">Disable all other authentication sources.</span></span> 
    
     ![Azure AD çoklu oturum açma][17]

13. <span data-ttu-id="8bd32-192">Azure Klasik portalında üzerinde **tek oturum açma onay** sayfasında, **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="8bd32-192">In the Azure classic portal, on the **Single sign-on confirmation** page, click **Next**.</span></span>  
    
     ![Azure AD çoklu oturum açma][18]

14. <span data-ttu-id="8bd32-194">Üzerinde **tek oturum açma onay** sayfasında, **tam**.</span><span class="sxs-lookup"><span data-stu-id="8bd32-194">On the **Single sign-on confirmation** page, click **Complete**.</span></span>
    
     ![Azure AD çoklu oturum açma][19]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="8bd32-196">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="8bd32-196">Create an Azure AD test user</span></span>
<span data-ttu-id="8bd32-197">Bu bölümün amacı, Britta Simon adlı Klasik Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="8bd32-197">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][20]

<span data-ttu-id="8bd32-199">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="8bd32-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8bd32-200">İçinde **Klasik Azure portalı**, sol gezinti bölmesinde tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8bd32-200">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_09.png)  

2. <span data-ttu-id="8bd32-202">Gelen **Directory** listesinde, directory tümleştirmesini etkinleştirmek istediğiniz dizini seçin.</span><span class="sxs-lookup"><span data-stu-id="8bd32-202">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="8bd32-203">Üstteki menüde kullanıcıların listesini görüntülemek için tıklatın **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="8bd32-203">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8bd32-205">Açmak için **Kullanıcı Ekle** iletişim kutusunda, araç çubuğunda alt tıklatın **Kullanıcı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="8bd32-205">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span> 
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="8bd32-207">Üzerinde **bu kullanıcı hakkında bize** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="8bd32-207">On the **Tell us about this user** dialog page, perform the following steps:</span></span> 
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_05.png)  
 1. <span data-ttu-id="8bd32-209">Kullanıcı türü olarak, kuruluşunuzdaki yeni kullanıcı seçin.</span><span class="sxs-lookup"><span data-stu-id="8bd32-209">As Type Of User, select New user in your organization.</span></span>  
 2. <span data-ttu-id="8bd32-210">Kullanıcı adı **textbox**, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8bd32-210">In the User Name **textbox**, type **BrittaSimon**.</span></span> 
 3. <span data-ttu-id="8bd32-211">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8bd32-211">Click **Next**.</span></span>

6. <span data-ttu-id="8bd32-212">Üzerinde **kullanıcı profili** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="8bd32-212">On the **User Profile** dialog page, perform the following steps:</span></span> 
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_06.png)  
 1. <span data-ttu-id="8bd32-214">İçinde **ad** metin kutusuna, türü **Britta**.</span><span class="sxs-lookup"><span data-stu-id="8bd32-214">In the **First Name** textbox, type **Britta**.</span></span>    
 2. <span data-ttu-id="8bd32-215">İçinde **Soyadı** metin kutusuna, türü, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="8bd32-215">In the **Last Name** textbox, type, **Simon**.</span></span> 
 3. <span data-ttu-id="8bd32-216">İçinde **görünen adı** metin kutusuna, türü **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="8bd32-216">In the **Display Name** textbox, type **Britta Simon**.</span></span> 
 4. <span data-ttu-id="8bd32-217">İçinde **rol** listesinde **kullanıcı**.</span><span class="sxs-lookup"><span data-stu-id="8bd32-217">In the **Role** list, select **User**.</span></span>
 5. <span data-ttu-id="8bd32-218">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8bd32-218">Click **Next**.</span></span>

7. <span data-ttu-id="8bd32-219">Üzerinde **Get geçici parola** iletişim sayfasında, tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="8bd32-219">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="8bd32-221">Üzerinde **Get geçici parola** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="8bd32-221">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_08.png)  
 1. <span data-ttu-id="8bd32-223">Değerini yazmak **yeni parola**.</span><span class="sxs-lookup"><span data-stu-id="8bd32-223">Write down the value of the **New Password**.</span></span> 
 2. <span data-ttu-id="8bd32-224">**Tamamla**’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8bd32-224">Click **Complete**.</span></span>   

### <a name="create-a-silkroad-life-suite-test-user"></a><span data-ttu-id="8bd32-225">SilkRoad yaşam Suite test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="8bd32-225">Create a SilkRoad Life Suite test user</span></span>
<span data-ttu-id="8bd32-226">Bu bölümün amacı Britta Simon SilkRoad yaşam paketindeki adlı bir kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="8bd32-226">The objective of this section is to create a user called Britta Simon in SilkRoad Life Suite.</span></span> <span data-ttu-id="8bd32-227">Britta'nın bir SSO kimliği olmalıdır (bazen denir bir *AuthParam*) Britta'nın eşleşen **emailaddress** Azure AD'de.</span><span class="sxs-lookup"><span data-stu-id="8bd32-227">Britta's must have an SSO ID (sometimes referred to as an *AuthParam*) that matches Britta's **emailaddress** in Azure AD.</span></span>

<span data-ttu-id="8bd32-228">**Britta Simon SilkRoad yaşam paketindeki adlı bir kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="8bd32-228">**To create a user called Britta Simon in SilkRoad Life Suite, perform the following steps:**</span></span>

- <span data-ttu-id="8bd32-229">Sahip bir kullanıcı oluşturmak için SilkRoad yaşam Suite Destek ekibinize başvurun **SSO kimliği** aynı değere özniteliği **emailaddress** Britta Simon Azure AD'de.</span><span class="sxs-lookup"><span data-stu-id="8bd32-229">Ask your SilkRoad Life Suite support team to create a user that has as **SSO ID** attribute the same value as the **emailaddress** of Britta Simon in Azure AD.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="8bd32-230">Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="8bd32-230">Assign the Azure AD test user</span></span>
<span data-ttu-id="8bd32-231">Bu bölümün amacı Britta SilkRoad yaşam paketine kendi erişim vererek Azure SSO kullanılacak Simon sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="8bd32-231">The objective of this section is to enable Britta Simon to use Azure SSO by granting her access to SilkRoad Life Suite.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="8bd32-233">**Britta Simon SilkRoad yaşam paketine atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="8bd32-233">**To assign Britta Simon to SilkRoad Life Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="8bd32-234">Azure Klasik portalı üzerinde dizin görünümünde uygulamaları görünümü açmak için tıklatın **uygulamaları** üst menüde.</span><span class="sxs-lookup"><span data-stu-id="8bd32-234">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Kullanıcı atama][201] 

2. <span data-ttu-id="8bd32-236">Uygulamalar listesinde **SilkRoad yaşam Suite**.</span><span class="sxs-lookup"><span data-stu-id="8bd32-236">In the applications list, select **SilkRoad Life Suite**.</span></span>
   
    ![Kullanıcı atama][202] 

3. <span data-ttu-id="8bd32-238">Üstteki menüde tıklatın **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="8bd32-238">In the menu on the top, click **Users**.</span></span>
   
    ![Kullanıcı atama][203] 

4. <span data-ttu-id="8bd32-240">Kullanıcılar listesinden seçin **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="8bd32-240">In the Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="8bd32-241">Araç çubuğunda alt tıklatın **atamak**.</span><span class="sxs-lookup"><span data-stu-id="8bd32-241">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Kullanıcı atama][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="8bd32-243">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="8bd32-243">Test single sign-on</span></span>
<span data-ttu-id="8bd32-244">Bu bölümün amacı erişim paneli kullanılarak Azure AD SSO yapılandırmanızı test etmektir.</span><span class="sxs-lookup"><span data-stu-id="8bd32-244">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="8bd32-245">Erişim paneli SilkRoad yaşam Suite parçasında tıklattığınızda, otomatik olarak SilkRoad yaşam Suite uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="8bd32-245">When you click the SilkRoad Life Suite tile in the Access Panel, you should get automatically signed-on to your SilkRoad Life Suite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8bd32-246">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="8bd32-246">Additional Resources</span></span>
* [<span data-ttu-id="8bd32-247">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="8bd32-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8bd32-248">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="8bd32-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_01.png
[50]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_02.png

[6]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_05.png
[7]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_03.png
[8]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_04.png
[9]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_05.png
[10]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_06.png
[11]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_07.png
[12]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_08.png
[13]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_09.png
[14]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_10.png
[15]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_11.png
[16]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_12.png
[17]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_13.png
[18]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_06.png
[19]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_07.png


[20]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_100.png
[21]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_15.png


[200]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_14.png
[203]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_205.png





