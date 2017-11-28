---
title: "aaaActive Directory Federasyon Hizmetleri Yönetimi ve Azure AD Connect ile özelleştirme | Microsoft Docs"
description: "Azure AD Connect ve AD FS oturum açma ile kullanıcı deneyimi Azure AD Connect ve PowerShell özelleştirmesini ile AD FS yönetimi."
keywords: "AD FS, ADFS, AD FS yönetimi, AAD bağlanma, bağlan, oturum açma, AD FS özelleştirmesi, onarım güven, O365, Federasyon, bağlı olan taraf"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: 2593b6c6-dc3f-46ef-8e02-a8e2dc4e9fb9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 361a2bfd6d7a6993dbe773d6ea039ad1afc6346a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-and-customize-active-directory-federation-services-by-using-azure-ad-connect"></a><span data-ttu-id="070d9-104">Yönetmek ve Azure AD Connect kullanarak Active Directory Federasyon Hizmetleri özelleştirme</span><span class="sxs-lookup"><span data-stu-id="070d9-104">Manage and customize Active Directory Federation Services by using Azure AD Connect</span></span>
<span data-ttu-id="070d9-105">Bu makalede nasıl toomanage ve Azure Active Directory (Azure AD) Bağlan kullanarak Active Directory Federasyon Hizmetleri (AD FS) özelleştirin.</span><span class="sxs-lookup"><span data-stu-id="070d9-105">This article describes how toomanage and customize Active Directory Federation Services (AD FS) by using Azure Active Directory (Azure AD) Connect.</span></span> <span data-ttu-id="070d9-106">Ayrıca, bir AD FS grubu için bir tam yapılandırma toodo gerekebilecek diğer ortak AD FS görevler içerir.</span><span class="sxs-lookup"><span data-stu-id="070d9-106">It also includes other common AD FS tasks that you might need toodo for a complete configuration of an AD FS farm.</span></span>

