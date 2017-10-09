---
title: aaaGet verileri kullanarak Azure AD raporlama API'si sertifikalarla hello | Microsoft Docs
description: "Nasıl toouse hello Azure AD raporlama API'si ile sertifika kimlik bilgileri tooget verileri kullanıcı müdahalesi olmadan dizinlerinden açıklanmaktadır."
services: active-directory
documentationcenter: 
author: ramical
writer: v-lorisc
manager: kannar
ms.assetid: 
ms.service: active-directory
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/24/2017
ms.author: ramical
ms.openlocfilehash: 00ddfaefe32ea6ae48f276c974a17ddcf84f7894
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-data-using-hello-azure-ad-reporting-api-with-certificates"></a><span data-ttu-id="c00fc-103">Hello Azure AD raporlama API'si ile sertifika kullanımı Veri Al</span><span class="sxs-lookup"><span data-stu-id="c00fc-103">Get data using hello Azure AD Reporting API with certificates</span></span>
<span data-ttu-id="c00fc-104">Bu makalede nasıl toouse hello Azure AD raporlama API'si ile sertifika kimlik bilgileri tooget verileri kullanıcı müdahalesi olmadan dizinlerinden anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="c00fc-104">This article discusses how toouse hello Azure AD Reporting API with certificate credentials tooget data from directories without user intervention.</span></span> 

## <a name="use-hello-azure-ad-reporting-api"></a><span data-ttu-id="c00fc-105">Kullanım hello Azure AD raporlama API'si</span><span class="sxs-lookup"><span data-stu-id="c00fc-105">Use hello Azure AD Reporting API</span></span> 
<span data-ttu-id="c00fc-106">Azure AD raporlama API'si hello aşağıdaki adımları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="c00fc-106">Azure AD Reporting API requires that you complete hello following steps:</span></span>
 *  <span data-ttu-id="c00fc-107">Ön koşulları yükleme</span><span class="sxs-lookup"><span data-stu-id="c00fc-107">Install prerequisites</span></span>
 *  <span data-ttu-id="c00fc-108">Uygulamanızda hello sertifikayı ayarlayın</span><span class="sxs-lookup"><span data-stu-id="c00fc-108">Set hello certificate in your app</span></span>
 *  <span data-ttu-id="c00fc-109">Bir erişim belirteci alma</span><span class="sxs-lookup"><span data-stu-id="c00fc-109">Get an access token</span></span>
 *  <span data-ttu-id="c00fc-110">Merhaba erişim belirteci toocall hello grafik API'sini kullanın</span><span class="sxs-lookup"><span data-stu-id="c00fc-110">Use hello access token toocall hello Graph API</span></span>

