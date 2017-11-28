---
title: "Öğretici: İş için Dropbox Azure Active Directory Tümleştirme | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve iş için Dropbox arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0f3a42e4-6897-4234-af84-b47c148ec3e1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 0fb01eab4f7c6c4516eac64a4343e46ea221f98d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-dropbox-for-business-for-automatic-user-provisioning"></a><span data-ttu-id="fe910-103">Öğretici: Otomatik kullanıcı sağlamak için Dropbox iş için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="fe910-103">Tutorial: Configuring Dropbox for Business for Automatic User Provisioning</span></span>

<span data-ttu-id="fe910-104">Bu öğretici Hello amacı, Dropbox tooperform iş ve Azure AD tooautomatically sağlama ve devre dışı bırakma sağlama kullanıcı hesaplarından Azure AD tooDropbox için iş için gereken adımları hello tooshow ' dir.</span><span class="sxs-lookup"><span data-stu-id="fe910-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Dropbox for Business and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooDropbox for Business.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fe910-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="fe910-105">Prerequisites</span></span>

<span data-ttu-id="fe910-106">Bu öğreticide gösterilen hello senaryo aşağıdaki öğelerindeki hello zaten sahip olduğunuzu varsayar:</span><span class="sxs-lookup"><span data-stu-id="fe910-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="fe910-107">Bir Azure Active directory kiracısı.</span><span class="sxs-lookup"><span data-stu-id="fe910-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="fe910-108">Bir Dropbox iş çoklu oturum açma etkin abonelik için.</span><span class="sxs-lookup"><span data-stu-id="fe910-108">A Dropbox for Business single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="fe910-109">İş için Dropbox takım yönetici izinlerine sahip bir kullanıcı hesabının.</span><span class="sxs-lookup"><span data-stu-id="fe910-109">A user account in Dropbox for Business with Team Admin permissions.</span></span>

## <a name="assigning-users-toodropbox-for-business"></a><span data-ttu-id="fe910-110">İş için kullanıcıların tooDropbox atama</span><span class="sxs-lookup"><span data-stu-id="fe910-110">Assigning users tooDropbox for Business</span></span>

<span data-ttu-id="fe910-111">Azure Active Directory hangi kullanıcıların erişim tooselected uygulamaları alması "atamaları" toodetermine adlı bir kavramı kullanır.</span><span class="sxs-lookup"><span data-stu-id="fe910-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="fe910-112">Otomatik olarak bir kullanıcı hesabı sağlama hello bağlamında, yalnızca hello kullanıcıların ve grupların "Azure AD tooan uygulamada atanmış" eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="fe910-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="fe910-113">Yapılandırma ve hizmet sağlama hello etkinleştirmeden önce hangi kullanıcılara ve/veya Azure AD tooyour Dropbox iş uygulama için erişim hello kullanıcıları temsil gruplarında toodecide gerekir.</span><span class="sxs-lookup"><span data-stu-id="fe910-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Dropbox for Business app.</span></span> <span data-ttu-id="fe910-114">Karar sonra buraya hello yönergeleri izleyerek iş uygulama bu kullanıcıların tooyour Dropbox atayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="fe910-114">Once decided, you can assign these users tooyour Dropbox for Business app by following hello instructions here:</span></span>

