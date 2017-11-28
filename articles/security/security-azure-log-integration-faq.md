---
title: "aaaAzure günlük tümleştirme SSS | Microsoft Docs"
description: "Bu makalede Azure günlük tümleştirmesi hakkında sorular yanıtlanmaktadır."
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TerryLanfear
ms.assetid: d06d1ac5-5c3b-49de-800e-4d54b3064c64
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload8: na
ms.date: 08/07/2017
ms.author: TomSh
ms.custom: azlog
ms.openlocfilehash: e886035c9a180d0cd5fcbe9cc02483782df6dbe4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-log-integration-faq"></a><span data-ttu-id="acf23-103">Azure günlük tümleştirme hakkında SSS</span><span class="sxs-lookup"><span data-stu-id="acf23-103">Azure Log Integration FAQ</span></span>
<span data-ttu-id="acf23-104">Bu makalede Azure günlük tümleştirmesi hakkında sık sorulan sorular (SSS) yanıtlar.</span><span class="sxs-lookup"><span data-stu-id="acf23-104">This article answers frequently asked questions (FAQ) about Azure Log Integration.</span></span> 

<span data-ttu-id="acf23-105">Azure günlük tümleştirme toointegrate ham günlükleri, şirket içi güvenlik bilgileri ve Olay yönetimi (SIEM) sistemlere Azure kaynaklarınızdan kullanabilirsiniz bir Windows işletim sistemi hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="acf23-105">Azure Log Integration is a Windows operating system service that you can use toointegrate raw logs from your Azure resources into your on-premises security information and event management (SIEM) systems.</span></span> <span data-ttu-id="acf23-106">Bu tümleştirme, tüm varlıklarınızı, şirket içi veya hello bulutta birleştirilmiş bir Pano sağlar.</span><span class="sxs-lookup"><span data-stu-id="acf23-106">This integration provides a unified dashboard for all your assets, on-premises or in hello cloud.</span></span> <span data-ttu-id="acf23-107">Ardından toplama, bağıntılı, çözümleyebilir ve uygulamalarınız ile ilişkili güvenlik olayları için uyarı.</span><span class="sxs-lookup"><span data-stu-id="acf23-107">You can then aggregate, correlate, analyze, and alert for security events associated with your applications.</span></span>

## <a name="is-hello-azure-log-integration-software-free"></a><span data-ttu-id="acf23-108">Hello Azure günlük tümleştirme yazılım ücretsiz mi?</span><span class="sxs-lookup"><span data-stu-id="acf23-108">Is hello Azure Log Integration software free?</span></span>
<span data-ttu-id="acf23-109">Evet.</span><span class="sxs-lookup"><span data-stu-id="acf23-109">Yes.</span></span> <span data-ttu-id="acf23-110">Hello Azure günlük tümleştirme yazılımı için ücret ödemeden yoktur.</span><span class="sxs-lookup"><span data-stu-id="acf23-110">There is no charge for hello Azure Log Integration software.</span></span>

## <a name="where-is-azure-log-integration-available"></a><span data-ttu-id="acf23-111">Burada Azure günlük tümleştirmesi var mı?</span><span class="sxs-lookup"><span data-stu-id="acf23-111">Where is Azure Log Integration available?</span></span>

<span data-ttu-id="acf23-112">Azure ticari ve Azure kamu şu anda kullanılabilir değil ve Çin veya Almanya kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="acf23-112">It is currently available in Azure Commercial and Azure Government and is not available in China or Germany.</span></span>

## <a name="how-can-i-see-hello-storage-accounts-from-which-azure-log-integration-is-pulling-azure-vm-logs"></a><span data-ttu-id="acf23-113">Merhaba depolama hesaplarını Azure günlük tümleştirme Azure VM günlükleri çekme nasıl görebilirim?</span><span class="sxs-lookup"><span data-stu-id="acf23-113">How can I see hello storage accounts from which Azure Log Integration is pulling Azure VM logs?</span></span>
<span data-ttu-id="acf23-114">Merhaba komutu çalıştırmak **azlog kaynağı listesi**.</span><span class="sxs-lookup"><span data-stu-id="acf23-114">Run hello command **azlog source list**.</span></span>

## <a name="how-can-i-tell-which-subscription-hello-azure-log-integration-logs-are-from"></a><span data-ttu-id="acf23-115">Hangi abonelik hello günlükleri arasındadır Azure günlük tümleştirme nasıl anlayabilirim?</span><span class="sxs-lookup"><span data-stu-id="acf23-115">How can I tell which subscription hello Azure Log Integration logs are from?</span></span>

