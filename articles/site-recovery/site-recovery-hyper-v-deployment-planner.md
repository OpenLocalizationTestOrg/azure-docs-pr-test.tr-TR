---
title: "Hyper-V’den Azure’a Azure Site Recovery dağıtım planlayıcısı| Microsoft Docs"
description: "Bu belge, Hyper-V’den Azure’a dağıtım senaryosu için Azure Site Recovery dağıtım planlayıcısı kullanım kılavuzudur."
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
ms.date: 12/02/2017
ms.author: nisoneji
ms.openlocfilehash: 0baf595266e71fad2df16996d63af3ba7d23a6ac
ms.sourcegitcommit: 176c575aea7602682afd6214880aad0be6167c52
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/09/2018
---
# <a name="azure-site-recovery-deployment-planner-for-hyper-v-to-azure"></a>Hyper-V’den Azure’a Azure Site Recovery Dağıtım Planlayıcısı
Bu makale, Hyper-V’den Azure’a üretim dağıtımları için Azure Site Recovery Dağıtım Planlayıcısı kullanım kılavuzudur.

## <a name="overview"></a>Genel Bakış
Site Recovery kullanarak herhangi bir Hyper-V sanal makinesini (VM) korumaya başlamadan önce, istenen Kurtarma Noktası Hedefini (RPO) karşılayacak günlük veri değişikliği hızınıza göre yeterli bant genişliğini ve şirket içindeki her bir Hyper-V depolama biriminde yeterli boş alanı ayırmanız gerekir.

Ayrıca doğru tür ve sayıda hedef Azure depolama hesabı oluşturmanız gerekir. Zaman içinde artan kullanım nedeniyle kaynak üretim sunucularınızdaki büyümeyi hesaba katarak standart veya premium depolama hesapları oluşturun. Saniyede okuma/yazma G/Ç işlemi (IOPS) veya veri değişim sıklığı gibi iş yükü özelliklerine ve Azure Site Recovery limitlerine göre VM başına depolama türü seçin. 

Azure Site Recovery dağıtım planlayıcısı, şu anda hem Hyper-V’den Azure’a hem de VMware’den Azure’a olağanüstü durum kurtarma senaryoları için kullanılabilen bir komut satırı aracıdır. Başarılı çoğaltma ve yük devretme testine / yük devretmeye yönelik bant genişliği ve Azure depolama gereksinimlerini anlamak için, bu aracı kullanarak birden çok Hyper-V konağında bulunan Hyper-V sanal makinelerinizin profilini uzaktan oluşturabilirsiniz (herhangi bir üretim etkisi olmadan). Şirket içinde herhangi bir Azure Site Recovery bileşeni yüklemeden aracı çalıştırabilirsiniz. Ancak, elde edilen aktarım hızı sonuçlarını doğru şekilde almak için planlayıcıyı, Azure’da olağanüstü durum kurtarma korumasını etkinleştirmek için kullanacağınız Hyper-V sunucularıyla aynı donanım yapılandırmasına sahip bir Windows Server üzerinde çalıştırmanız önerilir. 

Araç aşağıdaki bilgileri sağlar:

**Uyumluluk değerlendirmesi**

* Disk sayısı, disk boyutu, IOPS, değişim sıklığı ve bazı VM özelliklerine göre VM uygunluk değerlendirmesi.

**Ağ bant genişliği ile RPO değerlendirmesi karşılaştırması**

* Delta çoğaltma için gereken tahmini ağ bant genişliği
* Azure Site Recovery’nin şirket içinden Azure’a alabileceği aktarım hızı
* Belirli bir bant genişliğinde ulaşılabilecek RPO
* Daha düşük bant genişliği sağlandığında istenen RPO üzerinde etki.

    
**Azure altyapı gereksinimleri**

* Her VM için depolama türü (standart veya premium depolama hesabı) gereksinimi
* Çoğaltma için ayarlanacak toplam standart ve premium depolama hesabı sayısı
* Azure Depolama kılavuzuna göre depolama hesabı adlandırma önerileri
* Tüm sanal makineler için depolama hesabı yerleşimi
* Abonelik üzerinde yük devretme testi veya yük devretme öncesinde ayarlanacak Azure çekirdek sayısı
* Şirket içindeki her VM için önerilen Azure VM boyutu

