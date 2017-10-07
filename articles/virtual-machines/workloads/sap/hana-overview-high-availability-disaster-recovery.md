---
title: "SAP HANA (büyük örnekler) azure'da aaaHigh kullanılabilirlik ve olağanüstü durum kurtarma | Microsoft Docs"
description: "Yüksek kullanılabilirlik ve Azure (büyük örnekler) üzerinde SAP HANA olağanüstü durum kurtarma planı oluşturun."
services: virtual-machines-linux
documentationcenter: 
author: RicksterCDN
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/01/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0c0967f54cf29bbb275eb7cda9d36608488add9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sap-hana-large-instances-high-availability-and-disaster-recovery-on-azure"></a>SAP HANA (büyük örnekler) Azure üzerinde yüksek kullanılabilirlik ve olağanüstü durum kurtarma 

Yüksek kullanılabilirlik ve olağanüstü durum kurtarma, kritik SAP HANA Azure (büyük örnekler) sunucuları üzerinde çalışan önemli yönleri şunlardır. Buna ait önemli toowork SAP ile sistem Tümleştirici veya Microsoft tooproperly mimarı ve uygulama sağ yüksek-kullanılabilirlik/olağanüstü durum kurtarma stratejisi hello. Bu ayrıca belirli tooyour ortamı önemli tooconsider hello kurtarma noktası hedefi ve kurtarma süresi hedefi olur.

## <a name="high-availability"></a>Yüksek kullanılabilirlik

Microsoft dahil SAP HANA yüksek kullanılabilirlik yöntemi "Merhaba kutusu dışı" destekler:

- **Depolama çoğaltma:** depolama sistemin özelliği tooreplicate tüm veri tooanother konumu hello (içinde veya ayrı, aynı veri merkezinde hello). SAP HANA bu yöntem bağımsız olarak çalışır.
- **HANA sistem çoğaltma:** SAP HANA tooa ayrı SAP HANA sistemdeki tüm veri çoğaltma hello. Merhaba kurtarma süresi hedefi düzenli aralıklarla veri çoğaltma ile en aza indirilir. SAP HANA zaman uyumsuz ve zaman uyumlu bellek içi ve zaman uyumlu modda destekler (yalnızca SAP HANA için önerilen içinde sistemlerini hello aynı veri merkezinde veya küçüktür 100 KM parçalayın). Merhaba geçerli tasarımında HANA örneği büyük Damgalar HANA sistem çoğaltma yalnızca yüksek kullanılabilirlik için kullanılabilir.
- **Konak otomatik yük devretme:** yerel arıza kurtarma çözümü toouse bir alternatif toosystem çoğaltma olarak. Merhaba ana düğüm kullanılamaz duruma geldiğinde, bir veya daha fazla bekleme SAP HANA düğümleri genişleme modunda yapılandırılmış ve SAP HANA otomatik olarak tooanother düğüm üzerinde başarısız olur.

SAP HANA yüksek kullanılabilirlik hakkında daha fazla bilgi için aşağıdaki SAP bilgilerle hello bakın:

- [SAP HANA yüksek kullanılabilirlik Teknik İnceleme](http://go.sap.com/documents/2016/05/f8e5eeba-737c-0010-82c7-eda71af511fa.html)
- [SAP HANA Yönetim Kılavuzu](http://help.sap.com/hana/SAP_HANA_Administration_Guide_en.pdf)
- [SAP HANA sistem çoğaltma SAP Akademi Video](http://scn.sap.com/community/hana-in-memory/blog/2015/05/19/sap-hana-system-replication)
- [SAP destek Not #1999880 – SAP HANA sistem çoğaltma hakkında SSS](https://bcs.wdf.sap.corp/sap/support/notes/1999880)
- [Destek Not #2165547 – SAP HANA yedekleme ve geri yükleme SAP HANA sistem çoğaltma ortamında SAP](https://websmp230.sap-ag.de/sap(bD1lbiZjPTAwMQ==)/bc/bsp/sno/ui_entry/entry.htm?param=69765F6D6F64653D3030312669765F7361706E6F7465735F6E756D6265723D3231363535343726)
- [En az/sıfır kapalı kalma süresi ile donanım Exchange için destek Not #1984882 – kullanarak SAP HANA sistem çoğaltma SAP](https://websmp230.sap-ag.de/sap(bD1lbiZjPTAwMQ==)/bc/bsp/sno/ui_entry/entry.htm?param=69765F6D6F64653D3030312669765F7361706E6F7465735F6E756D6265723D3139383438383226)

## <a name="disaster-recovery"></a>Olağanüstü durum kurtarma

SAP HANA Azure (büyük örnekler) üzerinde bir coğrafi bölgede iki Azure bölgelerindeki sunulur. Merhaba iki örnek büyük Damgalar iki farklı bölgeler arasında olağanüstü durum kurtarma sırasında veri çoğaltmak için bir doğrudan ağ bağlantısı olduğundan. Merhaba çoğaltma hello veri depolama altyapısını temel ' dir. Varsayılan olarak Hello çoğaltma yapılmadı. Merhaba olağanüstü durum kurtarma sıralı hello müşteri yapılandırmaları için yapılır. Merhaba geçerli tasarımında HANA sistem çoğaltma olağanüstü durum kurtarma için kullanılamaz.

Ancak, tootake avantajı hello olağanüstü durum kurtarma işlemi toostart toodesign hello ağ bağlantısı toohello iki farklı Azure bölgeleri gerekir. toodo bu nedenle, şirket içi bir Azure ExpressRoute bağlantı hattı bağlantısı, ana Azure bölgesini ve şirket içi tooyour olağanüstü durum kurtarma bölgesinden başka bir bağlantı hattı bağlantı gereksinim. Bu ölçüm, bir Microsoft enterprise edge (MSEE) yönlendirici konumu dahil olmak üzere bir tam bir Azure bölgesinde bir sorun var. bir durum karşılayacağını.

İkinci bir ölçü tooSAP HANA azure'da (büyük örnekler) bağlanan tüm Azure sanal ağlarda hello bölgeleri tooboth bu ExpressRoute bağlantı hatları, birinde bağlanabilir. Bu ölçü, burada Azure ile şirket içi konumunuz bağlayan yalnızca biri hello MSEE konumları görev dışı gider servis talebi giderir.

Merhaba aşağıdaki şekilde hello olağanüstü durum kurtarma için en uygun yapılandırma gösterilmektedir:

![Olağanüstü durum kurtarma için en uygun yapılandırma](./media/hana-overview-high-availability-disaster-recovery/image1-optimal-configuration.png)

Merhaba en iyi bir olağanüstü durum kurtarma yapılandırması hello ağ için toohave iki ExpressRoute bağlantı hatları şirket içi toohello iki farklı bölgelerdeki Azure durumdur. Bir bağlantı hattı üretim örneğini çalıştıran tooregion #1 gider. Merhaba ikinci expressroute bağlantı hattı tooregion #2 ' çalışan bazı üretim dışı HANA örnekler gider. (Merhaba MSEE ve örnek büyük damga dahil olmak üzere tüm Azure bölgesi hello kılavuz devre dışı kalırsa önemlidir.)

İkinci bir ölçü çeşitli sanal ağlar hello bağlı toohello bağlı tooSAP HANA Azure (büyük örnekler) ile ilgili olan çeşitli ExpressRoute bağlantı hatları şunlardır. Daha sonra aşağıdakiler ele gibi burada bir MSEE başarısız olduğu veya hello kurtarma noktası hedefi, olağanüstü durum kurtarma için düşürebilirsiniz hello konumu devre dışı bırakabilir.

bir olağanüstü durum kurtarma kurulumu için Hello sonraki gereksinimleri şunlardır:

- Aynı SKU'ları üretim boyut ve bunları hello olağanüstü durum kurtarma bölgede dağıtma Merhaba, Azure (büyük örnekler) SKU'ları üzerinde SAP HANA sıralamanız gerekir. Bu örnekler, kullanılan toorun test, korumalı alan veya QA HANA örnekler olabilir.
- Bir olağanüstü durum kurtarma profili her Azure (büyük örnekler) SKU'ları üzerinde SAP HANA toorecover hello olağanüstü durum kurtarma sitesindeki istediğiniz gerekirse sipariş gerekir. Bu eylemin hello depolama Çoğaltmada üretim bölgenizi hello olağanüstü durum kurtarma bölge içine hello hedefi olan depolama birimleri toohello ayrılması yol açar.

Hello gereksinimleri önceki karşılayan sonra sorumluluk toostart hello depolama çoğaltma olur. SAP HANA azure'da (büyük örnekler) için kullanılan hello depolama altyapısında hello depolama çoğaltma depolama anlık görüntüleri temelini oluşturur. toostart hello olağanüstü durum kurtarma, çoğaltma tooperform gerekir:

- Daha önce açıklandığı gibi LUN, önyükleme görüntüsünü.
- Daha önce açıklandığı gibi HANA ilgili birim, anlık görüntü.

Bu anlık görüntüleri yürüttükten sonra olağanüstü durum kurtarma profilinizde hello olağanüstü durum kurtarma bölge ile ilişkili hello birimlerde hello birimleri ilk çoğaltmasını sağlanmış.

Merhaba en son depolama anlık görüntü saatte daha sonra kullanılan hello depolama birimlerde geliştirmek tooreplicate hello farkları.

Bu yapılandırma ile elde edilen hello kurtarma noktası hedefi 60 too90 dakikadır. tooachieve daha iyi bir kurtarma hedefi hello olağanüstü durum kurtarma durumda, kopyalama hello HANA işlem günlüğü yedeklemeleri SAP HANA gelen Azure (büyük örnekler) toohello üzerinde başka bir Azure bölgesine işaret edin. tooachieve bu kurtarma noktası hedefi aşağıdaki hello:

1. Geri hello HANA Hareketi oluşturan sıklıkta olabildiğince çok/hana/günlük/yedekleme oturum açın.
2. Tamamlanmış tooan Azure sanal toohello SAP HANA Azure (büyük örnekler) sunucuya bağlanan sanal ağ olan makine (VM) olduklarında hello işlem günlüğü yedeklemeleri kopyalayın.
3. Bu sanal makineden hello yedekleme tooa hello olağanüstü durum kurtarma bölgede bulunan bir sanal ağ içinde VM kopyalayın.
4. Merhaba işlem günlüğü yedeklemeleri hello VM bu bölgede unutmayın.

Merhaba olağanüstü durum kurtarma profili gerçek bir sunucuda dağıtıldıktan sonra olağanüstü bir durumunda hello işlem günlüğü yedeklemeleri hello VM toohello SAP HANA azure'da hello olağanüstü durum kurtarma bölgede şimdi hello birincil sunucu olan (büyük örnekler) kopyalayın ve Bu yedekleri geri yükleyin. HANA Hello durumunu hello olağanüstü durum kurtarma disklerde, HANA anlık görüntüsünün olduğundan bu kurtarma mümkün değildir. İşlem günlüğü yedeklemeleri, daha fazla geri yüklemeler için uzaklık noktası hello budur.

## <a name="backup-and-restore"></a>Yedekleme ve geri yükleme

Merhaba en önemli yönleri toooperating veritabanlarından birini hello veritabanı çeşitli yıkıcı olaylarından korunabilir emin yapılmasıdır. Bu olaylar tarafından herhangi bir şey doğal afetler toosimple kullanıcı hatalarından neden olabilir.

Bir veritabanıyla hello özelliği toorestore onu tooany noktası zamanında yedekleme (gibi birisi kritik verileri silmeden önce), başlangıç engellemeyi oluşmadan önce olduğu gibi olası toohello yol kapatmak gibi geri yükleme tooa durumunu sağlar.

En iyi sonuçlar için yedeklemeler iki tür gerçekleştirilmesi gerekir:

- Veritabanı yedeklemeleri
- İşlem günlüğü yedeklemeleri

Ayrıca bir uygulama düzeyinde gerçekleştirilen toofull veritabanı yedeklemeleri, depolama anlık görüntüleri yedeklemelerde gerçekleştirerek daha kapsamlı olabilir. Günlük yedeklemeleri gerçekleştirmek da hello veritabanı (ve tooempty hello zaten yürütülen işlemler günlüklerinden) geri yüklemek için önemlidir.

SAP HANA Azure (büyük örnekler) üzerinde iki yedekleme ve geri yükleme seçenekleri sunar:

- Bunu kendiniz (DIY). Yeterli disk alanı tooensure hesaplamak sonra tam veritabanı ve günlük yedekleri disk yedekleme yöntemleri (toothose diskleri) kullanarak gerçekleştirin. Zaman içerisinde, hello yedeklemeleri kopyalanan tooan (bir Azure tabanlı bir dosya sunucusu ile neredeyse sınırsız depolama ayarladıktan sonra) Azure depolama hesabı olan veya bir Azure yedekleme kasası veya Azure soğuk depolama kullanın. Tooa depolama hesabı CommVault, bunlar sonra toostore hello yedeklemeleri kopyalanan gibi başka bir seçenek toouse bir üçüncü taraf veri koruma Aracı ' dir. Merhaba Dıy yedekleme seçeneği de uyumluluk ve denetleme amaçları için uzun süre depolanan toobe gereken veriler için gerekli olabilir.
- Merhaba yedekleme ve geri yükleme altyapının SAP HANA (büyük örnekler) azure'da hello işlevselliği sağlar. Bu seçenek yedeklemeleri hello gereksinimini yerine getirir ve el ile yedekleme (burada veri yedeklemeleri uyumluluk amacıyla gerekli olan dışında) neredeyse geçersiz kılar. Bu bölümde adresleri Hello kalanını yedekleme hello ve HANA (büyük örnekler) ile sunulan işlevselliği geri yükleyin.

> [!NOTE]
> Merhaba temel altyapısı HANA (büyük örnekler) tarafından kullanılan hello anlık görüntü teknolojisi SAP HANA anlık görüntü bir bağımlılığa sahiptir. SAP HANA anlık görüntüler, SAP HANA çok kullanıcılı veritabanı kapsayıcıları ile birlikte çalışmaz. Sonuç olarak, bu yöntem Yedekleme kullanılan toodeploy SAP HANA çok kullanıcılı veritabanı kapsayıcıları olamaz.

### <a name="using-storage-snapshots-of-sap-hana-on-azure-large-instances"></a>SAP HANA depolama anlık görüntüleri (büyük örnekler) Azure üzerinde kullanma

SAP HANA Azure (büyük örnekler) ile ilgili temel hello depolama altyapısını birimleri depolama görüntüsünü hello kavramını destekler. İle ilgili önemli noktalar aşağıdaki hello yedekleme ve geri yükleme belirli bir birimi desteklenir:

- Veritabanı Yedeklemeleri yerine depolama birim anlık görüntülerini üzerinde düzenli aralıklarla alınır.
- Merhaba depolama anlık görüntü yürütülmeden önce hello depolama anlık görüntü SAP HANA anlık görüntü başlatır. Bu SAP HANA anlık görüntü hello Kurulum son günlük geri yüklemeler için hello depolama anlık görüntü kurtarma işleminden sonra noktasıdır.
- Merhaba depolama anlık görüntü başarıyla çalıştırıldığı hello noktada hello SAP HANA anlık görüntü silinir.
- Günlük yedeklerini sık gerçekleştirilen ve hello günlük yedekleme birimi veya Azure depolanır.
- Merhaba veritabanının geri yüklenmesi gerekiyorsa tooa belirli bir nokta, bir istek tooMicrosoft Azure desteği (üretim kesinti) veya SAP HANA Azure Hizmet Yönetimi toorestore tooa üzerinde belirli yapıldığında depolama anlık görüntü (örneğin, bir planlı geri yüklenmesini bir korumalı alan sistemi tooits özgün durumuna).
- Merhaba depolama anlık görüntüsüne dahil hello SAP HANA anlık görüntü yürütülen ve hello depolama anlık görüntü alındıktan sonra depolanan günlük yedeklerini uygulamak için uzaklık bir noktadır.
- Bu günlük yedeklemeler toorestore alınır hello veritabanı geri tooa belirli bir nokta.

Belirten hello yedekleme\_adı birimler aşağıdaki hello görüntüsünü oluşturur:

- hana/veri
- hana/günlük
- hana/log\_yedekleme (yedekleme olarak hana/günlüğüne bağlı)
- hana ve paylaşılan

### <a name="storage-snapshot-considerations"></a>Depolama anlık görüntü konuları

>[!NOTE]
>Depolama anlık görüntüleri _değil_ sağlanan ek depolama alanı ayrılmış olduğundan gider, boş.

SAP HANA Azure (büyük örnekler) üzerinde depolama anlık görüntüleri belirli mekanikleri Hello şunları içerir:

- Belirli bir depolama anlık görüntü (noktasında hello zaman geçen süre) çok az depolama kullanır.
- Veri içerik değişikliklerini ve SAP HANA veri dosyaları hello depolama biriminde değiştirme hello içeriği hello anlık görüntü toostore hello özgün blok içerik gerekir.
- Merhaba depolama anlık görüntü boyutunu artırır. Merhaba uzun hello anlık görüntü var, hello büyük hello depolama anlık görüntüsü olur.
- Daha fazla yapılan değişiklikler toohello SAP HANA veritabanı birimindeki depolama anlık görüntü hello ömrü boyunca Merhaba, hello büyük hello alanı tüketimini hello depolama anlık görüntüsünün olur.

SAP HANA (büyük örnekler) azure'da hello SAP HANA veri ve günlük birimi sabit birim boyutlarını birlikte gönderilir. Böylece, sorumluluk tooschedule depolama anlık görüntüler (içinde SAP HANA hello Azure [büyük örneklerini] işleme) bu birimlerin anlık görüntüleri gerçekleştirme, Birim alanına eats.

Merhaba aşağıdaki bölümlerde genel öneriler dahil olmak üzere, bu anlık görüntüleri gerçekleştirmeye yönelik bilgileri sağlayın:

- Merhaba donanım 255 anlık görüntüler birim başına karşılayabilir rağmen bu sayının altına de Kal öneririz.
- Depolama anlık görüntüleri gerçekleştirmeden önce izlemek ve boş alan izler.
- Alt hello boş disk alanına dayalı depolama anlık görüntü sayısı. Toolower hello güvenliğinizi anlık görüntü sayısı gerekebilir veya tooextend hello birimleri gerekebilir. (1 TB birimlerinde ek depolama alanı sıralayabilirsiniz.)
- SAP HANA sistem Geçiş Araçları (R3load veya SAP HANA veritabanlarını yedeklerden geri yükleme tarafından) veri taşıma gibi etkinlikleri sırasında yüksek oranda, tüm depolama anlık görüntüleri gerçekleştirmenizi değil önerilir. (Yeni bir SAP HANA sistemine yapılan bir sistem geçiş, depolama anlık görüntüleri gerçekleştirilen toobe ihtiyaç duymaz.)
- Sırasında daha büyük düzenlemelere SAP HANA tablo depolama anlık görüntüleri mümkünse kaçınılmalıdır.
- Depolama anlık görüntüler (büyük örnekler) azure'da SAP HANA önkoşul tooengaging hello olağanüstü durum kurtarma özelliklerini değildir.

### <a name="setting-up-storage-snapshots"></a>Depolama anlık görüntüleri ayarlama

1. Perl hello Linux işletim sisteminde hello HANA (büyük örnekler) sunucusunda yüklü olduğundan emin olun.
2. Değiştirme/etc/ssh/ssh\_config tooadd hello satır _Mac'ler hmac-sha1_.
3. Hello Yöneticisi düğümünde (varsa) çalıştıran her SAP HANA örneği için bir SAP HANA yedekleme kullanıcı hesabı oluşturun.
4. Merhaba SAP HANA HDB istemci tüm SAP HANA (büyük örnekler) sunucularda yüklü olması gerekir.
5. Merhaba ilk SAP HANA (büyük örnekler) sunucusuna her bölge, bir ortak anahtar anlık görüntü oluşturma denetimleri depolama altyapısını temel tooaccess hello oluşturulması gerekir.
6. Azure Hello betiği kopyalayın\_hana\_/scripts toohello konumundan backup.pl **hdbsql** hello SAP HANA yükleme.
7. Kopya hello HANABackupDetails.txt dosya/Scripts toohello aynı Perl komut dosyasını hello gibi konumu.
8. Merhaba HANABackupDetails.txt dosyasını hello uygun müşteri belirtimleri için gerektiği şekilde değiştirin.

### <a name="step-1-install-sap-hana-hdbclient"></a>1. adım: SAP HANA HDBClient yükleme

Merhaba SAP HANA Azure (büyük örnekler) üzerinde yüklü Linux hello klasörlerini içerir ve gerekli tooexecute SAP HANA depolama anlık görüntüleri yedekleme ve olağanüstü durum kurtarma amacıyla komut dosyaları. Ancak, SAP HANA yüklerken, sorumluluk tooinstall SAP HANA HDBclient olur. (Microsoft hello HDBclient ne SAP HANA yükler.)

### <a name="step-2-change-etcsshsshconfig"></a>2. adım: / etc/değiştirmek ssh/ssh\_yapılandırma

Değiştirme/etc/ssh/ssh\_ekleyerek config _Mac'ler hmac-sha1_ satır aşağıda gösterildiği gibi:
```
#   RhostsRSAAuthentication no
#   RSAAuthentication yes
#   PasswordAuthentication yes
#   HostbasedAuthentication no
#   GSSAPIAuthentication no
#   GSSAPIDelegateCredentials no
#   GSSAPIKeyExchange no
#   GSSAPITrustDNS no
#   BatchMode no
#   CheckHostIP yes
#   AddressFamily any
#   ConnectTimeout 0
#   StrictHostKeyChecking ask
#   IdentityFile ~/.ssh/identity
#   IdentityFile ~/.ssh/id_rsa
#   IdentityFile ~/.ssh/id_dsa
#   Port 22
Protocol 2
#   Cipher 3des
#   Ciphers aes128-ctr,aes192-ctr,aes256-ctr,arcfour256,arcfour128,aes128-cbc,3des-cbc
#   MACs hmac-md5,hmac-sha1,umac-64@openssh.com,hmac-ripemd160
MACs hmac-sha1
#   EscapeChar ~
#   Tunnel no
#   TunnelDevice any:any
#   PermitLocalCommand no
#   VisualHostKey no
#   ProxyCommand ssh -q -W %h:%p gateway.example.com
```

### <a name="step-3-create-a-public-key"></a>3. adım: bir ortak anahtar oluşturma

Üzerinde Hello Azure (büyük örnekler) sunucusundaki her bir Azure bölgesine ilk SAP HANA oluşturun kullanılan ortak anahtar toobe tooaccess hello depolama altyapısını böylece anlık görüntülerini oluşturabilirsiniz. Merhaba ortak anahtarı bir parola gerekli toosign toohello depolama değildir ve parola kimlik korunmuyor sağlar. Merhaba SAP HANA (büyük örnekler) sunucusunda Linux komut toogenerate hello ortak anahtar aşağıdaki hello yürütün:
```
  ssh-keygen –t dsa –b 1024
```
Merhaba yeni konumu: _/root/.ssh/id\_dsa.pub. Gerçek bir parola girmeyin, aksi takdirde oturum her zaman gerekli tooenter hello parola olacaktır. Bunun yerine, basın **Enter** iki kez tooremove hello oturum açmak için parola gereksinimi girin.

Toomake hello ortak anahtara düzeltildi klasörleri too/root/.ssh/ değiştirme ve hello yürütme beklendiği gibi emin denetleyin **ls** komutu. Merhaba anahtar mevcut değilse, komutu aşağıdaki hello çalıştırarak kopyalayabilirsiniz:

![Ortak anahtar şu komutu çalıştırarak kopyalanır.](./media/hana-overview-high-availability-disaster-recovery/image2-public-key.png)

Bu noktada, Azure Hizmet Yönetimi SAP HANA başvurun ve başlangıç anahtarı sağlayın. Merhaba temsilcisiyle kullanan hello ortak anahtar tooregister depolama altyapısını temel hello içinde.

### <a name="step-4-create-an-sap-hana-user-account"></a>4. adım: bir SAP HANA kullanıcı hesabı oluşturma

SAP HANA Studio'dan bir SAP HANA kullanıcı hesabıyla yedekleme amacıyla oluşturun. Bu hesabın ayrıcalıkları aşağıdaki hello olmalıdır: _yedekleme yönetici_ ve _katalog okuma_. Bu örnekte, hello kullanıcıadı SCADMIN oluşturulur.

![Bir kullanıcı HANA Studio'da oluşturma](./media/hana-overview-high-availability-disaster-recovery/image3-creating-user.png)

### <a name="step-5-authorize-hello-sap-hana-user-account"></a>5. adım: hello SAP HANA kullanıcı hesabı yetkilendirme

Merhaba SAP HANA kullanıcı hesabı (Merhaba komut dosyası her çalıştırıldığında yetkilendirme gerek kalmadan hello komut dosyaları tarafından kullanılan toobe) yetkilendirin. SAP HANA komutu Hello `hdbuserstore` bir veya daha fazla SAP HANA düğümde depolanan bir SAP HANA kullanıcı anahtarı hello oluşturulmasına izin verir. Merhaba kullanıcı anahtarı daha sonra açıklanan işlemi scripting hello içinde toomanage parolalardan gerek kalmadan hello kullanıcı tooaccess SAP HANA de sağlar.

>[!IMPORTANT]
>Çalışma hello komut olarak aşağıdaki `_root_`. Aksi takdirde hello betik düzgün çalışamaz.

Merhaba girin `hdbuserstore` gibi komut:

![Merhaba hdbuserstore komutu girin](./media/hana-overview-high-availability-disaster-recovery/image4-hdbuserstore-command.png)

Burada hello kullanıcı SCADMIN01 ve hello hostname lhanad01, örneğin, aşağıdaki hello hello komut şöyledir:
```
hdbuserstore set SCADMIN01 lhanad01:30115 <backup username> <password>
```
Tüm komut dosyası genişleme HANA örnekleri için tek bir sunucudan yönetin. Bu örnekte, hello SAP HANA anahtar SCADMIN01 ilgili toohello anahtarı hello konak yansıtır şekilde her bir konak için değiştirilmesi gerekir. Merhaba SAP HANA yedekleme hesabı hello örneği sayısıyla hello HANA DB, diğer bir deyişle, dayanıklıdır **lhanad**. başlangıç anahtarı atandığı hello ana bilgisayarda yönetici ayrıcalıklarına sahip olmalıdır ve hello yedekleme kullanıcı genişleme için erişim haklarını tooall SAP HANA örnekleri olması gerekir.
```
hdbuserstore set SCADMIN01 lhanad:30015 SCADMIN <password>
hdbuserstore set SCADMIN02 lhanad:30115 SCADMIN <password>
hdbuserstore set SCADMIN03 lhanad:30215 SCADMIN <password>
```

### <a name="step-6-copy-items-from-hello-scripts-folder"></a>6. adım: öğeleri hello/Scripts klasörüne kopyalayın.

Kopya hello aşağıdaki öğeleri hello / (Merhaba yüklemenin hello altın görüntüsünü dahil) klasöründen toohello çalışma dizini için komut dosyası **hdbsql**. Geçerli HANA yüklemeler için bu /hana/shared/D01/exe/linuxx86 dizindir\_64/hdb.
```
azure\_hana\_backup.pl
testHANAConnection.pl
testStorageSnapshotConnection.pl
removeTestStorageSnapshot.pl
HANABackupCustomerDetails.txt
```
Genişleme çalıştırıyorsanız aşağıdaki öğelerindeki hello veya OLAP kopyalayın:
```
azure\_hana\_backup\_bw.pl
testHANAConnectionBW.pl
testStorageSnapshotConnectionBW.pl
removeTestStorageSnapshotBW.pl
HANABackupCustomerDetailsBW.txt
```
Merhaba HANABackupCustomerDetails.txt dosya şu şekilde büyütme dağıtımlar için değiştirilebilir. Bunu hello denetim ve yapılandırma hello depolama anlık görüntüleri çalışan hello komut dosyasıdır. Hello alınan _depolama yedekleme adı_ ve _depolama IP adresi_ SAP HANA örneklerinizi dağıtıldığında Azure Hizmet Yönetimi'nden. Sıralama hello sırası değiştirilemiyor veya herhangi bir hello değişkenleri veya hello betik aralığını düzgün çalışmaz.

Büyütme dağıtımı için hello yapılandırma dosyası gibi görünür:
```
#Provided by Microsoft Service Management
Storage Backup Name: lhanad01backup
Storage IP Address: 10.250.20.21
#Created by customer using hdbuserstore
HANA Backup Name: SCADMIND01
```
Bir genişleme yapılandırması için hello HANABackupCustomerDetailsBW.txt dosya gibi görünür:
```
#Provided by Microsoft Service Management
Storage Backup Name: lhanad01backup
Storage IP Address: 10.250.20.21
#Node IP addresses, instance numbers, and HANA backup name
#provided by customer.  HANA backup name created using
#hdbuserstore utility.
Node 1 IP Address: 10.254.15.21
Node 1 HANA instance number: 01
Node 1 HANA Backup Name: SCADMIN01
Node 2 IP Address: 10.254.15.22
Node 2 HANA instance number: 02
Node 2 HANA Backup Name: SCADMIN02
Node 3 IP Address: 10.254.15.23
Node 3 HANA instance number: 03
Node 3 HANA Backup Name: SCADMIN03
Node 4 IP Address: 10.254.15.24
Node 4 HANA instance number: 04
Node 4 HANA Backup Name: SCADMIN04
Node 5 IP Address: 10.254.15.25
Node 5 HANA instance number: 05
Node 5 HANA Backup Name: SCADMIN05
Node 6 IP Address: 10.254.15.26
Node 6 HANA instance number: 06
Node 6 HANA Backup Name: SCADMIN06
Node 7 IP Address: 10.254.15.27
Node 7 HANA instance number: 07
Node 7 HANA Backup Name: SCADMIN07
Node 8 IP Address: 10.254.15.28
Node 8 HANA instance number: 08
Node 8 HANA Backup Name: SCADMIN08
```
>[!NOTE]
>Şu anda yalnızca düğüm 1 ayrıntıları hello gerçek HANA depolama anlık görüntü komut dosyasında kullanılır. Merhaba yönetici yedekleme düğümü hiç değişirse, zaten başka bir düğüme onun yerine düğüm 1 hello ayrıntılarında değiştirerek alabilir sağladıktan böylece tüm HANA düğümlerinden erişim tooor sınamanızı öneririz.

toocheck hello doğru yapılandırmaları hello yapılandırma dosyası veya komut dosyaları aşağıdaki hello birini çalıştırın, doğru bağlantı toohello HANA örnekleri için:
- Büyütme için bir yapılandırma (SAP iş yüküne bağımsız olarak):

 ```
testHANAConnection.pl
```
- Genişleme yapılandırma için:

 ```
testHANAConnectionBW.pl
```

Erişim gerekli tooall HANA sunucuları bu hello ana HANA örneği olduğundan emin olun. Parametreleri toohello betik vardır, ancak tamamlamanız gereken uygun HANABackupCustomerDetails hello / HANABackupCustomerDetailsBW hello betik toorun için doğru dosya. Yalnızca hello Kabuk komutu hata kodları döndürdüğünden, her örneği tooerror onay hello komut dosyası için bu mümkün değildir. Buna rağmen hello betik bazı yararlı yorumlar sağlar ve bu da, toodouble-denetle.

toorun hello komut dosyası:
```
 ./testHANAConnection.pl
```
 Merhaba komut dosyası başarıyla hello HANA örneği hello durumunu elde ederse hello HANA bağlantısı başarılı bir ileti görüntüler.

Ayrıca, ikinci bir türü yok komut dosyasının toohello depolama toocheck hello ana HANA örneği sunucunun özelliği toosign kullanabilirsiniz. Hello azure yürütmeden önce\_hana\_yedekleme (\_bw) .pl betik hello sonraki betik yürütmeniz gerekir. Bir birim anlık görüntü yok içeriyorsa, bu imkansız toodetermine hello birim yalnızca boş olduğu ya da olup bir ssh hatası tooobtain hello ayrıntıları anlık görüntüsünü alın. Bu nedenle, iki adımı hello komut dosyasını çalıştırır:

- Bu, bu hello depolama konsol erişilebilir durumda olduğunu doğrular.
- HANA örneği tarafından her birim için bir test veya kukla, anlık görüntü oluşturur.

Bu nedenle, hello HANA örneği bağımsız değişken olarak dahil edilir. Yeniden hello depolama bağlantı denetlemesi olası tooprovide hata olmadığı, ancak hello yürütme başarısız olursa hello betik yararlı ipuçları sağlar.

Merhaba komut dosyası olarak çalıştırın:
```
 ./testStorageSnapshotConnection.pl <hana instance>
```
Veya farklı çalıştır:
```
./testStorageSnapshotConnectionBW.pl <hana instance>
```
Merhaba komut ayrıca, sahip olduğunuz hello sunucu örnekleri tarafından kullanılan hello mantıksal birim numaraları (LUN) etrafında düzenlenmiştir uygun şekilde dağıtılan tooyour depolama kiracısında, mümkün toosign olduğunu bildiren bir mesaj görüntüler.

İlk Depolama anlık görüntü tabanlı yedeklemeleri hello yürütmeden önce hello sonraki komut dosyaları toomake bu hello yapılandırmasının doğru olduğundan emin çalıştırın.

Bu komut dosyalarını çalıştırdıktan sonra yürüterek hello anlık görüntüleri silebilirsiniz:
```
./removeTestStorageSnapshot.pl <hana instance>
```
Veya
```
./removeTestStorageSnapshot.pl <hana instance>
```

### <a name="step-7-perform-on-demand-snapshots"></a>7. adım: isteğe bağlı anlık görüntüler gerçekleştirin

İsteğe bağlı anlık görüntüleri (yanı sıra cron kullanarak normal anlık görüntüleri zamanlamak) burada açıklandığı gibi.

Büyütme yapılandırmaları için komut dosyası izleyen hello yürütün:
```
./azure_hana_backup.pl lhanad01 customer 20
```
Genişleme yapılandırmaları için komut dosyası izleyen hello yürütün:
```
./azure_hana_backup_bw.pl lhanad01 customer 20
```
Merhaba genişleme betik bazı ek denetimi toomake tüm HANA sunucuları erişilebilir ve tüm HANA örnekleri dönüş SAP HANA ya da depolama anlık görüntüleri oluşturma ile devam etmeden önce hello örneğinin uygun durumu emin yapar.

Şu bağımsız hello gereklidir:

- Merhaba HANA örneği gerektiren yedekleme.
- Merhaba depolama anlık görüntü için başlangıç anlık görüntü önek.
- Anlık görüntü toobe hello belirli önekini tutulan Hello sayısı.

```
./azure_hana_backup.pl lhanad01 customer 20
```

Merhaba betik yürütme işlemi hello bu üç ayrı evrede hello depolama anlık görüntü oluşturur:

- HANA anlık görüntü yürütün.
- Bir depolama anlık görüntü yürütün.
- Merhaba HANA anlık görüntü kaldırın.

Kopyalanmış olduğu hello HDB yürütülebilir klasöründen çağırarak Hello betiğini yürütün. Bu yedekler en az birimler Merhaba, ancak bunu da hello birim adı hello açık SAP HANA örnek adına sahip herhangi bir birim yedekler.
```
hana_data_<hana instance>_prod_t020_vol
hana_log_<hana instance>_prod_t020_vol
hana_log_backup_<hana instance>_prod_t020_vol
hana_shared_<hana instance>_prod_t020_vol
```
Merhaba saklama dönemi kesinlikle, anlık görüntü (örneğin, 20, daha önce gösterilen) hello komut yürüttüğünüzde parametre olarak gönderilen hello sayısı ile yönetilir. Bu nedenle hello süreyi anlık görüntüleri hello çağrısında hello komut yürütme ve hello sayısının hello döneminin bir işlevdir. Merhaba tutulur anlık görüntü sayısı hello çağrısında hello komut dosyasının bir parametre olarak adlı hello sayıyı aşarsa, bu etiketin eski depolama anlık görüntü hello (önceki örnekte _özel_) yeni bir anlık görüntüdür önce silinir yürütülebilir. Bu hello hello çağrının son parametre toocontrol hello anlık görüntü sayısı bir hello numarasını olarak size hello numarası anlamına gelir.

>[!NOTE]
>Merhaba etiketi değiştirmek hemen hello sayım yeniden başlatır.

Birden çok düğümlü ortamlarda anlık görüntüleri oluşturuyorsanız, bağımsız değişken olarak SAP HANA Azure Hizmet Yönetimi tarafından sağlanan tooinclude hello HANA örnek adı gerekir. Tek düğümlü ortamlarda, hello hello SAP HANA Azure (büyük örnekler) birimi üzerinde yeterli adıdır, ancak hello HANA örnek adı hala önerilir.

Ayrıca, geri kullanarak önyükleme volumes\LUNs yukarı aynı hello komut dosyası. HANA, ilk kez çalıştırdığınızda cron içinde önyükleme haftalık veya gecelik yedekleme zamanlaması öneririz rağmen önyükleme biriminizi en az bir kez yedeklemeniz gerekir. Bunun yerine bir SAP HANA örnek adı eklemek daha ekleme _önyükleme_ bağımsız değişkeni hello komut dosyanıza aşağıdaki gibi hello olarak:
```
./azure_hana_backup boot customer 20
```
Merhaba bir de toohello önyükleme birimi en aynı bekletme ilkesi karşılanan. İsteğe bağlı anlık görüntüler, açıklandığı gibi SAP geliştirmesini paket (EHP) yükseltme işlemi sırasında veya toocreate ayrı depolama anlık görüntü gerektiğinde gibi daha önce yalnızca, özel durumlar için kullanın.

Cron kullanarak zamanlanmış tooperform depolama anlık görüntüsünü öneririz ve tüm yedekleme ve olağanüstü durum kurtarma gereksinimlerini (çeşitli yedekleme kez istenen değiştirme hello komut dosyası girişleri toomatch hello) için aynı komut dosyası hello kullanmanızı öneririz. Bunlar tüm farklı cron kendi yürütme süresi bağlı olarak, zamanlanan: saat, 12 saatlik, günlük veya haftalık. daha önce ele alınan hello site dışındaki uzun dönem yedekleme için saklama etiketleme eşleşen tasarlanmış toocreate depolama anlık görüntüleri Hello cron zamanlamadır. Merhaba betik komutları tooback kendi istenen sıklığı (Merhaba önyükleme birimi günlük yedek desteklenir ancak veri ve günlük dosyaları saatlik yedekleme, yedeklenen) bağlı olarak tüm üretim birimleri içerir.

cron komut dosyası izleyen hello Hello girişlerinde saatte on dakika, her 12 saatte hello on dakika ve günlük hello on dakika hello çalıştırın. Merhaba saatlik ve günlük yedekleri hello aynı (12:10:00) saat gerçekleşmesi olmayan bir şekilde oluşturulan işleri hello cron bu yalnızca bir SAP HANA depolama anlık görüntü belirli bir saatte gerçekleşir. toohelp en iyi duruma getirme anlık görüntü oluşturma ve çoğaltma, SAP HANA Azure Hizmet Yönetimi Merhaba, toorun süredir Yedeklemelerinizin önerilen sağlar.

içinde /etc/crontab zamanlama hello varsayılan cron aşağıdaki gibidir:
```
10 1-11,13-23 * * * ./azure_hana_backup.pl lhanad01 hourly 66
10 12 * * *  ./azure_hana_backup.pl lhanad01 12hour 14
```
Merhaba önceki cron yönergelerinde hello etiketle anlık görüntü bir saatlik hello HANA birimler (olmadan, önyükleme birimi) alın. Bu anlık görüntülerini 66 korunur. Ayrıca, hello 12 saatlik etiketle 14 anlık görüntüleri korunur. Potansiyel olarak saatlik anlık görüntüleri üç gün artı 12 saatlik anlık görüntüler için başka bir dört anlık görüntü tüm bir hafta sağlayan gün boyunca alırsınız.

Hello komut dosyaları tarafından birkaç dakika dağılır sürece belirli bir anda yalnızca tek bir betik yürütülmesi gereken çünkü içinde cron zamanlama hassas, olabilir. Uzun vadeli bekletme için günlük yedeklemeler istiyorsanız, günlük bir anlık görüntü 12 saatlik anlık görüntü (yedi her bekletme sayısı ile) birlikte tutulur veya sonraki 10 dakika hello saatlik anlık görüntü düzenlenmiş tootake yerdir. Yalnızca bir günlük anlık görüntü hello üretim biriminde tutulur.
```
10 1-11,13-23 * * * ./azure_hana_backup.pl lhanad01 hourly 66
10 12 * * *  ./azure_hana_backup.pl lhanad01 12hour 7
10 0 * * * ./azure_hana_backup.pl lhanad01 daily 7
```
Burada listelenen hello sıklıklarını yalnızca örnektir. tooderive, en uygun sayıda anlık görüntü, aşağıdaki ölçütleri kullanın hello:

- Kurtarma süresi hedefi zaman içinde nokta kurtarma gereksinimleri.
- Alanı kullanımı.
- Gereksinimleri kurtarma noktası hedefi ve potansiyel olağanüstü durum kurtarma için kurtarma süresi hedefi.
- Diskleri karşı HANA tam veritabanı yedeklemeleri nihai yürütülmesi. Tam bir veritabanı yedeği her diskleri karşı veya _backint_ arabirim, olan gerçekleştirilen, depolama anlık görüntüleri hello yürütülmesi başarısız olur. Depolama anlık görüntüleri üstünde tooexecute tam veritabanı yedeklemeleri planlıyorsanız, depolama anlık görüntüleri hello yürütülmesi bu süre boyunca devre dışı bırakıldığından emin olun.

>[!IMPORTANT]
> yalnızca hello anlık görüntüleri SAP HANA günlük yedekleri birlikte gerçekleştirildiğinde depolama anlık görüntüleri hello kullanımını SAP HANA yedeklemeler için geçerlidir. Bu yedeklemeler gerek toobe mümkün toocover hello dönemleri hello depolama anlık görüntüleri arasında günlük. 30 günlük bir zaman içinde nokta kurtarma taahhüt toousers oluşturmadıysanız, hello aşağıdaki gerekir:

- Özelliği tooaccess 30 günden daha eski bir depolama anlık görüntüyü.
- Merhaba son 30 gün içinde bitişik günlük yedeklemeler.

Günlük yedeklerini Hello aralığında hello Yedekleme günlüğü de birimin anlık görüntüsünü oluşturun. Ancak, yapabilmeniz emin tooperform normal günlük yedeklerini olabilir:

- Merhaba bitişik günlük yedeklerini tooperform zaman içinde nokta kurtarma gerekli sahip.
- Merhaba SAP HANA günlük birimi azalmasını önler.

Merhaba son adımları tooschedule SAP HANA yedekleme günlükleri SAP HANA Studio'da biridir. Merhaba SAP HANA Yedekleme günlüğü hedef olan özel olarak oluşturulan hello hana/log\_yedeklemeler toplu /hana/log/backups hello bağlama noktası ile.

![SAP HANA yedekleme zamanlaması SAP HANA Studio'da günlüğe kaydeder](./media/hana-overview-high-availability-disaster-recovery/image5-schedule-backup.png)

Her 15 dakikadan daha sık yedeklemeler seçebilirsiniz. Devam eden önermiyoruz rağmen bazı kullanıcılar bile günlük dakikada, yedeklemeler _üzerinden_ 15 dakika.

Merhaba son tooperform dosya tabanlı Yedekleme (sonra ilk kez yüklenirken SAP HANA hello) toocreate hello yedekleme kataloğu içinde bulunması gereken tek bir yedekleme girişi adımdır. Aksi takdirde SAP HANA belirtilen günlük Yedeklemelerinizin başlatamaz.

![Dosya tabanlı Yedekleme toocreate tek bir yedekleme giriş yapın](./media/hana-overview-high-availability-disaster-recovery/image6-make-backup.png)

### <a name="monitoring-hello-number-and-size-of-snapshots-on-hello-disk-volume"></a>Merhaba sayısını ve boyutunu hello disk birimi anlık görüntü izleme

Bir depolama biriminde hello sayısı anlık görüntüler ve anlık görüntüleri hello depolama tüketimini izleyebilirsiniz. Merhaba `ls` değil Göster komutu hello anlık görüntü dizin veya dosyalar. Ancak, Linux işletim sistemi komutu hello `du` , komutları aşağıdaki hello ile yapar:

- `du –sh .snapshot`Başlangıç anlık görüntü dizini içindeki tüm anlık görüntüleri toplam sağlar.
- `du –sh --max-depth=1`Merhaba .snapshot klasörü ve her anlık görüntü boyutunu hello kaydedilmiş tüm anlık görüntüleri listeler.
- `du –hc`tüm anlık görüntüleri tarafından kullanılan hello toplam boyutu sağlar.

Bu komutlar toomake hello birimlerde tüm hello depolama alınır ve depolanan hello anlık görüntüleri kullanma değil emin kullanın.

### <a name="reducing-hello-number-of-snapshots-on-a-server"></a>Anlık görüntüler bir sunucuda Hello sayısını azaltma

Daha önce açıklandığı gibi hello belirli etiketleri depoladığınız anlık görüntü sayısını azaltabilirsiniz. Merhaba tooretain hello komutu tooinitiate bir anlık görüntüsü olan bir etiketi ve hello istediğiniz anlık görüntü sayısı iki parametrelerinin son.
```
./azure_hana_backup.pl lhanad01 customer 20
```
Başlangıç anlık görüntü etiketi Hello önceki örnekte olduğu _müşteri_ ve anlık görüntüleri korunur Bu etiket toobe ile Merhaba sayısı _20_. Toodisk alanı tüketimini yanıt olarak tooreduce hello depolanan anlık görüntü sayısı isteyebilirsiniz. Merhaba kolay yol tooreduce hello anlık görüntüleri sayısıdır hello son parametre kümesi too5 ile toorun hello komut dosyası:
```
./azure_hana_backup.pl lhanad01 customer 5
```
Bu ayar ile çalışan hello betik sonucunda hello anlık görüntüler, anlık görüntü, hello yeni depolama alanı ile birlikte sayısıdır _5_.

 >[!NOTE]
 > Yalnızca hello en son önceki anlık görüntünün birden fazla bir saat öncesine ise bu komut dosyası anlık görüntüleri hello sayısını azaltır. Merhaba betik değerinden bir saat öncesine anlık görüntüleri silmez.

Bu kısıtlamalar sunulan ilgili toohello isteğe bağlı olağanüstü durum kurtarma işlevselliği ' dir.

Toomaintain Bu önek ile anlık görüntü kümesi artık istemiyorsanız hello komut dosyasıyla yürütebilir _0_ Bu önek eşleştirme tüm anlık görüntüleri tooremove hello bekletme sayı olarak. Ancak, tüm anlık görüntüleri kaldırma olağanüstü durum kurtarma hello yeteneklerini etkileyebilir.

### <a name="recovering-toohello-most-recent-hana-snapshot"></a>Toohello en son HANA anlık görüntü kurtarma

Merhaba olayda karşılaştığınız bir üretim aşağı senaryo, bir depolama anlık görüntüden kurtarma işleminin hello müşterilerde SAP HANA Azure Hizmet Yönetimi ile olarak başlatılabilir. Veriler tooretrieve hello verilerdir toorestore hello üretim veritabanını bir üretim sistem ve hello yalnızca şekilde silindiyse beklenmeyen bir senaryo yüksek aciliyet sağlasa da olabilir.

Merhaba diğer yandan, zaman içinde nokta kurtarma düşük aciliyet olabilir ve önceden gün planlı. Yüksek öncelikli sorunu oluşturma yerine, bu kurtarma SAP HANA ile Azure Hizmet Yönetimi planlayabilirsiniz. Örneğin, tootry hello SAP yazılım yükseltmesini yeni bir geliştirme paketi ve uygulayarak planlama sonra toorevert hello EHP yükseltmeden önce hello durumunu temsil eden tooa anlık görüntü geri.

Merhaba isteği gönderin önce bazı hazırlık toodo gerekir. SAP HANA Azure Hizmet Yönetimi ekipteki sonra hello isteği işlemek ve geri hello birimleri sağlayın. Daha sonra tooyou toorestore hello HANA veritabanına hello anlık görüntü tabanlı çalışıyor. İşte nasıl hello tooprepare iste:

>[!NOTE]
>Kullanıcı arabirimi, ekran görüntüleri, kullanmakta olduğunuz SAP HANA yayın hello bağlı olarak aşağıdaki hello kadar değişiklik gösterebilir.

1. Hangi anlık görüntü toorestore karar verin. Aksi takdirde belirtmediği sürece yalnızca hello hana/veri birimi geri.

2. Merhaba HANA örneği kapatın.

 ![Merhaba HANA örneği Kapat](./media/hana-overview-high-availability-disaster-recovery/image7-shutdown-hana.png)

3. Merhaba veri birimleri her HANA veritabanına düğümde çıkarın. Merhaba veri birimleri kaldırılan değilse hello anlık görüntüsünün hello geri yükleme başarısız olur.

 ![Her HANA veritabanına düğümde Hello veri birimleri çıkarın](./media/hana-overview-high-availability-disaster-recovery/image8-unmount-data-volumes.png)

4. Bir Azure destek isteği tooinstruct hello belirli bir anlık görüntüye geri açın.

 - Merhaba geri yükleme sırasında: SAP HANA Azure Hizmet Yönetimi, tooattend hiçbir veri kaybı konferans tooensure isteyebilir.

 - Merhaba geri yükleme sonrasında: SAP HANA Azure hizmet yönetimi hakkında sizi uyarır hello depolama anlık görüntü geri olduğunda.

5. Merhaba geri yükleme işlemi tamamlandıktan sonra tüm veri birimleri yeniden bağlayın.

 ![Tüm veri birimleri yeniden bağlayın](./media/hana-overview-high-availability-disaster-recovery/image9-remount-data-volumes.png)

6. SAP HANA Studio aracılığıyla tooHANA DB bağlandığınızda bunlar otomatik olarak değil oluşturduysanız SAP HANA Studio'dan kurtarma seçeneklerini seçin. Merhaba aşağıdaki örnekte bir geri yükleme toohello son HANA anlık gösterir. Bir HANA anlık görüntü depolama anlık görüntü eklemeleri ve toohello en son depolama anlık görüntü geri yüklüyorsanız, hello en son HANA anlık görüntü olmalıdır. (Tooolder depolama anlık görüntüleri geri yüklüyorsanız, toolocate gereken hello HANA anlık görüntü hello hello depolama anlık görüntü üzerinde temel alındığı.)

 ![SAP HANA Studio içinde kurtarma seçeneklerini seçin](./media/hana-overview-high-availability-disaster-recovery/image10-recover-options-a.png)

7. Seçin **Kurtar hello veritabanı tooa belirli veri yedekleme depolama anlık görüntü veya**.

 ![Merhaba "Kurtarma türünü belirtin" penceresi](./media/hana-overview-high-availability-disaster-recovery/image11-recover-options-b.png)

8. Seçin **belirt yedekleme kataloğu olmadan**.

 ![Merhaba "Yedekleme konumu belirtin" penceresi](./media/hana-overview-high-availability-disaster-recovery/image12-recover-options-c.png)

9. Merhaba, **hedef türü** listesinde **anlık görüntü**.

 ![Merhaba "Belirt hello yedekleme tooRecover" penceresi](./media/hana-overview-high-availability-disaster-recovery/image13-recover-options-d.png)

10. Tıklatın **son** toostart hello kurtarma işlemi.

 ![Toostart hello kurtarma işlemi "Bitir"'ı tıklatın](./media/hana-overview-high-availability-disaster-recovery/image14-recover-options-e.png)

11. Merhaba HANA veritabanına geri yüklenir ve hello depolama anlık görüntüsüne dahil toohello HANA anlık görüntü kurtarıldı.

 ![HANA veritabanına geri yüklenen ve kurtarılan toohello HANA anlık görüntüsüdür](./media/hana-overview-high-availability-disaster-recovery/image15-recover-options-f.png)

### <a name="recovering-toohello-most-recent-state"></a>Toohello en son durumunu kurtarma

Merhaba aşağıdaki süreci hello depolama anlık görüntüsüne dahil hello HANA anlık görüntü geri yükler. Ardından, hello depolama anlık görüntü geri yüklemeden önce hello işlem günlüğü yedeklemeleri toohello en son hello veritabanının durumu da yükler.

>[!IMPORTANT]
>Devam etmeden önce işlem günlüğü yedeklemeleri tam ve bitişik zincirine sahip olduğunuzdan emin olun. Bu yedeklemeler hello veritabanının geçerli durumu hello geri yükleyemezsiniz.

1. "Kurtarma toohello en son HANA anlık." yordamdan önceki hello 1-6 adımlarını tamamlamanız

2. Seçin **kurtarmak hello veritabanı tooits en son durumunu**.

 !["Hello veritabanı tooits en son durumunu kurtarmak" seçin](./media/hana-overview-high-availability-disaster-recovery/image16-recover-database-a.png)

3. Merhaba en son HANA günlük yedeklerini Hello konumunu belirtin. Başlangıç konumu toocontain hello HANA anlık görüntü toohello en son durumundaki tüm HANA işlem günlüğü yedeklemeleri gerekir.

 ![Merhaba en son HANA günlük yedeklerini Hello konumunu belirtin](./media/hana-overview-high-availability-disaster-recovery/image17-recover-database-b.png)

4. Hangi toorecover hello veritabanından temel olarak bir yedek seçin. Bizim örneğimizde, bu hello depolama anlık görüntüsüne dahil hello HANA anlık görüntüsüdür. (Yalnızca bir anlık görüntü ekran aşağıdaki hello listelenir.)

 ![Hangi toorecover hello veritabanından temel olarak bir yedek seçin.](./media/hana-overview-high-availability-disaster-recovery/image18-recover-database-c.png)

5. Clear hello **kullanım değişim yedeklemeleri** hello HANA anlık görüntü başlangıç saati ve hello en son durum farkları yoksa, kutuyu.

 ![Hiçbir farkları varsa Temizle hello "Kullanım Delta yedekler" onay kutusu](./media/hana-overview-high-availability-disaster-recovery/image19-recover-database-d.png)

6. Merhaba Özet ekranında tıklatın **son** toostart hello geri yükleme yordamı.

 !["Bitir" Merhaba Özet ekranında'ı tıklatın.](./media/hana-overview-high-availability-disaster-recovery/image20-recover-database-e.png)

### <a name="recovering-tooanother-point-in-time"></a>Kurtarma tooanother noktaya
Merhaba HANA anlık görüntü (Merhaba depolama anlık görüntüsüne dahil) arasındaki hello HANA zaman içinde nokta kurtarma anlık görüntüsünü daha sonraki bir zamanda toorecover tooa noktası hello aşağıdaki:

1. Tüm işlem günlüğü yedeklemeleri zamandan toorecover istediğiniz hello HANA anlık görüntü toohello sahip olduğunuzdan emin olun.
2. Begin hello yordamı altında "Kurtarma toohello en son durumu."
3. Merhaba yordamda hello 2. adımda **kurtarma türünü belirtin** penceresinde, seçin **Kurtar hello veritabanı toohello aşağıdaki nokta**hello noktası süresini belirtin ve ardından 3-6 adımlarını tamamlayın.

## <a name="monitoring-hello-execution-of-snapshots"></a>Anlık görüntü Hello yürütme izleme

Depolama anlık görüntüleri toomonitor hello yürütülmesi gerekir. Depolama anlık görüntü yürütür hello betik çıktı tooa dosyasına yazar ve toohello kaydeder hello Perl betikleri aynı konumda. Her anlık görüntü için ayrı bir dosyaya yazılır. her dosyanın Hello çıktı hello hello anlık görüntü betiği yürüten çeşitli aşamaları açıkça gösterir:

- Bir anlık görüntü toocreate gereksinim hello birimleri bulma
- Bu birimlerden gerçekleştirilecek hello anlık görüntüleri bulma
- Nihai varolan anlık görüntüleri toomatch hello belirttiğiniz anlık görüntü sayısı silme
- HANA anlık görüntü oluşturma
- Merhaba birimler üzerinde Hello depolama anlık görüntü oluşturma
- Merhaba HANA anlık görüntü silme
- En son Hello çok anlık görüntü yeniden adlandırma**.0**

Merhaba en önemli hello betik bu parçasıdır:
```
**********************Creating HANA snapshot**********************
Creating hello HANA snapshot with command: "./hdbsql -n localhost -i 01 -U SCADMIN01 "backup data create snapshot"" ...
HANA snapshot created successfully.
**********************Creating Storage snapshot**********************
Taking snapshot hourly.recent for hana_data_lhanad01_t020_vol ...
Snapshot created successfully.
Taking snapshot hourly.recent for hana_log_backup_lhanad01_t020_vol ...
Snapshot created successfully.
Taking snapshot hourly.recent for hana_log_lhanad01_t020_vol ...
Snapshot created successfully.
Taking snapshot hourly.recent for hana_shared_lhanad01_t020_vol ...
Snapshot created successfully.
Taking snapshot hourly.recent for sapmnt_lhanad01_t020_vol ...
Snapshot created successfully.
**********************Deleting HANA snapshot**********************
Deleting hello HANA snapshot with command: "./hdbsql -n localhost -i 01 -U SCADMIN01 "backup data drop snapshot"" ...
HANA snapshot deletion successfully.
```
Bu örnekten nasıl hello betik kayıtları oluşturma hello HANA anlık görüntüsünün hello görebilirsiniz. Merhaba genişleme durumda hello ana düğüm üzerinde bu işlemi başlatılır. Merhaba ana düğüm hello zaman uyumlu hello anlık görüntülerin her hello çalışan düğümleri oluşturulmasını başlatır. Ardından hello depolama anlık görüntü alınır. Merhaba aktarılmadığı hello depolama anlık görüntüleri sonra hello HANA anlık görüntü silinir.
