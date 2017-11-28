---
title: "aaaAzure tanılama uzantısı 1.3 ve sonraki yapılandırma şeması | Microsoft Docs"
description: "Şema sürümü 1.3 ve daha sonra Azure tanılama hello Microsoft Azure SDK 2.4 ve daha sonraki bir parçası olarak gönderilir."
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
ms.openlocfilehash: bd15d3a79ea818fcb3235854717e58d5da36518e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-diagnostics-13-and-later-configuration-schema"></a><span data-ttu-id="a6293-103">Azure tanılama 1.3 ve daha sonra yapılandırma şeması</span><span class="sxs-lookup"><span data-stu-id="a6293-103">Azure Diagnostics 1.3 and later configuration schema</span></span>
> [!NOTE]
> <span data-ttu-id="a6293-104">Hello Azure tanılama uzantısını hello bileşen toocollect performans sayaçları ve diğer istatistiklerine kullanılır:</span><span class="sxs-lookup"><span data-stu-id="a6293-104">hello Azure Diagnostics extension is hello component used toocollect performance counters and other statistics from:</span></span>
> - <span data-ttu-id="a6293-105">Azure Sanal Makineler</span><span class="sxs-lookup"><span data-stu-id="a6293-105">Azure Virtual Machines</span></span> 
> - <span data-ttu-id="a6293-106">Sanal Makine Ölçek Kümeleri</span><span class="sxs-lookup"><span data-stu-id="a6293-106">Virtual Machine Scale Sets</span></span>
> - <span data-ttu-id="a6293-107">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="a6293-107">Service Fabric</span></span> 
> - <span data-ttu-id="a6293-108">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="a6293-108">Cloud Services</span></span> 
> - <span data-ttu-id="a6293-109">Ağ Güvenlik Grupları</span><span class="sxs-lookup"><span data-stu-id="a6293-109">Network Security Groups</span></span>
> 
> <span data-ttu-id="a6293-110">Bu sayfa, yalnızca bu hizmetlerden biri kullanıyorsanız geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="a6293-110">This page is only relevant if you are using one of these services.</span></span>

<span data-ttu-id="a6293-111">Bu sayfa sürümleri 1.3 ve daha yeni (Azure SDK 2.4 ve daha yeni) için geçerli değil.</span><span class="sxs-lookup"><span data-stu-id="a6293-111">This page is valid for versions 1.3 and newer (Azure SDK 2.4 and newer).</span></span> <span data-ttu-id="a6293-112">Yeni yapılandırma bölümlerinin eklendikleri hangi sürümünde açıklamalı tooshow ' dir.</span><span class="sxs-lookup"><span data-stu-id="a6293-112">Newer configuration sections are commented tooshow in what version they were added.</span></span>  

<span data-ttu-id="a6293-113">Merhaba tanılama başlatır izlediğinizde burada açıklanan hello yapılandırma kullanılan tooset tanılama yapılandırma ayarlarını dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="a6293-113">hello configuration file described here is used tooset diagnostic configuration settings when hello diagnostics monitor starts.</span></span>  

<span data-ttu-id="a6293-114">Merhaba uzantısı Azure monitör, Application Insights ve günlük analizi gibi diğer Microsoft tanılama ürün ile birlikte kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a6293-114">hello extension is used in conjunction with other Microsoft diagnostics products like Azure Monitor, Application Insights, and Log Analytics.</span></span>



<span data-ttu-id="a6293-115">Merhaba ortak yapılandırma dosyası şeması tanımı hello aşağıdaki PowerShell komutunu yürüterek yükleyin:</span><span class="sxs-lookup"><span data-stu-id="a6293-115">Download hello public configuration file schema definition by executing hello following PowerShell command:</span></span>  

```powershell  
(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File –Encoding utf8 -FilePath 'C:\temp\WadConfig.xsd'  
```  

