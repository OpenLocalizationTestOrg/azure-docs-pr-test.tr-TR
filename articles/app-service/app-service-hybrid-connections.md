---
title: "aaa \"Azure uygulama hizmeti karma bağlantılar | Microsoft Docs\""
description: "Nasıl farklı ağlarda toocreate ve kullanım karma bağlantılar tooaccess kaynakları"
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: 
ms.assetid: 66774bde-13f5-45d0-9a70-4e9536a4f619
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/22/2017
ms.author: ccompy
ms.openlocfilehash: 61d58068ab0a7c803019e3f0e92bde4273d1a053
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-hybrid-connections"></a>Azure uygulama hizmeti karma bağlantılar #

## <a name="overview"></a>Genel Bakış ##

Karma bağlantılar hem Azure hizmetinde, hem de hello Azure App Service içinde bir özellik değil.  Bir hizmet olarak kullanın ve hello Azure App Service işlevden ötesinde özellikler vardır.  Karma bağlantılar ve hello Azure App Service burada başlayabileceğini dışında kullanımı hakkında daha fazla toolearn [Azure geçişi karma bağlantılar][HCService]

Hello Azure App Service içinde karma bağlantılar diğer ağlarda kullanılan tooaccess uygulama kaynakları olabilir. Uygulama tooan uygulama uç NOKTASINDAN erişim sağlar.  Uygulamanızı bir alternatif yetenek tooaccess etkinleştirmez.  Merhaba uygulama hizmeti kullanılan gibi her bir karma bağlantı tooa tek TCP ana bilgisayarı ve bağlantı noktası bileşimi hatalarla ilintilidir.  Başka bir deyişle, bu hello karma bağlantı uç herhangi bir işletim sistemi ve herhangi bir uygulama üzerinde bir TCP dinleme bağlantı noktası devreyi sağlanabilir. Karma bağlantılar, bilmiyorsanız veya hangi hello uygulama protokolü veya erişmeye çalıştığınız dikkat edin.  Ayrıca, ağ erişimi yalnızca sağlamaktır.  


## <a name="how-it-works"></a>Nasıl çalışır? ##
Merhaba karma bağlantıları özelliği iki giden çağrıları tooService veri yolu geçişi oluşur.  Burada, uygulamanızın hello app service içinde çalışan ve ardından hello karma bağlantı Manager(HCM) tooService veri yolu geçişi öğesinden bir bağlantı yoktur hello ana bilgisayardaki bir kitaplıktan bir bağlantı yok.  Merhaba HCM hello ağ barındırma içinde dağıttığınız bir geçiş hizmetidir 

Merhaba uygulamanızı TCP tünel tooa sahip iki birleştirilmiş bağlantıları hello HCM diğer tarafını ana: bağlantı noktası bileşimi hello üzerinde sabit.  Merhaba bağlantı TLS 1.2 güvenlik ve kimlik doğrulama/yetkilendirme için SAS anahtarları kullanır.    

![][1]

Uygulamanızı bir DNS isteğinde bulunduğunda bir yapılandırma karma bağlantı uç noktası ile eşleşen sonra hello giden TCP trafiğine hello karma bağlantı yönlendirilir.  

> [!NOTE]
> Bu karma bağlantınız için bir DNS adı tooalways kullanım denemelisiniz anlamına gelir.  Hello uç noktası IP adresi yerine kullanıyorsa, bazı istemci yazılımı DNS araması yapın.
>
>

Karma bağlantılar, Azure geçiş altında bir hizmet olarak sunulan ve eski BizTalk karma bağlantılar hello hello yeni karma bağlantılar iki tür vardır.  Merhaba eski BizTalk karma bağlantılar hello portalında başvurulan tooas Klasik karma bağlantılar ' dir.  Bu belgede daha sonra bunları hakkında daha fazla bilgi yoktur.

### <a name="app-service-hybrid-connection-benefits"></a>Uygulama hizmeti karma bağlantı avantajları ###

Avantajları toohello karma bağlantıları yeteneği dahil olmak üzere, birkaç vardır

