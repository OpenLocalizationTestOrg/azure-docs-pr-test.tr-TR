---
title: "aaaSecure erişim tooAzure Logic Apps | Microsoft Docs"
description: "Erişim tootriggers, girişleri ve çıkışları, eylem parametrelerini ve iş akışlarıyla Azure Logic Apps içinde kullanılan hizmetler korumaya yönelik güvenlik ekleyin."
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 9fab1050-cfbc-4a8b-b1b3-5531bee92856
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 11/22/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: abda2179e4cc2d2295cd8332ec017c848a456264
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-access-tooyour-logic-apps"></a>Tooyour logic apps güvenli erişim

Mantıksal uygulamanızı güvenli birçok Araçlar kullanılabilir toohelp vardır.

* Bir mantıksal uygulama (HTTP isteği tetikleyici) erişim tootrigger güvenli hale getirme
* Erişim toomanage güvenli hale getirme, düzenleme veya bir mantıksal uygulama okuma
* Erişim toocontents girişleri ve çıkışları bir çalışması için güvenli hale getirme
* Parametreleri ya da bir iş akışında Eylemler içinde girişleri güvenliğini sağlama
* Bir iş akışından isteklerini alacak erişim tooservices güvenliğini sağlama

## <a name="secure-access-tootrigger"></a>Güvenli erişim tootrigger

Bir HTTP isteğiyle tetiklenen bir mantıksal uygulama ile çalışırken ([isteği](../connectors/connectors-native-reqres.md) veya [Web kancası](../connectors/connectors-native-webhook.md)), böylece yalnızca yetkili istemcilerin hello mantıksal uygulama tetikleyebilir erişimi kısıtlayabilirsiniz. Bir mantıksal uygulama içinde tüm istekleri şifrelenir ve SSL güvenli.

### <a name="shared-access-signature"></a>Paylaşılan erişim imzası

Her istek uç noktası için bir mantıksal uygulama içeren bir [paylaşılan erişim imzası (SAS)](../storage/common/storage-dotnet-shared-access-signature-part-1.md) hello URL'SİNİN bir parçası olarak. Her URL içeren bir `sp`, `sv`, ve `sig` sorgu parametresi. İzinleri tarafından belirtilen `sp`, ve izin verilen, tooHTTP yöntemleri karşılık `sv` hello kullanılan sürümü toogenerate olan ve `sig` kullanılan tooauthenticate erişim tootrigger değil. Merhaba imza, gizli bir anahtar tüm hello URL yollarını ve özellikleri ile Merhaba SHA256 algoritması kullanılarak oluşturulur. Merhaba gizli anahtar hiçbir zaman kullanıma sunulan ve yayımlanan ve şifrelenmiş ve hello mantığı uygulamanın parçası olarak depolanan tutulur. Mantıksal uygulamanızı yalnızca hello gizli anahtarı ile oluşturulan geçerli bir imzası içeren Tetikleyicileri yetkilendirir.

#### <a name="regenerate-access-keys"></a>Erişim anahtarlarını yeniden oluştur

Yeni güvenli bir anahtar adresindeki hello REST API veya Azure portalı üzerinden dilediğiniz zaman yeniden oluşturabilirsiniz. Merhaba eski anahtarı kullanarak önceden oluşturulan tüm geçerli URL'ler geçersiz ve artık yetkili toofire hello mantıksal uygulama ' dir.

1. Hello Azure portal, tooregenerate bir anahtar istediğiniz hello mantıksal uygulama açın
1. Merhaba tıklatın **erişim tuşları** menü öğesi altında **ayarları**
1. Merhaba anahtar tooregenerate ve tam hello işlemi seçin

Yeniden oluşturma tamamlandıktan sonra alma URL'leri hello yeni erişim anahtarı ile imzalanmış.

#### <a name="creating-callback-urls-with-an-expiration-date"></a>Geri çağırma URL'leri bir sona erme tarihi ile oluşturma

