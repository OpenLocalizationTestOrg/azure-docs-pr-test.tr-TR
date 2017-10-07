---
title: "Grafik Azure Automation runbook'ları işleme aaaError | Microsoft Docs"
description: "Bu makalede nasıl tooimplement hata Azure Automation grafik runbook mantığının işleme."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/26/2016
ms.author: magoedte
ms.openlocfilehash: b9ff01361d2ebd9c0174b074a7a290b1cc2fd1c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="error-handling-in-azure-automation-graphical-runbooks"></a>Azure Otomasyonu grafik runbook’larında hata işleme

Bir anahtar runbook tasarım asıl tooconsider bir runbook karşılaşabilirsiniz farklı sorunları tanımlamak için kullanılır. Bu sorunlar arasında başarı, beklenen hata durumları ve beklenmeyen hata koşulları sayılabilir.

Runbook’lar hata işleme özelliğini içermelidir. toovalidate etkinliğin çıktı hello veya grafik runbook'lar hatayla işlemek, bir Windows PowerShell kodunu aktivite kullanın, koşullu mantık hello etkinliğin çıktı bağlantıyı hello tanımlayın veya başka bir yöntem uygulayın.          

Genellikle, bir runbook etkinliğinden oluşur Sonlandırıcı olmayan bir hata varsa, aşağıdaki herhangi bir etkinlik hello hata bağımsız olarak işlenir. Merhaba hata, büyük olasılıkla toogenerate bir özel durum olmakla birlikte hello sonraki etkinliği toorun izin verilir. Bu PowerShell tasarlanmış toohandle hatalar olduğunu hello yoludur.    

yürütme sırasında oluşabilecek PowerShell hataları Hello türlerini sonlandırma veya Sonlandırıcı olmayan. sonlandırma ve sonlandırıcı olmayan hataları Hello farklarını aşağıdaki gibidir:

* **Hata sonlandırma**: hello komutu (veya komut dosyası yürütme) tamamen durdurur yürütme sırasında önemli bir hata. Örnek olarak mevcut olmayan cmdlet’ler, bir cmdlet’in çalışmasını önleyecek söz dizimi hataları veya diğer önemli hatalar verilebilir.

* **Olmayan sonlandırma hata**: yürütme toocontinue hello hatası rağmen izin veren ciddi olmayan bir hata oluştu. Örnek olarak bir dosyanın bulunamaması, hatalar ve izin sorunları yaşanması gibi işlemsel hatalar verilebilir.

Azure Otomasyonu grafik runbook hello yetenek tooinclude hata işleme ile geliştirilmiştir. Bundan böyle özel durumları sonlandırıcı olmayan hatalara dönüştürebilir ve etkinlikler arasında hata bağlantıları oluşturabilirsiniz. Bu işlem bir runbook yazarı toocatch hataları sağlar ve gerçekleştirilen veya beklenmeyen koşulları yönetin.  

## <a name="when-toouse-error-handling"></a>Zaman toouse hata işleme

Bir hata veya özel durum atar kritik bir etkinlik olduğunda, önemli tooprevent hello sonraki işleme ve toohandle hello hatadan runbook'unuzda uygun şekilde etkinliktir. Bu, özellikle de runbook’larınızın bir işletmeyi ya da hizmet işlemleri sürecini desteklediği durumlarda gereklidir.

Bir hata üretebilir her etkinlik için hello runbook yazarı tooany diğer etkinliklerin işaret eden bir hata bağlantı ekleyebilirsiniz.  Merhaba hedef etkinlik, bir cmdlet başka bir runbook çağırma çağırma kodu etkinlikler dahil olmak üzere herhangi bir türde, olması ve benzeri.

Ayrıca, hello hedef etkinlik giden bağlantıları da sağlayabilirsiniz. Bu bağlantılar normal bağlantılar veya hata bağlantıları olabilir. Merhaba runbook yazarı yeniden ayırma tooa olmadan karmaşık hata işleme mantığı uygulayabilirsiniz yani kod etkinlik. Merhaba toocreate ortak işlevselliği ile ayrılmış bir hata işleme runbook yöntemdir, ancak bu zorunlu değildir önerilir. Hata işleme mantığı öyle olmadığı bir PowerShell kodunu aktivite içinde hello yalnızca seçeneği.  

