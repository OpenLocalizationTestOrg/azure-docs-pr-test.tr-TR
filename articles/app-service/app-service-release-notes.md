---
title: "aaaAzure SDK'sı 2.5.1 .NET için sürüm notları"
description: "2.5.1 .NET için Azure SDK sürüm notları"
services: app-service
documentationcenter: .net,nodejs,java
author: Juliako
manager: erikre
editor: 
ms.assetid: 8d3d815f-bb58-447e-8ff0-f9b9603c7b00
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/10/2016
ms.author: juliako
ms.openlocfilehash: 5ee7688617c966baa409045881c172bbbc55ff63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-251-release-notes"></a>2.5.1 .NET için Azure SDK sürüm notları
.NET 2.5.1 yayın için bu belgenin hello sürüm notları hello Azure SDK'sı içerir. 

## <a name="azure-sdk-for-net-251-release-notes"></a>2.5.1 .NET için Azure SDK sürüm notları
Yeni özellikler ve güncelleştirmeler hello 2.5.1 .NET için Azure SDK'Hello aşağıda verilmiştir.

* Çok ilgili yeni features\scenarios**Web Tools Extensions**. 
  
  * Azure Web sitelerini yeniden adlandırılmış tooAzure uygulama hizmeti oluştu. Daha fazla bilgi için [Azure App Service ve mevcut Azure hizmetlerine](../app-service-web/app-service-changes-existing-services.md).
  * Azure API uygulamaları (Önizleme) desteği eklendi, böylece müşteriler API uygulamaları olarak ASP.NET projeleri yayımlamak ve hello Ekle kullanın > Azure API uygulama istemcisi hareketi kodda hello hello yapısına göre C# projeleri toogenerate dağıtılan API uygulaması. 
  * Kaynak Grup tabanlı Azure API Apps, Mobile Apps ve Web uygulamaları gruplandırma için destek içerir hello Azure uygulama hizmeti düğümünde yerine Hello Web siteleri Sunucu Gezgininde kullanım dışıdır.
  * Böylece müşteriler yeni Mobile Apps projeleri oluşturma, Mobile Apps denetleyicileri ekleme, hello projeleri yayımlamak ve uygulamaları uzaktan hata ayıklama azure Mobile Apps (Önizleme) desteği eklendi.
  * Ekle > Azure API uygulama istemcisi hareketi şimdi yerel Swagger JSON dosyalarını destekler, Web API geliştiricilere kullanabilmeniz için Swashbuckle toogenerate gibi üçüncü taraf NuGets Swagger veya el ile yazar. Bu şekilde, istemci geliştiriciler hello kod oluşturma özellikleri tooconsume herhangi bir Swagger uç nokta C# projelerinde kullanabilirsiniz. 
  * Web uygulaması ve API uygulaması yayımlama iletişim kutuları Gelişmiş toosupport hello Azure Portal gruplandırma kaynak kavramını ve seçim/Azure kaynak gruplarını ve App Service planları oluşturulmasını hello yeni Web uygulaması ve API uygulaması sağlama iletişim kutusunda gösterilir. 
  * Azure API uygulaması Sunucu Gezgini düğümleri bağlantılar toohello günlük akış ve uzaktan hata ayıklama gibi diğer özelliklerin yanı sıra hello Azure Portal, API uygulamaları derin bağlantı sağlar.
    
    Bilinen sorunlar ve geçerli sınırlamalar Azure SDK .NET 2.5.1 içinde [bu](app-service-release-notes.md#known_issues_2_5_1) bölümüne bakın.
* Çok ilgili yeni features\scenarios**Hdınsight Araçları** Visual Studio'da bu sürümde etkinleştirilir. 
  
  * Yerel doğrulama hive komut dosyaları. Betiğinizde herhangi bir hata varsa hello araç toosee hello doğrulama komut düğmesini tıklatın. 
  * Hive işleri hata ayıklama geliştirildi. Hive işleri Yarn günlüklerini Visual Studio'da erişerek şimdi ayıklayabilirsiniz. Uygulamanızın performans sorunları varsa, YARN günlüklerini araştırma yararlı bilgiler sağlayan...
  * (Genel Önizleme) Anahtar sözcüğü otomatik tamamlama ve IntelliSense için Hive'ı destekler. Visual Studio için Hdınsight araçları Hive komut dosyaları yazmak toohelp anahtar sözcüğü otomatik tamamlama ve Hive için IntelliSense desteği eklendi.
  * Storm desteği. Şimdi, Visual Studio toodevelop Storm topolojileri/Spout'lar/Cıvatalar C# için Hdınsight araçları da kullanabilirsiniz. Ardından, hello topoloji tooa Storm kümesi geliştirilen ve hello topoloji/Cıvata/spout durumunu görmek gönderebilirsiniz. Müşteri, Storm topolojileri/Cıvatalar/Spout'lar tootroubleshoot kaydeder ve sistem günlüklerini kullanabilirsiniz. Ayrıca, Hdınsight üzerinde Storm varolan JAVA varlıkları de kullanabilirsiniz.
    
    Daha fazla bilgi için bkz: [Visual Studio için Hdınsight Hadoop araçlarını kullanmaya başlamanıza](../hdinsight/hdinsight-hadoop-visual-studio-tools-get-started.md).

## <a id="known_issues_2_5_1"></a>Azure SDK'sı 2.5.1 .NET için bilinen sorunlar ve sınırlamalar
* Azure API uygulamaları, mobil uygulamalar için dağıtım hedefi olarak görülebilir. Web uygulamaları hello yalnızca hedef mobil uygulamalar için kadar sonraki bir sürüm olmalıdır. 
* Azure API uygulaması başarılı ancak zaman zaman başarısız tooupdate hello ilerleme hello Azure App Service etkinliği penceresindeki neden olabilir. Geçici çözüm toocheck durumunu hello yeni Azure API uygulaması hello Azure Portal ' dir. 
* Dosya > Yeni Proje > API uygulaması > F5 deneyimi hiçbir default/index.html olduğundan HTTP hatayla sonuçlanır. Geçici çözüm toomanually Gözat toohello/api/değerleri URL'dir. 
* Zaman zaman, Sunucu Gezgini simgeler düzleştirilmiş görünür. VS yeniden başlatılması bu sorunu çözer. 
* Web uygulaması veya API uygulaması (aşıldı kota hataları veya yinelenen Azure API uygulama ağ geçidi adı gibi) sağlama işlemi sırasında bir özel durum, hello hataları ham JSON metinleri gösterir. 
* Proje oluşturma sırasında Application Insights işaretlendiğinde aralıklı proje oluşturma sorunları.
* Bazen, oluşturulan hello Azure API uygulama istemcisi kodu ad alanları eksik, el ile dahil toobe ihtiyaç duydukları (veya Visual Studio yardımlar aracılığıyla otomatik olarak içeri aktarılan) kod toocompile için. 
* Mobil uygulama projeleri yayımlanan tooweb uygulamaları olmalı, ancak mobil uygulama projeleri bir veritabanı gerektirir beri hello Azure Portal'ın bir mobil uygulama olarak oluşturulmuş bir site seçmeniz gerekir. 
* Merhaba terimini "mobil uygulamalar" yerine "mobil hizmeti" Merhaba başlangıç sayfasına Mobile Apps kullanır 
* Mobil uygulama projesi oluşturmayı tooa minute toocreate sürebilir. 
* API uygulaması sırasında bir hata (bazı durumlarda) sağlama hello izinleri düzgün API uygulaması düzgün şekilde sağlandığını ve kullanıma hazırdır hello sırasında ayarlanamadı, Azure API hello yansıtma öğesinden gelir. İzinlerini hello Azure Portal'ı kullanarak el ile ayarlayabilirsiniz.
* Application Insights API'si uygulama şablonları ve mobil uygulama şablonları desteklenmiyor.
* API uygulaması projeleri, bulut hizmeti projeleri ile birlikte kullanılamaz.
* API uygulaması proje şablonları yalnızca C# dilinde kullanılabilir.
* API uygulaması tüketiminin hello "Azure API uygulama istemcisi Ekle" bağlam menüsü ile yalnızca C# ' ta desteklenir.