Diğer kuruluşlarla hello URL paylaşıyorsanız, özel anahtarları ve gerektiği gibi sona erme tarihleri ile URL'leri oluşturabilir. Daha sonra sorunsuzca anahtarları alma, veya bir uygulamaya erişim toofire sağlamak belirli timespan kısıtlı tooa değil. Merhaba aracılığıyla bir URL'ye ilişkin bir sona erme tarihi belirtebilirsiniz [logic apps REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers):

``` http
POST 
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Logic/workflows/{workflowName}/triggers/{triggerName}/listCallbackUrl?api-version=2016-06-01
```

Merhaba gövdesinde hello özelliğini içeren `NotAfter` bir JSON tarih dizesi döndüren hello kadar yalnızca geçerli bir geri çağırma URL'si `NotAfter` tarih ve saat.

#### <a name="creating-urls-with-primary-or-secondary-secret-key"></a>Birincil veya ikincil gizli anahtarla URL'ler oluşturma

Oluşturmak veya istek tabanlı tetikleyiciler için geri çağırma URL'lerin listesi, hangi anahtar toouse toosign hello URL de belirtebilirsiniz.  Merhaba aracılığıyla belirli bir anahtarı tarafından imzalanan bir URL oluşturabileceğiniz [logic apps REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers) gibi:

``` http
POST 
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Logic/workflows/{workflowName}/triggers/{triggerName}/listCallbackUrl?api-version=2016-06-01
```

Merhaba gövdesinde hello özelliğini içeren `KeyType` olarak `Primary` veya `Secondary`.  Merhaba güvenli anahtar belirtilen tarafından imzalanmış bir URL döndürür.

### <a name="restrict-incoming-ip-addresses"></a>Gelen IP adreslerini kısıtlamak

Ayrıca toohello paylaşılan erişim imzası, yalnızca belirli istemcilerinden bir mantıksal uygulama çağırma toorestrict isteyebilir.  Örneğin, uç noktanızı Azure API Management üzerinden yönetiyorsanız, hello mantığı kısıtlayabilirsiniz uygulama tooonly hello isteği hello API Management örneği IP adres geldiğinde hello isteğini kabul.

Bu ayar hello mantığını uygulaması ayarları içinde yapılandırılabilir:

1. Hello Azure portal, tooadd IP adresi sınırlamaları istediğiniz hello mantıksal uygulama açın
1. Merhaba tıklatın **erişim denetimini yapılandırma** menü öğesi altında **ayarları**
1. IP adresi aralıkları toobe hello tetik tarafından kabul Hello listesini belirtin

Geçerli bir IP aralığı hello biçimini alır `192.168.1.1/255`. Merhaba mantığı uygulama tooonly yangın iç içe geçmiş mantıksal uygulama olarak istiyorsanız hello seçin **yalnızca diğer logic apps** seçeneği. Bu seçenek yalnızca çağrılarından hello kendisini (üst mantıksal uygulamalar) yangın başarıyla hizmet anlamına boş dizi toohello kaynak yazar.

> [!NOTE]
> Hala bir mantıksal uygulama isteği tetikleyici ile Merhaba REST API çalıştırabilirsiniz / Yönetim `/triggers/{triggerName}/run` IP ne olursa olsun. Bu senaryo hello Azure REST API'sine karşı kimlik doğrulamasını gerektirir ve tüm olayları hello Azure denetim günlüğünü görünür. Set erişim ilkelerini uygun şekilde denetler.

#### <a name="setting-ip-ranges-on-hello-resource-definition"></a>IP aralıklarını hello kaynak tanımı'nda ayarlama

Kullanıyorsanız bir [dağıtım şablonu](logic-apps-create-deploy-template.md) tooautomate hello IP aralığı ayarlarını dağıtımlarınızı hello kaynak şablonuna yapılandırılabilir.  

``` json
{
    "properties": {
        "definition": {
        },
        "parameters": {},
        "accessControl": {
            "triggers": {
                "allowedCallerIpAddresses": [
                    {
                        "addressRange": "192.168.12.0/23"
                    },
                    {
                        "addressRange": "2001:0db8::/64"
                    }
                ]
            }
        }
    },
    "type": "Microsoft.Logic/workflows"
}

```

