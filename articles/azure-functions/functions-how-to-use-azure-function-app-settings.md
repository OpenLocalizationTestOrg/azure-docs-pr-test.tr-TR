---
title: "aaaConfigure Azure işlevi uygulama ayarları | Microsoft Docs"
description: "Nasıl tooconfigure Azure işlev uygulaması ayarları hakkında bilgi edinin."
services: 
documentationcenter: .net
author: rachelappel
manager: erikre
editor: 
ms.assetid: 81eb04f8-9a27-45bb-bf24-9ab6c30d205c
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 04/23/2017
ms.author: glenga
ms.openlocfilehash: 539e203ac449061ef3ceae5e93df3bdbb326e43b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-a-function-app-in-hello-azure-portal"></a>Nasıl toomanage hello Azure portal'ın bir işlev uygulaması 

Azure işlevleri, bir işlev uygulaması, tek tek işlevleri için hello yürütme bağlamı sağlar. Verilen işlevin uygulama tarafından barındırılan tooall işlevleri işlevi uygulama davranışları uygulayın. Bu konuda açıklanmaktadır nasıl tooconfigure ve işlev uygulamalarınızda hello Azure portalında yönetin.

toobegin, Git toohello [Azure portal](http://portal.azure.com) ve tooyour Azure hesabı oturum açın. Merhaba arama çubuğunda hello portal hello üstündeki işlevi uygulamanızı hello adını yazın ve hello listeden seçin. İşlev uygulamanızı seçtikten sonra sayfa aşağıdaki hello bakın:

![Hello Azure portal işlevi uygulama genel bakış](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-main.png)

## <a name="manage-app-service-settings"></a>İşlev uygulama ayarları sekmesi

![İşlev uygulama hello Azure portalına genel bakış.](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-settings-tab.png)

Merhaba **ayarları** sekme kullanılabilir işlevi uygulamanız tarafından kullanılan hello işlevleri çalışma zamanı sürümü burada güncelleştirebilirsiniz. Ayrıca, hello konak kullanılan anahtarları toorestrict HTTP erişim tooall işlevleri hello işlevi uygulama tarafından barındırılan yöneteceğiniz unutulmamalıdır.

İşlevler tüketim barındırma ve App Service planları barındırma destekler. Daha fazla bilgi için bkz: [Seç hello doğru hizmet planı Azure işlevleri için](functions-scale.md). Merhaba tüketim planında daha iyi öngörülebilirlik için işlevleri sağlar, günlük kullanım kotası gigabayt saniye olarak ayarlayarak platform kullanımını sınırla. Merhaba günlük kullanım kotası ulaşıldığında, hello işlev uygulaması durdurulur. Kota harcama hello ulaştıktan sonucunda durduruldu bir işlev uygulaması hello yeniden etkinleştirilebilir günlük kota harcama hello kurma olarak aynı bağlamı. Merhaba bkz [Azure fiyatlandırma sayfası işlevleri](http://azure.microsoft.com/pricing/details/functions/) faturalama hakkında ayrıntılı bilgi için.   

## <a name="platform-features-tab"></a>Platform Özellikleri sekmesi

![İşlev uygulama platformu Özellikleri sekmesi.](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-features-tab.png)

İşlev uygulamalarının çalıştırmak ve hello Azure App Service platformu tarafından korunur. Bu nedenle, işlevi uygulamalarınızı hello Azure'nın çekirdek web barındırma platformu özelliklerini erişim toomost sahip. Merhaba **Platform özellikleri** sekme, burada erişim hello hello işlevi uygulamalarınızda kullanabileceğiniz App Service platformu özelliklerinin çoğu kullanılabilir. 

> [!NOTE]
> Bir işlev uygulaması hello tüketim barındırma planı üzerinde çalıştığında, tüm uygulama hizmeti özellikleri kullanılabilir.

Bu konunun geri kalanında Hello hello hello uygulama hizmeti özelliklerinde aşağıdaki işlevleri için yararlı olan Azure portal odaklanır:

+ [Uygulama hizmeti Düzenleyicisi](#editor)
+ [Uygulama ayarları](#settings) 
+ [Console](#console)
+ [Gelişmiş araçlar (Kudu)](#kudu)
+ [Dağıtım seçenekleri](#deployment)
+ [CORS](#cors)
+ [Kimlik doğrulaması](#auth)
+ [API tanımı](#swagger)

Hakkında daha fazla bilgi için uygulama hizmeti ayarlarla toowork bkz [Azure App Service ayarlarını yapılandır](../app-service-web/web-sites-configure.md).

### <a name="editor"></a>Uygulama hizmeti Düzenleyicisi

| | |
|-|-|
| ![İşlev uygulaması App Service Düzenleyici.](./media/functions-how-to-use-azure-function-app-settings/function-app-appsvc-editor.png)  | Hello uygulama hizmeti Düzenleyicisi toomodify JSON yapılandırma dosyalarını ve kod dosyaları aynı şekilde kullanabileceğiniz bir Gelişmiş portala düzenleyicisidir. Bu seçeneğin belirlenmesi temel bir düzenleyici olan ayrı bir tarayıcı sekmesi başlatır. Bu toointegrate hello Git deposu, çalıştırma ve hata ayıklama kodu sağlar ve işlev uygulama ayarlarını değiştirebilirsiniz. Bu düzenleyici hello varsayılan işlevi uygulaması dikey ile karşılaştırıldığında, İşlevler için bir Gelişmiş geliştirme ortamı sağlar.    |

![Merhaba uygulama hizmeti Düzenleyicisi](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-appservice-editor.png)

### <a name="settings"></a>Uygulama ayarları

| | |
|-|-|
| ![İşlev app uygulama ayarları.](./media/functions-how-to-use-azure-function-app-settings/function-app-application-settings.png) | Uygulama hizmeti Hello **uygulama ayarları** dikey penceresinde, burada yapılandırın ve framework sürümleri, uzaktan hata ayıklama, uygulama ayarları ve bağlantı dizelerini Yönet. Diğer Azure ve üçüncü taraf hizmetleri ile işlevi uygulamanızı'i tümleştirdiğinizde burada bu ayarları değiştirebilirsiniz. |

![Uygulama ayarlarını yapılandırın](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-settings.png)

### <a name="console"></a>Konsol

| | |
|-|-|
| ![Hello Azure portalında uygulama konsolunda işlevi](./media/functions-how-to-use-azure-function-app-settings/function-app-console.png) | Merhaba komut satırından işlevi uygulamanızla toointeract tercih zaman hello portala konsolu bir ideal Geliştirici aracıdır. Sık kullanılan komutlar dizin ve dosya oluşturma ve gezinti yanı toplu iş dosyaları ve komut dosyaları yürütme içerir. |

![Uygulama Konsolu işlevi](./media/functions-how-to-use-azure-function-app-settings/configure-function-console.png)

### <a name="kudu"></a>Gelişmiş araçlar (Kudu)

| | |
|-|-|
| ![Hello Azure portal Kudu uygulamada işlevi](./media/functions-how-to-use-azure-function-app-settings/function-app-advanced-tools.png) | Merhaba uygulama hizmeti (Kudu olarak da bilinir) için Gelişmiş araçlar erişim işlevi uygulamanızı tooadvanced yönetim özelliklerini sağlar. Kudu sistem bilgileri, uygulama ayarları, ortam değişkenleri, site uzantıları, HTTP üstbilgileri ve sunucu değişkenlerine yönetin. Ayrıca başlatma **Kudu** işlev uygulamanız için toohello SCM uç noktasının gibi giderek`https://<myfunctionapp>.scm.azurewebsites.net/` |

![Kudu yapılandırın](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-kudu.png)


### <a name="a-namedeploymentdeployment-options"></a><a name="deployment">Dağıtım seçenekleri

| | |
|-|-|
| ![Hello Azure portal'ın işlevi uygulama dağıtım seçenekleri](./media/functions-how-to-use-azure-function-app-settings/function-app-deployment-source.png) | İşlevler işlevi kodunuzu yerel makinenizde geliştirmenize olanak sağlar. Ardından, yerel bir işlev uygulaması proje tooAzure karşıya yükleyebilirsiniz. Ayrıca tootraditional FTP karşıya yükleme, işlevler sağlar, GitHub, VSTS, Dropbox, Bitbucket ve diğerleri gibi popüler sürekli tümleştirme çözümleri kullanarak işlevi uygulamanızı dağıtma. Daha fazla bilgi için bkz: [Azure işlevleri için sürekli dağıtım](functions-continuous-deployment.md). FTP veya yerel Git kullanarak el ile tooupload ayrıca gerekir [dağıtım kimlik bilgilerinizi yapılandırma](functions-continuous-deployment.md#credentials). |


### <a name="cors"></a>CORS

| | |
|-|-|
| ![Hello Azure portal CORS uygulamada işlevi](./media/functions-how-to-use-azure-function-app-settings/function-app-cors.png) | tooprevent kötü amaçlı kod yürütme hizmetlerinizde uygulama hizmeti blokları, dış kaynaklardan tooyour işlev uygulamalarının çağırır. Çıkış noktaları arası kaynak paylaşımı (CORS) toolet "işlevlerinizi Uzak istekleri kabul edebilir çıkış izin verilen bir beyaz liste", tanımladığınız işlevlerini destekler.  |

![İşlev uygulamanın yapılandırma CORS](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-cors.png)

### <a name="auth"></a>Kimlik doğrulaması

| | |
|-|-|
| ![Hello Azure portal işlevi uygulama kimlik doğrulaması](./media/functions-how-to-use-azure-function-app-settings/function-app-authentication.png) | İşlevler bir HTTP tetikleyicisi kullandığınızda çağrıları gerektirebilir toofirst kimlik doğrulaması. Uygulama hizmeti, Azure Active Directory kimlik doğrulaması ve oturum açın. Facebook, Microsoft ve Twitter gibi sosyal sağlayıcılardan destekler. Özel kimlik doğrulama sağlayıcılarını yapılandırma hakkında daha fazla bilgi için bkz: [Azure App Service kimlik doğrulamasına genel bakış](../app-service/app-service-authentication-overview.md). |

![Bir işlev uygulaması için kimlik doğrulamasını yapılandırma](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-authentication.png)


### <a name="swagger"></a>API tanımı

| | |
|-|-|
| ![İşlevi uygulama API'si swagger tanımında hello Azure portalı](./media/functions-how-to-use-azure-function-app-settings/function-app-api-definition.png) | İşlevlerini destekleyen Swagger tooallow istemcileri toomore kolayca kullanmalarını HTTP tetiklemeli işlevleri. Swagger ile API tanımları oluşturma hakkında daha fazla bilgi için [API Apps, ASP.NET ve Swagger Azure ile çalışmaya başlama](../app-service-api/app-service-api-dotnet-get-started.md). İşlevler proxy'leri toodefine tek bir API yüzeyi birden çok işlevleri için de kullanabilirsiniz. Daha fazla bilgi için bkz: [Azure işlevleri proxy'leri çalışma](functions-proxies.md). |

![İşlev uygulamanın API yapılandırın](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-apidef.png)



## <a name="next-steps"></a>Sonraki adımlar

+ [Azure App Service ayarlarını yapılandırma](../app-service-web/web-sites-configure.md)
+ [Azure İşlevleri için sürekli dağıtım](functions-continuous-deployment.md)