<span data-ttu-id="c00fc-111">Kaynak kodu hakkında bilgi için bkz. [Rapor API Modülünden Yararlanma](https://github.com/AzureAD/azure-activedirectory-powershell/tree/gh-pages/Modules/AzureADUtils).</span><span class="sxs-lookup"><span data-stu-id="c00fc-111">For information about source code, see [Leverage Report API Module](https://github.com/AzureAD/azure-activedirectory-powershell/tree/gh-pages/Modules/AzureADUtils).</span></span> 

### <a name="install-prerequisites"></a><span data-ttu-id="c00fc-112">Ön koşulları yükleme</span><span class="sxs-lookup"><span data-stu-id="c00fc-112">Install prerequisites</span></span>
<span data-ttu-id="c00fc-113">Azure AD PowerShell V2 toohave ve AzureADUtils modül yüklü gerekir.</span><span class="sxs-lookup"><span data-stu-id="c00fc-113">You will need toohave Azure AD PowerShell V2 and AzureADUtils module installed.</span></span>

1. <span data-ttu-id="c00fc-114">Azure AD Powershell V2 hello yönergeleri izleyerek, karşıdan yüklenip [Azure Active Directory PowerShell](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure AD Cmdlets/AzureAD/index.md).</span><span class="sxs-lookup"><span data-stu-id="c00fc-114">Download and install Azure AD Powershell V2, following hello instructions at [Azure Active Directory PowerShell](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure AD Cmdlets/AzureAD/index.md).</span></span>
2. <span data-ttu-id="c00fc-115">Hello Azure AD yardımcı programları modülünden karşıdan [Azuread'i/azure-Active Directory-powershell](https://github.com/AzureAD/azure-activedirectory-powershell/blob/gh-pages/Modules/AzureADUtils/AzureADUtils.psm1).</span><span class="sxs-lookup"><span data-stu-id="c00fc-115">Download hello Azure AD Utils module from [AzureAD/azure-activedirectory-powershell](https://github.com/AzureAD/azure-activedirectory-powershell/blob/gh-pages/Modules/AzureADUtils/AzureADUtils.psm1).</span></span> 
  <span data-ttu-id="c00fc-116">Bu modül aşağıdaki çeşitli yardımcı program cmdlet'lerini sağlar:</span><span class="sxs-lookup"><span data-stu-id="c00fc-116">This module provides several utility cmdlets including:</span></span>
   * <span data-ttu-id="c00fc-117">Nuget kullanarak ADAL Hello en son sürümü</span><span class="sxs-lookup"><span data-stu-id="c00fc-117">hello latest version of ADAL using Nuget</span></span>
   * <span data-ttu-id="c00fc-118">ADAL kullanarak kullanıcı, uygulama anahtarları ve sertifikalardan erişim belirteçleri</span><span class="sxs-lookup"><span data-stu-id="c00fc-118">Access tokens from user, application keys, and certificates using ADAL</span></span>
   * <span data-ttu-id="c00fc-119">Disk belleğine alınmış Grafik API'si işleme sonuçları</span><span class="sxs-lookup"><span data-stu-id="c00fc-119">Graph API handling paged results</span></span>

<span data-ttu-id="c00fc-120">**tooinstall hello Azure AD yardımcı programları Modülü:**</span><span class="sxs-lookup"><span data-stu-id="c00fc-120">**tooinstall hello Azure AD Utils module:**</span></span>

1. <span data-ttu-id="c00fc-121">Bir dizin toosave hello yardımcı programları modül (örneğin, c:\azureAD) oluşturun ve hello modül Github'dan yükleyin.</span><span class="sxs-lookup"><span data-stu-id="c00fc-121">Create a directory toosave hello utilities module (for example, c:\azureAD) and download hello module from GitHub.</span></span>
2. <span data-ttu-id="c00fc-122">Bir PowerShell oturumu açın ve yeni oluşturduğunuz toohello dizinine gidin.</span><span class="sxs-lookup"><span data-stu-id="c00fc-122">Open a PowerShell session, and go toohello directory you just created.</span></span> 
3. <span data-ttu-id="c00fc-123">Merhaba modülünü içeri aktarın ve hello yükleme AzureADUtilsModule cmdlet'ini kullanarak hello PowerShell modülü yolunda yükleyin.</span><span class="sxs-lookup"><span data-stu-id="c00fc-123">Import hello module, and install it in hello PowerShell module path using hello Install-AzureADUtilsModule cmdlet.</span></span> 

<span data-ttu-id="c00fc-124">Merhaba oturum toothis ekran benzer görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="c00fc-124">hello session should look similar toothis screen:</span></span>

  ![Windows PowerShell](./media/active-directory-report-api-with-certificates/windows-powershell.png)

### <a name="set-hello-certificate-in-your-app"></a><span data-ttu-id="c00fc-126">Uygulamanızda hello sertifikayı ayarlayın</span><span class="sxs-lookup"><span data-stu-id="c00fc-126">Set hello certificate in your app</span></span>
1. <span data-ttu-id="c00fc-127">Bir uygulama zaten varsa, nesne kimliği hello Azure Portal ' alın.</span><span class="sxs-lookup"><span data-stu-id="c00fc-127">If you already have an app, get its Object ID from hello Azure Portal.</span></span> 

  ![Azure portalına](./media/active-directory-report-api-with-certificates/azure-portal.png)

2. <span data-ttu-id="c00fc-129">Bir PowerShell oturumu açın ve tooAzure AD connect hello Connect-Azuread'i cmdlet'ini kullanarak.</span><span class="sxs-lookup"><span data-stu-id="c00fc-129">Open a PowerShell session and connect tooAzure AD using hello Connect-AzureAD cmdlet.</span></span>

  ![Azure portalına](./media/active-directory-report-api-with-certificates/connect-azuaread-cmdlet.png)

3. <span data-ttu-id="c00fc-131">Sertifika kimlik bilgisi tooit AzureADUtils tooadd'ndan Hello yeni AzureADApplicationCertificateCredential cmdlet'ini kullanın.</span><span class="sxs-lookup"><span data-stu-id="c00fc-131">Use hello New-AzureADApplicationCertificateCredential cmdlet from AzureADUtils tooadd a certificate credential tooit.</span></span> 

>[!Note]
><span data-ttu-id="c00fc-132">Tooprovide hello uygulama, daha önce yakalanan bir nesne kimliği gerekir yanı sıra hello sertifika nesnesi (kullanarak bu almak sertifika hello: sürücü).</span><span class="sxs-lookup"><span data-stu-id="c00fc-132">You need tooprovide hello application Object ID that you captured earlier, as well as hello certificate object (get this using hello Cert: drive).</span></span>
>


  ![Azure portalına](./media/active-directory-report-api-with-certificates/add-certificate-credential.png)
  
### <a name="get-an-access-token"></a><span data-ttu-id="c00fc-134">Bir erişim belirteci alma</span><span class="sxs-lookup"><span data-stu-id="c00fc-134">Get an access token</span></span>

<span data-ttu-id="c00fc-135">tooget bir erişim belirteci AzureADUtils'ndan hello Get-AzureADGraphAPIAccessTokenFromCert cmdlet'ini kullanın.</span><span class="sxs-lookup"><span data-stu-id="c00fc-135">tooget an access token, use hello Get-AzureADGraphAPIAccessTokenFromCert cmdlet from AzureADUtils.</span></span> 

>[!NOTE]
><span data-ttu-id="c00fc-136">Merhaba hello son bölümünde kullanılan nesne kimliği yerine toouse hello uygulama kimliği gerekir.</span><span class="sxs-lookup"><span data-stu-id="c00fc-136">You need toouse hello Application ID instead of hello Object ID that you used in hello last section.</span></span>
>

 ![Azure portalına](./media/active-directory-report-api-with-certificates/application-id.png)

### <a name="use-hello-access-token-toocall-hello-graph-api"></a><span data-ttu-id="c00fc-138">Merhaba erişim belirteci toocall hello grafik API'sini kullanın</span><span class="sxs-lookup"><span data-stu-id="c00fc-138">Use hello access token toocall hello Graph API</span></span>

<span data-ttu-id="c00fc-139">Şimdi hello komut dosyası oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c00fc-139">Now you can create hello script.</span></span> <span data-ttu-id="c00fc-140">Aşağıda hello AzureADUtils'ndan hello Invoke-AzureADGraphAPIQuery cmdlet'ini kullanarak bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="c00fc-140">Below is an example using hello Invoke-AzureADGraphAPIQuery cmdlet from hello AzureADUtils.</span></span> <span data-ttu-id="c00fc-141">Bu cmdlet birden çok disk belleğine alınmış sonuçlar işler ve daha sonra bu sonuçlar toohello PowerShell komut zincirini gönderir.</span><span class="sxs-lookup"><span data-stu-id="c00fc-141">This cmdlet handles multi-paged results, and then sends those results toohello PowerShell pipeline.</span></span> 

 ![Azure portalına](./media/active-directory-report-api-with-certificates/script-completed.png)

<span data-ttu-id="c00fc-143">Hazır tooexport tooa CSV sunulmuştur ve tooa SIEM sisteminde kaydedin.</span><span class="sxs-lookup"><span data-stu-id="c00fc-143">You are now ready tooexport tooa CSV and save tooa SIEM system.</span></span> <span data-ttu-id="c00fc-144">Ayrıca kodunuzu bir zamanlanmış görev tooget Azure AD veri kiracınız düzenli aralıklarla hello kaynak kodunda toostore uygulama anahtarları gerekmeden kayabilir.</span><span class="sxs-lookup"><span data-stu-id="c00fc-144">You can also wrap your script in a scheduled task tooget Azure AD data from your tenant periodically without having toostore application keys in hello source code.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c00fc-145">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c00fc-145">Next steps</span></span>
[<span data-ttu-id="c00fc-146">Azure Kimlik Yönetimi Hello temelleri</span><span class="sxs-lookup"><span data-stu-id="c00fc-146">hello fundamentals of Azure identity management</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/fundamentals-identity)<br>



