---
title: "aaaCloud Hizmetleri rolünü config XPath kopya sayfası | Microsoft Docs"
description: "Merhaba bulut hizmeti rolünü yapılandırma tooexpose ayarlarında bir ortam değişkeni kullanabileceğiniz çeşitli XPath ayarları hello."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: c51e4493-0643-4d05-bc44-06c76bcbf7d1
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: 27f98f956a1c790c9bb30f9fefe1ab1736b2b150
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="expose-role-configuration-settings-as-an-environment-variable-with-xpath"></a>Rol yapılandırma ayarlarını XPath olan bir ortam değişkeni olarak kullanıma sunma
Merhaba bulut hizmeti çalışan veya web rolü Hizmet tanım dosyası, ortam değişkenleri olarak çalışma zamanı yapılandırma değerlerini getirebilir. XPath değerleri aşağıdaki hello (hangi tooAPI değerler karşılık gelir) desteklenir.

Bu XPath değerleri de hello kullanılabilir [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) kitaplığı. 

## <a name="app-running-in-emulator"></a>Öykünücüde çalışan uygulama
Bu hello uygulama hello öykünücüsünde çalışmadığını gösterir.

| Tür | Örnek |
| --- | --- |
| XPath |XPath = "/RoleEnvironment/Deployment/@emulated" |
| Kod |var x RoleEnvironment.IsEmulated; = |

## <a name="deployment-id"></a>Dağıtım kimliği
Merhaba örneğinin Hello dağıtım kimliği alır.

| Tür | Örnek |
| --- | --- |
| XPath |XPath = "/RoleEnvironment/Deployment/@id" |
| Kod |var Deploymentıd = RoleEnvironment.DeploymentId; |

## <a name="role-id"></a>Rol Kimliği
Merhaba geçerli rol kimliği hello örneği alır.

| Tür | Örnek |
| --- | --- |
| XPath |XPath = "/RoleEnvironment/CurrentInstance/@id" |
| Kod |var kimliği = RoleEnvironment.CurrentRoleInstance.Id; |

## <a name="update-domain"></a>etki alanı güncelleştirme
Merhaba örneğinin Hello güncelleştirme etki alanı alır.

| Tür | Örnek |
| --- | --- |
| XPath |XPath = "/RoleEnvironment/CurrentInstance/@updateDomain" |
| Kod |var ud RoleEnvironment.CurrentRoleInstance.UpdateDomain; = |

## <a name="fault-domain"></a>hata etki alanı
Merhaba örneğinin Hello hata etki alanı alır.

| Tür | Örnek |
| --- | --- |
| XPath |XPath = "/RoleEnvironment/CurrentInstance/@faultDomain" |
| Kod |var fd RoleEnvironment.CurrentRoleInstance.FaultDomain; = |

## <a name="role-name"></a>Rol adı
Merhaba örneklerinin Hello rol adını alır.

| Tür | Örnek |
| --- | --- |
| XPath |XPath = "/RoleEnvironment/CurrentInstance/@roleName" |
| Kod |var rname = RoleEnvironment.CurrentRoleInstance.Role.Name; |

## <a name="config-setting"></a>Yapılandırma ayarı
Yapılandırma ayarı tanımlanmış hello hello değeri alır.

| Tür | Örnek |
| --- | --- |
| XPath |XPath = "/ RoleEnvironment/currentınstance değerinin/ConfigurationSettings/ConfigurationSetting [@name'Setting1' =]/@value" |
| Kod |değişken ayarı RoleEnvironment.GetConfigurationSettingValue("Setting1"); = |

## <a name="local-storage-path"></a>Yerel depolama alanı yolu
Merhaba örneğin Hello yerel depolama yolunu alır.

| Tür | Örnek |
| --- | --- |
| XPath |XPath = "/ RoleEnvironment/currentınstance değerinin/LocalResources/LocalResource [@name'LocalStore1' =]/@path" |
| Kod |var localResourcePath RoleEnvironment.GetLocalResource("LocalStore1") =. RootPath; |

## <a name="local-storage-size"></a>Yerel depolama boyutu
Merhaba hello hello örneği için yerel depolama alanının boyutunu alır.

| Tür | Örnek |
| --- | --- |
| XPath |XPath = "/ RoleEnvironment/currentınstance değerinin/LocalResources/LocalResource [@name'LocalStore1' =]/@sizeInMB" |
| Kod |var localResourceSizeInMB RoleEnvironment.GetLocalResource("LocalStore1") =. MaximumSizeInMegabytes; |

## <a name="endpoint-protocol"></a>Uç nokta Protokolü
Merhaba örneğe Hello uç nokta protokolünü alır.

| Tür | Örnek |
| --- | --- |
| XPath |XPath = "/ RoleEnvironment/currentınstance değerinin/uç noktalar/uç noktanın [@name'Bitiş noktası 1' =]/@protocol" |
| Kod |var KOR RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1 ="]. Protokol; |

## <a name="endpoint-ip"></a>Uç nokta IP
Alır hello uç noktanın IP adresi belirtildi.

| Tür | Örnek |
| --- | --- |
| XPath |XPath = "/ RoleEnvironment/currentınstance değerinin/uç noktalar/uç noktanın [@name'Bitiş noktası 1' =]/@address" |
| Kod |var adresi RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1 ="]. IPEndpoint.Address |

## <a name="endpoint-port"></a>uç nokta bağlantı noktası
Merhaba örneğinin Hello uç nokta bağlantı noktası alır.

| Tür | Örnek |
| --- | --- |
| XPath |XPath = "/ RoleEnvironment/currentınstance değerinin/uç noktalar/uç noktanın [@name'Bitiş noktası 1' =]/@port" |
| Kod |bağlantı noktası var RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1 ="]. IPEndpoint.Port; |

## <a name="example"></a>Örnek
Bir başlangıç görevi adında bir ortam değişkeni oluşturan çalışan rolü bir örneği burada verilmiştir `TestIsEmulated` ayarlamak toohello [ @emulated xpath değeri](#app-running-in-emulator). 

```xml
<WorkerRole name="Role1">
    <ConfigurationSettings>
      <Setting name="Setting1" />
    </ConfigurationSettings>
    <LocalResources>
      <LocalStorage name="LocalStore1" sizeInMB="1024"/>
    </LocalResources>
    <Endpoints>
      <InternalEndpoint name="Endpoint1" protocol="tcp" />
    </Endpoints>
    <Startup>
      <Task commandLine="example.cmd inputParm">
        <Environment>
          <Variable name="TestConstant" value="Constant"/>
          <Variable name="TestEmptyValue" value=""/>
          <Variable name="TestIsEmulated">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated"/>
          </Variable>
          ...
        </Environment>
      </Task>
    </Startup>
    <Runtime>
      <Environment>
        <Variable name="TestConstant" value="Constant"/>
        <Variable name="TestEmptyValue" value=""/>
        <Variable name="TestIsEmulated">
          <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated"/>
        </Variable>
        ...
      </Environment>
    </Runtime>
    ...
</WorkerRole>
```

## <a name="next-steps"></a>Sonraki adımlar
Merhaba hakkında daha fazla bilgi [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#serviceconfigurationcscfg) dosya.

Oluşturma bir [ServicePackage.cspkg](cloud-services-model-and-package.md#servicepackagecspkg) paket.

Etkinleştirme [Uzak Masaüstü](cloud-services-role-enable-remote-desktop.md) bir rol için.

