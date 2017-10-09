---
title: "aaaAzure tanılama 1.0 yapılandırma şeması | Microsoft Docs"
description: "YALNIZCA ilgili Azure SDK 2.4 kullanıyorsanız ve aşağıda Azure sanal makineler, sanal makine ölçek kümeleri, Service Fabric veya Bulut Hizmetleri ile."
services: monitoring-and-diagnostics
documentationcenter: .net
author: rboucher
manager: carmonm
editor: 
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/15/2017
ms.author: robb
ms.openlocfilehash: bdd2b26217d6ea28f19e651ab429e7e7401ff57b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-diagnostics-10-configuration-schema"></a><span data-ttu-id="f2713-103">Azure tanılama 1.0 yapılandırma şeması</span><span class="sxs-lookup"><span data-stu-id="f2713-103">Azure Diagnostics 1.0 Configuration Schema</span></span>
> [!NOTE]
> <span data-ttu-id="f2713-104">Azure tanılama hello kullanılan bileşen toocollect performans sayaçları ve diğer Azure sanal makineler, sanal makine ölçek kümeleri, Service Fabric ve Cloud Services istatistiklerine ' dir.</span><span class="sxs-lookup"><span data-stu-id="f2713-104">Azure Diagnostics is hello component used toocollect performance counters and other statistics from Azure Virtual Machines, Virtual Machine Scale Sets, Service Fabric, and Cloud Services.</span></span>  <span data-ttu-id="f2713-105">Bu sayfa, yalnızca bu hizmetlerden biri kullanıyorsanız geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="f2713-105">This page is only relevant if you are using one of these services.</span></span>
>

<span data-ttu-id="f2713-106">Azure tanılama Azure monitör, Application Insights ve günlük analizi gibi diğer Microsoft tanılama ürünlerle kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f2713-106">Azure Diagnostics is used with other Microsoft diagnostics products like Azure Monitor, Application Insights, and Log Analytics.</span></span>

