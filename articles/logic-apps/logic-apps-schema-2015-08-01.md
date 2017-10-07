---
title: "aaaSchema güncelleştirmeleri Ağustos 1 2015 preview - Azure Logic Apps | Microsoft Docs"
description: "Şema sürüm 2015-08-01-Önizleme ile Azure Logic Apps için JSON tanımları oluşturma"
author: stepsic-microsoft-com
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 0d03a4d4-e8a8-4c81-aed5-bfd2a28c7f0c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 05/31/2016
ms.author: LADocs; stepsic
ms.openlocfilehash: 950cd18a27aa1859c4f0b6116de3fb8699d746c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="schema-updates-for-azure-logic-apps---august-1-2015-preview"></a>Azure mantıksal uygulamaları - 1 Ağustos 2015 preview şema güncelleştirmeleri

Bu yeni şema ve API sürümü Azure mantıksal uygulamaları için daha fazla mantıksal uygulamalar olun anahtar iyileştirmeler içerir güvenilir ve kolay toouse:

*   Merhaba **APIApp** eylem türüdür yeni güncelleştirilmiş tooa [ **APIConnection** ](#api-connections) eylem türü.
*   **Yineleme** çok adlandırılır[**Foreach**](#foreach).
*   Merhaba [ **HTTP dinleyicisi** API uygulaması](#http-listener) artık gerekli değildir.
*   Alt iş akışlarını çağırma kullanan bir [yeni şema](#child-workflows).

<a name="api-connections"></a>
## <a name="move-tooapi-connections"></a>Taşıma tooAPI bağlantıları

Merhaba büyük değişiklik API'lerini kullanabilmek için toodeploy API uygulamaları Azure aboneliğinizde artık sahip olabilir. API'ler kullanabilirsiniz hello yollar şunlardır:

* Yönetilen API'ler
* Özel Web API'leri

Kendi yönetim ve barındırma modellerini farklı olduğundan her şekilde biraz farklı şekilde ele alınır. Bu modelin avantajlarından biri artık sınırlı Azure kaynak grubunda dağıtılan tooresources. 

### <a name="managed-apis"></a>Yönetilen API'ler

Microsoft Office 365, Salesforce, Twitter ve FTP gibi sizin adınıza bazı API'leri yönetir. Bazı yönetilen API'ler kullanabilirsiniz-diğer yapılandırma gerektirirken, Bing Çevir gibi ise. Bu yapılandırma adlı bir *bağlantı*.

Örneğin, Office 365 kullandığınızda, Office 365 oturum açma belirtecinizi içeren bir bağlantı oluşturmanız gerekir. Bu belirteç güvenli bir şekilde depolanır ve böylece mantıksal uygulamanızı her zaman hello Office 365 API çağrısı yenilenir. Alternatif olarak, tooconnect tooyour SQL veya FTP sunucusunu istiyorsanız hello bağlantı dizesi olan bir bağlantı oluşturmanız gerekir. 

Bu tanımı'nda, bu eylemleri denir `APIConnection`. Office 365 toosend bir e-posta çağıran bir bağlantı bir örneği burada verilmiştir:

```
{
    "actions": {
        "Send_Email": {
            "type": "ApiConnection",
            "inputs": {
                "host": {
                    "api": {
                        "runtimeUrl": "https://msmanaged-na.azure-apim.net/apim/office365"
                    },
                    "connection": {
                        "name": "@parameters('$connections')['shared_office365']['connectionId']"
                    }
                },
                "method": "post",
                "body": {
                    "Subject": "Reminder",
                    "Body": "Don't forget!",
                    "To": "me@contoso.com"
                },
                "path": "/Mail"
            }
        }
    }
}
```

Merhaba `host` nesnesidir benzersiz tooAPI bağlantıları ve satırındaki bölümleri içeren girişleri kısmı: `api` ve `connection`.

Merhaba `api` hello çalışma zamanı, API yönetildiği URL'sini barındırılır sahiptir. Kullanılabilir tüm hello yönetilen API'ler çağırarak görebilirsiniz `GET https://management.azure.com/subscriptions/{subid}/providers/Microsoft.Web/managedApis/?api-version=2015-08-01-preview`.

Bir API kullandığınızda, hello API sahip olabilir veya herhangi bir değil *bağlantı parametrelerini* tanımlanmış. Merhaba API seçili değilse, hiçbir *bağlantı* gereklidir. Merhaba API varsa, bir bağlantı oluşturmanız gerekir. oluşturulan hello bağlantı seçtiğiniz hello adına sahip. Ardından hello hello adına başvuru `connection` nesne hello içinde `host` nesnesi. toocreate çağrısı bir kaynak grubunda bağlantı:

```
PUT https://management.azure.com/subscriptions/{subid}/resourceGroups/{rgname}/providers/Microsoft.Web/connections/{name}?api-version=2015-08-01-preview
```

Gövde aşağıdaki hello ile:

```
{
  "properties": {
    "api": {
      "id": "/subscriptions/{subid}/providers/Microsoft.Web/managedApis/azureblob"
    },
    "parameterValues": {
        "accountName": "{hello name of hello storage account -- hello set of parameters is different for each API}"
    }
  },
  "location": "{Logic app's location}"
}
```

### <a name="deploy-managed-apis-in-an-azure-resource-manager-template"></a>Yönetilen API'leri bir Azure Resource Manager şablonu dağıtma

Etkileşimli oturum açma gerekli olmadığı sürece, tüm bir uygulamayı bir Azure Resource Manager şablonu oluşturabilirsiniz.
Oturum açma gerekiyorsa, her şeyi hello Azure Resource Manager şablonu ile ayarlayabilirsiniz ancak toovisit hello portal tooauthorize hello bağlantıları çözümlenmedi. 

```
    "resources": [{
        "apiVersion": "2015-08-01-preview",
        "name": "azureblob",
        "type": "Microsoft.Web/connections",
        "location": "[resourceGroup().location]",
        "properties": {
            "api": {
                "id": "[concat(subscription().id,'/providers/Microsoft.Web/locations/westus/managedApis/azureblob')]"
            },
            "parameterValues": {
                "accountName": "[parameters('storageAccountName')]",
                "accessKey": "[parameters('storageAccountKey')]"
            }
        }
    }, {
        "type": "Microsoft.Logic/workflows",
        "apiVersion": "2015-08-01-preview",
        "name": "[parameters('logicAppName')]",
        "location": "[resourceGroup().location]",
        "dependsOn": ["[resourceId('Microsoft.Web/connections', 'azureblob')]"
        ],
        "properties": {
            "sku": {
                "name": "[parameters('sku')]",
                "plan": {
                    "id": "[concat(resourceGroup().id, '/providers/Microsoft.Web/serverfarms/',parameters('svcPlanName'))]"
                }
            },
            "definition": {
                "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2015-08-01-preview/workflowdefinition.json#",
                "actions": {
                    "Create_file": {
                        "type": "apiconnection",
                        "inputs": {
                            "host": {
                                "api": {
                                    "runtimeUrl": "https://logic-apis-westus.azure-apim.net/apim/azureblob"
                                },
                                "connection": {
                                    "name": "@parameters('$connections')['azureblob']['connectionId']"
                                }
                            },
                            "method": "post",
                            "queries": {
                                "folderPath": "[concat('/', parameters('containerName'))]",
                                "name": "helloworld.txt"
                            },
                            "body": "@decodeDataUri('data:, Hello+world!')",
                            "path": "/datasets/default/files"
                        },
                        "conditions": []
                    }
                },
                "contentVersion": "1.0.0.0",
                "outputs": {},
                "parameters": {
                    "$connections": {
                        "defaultValue": {},
                        "type": "Object"
                    }
                },
                "triggers": {
                    "recurrence": {
                        "type": "Recurrence",
                        "recurrence": {
                            "frequency": "Day",
                            "interval": 1
                        }
                    }
                }
            },
            "parameters": {
                "$connections": {
                    "value": {
                        "azureblob": {
                            "connectionId": "[concat(resourceGroup().id,'/providers/Microsoft.Web/connections/azureblob')]",
                            "connectionName": "azureblob",
                            "id": "[concat(subscription().id,'/providers/Microsoft.Web/locations/westus/managedApis/azureblob')]"
                        }

                    }
                }
            }
        }
    }]
```

Bu örnekte hello bağlantıların kaynak grubunuzdaki Canlı yalnızca kaynakları olduğunu görebilirsiniz. Yönetilen hello API'leri kullanılabilir tooyou aboneliğinizde başvuruyor.

### <a name="your-custom-web-apis"></a>Özel Web API'leri

Merhaba yerleşik değil Microsoft tarafından yönetilen olanları kendi API kullanırsanız kullanın **HTTP** eylem toocall bunları. İdeal bir deneyim için API için Swagger uç nokta maruz bırakmamalısınız. Bu uç noktaya hello mantığı Uygulama Tasarımcısı toorender hello girişleri etkinleştirir ve API için çıkarır. Swagger hello Tasarımcısı sadece hello girişleri ve çıkışları donuk JSON nesneler olarak gösterebilir.

Yeni bir örnek gösteren hello işte `metadata.apiDefinitionUrl` özelliği:

```
{
   "actions": {
        "mycustomAPI": {
            "type": "http",
            "metadata": {
              "apiDefinitionUrl": "https://mysite.azurewebsites.net/api/apidef/"  
            },
            "inputs": {
                "uri": "https://mysite.azurewebsites.net/api/getsomedata",
                "method": "GET"
            }
        }
    }
}
```

Azure App Service'te Web API'nizi barındırıyorsanız, Web API otomatik olarak hello Tasarımcısı'nda kullanılabilir eylemleri hello listesinde görüntülenir. Değilse, toopaste hello URL'de doğrudan sahip. Merhaba API kendisini Swagger destekler ne olursa olsun yöntemleriyle güvenli rağmen hello Swagger uç nokta kimliği doğrulanmamış toobe hello mantığı Uygulama Tasarımcısı kullanılabilir olması gerekir.

### <a name="call-deployed-api-apps-with-2015-08-01-preview"></a>Dağıtılan API apps 2015-08-01-Önizleme ile çağırın

Bir API uygulamasını daha önce dağıttıysanız hello hello uygulamayla çağırabilirsiniz **HTTP** eylem.

Örneğin, Dropbox toolist dosyaları kullanırsanız, **2014-12-01-Önizleme** şema sürümü tanımı şöyle olabilir:

```
{
    "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2014-12-01-preview/workflowdefinition.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector/token": {
            "defaultValue": "eyJ0eX...wCn90",
            "type": "String",
            "metadata": {
                "token": {
                    "name": "/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector/token"
                }
            }
        }
    },
    "actions": {
        "dropboxconnector": {
            "type": "ApiApp",
            "inputs": {
                "apiVersion": "2015-01-14",
                "host": {
                    "id": "/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector",
                    "gateway": "https://avdemo.azurewebsites.net"
                },
                "operation": "ListFiles",
                "parameters": {
                    "FolderPath": "/myfolder"
                },
                "authentication": {
                    "type": "Raw",
                    "scheme": "Zumo",
                    "parameter": "@parameters('/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector/token')"
                }
            }
        }
    }
}
```

Merhaba parametreleri hello mantıksal uygulama tanımını bölümünü değişmeden kalır ancak bu örnek gibi hello eşdeğer HTTP eylemi oluşturabileceğiniz:

```
{
    "actions": {
        "dropboxconnector": {
            "type": "Http",
            "metadata": {
              "apiDefinitionUrl": "https://avdemo.azurewebsites.net/api/service/apidef/dropboxconnector/?api-version=2015-01-14&format=swagger-2.0-standard"  
            },
            "inputs": {
                "uri": "https://avdemo.azurewebsites.net/api/service/invoke/dropboxconnector/ListFiles?api-version=2015-01-14",
                "method": "POST",
                "body": {
                    "FolderPath": "/myfolder"
                },
                "authentication": {
                    "type": "Raw",
                    "scheme": "Zumo",
                    "parameter": "@parameters('/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector/token')"
                }
            }
        }
    }
}
```

Bu özellikleri tek tek taramasını:

| Action özelliği | Açıklama |
| --- | --- |
| `type` |`Http`Onun yerine`APIapp` |
| `metadata.apiDefinitionUrl` |toouse, bu eylemin hello mantığı Uygulama Tasarımcısı'ndan oluşturulan hello meta veri uç şunları içerir:`{api app host.gateway}/api/service/apidef/{last segment of hello api app host.id}/?api-version=2015-01-14&format=swagger-2.0-standard` |
| `inputs.uri` |Gelen oluşturulur:`{api app host.gateway}/api/service/invoke/{last segment of hello api app host.id}/{api app operation}?api-version=2015-01-14` |
| `inputs.method` |Her zaman`POST` |
| `inputs.body` |Aynı toohello API uygulaması parametreleri |
| `inputs.authentication` |Aynı toohello API uygulama kimlik doğrulaması |

Bu yaklaşım, tüm API uygulaması eylemler için çalışması gerekir. Ancak, bu önceki API uygulamaları artık desteklendiğini unutmayın. Bu nedenle hello tooone iki diğer önceki seçenekleri, yönetilen bir API veya özel Web API'nizi barındıran taşımanız gerekir.

<a name="foreach"></a>
## <a name="renamed-repeat-tooforeach"></a>'Repeat' too'foreach yeniden adlandırılmış '

Merhaba önceki şema sürümü için çok müşteri geri bildirimi aldık, **yineleyin** kafa karıştırıcı ve düzgün şekilde yakalama alamadık **yineleyin** gerçekten için-her bir döngü oluştu. Sonuç olarak, biz adlandırdınız `repeat` çok`foreach`. Örneğin, daha önce aşağıdakileri yazarsınız:

```
{
    "actions": {
        "pingBing": {
            "type": "Http",
            "repeat": "@range(0,2)",
            "inputs": {
                "method": "GET",
                "uri": "https://www.bing.com/search?q=@{repeatItem()}"
            }
        }
    }
}
```

Şimdi, yazarsınız:

```
{
    "actions": {
        "pingBing": {
            "type": "Http",
            "foreach": "@range(0,2)",
            "inputs": {
                "method": "GET",
                "uri": "https://www.bing.com/search?q=@{item()}"
            }
        }
    }
}
```

Merhaba işlevi `@repeatItem()` olan daha önce kullanılan tooreference hello geçerli öğe olan yinelendiğinde üzerinden. Bu işlev artık çok basitleştirilmiştir`@item()`. 

### <a name="reference-outputs-from-foreach"></a>'Foreach' başvuru çıkışlarından

Gelen hello basitleştirme için çıkarır `foreach` Eylemler adlı bir nesne değil sarılır `repeatItems`. Merhaba hello önceki çıkarır sırada `repeat` örnek olan:

```
{
    "repeatItems": [
        {
            "name": "pingBing",
            "inputs": {
                "uri": "https://www.bing.com/search?q=0",
                "method": "GET"
            },
            "outputs": {
                "headers": { },
                "body": "<!DOCTYPE html><html lang=\"en\" xml:lang=\"en\" xmlns=\"http://www.w3.org/1999/xhtml\" xmlns:Web=\"http://schemas.live.com/Web/\">...</html>"
            }
            "status": "Succeeded"
        }
    ]
}
```

Bu çıktı sunulmuştur:

```
[
    {
        "name": "pingBing",
        "inputs": {
            "uri": "https://www.bing.com/search?q=0",
            "method": "GET"
        },
        "outputs": {
            "headers": { },
            "body": "<!DOCTYPE html><html lang=\"en\" xml:lang=\"en\" xmlns=\"http://www.w3.org/1999/xhtml\" xmlns:Web=\"http://schemas.live.com/Web/\">...</html>"
        }
        "status": "Succeeded"
    }
]
```

Daha önce tooget toohello gövdesi bu çıktılar başvururken hello eylem:

```
{
    "actions": {
        "secondAction": {
            "type": "Http",
            "repeat": "@outputs('pingBing').repeatItems",
            "inputs": {
                "method": "POST",
                "uri": "http://www.example.com",
                "body": "@repeatItem().outputs.body"
            }
        }
    }
}
```

Bunun yerine şimdi yapabilirsiniz:

```
{
    "actions": {
        "secondAction": {
            "type": "Http",
            "foreach": "@outputs('pingBing')",
            "inputs": {
                "method": "POST",
                "uri": "http://www.example.com",
                "body": "@item().outputs.body"
            }
        }
    }
}
```

Bu değişiklikler ile Merhaba işlevleri `@repeatItem()`, `@repeatBody()`, ve `@repeatOutputs()` kaldırılır.

<a name="http-listener"></a>
## <a name="native-http-listener"></a>Yerel HTTP dinleyicisi

Merhaba HTTP dinleyicisi özellikleri artık yerleşiktir. Bu nedenle, artık toodeploy bir HTTP dinleyicisi API uygulaması gerekir. Bkz: [hello ayrıntıların nasıl toomake, mantığı uygulama uç noktası aranabilir burada](../logic-apps/logic-apps-http-endpoint.md). 

Bu değişikliklerle biz hello kaldırılan `@accessKeys()` biz hello ile değiştirilen işlevi `@listCallbackURL()` hello endpoint gerektiğinde alma işlevi. Ayrıca, mantıksal uygulamanızı şimdi en az bir tetikleyici tanımlamanız gerekir. Çok istiyorsanız`/run` iş akışı Merhaba, bu Tetikleyiciler birine sahip olmalıdır: `manual`, `apiConnectionWebhook`, veya `httpWebhook`.

<a name="child-workflows"></a>
## <a name="call-child-workflows"></a>Alt iş akışlarını çağırma

Daha önce alt iş akışlarını çağırma toohello iş akışı, hello erişim belirteci ve yapıştırma hello belirteci toocall istediğiniz hello mantığı uygulama tanımında alt iş akışının alma giderek gereklidir. Merhaba tanımı tüm gizli olmayan sahip çok yapıştırdığınız şekilde hello yeni şema ile Merhaba Logic Apps altyapısı SAS için çalışma zamanında otomatik olarak oluşturur alt iş akışı hello. Örnek aşağıda verilmiştir:

```
"mynestedwf": {
    "type": "workflow",
    "inputs": {
        "host": {
            "id": "/subscriptions/xxxxyyyyzzz/resourceGroups/rg001/providers/Microsoft.Logic/mywf001",
            "triggerName": "myendpointtrigger"
        },
        "queries": {
            "extrafield": "specialValue"
        },
        "headers": {
            "x-ms-date": "@utcnow()",
            "Content-type": "application/json"
        },
        "body": {
            "contentFieldOne": "value100",
            "anotherField": 10.001
        }
    },
    "conditions": []
}
```

İkinci bir geliştirme hello alt iş akışları tam erişim toohello gelen istek verirsiniz ' dir. Hello parametreleri geçirebilirsiniz anlamına *sorguları* bölüm ve hello *üstbilgileri* nesne ve tam olarak tanımlayabileceğiniz hello tüm gövdesi.

Son olarak, gerekli değişiklikleri toohello alt iş akışı vardır. Şimdi daha önce bir alt iş akışı doğrudan çağırabilirsiniz olsa da, hello iş akışında hello üst toocall için bir tetikleyici uç noktasını tanımlamanız gerekir. Genellikle, sahip bir tetikleyici eklemek `manual` yazın ve ardından tetikleyicisi hello üst tanımında kullanın. Not hello `host` özelliği özellikle sahip bir `triggerName` tetikleyicinin her zaman belirtmeniz gerekir çünkü çağırma.

## <a name="other-changes"></a>Diğer değişiklikler

### <a name="new-queries-property"></a>Yeni 'sorguları' özelliği

Tüm eylem türleri şimdi adlı yeni bir giriş Destek `queries`. Bu giriş, yapılandırılmış nesne yerine, el ile tooassemble hello dize sahip olabilir.

### <a name="renamed-parse-function-toojson"></a>'Parse()' işlevi too'json() yeniden adlandırılmış '

Biz hello yeniden adlandırılmış şekilde daha fazla içerik türleri yakında ekliyoruz `parse()` çok işlev`json()`.

## <a name="coming-soon-enterprise-integration-apis"></a>Yakında: Kurumsal tümleştirme API'leri

Biz yönetilen sürümleri henüz hello AS2 gibi Kurumsal tümleştirme API'leri yok. Bu arada, var olan dağıtılmış BizTalk API'leri aracılığıyla hello HTTP eylemi kullanabilirsiniz. Ayrıntılar için bkz: "zaten dağıtılmış API uygulamalarınızı hello kullanarak" [tümleştirme Haritası](http://www.zdnet.com/article/microsoft-outlines-its-cloud-and-server-integration-roadmap-for-2016/). 
