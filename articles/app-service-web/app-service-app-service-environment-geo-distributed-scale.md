---
title: "Uygulama hizmeti ortamları dağıtılmış ölçekli aaaGeo"
description: "Nasıl toohorizontally ölçeklendirme Traffic Manager ve App Service ortamları coğrafi dağıtım kullanarak uygulamaları hakkında bilgi edinin."
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: c1b05ca8-3703-4d87-a9ae-819d741787fb
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/07/2016
ms.author: stefsch
ms.openlocfilehash: 9b441f637d8b7f679b3d83240baf99b8ee57e8f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="geo-distributed-scale-with-app-service-environments"></a>App Service Ortamları ile Coğrafi Olarak Dağıtılmış Ölçek
## <a name="overview"></a>Genel Bakış
Çok büyük ölçekli gerektiren uygulama senaryoları hello işlem kaynak kapasite kullanılabilir tooa tek dağıtım, bir uygulamanın aşabilir.  Uygulamaları oylama, spor olaylar ve televised eğlence olaylar tüm son derece yüksek ölçekli gerektiren senaryolara verilen örneklerdir. Yüksek ölçekli gereksinimleri yatay uygulamalarını, tek bir bölge içinde ve aynı zamanda bölgelere, toohandle aşırı yük gereksinimlerine yapılan birden çok uygulama dağıtımı ile ölçeklendirme tarafından karşılanabilir.

Uygulama hizmeti ortamları yatay ölçek genişletme için ideal bir platform ' dir.  Bir uygulama hizmeti ortamı yapılandırma seçildiğinde bilinen istek hızı destekleyen, geliştiricilerin "Tanımlama Bilgisi kesici" şekilde tooattain istenen yoğun yük kapasitesi ek uygulama hizmeti ortamlarında dağıtabilirsiniz.

Örneğin bir uygulama hizmeti ortamı yapılandırması üzerinde çalışan bir uygulama sınanan toohandle 20 K istekleri / saniye (RPS) bırakıldı varsayalım.  Merhaba istenen yoğun yüklerseniz 100 K RPS kapasitesi ise, sonra beş (5) App Service ortamları oluşturulabilir ve yapılandırılmış tooensure Merhaba uygulaması hello en fazla tahmini yükleme işleyebilir.

Müşteriler genellikle bir özel (ya da gösterim) etki alanı, geliştiricilerin gerek kullanarak uygulamalara erişim bu yana bir şekilde toodistribute uygulaması tüm hello uygulama hizmeti ortamı örnekleri arasında ister.  Bu harika bir şekilde tooaccomplish tooresolve hello özel etki alanı kullanarak bir [Azure Traffic Manager profilini][AzureTrafficManagerProfile].  tek tek uygulama hizmeti ortamları hello Hello trafik Yöneticisi profili tüm yapılandırılmış toopoint olabilir.  Trafik Yöneticisi tüm hello yük dengeleme ayarlarını hello trafik Yöneticisi profili, uygulama hizmeti ortamları dayalı hello müşteriler dağıtma otomatik olarak işler.  Bu yaklaşım mı hello App Service ortamları tümünün tek bir Azure bölgesinde dağıtılan veya birçok Azure bölgesinde dünya çapında dağıtılan bağımsız olarak çalışır.

Ayrıca, müşteriler uygulamaları üzerinden hello gösterim etki alanına erişim bu yana müşteriler bir uygulamayı çalıştıran uygulama hizmeti ortamları hello sayısı farkında değildir.  Sonuç olarak geliştiricilerin hızla ve kolayca, ekleyip kaldırabilirsiniz, App Service ortamları gözlemlenen trafiği yüküne göre.

Merhaba kavramsal diyagram aşağıdaki yatay çıkışı tek bir bölge içinde üç uygulama hizmeti ortamları boyunca ölçeklendirilmiş bir uygulamayı gösterir.

![Kavramsal mimarisi][ConceptualArchitecture] 

Bu konuda Hello kalanı hello örnek uygulaması kullanarak birden fazla App Service ortamları için Dağıtılmış bir topolojiyi ayarlama ile ilgili hello adım adım anlatılmaktadır.

## <a name="planning-hello-topology"></a>Merhaba topolojisini planlama
Dağıtılmış uygulama ayak izini çıkışı yapılandırmadan önce toohave vaktinden birkaç parça bilgiler sağlar.

