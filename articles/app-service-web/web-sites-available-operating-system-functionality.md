---
title: "Azure App Service'te aaaOperating sistem işlevi"
description: "Merhaba OS işlevselliği kullanılabilir tooweb uygulamalar, mobil uygulaması arka uçlarını ve Azure App Service'te API uygulamaları hakkında bilgi edinin"
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: 39d5514f-0139-453a-b52e-4a1c06d8d914
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/01/2016
ms.author: cephalin
ms.openlocfilehash: 695188c48102b10ece326fba8d50a5f55b03b003
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="operating-system-functionality-on-azure-app-service"></a>Azure App Service'te işletim sistemi işlevi
Bu makalede çalışan kullanılabilir tooall uygulamaları hello ortak temel işletim sistemi işlevleri [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714). Bu işlevsellik, dosya, ağ ve kayıt defteri erişimi ve tanılama günlüklerini ve olayları içerir. 

<a id="tiers"></a>

## <a name="app-service-plan-tiers"></a>Uygulama hizmeti planı katmanları
Uygulama hizmeti çok kiracılı bir barındırma ortamında müşteri uygulamalar çalışır. Hello dağıtılan uygulamalar **serbest** ve **paylaşılan** katmanları hello dağıtılan uygulamalar sırasında paylaşılan sanal makinelerde çalışan işlemlerini çalıştırmak **standart** ve  **Premium** katmanları özellikle tek bir müşteri ile ilişkili hello uygulamalar için ayrılmış sanal makineleri üzerinde çalışır.

Uygulama hizmeti farklı katmanlar arasında sorunsuz ölçeklendirme bir deneyim desteklediğinden, hello güvenlik yapılandırması aynı uygulama hizmeti uygulamaları kalır hello için zorunlu. Bu uygulamalar aniden farklı şekilde, bir katmanlı tooanother uygulama hizmeti planı geçiş yaparken beklenmeyen şekilde başarısız davrandığını yok sağlar.

<a id="developmentframeworks"></a>

## <a name="development-frameworks"></a>Geliştirme çerçeveleri
Uygulama hizmeti fiyatlandırma katmanları denetim hello işlem kaynakları (CPU, disk depolama, bellek ve ağ çıkış) miktarı kullanılabilir tooapps. Ancak, aynı bakılmaksızın katmanları ölçeklendirme hello hello framework işlevselliği kullanılabilir tooapps hello derecesini kalır.

App Service ASP.NET, klasik ASP, node.js dahil olmak üzere geliştirme çerçeveleri, PHP ve Python tümü uzantıları IIS içinde farklı çalıştır - çeşitli destekler. Sipariş toosimplify içinde ve güvenlik yapılandırması normalleştirin, App Service uygulamalarının genellikle hello çeşitli geliştirme çerçeveleri kendi varsayılan ayarlarla çalıştırılır. Bir yaklaşım tooconfiguring uygulamaları toocustomize hello API yüzey alanını ve her bireysel geliştirme çerçevesi için işlevselliği silinmiş. Uygulama hizmeti bir uygulamanın geliştirme framework bakılmaksızın işletim sistemi işlevselliğini ortak bir taban çizgisi sağlayarak daha genel bir yaklaşım yerine alır.

Merhaba aşağıdaki bölümlerde hello genel işletim sistemi işlevselliği kullanılabilir tooApp hizmet uygulamaları türlerini özetler.

<a id="FileAccess"></a>

## <a name="file-access"></a>Dosya erişimi
Yerel sürücüler ve ağ sürücülerini içeren uygulama hizmeti içinde çeşitli sürücüsü yok.

<a id="LocalDrives"></a>

### <a name="local-drives"></a>Yerel sürücüler
Özünde, uygulama hizmeti hello Azure PaaS (hizmet olarak platform) altyapısı üzerinde çalışan bir hizmettir. Merhaba yerel sürücülerinin bir sonucu "tooa sanal makineye bağlı şekilde" Merhaba aynı sürücü türleri kullanılabilir tooany çalışan rolü Azure üzerinde çalışıyor. Bu işletim sistemi sürücüsü (Merhaba D:\ sürücüsüne), özel olarak App Service (ve erişilemez toocustomers) kullanılan Azure paket cspkg dosyalarını içeren bir uygulama sürücü ve büyüklüğü hello büyüklüğüne bağlı olarak değişir "kullanıcı" sürücüsü (Merhaba C:\ sürücüsü) içerir Merhaba VM.

<a id="NetworkDrives"></a>