<span data-ttu-id="f2713-107">Hello Azure tanılama yapılandırma dosyası kullanılan tooinitialize hello Tanılama izleme olan değerleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="f2713-107">hello Azure Diagnostics configuration file defines values that are used tooinitialize hello Diagnostics Monitor.</span></span> <span data-ttu-id="f2713-108">Merhaba tanılama başlatır izlerken bu kullanılan tooinitialize tanılama yapılandırma ayarlarını dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="f2713-108">This file is used tooinitialize diagnostic configuration settings when hello diagnostics monitor starts.</span></span>  

 <span data-ttu-id="f2713-109">Varsayılan olarak, yüklü toohello hello Azure tanılama yapılandırması şema dosyası olan `C:\Program Files\Microsoft SDKs\Azure\.NET SDK\<version>\schemas` dizini.</span><span class="sxs-lookup"><span data-stu-id="f2713-109">By default, hello Azure Diagnostics configuration schema file is installed toohello `C:\Program Files\Microsoft SDKs\Azure\.NET SDK\<version>\schemas` directory.</span></span> <span data-ttu-id="f2713-110">Değiştir `<version>` hello yüklü hello sürümüyle [Azure SDK'sı](http://www.windowsazure.com/develop/downloads/).</span><span class="sxs-lookup"><span data-stu-id="f2713-110">Replace `<version>` with hello installed version of hello [Azure SDK](http://www.windowsazure.com/develop/downloads/).</span></span>  

> [!NOTE]
>  <span data-ttu-id="f2713-111">Merhaba tanılama yapılandırma dosyası, genellikle önceki hello başlatma işleminde toplanan tanılama veri toobe gerektiren başlangıç görevleri ile kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f2713-111">hello diagnostics configuration file is typically used with startup tasks that require diagnostic data toobe collected earlier in hello startup process.</span></span> <span data-ttu-id="f2713-112">Azure tanılama kullanma hakkında daha fazla bilgi için bkz: [kullanarak Azure tanılama tarafından günlüğü verilerini toplamak](assetId:///83a91c23-5ca2-4fc9-8df3-62036c37a3d7).</span><span class="sxs-lookup"><span data-stu-id="f2713-112">For more information about using Azure Diagnostics, see [Collect Logging Data by Using Azure Diagnostics](assetId:///83a91c23-5ca2-4fc9-8df3-62036c37a3d7).</span></span>  

## <a name="example-of-hello-diagnostics-configuration-file"></a><span data-ttu-id="f2713-113">Merhaba tanılama yapılandırma dosyası örneği</span><span class="sxs-lookup"><span data-stu-id="f2713-113">Example of hello diagnostics configuration file</span></span>  
 <span data-ttu-id="f2713-114">Aşağıdaki örnek hello tipik tanılama yapılandırma dosyası gösterir:</span><span class="sxs-lookup"><span data-stu-id="f2713-114">hello following example shows a typical diagnostics configuration file:</span></span>  

```xml  
<?xml version="1.0" encoding="utf-8"?>
<DiagnosticMonitorConfiguration xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration"  
      configurationChangePollInterval="PT1M"  
      overallQuotaInMB="4096">  
   <DiagnosticInfrastructureLogs bufferQuotaInMB="1024"  
      scheduledTransferLogLevelFilter="Verbose"  
      scheduledTransferPeriod="PT1M" />  
   <Logs bufferQuotaInMB="1024"  
      scheduledTransferLogLevelFilter="Verbose"  
      scheduledTransferPeriod="PT1M" />  

   <Directories bufferQuotaInMB="1024"   
      scheduledTransferPeriod="PT1M">  

      <!-- These three elements specify hello special directories   
           that are set up for hello log types -->  
      <CrashDumps container="wad-crash-dumps" directoryQuotaInMB="256" />  
      <FailedRequestLogs container="wad-frq" directoryQuotaInMB="256" />  
      <IISLogs container="wad-iis" directoryQuotaInMB="256" />  

      <!-- For regular directories hello DataSources element is used -->  
      <DataSources>  
         <DirectoryConfiguration container="wad-panther" directoryQuotaInMB="128">  
            <!-- Absolute specifies an absolute path with optional environment expansion -->  
            <Absolute expandEnvironment="true" path="%SystemRoot%\system32\sysprep\Panther" />  
         </DirectoryConfiguration>  
         <DirectoryConfiguration container="wad-custom" directoryQuotaInMB="128">  
            <!-- LocalResource specifies a path relative tooa local   
                 resource defined in hello service definition -->  
            <LocalResource name="MyLoggingLocalResource" relativePath="logs" />  
         </DirectoryConfiguration>  
      </DataSources>  
   </Directories>  

   <PerformanceCounters bufferQuotaInMB="512" scheduledTransferPeriod="PT1M">  
      <!-- hello counter specifier is in hello same format as hello imperative   
           diagnostics configuration API -->  
      <PerformanceCounterConfiguration   
         counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT5S" />  
   </PerformanceCounters>  

   <WindowsEventLog bufferQuotaInMB="512"  
      scheduledTransferLogLevelFilter="Verbose"  
      scheduledTransferPeriod="PT1M">  
      <!-- hello event log name is in hello same format as hello imperative   
           diagnostics configuration API -->  
      <DataSource name="System!*" />  
   </WindowsEventLog>  
</DiagnosticMonitorConfiguration>  
```  

## <a name="diagnosticsconfiguration-namespace"></a><span data-ttu-id="f2713-115">DiagnosticsConfiguration Namespace</span><span class="sxs-lookup"><span data-stu-id="f2713-115">DiagnosticsConfiguration Namespace</span></span>  
 <span data-ttu-id="f2713-116">Merhaba tanılama yapılandırma dosyası için Hello XML ad alanı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="f2713-116">hello XML namespace for hello diagnostics configuration file is:</span></span>  

```  
http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration  
```  

## <a name="schema-elements"></a><span data-ttu-id="f2713-117">Şema öğeleri</span><span class="sxs-lookup"><span data-stu-id="f2713-117">Schema Elements</span></span>  
 <span data-ttu-id="f2713-118">Merhaba tanılama yapılandırma dosyası hello aşağıdaki öğeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="f2713-118">hello diagnostics configuration file includes hello following elements.</span></span>


## <a name="diagnosticmonitorconfiguration-element"></a><span data-ttu-id="f2713-119">DiagnosticMonitorConfiguration öğesi</span><span class="sxs-lookup"><span data-stu-id="f2713-119">DiagnosticMonitorConfiguration Element</span></span>  
<span data-ttu-id="f2713-120">Merhaba hello tanılama yapılandırma dosyasının en üst düzey öğesi.</span><span class="sxs-lookup"><span data-stu-id="f2713-120">hello top-level element of hello diagnostics configuration file.</span></span>  

<span data-ttu-id="f2713-121">Öznitelikleri:</span><span class="sxs-lookup"><span data-stu-id="f2713-121">Attributes:</span></span>

|<span data-ttu-id="f2713-122">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="f2713-122">Attribute</span></span>  |<span data-ttu-id="f2713-123">Tür</span><span class="sxs-lookup"><span data-stu-id="f2713-123">Type</span></span>   |<span data-ttu-id="f2713-124">Gerekli</span><span class="sxs-lookup"><span data-stu-id="f2713-124">Required</span></span>| <span data-ttu-id="f2713-125">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="f2713-125">Default</span></span> | <span data-ttu-id="f2713-126">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f2713-126">Description</span></span>|  
|-----------|-------|--------|---------|------------|  
|<span data-ttu-id="f2713-127">**configurationChangePollInterval**</span><span class="sxs-lookup"><span data-stu-id="f2713-127">**configurationChangePollInterval**</span></span>|<span data-ttu-id="f2713-128">Süre</span><span class="sxs-lookup"><span data-stu-id="f2713-128">duration</span></span>|<span data-ttu-id="f2713-129">İsteğe bağlı</span><span class="sxs-lookup"><span data-stu-id="f2713-129">Optional</span></span> | <span data-ttu-id="f2713-130">PT1M</span><span class="sxs-lookup"><span data-stu-id="f2713-130">PT1M</span></span>| <span data-ttu-id="f2713-131">Hangi hello tanı İzleyicisi yoklamalar Hello aralıkta tanılama yapılandırma değişikliklerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="f2713-131">Specifies hello interval at which hello diagnostic monitor polls for diagnostic configuration changes.</span></span>|  
|<span data-ttu-id="f2713-132">**overallQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="f2713-132">**overallQuotaInMB**</span></span>|<span data-ttu-id="f2713-133">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="f2713-133">unsignedInt</span></span>|<span data-ttu-id="f2713-134">İsteğe bağlı</span><span class="sxs-lookup"><span data-stu-id="f2713-134">Optional</span></span>| <span data-ttu-id="f2713-135">4000 MB.</span><span class="sxs-lookup"><span data-stu-id="f2713-135">4000 MB.</span></span> <span data-ttu-id="f2713-136">Bir değer belirtirseniz, bu miktar aşmamalıdır</span><span class="sxs-lookup"><span data-stu-id="f2713-136">If you provide a value, it must not exceed this amount</span></span> |<span data-ttu-id="f2713-137">Merhaba tüm günlük arabellekleri için ayrılan dosya sistemi depolama alanının toplam tutar.</span><span class="sxs-lookup"><span data-stu-id="f2713-137">hello total amount of file system storage allocated for all logging buffers.</span></span>|  

## <a name="diagnosticinfrastructurelogs-element"></a><span data-ttu-id="f2713-138">DiagnosticInfrastructureLogs öğesi</span><span class="sxs-lookup"><span data-stu-id="f2713-138">DiagnosticInfrastructureLogs Element</span></span>  
<span data-ttu-id="f2713-139">Merhaba temel Tanılama Altyapısı tarafından oluşturulan hello günlükleri Hello arabellek yapılandırmasını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="f2713-139">Defines hello buffer configuration for hello logs that are generated by hello underlying diagnostics infrastructure.</span></span>

<span data-ttu-id="f2713-140">Üst öğe: [DiagnosticMonitorConfiguration öğesi](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="f2713-140">Parent Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>  

<span data-ttu-id="f2713-141">Öznitelikleri:</span><span class="sxs-lookup"><span data-stu-id="f2713-141">Attributes:</span></span>

|<span data-ttu-id="f2713-142">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="f2713-142">Attribute</span></span>|<span data-ttu-id="f2713-143">Tür</span><span class="sxs-lookup"><span data-stu-id="f2713-143">Type</span></span>|<span data-ttu-id="f2713-144">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f2713-144">Description</span></span>|  
|---------|----|-----------------|  
|<span data-ttu-id="f2713-145">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="f2713-145">**bufferQuotaInMB**</span></span>|<span data-ttu-id="f2713-146">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="f2713-146">unsignedInt</span></span>|<span data-ttu-id="f2713-147">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="f2713-147">Optional.</span></span> <span data-ttu-id="f2713-148">Merhaba en belirtilen hello için kullanılabilir olan dosya sistemi depolama miktarını belirtir veri.</span><span class="sxs-lookup"><span data-stu-id="f2713-148">Specifies hello maximum amount of file system storage that is available for hello specified data.</span></span><br /><br /> <span data-ttu-id="f2713-149">Merhaba varsayılan 0'dır.</span><span class="sxs-lookup"><span data-stu-id="f2713-149">hello default is 0.</span></span>|  
|<span data-ttu-id="f2713-150">**scheduledTransferLogLevelFilter**</span><span class="sxs-lookup"><span data-stu-id="f2713-150">**scheduledTransferLogLevelFilter**</span></span>|<span data-ttu-id="f2713-151">Dize</span><span class="sxs-lookup"><span data-stu-id="f2713-151">string</span></span>|<span data-ttu-id="f2713-152">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="f2713-152">Optional.</span></span> <span data-ttu-id="f2713-153">Aktarılır günlük girişlerini Hello en düşük önem derecesini belirtir.</span><span class="sxs-lookup"><span data-stu-id="f2713-153">Specifies hello minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="f2713-154">Merhaba varsayılan değer **tanımlanmamış**.</span><span class="sxs-lookup"><span data-stu-id="f2713-154">hello default value is **Undefined**.</span></span> <span data-ttu-id="f2713-155">Diğer olası değerler şunlardır: **ayrıntılı**, **bilgi**, **uyarı**, **hata**, ve **kritik**.</span><span class="sxs-lookup"><span data-stu-id="f2713-155">Other possible values are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="f2713-156">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="f2713-156">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="f2713-157">Süre</span><span class="sxs-lookup"><span data-stu-id="f2713-157">duration</span></span>|<span data-ttu-id="f2713-158">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="f2713-158">Optional.</span></span> <span data-ttu-id="f2713-159">Zamanlanmış toohello minute en yakın yukarı yuvarlanmasını veri aktarımını Hello aralığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="f2713-159">Specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span><br /><br /> <span data-ttu-id="f2713-160">Merhaba, PT0S varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="f2713-160">hello default is PT0S.</span></span>|  

## <a name="logs-element"></a><span data-ttu-id="f2713-161">Günlükleri öğesi</span><span class="sxs-lookup"><span data-stu-id="f2713-161">Logs Element</span></span>  
 <span data-ttu-id="f2713-162">Temel Azure günlükleri Hello arabellek yapılandırmasını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="f2713-162">Defines hello buffer configuration for basic Azure logs.</span></span>

 <span data-ttu-id="f2713-163">Üst öğenin: [DiagnosticMonitorConfiguration öğesi](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="f2713-163">Parent element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>  

<span data-ttu-id="f2713-164">Öznitelikleri:</span><span class="sxs-lookup"><span data-stu-id="f2713-164">Attributes:</span></span>  

|<span data-ttu-id="f2713-165">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="f2713-165">Attribute</span></span>|<span data-ttu-id="f2713-166">Tür</span><span class="sxs-lookup"><span data-stu-id="f2713-166">Type</span></span>|<span data-ttu-id="f2713-167">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f2713-167">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="f2713-168">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="f2713-168">**bufferQuotaInMB**</span></span>|<span data-ttu-id="f2713-169">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="f2713-169">unsignedInt</span></span>|<span data-ttu-id="f2713-170">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="f2713-170">Optional.</span></span> <span data-ttu-id="f2713-171">Merhaba en belirtilen hello için kullanılabilir olan dosya sistemi depolama miktarını belirtir veri.</span><span class="sxs-lookup"><span data-stu-id="f2713-171">Specifies hello maximum amount of file system storage that is available for hello specified data.</span></span><br /><br /> <span data-ttu-id="f2713-172">Merhaba varsayılan 0'dır.</span><span class="sxs-lookup"><span data-stu-id="f2713-172">hello default is 0.</span></span>|  
|<span data-ttu-id="f2713-173">**scheduledTransferLogLevelFilter**</span><span class="sxs-lookup"><span data-stu-id="f2713-173">**scheduledTransferLogLevelFilter**</span></span>|<span data-ttu-id="f2713-174">Dize</span><span class="sxs-lookup"><span data-stu-id="f2713-174">string</span></span>|<span data-ttu-id="f2713-175">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="f2713-175">Optional.</span></span> <span data-ttu-id="f2713-176">Aktarılır günlük girişlerini Hello en düşük önem derecesini belirtir.</span><span class="sxs-lookup"><span data-stu-id="f2713-176">Specifies hello minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="f2713-177">Merhaba varsayılan değer **tanımlanmamış**.</span><span class="sxs-lookup"><span data-stu-id="f2713-177">hello default value is **Undefined**.</span></span> <span data-ttu-id="f2713-178">Diğer olası değerler şunlardır: **ayrıntılı**, **bilgi**, **uyarı**, **hata**, ve **kritik**.</span><span class="sxs-lookup"><span data-stu-id="f2713-178">Other possible values are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="f2713-179">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="f2713-179">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="f2713-180">Süre</span><span class="sxs-lookup"><span data-stu-id="f2713-180">duration</span></span>|<span data-ttu-id="f2713-181">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="f2713-181">Optional.</span></span> <span data-ttu-id="f2713-182">Zamanlanmış toohello minute en yakın yukarı yuvarlanmasını veri aktarımını Hello aralığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="f2713-182">Specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span><br /><br /> <span data-ttu-id="f2713-183">Merhaba, PT0S varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="f2713-183">hello default is PT0S.</span></span>|  

## <a name="directories-element"></a><span data-ttu-id="f2713-184">Dizinleri öğesi</span><span class="sxs-lookup"><span data-stu-id="f2713-184">Directories Element</span></span>  
<span data-ttu-id="f2713-185">Merhaba arabellek yapılandırmasını tanımlamak dosya tabanlı günlükleri için tanımlar.</span><span class="sxs-lookup"><span data-stu-id="f2713-185">Defines hello buffer configuration for file-based logs that you can define.</span></span>

<span data-ttu-id="f2713-186">Üst öğenin: [DiagnosticMonitorConfiguration öğesi](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="f2713-186">Parent element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>  


<span data-ttu-id="f2713-187">Öznitelikleri:</span><span class="sxs-lookup"><span data-stu-id="f2713-187">Attributes:</span></span>  

|<span data-ttu-id="f2713-188">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="f2713-188">Attribute</span></span>|<span data-ttu-id="f2713-189">Tür</span><span class="sxs-lookup"><span data-stu-id="f2713-189">Type</span></span>|<span data-ttu-id="f2713-190">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f2713-190">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="f2713-191">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="f2713-191">**bufferQuotaInMB**</span></span>|<span data-ttu-id="f2713-192">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="f2713-192">unsignedInt</span></span>|<span data-ttu-id="f2713-193">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="f2713-193">Optional.</span></span> <span data-ttu-id="f2713-194">Merhaba en belirtilen hello için kullanılabilir olan dosya sistemi depolama miktarını belirtir veri.</span><span class="sxs-lookup"><span data-stu-id="f2713-194">Specifies hello maximum amount of file system storage that is available for hello specified data.</span></span><br /><br /> <span data-ttu-id="f2713-195">Merhaba varsayılan 0'dır.</span><span class="sxs-lookup"><span data-stu-id="f2713-195">hello default is 0.</span></span>|  
|<span data-ttu-id="f2713-196">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="f2713-196">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="f2713-197">Süre</span><span class="sxs-lookup"><span data-stu-id="f2713-197">duration</span></span>|<span data-ttu-id="f2713-198">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="f2713-198">Optional.</span></span> <span data-ttu-id="f2713-199">Zamanlanmış toohello minute en yakın yukarı yuvarlanmasını veri aktarımını Hello aralığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="f2713-199">Specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span><br /><br /> <span data-ttu-id="f2713-200">Merhaba, PT0S varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="f2713-200">hello default is PT0S.</span></span>|  

## <a name="crashdumps-element"></a><span data-ttu-id="f2713-201">CrashDumps öğesi</span><span class="sxs-lookup"><span data-stu-id="f2713-201">CrashDumps Element</span></span>  
 <span data-ttu-id="f2713-202">Merhaba kilitlenme dökümleri directory tanımlar.</span><span class="sxs-lookup"><span data-stu-id="f2713-202">Defines hello crash dumps directory.</span></span>

 <span data-ttu-id="f2713-203">Üst öğe: [dizinleri öğesi](#Directories).</span><span class="sxs-lookup"><span data-stu-id="f2713-203">Parent Element: [Directories Element](#Directories).</span></span>  

<span data-ttu-id="f2713-204">Öznitelikleri:</span><span class="sxs-lookup"><span data-stu-id="f2713-204">Attributes:</span></span>  

|<span data-ttu-id="f2713-205">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="f2713-205">Attribute</span></span>|<span data-ttu-id="f2713-206">Tür</span><span class="sxs-lookup"><span data-stu-id="f2713-206">Type</span></span>|<span data-ttu-id="f2713-207">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f2713-207">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="f2713-208">**kapsayıcı**</span><span class="sxs-lookup"><span data-stu-id="f2713-208">**container**</span></span>|<span data-ttu-id="f2713-209">Dize</span><span class="sxs-lookup"><span data-stu-id="f2713-209">string</span></span>|<span data-ttu-id="f2713-210">Merhaba hello dizinin Merhaba içeriğine toobe olduğu hello kapsayıcının adını aktarılan.</span><span class="sxs-lookup"><span data-stu-id="f2713-210">hello name of hello container where hello contents of hello directory is toobe transferred.</span></span>|  
|<span data-ttu-id="f2713-211">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="f2713-211">**directoryQuotaInMB**</span></span>|<span data-ttu-id="f2713-212">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="f2713-212">unsignedInt</span></span>|<span data-ttu-id="f2713-213">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="f2713-213">Optional.</span></span> <span data-ttu-id="f2713-214">Hello dizinin Hello maksimum boyutu megabayt cinsinden belirtir.</span><span class="sxs-lookup"><span data-stu-id="f2713-214">Specifies hello maximum size of hello directory in megabytes.</span></span><br /><br /> <span data-ttu-id="f2713-215">Merhaba varsayılan 0'dır.</span><span class="sxs-lookup"><span data-stu-id="f2713-215">hello default is 0.</span></span>|  

## <a name="failedrequestlogs-element"></a><span data-ttu-id="f2713-216">FailedRequestLogs öğesi</span><span class="sxs-lookup"><span data-stu-id="f2713-216">FailedRequestLogs Element</span></span>  
 <span data-ttu-id="f2713-217">Merhaba başarısız istek günlük dizini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="f2713-217">Defines hello failed request log directory.</span></span>

 <span data-ttu-id="f2713-218">Üst öğesi [dizinleri öğesi](#Directories).</span><span class="sxs-lookup"><span data-stu-id="f2713-218">Parent Element [Directories Element](#Directories).</span></span>  

<span data-ttu-id="f2713-219">Öznitelikleri:</span><span class="sxs-lookup"><span data-stu-id="f2713-219">Attributes:</span></span>  

|<span data-ttu-id="f2713-220">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="f2713-220">Attribute</span></span>|<span data-ttu-id="f2713-221">Tür</span><span class="sxs-lookup"><span data-stu-id="f2713-221">Type</span></span>|<span data-ttu-id="f2713-222">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f2713-222">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="f2713-223">**kapsayıcı**</span><span class="sxs-lookup"><span data-stu-id="f2713-223">**container**</span></span>|<span data-ttu-id="f2713-224">Dize</span><span class="sxs-lookup"><span data-stu-id="f2713-224">string</span></span>|<span data-ttu-id="f2713-225">Merhaba hello dizinin Merhaba içeriğine toobe olduğu hello kapsayıcının adını aktarılan.</span><span class="sxs-lookup"><span data-stu-id="f2713-225">hello name of hello container where hello contents of hello directory is toobe transferred.</span></span>|  
|<span data-ttu-id="f2713-226">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="f2713-226">**directoryQuotaInMB**</span></span>|<span data-ttu-id="f2713-227">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="f2713-227">unsignedInt</span></span>|<span data-ttu-id="f2713-228">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="f2713-228">Optional.</span></span> <span data-ttu-id="f2713-229">Hello dizinin Hello maksimum boyutu megabayt cinsinden belirtir.</span><span class="sxs-lookup"><span data-stu-id="f2713-229">Specifies hello maximum size of hello directory in megabytes.</span></span><br /><br /> <span data-ttu-id="f2713-230">Merhaba varsayılan 0'dır.</span><span class="sxs-lookup"><span data-stu-id="f2713-230">hello default is 0.</span></span>|  

##  <a name="iislogs-element"></a><span data-ttu-id="f2713-231">IISLogs öğesi</span><span class="sxs-lookup"><span data-stu-id="f2713-231">IISLogs Element</span></span>  
 <span data-ttu-id="f2713-232">Merhaba IIS Günlük dizini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="f2713-232">Defines hello IIS log directory.</span></span>

 <span data-ttu-id="f2713-233">Üst öğesi [dizinleri öğesi](#Directories).</span><span class="sxs-lookup"><span data-stu-id="f2713-233">Parent Element [Directories Element](#Directories).</span></span>  

<span data-ttu-id="f2713-234">Öznitelikleri:</span><span class="sxs-lookup"><span data-stu-id="f2713-234">Attributes:</span></span>  

|<span data-ttu-id="f2713-235">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="f2713-235">Attribute</span></span>|<span data-ttu-id="f2713-236">Tür</span><span class="sxs-lookup"><span data-stu-id="f2713-236">Type</span></span>|<span data-ttu-id="f2713-237">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f2713-237">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="f2713-238">**kapsayıcı**</span><span class="sxs-lookup"><span data-stu-id="f2713-238">**container**</span></span>|<span data-ttu-id="f2713-239">Dize</span><span class="sxs-lookup"><span data-stu-id="f2713-239">string</span></span>|<span data-ttu-id="f2713-240">Merhaba hello dizinin Merhaba içeriğine toobe olduğu hello kapsayıcının adını aktarılan.</span><span class="sxs-lookup"><span data-stu-id="f2713-240">hello name of hello container where hello contents of hello directory is toobe transferred.</span></span>|  
|<span data-ttu-id="f2713-241">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="f2713-241">**directoryQuotaInMB**</span></span>|<span data-ttu-id="f2713-242">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="f2713-242">unsignedInt</span></span>|<span data-ttu-id="f2713-243">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="f2713-243">Optional.</span></span> <span data-ttu-id="f2713-244">Hello dizinin Hello maksimum boyutu megabayt cinsinden belirtir.</span><span class="sxs-lookup"><span data-stu-id="f2713-244">Specifies hello maximum size of hello directory in megabytes.</span></span><br /><br /> <span data-ttu-id="f2713-245">Merhaba varsayılan 0'dır.</span><span class="sxs-lookup"><span data-stu-id="f2713-245">hello default is 0.</span></span>|  

## <a name="datasources-element"></a><span data-ttu-id="f2713-246">Veri kaynakları öğesi</span><span class="sxs-lookup"><span data-stu-id="f2713-246">DataSources Element</span></span>  
 <span data-ttu-id="f2713-247">Sıfır veya daha fazla ek günlük dizinleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="f2713-247">Defines zero or more additional log directories.</span></span>

 <span data-ttu-id="f2713-248">Üst öğe: [dizinleri öğesi](#Directories).</span><span class="sxs-lookup"><span data-stu-id="f2713-248">Parent Element: [Directories Element](#Directories).</span></span>

## <a name="directoryconfiguration-element"></a><span data-ttu-id="f2713-249">DirectoryConfiguration öğesi</span><span class="sxs-lookup"><span data-stu-id="f2713-249">DirectoryConfiguration Element</span></span>  
 <span data-ttu-id="f2713-250">Günlük dosyaları toomonitor Hello dizini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="f2713-250">Defines hello directory of log files toomonitor.</span></span>

 <span data-ttu-id="f2713-251">Üst öğe: [veri kaynakları öğesi](#DataSources).</span><span class="sxs-lookup"><span data-stu-id="f2713-251">Parent Element: [DataSources Element](#DataSources).</span></span>

<span data-ttu-id="f2713-252">Öznitelikleri:</span><span class="sxs-lookup"><span data-stu-id="f2713-252">Attributes:</span></span>

|<span data-ttu-id="f2713-253">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="f2713-253">Attribute</span></span>|<span data-ttu-id="f2713-254">Tür</span><span class="sxs-lookup"><span data-stu-id="f2713-254">Type</span></span>|<span data-ttu-id="f2713-255">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f2713-255">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="f2713-256">**kapsayıcı**</span><span class="sxs-lookup"><span data-stu-id="f2713-256">**container**</span></span>|<span data-ttu-id="f2713-257">Dize</span><span class="sxs-lookup"><span data-stu-id="f2713-257">string</span></span>|<span data-ttu-id="f2713-258">Merhaba hello dizinin Merhaba içeriğine toobe olduğu hello kapsayıcının adını aktarılan.</span><span class="sxs-lookup"><span data-stu-id="f2713-258">hello name of hello container where hello contents of hello directory is toobe transferred.</span></span>|  
|<span data-ttu-id="f2713-259">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="f2713-259">**directoryQuotaInMB**</span></span>|<span data-ttu-id="f2713-260">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="f2713-260">unsignedInt</span></span>|<span data-ttu-id="f2713-261">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="f2713-261">Optional.</span></span> <span data-ttu-id="f2713-262">Hello dizinin Hello maksimum boyutu megabayt cinsinden belirtir.</span><span class="sxs-lookup"><span data-stu-id="f2713-262">Specifies hello maximum size of hello directory in megabytes.</span></span><br /><br /> <span data-ttu-id="f2713-263">Merhaba varsayılan 0'dır.</span><span class="sxs-lookup"><span data-stu-id="f2713-263">hello default is 0.</span></span>|  

## <a name="absolute-element"></a><span data-ttu-id="f2713-264">Mutlak öğesi</span><span class="sxs-lookup"><span data-stu-id="f2713-264">Absolute Element</span></span>  
 <span data-ttu-id="f2713-265">İsteğe bağlı ortam genişletme ile Merhaba dizin toomonitor mutlak bir yol tanımlar.</span><span class="sxs-lookup"><span data-stu-id="f2713-265">Defines an absolute path of hello directory toomonitor with optional environment expansion.</span></span>

 <span data-ttu-id="f2713-266">Üst öğe: [DirectoryConfiguration öğesi](#DirectoryConfiguration).</span><span class="sxs-lookup"><span data-stu-id="f2713-266">Parent Element: [DirectoryConfiguration Element](#DirectoryConfiguration).</span></span>  

<span data-ttu-id="f2713-267">Öznitelikleri:</span><span class="sxs-lookup"><span data-stu-id="f2713-267">Attributes:</span></span>  

|<span data-ttu-id="f2713-268">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="f2713-268">Attribute</span></span>|<span data-ttu-id="f2713-269">Tür</span><span class="sxs-lookup"><span data-stu-id="f2713-269">Type</span></span>|<span data-ttu-id="f2713-270">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f2713-270">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="f2713-271">**yol**</span><span class="sxs-lookup"><span data-stu-id="f2713-271">**path**</span></span>|<span data-ttu-id="f2713-272">Dize</span><span class="sxs-lookup"><span data-stu-id="f2713-272">string</span></span>|<span data-ttu-id="f2713-273">Gereklidir.</span><span class="sxs-lookup"><span data-stu-id="f2713-273">Required.</span></span> <span data-ttu-id="f2713-274">mutlak yol toohello directory toomonitor hello.</span><span class="sxs-lookup"><span data-stu-id="f2713-274">hello absolute path toohello directory toomonitor.</span></span>|  
|<span data-ttu-id="f2713-275">**expandEnvironment**</span><span class="sxs-lookup"><span data-stu-id="f2713-275">**expandEnvironment**</span></span>|<span data-ttu-id="f2713-276">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="f2713-276">boolean</span></span>|<span data-ttu-id="f2713-277">Gereklidir.</span><span class="sxs-lookup"><span data-stu-id="f2713-277">Required.</span></span> <span data-ttu-id="f2713-278">Varsa çok ayarlamak**doğru**, ortam değişkenleri hello yolun genişletilmiş.</span><span class="sxs-lookup"><span data-stu-id="f2713-278">If set too**true**, environment variables in hello path are expanded.</span></span>|  

## <a name="localresource-element"></a><span data-ttu-id="f2713-279">LocalResource öğesi</span><span class="sxs-lookup"><span data-stu-id="f2713-279">LocalResource Element</span></span>  
 <span data-ttu-id="f2713-280">Merhaba hizmet tanımında tanımlanan yolu göreli tooa yerel bir kaynak tanımlar.</span><span class="sxs-lookup"><span data-stu-id="f2713-280">Defines a path relative tooa local resource defined in hello service definition.</span></span>

 <span data-ttu-id="f2713-281">Üst öğe: [DirectoryConfiguration öğesi](#DirectoryConfiguration).</span><span class="sxs-lookup"><span data-stu-id="f2713-281">Parent Element: [DirectoryConfiguration Element](#DirectoryConfiguration).</span></span>  

<span data-ttu-id="f2713-282">Öznitelikleri:</span><span class="sxs-lookup"><span data-stu-id="f2713-282">Attributes:</span></span>  

|<span data-ttu-id="f2713-283">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="f2713-283">Attribute</span></span>|<span data-ttu-id="f2713-284">Tür</span><span class="sxs-lookup"><span data-stu-id="f2713-284">Type</span></span>|<span data-ttu-id="f2713-285">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f2713-285">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="f2713-286">**adı**</span><span class="sxs-lookup"><span data-stu-id="f2713-286">**name**</span></span>|<span data-ttu-id="f2713-287">Dize</span><span class="sxs-lookup"><span data-stu-id="f2713-287">string</span></span>|<span data-ttu-id="f2713-288">Gereklidir.</span><span class="sxs-lookup"><span data-stu-id="f2713-288">Required.</span></span> <span data-ttu-id="f2713-289">Merhaba dizin toomonitor içeren hello yerel kaynak Hello adı.</span><span class="sxs-lookup"><span data-stu-id="f2713-289">hello name of hello local resource that contains hello directory toomonitor.</span></span>|  
|<span data-ttu-id="f2713-290">**relativePath**</span><span class="sxs-lookup"><span data-stu-id="f2713-290">**relativePath**</span></span>|<span data-ttu-id="f2713-291">Dize</span><span class="sxs-lookup"><span data-stu-id="f2713-291">string</span></span>|<span data-ttu-id="f2713-292">Gereklidir.</span><span class="sxs-lookup"><span data-stu-id="f2713-292">Required.</span></span> <span data-ttu-id="f2713-293">Merhaba yolu göreli toohello yerel kaynak toomonitor.</span><span class="sxs-lookup"><span data-stu-id="f2713-293">hello path relative toohello local resource toomonitor.</span></span>|  

## <a name="performancecounters-element"></a><span data-ttu-id="f2713-294">PerformanceCounters öğesi</span><span class="sxs-lookup"><span data-stu-id="f2713-294">PerformanceCounters Element</span></span>  
 <span data-ttu-id="f2713-295">Merhaba yolu toohello performans sayacı toocollect tanımlar.</span><span class="sxs-lookup"><span data-stu-id="f2713-295">Defines hello path toohello performance counter toocollect.</span></span>

 <span data-ttu-id="f2713-296">Üst öğe: [DiagnosticMonitorConfiguration öğesi](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="f2713-296">Parent Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>


 <span data-ttu-id="f2713-297">Öznitelikleri:</span><span class="sxs-lookup"><span data-stu-id="f2713-297">Attributes:</span></span>  

|<span data-ttu-id="f2713-298">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="f2713-298">Attribute</span></span>|<span data-ttu-id="f2713-299">Tür</span><span class="sxs-lookup"><span data-stu-id="f2713-299">Type</span></span>|<span data-ttu-id="f2713-300">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f2713-300">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="f2713-301">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="f2713-301">**bufferQuotaInMB**</span></span>|<span data-ttu-id="f2713-302">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="f2713-302">unsignedInt</span></span>|<span data-ttu-id="f2713-303">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="f2713-303">Optional.</span></span> <span data-ttu-id="f2713-304">Merhaba en belirtilen hello için kullanılabilir olan dosya sistemi depolama miktarını belirtir veri.</span><span class="sxs-lookup"><span data-stu-id="f2713-304">Specifies hello maximum amount of file system storage that is available for hello specified data.</span></span><br /><br /> <span data-ttu-id="f2713-305">Merhaba varsayılan 0'dır.</span><span class="sxs-lookup"><span data-stu-id="f2713-305">hello default is 0.</span></span>|  
|<span data-ttu-id="f2713-306">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="f2713-306">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="f2713-307">Süre</span><span class="sxs-lookup"><span data-stu-id="f2713-307">duration</span></span>|<span data-ttu-id="f2713-308">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="f2713-308">Optional.</span></span> <span data-ttu-id="f2713-309">Zamanlanmış toohello minute en yakın yukarı yuvarlanmasını veri aktarımını Hello aralığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="f2713-309">Specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span><br /><br /> <span data-ttu-id="f2713-310">Merhaba, PT0S varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="f2713-310">hello default is PT0S.</span></span>|  

## <a name="performancecounterconfiguration-element"></a><span data-ttu-id="f2713-311">PerformanceCounterConfiguration öğesi</span><span class="sxs-lookup"><span data-stu-id="f2713-311">PerformanceCounterConfiguration Element</span></span>  
 <span data-ttu-id="f2713-312">Merhaba performans sayacı toocollect tanımlar.</span><span class="sxs-lookup"><span data-stu-id="f2713-312">Defines hello performance counter toocollect.</span></span>

 <span data-ttu-id="f2713-313">Üst öğe: [PerformanceCounters öğesi](#PerformanceCounters).</span><span class="sxs-lookup"><span data-stu-id="f2713-313">Parent Element: [PerformanceCounters Element](#PerformanceCounters).</span></span>  

 <span data-ttu-id="f2713-314">Öznitelikleri:</span><span class="sxs-lookup"><span data-stu-id="f2713-314">Attributes:</span></span>  

|<span data-ttu-id="f2713-315">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="f2713-315">Attribute</span></span>|<span data-ttu-id="f2713-316">Tür</span><span class="sxs-lookup"><span data-stu-id="f2713-316">Type</span></span>|<span data-ttu-id="f2713-317">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f2713-317">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="f2713-318">**counterSpecifier**</span><span class="sxs-lookup"><span data-stu-id="f2713-318">**counterSpecifier**</span></span>|<span data-ttu-id="f2713-319">Dize</span><span class="sxs-lookup"><span data-stu-id="f2713-319">string</span></span>|<span data-ttu-id="f2713-320">Gereklidir.</span><span class="sxs-lookup"><span data-stu-id="f2713-320">Required.</span></span> <span data-ttu-id="f2713-321">Merhaba yolu toohello performans sayacı toocollect.</span><span class="sxs-lookup"><span data-stu-id="f2713-321">hello path toohello performance counter toocollect.</span></span>|  
|<span data-ttu-id="f2713-322">**sampleRate**</span><span class="sxs-lookup"><span data-stu-id="f2713-322">**sampleRate**</span></span>|<span data-ttu-id="f2713-323">Süre</span><span class="sxs-lookup"><span data-stu-id="f2713-323">duration</span></span>|<span data-ttu-id="f2713-324">Gereklidir.</span><span class="sxs-lookup"><span data-stu-id="f2713-324">Required.</span></span> <span data-ttu-id="f2713-325">Performans sayacı hangi hello toplanması gereken hello oranı.</span><span class="sxs-lookup"><span data-stu-id="f2713-325">hello rate at which hello performance counter should be collected.</span></span>|  

## <a name="windowseventlog-element"></a><span data-ttu-id="f2713-326">WindowsEventLog öğesi</span><span class="sxs-lookup"><span data-stu-id="f2713-326">WindowsEventLog Element</span></span>  
 <span data-ttu-id="f2713-327">Merhaba olay günlüklerini toomonitor tanımlar.</span><span class="sxs-lookup"><span data-stu-id="f2713-327">Defines hello event logs toomonitor.</span></span>

 <span data-ttu-id="f2713-328">Üst öğe: [DiagnosticMonitorConfiguration öğesi](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="f2713-328">Parent Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>

  <span data-ttu-id="f2713-329">Öznitelikleri:</span><span class="sxs-lookup"><span data-stu-id="f2713-329">Attributes:</span></span>

|<span data-ttu-id="f2713-330">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="f2713-330">Attribute</span></span>|<span data-ttu-id="f2713-331">Tür</span><span class="sxs-lookup"><span data-stu-id="f2713-331">Type</span></span>|<span data-ttu-id="f2713-332">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f2713-332">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="f2713-333">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="f2713-333">**bufferQuotaInMB**</span></span>|<span data-ttu-id="f2713-334">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="f2713-334">unsignedInt</span></span>|<span data-ttu-id="f2713-335">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="f2713-335">Optional.</span></span> <span data-ttu-id="f2713-336">Merhaba en belirtilen hello için kullanılabilir olan dosya sistemi depolama miktarını belirtir veri.</span><span class="sxs-lookup"><span data-stu-id="f2713-336">Specifies hello maximum amount of file system storage that is available for hello specified data.</span></span><br /><br /> <span data-ttu-id="f2713-337">Merhaba varsayılan 0'dır.</span><span class="sxs-lookup"><span data-stu-id="f2713-337">hello default is 0.</span></span>|  
|<span data-ttu-id="f2713-338">**scheduledTransferLogLevelFilter**</span><span class="sxs-lookup"><span data-stu-id="f2713-338">**scheduledTransferLogLevelFilter**</span></span>|<span data-ttu-id="f2713-339">Dize</span><span class="sxs-lookup"><span data-stu-id="f2713-339">string</span></span>|<span data-ttu-id="f2713-340">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="f2713-340">Optional.</span></span> <span data-ttu-id="f2713-341">Aktarılır günlük girişlerini Hello en düşük önem derecesini belirtir.</span><span class="sxs-lookup"><span data-stu-id="f2713-341">Specifies hello minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="f2713-342">Merhaba varsayılan değer **tanımlanmamış**.</span><span class="sxs-lookup"><span data-stu-id="f2713-342">hello default value is **Undefined**.</span></span> <span data-ttu-id="f2713-343">Diğer olası değerler şunlardır: **ayrıntılı**, **bilgi**, **uyarı**, **hata**, ve **kritik**.</span><span class="sxs-lookup"><span data-stu-id="f2713-343">Other possible values are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="f2713-344">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="f2713-344">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="f2713-345">Süre</span><span class="sxs-lookup"><span data-stu-id="f2713-345">duration</span></span>|<span data-ttu-id="f2713-346">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="f2713-346">Optional.</span></span> <span data-ttu-id="f2713-347">Zamanlanmış toohello minute en yakın yukarı yuvarlanmasını veri aktarımını Hello aralığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="f2713-347">Specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span><br /><br /> <span data-ttu-id="f2713-348">Merhaba, PT0S varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="f2713-348">hello default is PT0S.</span></span>|  

## <a name="datasource-element"></a><span data-ttu-id="f2713-349">Veri kaynağı öğesi</span><span class="sxs-lookup"><span data-stu-id="f2713-349">DataSource Element</span></span>  
 <span data-ttu-id="f2713-350">Merhaba olay günlüğü toomonitor tanımlar.</span><span class="sxs-lookup"><span data-stu-id="f2713-350">Defines hello event log toomonitor.</span></span>

 <span data-ttu-id="f2713-351">Üst öğe: [WindowsEventLog öğesi](#windowsEventLog).</span><span class="sxs-lookup"><span data-stu-id="f2713-351">Parent Element: [WindowsEventLog Element](#windowsEventLog).</span></span>  

 <span data-ttu-id="f2713-352">Öznitelikleri:</span><span class="sxs-lookup"><span data-stu-id="f2713-352">Attributes:</span></span>

|<span data-ttu-id="f2713-353">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="f2713-353">Attribute</span></span>|<span data-ttu-id="f2713-354">Tür</span><span class="sxs-lookup"><span data-stu-id="f2713-354">Type</span></span>|<span data-ttu-id="f2713-355">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f2713-355">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="f2713-356">**adı**</span><span class="sxs-lookup"><span data-stu-id="f2713-356">**name**</span></span>|<span data-ttu-id="f2713-357">Dize</span><span class="sxs-lookup"><span data-stu-id="f2713-357">string</span></span>|<span data-ttu-id="f2713-358">Gereklidir.</span><span class="sxs-lookup"><span data-stu-id="f2713-358">Required.</span></span> <span data-ttu-id="f2713-359">Merhaba günlük toocollect belirten bir XPath ifadesi.</span><span class="sxs-lookup"><span data-stu-id="f2713-359">An XPath expression specifying hello log toocollect.</span></span>|  
