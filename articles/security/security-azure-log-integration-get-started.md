---
title: "aaaGet başlatılan ile Azure günlük tümleştirme | Microsoft Docs"
description: "Nasıl tooinstall hello Azure tümleştirme hizmeti oturum ve Azure depolama, Azure denetim günlükleri ve Azure Güvenlik Merkezi uyarılarını günlüklerinden tümleştirmek öğrenin."
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 53f67a7c-7e17-4c19-ac5c-a43fabff70e1
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ums.workload: na
ms.date: 07/26/2017
ms.author: TomSh
ms.custom: azlog
ms.openlocfilehash: 26c19070d76ff73b1bdbd32ba77fb04978af387e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-log-integration-with-azure-diagnostics-logging-and-windows-event-forwarding"></a>Azure tanılama günlüğü ve Windows Olay iletme Azure günlük tümleştirme
Azure günlük tümleştirme (AzLog), şirket içi güvenlik bilgileri ve Olay yönetimi (SIEM) sistemlere toointegrate ham Azure kaynaklarınızı günlüklerinden sağlar. Bu tümleştirme olası toohave tüm varlıklar için birleştirilmiş güvenlik Pano kolaylaştırır, şirket içi veya hello bulutta araya getirebilirsiniz böylece ilişkilendirmek, çözümlemek ve uygulamalarınız ile ilişkili güvenlik olayları için uyarı.
>[!NOTE]
Azure günlük tümleştirme hakkında daha fazla bilgi için hello gözden geçirebilirsiniz [Azure günlük tümleştirmesine genel bakış](https://docs.microsoft.com/azure/security/security-azure-log-integration-overview).

Bu makalede Azure günlük tümleşme hello hello Azlog service yüklemesinde odaklanma ve hello hizmeti ile Azure tanılama tümleştirme başlamanıza yardımcı olur. Hello Azure günlük tümleştirme hizmeti ardından mümkün toocollect hello Windows Güvenlik olay kanalı Azure Iaas dağıtılan sanal makinelerden Windows olay günlüğü bilgileri olacaktır. Bu çok benzer çok "Olay kullanmış yönlendirme" şirket içi.

>[!NOTE]
>Merhaba özelliği toobring hello toohello Azure günlük tümleştirmesine çıktısını SIEM hello SIEM kendisi tarafından sağlanır. Lütfen hello makalesine bakın [, şirket içi SIEM ile Azure günlük tümleştirme tümleştirme](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/) daha fazla bilgi için.

toobe açıkça - hello Azure günlük tümleştirme hizmeti çalıştıran hello Windows Server 2008 R2 kullanarak bir fiziksel veya sanal bilgisayar veya üzeri işletim sistemine (Windows Server 2012 R2 veya Windows Server 2016 tercih edilen).

Merhaba fiziksel bilgisayarı, şirket içi çalıştırabilirsiniz (veya bir barındırıcı sitesinde). Bir sanal makinede toorun hello Azure günlük tümleştirme hizmeti seçerseniz, bu sanal makine şirket içi olabilir veya Microsoft Azure gibi genel bulut.

Merhaba fiziksel veya hello Azure günlük tümleştirme hizmeti çalıştıran sanal makine ağ bağlantısı toohello Azure genel bulut gerektirir. Bu makaledeki adımları hello yapılandırma hakkında ayrıntılar sağlanmaktadır.

## <a name="prerequisites"></a>Ön koşullar
En azından aşağıdaki öğelerindeki hello AzLog hello yüklenmesini gerektirir:
* Bir **Azure aboneliği**. Bir aboneliğiniz yoksa [ücretsiz hesap](https://azure.microsoft.com/free/) için kaydolabilirsiniz.
* A **depolama hesabı** için Windows Azure tanılama günlük kullanılabilir (bir önceden yapılandırılmış depolama hesabı kullanın veya yeni bir tane oluşturun – biz nasıl tooconfigure hello depolama hesabı bu makalenin sonraki bölümlerinde gösterilmektedir)
  >[!NOTE]
  Senaryonuza bağlı olarak bir depolama hesabı gerekli olmayabilir. Merhaba Azure tanılama senaryo biri gereklidir bu makalede ele alınan.
* **İki sistem**: hello Azure günlük tümleştirme hizmeti çalışacak bir makine ve izlenecek ve toohello Azlog hizmet makine gönderilen kendi günlük bilgileri olan bir makineden.
   * Toomonitor – istediğiniz bir makine olarak çalışan bir VM budur bir [Azure sanal makine](../virtual-machines/virtual-machines-windows-overview.md)
   * Hello Azure günlük tümleştirme hizmeti çalışacak bir makine; Bu makineyi daha sonra SIEM içeri aktarılacak tüm hello günlük bilgi toplar.
    * Bu bir sistem şirket içi olabilir veya Microsoft Azure'da.  
    * X x64 çalıştıran toobe gereken Windows server 2008 R2 SP1 sürümü veya daha yüksek ve .NET 4.5.1'in yüklü olması. Merhaba .NET sürüm başlıklı aşağıdaki hello makalesiyle yüklü belirleyebilirsiniz [nasıl yapılır: belirlemek, .NET Framework sürümlerinin yüklendiğini](https://msdn.microsoft.com/library/hh925568)  
    Azure tanılama günlüğü için kullanılan bağlantı toohello Azure depolama hesabı olmalıdır. Biz bu makalenin sonraki bölümlerinde bu bağlantının nasıl onaylayabilirsiniz üzerinde talimatları içerir

Hello Azure portal kullanarak bir sanal makine oluşturma işleminin hello hızlı tanıtımı için aşağıda video hello göz atın.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Log-Integration-Videos-Create-a-Virtual-Machine/player]



## <a name="deployment-considerations"></a>Dağıtma konuları
Azure günlük tümleştirme test ederken hello en düşük işletim sistemi gereksinimlerini karşılayan sistemi kullanabilirsiniz. Ancak, bir üretim ortamında Merhaba veya ölçeklendirmeye yönelik tooplan yük gerektirebilir.

Olay birim yüksekse hello Azure günlük tümleştirme hizmeti (fiziksel veya sanal makine başına tek örnek) birden çok örneğini çalıştırabilirsiniz. Ayrıca, Azure Diagnostics depolama hesapları Windows (WAD) ve abonelikleri tooprovide toohello örneği hello sayısı için kapasite dayanmalıdır Bakiye yükleyebilirsiniz.
>[!NOTE]
Şu anda, biz belirli öneriler Azure örneklerini çıkışı tooscale tümleştirme makineler (yani, hello Azure günlük tümleştirme hizmeti çalışan sanal makineleri) oturum açtıklarında veya depolama hesapları ya da abonelik yok. Bu alanların her biri de, performans gözlemleri kararları ölçeklendirme dayanmalıdır.

Ayrıca performansı hello seçeneği tooscale'hello Azure günlük tümleştirme hizmeti toohelp yukarı vardır. Performans ölçümleri aşağıdaki hello toorun hello Azure günlük tümleştirme hizmeti seçtiğiniz hello makineler boyutlandırma yardımcı olabilir:
* Bir 8 işlemci (Temel) makinede Azlog Tümleştirici tek bir örneğini (~1M/hour) günde yaklaşık 24 milyon olay işleyebilir.

* 4 İşlemci (Temel) makinede Azlog Tümleştirici tek bir örneğini (~62.5K/hour) günde yaklaşık 1,5 milyon olayları işleyebilir.

## <a name="install-azure-log-integration"></a>Azure günlük tümleştirme yükleyin
tooinstall Azure günlük tümleştirme, gereksinim duyduğunuz toodownload hello [Azure günlük tümleştirme](https://www.microsoft.com/download/details.aspx?id=53324) yükleme dosyası. Merhaba Kurulum yordamı çalıştırın ve tooprovide telemetri bilgileri tooMicrosoft isteyip istemediğinize karar verin.  

![Yükleme ekran telemetri kutusu işaretli](./media/security-azure-log-integration-get-started/telemetry.png)

*
> [!NOTE]
> Microsoft toocollect telemetri verilerini izin öneririz. Bu seçenek kaldırarak telemetri veri koleksiyonunu devre dışı bırakabilirsiniz.
>


Hello Azure günlük tümleştirme hizmeti yüklü olduğu hello makineden telemetri verileri toplar.  

Toplanan telemetri verileri şöyledir:

* Azure günlük tümleştirme yürütülmesi sırasında oluşan özel durumlar
* Ölçümleri hello sayısı sorgular ve işlenen olayların hakkında
* Komut satırı seçenekleri hakkında hangi Azlog.exe kullanılan istatistikleri

Merhaba yükleme işlemi hello video aşağıda ele alınmıştır.
> [!VIDEO https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Log-Integration-Videos-Install-Azure-Log-Integration/player]



## <a name="post-installation-and-validation-steps"></a>Yükleme ve doğrulama adımlarını sonrası
Merhaba temel kurulum yordamı tamamladıktan sonra yükleme ve doğrulama hazır adım tooperform post adım uzaktasınız:
1. Yükseltilmiş bir PowerShell penceresi açın ve çok gidin**c:\Program Files\Microsoft Azure günlük tümleştirme**
2. tootake ihtiyacınız hello ilk AzLog cmdlet'leri içe tooget hello adımdır. Bunu hello komut dosyasını çalıştırarak yapabilirsiniz **LoadAzlogModule.ps1** (bildirim hello ". \" komutunu aşağıdaki hello içinde). Tür **.\LoadAzlogModule.ps1** ve basın **ENTER**.  
Aşağıdaki hello şekilde görünen gibi bir şey görmeniz gerekir. </br></br>
![Yükleme ekran telemetri kutusu işaretli](./media/security-azure-log-integration-get-started/loaded-modules.png) </br></br>
3. Şimdi tooconfigure AzLog toouse belirli bir Azure ortamı gerekir. Bir "Azure ortamı" Merhaba "" ile toowork istediğiniz Azure bulut veri merkezini türüdür. Şu anda birkaç Azure ortamı varken hello şu anda uygun seçenekleri olan **AzureCloud** veya **AzureUSGovernment**.   Yükseltilmiş PowerShell ortamınızda içinde olduğundan emin olun **c:\program files\Microsoft Azure günlük tümleştirme\** </br></br>
    Bir kez, hello komutu çalıştırın: </br>
    ``Set-AzlogAzureEnvironment -Name AzureCloud``(Azure ticari için)

      >[!NOTE]
      Merhaba komut başarılı olduğunda bir geri bildirim almazsınız.  Toouse hello US Government Azure bulut istiyorsanız, kullanacağınız **AzureUSGovernment** (için hello - adı değişkeni) hello ABD bulutu için. Diğer Azure Bulutları şu anda desteklenmiyor.  
4. Bir sistem izleyebilmeniz için Azure tanılama hello depolama hesabı kullanımda hello adı gerekir.  Hello Azure portalına gidin çok**sanal makineleri** ve hello sanal makine için izleyeceğiniz bakın. Merhaba, **özellikleri** bölümünde, seçin **tanılama ayarlarını**.  Tıklayın **Aracısı** ve belirtilen hello depolama hesabı adını not edin. Bu hesap adı, sonraki adım için gerekir.
![Azure tanılama ayarları](./media/security-azure-log-integration-get-started/storage-account-large.png) </br></br>

      ![Azure tanılama ayarları](./media/security-azure-log-integration-get-started/azure-monitoring-not-enabled-large.png)
      >[!NOTE]
      İzleme sırasında sanal makine oluşturma etkinleştirilmediyse hello seçeneği tooenable verilir, yukarıda gösterildiği gibi.
5. Şimdi biz bizim dikkat geri toohello Azure günlük tümleştirme makine geçiş yaparsınız. Azure günlük tümleştirme yüklendiği hello sisteminden bağlantı toohello depolama hesabına sahip tooverify ihtiyacımız var. Merhaba fiziksel bilgisayara veya hello Azure günlük hizmeti her hello yapılandırıldığı gibi Azure tanılama tarafından günlüğe kaydedilen toohello depolama hesabı tooretrieve bilgi erişimi gerektirir tümleştirme çalıştıran sanal makine sistemleri izlenen.  
  1. Azure Storage Gezgini indirebilirsiniz [burada](http://storageexplorer.com/).
  2. Merhaba Kurulum yordamı çalıştırma
  3. Tıklatın Hello yükleme işlemi tamamlandıktan sonra **sonraki** hello onay kutusunu bırakıp **başlatma Microsoft Azure Storage Gezgini** işaretli.  
  4. TooAzure oturum açın.
  5. Azure tanılama için yapılandırılmış hello depolama hesabı görebildiğini doğrulayın.  
![Depolama hesapları](./media/security-azure-log-integration-get-started/storage-account.jpg) </br></br>
   6. Depolama hesapları altında birkaç seçenek olduğuna dikkat edin. Bunlardan biri olan **tabloları**. Altında **tabloları** adlı görmelisiniz **WADWindowsEventLogsTable**. </br></br>
   ![Depolama hesapları](./media/security-azure-log-integration-get-started/storage-explorer.png) </br>

## <a name="integrate-azure-diagnostic-logging"></a>Azure tanılama günlük tümleştirme
Bu adımda, hello günlük dosyalarını içeren hello Azure günlük tümleştirme hizmeti tooconnect toohello depolama hesabı çalıştıran hello makine yapılandırır.
toocomplete birkaç Önden gerekir ki bu adımı.  
* **FriendlyNameForSource:** bu toohello depolama hesabı, Azure tanılama hello sanal makine toostore bilgilerinin yapılandırdığınız uygulayabilirsiniz kolay adıdır
* **StorageAccountName:** bu hello Azure diagnotics yapılandırdığınızda belirtilen hello depolama hesabının adıdır.  
* **Depolama anahtarı:** hello Azure tanılama bilgileri bu sanal makine için depolandığı hello depolama hesabının hello depolama anahtarı budur.  

Aşağıdaki adımları tooobtain hello depolama anahtarı hello gerçekleştirin:
 1. Toohello Gözat [Azure portal](http://portal.azure.com).
 2. ' Hello Azure Hello Gezinti bölmesinde konsolunda toohello alt'e gidin ve tıklatın **daha fazla hizmet.**

 ![Daha fazla hizmet](./media/security-azure-log-integration-get-started/more-services.png)
 3. Girin **depolama** hello içinde **filtre** metin kutusu. Tıklatın **depolama hesapları** (girdikten sonra bu görünür **depolama**)

   ![Filtre kutusuna](./media/security-azure-log-integration-get-started/filter.png)
 4. Depolama hesapları içeren bir liste görünür, çift tooLog depolama atanmış hello hesabına tıklayın.

   ![Depolama hesaplarının listesi](./media/security-azure-log-integration-get-started/storage-accounts.png)
 5. Tıklayın **erişim anahtarları** hello içinde **ayarları** bölümü.

  ![Erişim tuşları](./media/security-azure-log-integration-get-started/storage-account-access-keys.png)
 6. Kopya **key1** ve hello sonraki adımda erişmek için güvenli bir konuma yerleştirin.

   ![iki erişim tuşu](./media/security-azure-log-integration-get-started/storage-account-access-keys.png)
 7. Azure günlük tümleştirme yüklü hello sunucuda yükseltilmiş bir komut istemi (biz yükseltilmiş bir komut istemi penceresi burada kullandığınız Not, yükseltilmiş bir PowerShell konsol değil) açın.
 8. Çok gidin**c:\Program Files\Microsoft Azure günlük tümleştirme**
 9. ``Azlog source add <FriendlyNameForTheSource> WAD <StorageAccountName> <StorageKey> `` öğesini çalıştırın </br> Örneğin ``Azlog source add Azlogtest WAD Azlog9414 fxxxFxxxxxxxxywoEJK2xxxxxxxxxixxxJ+xVJx6m/X5SQDYc4Wpjpli9S9Mm+vXS2RVYtp1mes0t9H5cuqXEw==`` hello abonelik kimliği tooshow yukarı hello olay XML isterseniz, hello abonelik kimliği toohello kolay ad eklemek: ``Azlog source add <FriendlyNameForTheSource>.<SubscriptionID> WAD <StorageAccountName> <StorageKey>`` veya örneğin,``Azlog source add Azlogtest.YourSubscriptionID WAD Azlog9414 fxxxFxxxxxxxxywoEJK2xxxxxxxxxixxxJ+xVJx6m/X5SQDYc4Wpjpli9S9Mm+vXS2RVYtp1mes0t9H5cuqXEw==``

>[!NOTE]  
Too60 dakika bekleyin, sonra hello depolama hesabından çekilen hello olayları görüntüleyin. tooview, açık **Olay Görüntüleyicisi'ni > Windows Günlükleri > iletilen olaylar** hello Azlog Tümleştirici üzerinde.

Burada hello adımları giderek bir video yukarıda ele görebilirsiniz.
> [!VIDEO https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Log-Integration-Videos-Enable-Diagnostics-and-Storage/player]


## <a name="what-if-data-is-not-showing-up-in-hello-forwarded-events-folder"></a>Ne veri hello iletilen olaylar klasöründe göstermiyor?
Bir saat sonra veri hello göstermiyor ise **iletilen olaylar** klasörü, sonra:

1. Merhaba makine çalışan hello Azure günlük tümleştirme hizmeti denetleyin ve Azure erişebildiğinizden emin olun. tootest bağlantısı, try tooopen hello [Azure portal](http://portal.azure.com) hello tarayıcısından.
2. Emin hello kullanıcı hesabını **Azlog** hello klasörde yazma izni **users\Azlog**.
  <ol type="a">
   <li>Açık **Windows Gezgini** </li>
  <li> Çok gidin**c:\users** </li>
  <li> Sağ tıklayın **c:\users\Azlog** </li>
  <li> Tıklayın **güvenlik**  </li>
  <li> Tıklayın **NT Service\Azlog** ve hello hello hesap izinlerini denetleyin. Bu sekmeden Hello hesabı yoksa veya hello uygun izinleri şu anda değilseniz, gösteren hello hesap hakları bu sekmede verebilirsiniz.</li>
  </ol>
3.Merhaba komutta eklenen emin hello depolama hesabını **Azlog kaynağı Ekle** hello komutunu çalıştırdığınızda listelenen **Azlog kaynağı listesi**.
4. Çok Git**Olay Görüntüleyicisi'ni > Windows Günlükleri > Uygulama** herhangi bir hata varsa toosee hello Azure günlük entegrasyonunu bildirdi.


Merhaba yükleme ve yapılandırma sırasında herhangi bir sorunla çalıştırırsanız, lütfen açık bir [destek isteği](../azure-supportability/how-to-create-azure-support-request.md)seçin **günlük tümleştirme** destek isteyen hello hizmet olarak.

Başka bir destek seçeneği hello olan [Azure günlük tümleştirme MSDN Forumu](https://social.msdn.microsoft.com/Forums/home?forum=AzureLogIntegration). Burada hello topluluk birbirine sorular, yanıtlar, ipuçları ve püf noktaları nasıl tooget hello en Azure günlük tümleştirme dışında üzerinde destekleyebilir. Ayrıca, hello Azure günlük tümleştirme takım Bu forumda izler ve geçebiliriz her yardımcı olur.

## <a name="next-steps"></a>Sonraki adımlar
Azure günlük tümleştirme hakkında daha fazla toolearn belgeleri aşağıdaki hello bakın:

* [Microsoft Azure günlük tümleştirme Azure günlükleri için](https://www.microsoft.com/download/details.aspx?id=53324) – merkezi ayrıntılı bilgi için sistem gereksinimleri, yükleyip yönergeler Azure günlük tümleştirme.
* [Giriş tooAzure günlük tümleştirme](security-azure-log-integration-overview.md) – bu belgeyi tooAzure günlük tümleştirme, önemli işlevleri ve nasıl çalıştığı tanıtır.
* [Ortak yapılandırma adımları](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/) – bu blog gönderisine nasıl tooconfigure Azure oturum tümleştirme toowork Splunk, HP ArcSight ve IBM QRadar ile iş ortağı çözümlerini gösterir. Geçerli kılavuzumuzu nasıl tooconfigure hello SIEM bileşenleri üzerinde budur. SIEM satıcınıza ilk ek ayrıntılar için lütfen denetleyin.
* [Azure günlük sık sorulan sorular (SSS) tümleştirme](security-azure-log-integration-faq.md) -bu SSS Azure günlük tümleştirmesi hakkında sorular yanıtlanmaktadır.
* [Güvenlik Merkezi tümleştirme uyarıları Azure ile tümleştirme oturum](../security-center/security-center-integrating-alerts-with-log-integration.md) – bu belge size nasıl toosync Güvenlik Merkezi, sanal makine güvenlik olayları, günlük analizi ile Azure tanılama ve Azure etkinlik günlükleri tarafından toplanan birlikte uyarıları gösterir. veya SIEM çözümünden.
* [Azure tanılama ve Azure denetim günlükleri için yeni özellikler](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/) – bu blog gönderisine tooAzure denetim günlüklerini tanıtır ve yardımcı diğer özellikleri Azure kaynaklarınızı hello işlemlerini alın.