### <a name="network-drives-aka-unc-shares"></a>Ağ sürücüleri (diğer adıyla UNC paylaşımları)
Uygulama dağıtımını ve bakımını basitleştirir uygulama hizmeti benzersiz yönleri hello tüm kullanıcı içeriğin UNC paylaşımlarına kümesine göre depolandığı biridir. Bu model çok iyi toohello yaygın olarak kullanılan deseni birden çok Yük Dengeleme sunucuları sahip ortamlarda şirket içi web sitesi barındırma tarafından kullanılan içerik depolama eşler. 

App Service içinde vardır her veri merkezinde oluşturulan UNC paylaşımlarına sayısı. Her veri merkezi tüm müşteriler için hello kullanıcı içeriği yüzdesi UNC paylaşımı tooeach tahsis edilir. Ayrıca, tüm hello dosya içeriği tek bir müşterinin aboneliğini için her zaman yerleştirilir aynı UNC paylaşımı hello üzerinde. 

Toohow bulut Hizmetleri son çalışma unutmayın, hello belirli bir sanal makine bir UNC paylaşımı barındırmak için sorumlu zaman içinde değişir. Yukarı ve aşağı hello normal seyri bulut işlemleri sırasında duruma gibi UNC paylaşımlarına farklı sanal makineler tarafından bağlanacaktır sağlanır. Bu nedenle, uygulamaları hiçbir zaman bir UNC dosya yolu hello makine bilgileri zamanla kararlı kalacak sabit kodlanmış varsayımlar olmanız gerekir. Bunun yerine, uygun hello kullanmalısınız *sahte* mutlak bir yol **D:\home\site** , uygulama hizmeti sağlar. Bu sahte mutlak yolu tooone's kendi uygulama başvuran taşınabilir, uygulama ve kullanıcı belirsiz bir yöntem sağlar. Kullanarak **D:\home\site**, bir aktarma paylaşılan dosyaları uygulama tooapp her aktarımı için yeni bir mutlak yol tooconfigure gerek kalmadan.

<a id="TypesOfFileAccess"></a>

### <a name="types-of-file-access-granted-tooan-app"></a>Dosya erişim türleri tooan uygulama verildi
Her müşterinin aboneliğini, bir veri merkezi içinde belirli bir UNC paylaşımında ayrılmış dizin yapısının. Tüm tooa tek müşteri aboneliğe ait hello dizinleri hello üzerinde oluşturulacak şekilde aynı UNC paylaşımı, bir müşteri belirli veri merkezi içinde oluşturulan birden fazla uygulama sahip. Merhaba paylaşımı içerik, hata ve tanılama günlüklerini ve kaynak denetimi tarafından oluşturulan hello uygulaması önceki sürümleri için olanlar gibi dizinleri içerebilir. Beklendiği gibi müşteri'nin uygulama dizinleri okuma ve yazma erişimi hello uygulamanın uygulama kodu tarafından çalışma zamanında için kullanılabilir.

Bir uygulama çalıştıran toohello sanal makineyi yerel sürücüler üzerinde Hello bağlı, uygulama hizmeti bir öbek hello C:\ sürücüsü uygulamaya özgü geçici yerel depolama birimi için alan ayırır. Bir uygulama tooits geçici kendi tam okuma/yazma erişimi olmasına karşın yerel depolama, depolama birimini doğrudan hello uygulama kodu tarafından kullanılan hedeflenen toobe gerçekten değil. Bunun yerine, hello hedefi tooprovide geçici dosya depolaması için IIS ve web uygulama çerçeveleri ' dir. Uygulama hizmeti de aşırı miktarda yerel dosya depolama alanı kullanan geçici yerel depolama kullanılabilir tooeach uygulama tooprevent tek tek uygulamalarının hello miktarını sınırlar.

Merhaba dizin ASP.NET dosyaları için nasıl uygulama hizmeti geçici yerel depolama alanı kullanır, iki örnek verilmiştir ve IIS için başlangıç dizini sıkıştırılmış dosyaları dışarıda bırak. Merhaba ASP.NET derleme sistem hello "ASP.NET dosyaları" dizininin geçici derleme önbellek konumu olarak kullanır. IIS hello "IIS geçici sıkıştırılmış dosyaların" dizin sıkıştırılmış toostore yanıt çıktısı kullanır. Bu tür dosyası kullanımı (yanı sıra diğerleri) hem de uygulama hizmeti tooper uygulama geçici yerel depolama eşleştirilir. Bu yeniden eşleme işlevselliği beklendiği gibi devam etmesini sağlar.