| <span data-ttu-id="070d9-107">Konu</span><span class="sxs-lookup"><span data-stu-id="070d9-107">Topic</span></span> | <span data-ttu-id="070d9-108">Ne kapsar</span><span class="sxs-lookup"><span data-stu-id="070d9-108">What it covers</span></span> |
|:--- |:--- |
| <span data-ttu-id="070d9-109">**AD FS yönetme**</span><span class="sxs-lookup"><span data-stu-id="070d9-109">**Manage AD FS**</span></span> | |
| [<span data-ttu-id="070d9-110">Onarım hello güven</span><span class="sxs-lookup"><span data-stu-id="070d9-110">Repair hello trust</span></span>](#repairthetrust) |<span data-ttu-id="070d9-111">Nasıl toorepair hello Federasyon ile Office 365 güven.</span><span class="sxs-lookup"><span data-stu-id="070d9-111">How toorepair hello federation trust with Office 365.</span></span> |
| [<span data-ttu-id="070d9-112">Alternatif oturum açma Kimliğini kullanarak Azure AD ile birleştirmek</span><span class="sxs-lookup"><span data-stu-id="070d9-112">Federate with Azure AD using alternate login ID </span></span>](#alternateid) | <span data-ttu-id="070d9-113">Alternatif oturum açma Kimliğini kullanarak Federasyon yapılandırma</span><span class="sxs-lookup"><span data-stu-id="070d9-113">Configure federation using alternate login ID</span></span>  |
| [<span data-ttu-id="070d9-114">Bir AD FS sunucu ekleme</span><span class="sxs-lookup"><span data-stu-id="070d9-114">Add an AD FS server</span></span>](#addadfsserver) |<span data-ttu-id="070d9-115">Nasıl tooexpand bir AD FS ile ek bir AD FS sunucu grubu.</span><span class="sxs-lookup"><span data-stu-id="070d9-115">How tooexpand an AD FS farm with an additional AD FS server.</span></span> |
| [<span data-ttu-id="070d9-116">Bir AD FS Web uygulaması Ara Sunucusu Ekle</span><span class="sxs-lookup"><span data-stu-id="070d9-116">Add an AD FS Web Application Proxy server</span></span>](#addwapserver) |<span data-ttu-id="070d9-117">Nasıl tooexpand bir AD FS ile ek bir Web uygulaması Ara sunucusu (WAP) sunucu grubu.</span><span class="sxs-lookup"><span data-stu-id="070d9-117">How tooexpand an AD FS farm with an additional Web Application Proxy (WAP) server.</span></span> |
| [<span data-ttu-id="070d9-118">Bir Federasyon etki alanına ekleme</span><span class="sxs-lookup"><span data-stu-id="070d9-118">Add a federated domain</span></span>](#addfeddomain) |<span data-ttu-id="070d9-119">Nasıl tooadd federe bir etki alanı.</span><span class="sxs-lookup"><span data-stu-id="070d9-119">How tooadd a federated domain.</span></span> |
| [<span data-ttu-id="070d9-120">Merhaba SSL sertifikasını güncelleştir</span><span class="sxs-lookup"><span data-stu-id="070d9-120">Update hello SSL certificate</span></span>](active-directory-aadconnectfed-ssl-update.md)| <span data-ttu-id="070d9-121">Nasıl tooupdate hello SSL sertifikası için bir AD FS grubu.</span><span class="sxs-lookup"><span data-stu-id="070d9-121">How tooupdate hello SSL certificate for an AD FS farm.</span></span> |
| <span data-ttu-id="070d9-122">**AD FS özelleştirme**</span><span class="sxs-lookup"><span data-stu-id="070d9-122">**Customize AD FS**</span></span> | |
| [<span data-ttu-id="070d9-123">Özel şirket logosu veya çizim ekleme</span><span class="sxs-lookup"><span data-stu-id="070d9-123">Add a custom company logo or illustration</span></span>](#customlogo) |<span data-ttu-id="070d9-124">Nasıl toocustomize bir AD FS oturum açma sayfasında bir şirket logo ve çizim.</span><span class="sxs-lookup"><span data-stu-id="070d9-124">How toocustomize an AD FS sign-in page with a company logo and illustration.</span></span> |
| [<span data-ttu-id="070d9-125">Bir oturum açma açıklama ekleme</span><span class="sxs-lookup"><span data-stu-id="070d9-125">Add a sign-in description</span></span>](#addsignindescription) |<span data-ttu-id="070d9-126">Nasıl bir oturum açma tooadd sayfa açıklaması.</span><span class="sxs-lookup"><span data-stu-id="070d9-126">How tooadd a sign-in page description.</span></span> |
| [<span data-ttu-id="070d9-127">AD FS talep kuralları değiştirme</span><span class="sxs-lookup"><span data-stu-id="070d9-127">Modify AD FS claim rules</span></span>](#modclaims) |<span data-ttu-id="070d9-128">Nasıl toomodify AD FS için çeşitli Federasyon senaryoları talepleri.</span><span class="sxs-lookup"><span data-stu-id="070d9-128">How toomodify AD FS claims for various federation scenarios.</span></span> |

## <a name="manage-ad-fs"></a><span data-ttu-id="070d9-129">AD FS yönetme</span><span class="sxs-lookup"><span data-stu-id="070d9-129">Manage AD FS</span></span>
<span data-ttu-id="070d9-130">Hello Azure AD Connect Sihirbazı'nı kullanarak Azure AD CONNECT'te minimum kullanıcı katılımıyla çeşitli AD FS ile ilgili görevleri gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="070d9-130">You can perform various AD FS-related tasks in Azure AD Connect with minimal user intervention by using hello Azure AD Connect wizard.</span></span> <span data-ttu-id="070d9-131">Çalışan Başlangıç Sihirbazı tarafından Azure AD Connect'i yüklemeye bitirdikten sonra hello Sihirbazı'nı çalıştırabilirsiniz yeniden tooperform ek görevleri.</span><span class="sxs-lookup"><span data-stu-id="070d9-131">After you've finished installing Azure AD Connect by running hello wizard, you can run hello wizard again tooperform additional tasks.</span></span>

## <span data-ttu-id="070d9-132">Onarım hello güven<a name=repairthetrust></a></span><span class="sxs-lookup"><span data-stu-id="070d9-132">Repair hello trust <a name=repairthetrust></a></span></span>
<span data-ttu-id="070d9-133">Azure AD Connect toocheck hello geçerli durumunu hello AD FS ve Azure AD güveni kullanın ve uygun eylemleri toorepair hello güven gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="070d9-133">You can use Azure AD Connect toocheck hello current health of hello AD FS and Azure AD trust and take appropriate actions toorepair hello trust.</span></span> <span data-ttu-id="070d9-134">Bu adımları toorepair izleyin, Azure AD ve AD FS güven.</span><span class="sxs-lookup"><span data-stu-id="070d9-134">Follow these steps toorepair your Azure AD and AD FS trust.</span></span>

1. <span data-ttu-id="070d9-135">Seçin **onarım AAD ve ADFS güven** ek görevleri hello listesinden.</span><span class="sxs-lookup"><span data-stu-id="070d9-135">Select **Repair AAD and ADFS Trust** from hello list of additional tasks.</span></span>
   <span data-ttu-id="070d9-136">![Onarım AAD ve ADFS güveni](media/active-directory-aadconnect-federation-management/RepairADTrust1.PNG)</span><span class="sxs-lookup"><span data-stu-id="070d9-136">![Repair AAD and ADFS Trust](media/active-directory-aadconnect-federation-management/RepairADTrust1.PNG)</span></span>

2. <span data-ttu-id="070d9-137">Merhaba üzerinde **tooAzure AD Connect** sayfasında, Azure AD genel yönetici kimlik bilgilerinizi sağlayın ve tıklayın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="070d9-137">On hello **Connect tooAzure AD** page, provide your global administrator credentials for Azure AD, and click **Next**.</span></span>
   <span data-ttu-id="070d9-138">![TooAzure AD connect](media/active-directory-aadconnect-federation-management/RepairADTrust2.PNG)</span><span class="sxs-lookup"><span data-stu-id="070d9-138">![Connect tooAzure AD](media/active-directory-aadconnect-federation-management/RepairADTrust2.PNG)</span></span>

3. <span data-ttu-id="070d9-139">Merhaba üzerinde **uzaktan erişim kimlik bilgileri** sayfasında, hello etki alanı yöneticisi hello kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="070d9-139">On hello **Remote access credentials** page, enter hello credentials for hello domain administrator.</span></span>

   ![Uzaktan erişim kimlik bilgileri](media/active-directory-aadconnect-federation-management/RepairADTrust3.PNG)

    <span data-ttu-id="070d9-141">Tıklattıktan sonra **sonraki**, Azure AD Connect için sertifika durumu denetler ve sorunları gösterir.</span><span class="sxs-lookup"><span data-stu-id="070d9-141">After you click **Next**, Azure AD Connect checks for certificate health and shows any issues.</span></span>

    ![Sertifika durumu](media/active-directory-aadconnect-federation-management/RepairADTrust4.PNG)

    <span data-ttu-id="070d9-143">Merhaba **hazır tooconfigure** sayfa gösterir hello olacaktır eylemlerin listesini gerçekleştirilen toorepair hello güven.</span><span class="sxs-lookup"><span data-stu-id="070d9-143">hello **Ready tooconfigure** page shows hello list of actions that will be performed toorepair hello trust.</span></span>

    ![Hazır tooconfigure](media/active-directory-aadconnect-federation-management/RepairADTrust5.PNG)

4. <span data-ttu-id="070d9-145">Tıklatın **yükleme** toorepair hello güven.</span><span class="sxs-lookup"><span data-stu-id="070d9-145">Click **Install** toorepair hello trust.</span></span>

> [!NOTE]
> <span data-ttu-id="070d9-146">Azure AD Connect can yalnızca onarma veya otomatik olarak imzalanan sertifikalar vermemizi.</span><span class="sxs-lookup"><span data-stu-id="070d9-146">Azure AD Connect can only repair or act on certificates that are self-signed.</span></span> <span data-ttu-id="070d9-147">Azure AD Connect, üçüncü taraf sertifikalarının onarılamıyor.</span><span class="sxs-lookup"><span data-stu-id="070d9-147">Azure AD Connect can't repair third-party certificates.</span></span>

## <span data-ttu-id="070d9-148">AlternateID kullanarak Azure AD ile birleştirmek<a name=alternateid></a></span><span class="sxs-lookup"><span data-stu-id="070d9-148">Federate with Azure AD using AlternateID <a name=alternateid></a></span></span>
<span data-ttu-id="070d9-149">Bunu hello içi kullanıcı asıl Name(UPN) ve kullanıcı asıl adı tutulur hello Bulut aynı hello önerilir.</span><span class="sxs-lookup"><span data-stu-id="070d9-149">It is recommended that hello on-premises User Principal Name(UPN) and hello cloud User Principal Name are kept hello same.</span></span> <span data-ttu-id="070d9-150">Merhaba içi UPN (örn. yönlendirilemeyen bir etki alanı kullanıyorsa</span><span class="sxs-lookup"><span data-stu-id="070d9-150">If hello on-premises UPN uses a non-routable domain (ex.</span></span> <span data-ttu-id="070d9-151">Contoso.local) ya da değiştirilemez toolocal uygulama bağımlılıkları öneririz alternatif oturum açma kimliği ayarlama</span><span class="sxs-lookup"><span data-stu-id="070d9-151">Contoso.local) or cannot be changed due toolocal application dependencies, we recommend setting up alternate login ID.</span></span> <span data-ttu-id="070d9-152">Alternatif oturum açma kimliği, bir oturum açma deneyimi posta gibi kendi UPN dışında bir öznitelik oturum nerede kullanıcılar oturum tooconfigure sağlar.</span><span class="sxs-lookup"><span data-stu-id="070d9-152">Alternate login ID allows you tooconfigure a sign-in experience where users can sign in with an attribute other than their UPN, such as mail.</span></span> <span data-ttu-id="070d9-153">Azure AD Connect varsayılan toohello userPrincipalName özniteliğindeki Active Directory kullanıcı asıl adı için Hello seçimdir.</span><span class="sxs-lookup"><span data-stu-id="070d9-153">hello choice for User Principal Name in Azure AD Connect defaults toohello userPrincipalName attribute in Active Directory.</span></span> <span data-ttu-id="070d9-154">Kullanıcı asıl adı için başka bir öznitelik seçin ve AD FS kullanarak federasyonunu, ardından Azure AD Connect alternatif oturum açma kimliği için AD FS yapılandırma</span><span class="sxs-lookup"><span data-stu-id="070d9-154">If you choose any other attribute for User Principal Name and are federating using AD FS, then Azure AD Connect will configure AD FS for alternate login ID.</span></span> <span data-ttu-id="070d9-155">Kullanıcı asıl adı için farklı bir öznitelik seçme örneği aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="070d9-155">An example of choosing a different attribute for User Principal Name is shown below:</span></span>

![Alternatif kimlik öznitelik seçimi](media/active-directory-aadconnect-federation-management/attributeselection.png)

<span data-ttu-id="070d9-157">AD FS için alternatif oturum açma Kimliğini yapılandırma iki ana adımdan oluşur:</span><span class="sxs-lookup"><span data-stu-id="070d9-157">Configuring alternate login ID for AD FS consists of two main steps:</span></span>
1. <span data-ttu-id="070d9-158">**Merhaba sağ verme talep kümesini yapılandırmak**: hello verme talep kurallarıyla hello Azure AD bağlı olan taraf güven alternatif hello kullanıcının Kimliğini hello gibi değiştirilmiş toouse seçili hello UserPrincipalName özniteliği olan.</span><span class="sxs-lookup"><span data-stu-id="070d9-158">**Configure hello right set of issuance claims**: hello issuance claim rules in hello Azure AD relying party trust are modified toouse hello selected UserPrincipalName attribute as hello alternate ID of hello user.</span></span>
2. <span data-ttu-id="070d9-159">**Alternatif oturum açma kimliği hello AD FS yapılandırması etkinleştirme**: hello AD FS yapılandırması, böylece kullanıcılar hello uygun ormanlarda hello alternatif kimliğini kullanarak AD FS arayabilir güncelleştirilir</span><span class="sxs-lookup"><span data-stu-id="070d9-159">**Enable alternate login ID in hello AD FS configuration**: hello AD FS configuration is updated so that AD FS can look up users in hello appropriate forests using hello alternate ID.</span></span> <span data-ttu-id="070d9-160">Bu yapılandırma, AD FS için Windows Server 2012 R2 (KB2919355) veya sonraki sürümlerde desteklenir.</span><span class="sxs-lookup"><span data-stu-id="070d9-160">This configuration is supported for AD FS on Windows Server 2012 R2 (with KB2919355) or later.</span></span> <span data-ttu-id="070d9-161">Merhaba AD FS 2012 R2 sunuculardır, Azure AD Connect hello hello varlığını denetler KB gereklidir.</span><span class="sxs-lookup"><span data-stu-id="070d9-161">If hello AD FS servers are 2012 R2, Azure AD Connect checks for hello presence of hello required KB.</span></span> <span data-ttu-id="070d9-162">Merhaba KB algılanmazsa, yapılandırma tamamlandıktan sonra bir uyarı aşağıda gösterildiği gibi görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="070d9-162">If hello KB is not detected, a warning will be displayed after configuration completes, as shown below:</span></span>

    ![KB 2012R2 üzerinde eksik uyarı](media/active-directory-aadconnect-federation-management/kbwarning.png)

    <span data-ttu-id="070d9-164">eksik KB durumunda toorectify hello yapılandırmasını yüklemek gerekli hello [KB2919355](http://go.microsoft.com/fwlink/?LinkID=396590) ve güven hello kullanarak Onar [AAD onarın ve AD FS güven](#repairthetrust).</span><span class="sxs-lookup"><span data-stu-id="070d9-164">toorectify hello configuration in case of missing KB, install hello required [KB2919355](http://go.microsoft.com/fwlink/?LinkID=396590) and then repair hello trust using [Repair AAD and AD FS Trust](#repairthetrust).</span></span>

> [!NOTE]
> <span data-ttu-id="070d9-165">AlternateID ve adımları toomanually hakkında daha fazla bilgi için yapılandırma, okuma [alternatif oturum açma Kimliğini yapılandırma](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configuring-alternate-login-id)</span><span class="sxs-lookup"><span data-stu-id="070d9-165">For more information on alternateID and steps toomanually configure, read [Configuring Alternate Login ID](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configuring-alternate-login-id)</span></span>

## <span data-ttu-id="070d9-166">Bir AD FS sunucu ekleme<a name=addadfsserver></a></span><span class="sxs-lookup"><span data-stu-id="070d9-166">Add an AD FS server <a name=addadfsserver></a></span></span>

> [!NOTE]
> <span data-ttu-id="070d9-167">tooadd bir AD FS sunucusu, Azure AD Connect hello PFX sertifikası gerektirir.</span><span class="sxs-lookup"><span data-stu-id="070d9-167">tooadd an AD FS server, Azure AD Connect requires hello PFX certificate.</span></span> <span data-ttu-id="070d9-168">Bu nedenle, yalnızca hello AD FS grubunu Azure AD Connect kullanarak yapılandırdıysanız bu işlemi gerçekleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="070d9-168">Therefore, you can perform this operation only if you configured hello AD FS farm by using Azure AD Connect.</span></span>

1. <span data-ttu-id="070d9-169">Seçin **ek bir Federasyon Sunucusu'nu Dağıtma**, tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="070d9-169">Select **Deploy an additional Federation Server**, and click **Next**.</span></span>

   ![Ek Federasyon sunucusu](media/active-directory-aadconnect-federation-management/AddNewADFSServer1.PNG)

2. <span data-ttu-id="070d9-171">Merhaba üzerinde **tooAzure AD Connect** sayfasında, Azure AD genel yönetici kimlik bilgilerinizi girin ve tıklayın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="070d9-171">On hello **Connect tooAzure AD** page, enter your global administrator credentials for Azure AD, and click **Next**.</span></span>

   ![TooAzure AD connect](media/active-directory-aadconnect-federation-management/AddNewADFSServer2.PNG)

3. <span data-ttu-id="070d9-173">Merhaba etki alanı yönetici kimlik bilgilerini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="070d9-173">Provide hello domain administrator credentials.</span></span>

   ![Etki alanı yönetici kimlik bilgileri](media/active-directory-aadconnect-federation-management/AddNewADFSServer3.PNG)

4. <span data-ttu-id="070d9-175">Azure AD Connect Azure AD Connect ile yeni AD FS grubunuzu yapılandırılırken sağlanmış hello PFX dosyasının hello parola ister.</span><span class="sxs-lookup"><span data-stu-id="070d9-175">Azure AD Connect asks for hello password of hello PFX file that you provided while configuring your new AD FS farm with Azure AD Connect.</span></span> <span data-ttu-id="070d9-176">Tıklatın **parolasını girin** hello PFX dosyası tooprovide hello parolası.</span><span class="sxs-lookup"><span data-stu-id="070d9-176">Click **Enter Password** tooprovide hello password for hello PFX file.</span></span>

   ![Sertifika parolası](media/active-directory-aadconnect-federation-management/AddNewADFSServer4.PNG)

    ![SSL sertifikasını belirtin](media/active-directory-aadconnect-federation-management/AddNewADFSServer5.PNG)

5. <span data-ttu-id="070d9-179">Merhaba üzerinde **AD FS sunucuları** hello sunucu adı veya IP adresi toobe eklenen want toohello AD FS grubu.</span><span class="sxs-lookup"><span data-stu-id="070d9-179">On hello **AD FS Servers** page, enter hello server name or IP address toobe added toohello AD FS farm.</span></span>

   ![AD FS sunucuları](media/active-directory-aadconnect-federation-management/AddNewADFSServer6.PNG)

6. <span data-ttu-id="070d9-181">Tıklatın **sonraki**ve hello son Git **yapılandırma** sayfası.</span><span class="sxs-lookup"><span data-stu-id="070d9-181">Click **Next**, and go through hello final **Configure** page.</span></span> <span data-ttu-id="070d9-182">Azure AD Connect hello sunucuları toohello AD FS grubu ekleme tamamlandıktan sonra hello seçeneği tooverify hello bağlantısı verilir.</span><span class="sxs-lookup"><span data-stu-id="070d9-182">After Azure AD Connect has finished adding hello servers toohello AD FS farm, you will be given hello option tooverify hello connectivity.</span></span>

   ![Hazır tooconfigure](media/active-directory-aadconnect-federation-management/AddNewADFSServer7.PNG)

    ![Yükleme tamamlandı](media/active-directory-aadconnect-federation-management/AddNewADFSServer8.PNG)

## <span data-ttu-id="070d9-185">Bir AD FS WAP sunucusu ekleme<a name=addwapserver></a></span><span class="sxs-lookup"><span data-stu-id="070d9-185">Add an AD FS WAP server <a name=addwapserver></a></span></span>

> [!NOTE]
> <span data-ttu-id="070d9-186">tooadd WAP sunucusu, Azure AD Connect hello PFX sertifikası gerektirir.</span><span class="sxs-lookup"><span data-stu-id="070d9-186">tooadd a WAP server, Azure AD Connect requires hello PFX certificate.</span></span> <span data-ttu-id="070d9-187">Bu nedenle, Azure AD Connect kullanarak hello AD FS grubunu yapılandırdıysanız bu işlemi yalnızca gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="070d9-187">Therefore, you can only perform this operation if you configured hello AD FS farm by using Azure AD Connect.</span></span>

1. <span data-ttu-id="070d9-188">Seçin **Web uygulaması proxy'si dağıtmak** hello kullanılabilir görevler listesinden.</span><span class="sxs-lookup"><span data-stu-id="070d9-188">Select **Deploy Web Application Proxy** from hello list of available tasks.</span></span>

   ![Web uygulaması Ara sunucusu](media/active-directory-aadconnect-federation-management/WapServer1.PNG)

2. <span data-ttu-id="070d9-190">Hello Azure genel yönetici kimlik bilgilerini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="070d9-190">Provide hello Azure global administrator credentials.</span></span>

   ![TooAzure AD connect](media/active-directory-aadconnect-federation-management/wapserver2.PNG)

3. <span data-ttu-id="070d9-192">Merhaba üzerinde **belirtin SSL sertifikası** sayfasında, Azure AD Connect ile Merhaba AD FS grubu yapılandırıldığında, sağladığınız hello PFX dosyasının hello parola sağlayın.</span><span class="sxs-lookup"><span data-stu-id="070d9-192">On hello **Specify SSL certificate** page, provide hello password for hello PFX file that you provided when you configured hello AD FS farm with Azure AD Connect.</span></span>
   <span data-ttu-id="070d9-193">![Sertifika parolası](media/active-directory-aadconnect-federation-management/WapServer3.PNG)</span><span class="sxs-lookup"><span data-stu-id="070d9-193">![Certificate password](media/active-directory-aadconnect-federation-management/WapServer3.PNG)</span></span>

    ![SSL sertifikasını belirtin](media/active-directory-aadconnect-federation-management/WapServer4.PNG)

4. <span data-ttu-id="070d9-195">WAP sunucusu olarak eklenen hello sunucu toobe ekleyin.</span><span class="sxs-lookup"><span data-stu-id="070d9-195">Add hello server toobe added as a WAP server.</span></span> <span data-ttu-id="070d9-196">Merhaba WAP sunucusu etki alanına katılmış toohello olabilir çünkü hello sihirbaz eklenen yönetici kimlik bilgileri toohello sunucusu için sorar.</span><span class="sxs-lookup"><span data-stu-id="070d9-196">Because hello WAP server might not be joined toohello domain, hello wizard asks for administrative credentials toohello server being added.</span></span>

   ![Yönetim sunucusu kimlik bilgileri](media/active-directory-aadconnect-federation-management/WapServer5.PNG)

5. <span data-ttu-id="070d9-198">Merhaba üzerinde **Proxy güven kimlik bilgilerini** sayfasında, yönetici kimlik bilgileri tooconfigure hello proxy hello AD FS grubunda, hello birincil sunucu güven ve erişim sağlayın.</span><span class="sxs-lookup"><span data-stu-id="070d9-198">On hello **Proxy trust credentials** page, provide administrative credentials tooconfigure hello proxy trust and access hello primary server in hello AD FS farm.</span></span>

   ![Proxy güven kimlik bilgileri](media/active-directory-aadconnect-federation-management/WapServer6.PNG)

6. <span data-ttu-id="070d9-200">Merhaba üzerinde **hazır tooconfigure** sayfasında, hello Sihirbazı gerçekleştirilecek eylemler hello listesini gösterir.</span><span class="sxs-lookup"><span data-stu-id="070d9-200">On hello **Ready tooconfigure** page, hello wizard shows hello list of actions that will be performed.</span></span>

   ![Hazır tooconfigure](media/active-directory-aadconnect-federation-management/WapServer7.PNG)

7. <span data-ttu-id="070d9-202">Tıklatın **yükleme** toofinish hello yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="070d9-202">Click **Install** toofinish hello configuration.</span></span> <span data-ttu-id="070d9-203">Merhaba Yapılandırma tamamlandıktan sonra seçeneği tooverify hello hello Sihirbazı verir bağlantı toohello sunucuları hello.</span><span class="sxs-lookup"><span data-stu-id="070d9-203">After hello configuration is complete, hello wizard gives you hello option tooverify hello connectivity toohello servers.</span></span> <span data-ttu-id="070d9-204">Tıklatın **doğrula** toocheck bağlantısı.</span><span class="sxs-lookup"><span data-stu-id="070d9-204">Click **Verify** toocheck connectivity.</span></span>

   ![Yükleme tamamlandı](media/active-directory-aadconnect-federation-management/WapServer8.PNG)

## <span data-ttu-id="070d9-206">Bir Federasyon etki alanına ekleme<a name=addfeddomain></a></span><span class="sxs-lookup"><span data-stu-id="070d9-206">Add a federated domain <a name=addfeddomain></a></span></span>

<span data-ttu-id="070d9-207">Azure AD Connect kullanarak Azure AD ile bir etki alanı toobe federe kolay tooadd olur.</span><span class="sxs-lookup"><span data-stu-id="070d9-207">It's easy tooadd a domain toobe federated with Azure AD by using Azure AD Connect.</span></span> <span data-ttu-id="070d9-208">Azure AD Connect hello etki alanını Federasyon ekler ve hello talep kuralları toocorrectly yansıtmak hello veren Azure AD ile birleştirildiyse birden çok etki alanınız olduğunda değiştirir.</span><span class="sxs-lookup"><span data-stu-id="070d9-208">Azure AD Connect adds hello domain for federation and modifies hello claim rules toocorrectly reflect hello issuer when you have multiple domains federated with Azure AD.</span></span>

1. <span data-ttu-id="070d9-209">tooadd bir Federasyon etki alanını seçin hello görev **ek bir ekleme Azure AD etki alanı**.</span><span class="sxs-lookup"><span data-stu-id="070d9-209">tooadd a federated domain, select hello task **Add an additional Azure AD domain**.</span></span>

   ![Ek Azure AD etki alanı](media/active-directory-aadconnect-federation-management/AdditionalDomain1.PNG)

2. <span data-ttu-id="070d9-211">Hello sonraki sayfada hello Sihirbazı'nın, Azure AD için hello genel yönetici kimlik bilgilerini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="070d9-211">On hello next page of hello wizard, provide hello global administrator credentials for Azure AD.</span></span>

   ![TooAzure AD connect](media/active-directory-aadconnect-federation-management/AdditionalDomain2.PNG)

3. <span data-ttu-id="070d9-213">Merhaba üzerinde **uzaktan erişim kimlik bilgileri** sayfasında, hello etki alanı yönetici kimlik bilgilerini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="070d9-213">On hello **Remote access credentials** page, provide hello domain administrator credentials.</span></span>

   ![Uzaktan erişim kimlik bilgileri](media/active-directory-aadconnect-federation-management/additionaldomain3.PNG)

4. <span data-ttu-id="070d9-215">Merhaba sonraki sayfada, Başlangıç Sihirbazı, şirket içi dizininizle Azure AD etki alanlarının bir listesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="070d9-215">On hello next page, hello wizard provides a list of Azure AD domains that you can federate your on-premises directory with.</span></span> <span data-ttu-id="070d9-216">Merhaba etki alanı hello listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="070d9-216">Choose hello domain from hello list.</span></span>

   ![Azure AD etki alanı](media/active-directory-aadconnect-federation-management/AdditionalDomain4.PNG)

    <span data-ttu-id="070d9-218">Hello etki alanını seçtikten sonra Başlangıç Sihirbazı, sihirbaz hello başka eylemler hakkında uygun bilgilerle alın ve hello yapılandırma etkisini hello sağlar.</span><span class="sxs-lookup"><span data-stu-id="070d9-218">After you choose hello domain, hello wizard provides you with appropriate information about further actions that hello wizard will take and hello impact of hello configuration.</span></span> <span data-ttu-id="070d9-219">Bazı durumlarda, Azure AD'de hello Sihirbazı ile bilgi toohelp sağlar henüz doğrulandı olmayan bir etki alanı seçerseniz hello etki alanını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="070d9-219">In some cases, if you select a domain that isn't yet verified in Azure AD, hello wizard provides you with information toohelp you verify hello domain.</span></span> <span data-ttu-id="070d9-220">Bkz: [özel etki alanı adı tooAzure Active Directory eklemek](../active-directory-add-domain.md) daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="070d9-220">See [Add your custom domain name tooAzure Active Directory](../active-directory-add-domain.md) for more details.</span></span>

5. <span data-ttu-id="070d9-221">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="070d9-221">Click **Next**.</span></span> <span data-ttu-id="070d9-222">Merhaba **hazır tooconfigure** sayfası hello Azure AD Connect gerçekleştireceği eylemlerin listesini gösterir.</span><span class="sxs-lookup"><span data-stu-id="070d9-222">hello **Ready tooconfigure** page shows hello list of actions that Azure AD Connect will perform.</span></span> <span data-ttu-id="070d9-223">Tıklatın **yükleme** toofinish hello yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="070d9-223">Click **Install** toofinish hello configuration.</span></span>

   ![Hazır tooconfigure](media/active-directory-aadconnect-federation-management/AdditionalDomain5.PNG)

> [!NOTE]
> <span data-ttu-id="070d9-225">Merhaba kullanıcılardan mümkün toologin tooAzure AD olabilmesi Federasyon etki alanını eşitlenmesi gereken eklendi.</span><span class="sxs-lookup"><span data-stu-id="070d9-225">Users from hello added federated domain must be synchronized before they will be able toologin tooAzure AD.</span></span>

## <a name="ad-fs-customization"></a><span data-ttu-id="070d9-226">AD FS özelleştirmesi</span><span class="sxs-lookup"><span data-stu-id="070d9-226">AD FS customization</span></span>
<span data-ttu-id="070d9-227">Merhaba aşağıdaki bölümler hello yaygın görevlerden bazıları hakkında ayrıntılar AD FS oturum açma sayfanız özelleştirdiğinizde tooperform olabilir sağlar.</span><span class="sxs-lookup"><span data-stu-id="070d9-227">hello following sections provide details about some of hello common tasks that you might have tooperform when you customize your AD FS sign-in page.</span></span>

## <span data-ttu-id="070d9-228">Özel şirket logosu veya çizim ekleme<a name=customlogo></a></span><span class="sxs-lookup"><span data-stu-id="070d9-228">Add a custom company logo or illustration <a name=customlogo></a></span></span>
<span data-ttu-id="070d9-229">Merhaba üzerinde görüntülenen hello şirketin toochange hello logosunu **oturum açma** sayfasında, aşağıdaki Windows PowerShell cmdlet'ini ve sözdizimini hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="070d9-229">toochange hello logo of hello company that's displayed on hello **Sign-in** page, use hello following Windows PowerShell cmdlet and syntax.</span></span>

> [!NOTE]
> <span data-ttu-id="070d9-230">Merhaba Hello logosu için bir dosya boyutu 10 KB'den büyük olmaması 96 dpi'de 260 x 35 boyutları önerilir.</span><span class="sxs-lookup"><span data-stu-id="070d9-230">hello recommended dimensions for hello logo are 260 x 35 @ 96 dpi with a file size no greater than 10 KB.</span></span>

    Set-AdfsWebTheme -TargetName default -Logo @{path="c:\Contoso\logo.PNG"}

> [!NOTE]
> <span data-ttu-id="070d9-231">Merhaba *TargetName* parametresi gereklidir.</span><span class="sxs-lookup"><span data-stu-id="070d9-231">hello *TargetName* parameter is required.</span></span> <span data-ttu-id="070d9-232">AD FS ile yayımlanan hello varsayılan tema varsayılan olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="070d9-232">hello default theme that's released with AD FS is named Default.</span></span>

## <span data-ttu-id="070d9-233">Bir oturum açma açıklama ekleme<a name=addsignindescription></a></span><span class="sxs-lookup"><span data-stu-id="070d9-233">Add a sign-in description <a name=addsignindescription></a></span></span>
<span data-ttu-id="070d9-234">bir oturum açma sayfası açıklaması toohello tooadd **oturum açma sayfası**, Windows PowerShell cmdlet'ini ve sözdizimini aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="070d9-234">tooadd a sign-in page description toohello **Sign-in page**, use hello following Windows PowerShell cmdlet and syntax.</span></span>

    Set-AdfsGlobalWebContent -SignInPageDescriptionText "<p>Sign-in tooContoso requires device registration. Click <A href='http://fs1.contoso.com/deviceregistration/'>here</A> for more information.</p>"

## <span data-ttu-id="070d9-235">AD FS talep kuralları değiştirme<a name=modclaims></a></span><span class="sxs-lookup"><span data-stu-id="070d9-235">Modify AD FS claim rules <a name=modclaims></a></span></span>
<span data-ttu-id="070d9-236">AD FS kullanabileceğiniz bir zengin talep dili destekler toocreate özel talep kuralları.</span><span class="sxs-lookup"><span data-stu-id="070d9-236">AD FS supports a rich claim language that you can use toocreate custom claim rules.</span></span> <span data-ttu-id="070d9-237">Daha fazla bilgi için bkz: [hello talep kuralı dili rolü hello](https://technet.microsoft.com/library/dd807118.aspx).</span><span class="sxs-lookup"><span data-stu-id="070d9-237">For more information, see [hello Role of hello Claim Rule Language](https://technet.microsoft.com/library/dd807118.aspx).</span></span>

<span data-ttu-id="070d9-238">Merhaba aşağıdaki bölümlerde tooAzure AD ve AD FS federasyon ile ilgili bazı senaryolar için özel kurallar nasıl yazabilirsiniz açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="070d9-238">hello following sections describe how you can write custom rules for some scenarios that relate tooAzure AD and AD FS federation.</span></span>

### <a name="immutable-id-conditional-on-a-value-being-present-in-hello-attribute"></a><span data-ttu-id="070d9-239">Merhaba özniteliğinde bulunmasına değere koşullu bir sabit kimlik</span><span class="sxs-lookup"><span data-stu-id="070d9-239">Immutable ID conditional on a value being present in hello attribute</span></span>
<span data-ttu-id="070d9-240">Azure AD Connect nesneleri olduğunda kaynak bağlantısı tooAzure AD eşitlenmiş olarak kullanılan bir özniteliği toobe belirtmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="070d9-240">Azure AD Connect lets you specify an attribute toobe used as a source anchor when objects are synced tooAzure AD.</span></span> <span data-ttu-id="070d9-241">Merhaba değer hello özel öznitelik boş değilse, tooissue bir değişmez kimliği talebi isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="070d9-241">If hello value in hello custom attribute is not empty, you might want tooissue an immutable ID claim.</span></span>

<span data-ttu-id="070d9-242">Örneğin, seçebilirsiniz **ms ds consistencyguid** hello kaynak bağlantısı ve sorunu hello özniteliği olarak **İmmutableıd** olarak **ms ds consistencyguid** içindeki case hello öznitelik karşısında bir değer içeriyor.</span><span class="sxs-lookup"><span data-stu-id="070d9-242">For example, you might select **ms-ds-consistencyguid** as hello attribute for hello source anchor and issue **ImmutableID** as **ms-ds-consistencyguid** in case hello attribute has a value against it.</span></span> <span data-ttu-id="070d9-243">Merhaba özniteliği karşı değer yoksa, sorunu **objectGUID** değişmez kimliği hello gibi</span><span class="sxs-lookup"><span data-stu-id="070d9-243">If there's no value against hello attribute, issue **objectGuid** as hello immutable ID.</span></span> <span data-ttu-id="070d9-244">Bölümden hello açıklandığı gibi hello özel talep kuralları kümesi oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="070d9-244">You can construct hello set of custom claim rules as described in hello following section.</span></span>

<span data-ttu-id="070d9-245">**Kural 1: Sorgu öznitelikleri**</span><span class="sxs-lookup"><span data-stu-id="070d9-245">**Rule 1: Query attributes**</span></span>

    c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"]
    => add(store = "Active Directory", types = ("http://contoso.com/ws/2016/02/identity/claims/objectguid", "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"), query = "; objectGuid,ms-ds-consistencyguid;{0}", param = c.Value);

<span data-ttu-id="070d9-246">Bu kuralda hello değerlerini sorgulama **ms ds consistencyguid** ve **objectGUID** Active Directory'den hello kullanıcı için.</span><span class="sxs-lookup"><span data-stu-id="070d9-246">In this rule, you're querying hello values of **ms-ds-consistencyguid** and **objectGuid** for hello user from Active Directory.</span></span> <span data-ttu-id="070d9-247">Merhaba deposu tooan uygun depolama adı, AD FS dağıtımında değiştirin.</span><span class="sxs-lookup"><span data-stu-id="070d9-247">Change hello store name tooan appropriate store name in your AD FS deployment.</span></span> <span data-ttu-id="070d9-248">Ayrıca hello talep tooa uygun talep türü, Federasyon için tanımlanan değiştirme **objectGUID** ve **ms ds consistencyguid**.</span><span class="sxs-lookup"><span data-stu-id="070d9-248">Also change hello claims type tooa proper claims type for your federation, as defined for **objectGuid** and **ms-ds-consistencyguid**.</span></span>

<span data-ttu-id="070d9-249">Kullanarak Ayrıca, **ekleme** ve **sorunu**, hello varlık için giden sorun eklemekten kaçının ve başlangıç değerleri Ara değer olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="070d9-249">Also, by using **add** and not **issue**, you avoid adding an outgoing issue for hello entity, and can use hello values as intermediate values.</span></span> <span data-ttu-id="070d9-250">Hangi değer toouse değişmez kimliği hello gibi kurduktan sonra bir sonraki kuralında hello talep verecek</span><span class="sxs-lookup"><span data-stu-id="070d9-250">You will issue hello claim in a later rule after you establish which value toouse as hello immutable ID.</span></span>

<span data-ttu-id="070d9-251">**Kural 2: ms ds consistencyguid hello kullanıcısı için olup olmadığını kontrol edin.**</span><span class="sxs-lookup"><span data-stu-id="070d9-251">**Rule 2: Check if ms-ds-consistencyguid exists for hello user**</span></span>

    NOT EXISTS([Type == "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"])
    => add(Type = "urn:anandmsft:tmp/idflag", Value = "useguid");

<span data-ttu-id="070d9-252">Bu kural adlı geçici bir bayrak tanımlar **idflag** ayarlanan çok**useguid** yoksa hiçbir **ms ds consistencyguid** hello kullanıcı için doldurulur.</span><span class="sxs-lookup"><span data-stu-id="070d9-252">This rule defines a temporary flag called **idflag** that is set too**useguid** if there's no **ms-ds-consistencyguid** populated for hello user.</span></span> <span data-ttu-id="070d9-253">Bu arkasındaki Hello mantığı, AD FS boş talep izin vermeyen hello gerçeğidir.</span><span class="sxs-lookup"><span data-stu-id="070d9-253">hello logic behind this is hello fact that AD FS doesn't allow empty claims.</span></span> <span data-ttu-id="070d9-254">Kural 1'de talep http://contoso.com/ws/2016/02/identity/claims/objectguid ve http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid eklediğinizde, şunun için bir **msdsconsistencyguid** talep eksikse Merhaba değeri hello kullanıcı için doldurulur.</span><span class="sxs-lookup"><span data-stu-id="070d9-254">So when you add claims http://contoso.com/ws/2016/02/identity/claims/objectguid and http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid in Rule 1, you end up with an **msdsconsistencyguid** claim only if hello value is populated for hello user.</span></span> <span data-ttu-id="070d9-255">Doldurulmuş değil, AD FS boş değere sahip olur ve hemen bırakır görür.</span><span class="sxs-lookup"><span data-stu-id="070d9-255">If it isn't populated, AD FS sees that it will have an empty value and drops it immediately.</span></span> <span data-ttu-id="070d9-256">Tüm nesneler sahip **objectGUID**, kural 1 yürütüldükten sonra bu talep böylece her zaman vardır olur.</span><span class="sxs-lookup"><span data-stu-id="070d9-256">All objects will have **objectGuid**, so that claim will always be there after Rule 1 is executed.</span></span>

<span data-ttu-id="070d9-257">**3. kural: varsa, ms ds consistencyguid değişmez kimliği olarak verme**</span><span class="sxs-lookup"><span data-stu-id="070d9-257">**Rule 3: Issue ms-ds-consistencyguid as immutable ID if it's present**</span></span>

    c:[Type == "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"]
    => issue(Type = "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier", Value = c.Value);

<span data-ttu-id="070d9-258">Örtülü budur **mevcut** denetleyin.</span><span class="sxs-lookup"><span data-stu-id="070d9-258">This is an implicit **Exist** check.</span></span> <span data-ttu-id="070d9-259">Hello talep için başlangıç değeri varsa, daha sonra değişmez hello kimliği sorun</span><span class="sxs-lookup"><span data-stu-id="070d9-259">If hello value for hello claim exists, then issue that as hello immutable ID.</span></span> <span data-ttu-id="070d9-260">Merhaba önceki örnek kullanır hello **NameIdentifier** talep.</span><span class="sxs-lookup"><span data-stu-id="070d9-260">hello previous example uses hello **nameidentifier** claim.</span></span> <span data-ttu-id="070d9-261">Ortamınızda hello değişmez kimliği için bu toohello uygun talep türü toochange gerekir.</span><span class="sxs-lookup"><span data-stu-id="070d9-261">You'll have toochange this toohello appropriate claim type for hello immutable ID in your environment.</span></span>

<span data-ttu-id="070d9-262">**Kural 4: ms ds consistencyGuid mevcut değilse objectGUID değişmez kimliği olarak verme**</span><span class="sxs-lookup"><span data-stu-id="070d9-262">**Rule 4: Issue objectGuid as immutable ID if ms-ds-consistencyGuid is not present**</span></span>

    c1:[Type == "urn:anandmsft:tmp/idflag", Value =~ "useguid"]
    && c2:[Type == "http://contoso.com/ws/2016/02/identity/claims/objectguid"]
    => issue(Type = "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier", Value = c2.Value);

<span data-ttu-id="070d9-263">Bu kuralda, yalnızca hello geçici bayrağı denetimi **idflag**.</span><span class="sxs-lookup"><span data-stu-id="070d9-263">In this rule, you're simply checking hello temporary flag **idflag**.</span></span> <span data-ttu-id="070d9-264">Tooissue hello talep tabanlı olup olmadığını karar değerini üzerinde.</span><span class="sxs-lookup"><span data-stu-id="070d9-264">You decide whether tooissue hello claim based on its value.</span></span>

> [!NOTE]
> <span data-ttu-id="070d9-265">Bu kurallar Hello sırası önemlidir.</span><span class="sxs-lookup"><span data-stu-id="070d9-265">hello sequence of these rules is important.</span></span>

### <a name="sso-with-a-subdomain-upn"></a><span data-ttu-id="070d9-266">Bir alt etki alanı UPN SSO'su</span><span class="sxs-lookup"><span data-stu-id="070d9-266">SSO with a subdomain UPN</span></span>
<span data-ttu-id="070d9-267">Azure AD Connect kullanarak açıklandığı gibi Federasyon birden fazla etki alanı toobe ekleyebilirsiniz [yeni bir Federasyon etki alanına eklemek](active-directory-aadconnect-federation-management.md#addfeddomain).</span><span class="sxs-lookup"><span data-stu-id="070d9-267">You can add more than one domain toobe federated by using Azure AD Connect, as described in [Add a new federated domain](active-directory-aadconnect-federation-management.md#addfeddomain).</span></span> <span data-ttu-id="070d9-268">Böylece Hello verenin kimliği toohello kök etki alanı ve değil hello alt etki alanı, karşılık gelen hello Federasyon kök etki alanı da hello alt kapsar çünkü hello kullanıcı asıl adı (UPN) talebi değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="070d9-268">You must modify hello user principal name (UPN) claim so that hello issuer ID corresponds toohello root domain and not hello subdomain, because hello federated root domain also covers hello child.</span></span>

<span data-ttu-id="070d9-269">Varsayılan olarak, hello talep kuralı verenin Kimliğini olarak ayarlamak için:</span><span class="sxs-lookup"><span data-stu-id="070d9-269">By default, hello claim rule for issuer ID is set as:</span></span>

    c:[Type
    == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(c.Value, “.+@(?<domain>.+)“, “http://${domain}/adfs/services/trust/“));

![Varsayılan veren kimliği talebi](media/active-directory-aadconnect-federation-management/issuer_id_default.png)

<span data-ttu-id="070d9-271">Merhaba varsayılan kuralı yalnızca hello UPN sonekini alır ve hello veren kimliği talebi kullanır.</span><span class="sxs-lookup"><span data-stu-id="070d9-271">hello default rule simply takes hello UPN suffix and uses it in hello issuer ID claim.</span></span> <span data-ttu-id="070d9-272">Örneğin, John sub.contoso.com içinde bir kullanıcıdır ve contoso.com Azure AD ile birleştirildiyse.</span><span class="sxs-lookup"><span data-stu-id="070d9-272">For example, John is a user in sub.contoso.com, and contoso.com is federated with Azure AD.</span></span> <span data-ttu-id="070d9-273">John girer john@sub.contoso.com tooAzure AD imzalarken kullanıcıadı hello gibi.</span><span class="sxs-lookup"><span data-stu-id="070d9-273">John enters john@sub.contoso.com as hello username while signing in tooAzure AD.</span></span> <span data-ttu-id="070d9-274">Merhaba varsayılan veren kimliği talep kuralı AD FS'de, aşağıdaki şekilde hello işleme:</span><span class="sxs-lookup"><span data-stu-id="070d9-274">hello default issuer ID claim rule in AD FS handles it in hello following manner:</span></span>

    c:[Type
    == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(john@sub.contoso.com, “.+@(?<domain>.+)“, “http://${domain}/adfs/services/trust/“));

<span data-ttu-id="070d9-275">**Talep değeri:** http://sub.contoso.com/adfs/services/trust/</span><span class="sxs-lookup"><span data-stu-id="070d9-275">**Claim value:**  http://sub.contoso.com/adfs/services/trust/</span></span>

<span data-ttu-id="070d9-276">toohave yalnızca hello kök etki alanında hello verenin talep değeri, hello talep kuralı toomatch hello şu değiştirin:</span><span class="sxs-lookup"><span data-stu-id="070d9-276">toohave only hello root domain in hello issuer claim value, change hello claim rule toomatch hello following:</span></span>

    c:[Type == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(c.Value, “^((.*)([.|@]))?(?<domain>[^.]*[.].*)$”, “http://${domain}/adfs/services/trust/“));

## <a name="next-steps"></a><span data-ttu-id="070d9-277">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="070d9-277">Next steps</span></span>
<span data-ttu-id="070d9-278">Daha fazla bilgi edinmek [kullanıcı oturum açma seçenekleri](active-directory-aadconnect-user-signin.md).</span><span class="sxs-lookup"><span data-stu-id="070d9-278">Learn more about [user sign-in options](active-directory-aadconnect-user-signin.md).</span></span>
