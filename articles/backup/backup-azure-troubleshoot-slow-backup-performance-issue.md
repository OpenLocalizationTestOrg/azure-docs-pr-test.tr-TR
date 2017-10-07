---
title: "Dosya ve klasörleri Azure Yedekleme'de yavaş yedeğini aaaTroubleshoot | Microsoft Docs"
description: "Sağlayan Azure Backup performans sorunlarını hello nedenini tanılamak Kılavuzu toohelp sorun giderme"
services: backup
documentationcenter: 
author: genlin
manager: cshepard
editor: 
ms.assetid: e379180a-db13-4e0c-90e4-28e5dd6f5b14
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: genli
ms.openlocfilehash: 21d79bbd03c2706bc43fcc7c14020cffd6b919c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-slow-backup-of-files-and-folders-in-azure-backup"></a>Azure Backup’ta dosya ve klasörlerin yavaş yedekleme sorunlarını giderme
Bu makalede sorun giderme kılavuzu verilmiştir toohelp dosyalar ve klasörler için yavaş yedekleme performansını hello neden Azure yedekleme kullanırken tanılayın. Dosyaları hello Azure Yedekleme aracısı tooback kullandığınızda, hello yedekleme işlemi beklenenden daha uzun sürebilir. Bu gecikme bir veya daha fazlasını hello tarafından nedeni olabilir:

* [Yedeklenmekte hello bilgisayarda performans sorunları vardır.](#cause1)
* [Başka bir işlem veya virüsten koruma yazılımı ile hello Azure yedekleme işlemi engelliyor.](#cause2)
* [Merhaba Yedekleme aracısı, Azure sanal makine (VM) çalışıyor.](#cause3)  
* [Çok sayıda dosya (milyonlarca) yedekleme yapıyorsanız.](#cause4)

Karşıdan yükle ve hello yükleme sorunlarını giderme başlamadan önce öneririz [en son Azure Backup aracısını](http://aka.ms/azurebackup_agent). Biz sık güncelleştirmeler toohello yedekleme aracısını toofix çeşitli sorunları olun, özellikleri ekleyin ve performansı.

Ayrıca hello gözden geçirmenizi öneririz [Azure Backup hizmeti ile ilgili SSS](backup-azure-backup-faq.md) toomake, değil yaşıyorsunuz hello ortak yapılandırma sorunlardan biri emin.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

<a id="cause1"></a>

## <a name="cause-performance-bottlenecks-on-hello-computer"></a>Neden: Performans sorunları hello bilgisayarda
Performans sorunlarını yedeklenmekte hello bilgisayarda gecikmelere neden olabilir. Örneğin, bilgisayarın özelliği tooread veya yazma toodisk hello veya kullanılabilir bant genişliğini toosend veri hello ağ üzerinden performans sorunlarını neden olabilir.

Windows adlı yerleşik bir araç sağlar [Performans İzleyicisi](https://technet.microsoft.com/magazine/2008.08.pulse.aspx) (Perfmon) toodetect bu performans sorunlarını.

Bazı performans sayaçları ve en iyi yedeklemeler için performans sorunlarını tanılamada yararlı olabilir aralıkları aşağıda verilmiştir.

| Sayaç | Durum |
| --- | --- |
| Mantıksal Disk (Fiziksel Disk)--% boşta |• % 100 boşta too50% boşta Sağlıklı =</br>• %49 boşta too20% boşta uyarı veya İzleyici =</br>• % 19 boşta too0% boşta kritik veya dışı Spec = |
| Mantıksal Disk (Fiziksel Disk)--% Ort. Disk sn okuma veya yazma |• 0,001 ms too0.015 ms Sağlıklı =</br>• 0.015 ms too0.025 ms uyarı veya İzleyici =</br>• 0.026 ms veya kritik veya dışı Spec artık = |
| Mantıksal Disk (Fiziksel Disk)--geçerli Disk Sırası Uzunluğu (tüm örnekler) |6 dakikadan fazla için 80 istek |
| Bellek--olmayan havuzda bayt |• Tüketilen havuzu % 60'den Sağlıklı =<br>• % 61'i too80% tüketilen havuzunun uyarı veya İzleyici =</br>• Tüketilen % 80 havuzu büyük kritik veya dışı Spec = |
| Bellek--disk belleği havuzu bayt sayısı |• Tüketilen havuzu % 60'den Sağlıklı =</br>• % 61'i too80% tüketilen havuzunun uyarı veya İzleyici =</br>• Tüketilen % 80 havuzu büyük kritik veya dışı Spec = |
| Bellek--kullanılabilir megabayt |• kullanılabilir boş bellek % 50 veya daha iyi =</br>• 25 kullanılabilir boş bellek yüzdesi İzleyici =</br>• 10 kullanılabilir boş bellek yüzdesi uyarı =</br>• 100 MB veya kullanılabilir boş bellek % 5'den daha az önemli veya dışı Spec = |
| İşlemci--\%işlemci zamanı (tüm örnekler) |• % 60'den tüketilen Sağlıklı =</br>• % 61'i too90% tüketilen İzleyici veya uyarı =</br>• %91 too100% tüketilen kritik = |

> [!NOTE]
> Merhaba sorunlu hello altyapısıdır, öneririz, karar verirseniz daha iyi performans için düzenli aralıklarla hello diskleri birleştirin.
>
>

<a id="cause2"></a>

## <a name="cause-another-process-or-antivirus-software-interfering-with-azure-backup"></a>Neden: Başka işlem veya Azure yedekleme ile engellemesini virüsten koruma yazılımı
Diğer işlemlerin hello Windows Sistem hello Azure Yedekleme aracısı işlemi performansını olumsuz yönde burada etkilenen çeşitli örneklerine gördük. Örneğin, hello Azure Yedekleme aracısı ve verileri başka bir program tooback kullanıyorsanız veya virüsten koruma yazılımı çalışıyorsa ve dosyaları toobe üzerinde bir kilit yedeklenmiş olan hello dosyaları birden çok kilit çekişmesini neden olabilir. Bu durumda, hello yedekleme başarısız olabilir veya hello işi beklenenden daha uzun sürebilir.

Bu senaryoda en iyi öneri Hello hello Azure Yedekleme aracısı yedekleme zamanını hello değişip değişmediğini diğer yedekleme programı toosee tooturn hello kapalı olduğu. Genellikle, birden çok yedekleme işleri çalışmıyor emin hello sırasında yeterli tooprevent aynı zamandır birbirine etkilemesini bunları.

Virüsten koruma programları için hello aşağıdaki hariç olan öneririz dosyaları ve konumları:

* C:\Program Files\Microsoft Azure kurtarma Hizmetleri Agent\bin\cbengine.exe bir işlem olarak
* C:\Program Files\Microsoft Azure kurtarma Hizmetleri Agent\ klasörleri
* (Merhaba standart konumu değil kullanıyorsanız) konumu boş

<a id="cause3"></a>

## <a name="cause-backup-agent-running-on-an-azure-virtual-machine"></a>Neden: bir Azure sanal makine üzerinde çalışan yedekleme aracısı
Merhaba Backup Aracısı VM üzerinde çalıştırıyorsanız, performans, bir fiziksel makine çalıştırdığınızda yavaş olacaktır. Bu tooIOPS sınırlamaları beklenen bir durumdur.  Ancak, Premium depolama tooAzure yedeklenen hello veri sürücülerine geçiş yaparak hello performansını iyileştirebilirsiniz. Bu sorunu düzeltmeye çalışıyoruz ve hello düzeltme gelecekteki bir sürümde kullanılabilir olacaktır.

<a id="cause4"></a>

## <a name="cause-backing-up-a-large-number-millions-of-files"></a>Neden: Yedekleme dosyaları çok sayıda (milyonlarca)
Büyük miktarda veri taşıma daha küçük bir veri hacmi taşımaktan daha uzun sürer. Bazı durumlarda, yedekleme saati ile ilgili toonot yalnızca hello hello verileri, aynı zamanda hello sayısı dosya veya klasör boyutu. Bu özellikle true olduğunda küçük dosyalar milyonlarca (birkaç bayt tooa birkaç kilobayt) yedekleniyor.

Bu davranış hello verileri yedekleme ve tooAzure taşıma olsa da, Azure dosyalarınızı aynı anda katalog nedeniyle oluşur. Bazı nadir senaryolarda hello katalog işlemi beklenenden daha uzun sürebilir.

göstergeleri aşağıdaki hello hello performans sorunu anlamak ve uygun şekilde hello sonraki adımları çalışmanıza yardımcı olabilir:

* **UI hello veri aktarımı için ilerleme durumunu gösteren**. Merhaba veri hala aktarıldığı. Merhaba ağ bant genişliği veya verilerin hello boyutu gecikmelere neden.
* **Kullanıcı Arabirimi olmayan hello veri aktarımı için ilerleme durumu gösteren**. Açık hello günlükleri C:\Microsoft Azure kurtarma Hizmetleri Agent\Temp bulunan ve hello hello günlükleri FileProvider::EndData girişi için denetleyin. Bu girdi belirtir: hello veri aktarımı tamamlandı ve hello katalog işlemi gerçekleştiriliyor. Merhaba yedekleme işleri iptal etme. Bunun yerine, hello katalog işlemi toofinish için biraz daha uzun süre bekleyin. Merhaba sorun devam ederse, iletişim [Azure Destek](https://portal.azure.com/#create/Microsoft.Support).
