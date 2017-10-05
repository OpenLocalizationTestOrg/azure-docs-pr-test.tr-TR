---
title: "API bulma ve kod oluşturma için App Service API Apps meta verileri | Microsoft Docs"
description: "Swagger meta verileri Azure uygulama hizmetinde API uygulamaları API bulma ve kod oluşturma kolaylaştırmak için nasıl kullanacağınızı öğrenin."
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: c7f8e33a-61cc-486f-89df-4a97dc3c71d4
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/30/2016
ms.author: alkarche
ms.openlocfilehash: 800bb9df9b957bec2c80abb3edefbaf354b549ca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="app-service-api-apps-metadata-for-api-discovery-and-code-generation"></a>API bulma ve kod oluşturma için App Service API Apps meta verileri
Desteği [Swagger 2.0](http://swagger.io/) API meta verileri, App Service API Apps içinde oluşturulur. Swagger kullanmanız gerekmez, ancak onu kullanmıyorsa, bulma ve kullanımını kolaylaştırmak API Apps özelliklerinden yararlanabilir.   

## <a name="swagger-endpoint"></a>Swagger uç nokta
API uygulamasının bir özelliği bir API uygulamasına Swagger 2.0 JSON meta verileri sağlayan bir uç nokta belirtebilirsiniz. Uç nokta API uygulamasının temel URL'si veya mutlak bir URL göreli olabilir. Mutlak URL'ler dışında API uygulaması işaret edebilir. 

Birçok aşağı akış istemcileri (örneğin, Visual Studio kod oluşturma ve PowerApps "API Ekle" akışı), URL (kullanıcı veya hizmet kimlik doğrulaması tarafından korumalı olmayan) genel olarak erişilebilir olmalıdır. Bu uygulama hizmeti kimlik doğrulaması kullanıyorsanız ve API tanımı, uygulamanızın içinde kullanıma sunmak istiyorsanız, API'nizi ulaşmak anonim trafiğe izin veren kimlik doğrulaması seçeneği kullanmak gerektiği anlamına gelir. Daha fazla bilgi için bkz: [kimlik doğrulama ve yetkilendirme için App Service API Apps](app-service-api-authentication.md).

### <a name="portal-blade"></a>Portal dikey penceresi
İçinde [Azure portal](https://portal.azure.com/) URL görülen ve üzerinde değiştirilmiş uç nokta **API tanımı** dikey.

![](./media/app-service-api-metadata/apidefblade.png)

### <a name="azure-resource-manager-property"></a>Azure Resource Manager özelliği
Kullanarak bir API uygulaması için API tanımı URL'si yapılandırabilirsiniz [kaynak Gezgini](https://resources.azure.com/) veya [Azure Resource Manager şablonları](../azure-resource-manager/resource-group-authoring-templates.md) gibi komut satırı araçlarında [Azure PowerShell](/powershell/azureps-cmdlets-docs)ve [Azure CLI](../cli-install-nodejs.md). 

İçinde **kaynak Gezgini**gidin **abonelikleri > {aboneliğinizi} > resourceGroups > {kaynak grubunuz} > sağlayıcıları > Microsoft.Web > siteleri > {sitenizi} > config > web** , ve göreceğiniz `apiDefinition` özelliği:

        "apiDefinition": {
          "url": "https://contactslistapi.azurewebsites.net/swagger/docs/v1"
        }

Ayarlar bir Azure Resource Manager şablonu örneği için `apiDefinition` özelliği, açık [Yapılacaklar listesi örnek uygulamasının deposundaki azuredeploy.json dosyasını](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json). Yukarıda gösterilen JSON örnek gibi görünen şablon bölümünü bulun.

### <a name="default-value"></a>Varsayılan değer
Bir API uygulaması oluşturmak için Visual Studio kullandığınızda API tanımı uç artı API uygulaması temel URL'sini otomatik olarak ayarlanır `/swagger/docs/v1`. Bu varsayılan URL'dir, [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) Swagger meta verileri bir ASP.NET Web API projesi için dinamik olarak üretilen sunmak için NuGet paketi kullanır. 

## <a name="code-generation"></a>Kod oluşturma
Azure API uygulamaları Swagger tümleştirme avantajlarını otomatik kod oluşturma biridir. Oluşturulan istemci sınıfları API uygulamasını çağıran bir kod yazmayı kolaylaştırır.

Visual Studio'yu kullanarak veya komut satırından bir API uygulaması için istemci kodu oluşturabilir. İstemci sınıfları bir ASP.NET Web API projesi için Visual Studio'da oluşturma hakkında daha fazla bilgi için bkz: [API uygulamaları ve ASP.NET kullanmaya başlama](app-service-api-dotnet-get-started.md#codegen). Tüm desteklenen diller için komut satırından nasıl yapılacağı hakkında daha fazla bilgi için Benioku dosyasına bakın [Azure/autorest](https://github.com/azure/autorest) Github.com'u havuzda.

## <a name="next-steps"></a>Sonraki adımlar
Dağıtma ve bir API uygulaması kullanma oluşturma size rehberlik eder bir adım adım öğretici için bkz: [Azure uygulama hizmetinde API uygulamaları ile çalışmaya başlama](app-service-api-dotnet-get-started.md).

API Apps ile Azure API Management kullanıyorsanız, Swagger meta verileri API'nizi API yönetime içeri aktarmak için kullanabilirsiniz. Daha fazla bilgi için bkz: [Azure API Management işlemleri olan bir API tanımını içeri aktarmak nasıl](../api-management/api-management-howto-import-api.md). 