* **Merhaba uygulaması için özel etki alanı:** müşteriler tooaccess hello uygulama kullanır hello özel etki alanı adı nedir?  Merhaba örnek uygulama hello özel etki alanı adıdır *www.scalableasedemo.com*
* **Trafik yöneticisi etki alanı:** toobe oluştururken, seçilen bir etki alanı adı gerekli bir [Azure Traffic Manager profilini][AzureTrafficManagerProfile].  Bu ada hello birleştirilecek *trafficmanager.net* tooregister trafik Yöneticisi tarafından yönetilen bir etki alanı girişi soneki.  Merhaba adı seçilen Hello örnek uygulama için olduğunu *ana demo ölçeklenebilir*.  Sonuç olarak, trafik Yöneticisi tarafından yönetilen hello tam etki alanı adıdır *ana demo.trafficmanager.net ölçeklenebilir*.
* **Merhaba uygulama ayak izini ölçeklendirmeye yönelik stratejisi:** hello uygulama kaplama alanı için tek bir bölge içinde birden fazla App Service ortamları arasında dağıtılmış?  Birden çok bölgeye?  Bir karışımını-ve-eşleşme her iki yaklaşımın?  Merhaba karar bir uygulamanın arka uç altyapısı destekleme iyi hello rest ölçeklendirebilirsiniz nasıl burada müşteri trafik, de kaynaklanan, beklentileri üzerine.  Örneğin, durum bilgisi olmayan bir % 100 uygulaması ile bir uygulama yüksek düzeyde birçok Azure bölgesinde dağıtılan uygulama hizmeti ortamları çarpılmasıyla Azure bölgesi başına birden fazla App Service ortamları birleşimini kullanarak genişletilebilir.  15 + ortak Azure bölgeleri kullanılabilir toochoose ile müşterilerin gerçekten dünya çapında hiper ölçekli uygulama ayak izini oluşturabilirsiniz.  Bu makale için kullanılan hello örnek uygulama için üç uygulama hizmeti ortamları bir tek Azure bölgesinde (Orta Güney ABD) oluşturuldu.
* **Uygulama hizmeti ortamları hello için adlandırma:** her uygulama hizmeti ortamı benzersiz bir ad gerektirir.  İsteğe bağlı olarak bir veya iki uygulama hizmeti ortamları yararlı toohave bir adlandırma kuralı olan toohelp her uygulama hizmeti ortamı tanımlayın.  Merhaba örnek uygulama için basit bir adlandırma kuralı kullanıldı.  Merhaba hello üç uygulama hizmeti ortamları adlarıdır *fe1ase*, *fe2ase*, ve *fe3ase*.
* **Merhaba uygulamaları için adlandırma:** hello uygulama birden çok örneğini dağıtılacak olduğundan, dağıtılan hello uygulama her örneği için bir ad gereklidir.  Bir bilinen az, ancak çok kullanışlı uygulama hizmeti ortamları aynı uygulama adı birden fazla App Service ortamları kullanılabilir o hello özelliğidir.  Her uygulama hizmeti ortamı benzersiz etki alanı soneki olduğundan, geliştiricilerin her ortamda toore kullanımlı hello tam aynı uygulama adı seçebilirsiniz.  Örneğin, bir geliştirici uygulamalar gibi adlı sahip olabilir: *myapp.foo1.p.azurewebsites.net*, *myapp.foo2.p.azurewebsites.net*, *myapp.foo3.p.azurewebsites.net*, vb..  Merhaba örnek uygulama için yine de her bir uygulama örneği de benzersiz bir ada sahip.  Merhaba kullanılan uygulama örnek adları olan *webfrontend1*, *webfrontend2*, ve *webfrontend3*.

## <a name="setting-up-hello-traffic-manager-profile"></a>Merhaba trafik Yöneticisi profili ayarlama
Bir uygulama birden çok örneği üzerinde birden fazla App Service ortamları dağıtıldığında hello tek tek uygulama örnekleri ile trafik Yöneticisi kaydedilebilir.  Merhaba örnek uygulama için bir trafik Yöneticisi profili için gerekli *ana demo.trafficmanager.net ölçeklenebilir* müşteriler aşağıdaki Merhaba, dağıtılan tooany app örnekleri yönlendirebilirsiniz:

* **webfrontend1.fe1ase.p.azurewebsites.NET:** dağıtılan hello örnek uygulaması örneğini hello ilk uygulama hizmeti ortamı.
* **webfrontend2.fe2ase.p.azurewebsites.NET:** dağıtılan hello örnek uygulaması örneğini hello ikinci uygulama hizmeti ortamı.
* **webfrontend3.fe3ase.p.azurewebsites.NET:** dağıtılan hello örnek uygulaması örneğini hello üçüncü uygulama hizmeti ortamı.

