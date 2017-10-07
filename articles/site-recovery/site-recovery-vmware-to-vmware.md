---
title: "aaaReplicate VMware Vm'lerini veya fiziksel sunucuları tooanother site (Klasik Azure portalı) | Microsoft Docs"
description: "Bu makale tooreplicate VMware Vm'leri veya Windows/Linux fiziksel sunucuları tooa ikincil siteyi Azure Site Recovery ile kullanın."
services: site-recovery
documentationcenter: 
author: nsoneji
manager: jwhit
editor: 
ms.assetid: b2cba944-d3b4-473c-8d97-9945c7eabf63
ms.service: site-recovery
ms.workload: backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: nisoneji
ms.openlocfilehash: 5789ca07f0aa15cf194615fd33103dac930d7b7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-on-premises-vmware-virtual-machines-or-physical-servers-tooa-secondary-site-in-hello-classic-azure-portal"></a>Şirket içi VMware sanal makineleri veya fiziksel sunucuları tooa ikincil site hello Klasik Azure Portalı'nda çoğaltma

## <a name="overview"></a>Genel Bakış
Azure Site kurtarma Inmage Scout şirket içi VMware siteler arasında gerçek zamanlı çoğaltma sağlar. Inmage Scout Azure Site Recovery hizmeti Aboneliklerde dahil edilir. 