Her uygulama App Service'te bir rastgele benzersiz düşük ayrıcalıklı çalışan işlem kimliğini hello "daha fazla burada açıklanan uygulama havuzu kimliğini" adlı gibi çalışır: [http://www.iis.net/learn/manage/configuring-security/application-pool-identities ](http://www.iis.net/learn/manage/configuring-security/application-pool-identities). Uygulama kodu temel salt okunur erişim toohello işletim sistemi sürücüsü (Merhaba D:\ sürücüsüne) için bu kimliği kullanır. Bu uygulama kodu ortak dizin yapıları listesinde ve işletim sistemi sürücüsünde ortak dosyaları okumasına anlamına gelir. Bu toobe biraz geniş bir erişim düzeyini görünür, aynı dizinlerde hello ve dosyaları erişilebilir olmasına karşın bir Azure çalışan rolünde sağlamak zaman barındırılan hizmetin ve hello sürücü içeriğini okuma. 

<a name="multipleinstances"></a>

### <a name="file-access-across-multiple-instances"></a>Birden çok örneği arasında dosya erişimi
bir uygulamanın içeriği Hello giriş dizini içerir ve uygulama kodu tooit yazabilirsiniz. Bir uygulama birden çok örneği üzerinde çalışıyorsa, tüm örnekler hello görebilmesi için hello giriş dizini tüm örnekler arasında paylaşılan aynı dizin. Bir uygulama karşıya yüklenen dosyaların toohello giriş dizini kaydederse, bu nedenle, örneğin, bu dosyaları hemen kullanılabilir tooall örnekleridir. 

<a id="NetworkAccess"></a>

## <a name="network-access"></a>Ağ erişimi
Temel UDP protokollerini toomake giden ağ dış hizmetler kullanıma bağlantıları tooInternet erişilebilir uç noktaları ve TCP/IP'yi uygulama kodu kullanabilirsiniz. Uygulamaları Azure & #151 içinde; Örneğin, HTTPS bağlantıları tooSQL veritabanı oluşturarak bu aynı protokolleri tooconnect tooservices kullanabilirsiniz.

Ayrıca uygulamalar tooestablish bir yerel bir geri döngü bağlantısı için sınırlı bir özellik vardır ve bu yerel bir geri döngü yuvadaki dinleme bir uygulamaya sahip. Bu özellik, öncelikle işlevleri bir parçası olarak yerel bir geri döngü yuvalarda dinleme tooenable uygulamaları bulunmaktadır. Her uygulama bir "özel" geri döngü bağlantı görür unutmayın; uygulama "A", "B" uygulama tarafından oluşturulan tooa yerel bir geri döngü yuva dinleyemiyor.

Adlandırılmış Kanallar topluca bir uygulama çalıştırmasına farklı işlemler arasında işlemler arası iletişim (IPC) mekanizması olarak da desteklenir. Örneğin, hello IIS Fastcgı modülü adlandırılmış kanallar üzerinde PHP sayfaları çalıştırmak toocoordinate hello tek tek işlemleri kullanır.

<a id="Code"></a>

## <a name="code-execution-processes-and-memory"></a>Kod yürütmeyi, işlemleri ve bellek
Daha önce belirtildiği gibi uygulamalar düşük ayrıcalıklı çalışan işlemleri içinde rastgele uygulama havuzu kimliği kullanarak çalıştırın. Uygulama kodu kökenli tüm alt işlemleri CGI işlemi veya diğer uygulamalar tarafından yanı sıra hello çalışan işlemi ile ilgili erişim toohello bellek alanı yok. Ancak, bir uygulama hello bellek erişilemiyor veya verileri başka bir uygulamanın üzerinde olsa bile aynı sanal makine hello.

Uygulamalar, komut dosyaları veya desteklenen web geliştirme çerçeveleri ile yazılan sayfa çalıştırabilirsiniz. Uygulama hizmeti tüm web framework ayarları kısıtlanmış toomore modları yapılandırmaz. Örneğin, uygulama hizmeti üzerinde çalışan ASP.NET uygulamaları "tam" güvende karşılıklı tooa daha fazla kısıtlı güven modu olarak çalıştırın. Web çerçeveleri, hem klasik ASP ve ASP.NET gibi hello Windows işletim sistemindeki varsayılan kayıtlı ADO (ActiveX Data Objects) gibi işlem içi COM bileşenleri (ancak işlem COM bileşenleri dışı) çağırabilirsiniz.