**Şirket içi altyapı gereksinimleri**
* Ürün uygulamalarınızın için istenmeyen biçimde kapalı kalmasına neden olmayacak VM çoğaltması sağlamak üzere ilk çoğaltma ve değişim çoğaltmasının başarılı olması için her bir Hyper-V depolama biriminde olması gereken boş depolama alanı
* Hyper-V çoğaltması için ayarlanabilecek en yüksek kopya sıklığı

**İlk çoğaltma işlem grubu oluşturma rehberi** 
* Koruma için kullanılacak VM batch sayısı
* Her batch’teki VM’lerin listesi
* Tüm batch’lerin korunma sırası
* Her batch’in ilk çoğaltmasının tahmini tamamlanma süresi

**Azure için tahmini DR maliyeti**
* Azure için tahmini DR maliyeti: işlem, depolama, ağ ve Azure Site Recovery lisans maliyeti
* VM başına ayrıntılı maliyet analiz



>[!IMPORTANT]
>
>Kullanım zaman içinde çoğalabileceğinden, önceki tüm araç hesaplamaları iş yükü özelliklerinde %30’luk bir büyüme olduğu varsayılarak ve tüm profil oluşturma ölçümlerinin (okuma/yazma IOPS, değişim hızı vb) yüzde 95’lik dilim değeri kullanılarak yapılır. Büyüme faktörü ve yüzdelik dilim hesaplaması öğelerinin her ikisi de yapılandırılabilir özelliktedir. Büyüme faktörü hakkında daha fazla bilgi almak için "Büyüme faktörü ile ilgili dikkat edilecek noktalar" bölümüne bakın. Yüzdelik dilim değeri hakkında daha fazla bilgi için "Hesaplama için kullanılan yüzdelik dilim değeri" bölümüne bakın.
>

## <a name="support-matrix"></a>Destek matrisi

| | **Vmware’den Azure’a** |**Hyper-V'den Azure'a**|**Azure'dan Azure'a**|**Hyper-V’den ikincil siteye**|**VMware’den ikincil siteye**
--|--|--|--|--|--
Desteklenen senaryolar |Evet|Evet|Hayır|Evet*|Hayır
Desteklenen Sürüm | vCenter 6.5, 6.0 veya 5.5| Windows Server 2016, Windows Server 2012 R2 | NA |Windows Server 2016, Windows Server 2012 R2|NA
Desteklenen yapılandırma|vCenter, ESXi| Hyper-V kümesi, Hyper-V konağı|NA|Hyper-V kümesi, Hyper-V konağı|NA|
Çalışan Azure Site Recovery Dağıtım Planlayıcısı örneği başına profili oluşturulabilecek sunucu sayısı |Tek (bir vCenter Server ve bir ESXi sunucusuna ait VM’lerin profili aynı anda oluşturulabilir)|Birden çok (birden çok konak veya konak kümesindeki sanal makinelerin profili tek seferde oluşturulabilir)| NA |Birden çok (birden çok konak veya konak kümesindeki sanal makinelerin profili tek seferde oluşturulabilir)| NA

*Bu araç, öncelikli olarak Hyper-V’den Azure’a olağanüstü durum kurtarma senaryosuna yöneliktir. Hyper-V’den ikincil olağanüstü durum kurtarmaya senaryosunda yalnızca gereken ağ bant genişliği, kaynak Hyper-V sunucuların her birinde gereken boş depolama alanı ve ilk çoğaltmadaki batch numaralarıyla batch açıklamaları gibi kaynak tarafı önerilerin anlaşılması için kullanılabilir.  Rapordaki Azure önerilerini ve maliyetleri dikkate almayın. Ayrıca Aktarım Hızı Alma işlemi, Hyper-V’den ikincil siteye olağanüstü durum kurtarma senaryosu için kullanılamaz.