## <a name="prerequisites"></a>Ön koşullar
**Azure hesabı**: ihtiyacınız vardır bir [Microsoft Azure](https://azure.microsoft.com/) hesabı. [Ücretsiz deneme sürümüyle](https://azure.microsoft.com/pricing/free-trial/) başlayabilirsiniz. Site Recovery fiyatlandırması hakkında [daha fazla bilgi edinin](https://azure.microsoft.com/pricing/details/site-recovery/).

## <a name="step-1-create-a-vault"></a>1. adım: bir kasa oluşturma
1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Yeni tıklayın > Yönetim > Yedekleme ve Site Kurtarma (OMS). Alternatif olarak, Gözat'ı tıklatabilirsiniz > Kurtarma Hizmetleri kasası > Ekle.
3. İçinde **adı** bir kolay ad tooidentify hello kasası belirtin. Birden fazla aboneliğiniz varsa bunlardan birini seçin.
4. İçinde **kaynak grubu** yeni bir kaynak grubu oluşturun veya varolan bir tanesini seçin. Bir Azure bölgesi toocomplete gerekli alanları belirtin.
5. İçinde **konumu**, hello hello kasa için coğrafi bölgeyi seçin. desteklenen toocheck bölgeler Bkz [Azure Site Recovery fiyatlandırma](https://azure.microsoft.com/pricing/details/site-recovery/).
6. İsterseniz tooquickly erişim hello hello Pano kasadan PIN toodashboard tıklayın ve Oluştur'u tıklatın.
7. Merhaba yeni kasa Panosu hello üzerinde görünür > tüm kaynakları ve üzerinde hello dikey ana kurtarma Hizmetleri kasaları.

## <a name="step-2-configure-hello-vault-and-download-inmage-scout-components"></a>Adım 2: hello kasası yapılandırma ve Inmage Scout bileşenlerini yükle
1. Merhaba kurtarma Hizmetleri kasaları dikey penceresinde kasanızı seçin ve Ayarlar'ı tıklatın.
2. İçinde **ayarları** > **Başlarken** tıklatın **Site Recovery** > 1. adım: **altyapıyı hazırlama**  >  **Koruma hedefi**.
3. İçinde **koruma hedefi** toorecovery site seçin ve VMware vSphere hiper yönetici Evet'i seçin. Daha sonra Tamam'a tıklayın.
4. İçinde **Scout Kurulum**, indirme toodownload Inmage Scout 8.0.1 GA yazılım ve kayıt anahtar'ı tıklatın. Merhaba Kurulum dosyaları için tüm hello bileşenleri hello indirilen .zip dosyasına gereklidir.

## <a name="step-3-install-component-updates"></a>3. adım: bileşen güncelleştirmeleri yükleme
Merhaba hakkında en son okuma [güncelleştirmeleri](#updates). Merhaba güncelleştirme dosyalarını sunucularda sırasının hello yükleyeceksiniz:

1. Varsa RX sunucu
2. Yapılandırma sunucuları
3. İşlem sunucuları
4. Ana hedef sunucusu
5. vContinuum sunucuları
6. Kaynak sunucu (Windows ve Linux sunucusu)

Merhaba güncelleştirmeleri gibi yükleyin:

1. Merhaba karşıdan [güncelleştirme](https://aka.ms/asr-scout-update5) .zip dosyası. Bu .zip dosyası hello aşağıdaki dosyaları içerir:

   * RX_8.0.4.0_GA_Update_4_8725872_16Sep16.Tar.gz
   * CX_Windows_8.0.4.0_GA_Update_4_8725865_14Sep16.exe
   * UA_Windows_8.0.5.0_GA_Update_5_11525802_20Apr17.exe
   * UA_RHEL6 64_8.0.4.0_GA_Update_4_9035261_26Sep16.tar.gz
   * vCon_Windows_8.0.5.0_GA_Update_5_11525767_20Apr17.exe
   * UA update4 BITS RHEL5, OL5, OL6, SUSE 10, SUSE 11: UA_<Linux OS>_8.0.4.0_GA_Update_4_9035261_26Sep16.tar.gz
2. Merhaba .zip dosyalarını ayıklayın.<br>
3. **Merhaba RX sunucusu**: kopyalama **RX_8.0.4.0_GA_Update_4_8725872_16Sep16.tar.gz** toohello RX sunucu ve ayıklayın. Hello klasöründe şunu çalıştırın ayıklanan **/yüklemesi**.<br>
4. **Merhaba yapılandırma sunucusu/işlem sunucusu için**: kopyalama **CX_Windows_8.0.4.0_GA_Update_4_8725865_14Sep16.exe** toohello yapılandırma sunucusu ve işlem sunucusu. Toorun çift tıklayın.<br>
5. **Merhaba Windows ana hedef sunucusu için**: tooupdate hello birleşik aracı, kopya **UA_Windows_8.0.5.0_GA_Update_5_11525802_20Apr17.exe** toohello ana hedef sunucusu. Buna çift tıklayarak toorun onu. Kaynak Update4 güncelleştirilmezse birleşik aracı hello de geçerli toohello kaynak sunucusu olduğunu unutmayın. Bu yanı, hello kaynak sunucuda daha sonra bu listede belirtildiği gibi yüklemeniz gerekir.<br>
6. **Merhaba vContinuum sunucusu**: kopyalama **vCon_Windows_8.0.5.0_GA_Update_5_11525767_20Apr17.exe** toohello vContinuum sunucusu.  Merhaba vContinuum Sihirbazı kapattığınız emin olun. Merhaba dosya toorun üzerinde çift tıklatın.<br>
7. **Merhaba Linux ana hedef sunucusu için**: tooupdate hello birleşik aracı, kopya **UA_RHEL6 64_8.0.4.0_GA_Update_4_9035261_26Sep16.tar.gz** toohello ana hedef sunucusu hem ayıklayın. Hello klasöründe şunu çalıştırın ayıklanan **/yüklemesi**.<br>
8. **Merhaba Windows kaynak sunucu için**: kimlikleri update4 üzerinde ise kaynak tooinstall güncelleştirme 5 aracısında gerekmez. Update4 küçüktür hello güncelleştirme 5 Aracısı uygulayın.
tooupdate hello birleşik aracı, kopya **UA_Windows_8.0.5.0_GA_Update_5_11525802_20Apr17.exe** toohello kaynak sunucu. Buna çift tıklayarak toorun onu. <br>
9. **Merhaba Linux kaynak sunucu için**: tooupdate hello birleşik aracı, UA dosya toohello Linux sunucusu söz konusu sürümü kopyalamak ve ayıklayın. Hello klasöründe şunu çalıştırın ayıklanan **/yüklemesi**.  Örnek: RHEL 6,7 64 bit sunucu için kopyalama **UA_RHEL6 64_8.0.4.0_GA_Update_4_9035261_26Sep16.tar.gz** toohello sunucu ve ayıklayın. Hello klasöründe şunu çalıştırın ayıklanan **/yüklemesi**.

## <a name="step-4-set-up-replication"></a>4. adım: Çoğaltmayı ayarlama
1. Siteler arasında hello kaynak ve hedef VMware çoğaltma ayarlayın.
2. Yönergeler için hello indirilir Inmage Scout belgelerine hello ürünle birlikte kullanın. Alternatif olarak, aşağıdaki gibi hello belgelere erişebilir:

   * [Sürüm notları](https://aka.ms/asr-scout-release-notes)
   * [Uyumluluk matrisi](https://aka.ms/asr-scout-cm)
   * [Kullanıcı Kılavuzu](https://aka.ms/asr-scout-user-guide)
   * [RX Kullanıcı Kılavuzu](https://aka.ms/asr-scout-rx-user-guide)
   * [Hızlı Yükleme Kılavuzu](https://aka.ms/asr-scout-quick-install-guide)

## <a name="updates"></a>Güncellemeler
### <a name="azure-site-recovery-scout-801-update-5"></a>Azure Site Recovery Scout 8.0.1 güncelleştirme 5
Scout güncelleştirme 5 birikmeli bir güncelleştirmedir. Update1 update4 ve yeni hata düzeltmeleri ve geliştirmeler aşağıdaki kasa tüm hello düzeltmelerini sahiptir.
ASR Scout update4 tooupdate5 eklenen düzeltmeler belirli tooMaster hedef ve vContinuum bileşenleridir. Tüm kaynak sunucularınız, ana hedef, yapılandırma sunucusu, işlem sunucusu ve RX zaten ASR Scout update4 üzerinde sonra kullanıyorsanız tooapply güncelleştirme 5 yalnızca ana hedef sunucusundaki. 

**Yeni platform desteği**
* SUSE Linux Enterprise Server 11 hizmet paketi 4(SP4)

> [!NOTE]
> SLES 11 SP4 64 bit **InMage_UA_8.0.1.0_SLES11-SP4-64_GA_13Apr2017_release.tar.gz** temel Scout GA paketi ile birlikte paketlenmiştir **InMage_Scout_Standard_8.0.1 GA.zip**. Bölümünde belirtildiği gibi portaldan Scout GA paketini indirin [1. adım](#step-1-create-a-vault).
>

**Hata düzeltmeleri ve geliştirmeleri**

* Windows Küme destek güvenilirliğini artırmak
    * Sabit-süre hello P2V MSCS bazıları hale küme disklerine RAW kurtarma işleminden sonra
    * Fixed-P2V MSCS küme kurtarma toodisk sipariş uyuşmazlığı başarısız oluyor
    * Fixed-MSCS kümesindeki ile disk boyutu uyumsuzluğu işlem başarısız diskleri ekleme
    * RDM LUN'ları eşleme hazırlık denetimi ile fixed-kaynak MSCS küme boyutu doğrulama başarısız
    * Fixed-tek bir düğümün küme koruma tooSCSI uyumsuzluğu sorunu başarısız oluyor 
    * Hedef küme diskleri mevcut olup olmadığını Fixed-yeniden koruma hello P2V Windows Küme sunucusu başarısız olur. 
    
* Seçili MT üzerinde değilse, hello kaynak makine (iletme koruma sırasında), vContinuum hello yanlış MT geri dönme Kurtarma sırasında seçer ve daha sonra kurtarma işlemi başarısız korumalı olarak geri dönme koruma sırasında aynı ESXi sunucusunda hello.

> [!NOTE]
> 
> * P2V küme düzeltmeleri geçerli tooonly istemcinin ASR Scout update5 ile korunan bu fiziksel MSCS kümelerdir. tooavail hello küme düzeltmeleri hello üzerinde zaten korumalı daha eski güncelleştirmeler ile P2V MSCS kümesindeki, 12 hello bölümünde açıklanan toofollow hello yükseltme adımları gerekir, yükseltme, P2V MSCS küme tooScout Update5 korumalı [ASR Scout sürüm Notlar](https://aka.ms/asr-scout-release-notes).
> 
> * Yeniden koruma fiziksel MSCS kümesindeki var olan hedef disklerin yalnızca zamanında hello yeniden koruma, hello diskleri aynı kümesini her hello küme düğümleri ilk defa oldukları gibi korunan etkin değilse yeniden kullanabilirsiniz. Değil, daha sonra el ile adımlar varsa, 12 bölümünde belirtildiği gibi [ASR Scout sürüm notları](https://aka.ms/asr-scout-release-notes) çok hello hedef tarafı diskleri toohello doğru veri deposu yolu toore kullanımı taşıma yeniden koruma sırasında bunları. Yükseltme adımlarını uymadan hello MSCS kümesindeki P2V modunda koruyun, bunu yeni bir disk hello hedef ESXi sunucusunda oluşturur. Toomanually delete hello eski disklerden hello veri deposu gerekir.
> 
> * Her SLES11 kaynağı veya herhangi bir hizmet paketi sunucu SLES11 düzgün biçimde yeniden sonra bir el ile işaretleme hello **kök** CX kullanıcı Arabiriminde bildirilmez gibi yeniden eşitlemek için çoğaltma çiftleri disk. Bunu yapmazsanız ' işareti hello kök disk için yeniden eşitleme, veri bütünlüğü (dı) sorunları görebilirsiniz.
> 

### <a name="azure-site-recovery-scout-801-update-4"></a>Azure Site Recovery Scout 8.0.1 güncelleştirme 4
Scout güncelleştirme 4 birikmeli bir güncelleştirmedir. Update1 update3 ve yeni hata düzeltmeleri ve geliştirmeler aşağıdaki kasa tüm hello düzeltmelerini sahiptir.

**Yeni platform desteği**

* VCenter/vSphere için 6.0, 6.1 ve 6.2 desteği eklendi
* Aşağıdaki Linux işletim sistemleri için destek eklenmiştir
  * Red Hat Enterprise Linux (RHEL) 7.0, 7.1 ve 7.2
  * CentOS 7.0, 7.1 ve 7.2
  * Red Hat Enterprise Linux (RHEL) 6,8
  * CentOS 6,8

> [!NOTE]
> RHEL/CentOS 7 64-bit **InMage_UA_8.0.1.0_RHEL7-64_GA_06Oct2016_release.tar.gz** temel Scout GA paketi ile birlikte paketlenmiştir **InMage_Scout_Standard_8.0.1 GA.zip**. Bölümünde belirtildiği gibi portaldan Scout GA paketini indirin [1. adım](#step-1-create-a-vault).
>
>

**Hata düzeltmeleri ve geliştirmeleri**

* Geliştirilmiş kapatma yeniden eşitleme istenmeyen sorunları aşağıdaki Linux İşletim Sistemleri'ni ve klonlar tooprevent için işleme.
  * Red Hat Enterprise Linux (RHEL) 6.x
  * Oracle Linux (OL) 6.x
* Linux için yalnızca toohello yerel kullanıcı izinleri birleşik aracı yükleme dizini içinde sunulmuştur klasörün tam erişim kısıtlı.
* Windows üzerinde yerel olarak ortak dağıtılmış tutarlılık işareti yoğun olarak sertifika veren çalışırken zaman aşımına sorunu SQL ve Share Point kümeleri gibi dağıtılmış uygulamalar yüklendi.
* Eklenen günlük CX temel yükleyici düzeltme ilgili.
* VMware vCLI 6.0 indirme bağlantısı tooWindows ana hedef temel yükleyici eklenir.
* Daha fazla denetim ve ağ yapılandırmaları değişiklikleri günlüklerinde yük devretme ve DR ayrıntısına sırasında eklendi.
* Süre bekletme bilgileri bildirilen toohello CX değil.  
* Kaynak birim küçültme oluştuğunda fiziksel küme için birim vContinuum Sihirbazı aracılığıyla yeniden boyutlandır işlemi başarısız oluyor.
* Küme korumayı "Başarısız toofind hello disk imzasını" hatasıyla başarısız oldu küme diski PRDM disk olduğunda.
* cxps aralık dışı özel durum nedeniyle sunucu kilitlenme taşıma.
* Sunucu adı ve IP sütunları şimdi anında yükleme sihirbazının sayfasında vContinuum yeniden boyutlandırılabilir.
* RX API'si geliştirmeleri
  * Beş en son kullanılabilir ortak tutarlılık noktası (yalnızca garanti etiketleri) sağlar.
  * Kapasite ve boş alan ayrıntıları tüm korumalı cihazların Merhaba sağlar.
  * Kaynak sunucuda Scout sürücü durumunu sağlar.

> [!NOTE]
> * **InMage_Scout_Standard_8.0.1_GA.zip** temel paket şimdi güncelleştirdi CX temel yükleyici **InMage_CX_8.0.1.0_Windows_GA_26Feb2015_release.exe** ve Windows ana hedef temel yükleyici **InMage_ Scout_vContinuum_MT_8.0.1.0_Windows_GA_26Feb2015_release.exe**. Tüm yeni yükleme için yeni CX ve Windows ana hedef GA BITS hizmetini kullanın.
> * Güncelleştirme 4 8.0.1 üzerinde doğrudan da uygulanabilir İST
> * Merhaba sistemde uygulanmasıyla geri sonra hello yapılandırma sunucusu ve RX güncelleştirmeleri alınamaz.
>
>

### <a name="azure-site-recovery-scout-801-update-3"></a>Azure Site Recovery Scout 8.0.1 güncelleştirme 3
Güncelleştirme 3 hello aşağıdakileri içeren hata düzeltmeleri ve geliştirmeler:

* Merhaba proxy'nin arkasında olduğunuzda hello yapılandırma sunucusu ve RX tooregister toohello Site Recovery kasası başarısız.
* Merhaba kurtarma noktası hedefi (RPO) hello saat sayısını karşılanmaması hello sistem durumu raporu güncelleştirilmiyor.
* Ağ ayrıntıları veya Hello ESX donanım ayrıntıları tüm UTF-8 karakterler içeriyorsa hello yapılandırma sunucusu ile RX eşitlemiyor.
* Windows Server 2008 R2 etki alanı denetleyicileri tooboot sonra kurtarma başarısız.
* Çevrimdışı eşitleme beklendiği gibi çalışmıyor.
* Sanal makine (VM) yük devretme sonrasında çoğaltma çifti silme hello CX UI uzun bir süredir takılmış ve kullanıcıların hello yeniden çalışmayı tamamla veya işlemini devam ettirmek.
* Genel hello tutarlılık işi tarafından yapılır anlık görüntüsü işlemleri iyileştirilmiş toohelp azaltmak uygulama gibi SQL istemcilerinin bağlantısını keser.
* Windows üzerinde anlık görüntü oluşturmak için gerekli olan hello bellek kullanımı azaltarak hello tutarlılık Aracı (VACP.exe) Hello performansı geliştirilmiştir.
* Merhaba Yükleme Hizmeti kilitleniyor hello parola 16 karakterden daha büyük olduğunda.
* vContinuum değil denetleme ve hello kimlik bilgileri değiştiğinde yeni vCenter kimlik bilgileri.
* Linux üzerinde hello ana hedef önbellek Yöneticisi (cachemgr) dosyaları çoğaltma çifti azaltma sonuçları hello işlem sunucusundan yüklüyor değil.
* Merhaba fiziksel yük devretme kümesi (MSCS) disk sırası aynı hello tüm hello düğümlerde değil olduğunda çoğaltma bazı hello küme birimleri için ayarlanmadı.
  <br/>Bu düzeltmeyi korunmuş toobe tootake avantajlarından bu hello küme gerekiyor unutmayın.  
* SMTP işlevselliği RX Scout 7.1 tooScout 8.0.1 ' yükseltildikten sonra beklendiği gibi çalışmıyor.
* Bunu geçen toocomplete hello geri alma işlemi tootrack hello süre için daha fazla istatistikleri hello günlüğüne eklenen onu.
* Merhaba kaynak sunucuda Linux işletim sistemleri için destek eklenmiştir:
  * Red Hat Enterprise Linux (RHEL) 6 güncelleştirme 7
  * CentOS 6 7 güncelleştirmesi
* Şimdi Hello CX ve RX UI hello bildirim bit eşlem moduna girer hello çifti için gösterebilir.
* Merhaba aşağıdaki güvenlik düzeltmeleri RX eklenmiştir:

| **Sorun açıklaması** | **Uygulama yordamları** |
| --- | --- |
| Yetkilendirme atlama parametre oynama aracılığıyla |Kısıtlı erişim toonon geçerli kullanıcılar. |
| Siteler arası istek sahteciliğine |Her sayfa için rastgele oluşturur uygulanan hello sayfa belirteci kavramıdır. <br/>Bu, görürsünüz: <li> Yalnızca bir tek oturum açma örneği hello için aynı kullanıcı.</li><li>Sayfa yenileme çalışmıyor--toohello Pano yönlendirir.</li> |
| Kötü amaçlı dosya karşıya yükleme |Kısıtlı dosyaları toocertain uzantıları. Uzantıları izin verilir: 7z, AIFF, asf, AVI, bmp, csv, belge, docx, fla, flv, GIF, gz, gzip, jpeg, jpg, günlük ortalarında, mov, mp3, mp4, mpc, mpeg, mpg, ods, odt, pdf, png, ppt, pptx, pxd, qt, ram, rar, rm, RMI, rmvb, rtf, sdc, sitd, swf, sxc, sxw, tar , tgz, TIF, TIFF, txt, vsd, wav, wma, wmv, xls, xlsx, xml ve zip. |
| Kalıcı siteler arası komut dosyası |Giriş doğrulamaları eklendi. |

> [!NOTE]
> * Tüm Site Recovery Toplu güncelleştirmelerin. Güncelleştirme 3 hello düzeltmelerin güncelleştirme 1 ve güncelleştirme 2 sahiptir. Güncelleştirme 3 8.0.1 üzerinde doğrudan da uygulanabilir İST
> * Merhaba sistemde uygulanmasıyla geri sonra hello yapılandırma sunucusu ve RX güncelleştirmeleri alınamaz.
>
>

### <a name="azure-site-recovery-scout-801-update-2-update-03dec15"></a>Azure Site Recovery Scout 8.0.1 güncelleştirme 2 (03 Ara 15 güncelleştirmesi)
Güncelleştirme 2'deki düzeltmeler içerir:

* **Yapılandırma sunucusu**: hello 31 gün ücretsiz ölçüm özellik hello yapılandırma sunucusu, Site Recovery kaydedildi beklendiği gibi çalışmasını engelleyen bir sorun için düzeltme.
* **Birleşik aracı**: sürüm 8.0 too8.0.1 yükseltildiğinde hello ana hedef sunucusunda yüklü değil hello güncelleştirme ile sonuçlandı güncelleştirme 1'deki bir sorun için düzeltme.

### <a name="azure-site-recovery-scout-801-update-1"></a>Azure Site Recovery Scout 8.0.1 güncelleştirme 1
Güncelleştirme 1'hello aşağıdakileri içeren hata düzeltmeleri ve yeni özellikleri:

* Sunucu örneği başına ücretsiz koruma 31 gün sayısı. Bu, tootest işlev veya bir, kavram ayarlama sağlar.
  * Hello sunucusunun, yük devretme ve yeniden çalışma, tüm işlemler bir sunucu ilk Site Recovery Scout ile korunan hello zamandan itibaren ilk 31 gün Merhaba boş değildir.
  * Hello 32nd gün ve sonraki sürümleri, Azure Site Recovery koruması tooa müşteri ait site için hello standart örnek hızında her korumalı sunucu ücretlendirilir.
  * Herhangi bir zamanda hello şu anda ücretlendirilmeden korumalı sunucu sayısı'hello Azure Site Recovery kasası hello panosu sayfasında kullanılabilir.
* 5.5 güncelleştirme 2 vSphere komut satırı arabirimi (vCLI) için ek destek.
* Destek hello kaynak sunucuda Linux işletim sistemleri için eklenmiştir:
  * RHEL 6 güncelleştirme 6
  * RHEL 5 güncelleştirme 11
  * CentOS 6 güncelleştirme 6
  * CentOS 5 güncelleştirme 11
* Hata düzeltmeleri tooaddress hello aşağıdaki sorunlar:
  * Merhaba yapılandırma sunucusu veya RX sunucusu için kasa kayıt başarısız olur.
  * Küme birimleri, bunlar sürdürdüğünüzde kümelenmiş sanal makineler korunmuş beklendiği gibi görünmüyor.
  * Merhaba ana hedef sunucusu hello şirket içi üretim sanal makinelerden farklı ESXi sunucusunda barındırılıyorsa, yeniden çalışma başarısız olur.
  * Yapılandırma dosyası izinleri, koruma ve işlemleri etkiler too8.0.1 yükselttiğinizde değiştirilir.
  * Merhaba yeniden eşitleme eşik beklendiği gibi tooinconsistent çoğaltma davranışı, müşteri adayları zorlanamaz.
  * Merhaba RPO ayarlarını hello yapılandırma sunucusu arabiriminde doğru görünmüyor. sıkıştırılmamış hello veri değeri yanlış sıkıştırılmış hello değerini gösterir.
  * Merhaba kaldırma işlemi hello vContinuum Sihirbazı'nda beklendiği gibi silmez ve çoğaltma hello yapılandırma sunucusu arabiriminden silinmez.
  * ' I tıklattığınızda hello vContinuum Sihirbazı'nda hello disk otomatik olarak işaretli olmadığından **ayrıntıları** MSCS sanal makinelerin korumasını sırasında hello disk görünümünde.
  * Merhaba fiziksel-sanal (P2V) senaryosu sırasında sanal makinenin kurtarma taşınan toomanual CIMnotify ve CqMgHost, gibi gerekli HP hizmetler değil. Bu ek önyükleme zamanında sonuçlanır.
  * Merhaba ana hedef sunucusunda birden fazla 26 diskleri olduğunda Linux sanal makine koruması başarısız olur.

## <a name="next-steps"></a>Sonraki adımlar
Merhaba üzerinde sahip herhangi bir sorunuz sonrası [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).