<span data-ttu-id="acf23-116">Hello yerleştirilir denetim günlüklerinin hello durumda **AzureResourcemanagerJson** dizinleri hello abonelik kimliği: hello günlük dosyası adı.</span><span class="sxs-lookup"><span data-stu-id="acf23-116">In hello case of audit logs that are placed in hello **AzureResourcemanagerJson** directories, hello subscription ID is in hello log file name.</span></span> <span data-ttu-id="acf23-117">Bu, aynı zamanda hello günlükleri için geçerlidir **AzureSecurityCenterJson** klasör.</span><span class="sxs-lookup"><span data-stu-id="acf23-117">This is also true for logs in hello **AzureSecurityCenterJson** folder.</span></span> <span data-ttu-id="acf23-118">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="acf23-118">For example:</span></span>

<span data-ttu-id="acf23-119">20170407T070805_2768037.0000000023. **1111e5ee-1111-111b-a11e-1e111e1111dc**.json</span><span class="sxs-lookup"><span data-stu-id="acf23-119">20170407T070805_2768037.0000000023.**1111e5ee-1111-111b-a11e-1e111e1111dc**.json</span></span>

<span data-ttu-id="acf23-120">Azure Active Directory denetim günlüklerini hello Kiracı kimliği hello adının bir parçası olarak içerir.</span><span class="sxs-lookup"><span data-stu-id="acf23-120">Azure Active Directory audit logs include hello tenant ID as part of hello name.</span></span>

<span data-ttu-id="acf23-121">Bir olay hub'ından okuma tanılama günlüklerini hello abonelik kimliği hello adının bir parçası olarak dahil etmeyin.</span><span class="sxs-lookup"><span data-stu-id="acf23-121">Diagnostic logs that are read from an event hub do not include hello subscription ID as part of hello name.</span></span> <span data-ttu-id="acf23-122">Bunun yerine, hello kolay ad hello kaynağı oluşturma işlemi hello olay hub'ı bir parçası olarak belirtilen içerirler.</span><span class="sxs-lookup"><span data-stu-id="acf23-122">Instead, they include hello friendly name specified as part of hello creation of hello event hub source.</span></span> 

## <a name="how-can-i-update-hello-proxy-configuration"></a><span data-ttu-id="acf23-123">Merhaba proxy yapılandırmasını nasıl güncelleştirebilir miyim?</span><span class="sxs-lookup"><span data-stu-id="acf23-123">How can I update hello proxy configuration?</span></span>
<span data-ttu-id="acf23-124">Proxy ayarı Azure depolama erişime doğrudan izin vermiyorsa, hello açmak **AZLOG. EXE. CONFIG** dosyasını **c:\Program Files\Microsoft Azure günlük tümleştirme**.</span><span class="sxs-lookup"><span data-stu-id="acf23-124">If your proxy setting does not allow Azure storage access directly, open hello **AZLOG.EXE.CONFIG** file in **c:\Program Files\Microsoft Azure Log Integration**.</span></span> <span data-ttu-id="acf23-125">Güncelleştirme hello dosya tooinclude hello **defaultProxy** hello proxy adresine sahip bir bölüm, kuruluşunuzun.</span><span class="sxs-lookup"><span data-stu-id="acf23-125">Update hello file tooinclude hello **defaultProxy** section with hello proxy address of your organization.</span></span> <span data-ttu-id="acf23-126">Merhaba güncelleştirme yapıldıktan sonra durdurmak ve hello komutlarını kullanarak hello hizmeti başlatmak **net stop azlog** ve **net Başlat azlog**.</span><span class="sxs-lookup"><span data-stu-id="acf23-126">After hello update is done, stop and start hello service by using hello commands **net stop azlog** and **net start azlog**.</span></span>

    <?xml version="1.0" encoding="utf-8"?>
    <configuration>
      <system.net>
        <connectionManagement>
          <add address="*" maxconnection="400" />
        </connectionManagement>
        <defaultProxy>
          <proxy usesystemdefault="true"
          proxyaddress=http://127.0.0.1:8888
          bypassonlocal="true" />
        </defaultProxy>
      </system.net>
      <system.diagnostics>
        <performanceCounters filemappingsize="20971520" />
      </system.diagnostics>   

