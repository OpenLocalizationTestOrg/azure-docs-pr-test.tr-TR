---
title: "Azure Automation aaaRunbook yürütme | Microsoft Docs"
description: "Azure automation'da bir runbook nasıl işleneceğini hello Ayrıntılar açıklanmaktadır."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: d10c8ce2-2c0b-4ea7-ba3c-d20e09b2c9ca
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/17/2017
ms.author: bwren
ms.openlocfilehash: bdb535675443353d44640bc7773de3f9dac5e42c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-execution-in-azure-automation"></a>Azure Otomasyonu Runbook yürütme
Azure Automation'da bir runbook başlattığınızda bir iş oluşturulur. Bir iş bir runbook tek yürütme örneğidir. Çalışan bir Azure Otomasyonu, her bir iş toorun atanmış. Çalışan birden çok Azure paylaştığı olsa da, farklı Automation hesapları işlerden birbirinden yalıtılır. İşiniz için hangi çalışan hizmetleri hello isteği üzerinde denetime sahip değil.  Tek bir runbook'ta aynı anda çalışan birden çok iş bulunabilir. Merhaba listesini hello Azure portalında görüntülediğinizde hello her runbook için başlatılan tüm işlerin durumunu listeler. Itanium tabanlı sistemler için sipariş tootrack hello durumu her içinde hello her runbook için iş listesini görüntüleyebilirsiniz. Merhaba farklı iş durumları açıklaması için bkz: [iş durumları](#job-statuses).

Merhaba Aşağıdaki diyagramda gösterilmiştir hello yaşam döngüsü için bir runbook işi [grafik runbook'lar](automation-runbook-types.md#graphical-runbooks) ve [PowerShell iş akışı runbook'ları](automation-runbook-types.md#powershell-workflow-runbooks).

![İş durumları - PowerShell iş akışı](./media/automation-runbook-execution/job-statuses.png)

Merhaba Aşağıdaki diyagramda gösterilmiştir hello yaşam döngüsü için bir runbook işi [PowerShell runbook'ları](automation-runbook-types.md#powershell-runbooks).

![İş durumları - PowerShell Betiği](./media/automation-runbook-execution/job-statuses-script.png)

Erişim tooyour Azure işleriniz sahip bir bağlantı tooyour Azure aboneliği yaparak kaynaklar. Bu kaynakları hello genel buluttan erişilebilir olması durumunda yalnızca erişim tooresources veri merkezinizde sahiptirler.

## <a name="job-statuses"></a>İş durumları
Merhaba aşağıdaki tabloda bir iş için olası farklı durumlarını hello açıklanmaktadır.

| Durum | Açıklama |
|:--- |:--- |
| tamamlandı |Merhaba işi başarıyla tamamlandı. |
| Başarısız oldu |İçin [grafik ve PowerShell iş akışı runbook'ları](automation-runbook-types.md), hello runbook toocompile başarısız oldu.  İçin [PowerShell Betiği runbook'ları](automation-runbook-types.md), hello runbook toostart başarısız oldu veya hello iş bir özel durumla karşılaştı. |
| Başarısız oldu, kaynaklar bekleniyor |Hello işi başarısız oldu hello ulaştığından [dengeli dağıtım](#fairshare) sınırlamak üç kez ve başlangıcı hello aynı denetim noktası veya hello her zaman hello runbook başlatın. |
| Sıraya alınmış |başlatılabilir böylece hello işin bir Otomasyon çalışan toocome üzerinde kullanılabilir kaynaklar için bekliyor. |
| Başlangıç |Merhaba iş tooa çalışan atandı ve bunu başlangıç hello işleminde hello sistemidir. |
| Devam ettirme |Merhaba sistem askıya alındıktan sonra hello işi hello işlemi devam ediyor. |
| Çalışıyor |Merhaba işi çalışıyor. |
| Çalıştıran, kaynaklar bekleniyor |Merhaba ulaştığından hello iş kaldırıldı [Orta paylaşımı](#fairshare) sınırı. Kısa bir süre sonra son denetim noktasından sürdürür. |
| Durduruldu |tamamlanmadan hello iş hello kullanıcı tarafından durduruldu. |
| Durduruluyor |Merhaba, hello işi durdurma, hello işleminde sistemidir. |
| askıya alındı |Merhaba iş hello kullanıcı, hello sistem veya hello runbook'taki bir komut tarafından askıya alındı. Askıya alınmış bir iş yeniden başlatılabilir ve en son denetim noktasından veya kontrol noktası yoksa hello hello runbook başlayan sürdürün. Merhaba runbook, yalnızca bir özel durum oluştuğunda hello sistem tarafından askıya alınır. Varsayılan olarak, ErrorActionPreference çok ayarlanır**devam**, o hello tutar işi bir hatayla anlamına gelir. Bu tercih değişkeni çok ayarlarsanız**durdurmak**, sonra da bir hata hello işini askıya alır.  Çok geçerlidir[grafik ve PowerShell iş akışı runbook'ları](automation-runbook-types.md) yalnızca. |
| Askıya alma |Merhaba sistem hello kullanıcı hello isteği toosuspend hello işi çalışıyor. Merhaba runbook, askıya alınmadan önce sonraki denetim noktasına erişmelidir. Askıya alınmadan önce tamamlandıktan sonra zaten en son denetim aktarılırsa.  Çok geçerlidir[grafik ve PowerShell iş akışı runbook'ları](automation-runbook-types.md) yalnızca. |

## <a name="viewing-job-status-from-hello-azure-portal"></a>Hello Azure Portalı'ndan işi durumunu görüntüleme
Tüm runbook işleri özetlenen durumunu görüntüleyin ya da belirli bir runbook işi hello Azure portal veya tümleştirme, Microsoft Operations Management Suite (OMS) günlük analizi çalışma alanı tooforward runbook iş durumu ile yapılandırarak ayrıntılarını ayrıntıya ve İş akışları.  OMS günlük analizi ile tümleştirme hakkında daha fazla bilgi için bkz: [Otomasyon tooLog analizi (OMS) iş durumu ve iş akışları iletmek](automation-manage-send-joblogs-log-analytics.md).  

### <a name="automation-runbook-jobs-summary"></a>Otomasyon runbook işleri özeti
Üzerinde Hello seçili Otomasyon hesabınızı sağında, tüm seçili bir Otomasyon hesabı altında için hello runbook işlerinin bir özetini görebilirsiniz **Proje istatistikleri** döşeme.<br><br> ![Proje istatistikleri döşeme](./media/automation-runbook-execution/automation-account-job-status-summary.png).<br> Bu kutucuğu sayısı ve grafik gösterimi yürütülen tüm işler hello iş durumunu görüntüler.  

Merhaba kutucuğa tıklandığında sunar hello **işleri** yürütülen tüm işler, durum, iş yürütme ve başlangıç ve tamamlanma sürelerini özetlenen bir listesini içeren dikey penceresi.<br><br> ![Otomasyon hesabı işler dikey](./media/automation-runbook-execution/automation-account-jobs-status-blade.png)<br><br>  Seçerek hello işlerin listesini filtreleyebilirsiniz **filtre işleri** ve belirli bir runbook, iş durumu, filtre veya tarih aralığı toosearch içinde hello aşağı açılan listeden hello.<br><br> ![Filtre iş durumu](./media/automation-runbook-execution/automation-account-jobs-filter.png)

Hello bu runbook seçerek belirli bir runbook için iş Özet Ayrıntıları alternatif olarak, görüntüleyebilirsiniz **Runbook'lar** dikey penceresinde, Automation hesabı ve ardından hello **işleri** döşeme.  Bu hello sunar **işleri** dikey penceresinde ve buradan hello iş kaydı tooview ayrıntılarını ve çıktısını tıklatabilirsiniz.<br><br> ![Otomasyon hesabı işler dikey](./media/automation-runbook-execution/automation-runbook-job-summary-blade.png)<br> 

### <a name="job-summary"></a>İş Özeti
Tüm belirli bir runbook ve en son durumlarını için oluşturulan hello işlerin bir listesini görüntüleyebilirsiniz. Bu listeyi iş durumuna göre filtre uygulayabilirsiniz ve hello tarih aralığına göre hello son toohello iş değiştirin. tooview, ayrıntılı bilgiler ve çıktıyı iş hello adını'ı tıklatın. Merhaba hello işin ayrıntılı görünümü toothat iş sağlanan hello runbook parametreleri için başlangıç değerlerini içerir.

Bir runbook için adımları tooview hello işleri aşağıdaki hello kullanabilirsiniz.

1. Hello Azure portal, seçin **Otomasyon** ve ardından bir Otomasyon hesabı hello adını seçin.
2. Merhaba hub'ından seçin **Runbook'lar** ve ardından hello **Runbook'lar** dikey penceresinde hello listeden bir runbook seçin.
3. Hello dikey penceresinde seçili hello runbook, hello tıklatın **işleri** döşeme.
4. Hello işleri hello listesinde birini tıklatın ve hello runbook işi ayrıntıları dikey penceresinde ayrıntılarını ve çıktısını görüntüleyebilirsiniz.

## <a name="retrieving-job-status-using-windows-powershell"></a>Windows PowerShell kullanarak iş durumunu alma
Merhaba kullanabilirsiniz [Get-AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx) belirli bir proje için bir runbook ve hello ayrıntıları oluşturulan tooretrieve hello işler. Windows PowerShell ile bir runbook başlatırsanız [başlangıç AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx), hello sonuçtaki işi verir. Kullanım [Get-AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx)çıkış tooget animasyonun bir proje çıktı.

Merhaba aşağıdaki örnek komutlar örnek bir runbook'un son işini hello almak ve durumunu, hello runbook parametreleri için sağlanan hello değerleri ve hello işinden çıkış hello görüntüler.

    $job = (Get-AzureRmAutomationJob –AutomationAccountName "MyAutomationAccount" `
    –RunbookName "Test-Runbook" -ResourceGroupName "ResourceGroup01" | sort LastModifiedDate –desc)[0]
    $job.Status
    $job.JobParameters
    Get-AzureRmAutomationJobOutput -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAcct" -Id $job.JobId –Stream Output

## <a name="fair-share"></a>Dengeli dağıtım
Sipariş tooshare kaynaklarında hello bulutta tüm runbook'lar arasında Azure Automation üç saat boyunca çalıştıktan sonra herhangi bir işi geçici olarak kaldıracak.  Bu süre boyunca işler [PowerShell tabanlı runbook'ları](automation-runbook-types.md#powershell-runbooks) durdurulur ve yeniden.  Merhaba iş durumu gösterir **durduruldu**.  Kontrol noktaları desteklemeyen beri bu tür bir runbook hello baştan her zaman yeniden başlatılır.  

[PowerShell iş akışı tabanlı runbook'ları](automation-runbook-types.md#powershell-workflow-runbooks) kendi sonuncudan sürdürülecek [denetim noktası](https://docs.microsoft.com/system-center/sma/overview-powershell-workflows#bk_Checkpoints).  Üç saat çalıştırdıktan sonra hello runbook işi hello hizmeti ve durumunu tarafından askıya alınacak gösterir **çalıştıran, kaynaklar bekleniyor**.  Bir korumalı alan kullanılabilir duruma geldiğinde hello runbook hello Otomasyon hizmeti ve sürdürür hello son denetim noktasından tarafından otomatik olarak başlatılır.  Askıya alma/yeniden başlatma için normal PowerShell iş akışı davranış budur.  Merhaba runbook yeniden çalışma zamanı, üç saatlik hello işlem yinelenir, toothree süreleri aşarsa.  Merhaba runbook hala tamamlanmadı üç saat sonra hello runbook işi başarısız oldu ve hello iş durumunu gösterir hello üçüncü yeniden başlatma işleminden sonra **kaynaklar bekleniyor başarısız**.  Bu durumda, özel durum hello başarısızlıkla aşağıdaki hello alırsınız.

*Merhaba işi art arda hello çıkarıldı çünkü çalıştıran devam edemiyor aynı denetim noktası. Runbook'unuzda durumuna kalıcı olmadan uzun işlemleri gerçekleştirmez emin olun.*

Bunlar mümkün toomake olmadığından bu tooprotect hello Tamamlanıyor, olmadan süresiz olarak runbook'ların çalışmasını hizmetidir onu yeniden kaldırılıyor olmadan toohello sonraki denetim.

Ardından Hello runbook herhangi bir denetim noktası varsa veya hello iş hello ilk denetim noktası kaldırıldığında önce ulaşmıştı değil, hello baştan başlatılır.  

Bir runbook oluşturduğunuzda, tüm etkinlikler iki kontrol noktaları arasında en fazla üç saat o hello zaman toorun emin olmalısınız. Bu bu üç saat sınırına ulaştığında ya da uzun süre sonu emin tooadd kontrol noktaları tooyour runbook tooensure gerekebilir işlemleri çalıştırma. Örneğin, runbook'unuz bir arat büyük bir SQL veritabanında gerçekleştirebilir. Bu tek bir işlem hello Orta içinde tamamlanmazsa paylaşımı sınırı sonra hello iş kaldırıldı ve hello baştan yeniden. Bu durumda, bir kerede bir tablo yeniden dizin oluşturmaya gibi birden çok adımlara hello arat işlemi bölmeniz ve böylece hello iş hello son işlemi toocomplete sonra devam her işlemden sonra bir denetim noktası ekleme gerekir.

## <a name="next-steps"></a>Sonraki adımlar
* toolearn kullanılan toostart Azure Automation runbook olabilecek daha hello farklı yöntemler hakkında bkz [Azure Otomasyonu runbook başlatma](automation-starting-a-runbook.md)