birden fazla Azure Uygulama Hizmeti uç noktası, hello tüm çalışan en kolay yolu tooregister hello **aynı** Azure bölgesi olan hello Powershell ile [Azure Kaynak Yöneticisi trafik Yöneticisi Destek] [ ARMTrafficManager].  

Merhaba ilk adımı toocreate bir Azure Traffic Manager profilini oluşturur.  Aşağıdaki Hello kodu hello profil hello örnek uygulama için nasıl oluşturulduğuna gösterir:

    $profile = New-AzureTrafficManagerProfile –Name scalableasedemo -ResourceGroupName yourRGNameHere -TrafficRoutingMethod Weighted -RelativeDnsName scalable-ase-demo -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"

Nasıl hello fark *RelativeDnsName* parametresi çok ayarlandığı*ana demo ölçeklenebilir*.  Bu olduğunu nasıl hello etki alanı adı *ana demo.trafficmanager.net ölçeklenebilir* oluşturulur ve bir trafik Yöneticisi profili ile ilişkilendirilmiş.

Merhaba *TrafficRoutingMethod* parametre tanımlar hello Yük Dengeleme İlkesi trafik Yöneticisi nasıl toospread müşteri yükünü tüm hello kullanılabilir uç noktaları arasında toodetermine kullanır.  Bu örnek hello içinde *Weighted* yöntemi seçildi.  Bu tüm kayıtlı hello uygulama uç hello göreli ağırlığı her bitiş noktasıyla ilişkili temel yayılmasını müşteri isteklerine neden olur. 

Oluşturulan hello profiliyle her uygulama örneği toohello profili yerel bir Azure uç noktası olarak eklenir.  Aşağıdaki Hello kodu bir başvuru tooeach ön uç web uygulaması getirir ve hello yapmamanız trafik Yöneticisi uç noktası olarak her uygulama ekler *uç noktası Targetresourceıd* parametresi.

    $webapp1 = Get-AzureRMWebApp -Name webfrontend1
    Add-AzureTrafficManagerEndpointConfig –EndpointName webfrontend1 –TrafficManagerProfile $profile –Type AzureEndpoints -TargetResourceId $webapp1.Id –EndpointStatus Enabled –Weight 10

    $webapp2 = Get-AzureRMWebApp -Name webfrontend2
    Add-AzureTrafficManagerEndpointConfig –EndpointName webfrontend2 –TrafficManagerProfile $profile –Type AzureEndpoints -TargetResourceId $webapp2.Id –EndpointStatus Enabled –Weight 10

    $webapp3 = Get-AzureRMWebApp -Name webfrontend3
    Add-AzureTrafficManagerEndpointConfig –EndpointName webfrontend3 –TrafficManagerProfile $profile –Type AzureEndpoints -TargetResourceId $webapp3.Id –EndpointStatus Enabled –Weight 10

    Set-AzureTrafficManagerProfile –TrafficManagerProfile $profile

Nasıl bir çağrı çok fark*Ekle AzureTrafficManagerEndpointConfig* her tek tek uygulama örneği.  Merhaba *uç noktası Targetresourceıd* her Powershell komutunu parametresinde bir hello üç dağıtılan uygulama örneklerinin başvuruyor.  Merhaba trafik Yöneticisi profili yük hello profilinde kayıtlı tüm üç uç noktaları arasında yayılır.

Tüm üç uç noktaları kullanma hello hello hello için aynı değeri (10) *ağırlık* parametresi.  Bu trafik Yöneticisi yayılmasından müşteri isteklerine tüm üç uygulama örneklerde görece eşit olur. 

## <a name="pointing-hello-apps-custom-domain-at-hello-traffic-manager-domain"></a>Merhaba Traffic Manager etki alanına işaret hello uygulamanın özel etki alanı
Merhaba son adım gerekli toopoint hello özel etki hello uygulama hello trafik yöneticisi etki alanıdır.  Merhaba örnek uygulama için bu işaret eden anlamına gelir *www.scalableasedemo.com* adresindeki *ana demo.trafficmanager.net ölçeklenebilir*.  Bu adım hello özel etki alanı yöneten hello etki alanı kayıt şirketinizle tamamlandı toobe gerekir.  

