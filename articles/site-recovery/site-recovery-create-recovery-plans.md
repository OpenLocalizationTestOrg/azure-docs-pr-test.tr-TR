---
title: "Yük devretme ve kurtarma Azure Site kurtarma aaaCreate kurtarma planlarına | Microsoft Docs"
description: "Açıklar nasıl toocreate üzerinden Azure Site Recovery, toofail kurtarma planları özelleştirmek ve sanal makineleri ve fiziksel sunucuları kurtarma"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 72408c62-fcb6-4ee2-8ff5-cab1218773f2
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 09ca7719e92460b283947fdbe752e8654e5b9cab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-recovery-plans"></a>Kurtarma planları oluşturma


Bu makalede oluşturma ve kurtarma planları özelleştirme hakkında bilgiler sağlanmaktadır [Azure Site Recovery](site-recovery-overview.md).

Tüm yorumlarınızı ve sorularınızı bu makalenin veya hello hello altındaki sonrası [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

 Aşağıdaki kurtarma planları toodo hello oluşturun:

* Birlikte yük devri ve birlikte başlatma makine grupları tanımlayın.
* Model bağımlılıkları birlikte kurtarma gruplandırarak tarafından makineler arasında Grup planlayın. Örneğin, toofail üzerinden ve belirli bir uygulamayı oluşturan Getir, tüm hello VM'ler hello bu uygulamaya için Grup aynı kurtarma planı grup.
* Bir yük devretme çalıştırın. Bir test, planlanmış veya planlanmamış yük devretme bir kurtarma planı çalıştırabilirsiniz.


## <a name="create-a-recovery-plan"></a>Kurtarma planı oluşturma

1. Tıklatın **kurtarma planlarına** > **kurtarma planı oluşturma**.
   Merhaba kurtarma planı, kaynak ve hedef için bir ad belirtin. Merhaba kaynak konumu, sanal makineler, yük devretme ve kurtarma için etkinleştirilmiş olması gerekir.

    - VMM tooVMM çoğaltma için seçin **kaynak türü** > **VMM**ve kaynak ve hedef VMM sunucuların hello. Tıklatın **Hyper-V** korunan toosee bulut.
    - VMM tooAzure için seçin **kaynak türü** > **VMM**.  Select hello kaynak VMM sunucusunu ve **Azure** hello hedefi olarak.
    - (VMM olmadan) Hyper-V çoğaltma tooAzure için seçin **kaynak türü** > **Hyper-V sitesi**. Select hello site hello kaynağı olarak ve **Azure** hello hedefi olarak.
    - VMware VM veya fiziksel sunucu tooAzure şirket, bir yapılandırma sunucusu hello kaynağı olarak seçin ve **Azure** hello hedefi olarak.
    - Bir Azure tooAzure kurtarma planı için bir Azure bölgesi hello kaynağı olarak ve ikincil bir Azure bölgesi hello hedefi olarak seçin. yalnızca toowhich sanal makineleri korumalı Hello ikincil Azure bölgeleri şunlardır.
2. İçinde **sanal makine Seç**, hello sanal makineleri (veya çoğaltma grubu) seçin hello kurtarma planında tooadd toohello varsayılan grubu (Grup 1) istiyor.

## <a name="customize-and-extend-recovery-plans"></a>Özelleştirme ve kurtarma planları genişletme

Özelleştirme ve kurtarma planları genişletir:

- **Yeni gruplar eklemek**— ek kurtarma planı gruplarını (tooseven) toohello varsayılan grubu ekleyin ve sonra daha fazla makine ya da çoğaltma grupları toothose kurtarma planı grupları ekleyin. Grupları, bunları eklediğiniz hello sırayla numaralandırılır. Yalnızca bir sanal makine ya da çoğaltma grubu bir kurtarma planı grubuna eklenebilir.
- **İşlemi el ile eklemek**— önce veya sonra bir kurtarma planı Grup çalıştırmak el ile yapılan eylemler ekleyebilirsiniz. Merhaba kurtarma planı çalıştığında hello işlemi el ile eklenen hello noktada durdurur. Bir iletişim kutusu hello el ile gerçekleştirilen işlemin tamamlandığını toospecify ister.
- **Bir komut dosyası eklemek**— önce veya sonra bir kurtarma planı Grup çalışan komut dosyaları ekleyebilirsiniz. Bir komut dosyası eklediğinizde, Eylemler hello grubu için yeni bir dizi ekler. Örneğin, Grup 1 öncesi adımları kümesini hello adıyla oluşturulur: Grup 1: öncesi adımları. Bu küme tüm öncesi adımları listelenir. Dağıtılan bir VMM sunucunuz varsa hello birincil sitede yalnızca bir komut dosyası ekleyebilirsiniz.
- **Azure runbook'ları ekleyin**— Azure runbook'ları içeren kurtarma planları genişletebilirsiniz. Örneğin, tooautomate görevler veya toocreate tek adımlı kurtarma. [Daha fazla bilgi edinin](site-recovery-runbook-automation.md).

## <a name="add-scripts"></a>Komut dosyaları ekleme

Kurtarma planlarınızı PowerShell komut dosyalarını kullanabilirsiniz.

 - Böylece Hello özel durumları düzgün biçimde işlenen komut dosyaları try-catch bloklarını kullandığınızdan emin olun.
    - Merhaba komut dosyasında bir özel durum ise, çalışmayı durdurur ve hello görev başarısız olarak gösterir.
    - Bir hata oluşursa hello betik, herhangi bir kalan parçası çalıştırmaz.
    - Planlanmamış bir yük devretme çalıştırdığınızda, bir hata oluşursa, hello kurtarma planı devam eder.
    - Planlanmış bir yük devretme çalıştırdığınızda, bir hata oluşursa, hello kurtarma planı durdurur. Toofix hello komut dosyası, beklendiği gibi çalışır onay ve çalıştırın gerek yeniden hello kurtarma planı.
- bir kurtarma planı betiği Hello Write-Host komutu çalışmıyor ve hello komut dosyası başarısız olur. toocreate çıkışı, sırayla ana komut çalıştıran bir proxy komut dosyası oluşturun. Tüm çıktı hello kullanarak varsayılır emin olun >> komutu.
  * 600 saniye içinde döndürmezse hello komut dosyası zaman aşımına uğradı.
  * Herhangi bir şey tooSTDERR yazılmışsa hello betiği başarısız olarak sınıflandırılır. Bu bilgiler hello komut dosyası yürütme ayrıntılar görüntülenir.

Dağıtımınızda VMM kullanıyorsanız:

* Komut dosyaları bir kurtarma planı hello hello VMM hizmet hesabı bağlamında çalışır. Bu hesap hello uzak paylaşımı üzerinde hangi hello betik bulunduğu için Okuma izinlerine sahip olduğundan emin olun. Merhaba betik toorun hello VMM hizmet hesabı ayrıcalık düzeyi adresindeki sınayın.
* VMM cmdlet'lerini Windows PowerShell modülündeki teslim edilir. Merhaba VMM konsolunu yüklediğinizde hello modülü yüklenir. Merhaba betik komutu aşağıdaki hello kullanarak kodunuzu içine yüklenebilir:
   - Import-Module-Name virtualmachinemanager. [Daha fazla bilgi edinin](https://technet.microsoft.com/library/hh875013.aspx).
* En az bir kitaplık sunucusu VMM dağıtımınızda olduğundan emin olun. Varsayılan olarak, hello kitaplık paylaşım yolu bir VMM sunucusunun yerel olarak hello hello klasör adıyla MSCVMMLibrary VMM sunucusu üzerinde bulunur.
    * Kitaplık paylaşım yolu uzaktan (veya yerel ancak MSCVMMLibrary ile paylaşılan) ise, hello paylaşımı aşağıdaki gibi yapılandırın (kullanarak \\libserver2.contoso.com\share\ bir örnek olarak):
      * Merhaba Kayıt Defteri Düzenleyicisi'ni açın ve çok gidin**HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\Azure Site Recovery\Registration**.
      * Merhaba değerini Düzenle **ScriptLibraryPath** ve olarak yerleştirme \\libserver2.contoso.com\share\. Belirtin tam FQDN hello. İzinleri toohello paylaşım konumunu belirtin.
      * Merhaba betik aynı hello sahip bir kullanıcı hesabıyla test ettiğinizden emin olun VMM hello gibi izinleri hizmet hesabı. Bu, tek başına denetler sınanan komut dosyalarını çalıştır Merhaba, aynı, Kurtarma planları şekilde göründükleri gibi. Merhaba VMM sunucusunda hello yürütme İlkesi toobypass aşağıdaki gibi ayarlayın:
        * Yükseltilmiş ayrıcalıklar kullanarak hello 64-bit Windows PowerShell konsolu açın.
        * Tür: **Set-executionpolicy bypass**. [Daha fazla bilgi edinin](https://technet.microsoft.com/library/ee176961.aspx).

## <a name="add-a-script-or-manual-action-tooa-plan"></a>Bir komut dosyası veya el ile işlem tooa plan Ekle

Sanal makineler veya çoğaltma gruplarına tooit eklenir ve hello planı oluşturuldu sonra bir komut dosyası toohello varsayılan kurtarma planı grup ekleyebilirsiniz.

1. Açık hello kurtarma planı.
2. Merhaba bir öğeyi tıklatın **adım** listeleyin ve ardından **betik** veya **el ile eylemi**.
3. Toowant tooadd hello betik veya eylem önce veya sonra hello öğesi seçili olup olmadığını belirtin. Kullanım hello **Yukarı Taşı** ve **Aşağı Taşı** düğmeleri, toomove hello hello komut dosyası konumunu yukarı veya aşağı.
4. VMM komut dosyası eklerseniz, seçin **yük devretme tooVMM betik**. İçinde **betik yolu**, türü hello göreli yol toohello paylaşımı. Merhaba VMM aşağıdaki örnekte, hello yolu belirtin: **\RPScripts\RPScript.PS1**.
5. Defterini çalıştır bir Azure Otomasyonu eklerseniz, hangi hello runbook bulunduğu ve select hello uygun Azure runbook betiğidir hello Azure Automation hesabını belirtin.
6. Merhaba kurtarma planı yük devretmesi yapmak için toomake emin hello betiği beklendiği gibi çalışır.


### <a name="add-a-vmm-script"></a>VMM komut ekleme

Bir VMM kaynak site varsa, hello VMM sunucusunda bir komut dosyası oluşturabilir ve kurtarma planınıza dahil.

1. Yeni bir klasör hello kitaplık paylaşımı oluşturun. Örneğin, \<Vmmsunucusuadı > \MSSCVMMLibrary\RPScripts. Merhaba kaynağında yerleştirin ve VMM sunucuyu hedefleyebilir.
2. Merhaba komut dosyası (örneğin RPScript) oluşturabilir ve beklendiği gibi çalıştığını denetleyin.
3. Merhaba betik hello konuma yerleştirin \<Vmmsunucusuadı > merhaba kaynak ve hedef VMM sunucularında \MSSCVMMLibrary.


## <a name="next-steps"></a>Sonraki adımlar

[Daha fazla bilgi edinin](site-recovery-failover.md) yük devretme işlemleri çalıştırma hakkında.