## <a name="prerequisites"></a>Önkoşullar
Araç, Hyper-V için üç ana aşama içerir: VM listesini alma, profil oluşturma ve rapor oluşturma. Yalnızca aktarım hızını hesaplamaya yönelik dördüncü bir seçenek de mevcuttur. Farklı aşamaların çalıştırılacağı sunucuya ilişkin gereksinimler aşağıdaki tabloda verilmiştir:

| Sunucu gereksinimi | Açıklama |
|---|---|
|VM listesini alma, profil oluşturma ve aktarım hızı ölçümü |<ul><li>İşletim sistemi: Microsoft Windows Server 2016 veya Microsoft Windows Server 2012 R2 </li><li>Makine yapılandırması: 8 vCPU, 16 GB RAM, 300 GB HDD</li><li>[Microsoft .NET Framework 4.5](https://aka.ms/dotnet-framework-45)</li><li>[Visual Studio 2012 için Microsoft Visual C++ Yeniden Dağıtılabilir](https://aka.ms/vcplusplus-redistributable)</li><li>Bu sunucudan Azure’a İnternet erişimi</li><li>Azure depolama hesabı</li><li>Sunucu üzerinde yönetici erişimi</li><li>En az 100 GB boş disk alanı (30 günlük profili oluşturulmuş ve her biri ortalama üç diske sahip 1000 VM varsayıldığında)</li><li>Azure Site Recovery dağıtım planlayıcısı aracını çalıştırdığınız sanal makinenin, tüm Hyper-V sunucularının TrustedHosts listesine eklenmesi gerekir.</li><li>Tüm Hyper-V sunucularının profili oluşturulacak VM’lerinin, aracın çalıştırıldığı istemci VM’nin TrustedHosts listesine eklenmesi gerekir. [TrustedHosts listesine sunucu eklemek için daha fazla bilgi edinin](#steps-to-add-servers-into-trustedhosts-list). </li><li> Araç, PowerShell veya istemci üzerindeki komut satırı konsolu üzerinde yönetici ayrıcalığı ile çalıştırılmalıdır</ul></ul>|
| Rapor oluşturma | Microsoft Excel 2013 ve üzerinin yüklü olduğu herhangi bir Windows PC ya da Windows Server |
| Kullanıcı izinleri | VM listesini alma ve profil oluşturma işlemleri sırasında Hyper-V kümesine/Hyper-V konağına erişmek için kullanılacak yönetici hesabı.<br>Profili oluşturulması gereken tüm konakların, aynı kimlik bilgilerine sahip (kullanıcı adı ve parola) bir etki alanı yönetici hesabı olmalıdır
 |

## <a name="steps-to-add-servers-into-trustedhosts-list"></a>TrustedHosts listesine sunucu ekleme adımları
1.  Aracın dağıtılacağı VM’nin, TrustedHosts listesinde profili oluşturulacak tüm konaklara sahip olması gerekir. İstemciyi Trustedhosts listesine eklemek için aşağıdaki komutu VM’deki yükseltilmiş bir PowerShell üzerinden çalıştırın. VM, Windows Server 2012 R2 veya Windows Server 2016 olabilir. 

            set-item wsman:\localhost\Client\TrustedHosts -value <ComputerName>[,<ComputerName>]

2.  Profili oluşturulması gereken her Hyper-V Konağı aşağıdakilere sahip olmalıdır:

    a. Aracın TrustedHosts listesi içinde çalıştırılacağı VM. Hyper-V konağındaki yükseltilmiş bir PowerShell üzerinden aşağıdaki komutu çalıştırın.

            set-item wsman:\localhost\Client\TrustedHosts -value <ComputerName>[,<ComputerName>]

    b. Etkinleştirilmiş durumda PowerShell uzaktan iletişimi.

            Enable-PSRemoting -Force

## <a name="download-and-extract-the-deployment-planner-tool"></a>Dağıtım planlayıcısı aracını indirme ve ayıklama

1.  [Azure Site Recovery dağıtım planlayıcısı](https://aka.ms/asr-deployment-planner)’nın en son sürümünü indirin.
Araç bir zip klasöründe paketlenmiştir. Aynı araç hem VMware’den Azure’a hem de Hyper-V’den Azure’a olağanüstü durum kurtarma senaryolarını destekler. Bu aracı Hyper-V’den ikincil siteye olağanüstü durum kurtarma senaryoları için de kullanabilirsiniz. Ancak bu durumda, rapordaki Azure altyapısı önerilerini dikkate almayın.

2.  Zip klasörünü, aracı çalıştırmak istediğiniz Windows Server’a kopyalayın. Aracı Windows Server 2012 R2 veya Windows Server 2016 üzerinde çalıştırabilirsiniz. Sunucunun, profili oluşturulacak VM’leri içeren Hyper-V kümesine veya Hyper-V konağına bağlanması için ağ erişimi olması gerekir. Korumak istediğiniz Hyper-V sunucusu ve aracın çalıştırılacağı VM ile aynı donanım yapılandırmasına sahip olmanız önerilir. Bu tür bir yapılandırma, araç tarafından elde edildiği rapor edilen aktarım hızının, Azure Site Recovery tarafından profil oluşturma sırasında elde edilebilecek gerçek aktarım hızı ile eşleşmesini sağlar. Aktarım hızı hesaplaması, sunucu üzerinde kullanılabilir ağ bant genişliğine ve sunucunun donanım yapılandırmasına (CPU, depolama vb.) bağlıdır. Aktarım hızı, aracın Azure’a çalıştırıldığı sunucudan hesaplanır. Sunucunun donanım yapılandırması, Hyper-V sunucusundan farklı olursa, aracın elde edildiğini rapor ettiği aktarım hızı hatalı olur.
Önerilen VM yapılandırması: 8 vCPU, 16 GB RAM, 300 GB HDD.

3.  .zip klasörünü ayıklayın.
Klasör birden fazla dosya ve alt klasör içerir. Yürütülebilir dosya, üst klasördeki ASRDeploymentPlanner.exe dosyasıdır.

Örnek: .zip dosyasını E:\ sürücüsüne kopyalayıp ayıklayın. E:\ASR Deployment Planner_v2.1.zip

E:\ASR Deployment Planner_v2.1\ASRDeploymentPlanner.exe

### <a name="updating-to-the-latest-version-of-deployment-planner"></a>Dağıtım planlayıcısını en son sürüme güncelleştirme
Dağıtım planlayıcısının önceki sürümüne sahipseniz şunlardan birini yapın:
 * En son sürüm bir profil oluşturma düzeltmesi içermiyor ve profil oluşturma planlayıcının geçerli sürümünde devam ediyorsa, profil oluşturmaya devam edin.
 * En son sürüm bir profil oluşturma düzeltmesi içeriyorsa, geçerli sürümünüzde profil oluşturmayı durdurmanız ve profil oluşturma işlemini yeni sürümle yeniden başlatmanız önerilir.


  >[!NOTE]
  >
  >Yeni sürümle profil oluşturma işlemini başlattığınızda, aracın profil verilerini mevcut dosyalara iliştirebilmesi için aynı çıktı dizini yolunu geçirin. Raporu oluşturmak için profili oluşturulmuş verilerin tamamı kullanılır. Farklı bir çıktı dizininden geçerseniz, yeni dosyalar oluşturulur ve profili oluşturulmuş eski veriler rapor oluşturma işleminde kullanılamaz.
  >
  >Her yeni dağıtım planlayıcısı, .zip dosyasının toplu bir güncelleştirmesidir. En yeni dosyaları önceki klasöre kopyalamanız gerekmez. Yeni bir klasör oluşturup kullanabilirsiniz.

## <a name="version-history"></a>Sürüm geçmişi
En son ASR Dağıtım Planlayıcısı aracı sürümü 2.1’dir.
Her güncelleştirmede eklenen düzeltmeler için [ASR Dağıtım Planlayıcısı Sürüm Geçmişi](https://social.technet.microsoft.com/wiki/contents/articles/51049.asr-deployment-planner-version-history.aspx) sayfasına bakın.


## <a name="next-steps"></a>Sonraki adımlar
* [Dağıtım planlayıcısını çalıştırın](site-recovery-hyper-v-deployment-planner-run.md).