Kayıt şirketinizin etki alanı Yönetim Araçları'nı kullanarak bir CNAME kayıtları gereksinimlerini toobe hello Traffic Manager etki alanına hangi noktaları hello özel etki alanı oluşturuldu.  Merhaba resimde bu CNAME yapılandırma benzer bir örnek gösterilmektedir:

![Özel etki alanı için CNAME][CNAMEforCustomDomain] 

Bu konuda ele değil de, her tek tek uygulama örneği ile de kayıtlı toohave hello özel etki alanı gerektiğini unutmayın.  Aksi takdirde Merhaba uygulaması hello uygulamayla kayıtlı hello özel etki alanı yok ve bir istek tooan uygulama örneği kolaylaştırır, hello isteği başarısız olur.  

Bu örnek hello özel etki alanı içinde *www.scalableasedemo.com*, ve her uygulama örneğinin ilişkili hello özel etki alanı vardır.

![Özel Etki Alanı][CustomDomain] 

Azure uygulama hizmeti uygulamaları ile özel bir etki alanı kaydı bir özeti için aşağıdaki makaleye bakın hello bkz [özel etki alanlarını kaydetme][RegisterCustomDomain].

## <a name="trying-out-hello-distributed-topology"></a>Dağıtılmış topoloji Hello çalışıyor
Merhaba son hello trafik Yöneticisi ve DNS yapılandırması yönelik isteklere sonucudur *www.scalableasedemo.com* dizisi aşağıdaki hello akar:

1. DNS araması yapmak bir tarayıcı veya aygıt *www.scalableasedemo.com*
2. Merhaba hello etki alanı kayıt CNAME girdisi hello DNS Arama yeniden yönlendirilen toobe tooAzure trafik Yöneticisi neden olur.
3. DNS araması yapılan *ana demo.trafficmanager.net ölçeklenebilir* hello Azure trafik Yöneticisi DNS sunucularından birinde karşı.
4. Merhaba Yük Dengeleme İlkesi tabanlı (Merhaba *TrafficRoutingMethod* hello trafik Yöneticisi profili oluştururken daha önce kullanılan parametresi), hello biri uç noktaları yapılandırılmış seçip dönüş trafik Yöneticisi Merhaba, FQDN'si uç nokta toohello tarayıcı veya aygıt.
5. Bir uygulama hizmeti ortamı üzerinde çalışan bir uygulama örneğine hello URL'sini Hello hello uç noktası FQDN'si olduğuna göre hello tarayıcı veya aygıt bir Microsoft Azure DNS sunucusu tooresolve hello FQDN tooan IP adresi sorar. 
6. Merhaba tarayıcı veya aygıt hello HTTP/S isteği toohello IP adresine gönderir.  
7. Merhaba isteği hello App Service ortamları biri üzerinde çalışan hello app örnekleri birinde ulaşırsınız.

Merhaba konsol resimde gösterilmektedir hello üç örnek uygulama hizmeti ortamları biri üzerinde çalışan hello örnek uygulamanın özel etki alanı başarıyla çözümleme tooan uygulama örneği için DNS araması (Bu durumda hello hello üç uygulama hizmeti ortamları saniye):

![DNS araması][DNSLookup] 

## <a name="additional-links-and-information"></a>Ek bağlantıları ve bilgileri
Tüm makaleler ve nasıl-için uygulama hizmeti ortamları hello kullanılabilir için kullanıcının [uygulama hizmeti ortamları için Benioku](../app-service/app-service-app-service-environments-readme.md).

Merhaba Powershell belgelerine [Azure Kaynak Yöneticisi trafik Yöneticisi Destek][ARMTrafficManager].  

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[AzureTrafficManagerProfile]: ../traffic-manager/traffic-manager-manage-profiles.md
[ARMTrafficManager]: ../traffic-manager/traffic-manager-powershell-arm.md
[RegisterCustomDomain]: app-service-web-tutorial-custom-domain.md


<!-- IMAGES -->
[ConceptualArchitecture]: ./media/app-service-app-service-environment-geo-distributed-scale/ConceptualArchitecture-1.png
[CNAMEforCustomDomain]:  ./media/app-service-app-service-environment-geo-distributed-scale/CNAMECustomDomain-1.png
[DNSLookup]:  ./media/app-service-app-service-environment-geo-distributed-scale/DNSLookup-1.png
[CustomDomain]:  ./media/app-service-app-service-environment-geo-distributed-scale/CustomDomain-1.png 
