---
title: "API bulma ve kod oluşturma için aaaApp hizmeti API uygulamaları meta verileri | Microsoft Docs"
description: "Azure uygulama hizmetinde API uygulamaları meta veri toofacilitate API bulma ve kod oluşturmanın nasıl kullandığı hakkında bilgi edinin."
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
ms.openlocfilehash: b27e70b7dd6bd97f5b0b490b496320befe7442c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-api-apps-metadata-for-api-discovery-and-code-generation"></a>API bulma ve kod oluşturma için App Service API Apps meta verileri
Desteği [Swagger 2.0](http://swagger.io/) API meta verileri, App Service API Apps içinde oluşturulur. Toouse Swagger yoktur, ancak onu kullanmıyorsa, bulma ve kullanımını kolaylaştırmak API Apps özelliklerinden yararlanabilir.   

## <a name="swagger-endpoint"></a>Swagger uç nokta
Merhaba API uygulamasının bir özelliği bir API uygulamasına Swagger 2.0 JSON meta verileri sağlayan bir uç nokta belirtebilirsiniz. Merhaba endpoint hello API uygulamasının temel URL göreli toohello veya mutlak bir URL olabilir. Mutlak URL'ler hello API uygulaması dışında işaret edebilir. 

Birçok aşağı akış istemcileri (örneğin, Visual Studio kod oluşturma ve PowerApps "API Ekle" akış için) hello URL (kullanıcı veya hizmet kimlik doğrulaması tarafından korumalı olmayan) genel olarak erişilebilir olmalıdır. Bu uygulama hizmeti kimlik doğrulaması kullanıyorsanız ve tooexpose hello API tanımı, uygulamanızın içinde istiyorsanız anonim trafiği tooreach API'nizi veren toouse kimlik doğrulaması seçeneği gerektiği anlamına gelir. Daha fazla bilgi için bkz: [kimlik doğrulama ve yetkilendirme için App Service API Apps](app-service-api-authentication.md).

### <a name="portal-blade"></a>Portal dikey penceresi
Merhaba, [Azure portal](https://portal.azure.com/) URL görülen ve hello üzerinde değiştirilmiş endpoint hello **API tanımı** dikey.

![](./media/app-service-api-metadata/apidefblade.png)

### <a name="azure-resource-manager-property"></a>Azure Resource Manager özelliği
Kullanarak bir API uygulaması için hello API tanımı URL'si yapılandırabilirsiniz [kaynak Gezgini](https://resources.azure.com/) veya [Azure Resource Manager şablonları](../azure-resource-manager/resource-group-authoring-templates.md) gibi komut satırı araçlarında [Azure PowerShell](/powershell/azureps-cmdlets-docs)ve hello [Azure CLI](../cli-install-nodejs.md). 

İçinde **kaynak Gezgini**, çok Git**abonelikleri > {aboneliğinizi} > resourceGroups > {kaynak grubunuz} > sağlayıcıları > Microsoft.Web > siteleri > {sitenizi} > config > web**, hello görürsünüz `apiDefinition` özelliği:

        "apiDefinition": {
          "url": "https://contactslistapi.azurewebsites.net/swagger/docs/v1"
        }

Merhaba ayarlar bir Azure Resource Manager şablonu örneği için `apiDefinition` özelliği, açık hello [hello Yapılacaklar listesi örnek uygulaması deposundaki azuredeploy.json dosyasını](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json). Yukarıda gösterilen hello JSON örnek benzer hello şablon Hello bölümünü bulun.

### <a name="default-value"></a>Varsayılan değer
Visual Studio toocreate bir API uygulaması kullandığınızda hello API tanımı endpoint toohello temel URL'si artı hello API uygulamasının otomatik olarak ayarlanır `/swagger/docs/v1`. Merhaba varsayılan URL bu hello budur [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) NuGet paketi için bir ASP.NET Web API projesi dinamik olarak üretilen tooserve Swagger meta verileri kullanır. 

## <a name="code-generation"></a>Kod oluşturma
Azure API uygulamaları Swagger tümleştirme hello avantajları otomatik kod oluşturma biridir. Oluşturulan istemci sınıfları API uygulamasını çağıran bir daha kolay toowrite kod kolaylaştırır.

Visual Studio'yu kullanarak veya hello komut satırından bir API uygulaması için istemci kodu oluşturabilir. Nasıl toogenerate istemci için bir ASP.NET Web API projesini Visual Studio'da sınıfları hakkında daha fazla bilgi için bkz: [API uygulamaları ve ASP.NET kullanmaya başlama](app-service-api-dotnet-get-started.md#codegen). Merhaba hello Benioku dosyası nasıl toodo hello komutu ondan satır için tüm desteklenen dilleri hakkında daha fazla bilgi için bkz [Azure/autorest](https://github.com/azure/autorest) Github.com'u havuzda.

## <a name="next-steps"></a>Sonraki adımlar
Dağıtma ve bir API uygulaması kullanma oluşturma size rehberlik eder bir adım adım öğretici için bkz: [Azure uygulama hizmetinde API uygulamaları ile çalışmaya başlama](app-service-api-dotnet-get-started.md).

API Apps ile Azure API Management kullanıyorsanız, Swagger meta verileri tooimport API'nizi API yönetime kullanabilirsiniz. Daha fazla bilgi için bkz: [nasıl tooimport hello Azure API Management işlemleri olan bir API tanımı](../api-management/api-management-howto-import-api.md). 