## <a name="how-can-i-see-hello-subscription-information-in-windows-events"></a><span data-ttu-id="acf23-127">Windows olayları hello abonelik bilgileri nasıl görebilirim?</span><span class="sxs-lookup"><span data-stu-id="acf23-127">How can I see hello subscription information in Windows events?</span></span>
<span data-ttu-id="acf23-128">Merhaba abonelik kimliği toohello kolay adı hello kaynağı eklenirken ekleyin:</span><span class="sxs-lookup"><span data-stu-id="acf23-128">Append hello subscription ID toohello friendly name while adding hello source:</span></span>

    Azlog source add <sourcefriendlyname>.<subscription id> <StorageName> <StorageKey>  
<span data-ttu-id="acf23-129">Merhaba olay XML hello abonelik kimliği gibi meta veriler, aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="acf23-129">hello event XML has hello following metadata, including hello subscription ID:</span></span>

![Olay XML][1]

## <a name="error-messages"></a><span data-ttu-id="acf23-131">Hata iletileri</span><span class="sxs-lookup"><span data-stu-id="acf23-131">Error messages</span></span>
### <a name="when-i-run-hello-command-azlog-createazureid-why-do-i-get-hello-following-error"></a><span data-ttu-id="acf23-132">Merhaba komutu çalıştırdığınızda ı **azlog createazureid**, aşağıdaki hata hello neden alabilirim?</span><span class="sxs-lookup"><span data-stu-id="acf23-132">When I run hello command **azlog createazureid**, why do I get hello following error?</span></span>
<span data-ttu-id="acf23-133">Hata:</span><span class="sxs-lookup"><span data-stu-id="acf23-133">Error:</span></span>

  <span data-ttu-id="acf23-134">*Toocreate AAD uygulama - Kiracı 72f988bf-86f1-41af-91ab-2d7cd011db37 - neden başarısız = 'Yasak' - ileti 'yeterli ayrıcalığa sahip toocomplete hello işlemi' =*</span><span class="sxs-lookup"><span data-stu-id="acf23-134">*Failed toocreate AAD Application - Tenant 72f988bf-86f1-41af-91ab-2d7cd011db37 - Reason = 'Forbidden' - Message = 'Insufficient privileges toocomplete hello operation.'*</span></span>

<span data-ttu-id="acf23-135">Merhaba **azlog createazureid** komut çalışır toocreate Azure oturum açma hello hello abonelikler için tüm hello Azure AD kiracılar bir hizmet sorumlusu erişimi vardır.</span><span class="sxs-lookup"><span data-stu-id="acf23-135">hello **azlog createazureid** command attempts toocreate a service principal in all hello Azure AD tenants for hello subscriptions that hello Azure login has access to.</span></span> <span data-ttu-id="acf23-136">Azure oturum açma bilgilerinizi yalnızca Konuk kullanıcı olarak Azure AD Kiracı ise, "yeterli ayrıcalığa sahip toocomplete hello işlemiyle." Merhaba komutu başarısız</span><span class="sxs-lookup"><span data-stu-id="acf23-136">If your Azure login is only a guest user in that Azure AD tenant, hello command fails with "Insufficient privileges toocomplete hello operation."</span></span> <span data-ttu-id="acf23-137">Merhaba Kiracı yönetici tooadd isteyin hesabınız hello kiracısındaki bir kullanıcı olarak.</span><span class="sxs-lookup"><span data-stu-id="acf23-137">Ask hello tenant admin tooadd your account as a user in hello tenant.</span></span>

### <a name="when-i-run-hello-command-azlog-authorize-why-do-i-get-hello-following-error"></a><span data-ttu-id="acf23-138">Merhaba komutu çalıştırdığınızda ı **azlog yetkilendirmek**, aşağıdaki hata hello neden alabilirim?</span><span class="sxs-lookup"><span data-stu-id="acf23-138">When I run hello command **azlog authorize**, why do I get hello following error?</span></span>
<span data-ttu-id="acf23-139">Hata:</span><span class="sxs-lookup"><span data-stu-id="acf23-139">Error:</span></span>

  <span data-ttu-id="acf23-140">*Uyarı rol ataması - AuthorizationFailed oluşturma: hello istemci janedo@microsoft.com' olan nesne kimliği 'fe9e03e4-4dad-4328-910f-fd24a9660bd2' yetkilendirme tooperform eylemi 'Microsoft.Authorization/roleAssignments/write' kapsamı üzerinde yok ' / Abonelikleri / 70d 95299 d689 4c 97-b971-0d8ff0000000'.*</span><span class="sxs-lookup"><span data-stu-id="acf23-140">*Warning creating Role Assignment - AuthorizationFailed: hello client janedo@microsoft.com' with object id 'fe9e03e4-4dad-4328-910f-fd24a9660bd2' does not have authorization tooperform action 'Microsoft.Authorization/roleAssignments/write' over scope '/subscriptions/70d95299-d689-4c97-b971-0d8ff0000000'.*</span></span>

