---
title: "Microsoft Azure üzerinde aaaOracle çözümleri | Microsoft Docs"
description: "Desteklenen yapılandırmalar ve Oracle çözümlerinin Microsoft Azure ile ilgili sınırlamalar hakkında bilgi edinin."
services: virtual-machines-linux
documentationcenter: 
manager: timlt
author: rickstercdn
tags: azure-resource-management
ms.assetid: 5d71886b-463a-43ae-b61f-35c6fc9bae25
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 06/15/2017
ms.author: rclaus
ms.openlocfilehash: 54dc62e76129535da7fb6f131af90c83adfec6cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="oracle-solutions-and-their-deployment-on-microsoft-azure"></a>Oracle çözümleri ve Microsoft Azure üzerinde dağıtım
Bu makalede gerekli toosuccesfully dağıtmak çeşitli Oracle çözümleri Microsoft Azure ile ilgili bilgiler içerir. Bu çözüm sanal makine görüntülerini hello Azure Marketi Oracle tarafından yayımlanan dayanır. tooget listesini şu anda kullanılabilir görüntülerinin hello aşağıdaki komutu çalıştırın:
```azurecli-interactive
az vm image list --publisher oracle -o table --all
```
6 16 2017 hello görüntülerin listesi itibariyle hello şunlardır:
```bash
Offer                   Publisher    Sku                     Urn                                                          Version
----------------------  -----------  ----------------------  -----------------------------------------------------------  -------------
Oracle-Database-Ee      Oracle       12.1.0.2                Oracle:Oracle-Database-Ee:12.1.0.2:12.1.20170202             12.1.20170202
Oracle-Database-Se      Oracle       12.1.0.2                Oracle:Oracle-Database-Se:12.1.0.2:12.1.20170202             12.1.20170202
Oracle-Linux            Oracle       6.4                     Oracle:Oracle-Linux:6.4:6.4.20141206                         6.4.20141206
Oracle-Linux            Oracle       6.7                     Oracle:Oracle-Linux:6.7:6.7.20161007                         6.7.20161007
Oracle-Linux            Oracle       6.8                     Oracle:Oracle-Linux:6.8:6.8.20161020                         6.8.20161020
Oracle-Linux            Oracle       6.9                     Oracle:Oracle-Linux:6.9:6.9.20170406                         6.9.20170406
Oracle-Linux            Oracle       7.0                     Oracle:Oracle-Linux:7.0:7.0.20141217                         7.0.20141217
Oracle-Linux            Oracle       7.2                     Oracle:Oracle-Linux:7.2:7.2.20161020                         7.2.20161020
Oracle-Linux            Oracle       7.3                     Oracle:Oracle-Linux:7.3:7.3.20170320                         7.3.20170320
Oracle-WebLogic-Server  Oracle       Oracle-WebLogic-Server  Oracle:Oracle-WebLogic-Server:Oracle-WebLogic-Server:12.1.2  12.1.2
```