Uygulamaları oluşturma ve rasgele kod çalıştırabilir. Bir komut kabuğu oluşturma veya bir PowerShell betiğini çalıştırmak gibi bir uygulama toodo işlemler için izin verilebilir. Ancak, rastgele kod ve işlemleri bir uygulama da çalıştırılabilir program kökenli ve hala kısıtlı toohello ayrıcalıkları betiklerdir olsa bile verilen toohello üst uygulama havuzu. Örneğin, yürütülebilir aynı toounbind hello IP adresini kendi NIC'i bir sanal makineden çalışır ancak bu uygulama bir giden HTTP çağrı yapan bir yürütülebilir dosya oluşturabilir Giden ağ araması yapmadan toolow ayrıcalıklı kod izin verilir, ancak tooreconfigure ağ ayarları bir sanal makine üzerinde çalışırken yönetici ayrıcalıkları gerektirir.

<a id="Diagnostics"></a>

## <a name="diagnostics-logs-and-events"></a>Tanılama günlüklerini ve olayları
Günlük bilgileri başka bir veri bazı uygulamalar tooaccess çalışır kümesidir. günlük bilgileri kullanılabilir toocode App Service içinde çalışan Hello türleri tanılama içerir ve ayrıca kolayca erişilebilir toohello uygulama bir uygulama tarafından oluşturulan bilgileri günlüğe kaydeder. 

Örneğin, etkin bir uygulama tarafından oluşturulan W3C HTTP günlüklerin kullanılabilir herhangi bir günlük dizini hello ağ üzerinde paylaşın hello uygulaması için oluşturduğunuz konumu veya W3C günlük kaydı toostorage blob depolamada müşteri kullanılabilir ayarladı. bir ağ paylaşımı ile ilişkilendirilmiş hello dosya depolama sınırları aşan hello riski olmadan toplanan günlükleri toobe büyük miktarlarda Hello ikinci seçeneği sağlar.

Benzer bir damarlı içinde .NET uygulamalarını bilgilerinden hello .NET izleme ve tanılama altyapısı, seçenekleri toowrite ile kullanarak da kaydedilebilir gerçek zamanlı Tanılama izleme bilgilerini tooeither hello uygulamanın ağ paylaşımına veya alternatif olarak blob storage'ı tooa hello konum.

Kullanılabilir tooapps olmayan günlüğe kaydetme ve izleme tanılama Windows ETW olayları ve ortak Windows olay günlüklerini (örneğin sistem, uygulama ve güvenlik olay günlüklerini) alanlarıdır. ETW İzleme bilgilerini potansiyel olarak görüntülenebilir olabileceği için makine genelinde (ile Merhaba hakkı ACL'leri), okuma ve yazma erişimi tooETW olayları engellenir. Geliştiriciler fark tooread ve yazma ETW olayları bu API çağrılarının ve ortak Windows olay günlüklerini toowork görünür, ancak uygulama hizmeti "Merhaba çağrıları faking için" toosucceed görünmesini sağlayacak şekilde. Gerçekte, hello uygulama kodu erişim toothis olay veri yok.

<a id="RegistryAccess"></a>

## <a name="registry-access"></a>Kayıt defteri erişimi
(Tümü rağmen) uygulamalara sahip salt okunur erişim toomuch hello sanal makinenin bunlar üzerinde çalıştığını hello kayıt defteri. Uygulamada, bu salt okunur erişim toohello yerel kullanıcı grubu izin kayıt defteri anahtarlarını uygulamalar tarafından erişilebilen anlamına gelir. Bir okuma veya yazma erişimi için şu anda desteklenmiyor hello kayıt defteri alanıdır hello HKEY\_geçerli\_kullanıcı yığını.

Erişim tooany kullanıcı başına kayıt defteri anahtarlarına yazma erişimi toohello kayıt defteri engellendi. Uygulamaları (yapıp bu yana) hello uygulamanın açısından yazma erişimi toohello kayıt defteri hiçbir zaman üzerine hello Azure ortamı dayanıyordu farklı sanal makineler arasında geçişi. bir uygulama tarafından bağımlı hello yalnızca kalıcı yazılabilir depolama App Service UNC paylaşımlarını hello üzerinde depolanan hello uygulama başına içerik dizin yapısıdır. 

## <a name="more-information"></a>Daha fazla bilgi

[Azure Web uygulaması sandbox](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox) -App Service'in hello yürütme ortamı hakkında en güncel bilgileri hello. Bu sayfayı hello tarafından doğrudan App Service geliştirme ekibi korunur.

> [!NOTE]
> Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz. Kredi kartı ve taahhüt gerekmez.
> 
> 