- Uygulamaları güvenli bir şekilde şirket içi sistemleri ve Hizmetleri ile güvenli bir şekilde erişebilir
- Merhaba özelliği bir Internet erişilebilir uç nokta gerektirmez
- hızlı ve kolay tooset ayarlama  
- Her bir karma bağlantı bir mükemmel güvenlik durum olan tooa tek ana bilgisayar: bağlantı noktası birleşimi ile eşleşir
- Merhaba bağlantıları standart web bağlantı noktaları üzerinden giden tüm olduğu gibi normalde güvenlik duvarı delik gerektirmez
- Merhaba özelliği anlamına da ağ düzeyi olduğundan hello bitiş noktası tarafından kullanılan uygulama ve hello teknoloji tarafından kullanılan belirsiz toohello dilini değildir
- Bu olabilir tek bir uygulama birden çok ağlarda kullanılan tooprovide erişim 

### <a name="things-you-cannot-do-with-hybrid-connections"></a>Karma bağlantılar ile yapamayacağı noktalar ###

Karma bağlantılar ile yapamayacağınız birkaç şey vardır ve bunlar şunları içerir:

- bir sürücü bağlama
- UDP kullanma
- FTP Pasif modu veya genişletilmiş Pasif modu gibi dinamik bağlantı noktaları kullanan hizmetler dayalı TCP erişme
- UDP şekliyle bazen LDAP desteği gerektirir
- Active Directory desteği

## <a name="adding-and-creating-a-hybrid-connection-in-your-app"></a>Ekleme ve uygulamanızda karma bağlantı oluşturma ##

Karma bağlantılar hello uygulama portalı üzerinden veya hello karma bağlantı hizmet portalından oluşturulabilir.  Merhaba uygulama portal toocreate hello karma bağlantılar, uygulamanızı toouse istediğiniz kullanmak önerilir.  Karma bağlantı toocreate Git toohello [Azure portal] [ portal] ve uygulamanız için kullanıcı Arabirimi hello uygulamasına gidin.  Seçin **Ağ > karma bağlantı uç noktalarınızı yapılandırın**.  Buradan, uygulamanızı yapılandırılmış hello karma bağlantılar görebilirsiniz.  

![][2]

Yeni bir karma bağlantı tooadd karma Bağlantı Ekle'yi tıklatın.  Merhaba açılan UI hello karma bağlantılar'de, önceden oluşturduğunuz listeler.  bir veya daha fazla bunların tooadd tooyour uygulama, istediğiniz ve isabet hello olanları tıklatıldığında **Ekle seçili karma bağlantı**.  

![][3]

Yeni bir karma bağlantı toocreate istiyorsanız, **yeni karma bağlantı oluşturmak**.  Buradan belirtin: 

- uç nokta adı
- uç noktası ana bilgisayar adı
- uç nokta bağlantı noktası
- servicebus ad alanı toouse istiyor

![][4]

Her karma bağlantı bağlı tooa hizmet veri yolu ad alanıdır ve her hizmet veri yolu ad alanı bir Azure bölgesinde.  Tootry ve bir hizmet veri yolu ad alanında kullanım uygulamanızı aynı bölgede tooavoid kopyaladığınızda ağ gecikmesi olarak şekilde hello önemlidir.

Uygulamanızdan karma bağlantınız tooremove istiyorsanız, sağ tıklayın ve seçin **Bağlantıyı Kes**.  

Karma bağlantı tooyour web uygulaması eklendikten sonra Ayrıntılar üzerinde yalnızca tıklayarak görebilirsiniz.  

![][5]

## <a name="hybrid-connections-and-app-service-plans"></a>Karma bağlantılar ve uygulama hizmeti planları ##

Şimdi yapabileceğiniz hello yalnızca karma bağlantılar hello yeni karma bağlantılar ' dir.  Yalnızca temel, standart, Premium ve SKU'ları fiyatlandırması Isolated kullanılabilir.  Plan fiyatlandırması bağlı sınırları toohello vardır.  

| Plan fiyatlandırması | Karma bağlantılar hello planında kullanılabilir sayısı |
|----|----|
| Temel | 5 |
| Standart | 25 |
| Premium | 200 |
| Yalıtılmış | 200 |

Uygulama hizmeti planı kısıtlamaları bulunmaktadır UI hello kaç karma bağlantılar kullanıldığını gösterir App Service planı ve hangi uygulamaların bu yana.  

![][6]

Gibi hello uygulama görünümüyle ayrıntıları karma bağlantınız tıklayarak görebilirsiniz.  Merhaba uygulama Sergi sahip tüm hello bilgileri görebilir, ancak kaç hello uygulamalarında da görebilirsiniz burada gösterilen hello özelliklerinde aynı App Service planı kullandığınız Bu karma bağlantı.

![][7]