<span data-ttu-id="a6293-116">Azure tanılama kullanma hakkında daha fazla bilgi için bkz: [Azure tanılama uzantısını](azure-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="a6293-116">For more information about using Azure Diagnostics, see [Azure Diagnostics Extension](azure-diagnostics.md).</span></span>  

## <a name="example-of-hello-diagnostics-configuration-file"></a><span data-ttu-id="a6293-117">Merhaba tanılama yapılandırma dosyası örneği</span><span class="sxs-lookup"><span data-stu-id="a6293-117">Example of hello diagnostics configuration file</span></span>  
 <span data-ttu-id="a6293-118">Aşağıdaki örnek hello tipik tanılama yapılandırma dosyası gösterir:</span><span class="sxs-lookup"><span data-stu-id="a6293-118">hello following example shows a typical diagnostics configuration file:</span></span>  

```xml  
<?xml version="1.0" encoding="utf-8"?>  
<DiagnosticsConfiguration  xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">   
  <PublicConfig>  
    <WadCfg>  
      <DiagnosticMonitorConfiguration overallQuotaInMB="10000">  

        <PerformanceCounters scheduledTransferPeriod="PT1M">  
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT1M" unit="percent" />  
        </PerformanceCounters>  

        <Directories scheduledTransferPeriod="PT5M">  
          <IISLogs containerName="iislogs" />  
          <FailedRequestLogs containerName="iisfailed" />  

          <DataSources>  
            <DirectoryConfiguration containerName="mynewprocess">  
              <Absolute path="C:\MyNewProcess" expandEnvironment="false" />  
            </DirectoryConfiguration>  
            <DirectoryConfiguration containerName="badapp">  
              <Absolute path="%SYSTEMDRIVE%\BadApp" expandEnvironment="true" />  
            </DirectoryConfiguration>  
            <DirectoryConfiguration containerName="goodapp">  
              <LocalResource name="Skippy" relativePath="..\PeanutButter"/>  
            </DirectoryConfiguration>  
          </DataSources>  

        </Directories>  

        <EtwProviders>  
          <EtwEventSourceProviderConfiguration   
                       provider="MyProviderClass"   
                       scheduledTransferPeriod="PT5M">  
            <Event id="0"/>  
            <Event id="1" eventDestination="errorTable"/>  
            <DefaultEvents />  
          </EtwEventSourceProviderConfiguration>  
          <EtwManifestProviderConfiguration provider="5974b00b-84c2-44bc-9e58-3a2451b4e3ad" scheduledTransferLogLevelFilter="Information" scheduledTransferPeriod="PT2M">  
            <Event id="0"/>  
            <DefaultEvents eventDestination="defaultTable"/>  
          </EtwManifestProviderConfiguration>  
        </EtwProviders>  

        <WindowsEventLog scheduledTransferPeriod="PT5M">  
          <DataSource name="System!*[System[Provider[@Name='Microsoft Antimalware']]]"/>  
          <DataSource name="System!*[System[Provider[@Name='NTFS'] and (EventID=55)]]" />  
          <DataSource name="System!*[System[Provider[@Name='disk'] and (EventID=7 or EventID=52 or EventID=55)]]" />  
        </WindowsEventLog>  

        <Logs  bufferQuotaInMB="1024"   
             scheduledTransferPeriod="PT1M"   
             scheduledTransferLogLevelFilter="Verbose"   
             sinks="ApplicationInsights.AppLogs"/>  <!-- sinks attribute added in 1.5 -->  

        <CrashDumps containerName="wad-crashdumps" directoryQuotaPercentage="30" dumpType="Mini">  
          <CrashDumpConfiguration processName="mynewprocess.exe" />  
          <CrashDumpConfiguration processName="badapp.exe"/>  
        </CrashDumps>  

        <DockerSources> <!-- Added in 1.9 --> 
          <Stats enabled="true" sampleRate="PT1M" scheduledTransferPeriod="PT1M" />
        </DockerSources>

      </DiagnosticMonitorConfiguration>  

      <SinksConfig>   <!-- Added in 1.5 -->  
        <Sink name="ApplicationInsights">   
          <ApplicationInsights>{Insert InstrumentationKey}</ApplicationInsights>   
          <Channels>   
            <Channel logLevel="Error" name="Errors"  />   
            <Channel logLevel="Verbose" name="AppLogs"  />   
          </Channels>   
        </Sink>   
        <Sink name="EventHub"> <!-- Added in 1.7 -->
          <EventHub Url="https://myeventhub-ns.servicebus.windows.net/diageventhub" SharedAccessKeyName="SendRule" usePublisherId="false" />
        </Sink>
        <Sink name="secondaryEventHub"> <!-- Added in 1.7 -->
          <EventHub Url="https://myeventhub-ns.servicebus.windows.net/secondarydiageventhub" SharedAccessKeyName="SendRule" usePublisherId="false" />
        </Sink>
        <Sink name="secondaryStorageAccount"> <!-- Added in 1.7 -->
          <StorageAccount name="secondarydiagstorageaccount" endpoint="https://core.windows.net" />
        </Sink>
   </SinksConfig>

  </WadCfg>  

  <StorageAccount>diagstorageaccount</StorageAccount>
  <StorageType>TableAndBlob</StorageType> <!-- Added in 1.8 -->  
  </PublicConfig>  

  <PrivateConfig>  <!-- Added in 1.3 -->  
    <StorageAccount name="" key="" endpoint="" sasToken="{sas token}"  />  <!-- sasToken in Private config added in 1.8.1 -->  
    <EventHub Url="https://myeventhub-ns.servicebus.windows.net/diageventhub" SharedAccessKeyName="SendRule" SharedAccessKey="{base64 encoded key}" />
   
    <SecondaryStorageAccounts>
       <StorageAccount name="secondarydiagstorageaccount" key="{base64 encoded key}" endpoint="https://core.windows.net" sasToken="{sas token}" />
    </SecondaryStorageAccounts>
   
    <SecondaryEventHubs>
       <EventHub Url="https://myeventhub-ns.servicebus.windows.net/secondarydiageventhub" SharedAccessKeyName="SendRule" SharedAccessKey="{base64 encoded key}" />
    </SecondaryEventHubs>

  </PrivateConfig>  
  <IsEnabled>true</IsEnabled>  
</DiagnosticsConfiguration>  

```  

<span data-ttu-id="a6293-119">Merhaba önceki XML yapılandırma dosyası denk JSON.</span><span class="sxs-lookup"><span data-stu-id="a6293-119">JSON equivalent of hello previous XML configuration file.</span></span> 

<span data-ttu-id="a6293-120">json kullanımı genellikle farklı değişkenleri olarak geçirilen çünkü hello PublicConfig ve PrivateConfig ayrılır.</span><span class="sxs-lookup"><span data-stu-id="a6293-120">hello PublicConfig and PrivateConfig are separated because in most json usage cases, they are passed as different variables.</span></span> <span data-ttu-id="a6293-121">Bu durumlar: Resource Manager şablonları, PowerShell ve Visual Studio sanal makine ölçek kümesi.</span><span class="sxs-lookup"><span data-stu-id="a6293-121">These cases include Resource Manager templates, Virtual Machine Scale set PowerShell, and Visual Studio.</span></span> 

```json
"PublicConfig" {
    "WadCfg": {
        "DiagnosticMonitorConfiguration": {
            "overallQuotaInMB": 10000,
            "DiagnosticInfrastructureLogs": {
                "scheduledTransferLogLevelFilter": "Error"
            },
            "PerformanceCounters": {
                "scheduledTransferPeriod": "PT1M",
                "PerformanceCounterConfiguration": [
                    {
                        "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
                        "sampleRate": "PT1M",
                        "unit": "percent"
                    }
                ]
            },
            "Directories": {
                "scheduledTransferPeriod": "PT5M",
                "IISLogs": {
                    "containerName": "iislogs"
                },
                "FailedRequestLogs": {
                    "containerName": "iisfailed"
                },
                "DataSources": [
                    {
                        "containerName": "mynewprocess",
                        "Absolute": {
                            "path": "C:\\MyNewProcess",
                            "expandEnvironment": false
                        }
                    },
                    {
                        "containerName": "badapp",
                        "Absolute": {
                            "path": "%SYSTEMDRIVE%\\BadApp",
                            "expandEnvironment": true
                        }
                    },
                    {
                        "containerName": "goodapp",
                        "LocalResource": {
                            "relativePath": "..\\PeanutButter",
                            "name": "Skippy"
                        }
                    }
                ]
            },
            "EtwProviders": {
                "sinks": "",
                "EtwEventSourceProviderConfiguration": [
                    {
                        "scheduledTransferPeriod": "PT5M",
                        "provider": "MyProviderClass",
                        "Event": [
                            {
                                "id": 0
                            },
                            {
                                "id": 1,
                                "eventDestination": "errorTable"
                            }
                        ],
                        "DefaultEvents": {
                        }
                    }
                ],
                "EtwManifestProviderConfiguration": [
                    {
                        "scheduledTransferPeriod": "PT2M",
                        "scheduledTransferLogLevelFilter": "Information",
                        "provider": "5974b00b-84c2-44bc-9e58-3a2451b4e3ad",
                        "Event": [
                            {
                                "id": 0
                            }
                        ],
                        "DefaultEvents": {
                        }
                    }
                ]
            },
            "WindowsEventLog": {
                "scheduledTransferPeriod": "PT5M",
                "DataSource": [
                    {
                        "name": "System!*[System[Provider[@Name='Microsoft Antimalware']]]"
                    },
                    {
                        "name": "System!*[System[Provider[@Name='NTFS'] and (EventID=55)]]"
                    },
                    {
                        "name": "System!*[System[Provider[@Name='disk'] and (EventID=7 or EventID=52 or EventID=55)]]"
                    }
                ]
            },
            "Logs": {
                "scheduledTransferPeriod": "PT1M",
                "scheduledTransferLogLevelFilter": "Verbose",
                "sinks": "ApplicationInsights.AppLogs"
            },
            "CrashDumps": {
                "directoryQuotaPercentage": 30,
                "dumpType": "Mini",
                "containerName": "wad-crashdumps",
                "CrashDumpConfiguration": [
                    {
                        "processName": "mynewprocess.exe"
                    },
                    {
                        "processName": "badapp.exe"
                    }
                ]
            }
        },
        "SinksConfig": {
            "Sink": [
                {
                    "name": "ApplicationInsights",
                    "ApplicationInsights": "{Insert InstrumentationKey}",
                    "Channels": {
                        "Channel": [
                            {
                                "logLevel": "Error",
                                "name": "Errors"
                            },
                            {
                                "logLevel": "Verbose",
                                "name": "AppLogs"
                            }
                        ]
                    }
                },
                {
                    "name": "EventHub",
                    "EventHub": {
                        "Url": "https://myeventhub-ns.servicebus.windows.net/diageventhub",
                        "SharedAccessKeyName": "SendRule",
                        "usePublisherId": false
                    }
                },
                {
                    "name": "secondaryEventHub",
                    "EventHub": {
                        "Url": "https://myeventhub-ns.servicebus.windows.net/secondarydiageventhub",
                        "SharedAccessKeyName": "SendRule",
                        "usePublisherId": false
                    }
                },
                {
                    "name": "secondaryStorageAccount",
                    "StorageAccount": {
                        "name": "secondarydiagstorageaccount",
                        "endpoint": "https://core.windows.net"
                    }
                }
            ]
        }
    },
    "StorageAccount": "diagstorageaccount",
    "StorageType": "TableAndBlob"
}
```

```json
"PrivateConfig" {
    "storageAccountName": "diagstorageaccount",
    "storageAccountKey": "{base64 encoded key}",
    "storageAccountEndPoint": "https://core.windows.net",
    "storageAccountSasToken": "{sas token}",
    "EventHub": {
        "Url": "https://myeventhub-ns.servicebus.windows.net/diageventhub",
        "SharedAccessKeyName": "SendRule",
        "SharedAccessKey": "{base64 encoded key}"
    },
    "SecondaryStorageAccounts": {
        "StorageAccount": [
            {
                "name": "secondarydiagstorageaccount",
                "key": "{base64 encoded key}",
                "endpoint": "https://core.windows.net",
                "sasToken": "{sas token}"
            }
        ]
    },
    "SecondaryEventHubs": {
        "EventHub": [
            {
                "Url": "https://myeventhub-ns.servicebus.windows.net/secondarydiageventhub",
                "SharedAccessKeyName": "SendRule",
                "SharedAccessKey": "{base64 encoded key}"
            }
        ]
    }
}

```

## <a name="reading-this-page"></a><span data-ttu-id="a6293-122">Bu sayfa okuma</span><span class="sxs-lookup"><span data-stu-id="a6293-122">Reading this page</span></span>  
 <span data-ttu-id="a6293-123">Merhaba aşağıdaki kabaca hello önceki örnekte gösterilen sırada etiketleridir.</span><span class="sxs-lookup"><span data-stu-id="a6293-123">hello tags following are roughly in order shown in hello preceding example.</span></span>  <span data-ttu-id="a6293-124">Tam açıklama beklediğiniz burada görmüyorsanız, arama hello öğesi veya özniteliği için hello sayfası.</span><span class="sxs-lookup"><span data-stu-id="a6293-124">If you don't see a full description where you expect it, search hello page for hello element or attribute.</span></span>  

## <a name="common-attribute-types"></a><span data-ttu-id="a6293-125">Ortak öznitelik türleri</span><span class="sxs-lookup"><span data-stu-id="a6293-125">Common Attribute Types</span></span>  
 <span data-ttu-id="a6293-126">**scheduledTransferPeriod** özniteliği birkaç öğelerinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="a6293-126">**scheduledTransferPeriod** attribute appears in several elements.</span></span> <span data-ttu-id="a6293-127">Bu zamanlanmış aktarımları toostorage toohello minute en yakın yukarı yuvarlanmasını hello aralığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="a6293-127">It is hello interval between scheduled transfers toostorage rounded up toohello nearest minute.</span></span> <span data-ttu-id="a6293-128">Merhaba değeri bir [XML "Süre veri türü."](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="a6293-128">hello value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span>


## <a name="diagnosticsconfiguration-element"></a><span data-ttu-id="a6293-129">DiagnosticsConfiguration öğesi</span><span class="sxs-lookup"><span data-stu-id="a6293-129">DiagnosticsConfiguration Element</span></span>  
 <span data-ttu-id="a6293-130">*Ağaç: Kök - DiagnosticsConfiguration*</span><span class="sxs-lookup"><span data-stu-id="a6293-130">*Tree: Root - DiagnosticsConfiguration*</span></span>

<span data-ttu-id="a6293-131">Sürüm 1.3 eklendi.</span><span class="sxs-lookup"><span data-stu-id="a6293-131">Added in version 1.3.</span></span>  

<span data-ttu-id="a6293-132">Merhaba hello tanılama yapılandırma dosyasının en üst düzey öğesi.</span><span class="sxs-lookup"><span data-stu-id="a6293-132">hello top-level element of hello diagnostics configuration file.</span></span>  

<span data-ttu-id="a6293-133">**Öznitelik** xmlns - hello tanılama yapılandırma dosyası için XML ad alanı hello:</span><span class="sxs-lookup"><span data-stu-id="a6293-133">**Attribute**  xmlns - hello XML namespace for hello diagnostics configuration file is:</span></span>  
<span data-ttu-id="a6293-134">http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration</span><span class="sxs-lookup"><span data-stu-id="a6293-134">http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration</span></span>  


|<span data-ttu-id="a6293-135">Alt öğeler</span><span class="sxs-lookup"><span data-stu-id="a6293-135">Child Elements</span></span>|<span data-ttu-id="a6293-136">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a6293-136">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="a6293-137">**PublicConfig**</span><span class="sxs-lookup"><span data-stu-id="a6293-137">**PublicConfig**</span></span>|<span data-ttu-id="a6293-138">Gereklidir.</span><span class="sxs-lookup"><span data-stu-id="a6293-138">Required.</span></span> <span data-ttu-id="a6293-139">Açıklama, bu sayfada başka bir yerde bakın.</span><span class="sxs-lookup"><span data-stu-id="a6293-139">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="a6293-140">**PrivateConfig**</span><span class="sxs-lookup"><span data-stu-id="a6293-140">**PrivateConfig**</span></span>|<span data-ttu-id="a6293-141">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="a6293-141">Optional.</span></span> <span data-ttu-id="a6293-142">Açıklama, bu sayfada başka bir yerde bakın.</span><span class="sxs-lookup"><span data-stu-id="a6293-142">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="a6293-143">**IsEnabled**</span><span class="sxs-lookup"><span data-stu-id="a6293-143">**IsEnabled**</span></span>|<span data-ttu-id="a6293-144">Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="a6293-144">Boolean.</span></span> <span data-ttu-id="a6293-145">Açıklama, bu sayfada başka bir yerde bakın.</span><span class="sxs-lookup"><span data-stu-id="a6293-145">See description elsewhere on this page.</span></span>|  

## <a name="publicconfig-element"></a><span data-ttu-id="a6293-146">PublicConfig öğesi</span><span class="sxs-lookup"><span data-stu-id="a6293-146">PublicConfig Element</span></span>  
 <span data-ttu-id="a6293-147">*Ağaç: Kök - DiagnosticsConfiguration - PublicConfig*</span><span class="sxs-lookup"><span data-stu-id="a6293-147">*Tree: Root - DiagnosticsConfiguration - PublicConfig*</span></span>

 <span data-ttu-id="a6293-148">Merhaba genel tanılama yapılandırması açıklar.</span><span class="sxs-lookup"><span data-stu-id="a6293-148">Describes hello public diagnostics configuration.</span></span>  

|<span data-ttu-id="a6293-149">Alt öğeler</span><span class="sxs-lookup"><span data-stu-id="a6293-149">Child Elements</span></span>|<span data-ttu-id="a6293-150">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a6293-150">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="a6293-151">**WadCfg**</span><span class="sxs-lookup"><span data-stu-id="a6293-151">**WadCfg**</span></span>|<span data-ttu-id="a6293-152">Gereklidir.</span><span class="sxs-lookup"><span data-stu-id="a6293-152">Required.</span></span> <span data-ttu-id="a6293-153">Açıklama, bu sayfada başka bir yerde bakın.</span><span class="sxs-lookup"><span data-stu-id="a6293-153">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="a6293-154">**StorageAccount**</span><span class="sxs-lookup"><span data-stu-id="a6293-154">**StorageAccount**</span></span>|<span data-ttu-id="a6293-155">hello Azure depolama hesabı toostore hello verilerde Hello adı.</span><span class="sxs-lookup"><span data-stu-id="a6293-155">hello name of hello Azure Storage account toostore hello data in.</span></span> <span data-ttu-id="a6293-156">Ayrıca bir parametre olarak hello kümesi AzureServiceDiagnosticsExtension cmdlet'ini çalıştırırken belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="a6293-156">May also be specified as a parameter when executing hello Set-AzureServiceDiagnosticsExtension cmdlet.</span></span>|  
|<span data-ttu-id="a6293-157">**StorageType**</span><span class="sxs-lookup"><span data-stu-id="a6293-157">**StorageType**</span></span>|<span data-ttu-id="a6293-158">Olabilir *tablo*, *Blob*, veya *TableAndBlob*.</span><span class="sxs-lookup"><span data-stu-id="a6293-158">Can be *Table*, *Blob*, or *TableAndBlob*.</span></span> <span data-ttu-id="a6293-159">Tablo varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="a6293-159">Table is default.</span></span> <span data-ttu-id="a6293-160">TableAndBlob seçildiğinde Tanılama verileri iki kez--tooeach türü kez yazılır.</span><span class="sxs-lookup"><span data-stu-id="a6293-160">When TableAndBlob is chosen, diagnostic data is written twice -- once tooeach type.</span></span>|  
|<span data-ttu-id="a6293-161">**LocalResourceDirectory**</span><span class="sxs-lookup"><span data-stu-id="a6293-161">**LocalResourceDirectory**</span></span>|<span data-ttu-id="a6293-162">Hello dizin hello sanal makineye burada hello Monitoring Agent olay verilerini depolar.</span><span class="sxs-lookup"><span data-stu-id="a6293-162">hello directory on hello virtual machine where hello Monitoring Agent stores event data.</span></span> <span data-ttu-id="a6293-163">Aksi takdirde, ayarlanırsa, hello varsayılan dizin kullanılır:</span><span class="sxs-lookup"><span data-stu-id="a6293-163">If not, set, hello default directory is used:</span></span><br /><br /> <span data-ttu-id="a6293-164">Worker/web rolü için:`C:\Resources\<guid>\directory\<guid>.<RoleName.DiagnosticStore\`</span><span class="sxs-lookup"><span data-stu-id="a6293-164">For a Worker/web role: `C:\Resources\<guid>\directory\<guid>.<RoleName.DiagnosticStore\`</span></span><br /><br /> <span data-ttu-id="a6293-165">Bir sanal makine için:`C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<WADVersion>\WAD<WADVersion>`</span><span class="sxs-lookup"><span data-stu-id="a6293-165">For a Virtual Machine: `C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<WADVersion>\WAD<WADVersion>`</span></span><br /><br /> <span data-ttu-id="a6293-166">Gerekli öznitelikler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="a6293-166">Required attributes are:</span></span><br /><br /> <span data-ttu-id="a6293-167">- **yol** - hello Azure tanılama tarafından kullanılan hello sistem toobe dizininde.</span><span class="sxs-lookup"><span data-stu-id="a6293-167">- **path** - hello directory on hello system toobe used by Azure Diagnostics.</span></span><br /><br /> <span data-ttu-id="a6293-168">- **expandEnvironment** -ortam değişkenleri hello yol adında genişletilmiş olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="a6293-168">- **expandEnvironment** - Controls whether environment variables are expanded in hello path name.</span></span>|  

## <a name="wadcfg-element"></a><span data-ttu-id="a6293-169">WadCFG öğesi</span><span class="sxs-lookup"><span data-stu-id="a6293-169">WadCFG Element</span></span>  
 <span data-ttu-id="a6293-170">*Ağaç: Kök - DiagnosticsConfiguration - PublicConfig - WadCFG*</span><span class="sxs-lookup"><span data-stu-id="a6293-170">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG*</span></span>
 
 <span data-ttu-id="a6293-171">Tanımlar ve toplanan hello telemetri verileri toobe yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="a6293-171">Identifies and configures hello telemetry data toobe collected.</span></span>  


## <a name="diagnosticmonitorconfiguration-element"></a><span data-ttu-id="a6293-172">DiagnosticMonitorConfiguration öğesi</span><span class="sxs-lookup"><span data-stu-id="a6293-172">DiagnosticMonitorConfiguration Element</span></span> 
 <span data-ttu-id="a6293-173">*Ağaç: Kök - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration*</span><span class="sxs-lookup"><span data-stu-id="a6293-173">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration*</span></span>

 <span data-ttu-id="a6293-174">Gerekli</span><span class="sxs-lookup"><span data-stu-id="a6293-174">Required</span></span> 

|<span data-ttu-id="a6293-175">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="a6293-175">Attributes</span></span>|<span data-ttu-id="a6293-176">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a6293-176">Description</span></span>|  
|----------------|-----------------|  
| <span data-ttu-id="a6293-177">**overallQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="a6293-177">**overallQuotaInMB**</span></span> | <span data-ttu-id="a6293-178">Merhaba maksimum hello tarafından tüketilen yerel disk alanı miktarını çeşitli tanılama veri türlerine Azure tanılama tarafından toplanan.</span><span class="sxs-lookup"><span data-stu-id="a6293-178">hello maximum amount of local disk space that may be consumed by hello various types of diagnostic data collected by Azure Diagnostics.</span></span> <span data-ttu-id="a6293-179">Merhaba varsayılan ayar 5120 MB'tır.</span><span class="sxs-lookup"><span data-stu-id="a6293-179">hello default setting is 5120 MB.</span></span><br />
|<span data-ttu-id="a6293-180">**useProxyServer**</span><span class="sxs-lookup"><span data-stu-id="a6293-180">**useProxyServer**</span></span> | <span data-ttu-id="a6293-181">IE ayarlarının kümesinde olarak Azure tanılama toouse hello proxy sunucusu ayarlarını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="a6293-181">Configure Azure Diagnostics toouse hello proxy server settings as set in IE settings.</span></span>|  

<br /> <br />

|<span data-ttu-id="a6293-182">Alt öğeler</span><span class="sxs-lookup"><span data-stu-id="a6293-182">Child Elements</span></span>|<span data-ttu-id="a6293-183">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a6293-183">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="a6293-184">**CrashDumps**</span><span class="sxs-lookup"><span data-stu-id="a6293-184">**CrashDumps**</span></span>|<span data-ttu-id="a6293-185">Açıklama, bu sayfada başka bir yerde bakın.</span><span class="sxs-lookup"><span data-stu-id="a6293-185">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="a6293-186">**DiagnosticInfrastructureLogs**</span><span class="sxs-lookup"><span data-stu-id="a6293-186">**DiagnosticInfrastructureLogs**</span></span>|<span data-ttu-id="a6293-187">Azure tanılama tarafından oluşturulan günlükleri koleksiyonunu etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="a6293-187">Enable collection of logs generated by Azure Diagnostics.</span></span> <span data-ttu-id="a6293-188">Merhaba Tanılama Altyapısı günlükleri hello tanılama sistem kendisini sorun giderme için yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="a6293-188">hello diagnostic infrastructure logs are useful for troubleshooting hello diagnostics system itself.</span></span> <span data-ttu-id="a6293-189">İsteğe bağlı öznitelikleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="a6293-189">Optional attributes are:</span></span><br /><br /> <span data-ttu-id="a6293-190">- **scheduledTransferLogLevelFilter** -toplanan hello günlüklerini hello en düşük önem derecesi yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="a6293-190">- **scheduledTransferLogLevelFilter** - Configures hello minimum severity level of hello logs collected.</span></span><br /><br /> <span data-ttu-id="a6293-191">- **scheduledTransferPeriod** -toohello minute en yakın yuvarlanan zamanlanmış aktarımları toostorage hello aralığıdır.</span><span class="sxs-lookup"><span data-stu-id="a6293-191">- **scheduledTransferPeriod** - hello interval between scheduled transfers toostorage rounded up toohello nearest minute.</span></span> <span data-ttu-id="a6293-192">Merhaba değeri bir [XML "Süre veri türü."](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="a6293-192">hello value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  
|<span data-ttu-id="a6293-193">**Dizinleri**</span><span class="sxs-lookup"><span data-stu-id="a6293-193">**Directories**</span></span>|<span data-ttu-id="a6293-194">Açıklama, bu sayfada başka bir yerde bakın.</span><span class="sxs-lookup"><span data-stu-id="a6293-194">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="a6293-195">**EtwProviders**</span><span class="sxs-lookup"><span data-stu-id="a6293-195">**EtwProviders**</span></span>|<span data-ttu-id="a6293-196">Açıklama, bu sayfada başka bir yerde bakın.</span><span class="sxs-lookup"><span data-stu-id="a6293-196">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="a6293-197">**Ölçümler**</span><span class="sxs-lookup"><span data-stu-id="a6293-197">**Metrics**</span></span>|<span data-ttu-id="a6293-198">Açıklama, bu sayfada başka bir yerde bakın.</span><span class="sxs-lookup"><span data-stu-id="a6293-198">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="a6293-199">**Performans sayaçları**</span><span class="sxs-lookup"><span data-stu-id="a6293-199">**PerformanceCounters**</span></span>|<span data-ttu-id="a6293-200">Açıklama, bu sayfada başka bir yerde bakın.</span><span class="sxs-lookup"><span data-stu-id="a6293-200">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="a6293-201">**WindowsEventLog**</span><span class="sxs-lookup"><span data-stu-id="a6293-201">**WindowsEventLog**</span></span>|<span data-ttu-id="a6293-202">Açıklama, bu sayfada başka bir yerde bakın.</span><span class="sxs-lookup"><span data-stu-id="a6293-202">See description elsewhere on this page.</span></span>| 
|<span data-ttu-id="a6293-203">**DockerSources**</span><span class="sxs-lookup"><span data-stu-id="a6293-203">**DockerSources**</span></span>|<span data-ttu-id="a6293-204">Açıklama, bu sayfada başka bir yerde bakın.</span><span class="sxs-lookup"><span data-stu-id="a6293-204">See description elsewhere on this page.</span></span> | 



## <a name="crashdumps-element"></a><span data-ttu-id="a6293-205">CrashDumps öğesi</span><span class="sxs-lookup"><span data-stu-id="a6293-205">CrashDumps Element</span></span>  
 <span data-ttu-id="a6293-206">*Ağaç: Kök - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - CrashDumps*</span><span class="sxs-lookup"><span data-stu-id="a6293-206">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - CrashDumps*</span></span>
 
 <span data-ttu-id="a6293-207">Kilitlenme bilgi dökümleri Hello koleksiyonunu etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="a6293-207">Enable hello collection of crash dumps.</span></span>  

|<span data-ttu-id="a6293-208">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="a6293-208">Attributes</span></span>|<span data-ttu-id="a6293-209">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a6293-209">Description</span></span>|  
|----------------|-----------------|  
|<span data-ttu-id="a6293-210">**kapsayıcı adı**</span><span class="sxs-lookup"><span data-stu-id="a6293-210">**containerName**</span></span>|<span data-ttu-id="a6293-211">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="a6293-211">Optional.</span></span> <span data-ttu-id="a6293-212">toostore kilitlenme bilgi dökümleri kullanılan Azure Storage hesabı toobe hello blob kapsayıcısında Hello adı.</span><span class="sxs-lookup"><span data-stu-id="a6293-212">hello name of hello blob container in your Azure Storage account toobe used toostore crash dumps.</span></span>|  
|<span data-ttu-id="a6293-213">**crashDumpType**</span><span class="sxs-lookup"><span data-stu-id="a6293-213">**crashDumpType**</span></span>|<span data-ttu-id="a6293-214">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="a6293-214">Optional.</span></span>  <span data-ttu-id="a6293-215">Azure tanılama toocollect mini ya da tam kilitlenme dökümleri yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="a6293-215">Configures Azure Diagnostics toocollect mini or full crash dumps.</span></span>|  
|<span data-ttu-id="a6293-216">**directoryQuotaPercentage**</span><span class="sxs-lookup"><span data-stu-id="a6293-216">**directoryQuotaPercentage**</span></span>|<span data-ttu-id="a6293-217">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="a6293-217">Optional.</span></span>  <span data-ttu-id="a6293-218">Merhaba yüzdesini yapılandırır **overallQuotaInMB** toobe hello VM üzerinde kilitlenme dökümleri için ayrılmış.</span><span class="sxs-lookup"><span data-stu-id="a6293-218">Configures hello percentage of **overallQuotaInMB** toobe reserved for crash dumps on hello VM.</span></span>|  

|<span data-ttu-id="a6293-219">Alt öğeler</span><span class="sxs-lookup"><span data-stu-id="a6293-219">Child Elements</span></span>|<span data-ttu-id="a6293-220">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a6293-220">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="a6293-221">**CrashDumpConfiguration**</span><span class="sxs-lookup"><span data-stu-id="a6293-221">**CrashDumpConfiguration**</span></span>|<span data-ttu-id="a6293-222">Gereklidir.</span><span class="sxs-lookup"><span data-stu-id="a6293-222">Required.</span></span> <span data-ttu-id="a6293-223">Her işlem için yapılandırma değerlerini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="a6293-223">Defines configuration values for each process.</span></span><br /><br /> <span data-ttu-id="a6293-224">özniteliği aşağıdaki hello de gereklidir:</span><span class="sxs-lookup"><span data-stu-id="a6293-224">hello following attribute is also required:</span></span><br /><br /> <span data-ttu-id="a6293-225">**işlemadı** - hello kilitlenme dökümü için kullanmak istediğiniz Azure tanılama toocollect hello işlemin adı.</span><span class="sxs-lookup"><span data-stu-id="a6293-225">**processName** - hello name of hello process you want Azure Diagnostics toocollect a crash dump for.</span></span>|  

## <a name="directories-element"></a><span data-ttu-id="a6293-226">Dizinleri öğesi</span><span class="sxs-lookup"><span data-stu-id="a6293-226">Directories Element</span></span> 
 <span data-ttu-id="a6293-227">*Ağaç: Kök - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - dizinler*</span><span class="sxs-lookup"><span data-stu-id="a6293-227">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration -  Directories*</span></span>

 <span data-ttu-id="a6293-228">Bir dizinin içeriğini hello koleksiyonunu etkinleştirir Merhaba, IIS erişim isteği günlükleri ve/veya IIS günlüklerini başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="a6293-228">Enables hello collection of hello contents of a directory, IIS failed access request logs and/or IIS logs.</span></span>  

 <span data-ttu-id="a6293-229">İsteğe bağlı **scheduledTransferPeriod** özniteliği.</span><span class="sxs-lookup"><span data-stu-id="a6293-229">Optional **scheduledTransferPeriod** attribute.</span></span> <span data-ttu-id="a6293-230">Daha önce açıklama konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="a6293-230">See explanation earlier.</span></span>  

|<span data-ttu-id="a6293-231">Alt öğeler</span><span class="sxs-lookup"><span data-stu-id="a6293-231">Child Elements</span></span>|<span data-ttu-id="a6293-232">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a6293-232">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="a6293-233">**IISLogs**</span><span class="sxs-lookup"><span data-stu-id="a6293-233">**IISLogs**</span></span>|<span data-ttu-id="a6293-234">Bu öğe hello yapılandırmasında dahil olmak üzere IIS günlüklerini hello koleksiyonunu sağlar:</span><span class="sxs-lookup"><span data-stu-id="a6293-234">Including this element in hello configuration enables hello collection of IIS logs:</span></span><br /><br /> <span data-ttu-id="a6293-235">**kapsayıcı adı** -toostore hello IIS günlüklerini kullanılan Azure Storage hesabı toobe hello blob kapsayıcısında hello adı.</span><span class="sxs-lookup"><span data-stu-id="a6293-235">**containerName** - hello name of hello blob container in your Azure Storage account toobe used toostore hello IIS logs.</span></span>|   
|<span data-ttu-id="a6293-236">**FailedRequestLogs**</span><span class="sxs-lookup"><span data-stu-id="a6293-236">**FailedRequestLogs**</span></span>|<span data-ttu-id="a6293-237">Bu öğe hello yapılandırmasında dahil olmak üzere başarısız isteklerin tooan IIS siteniz veya uygulamanız hakkında günlükleri koleksiyonunu sağlar.</span><span class="sxs-lookup"><span data-stu-id="a6293-237">Including this element in hello configuration enables collection of logs about failed requests tooan IIS site or application.</span></span> <span data-ttu-id="a6293-238">İzleme seçenekleri altında da etkinleştirmeniz gerekir **sistem. Web sunucusu** içinde **Web.config**.</span><span class="sxs-lookup"><span data-stu-id="a6293-238">You must also enable tracing options under **system.WebServer** in **Web.config**.</span></span>|  
|<span data-ttu-id="a6293-239">**Veri kaynakları**</span><span class="sxs-lookup"><span data-stu-id="a6293-239">**DataSources**</span></span>|<span data-ttu-id="a6293-240">Dizinleri toomonitor listesi.</span><span class="sxs-lookup"><span data-stu-id="a6293-240">A list of directories toomonitor.</span></span>| 




## <a name="datasources-element"></a><span data-ttu-id="a6293-241">Veri kaynakları öğesi</span><span class="sxs-lookup"><span data-stu-id="a6293-241">DataSources Element</span></span>  
 <span data-ttu-id="a6293-242">*Ağaç: Kök - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - dizinlere - veri kaynakları*</span><span class="sxs-lookup"><span data-stu-id="a6293-242">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources*</span></span>

 <span data-ttu-id="a6293-243">Dizinleri toomonitor listesi.</span><span class="sxs-lookup"><span data-stu-id="a6293-243">A list of directories toomonitor.</span></span>  

|<span data-ttu-id="a6293-244">Alt öğeler</span><span class="sxs-lookup"><span data-stu-id="a6293-244">Child Elements</span></span>|<span data-ttu-id="a6293-245">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a6293-245">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="a6293-246">**DirectoryConfiguration**</span><span class="sxs-lookup"><span data-stu-id="a6293-246">**DirectoryConfiguration**</span></span>|<span data-ttu-id="a6293-247">Gereklidir.</span><span class="sxs-lookup"><span data-stu-id="a6293-247">Required.</span></span> <span data-ttu-id="a6293-248">Gerekli öznitelik:</span><span class="sxs-lookup"><span data-stu-id="a6293-248">Required attribute:</span></span><br /><br /> <span data-ttu-id="a6293-249">**kapsayıcı adı** - hello hello bu toobe kullanılan toostore hello günlük dosyaları Azure depolama hesabınızdaki blob kapsayıcısının adı.</span><span class="sxs-lookup"><span data-stu-id="a6293-249">**containerName** - hello name of hello blob container in your Azure Storage account that toobe used toostore hello log files.</span></span>|  





## <a name="directoryconfiguration-element"></a><span data-ttu-id="a6293-250">DirectoryConfiguration öğesi</span><span class="sxs-lookup"><span data-stu-id="a6293-250">DirectoryConfiguration Element</span></span>  
 <span data-ttu-id="a6293-251">*Ağaç: Kök - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - dizinlere - veri kaynakları - DirectoryConfiguration*</span><span class="sxs-lookup"><span data-stu-id="a6293-251">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources - DirectoryConfiguration*</span></span>

 <span data-ttu-id="a6293-252">Her iki hello içerebilir **mutlak** veya **LocalResource** öğesi ikisini birden belirtmeyin.</span><span class="sxs-lookup"><span data-stu-id="a6293-252">May include either hello **Absolute** or **LocalResource** element but not both.</span></span>  

|<span data-ttu-id="a6293-253">Alt öğeler</span><span class="sxs-lookup"><span data-stu-id="a6293-253">Child Elements</span></span>|<span data-ttu-id="a6293-254">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a6293-254">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="a6293-255">**Mutlak**</span><span class="sxs-lookup"><span data-stu-id="a6293-255">**Absolute**</span></span>|<span data-ttu-id="a6293-256">mutlak yol toohello directory toomonitor hello.</span><span class="sxs-lookup"><span data-stu-id="a6293-256">hello absolute path toohello directory toomonitor.</span></span> <span data-ttu-id="a6293-257">Aşağıdaki öznitelikler hello gereklidir:</span><span class="sxs-lookup"><span data-stu-id="a6293-257">hello following attributes are required:</span></span><br /><br /> <span data-ttu-id="a6293-258">- **Yol** -mutlak bir yol toohello directory toomonitor hello.</span><span class="sxs-lookup"><span data-stu-id="a6293-258">- **Path** - hello absolute path toohello directory toomonitor.</span></span><br /><br /> <span data-ttu-id="a6293-259">- **expandEnvironment** -Path ortam değişkenleri genişletilmiş olup olmadığını yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="a6293-259">- **expandEnvironment** - Configures whether environment variables in Path are expanded.</span></span>|  
|<span data-ttu-id="a6293-260">**LocalResource**</span><span class="sxs-lookup"><span data-stu-id="a6293-260">**LocalResource**</span></span>|<span data-ttu-id="a6293-261">Merhaba yolu göreli tooa yerel kaynak toomonitor.</span><span class="sxs-lookup"><span data-stu-id="a6293-261">hello path relative tooa local resource toomonitor.</span></span> <span data-ttu-id="a6293-262">Gerekli öznitelikler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="a6293-262">Required attributes are:</span></span><br /><br /> <span data-ttu-id="a6293-263">- **Ad** -hello hello dizin toomonitor içeren yerel kaynak</span><span class="sxs-lookup"><span data-stu-id="a6293-263">- **Name** - hello local resource that contains hello directory toomonitor</span></span><br /><br /> <span data-ttu-id="a6293-264">- **relativePath** -hello dizin toomonitor içeren yolu göreli tooName hello</span><span class="sxs-lookup"><span data-stu-id="a6293-264">- **relativePath** - hello path relative tooName that contains hello directory toomonitor</span></span>|  



## <a name="etwproviders-element"></a><span data-ttu-id="a6293-265">EtwProviders öğesi</span><span class="sxs-lookup"><span data-stu-id="a6293-265">EtwProviders Element</span></span>  
 <span data-ttu-id="a6293-266">*Ağaç: Kök - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders*</span><span class="sxs-lookup"><span data-stu-id="a6293-266">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders*</span></span>

 <span data-ttu-id="a6293-267">EventSource ETW olayları koleksiyonu yapılandırır ve/veya ETW bildirim dayalı sağlayıcıları.</span><span class="sxs-lookup"><span data-stu-id="a6293-267">Configures collection of ETW events from EventSource and/or ETW Manifest based providers.</span></span>  

|<span data-ttu-id="a6293-268">Alt öğeler</span><span class="sxs-lookup"><span data-stu-id="a6293-268">Child Elements</span></span>|<span data-ttu-id="a6293-269">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a6293-269">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="a6293-270">**EtwEventSourceProviderConfiguration**</span><span class="sxs-lookup"><span data-stu-id="a6293-270">**EtwEventSourceProviderConfiguration**</span></span>|<span data-ttu-id="a6293-271">Koleksiyon üretilen olayların yapılandırır [EventSource sınıfı](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="a6293-271">Configures collection of events generated from [EventSource Class](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span></span> <span data-ttu-id="a6293-272">Gerekli öznitelik:</span><span class="sxs-lookup"><span data-stu-id="a6293-272">Required attribute:</span></span><br /><br /> <span data-ttu-id="a6293-273">**Sağlayıcı** -hello EventSource olay hello sınıfı adı.</span><span class="sxs-lookup"><span data-stu-id="a6293-273">**provider** - hello class name of hello EventSource event.</span></span><br /><br /> <span data-ttu-id="a6293-274">İsteğe bağlı öznitelikleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="a6293-274">Optional attributes are:</span></span><br /><br /> <span data-ttu-id="a6293-275">- **scheduledTransferLogLevelFilter** -hello minimum önem düzeyi tootransfer tooyour depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="a6293-275">- **scheduledTransferLogLevelFilter** - hello minimum severity level tootransfer tooyour storage account.</span></span><br /><br /> <span data-ttu-id="a6293-276">- **scheduledTransferPeriod** -toohello minute en yakın yuvarlanan zamanlanmış aktarımları toostorage hello aralığıdır.</span><span class="sxs-lookup"><span data-stu-id="a6293-276">- **scheduledTransferPeriod** - hello interval between scheduled transfers toostorage rounded up toohello nearest minute.</span></span> <span data-ttu-id="a6293-277">Merhaba değeri bir [XML "Süre veri türü."](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="a6293-277">hello value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  
|<span data-ttu-id="a6293-278">**EtwManifestProviderConfiguration**</span><span class="sxs-lookup"><span data-stu-id="a6293-278">**EtwManifestProviderConfiguration**</span></span>|<span data-ttu-id="a6293-279">Gerekli öznitelik:</span><span class="sxs-lookup"><span data-stu-id="a6293-279">Required attribute:</span></span><br /><br /> <span data-ttu-id="a6293-280">**Sağlayıcı** -hello Olay sağlayıcısı GUİD'si hello</span><span class="sxs-lookup"><span data-stu-id="a6293-280">**provider** - hello GUID of hello event provider</span></span><br /><br /> <span data-ttu-id="a6293-281">İsteğe bağlı öznitelikleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="a6293-281">Optional attributes are:</span></span><br /><br /> <span data-ttu-id="a6293-282">- **scheduledTransferLogLevelFilter** -hello minimum önem düzeyi tootransfer tooyour depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="a6293-282">- **scheduledTransferLogLevelFilter** - hello minimum severity level tootransfer tooyour storage account.</span></span><br /><br /> <span data-ttu-id="a6293-283">- **scheduledTransferPeriod** -toohello minute en yakın yuvarlanan zamanlanmış aktarımları toostorage hello aralığıdır.</span><span class="sxs-lookup"><span data-stu-id="a6293-283">- **scheduledTransferPeriod** - hello interval between scheduled transfers toostorage rounded up toohello nearest minute.</span></span> <span data-ttu-id="a6293-284">Merhaba değeri bir [XML "Süre veri türü."](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="a6293-284">hello value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  



## <a name="etweventsourceproviderconfiguration-element"></a><span data-ttu-id="a6293-285">EtwEventSourceProviderConfiguration öğesi</span><span class="sxs-lookup"><span data-stu-id="a6293-285">EtwEventSourceProviderConfiguration Element</span></span>  
 <span data-ttu-id="a6293-286">*Ağaç: Kök - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders - EtwEventSourceProviderConfiguration*</span><span class="sxs-lookup"><span data-stu-id="a6293-286">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders- EtwEventSourceProviderConfiguration*</span></span>

 <span data-ttu-id="a6293-287">Koleksiyon üretilen olayların yapılandırır [EventSource sınıfı](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="a6293-287">Configures collection of events generated from [EventSource Class](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span></span>  

|<span data-ttu-id="a6293-288">Alt öğeler</span><span class="sxs-lookup"><span data-stu-id="a6293-288">Child Elements</span></span>|<span data-ttu-id="a6293-289">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a6293-289">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="a6293-290">**DefaultEvents**</span><span class="sxs-lookup"><span data-stu-id="a6293-290">**DefaultEvents**</span></span>|<span data-ttu-id="a6293-291">İsteğe bağlı öznitelik:</span><span class="sxs-lookup"><span data-stu-id="a6293-291">Optional attribute:</span></span><br/><br/> <span data-ttu-id="a6293-292">**eventDestination** - hello hello tablo toostore hello olayları adı</span><span class="sxs-lookup"><span data-stu-id="a6293-292">**eventDestination** - hello name of hello table toostore hello events in</span></span>|  
|<span data-ttu-id="a6293-293">**Olay**</span><span class="sxs-lookup"><span data-stu-id="a6293-293">**Event**</span></span>|<span data-ttu-id="a6293-294">Gerekli öznitelik:</span><span class="sxs-lookup"><span data-stu-id="a6293-294">Required attribute:</span></span><br /><br /> <span data-ttu-id="a6293-295">**Kimliği** -hello olay hello kimliği.</span><span class="sxs-lookup"><span data-stu-id="a6293-295">**id** - hello id of hello event.</span></span><br /><br /> <span data-ttu-id="a6293-296">İsteğe bağlı öznitelik:</span><span class="sxs-lookup"><span data-stu-id="a6293-296">Optional attribute:</span></span><br /><br /> <span data-ttu-id="a6293-297">**eventDestination** - hello hello tablo toostore hello olayları adı</span><span class="sxs-lookup"><span data-stu-id="a6293-297">**eventDestination** - hello name of hello table toostore hello events in</span></span>|  



## <a name="etwmanifestproviderconfiguration-element"></a><span data-ttu-id="a6293-298">EtwManifestProviderConfiguration öğesi</span><span class="sxs-lookup"><span data-stu-id="a6293-298">EtwManifestProviderConfiguration Element</span></span>  
 <span data-ttu-id="a6293-299">*Ağaç: Kök - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders - EtwManifestProviderConfiguration*</span><span class="sxs-lookup"><span data-stu-id="a6293-299">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders - EtwManifestProviderConfiguration*</span></span>

|<span data-ttu-id="a6293-300">Alt öğeler</span><span class="sxs-lookup"><span data-stu-id="a6293-300">Child Elements</span></span>|<span data-ttu-id="a6293-301">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a6293-301">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="a6293-302">**DefaultEvents**</span><span class="sxs-lookup"><span data-stu-id="a6293-302">**DefaultEvents**</span></span>|<span data-ttu-id="a6293-303">İsteğe bağlı öznitelik:</span><span class="sxs-lookup"><span data-stu-id="a6293-303">Optional attribute:</span></span><br /><br /> <span data-ttu-id="a6293-304">**eventDestination** - hello hello tablo toostore hello olayları adı</span><span class="sxs-lookup"><span data-stu-id="a6293-304">**eventDestination** - hello name of hello table toostore hello events in</span></span>|  
|<span data-ttu-id="a6293-305">**Olay**</span><span class="sxs-lookup"><span data-stu-id="a6293-305">**Event**</span></span>|<span data-ttu-id="a6293-306">Gerekli öznitelik:</span><span class="sxs-lookup"><span data-stu-id="a6293-306">Required attribute:</span></span><br /><br /> <span data-ttu-id="a6293-307">**Kimliği** -hello olay hello kimliği.</span><span class="sxs-lookup"><span data-stu-id="a6293-307">**id** - hello id of hello event.</span></span><br /><br /> <span data-ttu-id="a6293-308">İsteğe bağlı öznitelik:</span><span class="sxs-lookup"><span data-stu-id="a6293-308">Optional attribute:</span></span><br /><br /> <span data-ttu-id="a6293-309">**eventDestination** - hello hello tablo toostore hello olayları adı</span><span class="sxs-lookup"><span data-stu-id="a6293-309">**eventDestination** - hello name of hello table toostore hello events in</span></span>|  



## <a name="metrics-element"></a><span data-ttu-id="a6293-310">Ölçümleri öğesi</span><span class="sxs-lookup"><span data-stu-id="a6293-310">Metrics Element</span></span>  
 <span data-ttu-id="a6293-311">*Ağaç: Kök - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - ölçümleri*</span><span class="sxs-lookup"><span data-stu-id="a6293-311">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Metrics*</span></span>

 <span data-ttu-id="a6293-312">Toogenerate hızlı sorguları için en iyi hale getirilmiş bir performans sayacı tablo sağlar.</span><span class="sxs-lookup"><span data-stu-id="a6293-312">Enables you toogenerate a performance counter table that is optimized for fast queries.</span></span> <span data-ttu-id="a6293-313">Hello tanımlanan her performans sayacı **performans sayaçları** öğesi hello ölçümleri toplama toohello performans sayacı tablo tablosunda depolanır.</span><span class="sxs-lookup"><span data-stu-id="a6293-313">Each performance counter that is defined in hello **PerformanceCounters** element is stored in hello Metrics table in addition toohello Performance Counter table.</span></span>  

 <span data-ttu-id="a6293-314">Merhaba **ResourceId** özniteliği gereklidir.</span><span class="sxs-lookup"><span data-stu-id="a6293-314">hello **resourceId** attribute is required.</span></span>  <span data-ttu-id="a6293-315">Sanal makine için Azure tanılama dağıtıyorsanız hello Hello kaynak kimliği.</span><span class="sxs-lookup"><span data-stu-id="a6293-315">hello resource ID of hello Virtual Machine you are deploying Azure Diagnostics to.</span></span> <span data-ttu-id="a6293-316">Merhaba alma **ResourceId** hello gelen [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a6293-316">Get hello **resourceID** from hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="a6293-317">Seçin **Gözat** -> **kaynak grupları** -> **< adı\>**.</span><span class="sxs-lookup"><span data-stu-id="a6293-317">Select **Browse** -> **Resource Groups** -> **<Name\>**.</span></span> <span data-ttu-id="a6293-318">Merhaba tıklatın **özellikleri** döşeme ve hello hello değerini kopyalayın **kimliği** alan.</span><span class="sxs-lookup"><span data-stu-id="a6293-318">Click hello **Properties** tile and copy hello value from hello **ID** field.</span></span>  

|<span data-ttu-id="a6293-319">Alt öğeler</span><span class="sxs-lookup"><span data-stu-id="a6293-319">Child Elements</span></span>|<span data-ttu-id="a6293-320">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a6293-320">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="a6293-321">**MetricAggregation**</span><span class="sxs-lookup"><span data-stu-id="a6293-321">**MetricAggregation**</span></span>|<span data-ttu-id="a6293-322">Gerekli öznitelik:</span><span class="sxs-lookup"><span data-stu-id="a6293-322">Required attribute:</span></span><br /><br /> <span data-ttu-id="a6293-323">**scheduledTransferPeriod** -toohello minute en yakın yuvarlanan zamanlanmış aktarımları toostorage hello aralığıdır.</span><span class="sxs-lookup"><span data-stu-id="a6293-323">**scheduledTransferPeriod** - hello interval between scheduled transfers toostorage rounded up toohello nearest minute.</span></span> <span data-ttu-id="a6293-324">Merhaba değeri bir [XML "Süre veri türü."](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="a6293-324">hello value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  



## <a name="performancecounters-element"></a><span data-ttu-id="a6293-325">PerformanceCounters öğesi</span><span class="sxs-lookup"><span data-stu-id="a6293-325">PerformanceCounters Element</span></span>  
 <span data-ttu-id="a6293-326">*Ağaç: Kök - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - performans sayaçları*</span><span class="sxs-lookup"><span data-stu-id="a6293-326">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - PerformanceCounters*</span></span>

 <span data-ttu-id="a6293-327">Performans sayaçları Hello koleksiyonunu sağlar.</span><span class="sxs-lookup"><span data-stu-id="a6293-327">Enables hello collection of performance counters.</span></span>  

 <span data-ttu-id="a6293-328">İsteğe bağlı öznitelik:</span><span class="sxs-lookup"><span data-stu-id="a6293-328">Optional attribute:</span></span>  

 <span data-ttu-id="a6293-329">İsteğe bağlı **scheduledTransferPeriod** özniteliği.</span><span class="sxs-lookup"><span data-stu-id="a6293-329">Optional **scheduledTransferPeriod** attribute.</span></span> <span data-ttu-id="a6293-330">Daha önce açıklama konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="a6293-330">See explanation earlier.</span></span>

|<span data-ttu-id="a6293-331">Alt öğe</span><span class="sxs-lookup"><span data-stu-id="a6293-331">Child Element</span></span>|<span data-ttu-id="a6293-332">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a6293-332">Description</span></span>|  
|-------------------|-----------------|  
|<span data-ttu-id="a6293-333">**PerformanceCounterConfiguration**</span><span class="sxs-lookup"><span data-stu-id="a6293-333">**PerformanceCounterConfiguration**</span></span>|<span data-ttu-id="a6293-334">Aşağıdaki öznitelikler hello gereklidir:</span><span class="sxs-lookup"><span data-stu-id="a6293-334">hello following attributes are required:</span></span><br /><br /> <span data-ttu-id="a6293-335">- **counterSpecifier** - hello hello performans sayacının adı.</span><span class="sxs-lookup"><span data-stu-id="a6293-335">- **counterSpecifier** - hello name of hello performance counter.</span></span> <span data-ttu-id="a6293-336">Örneğin, `\Processor(_Total)\% Processor Time`.</span><span class="sxs-lookup"><span data-stu-id="a6293-336">For example, `\Processor(_Total)\% Processor Time`.</span></span> <span data-ttu-id="a6293-337">tooget hello komutunu çalıştırın, ana bilgisayarda listesini performans sayaçları `typeperf`.</span><span class="sxs-lookup"><span data-stu-id="a6293-337">tooget a list of performance counters on your host, run hello command `typeperf`.</span></span><br /><br /> <span data-ttu-id="a6293-338">- **sampleRate** -ne sıklıkta hello sayaç örneklenen.</span><span class="sxs-lookup"><span data-stu-id="a6293-338">- **sampleRate** - How often hello counter should be sampled.</span></span><br /><br /> <span data-ttu-id="a6293-339">İsteğe bağlı öznitelik:</span><span class="sxs-lookup"><span data-stu-id="a6293-339">Optional attribute:</span></span><br /><br /> <span data-ttu-id="a6293-340">**Birim** -hello ölçü hello sayacı.</span><span class="sxs-lookup"><span data-stu-id="a6293-340">**unit** - hello unit of measure of hello counter.</span></span>|  




## <a name="windowseventlog-element"></a><span data-ttu-id="a6293-341">WindowsEventLog öğesi</span><span class="sxs-lookup"><span data-stu-id="a6293-341">WindowsEventLog Element</span></span>
 <span data-ttu-id="a6293-342">*Ağaç: Kök - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - WindowsEventLog*</span><span class="sxs-lookup"><span data-stu-id="a6293-342">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - WindowsEventLog*</span></span>
 
 <span data-ttu-id="a6293-343">Merhaba koleksiyonu, Windows olay günlüklerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="a6293-343">Enables hello collection of Windows Event Logs.</span></span>  

 <span data-ttu-id="a6293-344">İsteğe bağlı **scheduledTransferPeriod** özniteliği.</span><span class="sxs-lookup"><span data-stu-id="a6293-344">Optional **scheduledTransferPeriod** attribute.</span></span> <span data-ttu-id="a6293-345">Daha önce açıklama konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="a6293-345">See explanation  earlier.</span></span>  

|<span data-ttu-id="a6293-346">Alt öğe</span><span class="sxs-lookup"><span data-stu-id="a6293-346">Child Element</span></span>|<span data-ttu-id="a6293-347">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a6293-347">Description</span></span>|  
|-------------------|-----------------|  
|<span data-ttu-id="a6293-348">**Veri kaynağı**</span><span class="sxs-lookup"><span data-stu-id="a6293-348">**DataSource**</span></span>|<span data-ttu-id="a6293-349">Merhaba Windows olay günlüklerini toocollect.</span><span class="sxs-lookup"><span data-stu-id="a6293-349">hello Windows Event logs toocollect.</span></span> <span data-ttu-id="a6293-350">Gerekli öznitelik:</span><span class="sxs-lookup"><span data-stu-id="a6293-350">Required attribute:</span></span><br /><br /> <span data-ttu-id="a6293-351">**ad** -hello windows olayları toobe açıklayan hello XPath sorgusu toplanır.</span><span class="sxs-lookup"><span data-stu-id="a6293-351">**name** - hello XPath query describing hello windows events toobe collected.</span></span> <span data-ttu-id="a6293-352">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="a6293-352">For example:</span></span><br /><br /> `Application!*[System[(Level <=3)]], System!*[System[(Level <=3)]], System!*[System[Provider[@Name='Microsoft Antimalware']]], Security!*[System[(Level <= 3)]`<br /><br /> <span data-ttu-id="a6293-353">tüm olayları toocollect belirtin "*"</span><span class="sxs-lookup"><span data-stu-id="a6293-353">toocollect all events, specify "*"</span></span>|  




## <a name="logs-element"></a><span data-ttu-id="a6293-354">Günlükleri öğesi</span><span class="sxs-lookup"><span data-stu-id="a6293-354">Logs Element</span></span>  
 <span data-ttu-id="a6293-355">*Ağaç: Kök - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - günlükleri*</span><span class="sxs-lookup"><span data-stu-id="a6293-355">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Logs*</span></span>

 <span data-ttu-id="a6293-356">Sürüm 1.0 ve 1.1 sunar.</span><span class="sxs-lookup"><span data-stu-id="a6293-356">Present in version 1.0 and 1.1.</span></span> <span data-ttu-id="a6293-357">1.2 ile eksik.</span><span class="sxs-lookup"><span data-stu-id="a6293-357">Missing in 1.2.</span></span> <span data-ttu-id="a6293-358">1.3 geri eklendi.</span><span class="sxs-lookup"><span data-stu-id="a6293-358">Added back in 1.3.</span></span>  

 <span data-ttu-id="a6293-359">Temel Azure günlükleri Hello arabellek yapılandırmasını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="a6293-359">Defines hello buffer configuration for basic Azure logs.</span></span>  

|<span data-ttu-id="a6293-360">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="a6293-360">Attribute</span></span>|<span data-ttu-id="a6293-361">Tür</span><span class="sxs-lookup"><span data-stu-id="a6293-361">Type</span></span>|<span data-ttu-id="a6293-362">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a6293-362">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="a6293-363">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="a6293-363">**bufferQuotaInMB**</span></span>|<span data-ttu-id="a6293-364">**unsignedInt**</span><span class="sxs-lookup"><span data-stu-id="a6293-364">**unsignedInt**</span></span>|<span data-ttu-id="a6293-365">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="a6293-365">Optional.</span></span> <span data-ttu-id="a6293-366">Merhaba en belirtilen hello için kullanılabilir olan dosya sistemi depolama miktarını belirtir veri.</span><span class="sxs-lookup"><span data-stu-id="a6293-366">Specifies hello maximum amount of file system storage that is available for hello specified data.</span></span><br /><br /> <span data-ttu-id="a6293-367">Merhaba varsayılan 0'dır.</span><span class="sxs-lookup"><span data-stu-id="a6293-367">hello default is 0.</span></span>|  
|<span data-ttu-id="a6293-368">**scheduledTransferLogLevelFilterr**</span><span class="sxs-lookup"><span data-stu-id="a6293-368">**scheduledTransferLogLevelFilterr**</span></span>|<span data-ttu-id="a6293-369">**dize**</span><span class="sxs-lookup"><span data-stu-id="a6293-369">**string**</span></span>|<span data-ttu-id="a6293-370">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="a6293-370">Optional.</span></span> <span data-ttu-id="a6293-371">Aktarılır günlük girişlerini Hello en düşük önem derecesini belirtir.</span><span class="sxs-lookup"><span data-stu-id="a6293-371">Specifies hello minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="a6293-372">Merhaba varsayılan değer **tanımlanmamış**, tüm günlükleri aktarır.</span><span class="sxs-lookup"><span data-stu-id="a6293-372">hello default value is **Undefined**, which transfers all logs.</span></span> <span data-ttu-id="a6293-373">Diğer olası değerler (tooleast bilgilerin çoğu sırasına göre) **ayrıntılı**, **bilgi**, **uyarı**, **hata**ve **Kritik**.</span><span class="sxs-lookup"><span data-stu-id="a6293-373">Other possible values (in order of most tooleast information) are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="a6293-374">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="a6293-374">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="a6293-375">**süre**</span><span class="sxs-lookup"><span data-stu-id="a6293-375">**duration**</span></span>|<span data-ttu-id="a6293-376">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="a6293-376">Optional.</span></span> <span data-ttu-id="a6293-377">Zamanlanmış toohello minute en yakın yukarı yuvarlanmasını veri aktarımını Hello aralığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="a6293-377">Specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span><br /><br /> <span data-ttu-id="a6293-378">Merhaba, PT0S varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="a6293-378">hello default is PT0S.</span></span>|  
|<span data-ttu-id="a6293-379">**İç havuzlar** 1.5 inç eklendi</span><span class="sxs-lookup"><span data-stu-id="a6293-379">**sinks** Added in 1.5</span></span>|<span data-ttu-id="a6293-380">**dize**</span><span class="sxs-lookup"><span data-stu-id="a6293-380">**string**</span></span>|<span data-ttu-id="a6293-381">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="a6293-381">Optional.</span></span> <span data-ttu-id="a6293-382">Noktaları tooa havuz konumu tooalso tanılama verisi gönderin.</span><span class="sxs-lookup"><span data-stu-id="a6293-382">Points tooa sink location tooalso send diagnostic data.</span></span> <span data-ttu-id="a6293-383">Örneğin, Application Insights.</span><span class="sxs-lookup"><span data-stu-id="a6293-383">For example, Application Insights.</span></span>|  

## <a name="dockersources"></a><span data-ttu-id="a6293-384">DockerSources</span><span class="sxs-lookup"><span data-stu-id="a6293-384">DockerSources</span></span>
 <span data-ttu-id="a6293-385">*Ağaç: Kök - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - DockerSources*</span><span class="sxs-lookup"><span data-stu-id="a6293-385">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - DockerSources*</span></span>

 <span data-ttu-id="a6293-386">İçinde 1.9 eklendi.</span><span class="sxs-lookup"><span data-stu-id="a6293-386">Added in 1.9.</span></span>

|<span data-ttu-id="a6293-387">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="a6293-387">Element Name</span></span>|<span data-ttu-id="a6293-388">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a6293-388">Description</span></span>|  
|------------------|-----------------|  
|<span data-ttu-id="a6293-389">**İstatistikleri**</span><span class="sxs-lookup"><span data-stu-id="a6293-389">**Stats**</span></span>|<span data-ttu-id="a6293-390">Docker kapsayıcıları toocollect istatistikleri Hello sistem bildirir</span><span class="sxs-lookup"><span data-stu-id="a6293-390">Tells hello system toocollect stats for Docker containers</span></span>|  

## <a name="sinksconfig-element"></a><span data-ttu-id="a6293-391">SinksConfig öğesi</span><span class="sxs-lookup"><span data-stu-id="a6293-391">SinksConfig Element</span></span>  
 <span data-ttu-id="a6293-392">*Ağaç: Kök - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig*</span><span class="sxs-lookup"><span data-stu-id="a6293-392">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig*</span></span>

 <span data-ttu-id="a6293-393">Konumları toosend tanılama veri tooand hello yapılandırması konumların ile ilişkili bir listesi.</span><span class="sxs-lookup"><span data-stu-id="a6293-393">A list of locations toosend diagnostics data tooand hello configuration associated with those locations.</span></span>  

|<span data-ttu-id="a6293-394">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="a6293-394">Element Name</span></span>|<span data-ttu-id="a6293-395">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a6293-395">Description</span></span>|  
|------------------|-----------------|  
|<span data-ttu-id="a6293-396">**Havuz**</span><span class="sxs-lookup"><span data-stu-id="a6293-396">**Sink**</span></span>|<span data-ttu-id="a6293-397">Açıklama, bu sayfada başka bir yerde bakın.</span><span class="sxs-lookup"><span data-stu-id="a6293-397">See description elsewhere on this page.</span></span>|  

## <a name="sink-element"></a><span data-ttu-id="a6293-398">Öğe havuzu</span><span class="sxs-lookup"><span data-stu-id="a6293-398">Sink Element</span></span>
 <span data-ttu-id="a6293-399">*Ağaç: Kök - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - havuz*</span><span class="sxs-lookup"><span data-stu-id="a6293-399">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink*</span></span>

 <span data-ttu-id="a6293-400">Sürüm 1.5 eklendi.</span><span class="sxs-lookup"><span data-stu-id="a6293-400">Added in version 1.5.</span></span>  

 <span data-ttu-id="a6293-401">Konumları toosend Tanılama verileri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="a6293-401">Defines locations toosend diagnostic data to.</span></span> <span data-ttu-id="a6293-402">Örneğin, Application Insights hizmeti hello.</span><span class="sxs-lookup"><span data-stu-id="a6293-402">For example, hello Application Insights service.</span></span>  

|<span data-ttu-id="a6293-403">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="a6293-403">Attribute</span></span>|<span data-ttu-id="a6293-404">Tür</span><span class="sxs-lookup"><span data-stu-id="a6293-404">Type</span></span>|<span data-ttu-id="a6293-405">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a6293-405">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="a6293-406">**adı**</span><span class="sxs-lookup"><span data-stu-id="a6293-406">**name**</span></span>|<span data-ttu-id="a6293-407">Dize</span><span class="sxs-lookup"><span data-stu-id="a6293-407">string</span></span>|<span data-ttu-id="a6293-408">Bir dize tanımlayıcı hello sinkname.</span><span class="sxs-lookup"><span data-stu-id="a6293-408">A string identifying hello sinkname.</span></span>|  

|<span data-ttu-id="a6293-409">Öğesi</span><span class="sxs-lookup"><span data-stu-id="a6293-409">Element</span></span>|<span data-ttu-id="a6293-410">Tür</span><span class="sxs-lookup"><span data-stu-id="a6293-410">Type</span></span>|<span data-ttu-id="a6293-411">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a6293-411">Description</span></span>|  
|-------------|----------|-----------------|  
|<span data-ttu-id="a6293-412">**Application Insights**</span><span class="sxs-lookup"><span data-stu-id="a6293-412">**Application Insights**</span></span>|<span data-ttu-id="a6293-413">Dize</span><span class="sxs-lookup"><span data-stu-id="a6293-413">string</span></span>|<span data-ttu-id="a6293-414">Yalnızca veri tooApplication Öngörüler gönderirken kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a6293-414">Used only when sending data tooApplication Insights.</span></span> <span data-ttu-id="a6293-415">Merhaba erişiminiz etkin bir Application Insights hesabı için izleme anahtarını içerir.</span><span class="sxs-lookup"><span data-stu-id="a6293-415">Contain hello Instrumentation Key for an active Application Insights account that you have access to.</span></span>|  
|<span data-ttu-id="a6293-416">**Kanalları**</span><span class="sxs-lookup"><span data-stu-id="a6293-416">**Channels**</span></span>|<span data-ttu-id="a6293-417">Dize</span><span class="sxs-lookup"><span data-stu-id="a6293-417">string</span></span>|<span data-ttu-id="a6293-418">Her ek, akış filtrelemesi için bir tane</span><span class="sxs-lookup"><span data-stu-id="a6293-418">One for each additional filtering that stream that you</span></span>|  

## <a name="channels-element"></a><span data-ttu-id="a6293-419">Kanallar öğesi</span><span class="sxs-lookup"><span data-stu-id="a6293-419">Channels Element</span></span>  
 <span data-ttu-id="a6293-420">*Ağaç: Kök - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - havuz - kanalları*</span><span class="sxs-lookup"><span data-stu-id="a6293-420">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels*</span></span>

 <span data-ttu-id="a6293-421">Sürüm 1.5 eklendi.</span><span class="sxs-lookup"><span data-stu-id="a6293-421">Added in version 1.5.</span></span>  

 <span data-ttu-id="a6293-422">Bir havuz geçirme günlük veri akışları için filtreleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="a6293-422">Defines filters for streams of log data passing through a sink.</span></span>  

|<span data-ttu-id="a6293-423">Öğesi</span><span class="sxs-lookup"><span data-stu-id="a6293-423">Element</span></span>|<span data-ttu-id="a6293-424">Tür</span><span class="sxs-lookup"><span data-stu-id="a6293-424">Type</span></span>|<span data-ttu-id="a6293-425">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a6293-425">Description</span></span>|  
|-------------|----------|-----------------|  
|<span data-ttu-id="a6293-426">**Kanal**</span><span class="sxs-lookup"><span data-stu-id="a6293-426">**Channel**</span></span>|<span data-ttu-id="a6293-427">Dize</span><span class="sxs-lookup"><span data-stu-id="a6293-427">string</span></span>|<span data-ttu-id="a6293-428">Açıklama, bu sayfada başka bir yerde bakın.</span><span class="sxs-lookup"><span data-stu-id="a6293-428">See description elsewhere on this page.</span></span>|  

## <a name="channel-element"></a><span data-ttu-id="a6293-429">Kanal öğesi</span><span class="sxs-lookup"><span data-stu-id="a6293-429">Channel Element</span></span>
 <span data-ttu-id="a6293-430">*Ağaç: Kök - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - havuz - kanalları - kanal*</span><span class="sxs-lookup"><span data-stu-id="a6293-430">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels - Channel*</span></span>

 <span data-ttu-id="a6293-431">Sürüm 1.5 eklendi.</span><span class="sxs-lookup"><span data-stu-id="a6293-431">Added in version 1.5.</span></span>  

 <span data-ttu-id="a6293-432">Konumları toosend Tanılama verileri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="a6293-432">Defines locations toosend diagnostic data to.</span></span> <span data-ttu-id="a6293-433">Örneğin, Application Insights hizmeti hello.</span><span class="sxs-lookup"><span data-stu-id="a6293-433">For example, hello Application Insights service.</span></span>  

|<span data-ttu-id="a6293-434">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="a6293-434">Attributes</span></span>|<span data-ttu-id="a6293-435">Tür</span><span class="sxs-lookup"><span data-stu-id="a6293-435">Type</span></span>|<span data-ttu-id="a6293-436">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a6293-436">Description</span></span>|  
|----------------|----------|-----------------|  
|<span data-ttu-id="a6293-437">**logLevel**</span><span class="sxs-lookup"><span data-stu-id="a6293-437">**logLevel**</span></span>|<span data-ttu-id="a6293-438">**dize**</span><span class="sxs-lookup"><span data-stu-id="a6293-438">**string**</span></span>|<span data-ttu-id="a6293-439">Aktarılır günlük girişlerini Hello en düşük önem derecesini belirtir.</span><span class="sxs-lookup"><span data-stu-id="a6293-439">Specifies hello minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="a6293-440">Merhaba varsayılan değer **tanımlanmamış**, tüm günlükleri aktarır.</span><span class="sxs-lookup"><span data-stu-id="a6293-440">hello default value is **Undefined**, which transfers all logs.</span></span> <span data-ttu-id="a6293-441">Diğer olası değerler (tooleast bilgilerin çoğu sırasına göre) **ayrıntılı**, **bilgi**, **uyarı**, **hata**ve **Kritik**.</span><span class="sxs-lookup"><span data-stu-id="a6293-441">Other possible values (in order of most tooleast information) are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="a6293-442">**adı**</span><span class="sxs-lookup"><span data-stu-id="a6293-442">**name**</span></span>|<span data-ttu-id="a6293-443">**dize**</span><span class="sxs-lookup"><span data-stu-id="a6293-443">**string**</span></span>|<span data-ttu-id="a6293-444">Merhaba kanal toorefer için benzersiz bir ad</span><span class="sxs-lookup"><span data-stu-id="a6293-444">A unique name of hello channel toorefer to</span></span>|  


## <a name="privateconfig-element"></a><span data-ttu-id="a6293-445">PrivateConfig öğesi</span><span class="sxs-lookup"><span data-stu-id="a6293-445">PrivateConfig Element</span></span> 
 <span data-ttu-id="a6293-446">*Ağaç: Kök - DiagnosticsConfiguration - PrivateConfig*</span><span class="sxs-lookup"><span data-stu-id="a6293-446">*Tree: Root - DiagnosticsConfiguration - PrivateConfig*</span></span>

 <span data-ttu-id="a6293-447">Sürüm 1.3 eklendi.</span><span class="sxs-lookup"><span data-stu-id="a6293-447">Added in version 1.3.</span></span>  

 <span data-ttu-id="a6293-448">İsteğe bağlı</span><span class="sxs-lookup"><span data-stu-id="a6293-448">Optional</span></span>  

 <span data-ttu-id="a6293-449">Merhaba özel ayrıntıları hello depolama hesabının (adı, anahtar ve uç nokta) depolar.</span><span class="sxs-lookup"><span data-stu-id="a6293-449">Stores hello private details of hello storage account (name, key, and endpoint).</span></span> <span data-ttu-id="a6293-450">Bu bilgiler toohello sanal makine gönderilir, ancak ondan alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="a6293-450">This information is sent toohello virtual machine, but cannot be retrieved from it.</span></span>  

|<span data-ttu-id="a6293-451">Alt öğeler</span><span class="sxs-lookup"><span data-stu-id="a6293-451">Child Elements</span></span>|<span data-ttu-id="a6293-452">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a6293-452">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="a6293-453">**StorageAccount**</span><span class="sxs-lookup"><span data-stu-id="a6293-453">**StorageAccount**</span></span>|<span data-ttu-id="a6293-454">Merhaba depolama hesabı toouse.</span><span class="sxs-lookup"><span data-stu-id="a6293-454">hello storage account toouse.</span></span> <span data-ttu-id="a6293-455">Aşağıdaki öznitelikler hello gereklidir</span><span class="sxs-lookup"><span data-stu-id="a6293-455">hello following attributes are required</span></span><br /><br /> <span data-ttu-id="a6293-456">- **ad** - hello hello depolama hesabı adı.</span><span class="sxs-lookup"><span data-stu-id="a6293-456">- **name** - hello name of hello storage account.</span></span><br /><br /> <span data-ttu-id="a6293-457">- **anahtar** - hello anahtar toohello depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="a6293-457">- **key** - hello key toohello storage account.</span></span><br /><br /> <span data-ttu-id="a6293-458">- **uç nokta** -hello uç nokta tooaccess hello depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="a6293-458">- **endpoint** - hello endpoint tooaccess hello storage account.</span></span> <br /><br /> <span data-ttu-id="a6293-459">-**sasToken** (Merhaba özel yapılandırma dosyasında bir SAS belirteci bir depolama hesabı anahtarı yerine belirtebilirsiniz 1.8.1)-eklenir. Merhaba depolama hesabı anahtarı sağladıysanız, göz ardı edilir.</span><span class="sxs-lookup"><span data-stu-id="a6293-459">-**sasToken** (added 1.8.1)- You can specify an SAS token instead of a storage account key in hello private config. If provided, hello storage account key is ignored.</span></span> <br /><span data-ttu-id="a6293-460">SAS belirteci hello gereksinimleri:</span><span class="sxs-lookup"><span data-stu-id="a6293-460">Requirements for hello SAS Token:</span></span> <br /><span data-ttu-id="a6293-461">-Hesap SAS belirteci yalnızca destekler</span><span class="sxs-lookup"><span data-stu-id="a6293-461">- Supports account SAS token only</span></span> <br /><span data-ttu-id="a6293-462">- *b*, *t* hizmet türleri gereklidir.</span><span class="sxs-lookup"><span data-stu-id="a6293-462">- *b*, *t* service types are required.</span></span> <br /> <span data-ttu-id="a6293-463">- *bir*, *c*, *u*, *w* izinleri gereklidir.</span><span class="sxs-lookup"><span data-stu-id="a6293-463">- *a*, *c*, *u*, *w* permissions are required.</span></span> <br /> <span data-ttu-id="a6293-464">- *c*, *o* kaynak türleri gereklidir.</span><span class="sxs-lookup"><span data-stu-id="a6293-464">- *c*, *o* resource types are required.</span></span> <br /> <span data-ttu-id="a6293-465">-Yalnızca hello HTTPS protokolünü destekler</span><span class="sxs-lookup"><span data-stu-id="a6293-465">- Supports hello HTTPS protocol only</span></span> <br /> <span data-ttu-id="a6293-466">-Başlangıç ve sona erme saati geçerli olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a6293-466">- Start and expiry time must be valid.</span></span>|  


## <a name="isenabled-element"></a><span data-ttu-id="a6293-467">IsEnabled öğesi</span><span class="sxs-lookup"><span data-stu-id="a6293-467">IsEnabled Element</span></span>  
 <span data-ttu-id="a6293-468">*Ağaç: Kök - DiagnosticsConfiguration - IsEnabled*</span><span class="sxs-lookup"><span data-stu-id="a6293-468">*Tree: Root - DiagnosticsConfiguration - IsEnabled*</span></span>

 <span data-ttu-id="a6293-469">Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="a6293-469">Boolean.</span></span> <span data-ttu-id="a6293-470">Kullanım `true` tooenable hello Tanılama veya `false` toodisable hello tanılama.</span><span class="sxs-lookup"><span data-stu-id="a6293-470">Use `true` tooenable hello diagnostics or `false` toodisable hello diagnostics.</span></span>