[<span data-ttu-id="fe910-115">Bir kullanıcı veya grup tooan kuruluş uygulama atama</span><span class="sxs-lookup"><span data-stu-id="fe910-115">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toodropbox-for-business"></a><span data-ttu-id="fe910-116">İş için kullanıcıların tooDropbox atamak için önemli ipuçları</span><span class="sxs-lookup"><span data-stu-id="fe910-116">Important tips for assigning users tooDropbox for Business</span></span>

*   <span data-ttu-id="fe910-117">Önerilir tek bir Azure AD kullanıcısının yapılandırma sağlama iş tootest hello tooDropbox atanır.</span><span class="sxs-lookup"><span data-stu-id="fe910-117">It is recommended that a single Azure AD user is assigned tooDropbox for Business tootest hello provisioning configuration.</span></span> <span data-ttu-id="fe910-118">Ek kullanıcı ve/veya grupları daha sonra atanabilir.</span><span class="sxs-lookup"><span data-stu-id="fe910-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="fe910-119">İş için bir kullanıcı tooDropbox atarken, geçerli bir kullanıcı rolünün seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="fe910-119">When assigning a user tooDropbox for Business, you must select a valid user role.</span></span> <span data-ttu-id="fe910-120">Merhaba "Varsayılan erişim" rolü sağlama için çalışmaz...</span><span class="sxs-lookup"><span data-stu-id="fe910-120">hello "Default Access" role does not work for provisioning..</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="fe910-121">Otomatik kullanıcı sağlamayı etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="fe910-121">Enable Automated User Provisioning</span></span>

<span data-ttu-id="fe910-122">Bu bölümde, Azure AD tooDropbox API sağlama işletmenin kullanıcı hesabı için bağlanma yoluyla sırasında size kılavuzluk eder ve hizmet toocreate sağlama hello yapılandırma, güncelleştirme ve kullanıcı ve Grup bağlı iş için Dropbox atanan kullanıcı hesaplarında devre dışı bırak Azure AD'de atama.</span><span class="sxs-lookup"><span data-stu-id="fe910-122">This section guides you through connecting your Azure AD tooDropbox for Business's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Dropbox for Business based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="fe910-123">Dropbox sağlanan hello yönergeleri izleyerek, iş için SAML tabanlı çoklu oturum açma tooenabled seçebilirsiniz [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fe910-123">You may also choose tooenabled SAML-based Single Sign-On for Dropbox for Business, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="fe910-124">Bu iki özellik birbirine tamamlayıcı rağmen otomatik sağlamayı bağımsız olarak, çoklu oturum açma yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="fe910-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-automatic-user-account-provisioning"></a><span data-ttu-id="fe910-125">tooconfigure otomatik olarak bir kullanıcı hesabı sağlama:</span><span class="sxs-lookup"><span data-stu-id="fe910-125">tooconfigure automatic user account provisioning:</span></span>

1. <span data-ttu-id="fe910-126">Merhaba, [Azure portal](https://portal.azure.com), toohello Gözat **Azure Active Directory > Kurumsal uygulamaları > tüm uygulamaları** bölümü.</span><span class="sxs-lookup"><span data-stu-id="fe910-126">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="fe910-127">Çoklu oturum açma için zaten Dropbox iş için yapılandırdıysanız, Dropbox hello arama alanı kullanarak iş için örneğiniz arayın.</span><span class="sxs-lookup"><span data-stu-id="fe910-127">If you have already configured Dropbox for Business for single sign-on, search for your instance of Dropbox for Business using hello search field.</span></span> <span data-ttu-id="fe910-128">Aksi takdirde seçin **Ekle** arayın ve **iş için Dropbox** hello uygulama galerisinde.</span><span class="sxs-lookup"><span data-stu-id="fe910-128">Otherwise, select **Add** and search for **Dropbox for Business** in hello application gallery.</span></span> <span data-ttu-id="fe910-129">İş için Dropbox hello Arama sonuçlarından seçin ve uygulamaların tooyour listesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="fe910-129">Select Dropbox for Business from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="fe910-130">İş için Dropbox örneğiniz seçin, sonra seçin hello **sağlama** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="fe910-130">Select your instance of Dropbox for Business, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="fe910-131">Set hello **sağlama modu** çok**otomatik**.</span><span class="sxs-lookup"><span data-stu-id="fe910-131">Set hello **Provisioning Mode** too**Automatic**.</span></span> 

    ![Sağlama](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="fe910-133">Merhaba altında **yönetici kimlik bilgileri** 'yi tıklatın **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="fe910-133">Under hello **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="fe910-134">Bir Dropbox iş oturum açma iletişim için yeni bir tarayıcı penceresinde açar.</span><span class="sxs-lookup"><span data-stu-id="fe910-134">It opens a Dropbox for Business login dialog in a new browser window.</span></span>

6. <span data-ttu-id="fe910-135">Merhaba üzerinde **oturum açma tooDropbox toolink Azure AD ile** iletişim kutusunda, oturum açma tooyour Dropbox iş Kiracı için.</span><span class="sxs-lookup"><span data-stu-id="fe910-135">On hello **Sign-in tooDropbox toolink with Azure AD** dialog, sign in tooyour Dropbox for Business tenant.</span></span>

     <span data-ttu-id="fe910-136">![Kullanıcı sağlamayı](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769518.png "kullanıcı hazırlama")</span><span class="sxs-lookup"><span data-stu-id="fe910-136">![User provisioning](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769518.png "User provisioning")</span></span>

7. <span data-ttu-id="fe910-137">İş Kiracı için toogive Azure Active Directory izni toomake değişiklikleri tooyour Dropbox istediğiniz onaylayın.</span><span class="sxs-lookup"><span data-stu-id="fe910-137">Confirm that you would like toogive Azure Active Directory permission toomake changes tooyour Dropbox for Business tenant.</span></span> <span data-ttu-id="fe910-138">Tıklatın **izin**.</span><span class="sxs-lookup"><span data-stu-id="fe910-138">Click **Allow**.</span></span>
    
      <span data-ttu-id="fe910-139">![Kullanıcı sağlamayı](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769519.png "kullanıcı hazırlama")</span><span class="sxs-lookup"><span data-stu-id="fe910-139">![User provisioning](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769519.png "User provisioning")</span></span>

8. <span data-ttu-id="fe910-140">Hello Azure portal'ı tıklatın **Bağlantıyı Sına** tooensure Azure AD iş uygulaması için Dropbox tooyour bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="fe910-140">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Dropbox for Business app.</span></span> <span data-ttu-id="fe910-141">Merhaba bağlantı başarısız olursa, iş hesabı Team yönetici izinleri olan için Dropbox emin olun ve hello deneyin **"Yetkilendir"** adım yeniden uygulayın.</span><span class="sxs-lookup"><span data-stu-id="fe910-141">If hello connection fails, ensure your Dropbox for Business account has Team Admin permissions and try hello **"Authorize"** step again.</span></span>

9. <span data-ttu-id="fe910-142">Bir kişi veya hello sağlama hata bildirimi alması gereken Grup Hello e-posta adresini girin **bildirim e-posta** alan ve hello onay kutusunu işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="fe910-142">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox.</span></span>

10. <span data-ttu-id="fe910-143">Tıklatın **kaydedin.**</span><span class="sxs-lookup"><span data-stu-id="fe910-143">Click **Save.**</span></span>

11. <span data-ttu-id="fe910-144">Hello eşlemeleri bölümü altında seçin **iş için Azure Active Directory Kullanıcıları Eşitle tooDropbox.**</span><span class="sxs-lookup"><span data-stu-id="fe910-144">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooDropbox for Business.**</span></span>

12. <span data-ttu-id="fe910-145">Merhaba, **öznitelik eşlemelerini** bölümü, işletmeniz için Azure AD tooDropbox eşitlenir hello kullanıcı öznitelikleri gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="fe910-145">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooDropbox for Business.</span></span> <span data-ttu-id="fe910-146">Merhaba olarak seçilen öznitelikler **eşleşen** Itanium tabanlı sistemler için kullanılan toomatch hello kullanıcı hesapları, iş için Dropbox güncelleştirme işlemleri için özelliklerdir.</span><span class="sxs-lookup"><span data-stu-id="fe910-146">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Dropbox for Business for update operations.</span></span> <span data-ttu-id="fe910-147">Merhaba Kaydet düğmesine toocommit herhangi bir değişiklik seçin.</span><span class="sxs-lookup"><span data-stu-id="fe910-147">Select hello Save button toocommit any changes.</span></span>

13. <span data-ttu-id="fe910-148">tooenable hello Azure AD sağlama hizmeti iş, değişiklik hello için dropbox **sağlama durumu** çok**üzerinde** hello ayarları bölümünün içinde</span><span class="sxs-lookup"><span data-stu-id="fe910-148">tooenable hello Azure AD provisioning service for Dropbox for Business, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

14. <span data-ttu-id="fe910-149">Tıklatın **kaydedin.**</span><span class="sxs-lookup"><span data-stu-id="fe910-149">Click **Save.**</span></span>

<span data-ttu-id="fe910-150">Herhangi bir kullanıcı ve/veya hello kullanıcılar, iş için tooDropbox ve Gruplar bölümü atanan gruplarını hello ilk eşitleme başlatır.</span><span class="sxs-lookup"><span data-stu-id="fe910-150">It starts hello initial synchronization of any users and/or groups assigned tooDropbox for Business in hello Users and Groups section.</span></span> <span data-ttu-id="fe910-151">Merhaba ilk eşitleme yaklaşık 20 dakikada hello çalıştığı sürece oluşan sonraki eşitlemeler daha uzun tooperform alır.</span><span class="sxs-lookup"><span data-stu-id="fe910-151">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="fe910-152">Merhaba kullanabilirsiniz **eşitleme ayrıntıları** bölümünde toomonitor ilerleme ve, Dropbox bir hizmette iş uygulaması sağlama hello tarafından gerçekleştirilen tüm eylemler anlatılmaktadır bağlantılar tooprovisioning etkinlik raporları izleyin.</span><span class="sxs-lookup"><span data-stu-id="fe910-152">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Dropbox for Business app.</span></span>

<span data-ttu-id="fe910-153">Şimdi sınama hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fe910-153">You can now create a test account.</span></span> <span data-ttu-id="fe910-154">İçin iş için tooDropbox hello hesap tooverify eşitlenmiş too20 dakika bekleyin.</span><span class="sxs-lookup"><span data-stu-id="fe910-154">Wait for up too20 minutes tooverify that hello account has been synchronized tooDropbox for Business.</span></span>

<span data-ttu-id="fe910-155">Başarıyla tamamlanan kullanıcı döngüsü hazırlama ilgili durumuna göre belirtilir.</span><span class="sxs-lookup"><span data-stu-id="fe910-155">A successfully completed user provisioning cycle is indicated by a related status.</span></span>

<span data-ttu-id="fe910-156">![Kullanıcılar atama](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/IC769523.png "kullanıcı atama")</span><span class="sxs-lookup"><span data-stu-id="fe910-156">![Assign users](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/IC769523.png "Assign users")</span></span>


## <a name="additional-resources"></a><span data-ttu-id="fe910-157">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="fe910-157">Additional resources</span></span>

* [<span data-ttu-id="fe910-158">Kullanıcı hesabı Kurumsal uygulamaları için sağlama yönetme</span><span class="sxs-lookup"><span data-stu-id="fe910-158">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fe910-159">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="fe910-159">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="fe910-160">Çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="fe910-160">Configure Single Sign-on</span></span>](active-directory-saas-dropboxforbusiness-tutorial.md)