Bir uygulama hizmeti planı'nda kullanılabilir karma bağlantı uç hello sayısına bir sınır olsa da, bu uygulama hizmeti planı uygulamalarda herhangi bir sayıda genelinde kullanılan her karma bağlantı kullanılabilir.  My uygulama hizmeti planı'nda 5 ayrı uygulamalarında kullandım 1 karma bağlantı varsa, yine yalnızca 1 karma bağlantı olduğunu toosay olmasıdır.

Yalnızca temel, standart, Premium veya yalıtılmış SKU içinde kullanılabilir olan ötesinde ek maliyet toohybrid bağlantıları yoktur.  Karma bağlantı fiyatlandırma hakkında ayrıntılar lütfen buraya gidin: [Service Bus fiyatlandırma][sbpricing].

## <a name="hybrid-connection-manager"></a>Karma Bağlantı Yöneticisi ##

Karma bağlantılar toowork sırayla geçiş aracısı, karma bağlantı uç noktasını barındıran hello ağdaki gerekir.  Bu geçiş aracısı hello karma Bağlantı Yöneticisi (HCM) adı verilir.  Bu araç hello indirilebilir **Ağ > karma bağlantı uç noktalarınızı yapılandırın** UI hello uygulamanızda kullanılabilir [Azure portal][portal].  

Bu araç, Windows server 2008 R2 ve Windows'un sonraki sürümlerinde çalışır.  Bir kez yüklendikten sonra hello HCM bir hizmet olarak çalışır.  Bu hizmet yapılandırılmış hello uç noktalarda dayalı tooAzure servicebus geçiş bağlanır.  Merhaba HCM Hello bağlantılarından 80 ve 443 giden tooports ' dir.    

Merhaba HCM sahip bir kullanıcı Arabirimi tooconfigure onu.  HCM yüklü hello sonra hello karma Bağlantı Yöneticisi'ni yükleme dizininde bulunur HybridConnectionManagerUi.exe hello çalıştırarak UI hello kullanıma sunabilirsiniz.  Yazarak Windows 10'da kolayca ulaşıldığında *karma Bağlantı Yöneticisi kullanıcı Arabirimi* , arama kutusuna.  

HCM kullanıcı Arabirimi başlatıldığında, hello hello ilk şey, bkz: Merhaba HCM'ın bu örneğinin yapılandırılmış hello karma bağlantılar tümünün listeleyen bir tablo durumdur.  Herhangi bir değişiklik toomake isterseniz Azure ile tooauthenticate gerekir. 

tooadd bir veya daha fazla karma bağlantılar tooyour HCM:

1. Merhaba HCM UI Başlat
1. Başka bir karma bağlantı yapılandırmak tıklayın![][8]

1. Azure hesabınızla oturum açın
1. Bir abonelik seçin
1. ' I tıklatın Bu HCM toorelay istediğiniz hello karma bağlantıları![][9]

1. Kaydet’e tıklayın.

Bu noktada eklediğiniz hello karma bağlantılar görürsünüz.  Ayrıca, yapılandırılmış hello karma bağlantıda tıklatın ve hello bağlantı ayrıntılarını bakın.

![][10]

İle yapılandırılmış HCM toobe mümkün toosupport hello karma bağlantılarınız için onu gerekir:

- TCP bağlantı noktaları 80 ve 443 üzerinden erişim tooAzure
- TCP erişim toohello karma bağlantı uç noktasının
- özelliği toodo DNS aramalarına hello uç noktası ana bilgisayar ve hello azure servicebus ad alanı

Merhaba HCM, hem yeni karma bağlantılar, hem de hello eski BizTalk karma bağlantılar destekler.

### <a name="redundancy"></a>Yedeklilik ###

Her HCM, birden çok karma bağlantılar destekleyebilir.  Ayrıca, herhangi bir belirtilen karma bağlantıyı birden çok HCMs tarafından desteklenebilir.  Merhaba varsayılan davranışı tooround bir kez deneme trafik hello arasında HCMs herhangi belirli bir uç nokta için yapılandırıldı.  Yüksek kullanılabilirlik, karma bağlantılar ağınızdan isterseniz, yalnızca birden çok HCMs ayrı makinelerde örneği oluşturur. 

### <a name="manually-adding-a-hybrid-connection"></a>El ile karma bağlantı ekleme ###

Birisi, abonelik toohost dışında verilen karma bağlantı için bir HCM örneği istiyorsanız, bunları paylaşabilirsiniz hello hello karma bağlantı için ağ geçidi bağlantı dizesi.  Bu hello içinde karma bağlantı hello özelliklerinde görebilirsiniz [Azure portal][portal]. dize, toouse tıklatın hello **el ile yapılandırmanız** düğmesini hello HCM ve hello ağ geçidi bağlantı dizesini yapıştırın.