<span data-ttu-id="acf23-141">Merhaba **azlog yetkilendirmek** atar hello okuyucu toohello Azure AD hizmet sorumlusu rolü komutu (ile oluşturulan **azlog createazureid**) sağlanan toohello abonelikleri.</span><span class="sxs-lookup"><span data-stu-id="acf23-141">hello **azlog authorize** command assigns hello role of reader toohello Azure AD service principal (created with **azlog createazureid**) toohello provided subscriptions.</span></span> <span data-ttu-id="acf23-142">Hello Azure oturum açma bir ortak yönetici veya hello abonelik sahibi değilse, bir "Yetkilendirme başarısız oldu" hata iletisiyle başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="acf23-142">If hello Azure login is not a co-administrator or an owner of hello subscription, it fails with an "Authorization Failed" error message.</span></span> <span data-ttu-id="acf23-143">Azure rol tabanlı erişim denetimi (RBAC) ortak yönetici veya sahibi gerekli toocomplete bu eylemdir.</span><span class="sxs-lookup"><span data-stu-id="acf23-143">Azure Role-Based Access Control (RBAC) of co-administrator or owner is needed toocomplete this action.</span></span>

## <a name="where-can-i-find-hello-definition-of-hello-properties-in-hello-audit-log"></a><span data-ttu-id="acf23-144">Merhaba Denetim günlüğüne hello özellikleri hello tanımını nereden bulabilirim?</span><span class="sxs-lookup"><span data-stu-id="acf23-144">Where can I find hello definition of hello properties in hello audit log?</span></span>
<span data-ttu-id="acf23-145">Bkz.:</span><span class="sxs-lookup"><span data-stu-id="acf23-145">See:</span></span>

* [<span data-ttu-id="acf23-146">Azure Resource Manager ile işlemlerini denetleme</span><span class="sxs-lookup"><span data-stu-id="acf23-146">Audit operations with Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-audit.md)
* [<span data-ttu-id="acf23-147">Bir abonelikte hello Azure İzleyici REST API listesi hello yönetim olayları</span><span class="sxs-lookup"><span data-stu-id="acf23-147">List hello management events in a subscription in hello Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931934.aspx)