Örneğin, toostart çalışır bir runbook bir VM düşünün ve bir uygulamayı yükleyin. Merhaba VM doğru başlamazsa, iki eylemleri gerçekleştirir:

1. Bu sorun hakkında bir bildirim gönderir.
2. Bunun yerine otomatik olarak yeni bir VM sağlayan başka bir runbook başlatır.

Bir çözüm toohave tanıtıcıları bir adım tooan etkinlik işaret eden bir hata bağlantıdır. Örneğin, hello bağlantı kurulamadı **Write-Warning** hello gibi iki adımı için cmdlet tooan etkinlik **başlangıç AzureRmAutomationRunbook** cmdlet'i.

Birçok runbook'ları kullanmak için bu davranış generalize ayrı bir hata işleme runbook ve daha önce önerilen aşağıdaki hello kılavuz içinde bu iki etkinlik koyarak. Bu hata işleme runbook çağırmadan önce hello özgün runbook'taki hello verilerden özel bir ileti oluşturun ve bir parametre toohello hata işleme runbook geçirin.

## <a name="how-toouse-error-handling"></a>Nasıl toouse hata işleme

Her etkinliğin özel durumları sonlandırıcı olmayan hatalara dönüştürmeye yönelik bir yapılandırma ayarı vardır. Bu ayar varsayılan olarak devre dışıdır. Toohandle hataları istediğiniz herhangi bir etkinliğin bu ayarı etkinleştirmenizi öneririz.  

Bu yapılandırma etkinleştirerek hello etkinlik sonlandırma ve sonlandırıcı olmayan hataları Sonlandırıcı olmayan hata olarak ele alınır ve bir hata bağlantısıyla işlenebilir modemlerin.  

Bu ayar yapılandırdıktan sonra hello hata işleme bir etkinlik oluşturun. Bir etkinlik herhangi bir hata oluşturursa, bağlantılar ve ardından giden hata hello ve hello etkinlik de normal bir çıktı üretir olsa bile hello normal bağlantılar değildir.<br><br> ![Otomasyon runbook’u hata bağlantısı örneği](media/automation-runbook-graphical-error-handling/error-link-example.png)

Aşağıdaki örneğine hello bir runbook bir sanal makine hello bilgisayar adını içeren bir değişkeni alır. Daha sonra toostart hello sanal makine hello sonraki etkinliği ile çalışır.<br><br> ![Otomasyon runbook’u hata işleme örneği](media/automation-runbook-graphical-error-handling/runbook-example-error-handling.png)<br><br>      

Merhaba **Get-AutomationVariable** etkinlik ve **Start-AzureRmVm** yapılandırılmış tooconvert özel durumları tooerrors şunlardır.  Varsa VM hello değişken veya başlangıç alma sorunları hello sonra bir hata oluşturulmaz.<br><br> ![Otomasyon runbook’u hata işleme etkinlik ayarları](media/automation-runbook-graphical-error-handling/activity-blade-convertexception-option.png)

Hata bağlantıları akış bu etkinlikleri tooa tek **hata Yönetim** etkinliğine (kod etkinliği). Bu etkinlik hello kullanan basit bir PowerShell ifadesiyle yapılandırılmış *Throw* , bunların ile işleme anahtar sözcüğü toostop *$Error.Exception.Message* hello açıklayan tooget hello iletisi Geçerli özel durumu.<br><br> ![Otomasyon runbook’u hata işleme kod örneği](media/automation-runbook-graphical-error-handling/runbook-example-error-handling-code.png)


## <a name="next-steps"></a>Sonraki adımlar

* bağlantılar ve grafik runbook'lardaki bağlantı türleri hakkında daha fazla toolearn bkz [Azure Automation'da grafik yazma](automation-graphical-authoring-intro.md#links-and-workflow).

* toolearn hakkında daha fazla runbook yürütme toomonitor runbook işleri ve diğer teknik ayrıntıları görmek nasıl [bir runbook işi izlenemedi](automation-runbook-execution.md).