Bu görüntüler "Kendi lisansını getir" olarak kabul edilir ve bu nedenle, yalnızca işlem, depolama ve ağ maliyetlerini VM çalıştırarak ücrete ücretlendirilir.  Doğru lisanslı toouse Oracle yazılımlardır ve Oracle ile yerinde geçerli bir destek sözleşmesi sahip varsayılır. Oracle şirket içi tooAzure lisans taşınabilirliği garanti. Yayımlanan hello bkz [Oracle ve Microsoft](http://www.oracle.com/technetwork/topics/cloud/faq-1963009.html) lisans taşınabilirliği hakkında ayrıntılı bilgi için unutmayın. 

Kişiler çözümleri Azure sıfırdan oluşturabilir veya özel bir şirket içi ortamlarını görüntülerden karşıya özel görüntülerinde toobase tercih edebilirsiniz.

## <a name="support-for-jd-edwards"></a>JD Edirneli desteği
TooOracle destek Not göre [belge kimliği 2178595.1](https://support.oracle.com/epmos/faces/DocumentDisplay?_afrLoop=573435677515785&id=2178595.1&_afrWindowMode=0&_adf.ctrl-state=o852dw7d_4) , JD Edirneli EnterpriseOne verions 9.2 ve üzerinde yukarıdaki desteklenen **tüm genel bulut teklifi** kendi özel karşılayan `Minimum Technical Requirements` (MTR).  İşletim sistemi ve yazılım uygulama uyumluluğu için kendi MTR belirtimlere toocreate özel resimler gerekir. 

## <a name="oracle-database-virtual-machine-images"></a>Oracle veritabanı sanal makine görüntüleri
Oracle, Oracle Linux tabanlı sanal makine görüntüleri, Azure'da çalışan Oracle DB 12,1 Standard ve Enterprise sürümleri destekler.  Hello Azure üzerinde Oracle DB, üretim iş yükleri için en iyi performans, emin tooproperly boyutu hello VM görüntüsü olması ve Premium Depolama tarafından yedeklenen yönetilen diskleri kullanın. Yönergeler için tooquickly nereden bir Oracle DB hazır ve çalışır, hello Oracle kullanarak Azure VM görüntüsü, yayımlanan [hello Oracle DB Hızlı Başlangıç Kılavuzu deneyin](oracle-database-quick-create.md).

### <a name="attached-disk-configuration-options"></a>Ekli disk yapılandırma seçenekleri

Bağlı disklerde hello Azure Blob Depolama hizmetinin üzerinde kullanır. Her standart disk (IOPS) saniyede yaklaşık 500 giriş/çıkış işlemlerinin teorik maksimum yeteneğine sahiptir. Bizim premium disk sunumu, yüksek performanslı veritabanı iş yükleri için tercih edilir ve disk başına too5000 IOPS yukarı elde edebilirsiniz. Kullanabilirsiniz ancak performansınızı karşılayan tek bir disk gerekir - birden çok ekli disk kullanıyorsanız, veritabanı veri bunları yayılan ve Oracle otomatik Depolama Yönetimi (ASM) kullanmak hello etkili IOPS performansını iyileştirebilir. Bkz: [Oracle otomatik depolama genel bakış](http://www.oracle.com/technetwork/database/index-100339.html) daha fazla Oracle ASM belirli bilgiler için. Bir örnek için nasıl tooinstall ve Oracle ASM bir Linux Azure VM'de yapılandırma - hello deneyebilirsiniz [yükleme ve Oracle otomatik Depolama Yönetimi yapılandırma](configure-oracle-asm.md) Öğreticisi.

### <a name="oracle-realtime-application-cluster-rac"></a>Oracle gerçek zamanlı uygulama küme (RAC)
Oracle RAC tasarlanmış toomitigate hello tek bir düğümün bir şirket içi çok düğümlü bir küme yapılandırmasında hatasıdır.  Yerel toohyper ölçekli genel bulut ortamlarında değil olan iki şirket içi teknolojilerini kullanır: ağ çok noktaya yayın ve paylaşılan disk. Üçüncü taraf çözümleri şirketler tarafından oluşturulan vardır [FlashGrid gibi](https://www.flashgrid.io/oracle-rac-in-azure/) , öykünmek bu teknolojiler toodeploy Oracle RAC Azure gerekiyorsa. 

### <a name="high-availability-and-disaster-recovery-considerations"></a>Yüksek kullanılabilirlik ve olağanüstü durum kurtarma değerlendirmeleri
Oracle veritabanları Azure'da kullanırken, bir yüksek kullanılabilirlik ve olağanüstü durum kurtarma çözümü tooavoid kapalı kalma süresi uygulamak için sorumlu. 

Itanium tabanlı sistemler için Oracle veritabanı Enterprise Edition (RAC) olmadan Azure üzerinde için yüksek kullanılabilirlik ve olağanüstü durum kurtarma elde edilebilir kullanarak [veri koruma, etkin Data Guard](http://www.oracle.com/technetwork/articles/oem/dataguardoverview-083155.html), veya [Oracle Golden kapısı](http://www.oracle.com/technetwork/middleware/goldengate), iki veritabanlarında iki ayrı sanal makineler. Her iki sanal makine olması içinde hello aynı [sanal ağ](https://azure.microsoft.com/documentation/services/virtual-network/) bunlar erişebilir birbirine hello özel kalıcı bir IP adresi tooensure.  Ayrıca, hello sanal makine yerleştirme öneririz hello tooallow Azure tooplace aynı kullanılabilirlik kümesi bunları ayrı hata etki alanları ve yükseltme etki alanı.  Toohave coğrafi yedeklilik - isterseniz, bu iki veritabanı arasında iki farklı bölgelerde çoğaltabilir ve bir VPN ağ geçidi ile Merhaba iki örneği bağlanmak olabilir.

Bir öğretici sahip olduğumuz "[uygulama Oracle DataGuard azure'da](configure-oracle-dataguard.md)" hangi anlatılmaktadır, hello temel kurulum yordamı tootrial bu Azure üzerinde.  

Oracle Data Guard ile yüksek oranda kullanılabilir bir sanal makine, başka bir sanal makine, ikincil (bekleme) veritabanında birincil veritabanı ile elde edilebilir ve tek yönlü çoğaltma aralarında ayarlayın. Merhaba, okuma erişimi toohello hello veritabanının kopyasını sonucudur. Oracle GoldenGate ile Merhaba iki veritabanı arasında iki yönlü çoğaltma yapılandırabilirsiniz. Bu araçları kullanarak veritabanlarınız için yüksek kullanılabilirlik çözümü kurma tooset nasıl görürüm toolearn [etkin Data Guard](http://www.oracle.com/technetwork/database/features/availability/data-guard-documentation-152848.html) ve [GoldenGate](http://docs.oracle.com/goldengate/1212/gg-winux/index.html) hello Oracle Web sitesindeki belgeleri. Okuma-yazma erişimi toohello hello veritabanının kopyasını gereksinim duyarsanız, kullanabileceğiniz [Oracle etkin Data Guard](http://www.oracle.com/uk/products/database/options/active-data-guard/overview/index.html).

Bir öğretici sahip olduğumuz "[uygulama Oracle GoldenGate azure'da](configure-oracle-golden-gate.md)" hangi anlatılmaktadır, hello temel seup yordamı tootrial bu Azure üzerinde.

Azure'da tasarlanmış bir HA ve DR çözümü sahip olmasına rağmen bir yedekleme stratejisi veritabanınız yer toorestore sahip tooensure isteyeceksiniz.  Bir öğretici sahibiz [yedekleme ve kurtarma Oracle veritabanına](oracle-backup-recovery.md) hangi kılavuzluk, consistant yedekleme oluşturma için hello temel yordamı.

## <a name="oracle-weblogic-server-virtual-machine-images"></a>Oracle WebLogic Server sanal makine görüntüleri
* **Kümeleme Enterprise Edition'da yalnızca desteklenir.** Lisansına sahip olduğunuz toouse WebLogic yalnızca kullanırken kümeleme hello WebLogic Server, Enterprise sürümü. WebLogic Server Standard Edition ile kümeleme kullanmayın.
* **Çok noktaya yayın UDP desteklenmiyor.** Azure UDP tek, ancak çok noktaya yayın veya yayın destekler. WebLogic, üzerinde Azure UDP tek noktaya yayın yetenekleri mümkün toorely sunucusudur. En iyi sonuçları, UDP tek noktaya yayın üzerinde bağlı olan hello WebLogic küme boyutu statik tutulması önerilir için veya hello kümeye dahil en fazla 10 yönetilen sunucularla tutulmalıdır.
* **WebLogic Server ortak ve özel bağlantı noktaları toobe hello T3 için aynı (örneğin, Kurumsal JavaBeans kullanırken) erişim bekliyor.** Adlı vNet içindeki iki veya daha fazla VM oluşan bir WebLogic Server kümesinde bir hizmet Katmanı (EJB) uygulaması çalıştığı bir çok katmanlı senaryoyu düşünün **SLWLS**. Merhaba istemci katmanı olan hello farklı bir alt ağ toocall EJB hello hizmet katmanında çalışan basit bir Java program çalıştıran aynı sanal ağı. Gerekli tooload Bakiye hello hizmet katmanı olduğu için ortak bir yük dengeli uç nokta hello WebLogic Server küme hello sanal makineler için oluşturulan toobe gerekir. Belirttiğiniz hello özel bağlantı noktası hello ortak bağlantı noktasını (örneğin, 7006:7008) farklı olması durumunda hello aşağıdaki gibi bir hata oluşur:

       [java] javax.naming.CommunicationException [Root exception is java.net.ConnectException: t3://example.cloudapp.net:7006:

       Bootstrap to: example.cloudapp.net/138.91.142.178:7006' over: 't3' got an error or timed out]

   Bu herhangi T3, uzaktan erişim için WebLogic Server hello yük dengeleyici bağlantı noktası bekler ve hello yönetilen WebLogic server bağlantı noktası toobe aynı hello kaynaklanır. Merhaba çalışması üstüne Merhaba istemci bağlantı noktası 7006 (Merhaba yük dengeleyici bağlantı noktası) erişme ve hello yönetilen sunucu 7008 (Merhaba özel bağlantı noktası) üzerinde dinleme. Bu kısıtlama, yalnızca T3 erişimi için değil HTTP geçerlidir.

   tooavoid Bu sorun, geçici çözümler aşağıdaki hello birini kullanın:

  * Kullanım hello aynı özel ve ayrılmış uç noktaları tooT3 erişim genel bağlantı noktası numaralarını yük dengeli.
  * WebLogic Server başlatırken JVM parametresi aşağıdaki hello şunları içerir:

         -Dweblogic.rjvm.enableprotocolswitch=true

İlgili bilgi için bkz. KB makalesi **860340.1** adresindeki <http://support.oracle.com>.

* **Dinamik Kümeleme ve sınırlamaları Yük Dengeleme.** Toouse WebLogic Server dinamik bir kümede istediğiniz ve bir tek, ortak yük dengeli uç nokta Azure üzerinden kullanıma varsayalım. Her hello yönetilen sunucular (bir aralığından dinamik olarak atanır) ve yönetilen sunucular daha hello Yöneticisi izleme makineler çok başlatılmaz için sabit bağlantı noktası numarası kullandığınız sürece bu yapılabilir (diğer bir deyişle, birden fazla sunucu başına sanal Küp Str yönetilen ual makine). Sanal makineler çok başlatılmakta daha fazla WebLogic sunucuları yapılandırmanızı sonuçları (diğer bir deyişle, burada birden çok WebLogic sunucu örnekleri paylaşımı hello aynı sanal makine), birden fazla WebLogic Server bu örnekleri için mümkün değildir sunucuları toobind tooa verilen bağlantı noktası numarası – hello diğerlerinin bu sanal makinedeki başarısız olur.

   Merhaba üzerinde hello yönetim sunucusu tooautomatically yapılandırırsanız, diğer yandan, Ata benzersiz bağlantı noktası numaraları tooits yönetilen sunucuları, olduğu gibi Azure bir tek genel bağlantı noktası toomultiple özel bağlantı noktalarından eşleme desteklemediği için Yük Dengeleme mümkün değildir Bu yapılandırma için gerekli.
* **Bir sanal makinede Weblogic Server birden çok örneği.** Dağıtımınızın gereksinimlerine bağlı olarak, birden çok örneğini WebLogic Server hello üzerinde çalışan hello seçeneği düşünebilirsiniz aynı sanal hello sanal makine büyüklükte ise makine. Örneğin, bir orta büyüklükte sanal iki çekirdek içeren makinede WebLogic Server'ın iki örneği toorun seçebilir. Ancak hala tek hata noktaları bulundurmaktan WebLogic Server birden çok örneğini çalıştıran tek bir sanal makine kullandıysanız, hello durumda olur, mimariye Tanıtımı kaçının öneririz olduğunu unutmayın. En az iki sanal makineleri kullanarak daha iyi bir yaklaşım olabilir ve bu sanal makinelerin her biri daha sonra WebLogic Server birden çok örneğini çalıştırabilir. Her WebLogic Server'ın bu örnekler, hello parçası olabilir aynı küme. Unutmayın, ancak bunu şu anda olası içinde bu tür WebLogic Server dağıtımlar tarafından sunulan toouse Azure tooload dengele uç noktaları hello aynı sanal makine, Azure yük dengeleyici arasında dağıtılmış hello Yük Dengeleme sunucuları toobe gerektirdiğinden benzersiz sanal makineler.

## <a name="oracle-jdk-virtual-machine-images"></a>Oracle JDK sanal makine görüntüleri
* **JDK 6 ve 7 en son güncelleştirmeleri.** Merhaba son ortak, desteklenen bir sürümü Java (şu anda 8 Java) kullanmanızı öneririz, ancak Azure ayrıca JDK 6 ve 7 görüntüleri kullanılabilir hale getirir. Bu henüz hazır toobe tooJDK 8 yükseltilmemiş olan eski uygulamalar için tasarlanmıştır. Güncelleştirmeleri tooprevious JDK görüntüleri artık kullanılabilir toohello herkes olabilir ancak hello Oracle, hello JDK 6 ve 7 görüntüleri Azure tarafından sağlanan yöneticileriyle olan Microsoft toocontain normalde tarafından sunulan daha yeni bir genel olmayan güncelleştirme yüklenmelidir Oracle tooonly Oracle grubunu seçmek, müşterilerin desteklenen. Yeni sürümler hello JDK görüntülerinin JDK 6 ve 7, güncelleştirilmiş sürümleriyle zamanla kullanıma sunulacaktır.

   Merhaba JDK bu JDK 6 kullanılabilir ve 7 görüntüler ve hello sanal makineler ve kendilerinden türetilmiş görüntüleri yalnızca Azure içinde kullanılabilir.
* **64-bit JDK.** Merhaba Oracle WebLogic Server sanal makine görüntüleri ve Azure tarafından sağlanan hello Oracle JDK sanal makine görüntüleri hello 64 bit sürümleri hem Windows Server hem de hello JDK içerir.

## <a name="next-steps"></a>Sonraki adımlar
Artık Microsoft Azure üzerinde geçerli Oracle çözümleri genel bir bakış vardır. Sonraki adımınız toogo olduğunu ve Azure üzerinde ilk, Oracle veritabanı dağıtın.
- Merhaba deneyin [Azure üzerinde bir Oracle veritabanı oluşturma](oracle-database-quick-create.md) öğretici tooget başlatıldı.