### <a name="adding-azure-active-directory-oauth-or-other-security"></a>Azure Active Directory, OAuth veya diğer güvenlik ekleme

Daha fazla yetkilendirme protokolleri bir mantıksal uygulama üstünde tooadd [Azure API Management](https://azure.microsoft.com/services/api-management/) zengin izleme, güvenlik, ilke ve belgeleri hello yetenek tooexpose ile herhangi bir uç nokta için bir mantıksal uygulama olarak bir API sunar. Azure API Management genel veya özel uç noktası için Azure Active Directory, sertifika, OAuth veya diğer güvenlik standartları kullanabilirsiniz hello mantıksal uygulama getirebilir. Bir istek alındığında, Azure API Management hello isteği toohello mantıksal uygulama (herhangi bir gerekli dönüşümleri veya kısıtlamaları yürütülen gerçekleştirerek) iletir. Merhaba mantığı uygulama tooonly ayarlarını hello mantığı uygulama toobe tetiklenen API Yönetimi'nden izin hello gelen IP aralığı kullanabilirsiniz.

## <a name="secure-access-toomanage-or-edit-logic-apps"></a>Toomanage veya düzenleme logic apps güvenli erişim

Yalnızca belirli kullanıcılara veya gruplara hello kaynak mümkün tooperform işlemleri; böylece bir mantıksal uygulama erişim toomanagement işlemlerine kısıtlayabilirsiniz. Logic apps kullanmak hello Azure [rol tabanlı erişim denetimi (RBAC)](../active-directory/role-based-access-control-configure.md) özellik ve hello ile özelleştirilebilir aynı araçları.  Abonelik tooas üyeleri de atayabilirsiniz birkaç yerleşik roller vardır:

* **Mantığı uygulamasını katkıda bulunan** -erişim tooview, düzenleme ve güncelleştirme bir mantıksal uygulama sağlar.  Merhaba kaynak kaldıramaz veya yönetim işlemleri.
* **Mantıksal uygulama işleci** - görüntüleyebilir hello mantıksal uygulama ve çalıştırma geçmişi ve etkinleştir/devre dışı bırak.  Düzenleyemez veya hello tanımını güncelleştirin.

Aynı zamanda [Azure kaynak kilidi](../azure-resource-manager/resource-group-lock-resources.md) değiştirme veya silme logic apps tooprevent. Bu özellik değerli tooprevent üretim kaynaklardan değişiklikleri ya da silme işlemleri olur.

## <a name="secure-access-toocontents-of-hello-run-history"></a>Güvenli erişim toocontents çalıştırma geçmişi Merhaba

Önceki çalışır toospecific IP adres aralıklarının erişim toocontents girişleri veya çıkışları kısıtlayabilirsiniz.  

Yoldaki ve bekleyen iş akışı çalışması içinde tüm veriler şifrelenir. Bir arama toorun geçmişini yapıldığında, hello hizmet hello isteğin kimliğini doğrular ve bağlantıları toohello istek ve yanıt girişleri ve çıkışları sağlar. Bu bağlantı, atanan IP adres aralığından gelen tooview içeriği döndürmesi hello içeriği korumalı böylece yalnızca istekleri olabilir. Ek erişim denetimi için bu özelliği kullanabilirsiniz. Bir IP adresi gibi bile belirtebilirsiniz `0.0.0.0` hiç bir girdi/çıktı erişebilecek şekilde. Merhaba olasılığı için 'just-in-time' erişim tooworkflow içerik sağlama yalnızca yönetici izinlerine sahip olan kişi bu kısıtlama kaldırabilirsiniz.

Bu ayar hello kaynak ayarlarını hello Azure portalı içinde yapılandırılabilir:

1. Hello Azure portal, tooadd IP adresi sınırlamaları istediğiniz hello mantıksal uygulama açın
1. Merhaba tıklatın **erişim denetimini yapılandırma** menü öğesi altında **ayarları**
1. IP adresi aralıkları için erişim toocontent Hello listesini belirtin

#### <a name="setting-ip-ranges-on-hello-resource-definition"></a>IP aralıklarını hello kaynak tanımı'nda ayarlama

Kullanıyorsanız bir [dağıtım şablonu](logic-apps-create-deploy-template.md) tooautomate hello IP aralığı ayarlarını dağıtımlarınızı hello kaynak şablonuna yapılandırılabilir.  

``` json
{
    "properties": {
        "definition": {
        },
        "parameters": {},
        "accessControl": {
            "contents": {
                "allowedCallerIpAddresses": [
                    {
                        "addressRange": "192.168.12.0/23"
                    },
                    {
                        "addressRange": "2001:0db8::/64"
                    }
                ]
            }
        }
    },
    "type": "Microsoft.Logic/workflows"
}
```

## <a name="secure-parameters-and-inputs-within-a-workflow"></a>Güvenli parametreleri ve iş akışı içinde girişleri

Dağıtım için bir iş akışı tanımı bazı yönlerini tooparameterize ortamlar genelinde isteyebilirsiniz. Ayrıca, bazı parametreler gibi bir istemci kimliği ve istemci parolası için bir iş akışı düzenlerken tooappear istemiyorsanız güvenli parametreler olabilir [Azure Active Directory kimlik doğrulaması](../connectors/connectors-native-http.md#authentication) bir HTTP eylem.

### <a name="using-parameters-and-secure-parameters"></a>Parametreleri ve güvenli parametrelerini kullanma

tooaccess hello çalışma zamanında kaynak parametresinin değeri hello [iş akışı tanımlama dili](http://aka.ms/logicappsdocs) sağlayan bir `@parameters()` işlemi. Ayrıca, [hello kaynak dağıtım şablonu parametrelerini belirtin](../azure-resource-manager/resource-group-authoring-templates.md#parameters). Ancak başlangıç parametresi türü olarak belirtirseniz, `securestring`, hello parametresi hello hello kaynak tanımı kalanıyla döndürülen olmaz ve dağıtımdan sonra hello kaynak görüntüleyerek erişilebilir olmayacaktır.

> [!NOTE]
> Parametreniz hello üstbilgilerinde veya bir istek gövdesi kullanılırsa, hello parametre görünür hello çalıştırma geçmişi ve giden HTTP istek erişerek olabilir. Emin tooset içerik erişim ilkelerinizi buna göre yapın.
> Yetkilendirme üstbilgileri hiçbir zaman girişleri veya çıkışları görünür. Bu nedenle Hello gizli var. kullanılıyorsa hello gizli alınabilir değil.

#### <a name="resource-deployment-template-with-secrets"></a>Gizli anahtarlarla kaynak dağıtım şablonu

Merhaba aşağıdaki örnekte güvenli parametresinin başvuruda bulunan bir dağıtım gösterir `secret` çalışma zamanında. Ayrı Parametreler dosyasında hello hello ortamı değerini belirtebilirsiniz `secret`, veya [Azure Resource Manager KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) adresindeki tooretrieve gizli dağıtmak zaman.

``` json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "secretDeploymentParam": {
      "type": "securestring"
    }
  },
  "variables": {},
  "resources": [
    {
      "name": "secret-deploy",
      "type": "Microsoft.Logic/workflows",
      "location": "westus",
      "tags": {
        "displayName": "LogicApp"
      },
      "apiVersion": "2016-06-01",
      "properties": {
        "definition": {
          "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
          "actions": {
            "Call_External_API": {
              "type": "http",
              "inputs": {
                "headers": {
                  "Authorization": "@parameters('secret')"
                },
                "body": "This is hello request"
              },
              "runAfter": {}
            }
          },
          "parameters": {
            "secret": {
              "type": "SecureString"
            }
          },
          "triggers": {
            "manual": {
              "type": "Request",
              "kind": "Http",
              "inputs": {
                "schema": {}
              }
            }
          },
          "contentVersion": "1.0.0.0",
          "outputs": {}
        },
        "parameters": {
          "secret": {
            "value": "[parameters('secretDeploymentParam')]"
          }
        }
      }
    }
  ],
  "outputs": {}
}
```

## <a name="secure-access-tooservices-receiving-requests-from-a-workflow"></a>Bir iş akışı alma isteklerini tooservices güvenli erişim

Herhangi bir uç nokta hello mantığı uygulama tooaccess gereken güvenli birçok yolu toohelp vardır.

### <a name="using-authentication-on-outbound-requests"></a>Giden isteklerinde kimlik doğrulaması kullanma

Bir HTTP, HTTP + Swagger (açık API) veya Web kancası eylemi ile çalışırken, kimlik doğrulama toohello isteği gönderilen ekleyebilirsiniz. Temel kimlik doğrulaması, sertifika kimlik doğrulaması veya Azure Active Directory kimlik doğrulaması dahil olabilir. Bu kimlik doğrulama tooconfigure nasıl bulunabilir Ayrıntılar [bu makalede](../connectors/connectors-native-http.md#authentication).

### <a name="restricting-access-toologic-app-ip-addresses"></a>Erişim toologic uygulama IP adreslerine kısıtlama

Logic apps gelen tüm çağrıları belirli bir IP adresleri her bölge kümesini gelmektedir. Ek filtreleme ekleyebilirsiniz tooonly bu IP adreslerini belirlenmiş gelen istekleri kabul edin. Bu IP adresleri listesi için bkz: [mantığı uygulama sınırlarını ve yapılandırmasını](logic-apps-limits-and-config.md#configuration).

### <a name="on-premises-connectivity"></a>Şirket içi bağlantı

Logic apps birkaç Hizmetleri tooprovide güvenli ve güvenilir ile tümleştirme içi iletişim sağlar.

#### <a name="on-premises-data-gateway"></a>Şirket içi veri ağ geçidi

Birçok yönetilen bağlayıcılar mantıksal uygulamalar için güvenli bağlantı tooon içi sistemleri, dosya sistemi, SQL, SharePoint, DB2 ve daha fazlası da dahil olmak üzere sağlar. Merhaba ağ geçidi şifrelenmiş kanalda hello Azure Service Bus aracılığıyla şirket içi kaynaklardan veri aktarır. Güvenli giden trafiği hello ağ geçidi aracısından olarak tüm trafiğin kaynaklandığı. Daha fazla bilgi edinmek [hello veri ağ geçidi nasıl çalıştığını](logic-apps-gateway-install.md#gateway-cloud-service).

#### <a name="azure-api-management"></a>Azure API Management

[Azure API Management](https://azure.microsoft.com/services/api-management/) güvenli proxy ve iletişim tooon içi sistemler için siteden siteye VPN ve ExpressRoute tümleştirme de dahil olmak üzere şirket içi bağlantı seçenekleri vardır. Hello mantığı Uygulama Tasarımcısı'de, hızlı bir şekilde tooon içi sistemleri hızlı erişim sağlayan Azure API Yönetimi'nden bir iş akışı içinde kullanıma sunulan bir API'yi seçebilirsiniz.

#### <a name="hybrid-connections-from-azure-app-service"></a>Karma bağlantılar Azure uygulama hizmeti

Azure API ve Web uygulamaları toocommunicate şirket içi hello şirket içi karma bağlantı özelliğini kullanabilirsiniz.  Karma bağlantılar ve tooconfigure nasıl bulunabilir hakkında ayrıntılar [bu makalede](../app-service-web/web-sites-hybrid-connection-get-started.md).

## <a name="next-steps"></a>Sonraki adımlar
[Bir dağıtım şablonu oluşturma](logic-apps-create-deploy-template.md)  
[Özel durum işleme](logic-apps-exception-handling.md)  
[Mantıksal uygulamalarınızı izleyin](logic-apps-monitor-your-logic-apps.md)  
[Mantıksal uygulama hatalarını ve sorunlarını tanılama](logic-apps-diagnosing-failures.md)  