## <a name="where-can-i-find-details-on-azure-security-center-alerts"></a><span data-ttu-id="acf23-148">Azure Güvenlik Merkezi uyarılarını ayrıntıları nereden bulabilirim?</span><span class="sxs-lookup"><span data-stu-id="acf23-148">Where can I find details on Azure Security Center alerts?</span></span>
<span data-ttu-id="acf23-149">Bkz: [yönetme ve yanıt toosecurity Azure Güvenlik Merkezi'nde uyarıları](../security-center/security-center-managing-and-responding-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="acf23-149">See [Managing and responding toosecurity alerts in Azure Security Center](../security-center/security-center-managing-and-responding-alerts.md).</span></span>

## <a name="how-can-i-modify-what-is-collected-with-vm-diagnostics"></a><span data-ttu-id="acf23-150">Nasıl VM Tanılama ile toplanan değişiklik yapabilirsiniz?</span><span class="sxs-lookup"><span data-stu-id="acf23-150">How can I modify what is collected with VM diagnostics?</span></span>
<span data-ttu-id="acf23-151">Nasıl tooget, değiştirmek ve hello Azure tanılama yapılandırma hakkında ayrıntılar için bkz: [Windows çalıştıran bir sanal makinede kullan PowerShell tooenable Azure tanılama](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="acf23-151">For details on how tooget, modify, and set hello Azure Diagnostics configuration, see [Use PowerShell tooenable Azure Diagnostics in a virtual machine running Windows](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="acf23-152">Aşağıdaki örnek hello hello Azure Tanılama yapılandırmasını alır:</span><span class="sxs-lookup"><span data-stu-id="acf23-152">hello following example gets hello Azure Diagnostics configuration:</span></span>

    -AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient
    $publicsettings = (Get-AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient).PublicSettings
    $encodedconfig = (ConvertFrom-Json -InputObject $publicsettings).xmlCfg
    $xmlconfig = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($encodedconfig))
    Write-Host $xmlconfig

    $xmlconfig | Out-File -Encoding utf8 -FilePath "d:\WADConfig.xml"

<span data-ttu-id="acf23-153">Aşağıdaki örnek hello hello Azure Tanılama yapılandırmasını değiştirir.</span><span class="sxs-lookup"><span data-stu-id="acf23-153">hello following example modifies hello Azure Diagnostics configuration.</span></span> <span data-ttu-id="acf23-154">Bu yapılandırmada, yalnızca olay kimliği 4624 ve olay kimliği 4625 hello güvenlik olay günlüğü'nden toplanır.</span><span class="sxs-lookup"><span data-stu-id="acf23-154">In this configuration, only event ID 4624 and event ID 4625 are collected from hello security event log.</span></span> <span data-ttu-id="acf23-155">Azure olayları için Microsoft Antimalware hello sistem olay günlüğü'nden toplanır.</span><span class="sxs-lookup"><span data-stu-id="acf23-155">Microsoft Antimalware for Azure events are collected from hello system event log.</span></span> <span data-ttu-id="acf23-156">XPath ifadeleri hello kullanımı hakkında daha fazla bilgi için bkz: [tüketen olayları](https://msdn.microsoft.com/library/windows/desktop/dd996910(v=vs.85)).</span><span class="sxs-lookup"><span data-stu-id="acf23-156">For details on hello use of XPath expressions, see [Consuming Events](https://msdn.microsoft.com/library/windows/desktop/dd996910(v=vs.85)).</span></span>

    <WindowsEventLog scheduledTransferPeriod="PT1M">
        <DataSource name="Security!*[System[(EventID=4624 or EventID=4625)]]" />
        <DataSource name="System!*[System[Provider[@Name='Microsoft Antimalware']]]"/>
    </WindowsEventLog>

<span data-ttu-id="acf23-157">Merhaba aşağıdaki örnek hello Azure tanılama yapılandırması ayarlar:</span><span class="sxs-lookup"><span data-stu-id="acf23-157">hello following example sets hello Azure Diagnostics configuration:</span></span>

    $diagnosticsconfig_path = "d:\WADConfig.xml"
    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient -DiagnosticsConfigurationPath $diagnosticsconfig_path -StorageAccountName log3121 -StorageAccountKey <storage key>

<span data-ttu-id="acf23-158">Değişiklikleri yaptıktan sonra o hello olayları toplanan doğru hello depolama hesabı tooensure denetleyin.</span><span class="sxs-lookup"><span data-stu-id="acf23-158">After you make changes, check hello storage account tooensure that hello correct events are collected.</span></span>

<span data-ttu-id="acf23-159">Merhaba yükleme ve yapılandırma sırasında herhangi bir sorun varsa, lütfen açık bir [destek isteği](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request).</span><span class="sxs-lookup"><span data-stu-id="acf23-159">If you have any issues during hello installation and configuration, please open a [support request](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request).</span></span> <span data-ttu-id="acf23-160">Seçin **günlük tümleştirme** destek isteyen hello hizmet olarak.</span><span class="sxs-lookup"><span data-stu-id="acf23-160">Select **Log Integration** as hello service for which you are requesting support.</span></span>

## <a name="can-i-use-azure-log-integration-toointegrate-network-watcher-logs-into-my-siem"></a><span data-ttu-id="acf23-161">My SIEM Azure günlük tümleştirme toointegrate Ağ İzleyicisi günlüklerini kullanabilir miyim?</span><span class="sxs-lookup"><span data-stu-id="acf23-161">Can I use Azure Log Integration toointegrate Network Watcher logs into my SIEM?</span></span>

<span data-ttu-id="acf23-162">Azure Ağ İzleyicisi günlük bilgileri büyük miktarlarda oluşturur.</span><span class="sxs-lookup"><span data-stu-id="acf23-162">Azure Network Watcher generates large quantities of logging information.</span></span> <span data-ttu-id="acf23-163">Bu günlükler gönderilen yüksetlmesi toobe tooa SIEM olup olmadığı.</span><span class="sxs-lookup"><span data-stu-id="acf23-163">These logs are not meant toobe sent tooa SIEM.</span></span> <span data-ttu-id="acf23-164">yalnızca desteklenen hello hedef Ağ İzleyicisi günlükleri için bir depolama hesabıdır.</span><span class="sxs-lookup"><span data-stu-id="acf23-164">hello only supported destination for Network Watcher logs is a storage account.</span></span> <span data-ttu-id="acf23-165">Bu günlükler okuma ve kullanılabilir tooa SIEM yaparak Azure günlük tümleştirme desteklemez.</span><span class="sxs-lookup"><span data-stu-id="acf23-165">Azure Log Integration does not support reading these logs and making them available tooa SIEM.</span></span>

<!--Image references-->
[1]: ./media/security-azure-log-integration-faq/event-xml.png
