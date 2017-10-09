---
title: "VMware Azure aaaAzure Site Recovery dağıtımı Planlayıcısı | Microsoft Docs"
description: "Hello Azure Site Recovery dağıtımı Planlayıcısı Kullanıcı Kılavuzu'na budur."
services: site-recovery
documentationcenter: 
author: nsoneji
manager: garavd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 08/28/2017
ms.author: nisoneji
ms.openlocfilehash: a8c13cd47850575769e0186528807bc525bdeec7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-site-recovery-deployment-planner"></a>Azure Site Recovery dağıtım planlayıcısı
Bu makalede hello Azure Site Recovery dağıtımı Planlayıcısı kullanıcı VMware Azure üretim dağıtımları için bir kılavuzdur.

## <a name="overview"></a>Genel Bakış

Site Recovery kullanarak tüm VMware sanal makineleri (VM'ler) korumaya başlamadan önce yeterli bant genişliği ayırma günlük veri değişikliği hızınızı üzerinde toomeet istenen kurtarma noktası hedefi (RPO) bağlı. Emin toodeploy hello doğru sayıda yapılandırma sunucularına ve içi sunucuları işlemi olabilir.

Toocreate hello sağ türü ve hedef Azure depolama hesabı sayısı da gerekir. Zaman içinde artan kullanım nedeniyle kaynak üretim sunucularınızdaki büyümeyi hesaba katarak standart veya premium depolama hesapları oluşturun. İş yükü özelliklerine (örneğin, ikinci [IOPS] ya da veri dalgalanmasına başına okuma/yazma g/ç işlemleri) dayanarak VM başına hello depolama türü seçin ve Site Recovery sınırlar.

Merhaba Site Recovery dağıtımı Planlayıcısı genel Önizleme yalnızca hello VMware Azure senaryo için şu anda kullanılabilir olan bir komut satırı aracıdır. Uzaktan bu araçla (üretim etkisi doğabilecek) toounderstand hello bant genişliği ve Azure depolama gereksinimleri için başarılı çoğaltma kullanarak VMware sanal makinelerini profil ve yük devretme sınamasını. Tüm Site Recovery bileşenleri şirket içi yüklemeden hello aracını çalıştırabilirsiniz. Ancak, doğru tooget üretilen iş sonuçları elde, sonunda toodeploy hello ilk adımlarından biri değiştireceği hello en düşük gereksinimlerini karşılayan hello Site Recovery yapılandırma sunucusu Windows Server hello Planlayıcısı çalıştırmanızı öneririz Üretim dağıtımında.

Merhaba aracı aşağıdaki ayrıntılara hello sağlar:

**Uyumluluk değerlendirmesi**

* Disk sayısı, disk boyutu, IOPS, değişim sıklığı ve önyükleme türüne (EFI/BIOS) göre VM uygunluk değerlendirmesi
* Değişim çoğaltması için gerekli tahmini hello ağ bant genişliği

**Ağ bant genişliği ile RPO değerlendirmesi karşılaştırması**

* Değişim çoğaltması için gerekli tahmini hello ağ bant genişliği
* Site Recovery, şirket içi tooAzure alabilirsiniz hello işleme
* verilen sürede toocomplete ilk çoğaltma bant genişliği üzerinde hello tabanlı VM'ler toobatch Hello sayısı tahmini

**Azure altyapı gereksinimleri**

* Her VM için Hello depolama türü (standart veya premium depolama hesabı) gereksinimi
* Çoğaltma için ayarlanan standart ve premium depolama hesapları toobe Hello toplam sayısı
* Azure Depolama kılavuzuna göre depolama hesabı adlandırma önerileri
* Tüm VM'ler için Hello depolama hesabı yerleştirme
* test yük devretme veya yük devretme hello abonelikte önce Azure çekirdek toobe Hello sayısını ayarlama
* Hello Azure VM önerilen boyutu her içi VM

**Şirket içi altyapı gereksinimleri**
* Merhaba yapılandırma sunucularına sayısı gerekli ve şirket içi işlem sunucuları toobe dağıtılabilir

>[!IMPORTANT]
>
>Kullanım zamanla büyük olasılıkla tooincrease olduğundan, tüm hesaplamalar yüzde 30 büyüme faktörü iş yükü özellikleri içindeki varsayılarak ve ölçümleri profil tüm hello 95 yüzdebirlik değeri kullanılarak gerçekleştirilir önceki aracı hello (Okuma/sn, yazma karmaşıklığı ve bu nedenle İleri). Büyüme faktörü ve yüzdelik dilim hesaplaması öğelerinin her ikisi de yapılandırılabilir özelliktedir. Büyüme faktörü hakkında daha fazla toolearn hello "büyüme faktörü hususlar" bölümüne bakın. Yüzdelik değer hakkında daha fazla toolearn hello "Merhaba hesaplama için kullanılan yüzdelik değer" bölümüne bakın.
>

## <a name="requirements"></a>Gereksinimler
Merhaba aracı iki ana aşaması vardır: profil oluşturma ve rapor oluşturma. Bir üçüncü seçenek toocalculate işleme yalnızca yoktur. hangi hello profili oluşturma ve üretilen iş ölçüm başlatılan hello sunucu için Hello gereksinimleri, aşağıdaki tablonun hello sunulur:

| Sunucu gereksinimi | Açıklama|
|---|---|
|Profil oluşturma ve aktarım hızı ölçümü| <ul><li>İşletim sistemi: Microsoft Windows Server 2012 R2<br>(en az hello ideal eşleşen [boyut hello yapılandırma sunucusu için öneriler](https://aka.ms/asr-v2a-on-prem-components))</li><li>Makine yapılandırması: 8 vCPU, 16 GB RAM, 300 GB HDD</li><li>[Microsoft .NET Framework 4.5](https://aka.ms/dotnet-framework-45)</li><li>[VMware vSphere PowerCLI 6.0 R3](https://aka.ms/download_powercli)</li><li>[Visual Studio 2012 için Microsoft Visual C++ Yeniden Dağıtılabilir](https://aka.ms/vcplusplus-redistributable)</li><li>Internet erişimi tooAzure bu sunucudan</li><li>Azure depolama hesabı</li><li>Merhaba sunucusunda yönetici erişimi</li><li>En az 100 GB boş disk alanı (30 günlük profili oluşturulmuş ve her biri ortalama üç diske sahip 1000 VM varsayıldığında)</li><li>VMware vCenter istatistikleri düzeyi ayarları too2 veya yüksek düzey olarak ayarlanmalıdır.</li><li>443 bağlantı noktası izin ver: ASR dağıtım Planlayıcısı Bu bağlantı noktası tooconnect toovCenter sunucusunda/ESXi ana kullanır</ul></ul>|
| Rapor oluşturma | Microsoft Excel 2013 ve üzerinin yüklü olduğu herhangi bir Windows PC ya da Windows Server |
| Kullanıcı izinleri | Tooaccess hello VMware vCenter server/VMware vSphere ESXi konağı profil oluşturma sırasında kullanılan hello kullanıcı hesabı için salt okunur izni |

> [!NOTE]
>
>Merhaba aracı yalnızca VM'ler VMDK ve RDM'nin disklerle profil. VM profilini iSCSI veya NFS diskleri ile oluşturamaz. Site Recovery VMware sunucuları için iSCSI ve NFS diskleri desteklemiyor, ancak bir hello dağıtım Planlayıcısı hello Konuk içinde değil ve yalnızca vCenter performans sayaçlarını kullanarak profilleri çünkü hello aracı bu disk türleri görünürlük sahip değil.
>

## <a name="download-and-extract-hello-public-preview"></a>İndirmeyi ve ayıklamayı hello genel Önizleme
1. Hello hello en son sürümünü indirme [Site Recovery dağıtımı Planlayıcısı genel Önizleme](https://aka.ms/asr-deployment-planner).  
Merhaba aracı bir .zip klasörde paketlenmiştir. Merhaba hello aracının geçerli sürümü yalnızca hello VMware Azure senaryoyu destekler.

2. Merhaba .zip klasörü toohello Windows server toorun hello aracı istediğiniz kopyalayın.  
Profili hello VM'ler toobe tutan ağ erişim tooconnect toohello vCenter sunucusu/vSphere ESXi ana Hello sunucusu varsa, Windows Server 2012 R2'den hello aracını çalıştırabilirsiniz. Ancak, donanım yapılandırmasını hello karşılayan bir sunucuda hello aracı çalıştırmanızı öneririz [yapılandırma sunucusu boyutlandırma kılavuz](https://aka.ms/asr-v2a-on-prem-components). Site Recovery bileşenleri şirket içi zaten dağıttıysanız, hello yapılandırma sunucusundan hello aracını çalıştırın.

 Merhaba sahip olmasını öneririz (-yerleşik işlem sunucusu olan) hello yapılandırma sunucuya hello aracını çalıştırdığınız hello sunucuda olarak aynı donanım yapılandırması. Bu tür bir yapılandırma, Site Recovery çoğaltma sırasında elde edebileceğiniz bu hello aracı raporları eşleşmeleri hello gerçek aktarım hızı bu elde hello verimlilik sağlar. kullanılabilir ağ bant genişliği hello sunucuda ve hello sunucusunun donanım yapılandırması (CPU, depolama ve benzeri) Hello verimlilik hesaplama bağlıdır. Başka bir sunucudan hello aracı çalıştırırsanız hello verimlilik, sunucu tooMicrosoft Azure hesaplanır. Ayrıca, hello sunucusunun Hello donanım yapılandırması, hello yapılandırma sunucusu farklı olabilir çünkü aracı raporları hello elde hello verimlilik kesin olmayabilir.

3. Merhaba .zip klasöre ayıklayın.  
birden çok dosya ve alt Hello klasör içerir. Merhaba yürütülebilir hello üst klasöründeki ASRDeploymentPlanner.exe dosyasıdır.

    Örnek:  
    Merhaba .zip dosyasını tooE kopyalayın: \ sürücü ve ayıklayın.
   E:\ASR Deployment Planner-Preview_v1.2.zip

    E:\ASR Deployment Planner-Preview_v1.2\ ASR Deployment Planner-Preview_v1.2\ ASRDeploymentPlanner.exe

## <a name="capabilities"></a>Özellikler
Merhaba komut satırı aracı (ASRDeploymentPlanner.exe) üç modu aşağıdaki hello birini çalıştırabilirsiniz:

1. Profil oluşturma  
2. Rapor oluşturma
3. Aktarım hızı alma

İlk olarak, modu toogather VM veri dalgalanmasına ve IOPS profil hello aracını çalıştırın. Ardından, hello aracı toogenerate hello rapor toofind, hello ağ bant genişliği ve depolama gereksinimleri çalıştırın.

## <a name="profiling"></a>Profil oluşturma
Profil oluşturma modunda hello dağıtım planlayıcısı aracı toohello vCenter sunucusu/vSphere ESXi ana toocollect performans verileri hello VM hakkında bağlanır.

* Doğrudan bağlantı toothem yapmış profil hello üretim VM'ler, hello performansını etkilemez. Tüm performans verilerini hello vCenter sunucusu/vSphere ESXi ana bilgisayardan toplanır.
* olduğunu düşünülerek etkisi hello sunucuda profil nedeniyle, hello aracı sorguları hello vCenter sunucusu/vSphere ESXi ana her 15 dakikada tooensure. Bu sorgu aralığı profil doğruluğu tehlikeye Hello aracı dakikada 's performans sayacı verilerini depoladığından değil.

### <a name="create-a-list-of-vms-tooprofile"></a>Sanal makineleri tooprofile listesi oluşturma
İlk olarak, profili hello VM'ler toobe listesini gerekir. Aşağıdaki yordamı hello hello VMware vSphere Powerclı komutları kullanarak bir vCenter sunucusu/vSphere ESXi ana bilgisayarda sanal makineleri tüm hello adlarını alabilirsiniz. Alternatif olarak, bir dosya hello kolay adlarını listelemek veya VM'ler tooprofile el ile istediğiniz IP adreslerini hello.

1. Oturum açma toohello VM, VMware vSphere Powerclı yüklenir.
2. Merhaba VMware vSphere Powerclı konsolunu açın.
3. Merhaba yürütme İlkesi hello komut dosyası için etkinleştirildiğinden emin olun. Etkinleştirilirse, hello VMware vSphere Powerclı konsolunu Yönetici modunda başlatın ve hello aşağıdaki komutu çalıştırarak etkinleştirin:

            Set-ExecutionPolicy –ExecutionPolicy AllSigned

4. Connect VIServer cmdlet hello adı olarak tanınmıyor, komutu aşağıdaki optionly gerek toorun hello olabilir.
 
            Add-PSSnapin VMware.VimAutomation.Core 

5. tooget bir vCenter sunucusu/vSphere ESXi sanal makinelerin tüm hello adlarını barındırmak ve hello listesi çalışma hello iki komutları burada listelenen bir .txt dosyasında depolar.
&lsaquo;Sunucu adı&rsaquo;, &lsaquo;kullanıcı adı&rsaquo;, &lsaquo;parola&rsaquo;, &lsaquo;outputfile.txt&rsaquo; değerlerini girdilerinizle değiştirin.

            Connect-VIServer -Server <server name> -User <user name> -Password <password>

            Get-VM |  Select Name | Sort-Object -Property Name >  <outputfile.txt>

6. Merhaba çıktı dosyasını Not Defteri'nde açın ve ardından hello adları tooprofile tooanother dosyası (örneğin, ProfileVMList.txt), satır başına bir VM adı istediğiniz tüm VM'lerin kopyalayın. Bu dosya giriş toohello kullanılan *- VMListFile* hello komut satırı aracı parametresi.

    ![VM adı listesinde hello dağıtım Planlayıcısı](./media/site-recovery-deployment-planner/profile-vm-list.png)

### <a name="start-profiling"></a>Profil oluşturmaya başlama
Hello profili VM'ler toobe listesini oluşturduktan sonra profil oluşturma modu hello aracını çalıştırabilirsiniz. Profil oluşturma modunda hello aracı toorun zorunlu ve isteğe bağlı parametreleri hello listesi aşağıdadır.

ASRDeploymentPlanner.exe -Operation StartProfiling /?

| Parametre adı | Açıklama |
|---|---|
| -Operation | StartProfiling |
| -Server | Merhaba tam etki alanı adı veya profili toobe olan VM'ler olduğundan hello vCenter sunucusu/vSphere ESXi ana bilgisayarın IP adresi.|
| -User | Merhaba kullanıcı adı tooconnect toohello vCenter sunucusu/vSphere ESXi ana bilgisayar. Merhaba kullanıcı en az toohave salt okunur erişim verilmesi gerekir.|
| -VMListFile | hello profili VM'ler toobe listesini içeren hello dosyası. Merhaba dosya yolunu mutlak veya göreli olabilir. Merhaba dosya her satırda bir VM adı/IP adresi olmalıdır. Merhaba dosyasında belirtilen sanal makine adı olması hello hello vCenter sunucusu/vSphere ESXi ana bilgisayarda hello VM adı ile aynı.<br>Örneğin, hello dosyası VMList.txt VM'ler aşağıdaki hello içerir:<ul><li>virtual_machine_A</li><li>10.150.29.110</li><li>virtual_machine_B</li><ul> |
| -NoOfDaysToProfile | hangi profil oluşturma için toobe olduğu gün sayısını Hello çalıştırın. 15 ortamınızdaki iş yükü düzeni hello hello tooensure belirtilen dönem gözlenir ve tooprovide doğru bir öneri kullanılan günden fazla profil çalıştırmanızı öneririz. |
| -Directory | (İsteğe bağlı) hello Evrensel Adlandırma Kuralı (UNC) veya yerel dizin yolu toostore profil oluşturma sırasında oluşturulan veri profil oluşturma. Bir dizin adı verilmemişse hello geçerli yolu altında 'ProfiledData' adlı hello dizin hello varsayılan dizini olarak kullanılır. |
| -Password | (İsteğe bağlı) hello parola toouse tooconnect toohello vCenter sunucusu/vSphere ESXi ana bilgisayar. Bir şimdi belirtmezseniz, hello komutu çalıştırıldığında için istenir.|
| -StorageAccountName | Kullanılan toofind hello işleme çoğaltma verilerini ulaşılabilir (isteğe bağlı) hello depolama hesabı adı tooAzure şirket içi. Merhaba aracı yüklemeleri test veri toothis depolama hesabı toocalculate üretilen.|
| -StorageAccountKey | Tooaccess hello depolama hesabı kullandı (isteğe bağlı) hello depolama hesabı anahtarı. Toohello Azure portalına gidin > depolama hesapları ><*depolama hesabı adı*>> Ayarlar > erişim anahtarları > Key1 (veya Klasik depolama hesabı için birincil erişim anahtarı). |
| -Ortam | (isteğe bağlı) Bu, hedef Azure depolama hesabı ortamınızdır. Şu üç değerden herhangi birini alabilir: AzureCloud,AzureUSGovernment, AzureChinaCloud. Varsayılan seçenek AzureCloud değeridir. Hedef Azure bölgesi Azure ABD devlet kurumları veya Azure Çin bulut olduğunda hello parametresini kullanın. |


Vm'leriniz için en az 15 too30 gün Profil öneririz. Dönem profil hello sırasında ASRDeploymentPlanner.exe çalıştıran tutar. Merhaba aracı profil oluşturma zaman girişi gün içinde alır. Tooprofile birkaç saat veya dakika hello aracının hızlı testi için hello genel önizlemede isterseniz, hello eşdeğer ölçü gün tooconvert hello zaman gerekir. Örneğin, 30 dakika boyunca tooprofile hello giriş 30/(60*24) olmalıdır = 0.021 gün. zaman profil izin hello en az 30 dakikadır.

Profil oluşturma sırasında bir depolama hesabı adı ve Site Recovery çoğaltma hello yapılandırma sunucusundan veya işlem sunucusu tooAzure hello zamanında elde edebilirsiniz anahtar toofind hello verimlilik isteğe bağlı olarak geçirebilirsiniz. Merhaba depolama hesabı adı ve anahtarı profil oluşturma sırasında değil iletilirse, hello aracı ulaşılabilir verim hesaplamaz.

Merhaba aracı VM'ler çeşitli kümeleri için birden çok örneğini çalıştırabilirsiniz. Merhaba VM adları kümeleri profil hello hiçbirinde yinelenmeyecek emin olun. Örneğin, on VM'ler profili (VM1 VM10 aracılığıyla) ve birkaç gün sonra başka bir beş VM'ler tooprofile istiyorsanız (Merhaba ikinci VM'ler kümesi için başka bir komut satırı konsolundan hello aracını çalıştırabilirsiniz VM11 VM15 aracılığıyla), (VM11 VM15 aracılığıyla). Merhaba ikinci VM'ler kümesi herhangi bir VM ad hello ilk profil örneğinden sahip değil veya farklı bir çıkış dizini hello ikinci çalıştırmak için kullandığınız emin olun. Merhaba aracının iki örneğini profil oluşturma için kullanılıyorsa hello aynı VM'ler ve kullanım aynı çıktı dizini Merhaba, oluşturulan hello rapor yanlış olur.

VM yapılandırmaları kez hello işleminin profilini oluşturmaya hello başında yakalanan ve VMDetailList.xml adlı bir dosyada depolanır. Merhaba rapor oluşturulduğunda bu bilgiler kullanılır. Profil oluşturma hello başına toohello ucundan VM yapılandırması (örneğin, bir artan sayısı çekirdek, diskler veya NIC) herhangi bir değişiklik sayılmaz. Profili bir VM yapılandırması hello indirmelere, hello genel önizlemede profil oluşturma sırasında değiştiyse İşte hello geçici çözüm tooget son VM ayrıntıları hello rapor oluşturulurken:

* VMdetailList.xml yedekleyin ve hello dosyayı geçerli konumundan silin.
* -Kullanıcı ve - parola bağımsız değişkenler geçirme hello zaman rapor oluşturma.

komut profil hello dizin profil hello birkaç dosyaları oluşturur. Bunu yaptığınızda bu nedenle rapor oluşturma etkilediğinden hello dosyalardan birini silmeyin.

#### <a name="example-1-profile-vms-for-30-days-and-find-hello-throughput-from-on-premises-tooazure"></a>Örnek 1: Profil VM'ler için 30 gün ve şirket içi tooAzure hello akışından Bul
```
ASRDeploymentPlanner.exe -Operation StartProfiling -Directory “E:\vCenter1_ProfiledData” -Server vCenter1.contoso.com -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt”  -NoOfDaysToProfile  30  -User vCenterUser1 -StorageAccountName  asrspfarm1 -StorageAccountKey Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==
```

#### <a name="example-2-profile-vms-for-15-days"></a>Örnek 2: 15 günlük sanal makine profili oluşturma

```
ASRDeploymentPlanner.exe -Operation StartProfiling -Directory “E:\vCenter1_ProfiledData” -Server vCenter1.contoso.com -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt”  -NoOfDaysToProfile  15  -User vCenterUser1
```

#### <a name="example-3-profile-vms-for-1-hour-for-a-quick-test-of-hello-tool"></a>Örnek 3: Profili VM'ler hello Aracı'nın hızlı testi için 1 saat için
```
ASRDeploymentPlanner.exe -Operation StartProfiling -Directory “E:\vCenter1_ProfiledData” -Server vCenter1.contoso.com -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt”  -NoOfDaysToProfile  0.04  -User vCenterUser1
```

>[!NOTE]
>
>* Hello sunucu hello aracı ise yeniden başlatılıncaya kadar veya kilitlendi, üzerinde çalışan veya kapatın, aracı Ctrl kullanarak hello + C, hello profili verileri korunur. Ancak, son 15 dakika profili veri eksik hello olasılığını yoktur. Merhaba sunucu yeniden başlatıldıktan sonra bu tür bir örnekte profil oluşturma modunda hello aracı yeniden çalıştırın.
>* Ne zaman hello depolama hesabı adı ve anahtarı geçirilir, hello aracı ölçüleri hello verimlilik profil hello son adımı sırasında. Profil oluşturma tamamlanmadan önce hello aracı kapattıysanız, hello işleme hesaplanan değil. oluşturmadan toofind hello verimlilik Merhaba raporu, hello GetThroughput işlemi hello komut satırı konsolundan çalıştırabilirsiniz. Aksi takdirde, oluşturulan hello rapor hello verimlilik bilgi içermez.


## <a name="generate-a-report"></a>Rapor oluşturma
Merhaba aracı tüm hello dağıtım önerileri özetler hello rapor çıktısı, makrosu özellikli Microsoft Excel dosyasına (XLSM dosyası) oluşturur. Merhaba rapor DeploymentPlannerReport_ adlı <*benzersiz bir sayısal tanımlayıcı*> .xlsm ve içinde yerleştirilen hello belirtilen dizin.

Profil oluşturma tamamlandıktan sonra rapor oluşturma modunda hello aracını çalıştırabilirsiniz. Aşağıdaki tablonun hello zorunlu ve isteğe bağlı aracı parametreleri toorun rapor oluşturma modunda listesini içerir.

`ASRDeploymentPlanner.exe -Operation GenerateReport /?`

|Parametre adı | Açıklama |
|-|-|
| -Operation | GenerateReport |
| -Server |  Merhaba vCenter/vSphere sunucusu tam olarak nitelenmiş etki alanı adı veya IP adresi (kullanımı hello aynı adı veya profil hello zamanında kullanılan IP adresi) burada, rapor oluşturulan toobe olan VM'ler hello profili konumlandırıldığını. Profil oluşturma hello aynı anda bir vCenter sunucusu kullandıysanız, bir vSphere sunucusu rapor oluşturma ve tam tersini kullanamayacağınızı unutmayın.|
| -VMListFile | Rapor hello profili VM'ler hello listesini içeren hello için oluşturulan toobe dosyasıdır. Merhaba dosya yolunu mutlak veya göreli olabilir. Merhaba dosyası, bir VM adı veya IP adresi satır başına içermelidir. Merhaba dosyasında belirtilen hello VM adları olması hello hello vCenter sunucusu/vSphere ESXi konağına ve hangi profil oluşturma sırasında kullanılan eşleşme hello VM adları ile aynı.|
| -Directory | (İsteğe bağlı) hello UNC veya yerel dizin yolu burada hello profili verileri (profil oluşturma sırasında oluşturulan dosyaları) depolanır. Bu veriler, hello raporu oluşturmak için gereklidir. Bir ad belirtilmezse, 'ProfiledData' dizini kullanılır. |
| -GoalToCompleteIR | (İsteğe bağlı) hello VM'ler hello ilk çoğaltmasının hangi hello profili saat sayısını tamamlandı toobe gerekir. oluşturulan hello rapor sağlar, ilk çoğaltma tamamlanması belirtilen hello VM hello sayısı zaman. Merhaba, 72 saat varsayılandır. |
| -User | (İsteğe bağlı) hello kullanıcı adı toouse tooconnect toohello vCenter/vSphere sunucusu. Merhaba, hello hello disk sayısı, çekirdek sayısı ve NIC'ler, hello rapordaki toouse sayısı gibi VM'ler kullanılan toofetch hello en son yapılandırma bilgilerini adıdır. Merhaba adı sağlanmadı hello kickoff profil hello başında toplanan hello yapılandırma bilgileri kullanılır. |
| -Password | (İsteğe bağlı) hello parola toouse tooconnect toohello vCenter sunucusu/vSphere ESXi ana bilgisayar. Merhaba parola parametre olarak belirtilmezse, hello komutu çalıştırıldığında için daha sonra istenir. |
| -DesiredRPO | (İsteğe bağlı) hello istenen kurtarma noktası hedefi, dakika cinsinden. Merhaba varsayılan değer 15 dakikadır.|
| -Bandwidth | MB/sn cinsinden bant genişliği. Merhaba parametresi toouse toocalculate hello Merhaba elde edilebilir RPO bant genişliği belirtilmiş. |
| -StartDate | (İsteğe bağlı) Merhaba, MM tarih ve saat Başlat-GG-YYYY:HH:MM (24 saat biçiminde). *StartDate* değeri *EndDate* ile birlikte belirtilmelidir. StartDate belirtildiğinde, hello rapor StartDate ve EndDate arasındaki toplanan hello profili veriler için oluşturulur. |
| -EndDate | (İsteğe bağlı) hello son tarih ve saat AA-GG-YYYY:HH:MM (24 saat biçiminde). *EndDate* değeri *StartDate* ile birlikte belirtilmelidir. EndDate belirtildiğinde, hello rapor StartDate ve EndDate arasındaki toplanan hello profili veriler için oluşturulur. |
| -GrowthFactor | Yüzde olarak ifade (isteğe bağlı) hello büyüme faktörü. Merhaba, yüzde 30 varsayılandır. |
| -UseManagedDisks | (Optional) UseManagedDisks - Evet/Hayır. Varsayılan değer Evet’tir. sanal makinelerin tek bir depolama hesabına yerleştirilebilir Hello sayı olup olmadığını sanal makinelerin yük devretme ve Test yük devretme yönetilmeyen disk yerine yönetilen diskteki yapılır göz önünde bulundurularak hesaplanır. |

#### <a name="example-1-generate-a-report-with-default-values-when-hello-profiled-data-is-on-hello-local-drive"></a>Örnek 1: hello profili veri hello yerel sürücüde olduğunda varsayılan değerlerine sahip bir rapor oluşturur
```
ASRDeploymentPlanner.exe -Operation GenerateReport -Server vCenter1.contoso.com -Directory “\\PS1-W2K12R2\vCenter1_ProfiledData” -VMListFile “\\PS1-W2K12R2\vCenter1_ProfiledData\ProfileVMList1.txt”
```

#### <a name="example-2-generate-a-report-when-hello-profiled-data-is-on-a-remote-server"></a>Örnek 2: hello profili verilerini uzak bir sunucuda olduğunda bir rapor oluşturur
Merhaba Uzak dizin üzerinde okuma/yazma erişimi olmalıdır.
```
ASRDeploymentPlanner.exe -Operation GenerateReport -Server vCenter1.contoso.com -Directory “\\PS1-W2K12R2\vCenter1_ProfiledData” -VMListFile “\\PS1-W2K12R2\vCenter1_ProfiledData\ProfileVMList1.txt”
```

#### <a name="example-3-generate-a-report-with-a-specific-bandwidth-and-goal-toocomplete-ir-within-specified-time"></a>Örnek 3: belirtilen süre içinde bir özel bant genişliği ve hedef toocomplete IR sahip bir rapor oluşturun
```
ASRDeploymentPlanner.exe -Operation GenerateReport -Server vCenter1.contoso.com -Directory “E:\vCenter1_ProfiledData” -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt” -Bandwidth 100 -GoalToCompleteIR 24
```

#### <a name="example-4-generate-a-report-with-a-5-percent-growth-factor-instead-of-hello-default-30-percent"></a>Örnek 4: hello varsayılan yüzde 30 yerine yüzde 5 büyüme faktörü ile bir rapor oluşturun
```
ASRDeploymentPlanner.exe -Operation GenerateReport -Server vCenter1.contoso.com -Directory “E:\vCenter1_ProfiledData” -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt” -GrowthFactor 5
```

#### <a name="example-5-generate-a-report-with-a-subset-of-profiled-data"></a>Örnek 5: Profili oluşturulan verilerin bir alt kümesi ile rapor oluşturma
Örneğin, 30 gün içinde profili veri ve toogenerate bir rapor yalnızca 20 gün boyunca istiyor.
```
ASRDeploymentPlanner.exe -Operation GenerateReport -Server vCenter1.contoso.com -Directory “E:\vCenter1_ProfiledData” -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt” -StartDate  01-10-2017:12:30 -EndDate 01-19-2017:12:30
```

#### <a name="example-6-generate-a-report-for-5-minute-rpo"></a>Örnek 6: 5 dakikalık RPO için rapor oluşturma
```
ASRDeploymentPlanner.exe -Operation GenerateReport -Server vCenter1.contoso.com -Directory “E:\vCenter1_ProfiledData” -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt”  -DesiredRPO 5
```

## <a name="percentile-value-used-for-hello-calculation"></a>Merhaba hesaplama için kullanılan yüzdelik değer
**Bir rapor oluşturduğunda mu hello aracı kullanım profil oluşturma sırasında hangi hello performans ölçümleri varsayılan yüzde birlik değerini toplanan?**

Merhaba aracı Varsayılanları toohello 95 yüzde birlik değerini okuma/yazma IOPS, IOPS ve tüm hello Vm'leri profil oluşturma sırasında toplanan veri dalgalanmasına yazma. Bu ölçüm, VM'ler nedeniyle geçici olayları görebilirsiniz bu hello 100 yüzdebirlik depo sağlar hedef depolama hesabı ve kaynak bant genişliği gereksinimlerini kullanılmaz toodetermine olduğu. Örneğin, geçici olay günde bir kez gerçekleştirilen bir yedekleme işi, düzenli aralıklarla yapılan veritabanı dizini oluşturma veya analiz raporu oluşturma etkinliği ya da kısa süreli diğer benzer olaylar olabilir.

Azure'da Hello iş yükleri çalıştırırken 95 yüzdebirlik değerleri kullanarak en iyi performans sağlar, gerçek iş yükü özellikleri ve doğru bir resmini sağlar hello. Biz bu numarayı toochange gerekir düşündüğünüz değil. Merhaba değerini (toohello 90 yüzdebirlik, örneğin) değiştirirseniz, hello yapılandırma dosyasını Güncelleştir *ASRDeploymentPlanner.exe.config* hello varsayılan klasör ve hello profili var olan yeni bir rapor toogenerate Kaydet veriler.
```
<add key="WriteIOPSPercentile" value="95" />      
<add key="ReadWriteIOPSPercentile" value="95" />      
<add key="DataChurnPercentile" value="95" />
```

## <a name="growth-factor-considerations"></a>Büyüme faktörü ile ilgili dikkat edilmesi gerekenler
**Dağıtımları planlarken neden büyüme faktörünü göz önünde bulundurmalıyım?**

Bu, olası artış kullanım zaman içindeki varsayılarak, iş yükü özellikleri büyüme için kritik tooaccount olur. İş yükü özelliklerini değiştirirseniz koruma yerinde olduktan sonra koruma için tooa farklı depolama hesabı devre dışı bırakma ve hello korumayı yeniden etkinleştirmeden geçemezsiniz.

Örneğin, bugün sanal makinenizin standart bir depolama çoğaltma hesabına uygun olduğunu düşünelim. Merhaba sonraki üç ay, büyük olasılıkla toooccur bazı değişiklikler şunlardır:

* Merhaba VM üzerinde çalışan Merhaba uygulaması kullanıcı Hello sayısını artırır.
* Site Recovery çoğaltma ayak tutabilirsiniz böylece hello elde edilen artan karmaşıklık hello VM üzerinde hello VM toogo toopremium depolama gerektirir.
* Sonuç olarak, toodisable sahip ve koruma tooa premium depolama hesabı yeniden etkinleştirin.

Dağıtım planlama sırasında ve hello varsayılan değer yüzde 30 durumdayken büyüme için planlama öneririz. Üzerinde uygulama kullanımı düzeni ve büyüme tahminleri hello uzman olan ve bu numarayı uygun şekilde değiştirebilirsiniz Rapor oluştururken oluştu. Ayrıca, birden çok raporlar oluşturabilir hello çeşitli büyüme faktörleriyle ile aynı veri profili ve en iyi sizin için ne tür hedef depolama ve kaynak bant genişliği öneriler çalışacağını belirler.

Merhaba oluşturulan Microsoft Excel raporu aşağıdaki bilgilerle hello içerir:

* [Girdi](site-recovery-deployment-planner.md#input)
* [Öneriler](site-recovery-deployment-planner.md#recommendations-with-desired-rpo-as-input)
* [Öneriler-Bant Genişliği Girdisi](site-recovery-deployment-planner.md#recommendations-with-available-bandwidth-as-input)
* [VM<->Depolama Yerleşimi](site-recovery-deployment-planner.md#vm-storage-placement)
* [Uyumlu VM’ler](site-recovery-deployment-planner.md#compatible-vms)
* [Uyumsuz VM’ler](site-recovery-deployment-planner.md#incompatible-vms)

![Dağıtım planlayıcısı](./media/site-recovery-deployment-planner/dp-report.png)

## <a name="get-throughput"></a>Aktarım hızı alma

Site Recovery elde edebilirsiniz tooestimate hello işleme tooAzure GetThroughput modunda hello aracı çoğaltma sırasında şirket içi. Merhaba aracı hello verimlilik aracı hello hello sunucusundan çalıştıran hesaplar. İdeal olarak, bu sunucu hello yapılandırma sunucusu boyutlandırma kılavuzu temel alır. Site Recovery bileşenleri şirket içi altyapısı zaten dağıttıysanız, hello aracı hello yapılandırma sunucusunda çalıştırın.

Komut satırı konsolunu açın ve toohello Site Recovery dağıtımı planlama aracı klasörüne gidin. ASRDeploymentPlanner.exe dosyasını aşağıdaki parametrelerle çalıştırın.

`ASRDeploymentPlanner.exe -Operation GetThroughput /?`

|Parametre adı | Açıklama |
|-|-|
| -Operation | GetThroughput |
| -Directory | (İsteğe bağlı) hello UNC veya yerel dizin yolu burada hello profili verileri (profil oluşturma sırasında oluşturulan dosyaları) depolanır. Bu veriler, hello raporu oluşturmak için gereklidir. Bir dizin adı belirtilmezse ‘ProfiledData’ dizini kullanılır. |
| -StorageAccountName | Şirket içi tooAzure veri çoğaltma için kullanılan tüketilen toofind hello bant genişliği hello depolama hesabı adı. tüketilen hello aracı yüklemeleri test veri toothis depolama hesabı toofind hello bant genişliği. |
| -StorageAccountKey | tooaccess hello depolama hesabı kullandı hello depolama hesabı anahtarı. Toohello Azure portalına gidin > depolama hesapları ><*depolama hesabı adı*>> Ayarlar > erişim anahtarları > Key1 (veya bir Klasik depolama hesabı için birincil erişim anahtarını). |
| -VMListFile | tüketilen hesaplama hello için bant genişliği profili VM'ler toobe hello listesini içeren hello dosyası. Merhaba dosya yolunu mutlak veya göreli olabilir. Merhaba dosya her satırda bir VM adı/IP adresi olmalıdır. Merhaba dosyasında belirtilen hello VM adları olması hello hello VM adları hello vCenter sunucusu/vSphere ESXi ana bilgisayarda aynı.<br>Örneğin, hello dosyası VMList.txt VM'ler aşağıdaki hello içerir:<ul><li>VM_A</li><li>10.150.29.110</li><li>VM_B</li></ul>|
| -Ortam | (isteğe bağlı) Bu, hedef Azure depolama hesabı ortamınızdır. Şu üç değerden herhangi birini alabilir: AzureCloud,AzureUSGovernment, AzureChinaCloud. Varsayılan seçenek AzureCloud değeridir. Hedef Azure bölgesi Azure ABD devlet kurumları veya Azure Çin bulut olduğunda hello parametresini kullanın. |

Merhaba aracı oluşturur birkaç 64 MB'lık asrvhdfile <> # .vhd dosyaları (burada "#" Merhaba dosyalarının sayısıdır) hello belirtilen dizinde. Merhaba aracı hello dosyaları toohello depolama hesabı toofind hello üretilen yükler. Merhaba verimlilik ölçülen sonra hello aracı hello depolama hesabından ve hello yerel sunucudan tüm hello dosyaları siler. Üretilen iş hesaplama sırasında hello aracı herhangi bir nedenle sonlandırıldıysa hello depolama veya hello yerel sunucudan hello dosyaları silin değil. Toodelete olacaktır bunları el ile.

Merhaba üretilen iş belirtilen bir noktada zamanında ölçülür ve bu Site kurtarma, çoğaltma sırasında elde edebilirsiniz hello en fazla üretilen tüm diğer etkenlere bağlı kalır koşuluyla aynı hello. Örneğin, herhangi bir uygulama çoğaltma sırasında aynı ağ, hello gerçek verimlilik değişir hello hakkında daha fazla bant genişliği tüketmesi başlarsa. Bir yapılandırma sunucusundan hello GetThroughput komutu çalıştırıyorsanız, hello aracı tüm korumalı sanal makineleri ve devam eden çoğaltmayı farkında değildir. Merhaba hello ölçülen işleme hello hello VM'ler korumalı işlemini çalıştırın GetThroughput karmaşıklığı yüksek veri varsa farklı sonucudur. Hello aracı çeşitli noktalarda toounderstand profil oluşturma sırasında zaman düzeyleri çeşitli zamanlarda elde edilebilir hangi verimlilik çalıştırmanızı öneririz. Merhaba raporda hello aracı hello son ölçülen işleme gösterir.

### <a name="example"></a>Örnek
```
ASRDeploymentPlanner.exe -Operation GetThroughput -Directory  E:\vCenter1_ProfiledData -VMListFile E:\vCenter1_ProfiledData\ProfileVMList1.txt  -StorageAccountName  asrspfarm1 -StorageAccountKey by8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==
```

>[!NOTE]
>
> Hello aracı hello sahip bir sunucu üzerinde aynı depolama ve CPU özelliklerini hello yapılandırma sunucusu olarak.
>
> Çoğaltma için hello önerilen bant genişliği toomeet hello RPO hello süresinin yüzde 100 olarak ayarlayın. Merhaba aracı tarafından raporlanan elde hello verimlilik artış görmüyorsanız, hello sağ bant genişliği, ayarladıktan sonra aşağıdaki hello:
>
>  1. Toodetermine herhangi bir ağ, Site Recovery verimlilik sınırlama hizmet kalitesi (QoS) olup olmadığını denetleyin.
>
>  2. Site Recovery kasası hello fiziksel olarak desteklenen Microsoft Azure bölgesi toominimize ağ gecikmesini en yakın olup toodetermine denetleyin.
>
>  3. Yerel depolama özellikleri toodetermine hello donanım (örneğin, HDD tooSSD) artırabilir olup olmadığını denetleyin.
>
>  4. Merhaba işlem sunucusu Hello Site Recovery ayarları çok değiştirmek[hello çoğaltma için kullanılan ağ bant genişliği miktarını artırmak](./site-recovery-plan-capacity-vmware.md#control-network-bandwidth).

## <a name="recommendations-with-desired-rpo-as-input"></a>Girdi olarak istenen RPO ile öneriler

### <a name="profiled-data"></a>Profili oluşturulan veriler

![Merhaba dağıtım Planlayıcısı Hello profili veri görünümü](./media/site-recovery-deployment-planner/profiled-data-period.png)

**Profili veri süresi**: hello dönemi sırasında hangi hello profil çalıştırıldı. Belirli bir döneme ait hello raporu, rapor oluşturma sırasında StartDate ve EndDate seçenekleri kullanarak oluşturur sürece varsayılan olarak, tüm profili verileri hello aracı hello hesaplamadaki içerir.

**Sunucu adı**: hello adı veya IP adresini hello VMware vCenter veya ESXi ana bilgisayar, sanal makineleri rapor oluşturulur.

**RPO istenen**: hello kurtarma noktası hedefi, dağıtımınız için. Varsayılan olarak, ağ bant genişliği için RPO değerleri 15, 30 ve 60 dakika cinsinden hesaplanır hello gereklidir. Merhaba seçimi temel alınarak, etkilenen hello değerler hello sayfasında güncelleştirilir. Merhaba kullandıysanız *DesiredRPOinMin* değeri hello istenen RPO sonuçlarda gösterilen hello raporu, oluşturma sırasında parametre.

### <a name="profiling-overview"></a>Profil oluşturmaya genel bakış

![Merhaba dağıtım Planlayıcısı sonuçlarında profil oluşturma](./media/site-recovery-deployment-planner/profiling-overview.png)

**Toplam sanal makineleri profili**: hello profili verisini kullanılabilir sanal makineleri toplam sayısı. Merhaba VMListFile değil profili tüm VM'lerin adı varsa, bu VM'lerin hello rapor oluşturma dikkate alınmaz ve hello toplam profili VM'ler sayısını edilmez.

**Uyumlu sanal makinelere**: Merhaba korumalı tooAzure Site RECOVERY'yi kullanarak olabilir VM sayısı. Bunu hello toplam hangi hello için gerekli ağ bant genişliği, depolama hesabı sayısı, Azure çekirdek sayısı ve yapılandırma sunucuları ve ek işlem sunucuları sayısı hesaplanır uyumlu VM'ler sayısıdır. Merhaba ayrıntıları her uyumlu VM hello "Uyumlu VM'ler" bölümünde kullanılabilir.

**Uyumsuz sanal makineleri**: Merhaba Site Recovery ile koruma için uyumsuz profili VM sayısı. Uyumsuzluk Hello nedenlerle hello "Uyumsuz VM'ler" bölümünde belirtilmiştir. Merhaba VMListFile değil profili herhangi bir VM adlarını varsa, bu VM'lerin hello uyumsuz VM'ler sayısını hariç tutulur. Bu sanal makineleri hello "uyumsuz VM'ler" bölümünün hello sonunda "veri bulunamadı"olarak listelenir.

**İstenen RPO**: Dakika cinsinden istediğiniz kurtarma noktası hedefi. Merhaba rapor için üç RPO değerleri oluşturulur: 15 (varsayılan), 30-60 dakika. Merhaba bant genişliği öneri hello rapordaki hello sayfasının sağ hello üstünde hello istenen RPO aşağı açılan listesinde yaptığınız seçime göre değişir. Hello kullanarak, hello rapor oluşturulan durumunda *- DesiredRPO* özel bir değer parametresi, bu özel değer hello istenen RPO aşağı açılan listesinde hello varsayılan olarak gösterilir.

### <a name="required-network-bandwidth-mbps"></a>Gerekli ağ bant genişliği (Mb/sn)

![Merhaba dağıtım Planlayıcısı gerekli ağ bant genişliği](./media/site-recovery-deployment-planner/required-network-bandwidth.png)

**toomeet RPO hello süresinin yüzde 100:** hello önerilen toobe MB/sn cinsinden bant genişliği, istenen RPO toomeet hello süresinin yüzde 100 ayrılmış. Bu bant genişliği miktarını olmalıdır herhangi bir RPO ihlal tüm uyumlu VM'ler tooavoid kararlı durum değişim çoğaltması için ayrılmış.

**toomeet RPO yüzde 90'hello süre**: İstenen RPO hello süresinin yüzde 100 hello gerekli bant genişliği toomeet ayarlanamaz, geniş bant fiyatlandırma nedeniyle ya da herhangi bir nedenle toogo ayarını daha düşük bir bant genişliğine sahip karşılamak seçebileceğini, İstenen RPO yüzde 90'hello süre. Bu daha düşük bant genişliği ayarı toounderstand hello etkilerini, hello sayısını ve süresini RPO ihlalleri tooexpect üzerinde bir çözümlemeleri hello rapor sağlar.

**Arşivlenmiş verimlilik:** çalıştırdığınız hello GetThroughput komutu toohello Microsoft Azure bölgesini hello depolama hesabının bulunduğu hello sunucusundan hello işleme. Bu işleme sayı yapılandırma sunucusu veya işlem sunucusu depolama ve ağ özellikleri kalır sağlanan kullanarak Site Recovery uyumlu sanal makineleri aynı aynı hello hello koruduğunuzda, elde edebileceğiniz tahmini hello düzeyini gösterir Merhaba sunucu hello aracını çalıştırmanız gerekir.

Çoğaltma için hello önerilen bant genişliği toomeet hello RPO hello süresinin yüzde 100 ayarlamanız gerekir. Merhaba aracı tarafından raporlanan elde hello verimlilik, herhangi bir artış görmüyorsanız, hello bant genişliği'ni ayarladıktan sonra aşağıdaki hello yapın:

1. Toosee herhangi bir ağ, Site Recovery verimlilik sınırlama hizmet kalitesi (QoS) olup olmadığını denetleyin.

2. Site Recovery kasası hello fiziksel olarak desteklenen Microsoft Azure bölgesi toominimize ağ gecikmesini en yakın olup toosee denetleyin.

3. Yerel depolama özellikleri toodetermine hello donanım (örneğin, HDD tooSSD) artırabilir olup olmadığını denetleyin.

4. Merhaba işlem sunucusu Hello Site Recovery ayarları çok değiştirmek[hello tutar ağ bant genişliği çoğaltma için kullanılan artırmak](./site-recovery-plan-capacity-vmware.md#control-network-bandwidth).

Merhaba aracı yapılandırma sunucusu ya da sanal makineleri zaten korumalı işlem sunucusu çalıştırıyorsanız birkaç kez hello aracını çalıştırın. Merhaba verimlilik sayı değişiklikleri zamandaki o noktada işlenmekte olan karmaşası hello miktarını bağlı olarak elde.

Tüm kurumsal Site Recovery dağıtımları için [ExpressRoute](https://aka.ms/expressroute) kullanılması önerilir.

### <a name="required-storage-accounts"></a>Gerekli depolama hesapları
Tüm gerekli tooprotect olan grafik gösterir (standart ve premium) hello sayısı toplam depolama hesapları aşağıdaki hello uyumlu VM'ler hello. Her VM için hangi depolama hesabı toouse toolearn hello "VM depolama yerleştirme" bölümüne bakın.

![Gerekli depolama hesaplarında hello dağıtım Planlayıcısı](./media/site-recovery-deployment-planner/required-azure-storage-accounts.png)

### <a name="required-number-of-azure-cores"></a>Gerekli Azure çekirdek sayısı
Tüm yük devretme veya test yük devretme hello önce uyumlu VM'ler ayarlamanız çekirdek toobe toplam sayısı hello sonucudur. Çok az çekirdek hello abonelikte varsa, Site Recovery toocreate VM'ler hello aynı anda başarısız olur. yük devretme veya yük devretme testi.

![Merhaba dağıtım Planlayıcısı içinde Azure çekirdek sayısı](./media/site-recovery-deployment-planner/required-number-of-azure-cores.png)

### <a name="required-on-premises-infrastructure"></a>Gerekli şirket içi altyapısı
Bu şekil hello toplam sayısıdır yapılandırma sunucularına ve, tooprotect yeterli yapılandırılmış ek işlem sunucuları toobe tüm uyumlu VM'ler hello. Desteklenen hello bağlı olarak [boyut hello yapılandırma sunucusu için öneriler](https://aka.ms/asr-v2a-on-prem-components), hello aracı ek sunucular önerilir. hangisi ilk hello yapılandırma sunucusu veya hello ek işlem sunucusu isabet, Hello öneri hello hello gün başına karmaşası veya hello üst sınırını (VM başına üç disk ortalama varsayılarak) korumalı VM'lerin daha büyük temel alır. Her gün ve korumalı disklerin toplam sayısı toplam karmaşıklığa hello ayrıntılarını hello "Giriş" bölümünde bulabilirsiniz.

![Şirket içi altyapıda hello dağıtım Planlayıcısı](./media/site-recovery-deployment-planner/required-on-premises-infrastructure.png)

### <a name="what-if-analysis"></a>Benzetim analiz
Bu çözümleme, kaç tane ihlalleri hello süresinin yüzde 90'yalnızca istenen hello RPO toobe için daha düşük bir bant genişliği karşılanır ayarladığınızda dönemi profil hello sırasında gerçekleşebilir özetlenmektedir. Belirli bir günde bir veya daha fazla RPO ihlali ortaya çıkabilir. Merhaba grafik hello yoğun hello günün RPO gösterir.
Bu analize dayalı olarak, tüm gün ve yoğun günde isabet RPO arasında RPO ihlalleri hello sayısı ile kabul edilebilir ise hello daha düşük bant genişliği belirtilen karar verebilirsiniz. Kabul edilebilir ise, çoğaltma için hello daha düşük bant genişliği ayırma, başka önerilen toomeet hello RPO hello süresinin yüzde 100 istendiği gibi hello daha yüksek bant genişliği ayırma.

![Çözümlemeleri hello dağıtım Planlayıcısı içinde](./media/site-recovery-deployment-planner/what-if-analysis.png)

### <a name="recommended-vm-batch-size-for-initial-replication"></a>İlk çoğaltma için önerilen VM toplu iş boyutu
Bu bölümde, bant genişliği toomeet RPO ayarlanan hello süresinin yüzde 100 istenen hello hello ile 72 saat içinde paralel toocomplete hello ilk çoğaltma, korumalı VM'lerin sayısını önerilen öneririz. Bu değer yapılandırılabilir bir değerdir. toochange, rapor oluşturma zamanında kullanım hello *GoalToCompleteIR* parametresi.

Merhaba grafiği burada gösterir bant genişliği değerleri aralığı ve hello ortalama dayalı bir hesaplanan VM toplu iş boyutu sayısı toocomplete ilk çoğaltma 72 saat olarak algılanan VM boyutu tüm hello uyumlu VM'ler.

Merhaba genel önizlemede hello raporu hangi sanal makineleri bir toplu işlemde eklenmesi gereken belirtmiyor. Her sanal makinenin boyutu hello "uyumlu VM'ler" bölümü toofind gösterilen hello disk boyutu kullanın ve bunları toplu işlemi için seçin ya da bilinen iş yükü özellikler temelinde hello VM'ler seçebilirsiniz. Hello tamamlanma zamanı hello ilk çoğaltma değişiklikleri orantılı hello gerçek VM disk boyutuna göre kullanılan disk alanı ve kullanılabilir ağ verimliliği.

![Önerilen VM toplu iş boyutu](./media/site-recovery-deployment-planner/recommended-vm-batch-size.png)

### <a name="growth-factor-and-percentile-values-used"></a>Kullanılan büyüme faktörü ve yüzdelik değerler
Bu bölümde hello hello altındaki sayfa gösterir hello yüzdelik değer tüm hello performans sayaçlarının (varsayılan olarak 95) hello profili VM'ler için kullanılan ve hello büyüme faktörü (varsayılan değer yüzde 30) hesaplamalarının hello kullanılır.

![Kullanılan büyüme faktörü ve yüzdelik değerler](./media/site-recovery-deployment-planner/max-iops-and-data-churn-setting.png)

## <a name="recommendations-with-available-bandwidth-as-input"></a>Girdi olarak kullanılabilir bant genişliği ile ilgili öneriler

![Girdi olarak kullanılabilir bant genişliği ile ilgili öneriler](./media/site-recovery-deployment-planner/profiling-overview-bandwidth-input.png)

Site Recovery çoğaltması için x MB/sn’den fazla bant genişliği ayarlayamayacağınızı bildiğiniz bir durumla karşılaşabilirsiniz. Merhaba aracı tooinput kullanılabilir bant genişliği sağlar (kullanarak hello - bant genişliği parametre rapor oluşturma sırasında) ve ulaşılabilir RPO dakika cinsinden hello Al. Ulaşılabilir bir RPO değeri ile tooset ek bant genişliği yukarı gerekir ya da bu rpo'lu bir olağanüstü durum kurtarma çözümüne sahip olan Tamam olduğunu karar verebilirsiniz.

![500 MB/sn bant genişliği için elde edilebilen RPO](./media/site-recovery-deployment-planner/achievable-rpos.png)

## <a name="input"></a>Girdi
Merhaba giriş çalışma hello genel bir bakış VMware ortam profili sağlar.

![VMware ortamı hello genel bakış profili](./media/site-recovery-deployment-planner/Input.png)

**Başlangıç tarihi** ve **bitiş tarihi**: hello profil oluşturma rapor oluşturmak amacıyla kabul verilerini hello başlangıç ve bitiş tarihleri. Varsayılan olarak, hello başlangıç tarihi profil oluşturma başlatıldığında, başlangıç tarihidir ve hello bitiş tarihi başlangıç tarihi profil durduğunda. Bu parametrelerle Hello rapor oluşturulursa bu hello 'StartDate' ve 'EndDate' değerleri olabilir.

**Toplam sayısı gün Profil**: hello toplam arasında hello profil oluşturma gün sayısı başlangıç ve bitiş tarihleri hangi Merhaba rapor oluşturulur.

**Uyumlu sanal makine sayısı**: uyumlu VM'ler hangi gerekli hello ağ bant genişliği için toplam sayısını Merhaba, gereken sayıda depolama hesapları, Microsoft Azure çekirdek yapılandırma sunucularına ve ek işlem sunucusu hesaplanır.

**Uyumlu tüm sanal makineleri disklerde toplam sayısı**: hello biri olarak kullanılan hello numarası girdi yapılandırma sunucularına ve ek işlem sunucuları toobe hello dağıtımında kullanılan toodecide hello sayısı.

**Disk uyumlu sanal makine başına ortalama sayısı**: hello ortalama disk sayısı hesaplanan tüm uyumlu VM'ler arasında.

**Ortalama disk boyutu (GB)**: hello ortalama disk boyutu tüm uyumlu VM'ler üzerindeki hesaplanır.

**RPO (dakika) istenen**: ya da hello varsayılan kurtarma noktası hedefi veya hello geçirilen değer hello 'DesiredRPO' parametresi için rapor oluşturma tooestimate gerekli hello aynı anda bant genişliği.

**Bant genişliği (Mbps) istenen**: Merhaba rapor oluşturma tooestimate hello aynı anda hello 'Bant genişliği' parametresi için geçirilen değer elde edilebilir RPO.

**Gözlemlenen tipik veri dalgalanmasına (GB) günde**: hello ortalama veri dalgalanmasına gözlemlenen tüm profil gün boyunca. Bu sayı, hello girişleri toodecide hello yapılandırması sunucuların sayısını ve ek işlem sunucuları toobe hello dağıtımında kullanılan biri olarak kullanılır.


## <a name="vm-storage-placement"></a>VM-depolama yerleşimi

![VM-depolama yerleşimi](./media/site-recovery-deployment-planner/vm-storage-placement.png)

**Disk depolama türü**: tüm hello hello bahsedilen karşılık gelen VM'ler kullanılan tooreplicate olan herhangi bir standart veya premium depolama hesabı **VM'ler tooPlace** sütun.

**Önek önerilen**: hello depolama hesabını adlandırma için kullanılabilecek hello önerilen üç karakterli öneki. Kendi önek kullanabilirsiniz, ancak hello aracın öneri izleyen hello [depolama hesapları için adlandırma kuralı bölüm](https://aka.ms/storage-performance-checklist).

**Hesap adı önerilen**: hello önerilen önekini ekleyin sonra hello depolama hesabı adı. Merhaba adı içinde hello açılı ayraçları (< ve >) özel girişinizi ile değiştirin.

**Depolama hesabı oturum**: tüm hello çoğaltma günlükleri bir standart depolama hesabında depolanır. Bir ek bir standart depolama hesabı için günlük depolama tooa premium depolama hesabı çoğaltması VM'ler için ayarlayın. Tek bir standart kayıt depolama hesabı, birden fazla premium çoğaltma depolama hesabı tarafından kullanılabilir. Çoğaltılmış toostandard depolama hesaplarını kullanacak olan VM'ler hello günlükleri için aynı depolama hesabı.

**Günlük hesap adı önerilen**: hello önerilen önekini ekleyin sonra depolama günlük hesap adınız. Merhaba adı içinde hello açılı ayraçları (< ve >) özel girişinizi ile değiştirin.

**Yerleştirme Özet**: hello özetini hello depolama hesabı VM'lerin yükünü çoğaltma hello aynı anda toplam ve yük devretme veya yük devretme testi. Bu depolama hesabında, toplam yerleştirilen tüm VM'ler arasında IOPS yazma (Çoğaltma) IOPS, toplam kurulum boyutu tüm diskleri ve disk toplam sayısı, sanal makineleri eşlenen toohello depolama hesabı, toplam okuma/yazma hello toplam sayısını içerir.

**Sanal makineler tooPlace**: tüm listesini hello en iyi performans ve kullanım için depolama hesabı verilen hello yerleştirilmelidir VM'ler.

## <a name="compatible-vms"></a>Uyumlu VM’ler
![Uyumlu VM'lerin Excel elektronik tablosu](./media/site-recovery-deployment-planner/compatible-vms.png)

**VM adı**: VM adını veya bir rapor oluşturulduğunda hello VMListFile kullanılan IP adresini hello. Bu sütun, aynı zamanda ekli toohello VM'ler hello diskleri (VMDKs) listeler. toodistinguish vCenter VM'ler yinelenen adları veya IP adresleri ile Merhaba adlarını hello ESXi ana bilgisayar adını içerir. Merhaba listelenen ESXi hello bir dönem profil hello sırasında hello aracı tespit ettiğinizde burada hello VM yerleştirilen yöneticisidir.

**VM Uyumluluğu**: Değerler **Evet** ve **Evet**\* şeklindedir. **Evet** \* için hangi hello VM için uygun olan örnekleri [Azure Premium Storage](https://aka.ms/premium-storage-workload). Burada, yüksek karmaşası hello profili veya IOPS disk hello P20 veya P30 kategorideki uygun ancak hello hello diskin boyutunu P10 veya P20 tooa eşlenen toobe neden olur. Merhaba depolama hesabı, premium depolama disk tabanlı için boyutuna bir disk toomap yazın karar verir. Örneğin:
* <128 GB bir P10’dur.
* 128 GB too512 bir P20 GB'dir.
* 512 GB too1024 bir P30 GB'dir.
* 1025 bir P40 GB too2048 GB'dir.
* 2049 bir P50 GB too4095 GB'dir.

Bir disk Hello iş yükü özelliklerini put, bunu, hello P20 veya P30 kategori, ancak hello boyutu eşler, tooa alt premium depolama disk türü, hello aracı bu VM olarak işaretler **Evet**\*. Merhaba aracı ayrıca premium depolama disk türü önerilen hello hello kaynak disk boyutu toofit değiştirin ya da hello hedef disk türü yük devretme sonrasında değiştirmek, önerir.

**Depolama Türü**: Standart veya Premium.

**Önek önerilen**: hello üç karakterli depolama hesabı öneki.

**Depolama hesabı**: hello önerilen depolama hesabı öneki kullanan hello adı.

**R/W IOPS (ile büyüme faktörü)**: en yüksek iş yükü okuma/yazma IOPS hello diskteki hello (varsayılan olarak 95) hello gelecekteki büyüme faktörü dahil olmak üzere (varsayılan değer yüzde 30). Toplam okuma/yazma VM IOPS hello Not her zaman hello VM'in bağımsız diskler okuma/yazma IOPS hello toplamı değil, hello yoğun okuma/yazma hello VM IOPS hello Sum, tek tek disk hello yoğun olduğundan/IOPS hello dakikada sırasında okuma Profil oluşturma süresi.

**Veri karmaşıklığı MB/sn (ile büyüme faktörü) içinde**: hello yoğun karmaşıklık oranı hello disk üzerinde (varsayılan olarak 95) hello gelecekteki büyüme faktörü dahil olmak üzere (varsayılan değer yüzde 30). Bu hello Not toplam veri dalgalanmasına hello VM, her zaman hello VM'in bağımsız diskler veri dalgalanmasına hello toplamını hello yoğun veri dalgalanmasına hello VM, hello yoğun, tek tek disklerini karmaşası hello toplamı, her dönem profil hello dakikada olduğundan değil.

**Azure VM boyutu**: Bu VM şirket için ideal hello eşlenen Azure Cloud Services sanal makine boyutu. Merhaba eşleme hello şirket içi sanal makinenin bellek çekirdek/diskleri/NIC ve okuma/yazma IOPS sayısını temel alır. Merhaba her zaman tüm hello şirket içi VM özelliklerini eşleşen hello düşük Azure VM boyutu önerilir.

**Disk sayısı**: Merhaba hello VM üzerinde sanal makine disklerini (VMDKs) toplam sayısı.

**Disk boyutu (GB)**: Merhaba hello VM, tüm disklerin toplam kurulum boyutu. Hello aracı ayrıca hello VM hello bağımsız diskler için hello disk boyutunu gösterir.

**Çekirdek**: hello sayısı CPU çekirdeklerinin hello VM üzerinde.

**Bellek (MB)**: hello RAM hello VM üzerinde.

**NIC**: Merhaba hello VM NIC'ler sayısına.

**Önyükleme türü**: hello VM önyükleme türü. BIOS veya EFI olabilir. Şu anda Azure Site Recovery yalnızca BIOS önyükleme türünü destekler. EFI Önyükleme türündeki tüm hello sanal makineleri uyumsuz VM'ler çalışma sayfasında listelenir.

**İşletim sistemi türü**: hello hello VM işletim sistemi türü değil. Windows veya Linux ya da başka bir işletim sistemi olabilir.

## <a name="incompatible-vms"></a>Uyumsuz VM’ler

![Uyumsuz VM'lerin Excel elektronik tablosu](./media/site-recovery-deployment-planner/incompatible-vms.png)

**VM adı**: VM adını veya bir rapor oluşturulduğunda hello VMListFile kullanılan IP adresini hello. Bu sütun, aynı zamanda ekli toohello VM'ler hello VMDKs listeler. toodistinguish vCenter VM'ler yinelenen adları veya IP adresleri ile Merhaba adlarını hello ESXi ana bilgisayar adını içerir. Merhaba listelenen ESXi hello bir dönem profil hello sırasında hello aracı tespit ettiğinizde burada hello VM yerleştirilen yöneticisidir.

**VM Uyumluluk**: VM verilen hello neden Site Recovery ile kullanım için uyumsuz olduğunu gösterir. Merhaba nedenleri hello VM uyumsuz her disk için açıklanan ve temel üzerinde yayımlanan [depolama sınırları](https://aka.ms/azure-storage-scalbility-performance), hello aşağıdakilerden herhangi birini olabilir:

* Disk boyutu > 4095 GB’dir. Azure Depolama şu anda 4095 GB’den büyük veri diski boyutlarını desteklememektedir.
* İşletim sistemi diski >2048 GB'dir. Azure Depolama şu anda 2048 GB’den büyük işletim sistemi diski boyutunu desteklememektedir.
* Önyükleme türü EFI’dir. Şu anda Azure Site Recovery yalnızca BIOS önyükleme türündeki sanal makineleri destekler.

* Toplam VM boyutu (çoğaltma + TFO) desteklenen hello depolama hesabı boyut sınırını (35 TB) aşıyor. Merhaba maksimum desteklenen Azure veya Site kurtarma için sınırları standart depolama aşan bir performans karakteristiğini hello VM içinde tek bir diske sahip olduğunda bu uyumsuzluk genellikle oluşur. Bu tür bir örneğini hello VM hello premium depolama bölgeye iter. Ancak, desteklenen premium depolama hesabı 35 TB boyutta ve tek bir VM korumalı maksimum hello birden çok depolama hesaplarında korunamaz. Ayrıca korumalı bir VM üzerinde bir yük devretme testi çalıştırıldığında, hello çalıştığını unutmayın nerede çoğaltma İleri aşamalara aynı depolama hesabı. Bu örnekte, yük devretme toosucceed paralel olarak test etmek ve 2 x hello disk çoğaltma tooprogress için hello boyutunu ayarlayın.
* Kaynak IOPS, depolama IOPS için disk başına desteklenen 5000 limitini aşıyor.
* Kaynak IOPS, depolama IOPS için VM başına desteklenen 80.000 limitini aşıyor.
* Ortalama veri dalgalanmasına hello disk için ortalama g/ç boyutu 10 MB/sn desteklenen Site Recovery veri karmaşası sınırını aşıyor.
* Toplam veri dalgalanmasına hello VM üzerindeki tüm diskleri arasında VM başına 54 MBps hello maksimum desteklenen Site Recovery veri karmaşası sınırını aşıyor.
* Ortalama etkili yazma IOPS 840 disk için desteklenen hello Site kurtarma IOPS sınırını aşıyor.
* Hesaplanan anlık görüntü depolama, 10 TB desteklenen hello anlık görüntü depolama sınırını aşıyor.

**R/W IOPS (ile büyüme faktörü)**: hello diskteki hello en yüksek iş yükü IOPS (varsayılan olarak 95) hello gelecekteki büyüme faktörü dahil olmak üzere (varsayılan değer yüzde 30). Toplam okuma/yazma hello VM IOPS hello Not her zaman hello VM'in bağımsız diskler okuma/yazma IOPS hello toplamı değil, hello yoğun okuma/yazma hello VM IOPS hello Sum, tek tek disk hello yoğun olduğundan/IOPS hello dakikada sırasında okuma Profil oluşturma süresi.

**Veri karmaşıklığı MB/sn (ile büyüme faktörü) içinde**: hello yoğun karmaşıklık oranı diskteki hello gelecekteki büyüme faktörü (varsayılan 30 yüzde) dahil olmak üzere hello (varsayılan 95 yüzdebirlik). Bu hello Not toplam veri dalgalanmasına hello VM, her zaman hello VM'in bağımsız diskler veri dalgalanmasına hello toplamını hello yoğun veri dalgalanmasına hello VM, hello yoğun, tek tek disklerini karmaşası hello toplamı, her dönem profil hello dakikada olduğundan değil.

**Disk sayısı**: Merhaba hello VM üzerinde VMDKs toplam sayısı.

**Disk boyutu (GB)**: Merhaba hello VM, tüm disklerin toplam kurulum boyutu. Hello aracı ayrıca hello VM hello bağımsız diskler için hello disk boyutunu gösterir.

**Çekirdek**: hello sayısı CPU çekirdeklerinin hello VM üzerinde.

**Bellek (MB)**: hello RAM miktarının hello VM.

**NIC**: Merhaba hello VM NIC'ler sayısına.

**Önyükleme türü**: hello VM önyükleme türü. BIOS veya EFI olabilir. Şu anda Azure Site Recovery yalnızca BIOS önyükleme türünü destekler. EFI Önyükleme türündeki tüm hello sanal makineleri uyumsuz VM'ler çalışma sayfasında listelenir.

**İşletim sistemi türü**: hello hello VM işletim sistemi türü değil. Windows veya Linux ya da başka bir işletim sistemi olabilir.


## <a name="site-recovery-limits"></a>Site Recovery limitleri

**Çoğaltma depolama hedefi** | **Ortalama kaynak disk G/Ç boyutu** |**Ortalama kaynak disk veri değişim sıklığı** | **Günlük toplam kaynak disk veri değişim sıklığı**
---|---|---|---
Standart depolama | 8 KB | 2 Mb/sn | Disk başına 168 GB
Premium P10 disk | 8 KB | 2 Mb/sn | Disk başına 168 GB
Premium P10 disk | 16 KB | 4 Mb/sn | Disk başına 336 GB
Premium P10 disk | 32 KB veya daha büyük | 8 Mb/sn | Disk başına 672 GB
Premium P20 veya P30 disk | 8 KB  | 5 Mb/sn | Disk başına 421 GB
Premium P20 veya P30 disk | 16 KB veya daha büyük |10 Mb/sn | Disk başına 842 GB

Bunlar yüzde 30 G/Ç çakışmasını varsayan ortalama sayılardır. Site Recovery; çakışma oranı, büyük yazma boyutları ve gerçek iş yükü G/Ç davranışına göre daha yüksek aktarım hızını işleyebilir. Merhaba önceki numaraları tipik biriktirme listesi yaklaşık beş dakika varsayalım. Diğer bir deyişle, veriler karşıya yüklendikten sonra işlenir ve beş dakika içinde kurtarma noktası oluşturulur.

Bu limitler yaptığımız testleri temel alsa da mümkün olan tüm uygulama G/Ç birleşimlerini kapsamamaktadır. Gerçek sonuçlar, uygulamanızın G/Ç karışımına göre değişebilir. En iyi sonuçlar için dağıtım planlaması yaptıktan sonra bile, her zaman bir sınama yük devretme tooget hello true performans resmi kullanarak test kapsamlı uygulama gerçekleştirmek öneririz.

## <a name="updating-hello-deployment-planner"></a>Güncelleştirme hello dağıtım Planlayıcısı
tooupdate hello dağıtım Planlayıcısı aşağıdaki hello:

1. Hello hello en son sürümünü indirme [Azure Site Recovery dağıtımı Planlayıcısı](https://aka.ms/asr-deployment-planner).

2. Kopya hello .zip klasörü tooa toorun istediğiniz sunucu üzerinde.

3. Merhaba .zip klasöre ayıklayın.

4. Merhaba aşağıdakilerden birini yapın:
 * Merhaba en son sürümünü bir profil düzeltme içermiyor ve profil oluşturma hello Planlayıcısı geçerli sürümü üzerinde devam eden zaten ise, hello profil devam edin.
 * Merhaba en son sürümünü bir profil düzeltme içeriyorsa, bu, geçerli sürümü profil oluşturmayı durdurmak ve hello yeni sürümle hello profil yeniden başlatmanız önerilir.

  >[!NOTE]
  >
  >Böylece hello aracı profil verileri üzerinde ekler aynı çıkış dizini yolu hello yeni sürümle, geçişi hello profil başlattığınızda, varolan dosyaların hello. Eksiksiz profili veri olacaktır toogenerate hello rapor kullanılır. Farklı bir çıkış dizini geçirmezseniz, yeni dosyalar oluşturulur ve eski veri profili kullanılmaz toogenerate hello rapor.
  >
  >Her yeni dağıtım Planlayıcısı hello .zip dosyasının birikmeli bir güncelleştirmedir. Toocopy hello yeni dosyalar toohello önceki klasörü gerek yoktur. Yeni bir klasör oluşturup kullanabilirsiniz.


## <a name="version-history"></a>Sürüm geçmişi

### <a name="131"></a>1.3.1
Güncelleştirme: 19 Temmuz 2017

Aşağıdaki yeni özellik eklenmiştir:

* Rapor oluşturmaya büyük diskler (> 1 TB) için destek eklenmiştir. Artık dağıtım Planlayıcısı tooplan çoğaltma disk boyutları 1 TB'den (fazla 4095 GB) büyük olan sanal makineler için kullanabilirsiniz.
[Azure Site Recovery'de büyük disk desteği](https://azure.microsoft.com/en-us/blog/azure-site-recovery-large-disks/)


### <a name="13"></a>1.3
Güncelleştirme: 9 Mart 2017

Aşağıdaki yeni özellik eklenmiştir:

* Rapor oluşturma işlemine Yönetilen Disk desteği eklendi. Merhaba sanal makine sayısı tooa tek bir depolama yerleştirilebilir hesabıdır disk yönetiliyorsa göre hesaplanan yük devretme ve Test yük devretme için seçilmiş.        


### <a name="12"></a>1.2
Güncelleştirme: 7 Nisan 2017

Aşağıdaki düzeltmeler eklendi:

* Eklenen önyükleme hello sanal makine uyumlu veya uyumsuz hello koruma için ise her sanal makine toodetermine (BIOS veya EFI) denetle yazın.
* Eklenen OS hello uyumlu VM'ler her sanal makine için bilgi ve uyumsuz VM'ler çalışma yazın.
* Merhaba GetThroughput işlemi hello ABD devlet kurumları ve Çin Microsoft Azure bölgelerde artık desteklenmektedir.
* vCenter ve ESXi Server için birkaç tane daha ön koşul denetimi eklendi.
* Yanlış raporun üretildiği toonon İngilizce yerel ayarları ayarlandığında.


### <a name="11"></a>1.1
Güncelleştirme: 9 Mart 2017

Sorunları aşağıdaki sabit hello:

* Merhaba aracı VM'ler hello vCenter iki veya daha fazla VM'ler ile aynı adı veya IP adresi çeşitli ESXi ana bilgisayarları arasında hello varsa profil olamaz.
* Kopyalama ve arama hello uyumlu VM'ler ve uyumsuz VM'ler çalışma sayfaları için devre dışı bırakılmıştır.

### <a name="10"></a>1.0
Güncelleme: 23 Şubat 2017

Azure Site Recovery dağıtımı Planlayıcısı genel Önizleme 1.0 bilinen sorunlar (yaklaşan güncelleştirmelerinde ele toobe) hello aşağıdakileri içerir:

* Hyper V için Azure dağıtımları için VMware Azure senaryoları için yalnızca Hello aracı çalışır. Hyper V için Azure senaryolarının hello kullanmanız [Hyper-V kapasite planlayıcısı aracı](./site-recovery-capacity-planning-for-hyper-v-replication.md).
* Merhaba GetThroughput işlemi hello ABD devlet kurumları ve Çin Microsoft Azure bölgeleri desteklenmiyor.
* Merhaba aracı VM'ler hello vCenter sunucusu iki veya daha fazla VM'ler ile aynı adı veya IP adresi çeşitli ESXi ana bilgisayarları arasında hello varsa profil olamaz. Bu sürümde, yinelenen VM adlarını veya IP adresleri hello VMListFile profil hello aracı atlar. Merhaba geçici çözüm tooprofile hello VM'ler ESXi ana bilgisayar hello vCenter sunucusu yerine kullanmaktır. Her ESXi ana bilgisayarı için bir örnek çalıştırmanız gerekir.