## <a name="troubleshooting"></a>Sorun giderme ##

Ne zaman karma bağlantınız ile çalışan bir uygulama ayarlanır ve yapılandırılmış Bu karma bağlantısı olan en az bir HCM yoktur sonra hello durum söyleyin **bağlı** hello Portalı'nda.  Değil dediği varsa **bağlı** uygulamanızı çalışmıyor veya, HCM tooAzure 80 veya 443 bağlantı noktalarında giden bağlanamıyor anlamına gelir.  

Merhaba uç noktası bir DNS adı yerine bir IP adresi kullanarak belirtilmediğinden istemciler tootheir endpoint bağlanamıyor hello birincil nedenidir.  Uygulamanızı istenen hello endpoint ulaşamıyor ve bir IP adresi kullandıysanız toousing hello HCM çalıştığı hello konakta geçerli bir DNS adı geçin.  Diğer şeyleri toocheck olduğunuz nerede hello HCM çalıştıran sunucunun ve hello HCM toohello karma bağlantı uç noktasının çalıştığı hello ana bilgisayardan bağlantısı yok hello ana bilgisayarda bu hello DNS adı düzgün çözümler.  

Merhaba tcpping adlı hello konsolundan etkinleştirilebilir uygulama hizmeti bir aracı yoktur.  Bu araç erişim tooa TCP uç noktası sahip ancak erişim tooa karma bağlantı uç noktasının varsa söylemez anlayabilirsiniz.  Karma bağlantı uç noktasının karşı hello konsolunda kullanıldığında, başarılı bir ping işlemi yalnızca bu ana bilgisayar: bağlantı noktası bileşimi kullanan uygulamanız için yapılandırılmış karma bağlantı olduğunu söyler.  

## <a name="biztalk-hybrid-connections"></a>BizTalk Karma Bağlantıları ##

Merhaba eski BizTalk karma bağlantılar özelliği devre dışı toofurther BizTalk karma bağlantı oluşturmaları kapatıldı.  Önceden var olan BizTalk karma bağlantılarınızı uygulamalarınızı ile kullanmaya devam edebilirsiniz ancak toohello yeni hizmet geçirmeniz gerekir.  Merhaba arasında hello BizTalk sürüm üzerinden hello yeni hizmetindeki yararlar şunlardır:

- hiçbir ek BizTalk hesabı gereklidir
- TLS 1.2 BizTalk karma bağlantılar olduğu gibi 1.0 yerine olduğu
- İletişim diğer bağlantı noktaları 80 ve 443 bir IP adresi yerine Azure DNS ad tooreach ve bir dizi ek kullanarak bağlantı noktaları üzerinden önemlidir.  

tooadd bir BizTalk karma bağlantı tooyour uygulaması hello gidin tooyour uygulamada [Azure portal] [ portal] tıklatıp **Ağ > karma bağlantı uç noktalarınızı yapılandırın**.  Merhaba Klasik karma bağlantıları tabloda tıklatın **Klasik karma Bağlantı Ekle**.  Buradan, BizTalk karma bağlantılar listesini görürsünüz.  


<!--Image references-->
[1]: ./media/app-service-hybrid-connections/hybridconn-connectiondiagram.png
[2]: ./media/app-service-hybrid-connections/hybridconn-portal.png
[3]: ./media/app-service-hybrid-connections/hybridconn-addhc.png
[4]: ./media/app-service-hybrid-connections/hybridconn-createhc.png
[5]: ./media/app-service-hybrid-connections/hybridconn-properties.png
[6]: ./media/app-service-hybrid-connections/hybridconn-aspproperties.png
[7]: ./media/app-service-hybrid-connections/hybridconn-hcm.png
[8]: ./media/app-service-hybrid-connections/hybridconn-hcmadd.png
[9]: ./media/app-service-hybrid-connections/hybridconn-hcmadded.png
[10]: ./media/app-service-hybrid-connections/hybridconn-hcmdetails.png

<!--Links-->
[HCService]: http://docs.microsoft.com/azure/service-bus-relay/relay-hybrid-connections-protocol/
[portal]: http://portal.azure.com/
[oldhc]: http://docs.microsoft.com/azure/biztalk-services/integration-hybrid-connection-overview/
[sbpricing]: http://azure.microsoft.com/pricing/details/service-bus/

