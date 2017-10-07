---
title: "Azure yedekleme: uygulama tutarlı Linux VM'ler yedeklerini | Microsoft Docs"
description: "Komut dosyaları tooguarantee uygulamayla tutarlı yedeklemeler tooAzure, Linux sanal makineleriniz için kullanın. Merhaba komut dosyaları yalnızca Resource Manager dağıtım tooLinux Vm'lerde uygulanır; Merhaba betikleri tooWindows VM'ler veya service manager dağıtımları geçerli değildir. Bu makalede hello komut dosyaları, sorun giderme dahil olmak üzere yapılandırma hello adımlarında alır."
services: backup
documentationcenter: dev-center-name
author: anuragmehrotra
manager: shivamg
keywords: "uygulamayla tutarlı yedekleme; Uygulama tutarlı Azure VM backup; Linux VM yedekleme; Azure yedekleme"
ms.assetid: bbb99cf2-d8c7-4b3d-8b29-eadc0fed3bef
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 4/12/2017
ms.author: anuragm;markgal
ms.openlocfilehash: d557dd973364d79bb4d8ce954f648de835dd345f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="application-consistent-backup-of-azure-linux-vms-preview"></a>Azure Linux VM'ler (Önizleme) uygulama tutarlı yedekleme

Bu makalede hello Linux öncesi betiği ve sonrası betik framework ve kullanılan tootake uygulama tutarlı Azure Linux VM'ler yedeklerini nasıl olabilir hakkında alınmaktadır.

> [!Note]
> Merhaba öncesi betiğini ve sonrası betik framework yalnızca Azure Resource Manager tarafından dağıtılan Linux sanal makineleri için desteklenir. Uygulama tutarlılığı için komut dosyalarını Service Manager tarafından dağıtılan sanal makineler ya da Windows sanal makineleri için desteklenmez.
>

## <a name="how-hello-framework-works"></a>Merhaba framework nasıl çalışır?

Hello framework VM anlık görüntülerini alırken sonrası komut dosyası ve bir seçenek toorun özel öncesi komut dosyaları sağlar. Öncesi komut dosyaları yalnızca hello VM anlık görüntü alın ve hello VM anlık alma hemen sonra sonrası komut dosyaları çalıştırılır önce çalıştırılır. VM anlık görüntülerini alırken, esneklik toocontrol uygulamanız ve ortamınız hello kazandırır.

Bu senaryoda, önemli tooensure uygulama tutarlı VM yedeğidir. Merhaba öncesi betiği uygulama yerel API'leri tooquiesce hello IOs çağırma ve bellek içi içerik toohello disk temizleme. Bu, başlangıç anlık görüntü uygulama tutarlı sağlar (diğer bir deyişle, bu Merhaba uygulaması ne zaman gelen VM önyüklendiğinde hello geri yükleme sonrası). Sonrası betik kullanılan toothaw hello IOs olabilir. Merhaba uygulaması normal işlemler post VM anlık görüntü devam edebilmeniz için uygulamanın yerel API'lerini kullanarak bunu yapar.

## <a name="steps-tooconfigure-pre-script-and-post-script"></a>Adımları tooconfigure öncesi betiği ve sonrası komut dosyası

1. Kök kullanıcı toohello tooback kurmak istediğiniz bir Linux VM hello olarak oturum açın.

2. Karşıdan **VMSnapshotScriptPluginConfig.json** gelen [GitHub](https://github.com/MicrosoftAzureBackup/VMSnapshotPluginConfig)ve toohello kopyalayın **/etc/azure** tooback giderek yukarı tüm hello vm'lerde klasör. Merhaba oluşturma **/etc/azure** zaten yoksa dizin.

3. Merhaba öncesi betiğini ve sonrası betik yukarı tooback planladığınız tüm hello VM'ler uygulamanız için kopyalayın. Merhaba VM üzerinde hello betikleri tooany konuma kopyalayabilirsiniz. Merhaba komut dosyalarında emin tooupdate hello tam yolunu hello olması **VMSnapshotScriptPluginConfig.json** dosya.

4. Aşağıdaki izinleri bu dosyalar için hello emin olun:

   - **VMSnapshotScriptPluginConfig.json**: izni "600." Örneğin, yalnızca "root" kullanıcı "Okuma" ve "yazma" izinleri toothis dosyası olmalıdır ve hiçbir kullanıcı "Yürütme izinleri" olması gerekir.

   - **Öncesi betiği**: izni "700."  Örneğin, yalnızca "root" kullanıcı olmalıdır "Okuma", "yazma" ve "izinleri toothis dosyayı Yürüt".
  
   - **Sonrası betik** izni "700." Örneğin, yalnızca "root" kullanıcı olmalıdır "Okuma", "yazma" ve "izinleri toothis dosyayı Yürüt".

   > [!Important]
   > Merhaba framework kullanıcılara çok fazla güç sağlar. Güvenli ve yalnızca "root" kullanıcı erişimi toocritical JSON ve komut dosyalarının bulunduğundan önemlidir.
   > Merhaba önceki gereksinimleri karşılanmadığı takdirde hello komut çalışmaz. Bu dosya sistemi/kilitlenme tutarlı yedekleme sonuçlanır.
   >

5. Yapılandırma **VMSnapshotScriptPluginConfig.json** burada açıklandığı gibi:
    - **pluginName**: Bu alanı olduğu gibi bırakın ya da komut dosyalarınızı beklendiği gibi çalışmayabilir.

    - **preScriptLocation**: hello o giderek toobe yedeklenen VM üzerinde hello öncesi komut hello tam yolunu girin.

    - **postScriptLocation**: hello o giderek toobe yedeklenen VM üzerinde hello sonrası komut hello tam yolunu girin.

    - **preScriptParams**: toohello öncesi komut iletilen toobe gereken hello isteğe bağlı parametreleri sağlamak. Tüm parametreleri tırnak içine olmalıdır ve birden çok parametre varsa virgülle ayrılmış olması gerekir.

    - **postScriptParams**: toohello sonrası komut iletilen toobe gereken hello isteğe bağlı parametreleri sağlamak. Tüm parametreleri tırnak içine olmalıdır ve birden çok parametre varsa virgülle ayrılmış olması gerekir.

    - **preScriptNoOfRetries**: hello kaç kez hello öncesi betiği yeniden varsa herhangi bir hata sonlandırmadan önce ayarlayın. Sıfır anlamına gelir tek deneyin ve bir hata olduğunda hiçbir yeniden deneyin.

    - **postScriptNoOfRetries**: hello kaç kez hello sonrası betik yeniden varsa herhangi bir hata sonlandırmadan önce ayarlayın. Sıfır anlamına gelir tek deneyin ve bir hata olduğunda hiçbir yeniden deneyin.
    
    - **SaniyeOlarakZamanAşımıSüresi**: hello öncesi betiği ve hello sonrası komut dosyası için tek tek zaman aşımları belirtin.

    - **continueBackupOnFailure**: Bu değeri çok ayarlayın**true** Azure yedekleme toofall geri tooa dosya sisteminin tutarlı/kilitlenme tutarlı yedekleme öncesi betik istiyorsanız veya sonrası komut dosyası başarısız olur. Bu çok ayarı**false** başarısız hello yedekleme (dışında tek disk VM bu ayardan bağımsız olarak döner geri toocrash tutarlı yedekleme olduğunda) komut dosyası hatası durumunda.

    - **fsFreezeEnabled**: hello VM anlık görüntü tooensure dosya sistemi tutarlılığı alırken, Linux fsfreeze adlı olup olmadığını belirtin. Bu ayar çok ayarlamak tutma öneririz**true** uygulamanız fsfreeze devre dışı bırakma bir bağımlılık olmadıkça.

6. Merhaba betik framework artık yapılandırılmıştır. Merhaba VM yedekleme zaten yapılandırılmışsa hello sonraki yedekleme hello betikleri çağırır ve uygulama tutarlı yedekleme tetikler. Merhaba VM yedekleme yapılandırılmamışsa, kullanarak yapılandırma [tooRecovery Hizmetleri kasalarını Azure sanal makineleri yedekleyin.](https://docs.microsoft.com/azure/backup/backup-azure-vms-first-look-arm)

## <a name="troubleshooting"></a>Sorun giderme

Öncesi betiği ve sonrası komut dosyası yazılırken uygun günlük ekleyin ve komut dosyası günlükleri toofix betik sorunları gözden emin olun. Komut dosyası çalıştırarak sorunlarını yaşamaya devam ediyorsanız, aşağıdaki tablonun daha fazla bilgi için toohello bakın.

| Hata | Hata iletisi | Önerilen eylem |
| ------------------------ | -------------- | ------------------ |
| Öncesi ScriptExecutionFailed |Yedekleme uygulama tutarlı olmayabilir şekilde hello öncesi komut dosyası bir hata döndürdü. | Komut dosyası toofix hello sorununuzu için hello hata günlüklerine bakın.|  
|   POST ScriptExecutionFailed |    Merhaba sonrası betik uygulama durumunu etkileyebilecek bir hata döndürdü. |  Komut dosyası toofix hello sorununuzu için hello hata günlüklerine bakın ve hello uygulama durumunu denetleyin. |
| Öncesi ScriptNotFound |  Merhaba öncesi betik hello belirtilen hello konumda bulunamadı **VMSnapshotScriptPluginConfig.json** yapılandırma dosyası. | Yapma emin bu öncesi betiği hello yapılandırma dosyası tooensure uygulama tutarlı yedekleme içinde belirtilen hello yolunda bulunur.|
| POST ScriptNotFound | Merhaba sonrası betik hello belirtilen hello konumda bulunamadı **VMSnapshotScriptPluginConfig.json** yapılandırma dosyası. | Yapma emin bu sonrası betik hello yapılandırma dosyası tooensure uygulama tutarlı yedekleme içinde belirtilen hello yolunda bulunur.|
| IncorrectPluginhostFile | Merhaba **Pluginhost** hello VmSnapshotLinux uzantısı ile birlikte gelen, dosya bozuk, böylece öncesi betiği ve sonrası komut dosyası çalışamaz ve hello yedekleme uygulama tutarlı olmayacak.   | Merhaba kaldırma **VmSnapshotLinux** uzantısı ve onu otomatik olarak yeniden yüklenir hello sonraki yedekleme toofix hello sorun. |
| IncorrectJSONConfigFile | Merhaba **VMSnapshotScriptPluginConfig.json** dosyasıdır yanlış, bu nedenle öncesi betiği ve sonrası komut dosyası çalışamaz ve hello yedekleme uygulama tutarlı olmayacak. | Merhaba kopyadan karşıdan [GitHub](https://github.com/MicrosoftAzureBackup/VMSnapshotPluginConfig) ve yeniden yapılandırın. |
| InsufficientPermissionforPre-komut dosyası | Komut dosyaları çalıştırmak için "Kök" kullanıcı hello dosyanın hello sahibi olmalı ve hello dosya "700" izinlere sahip olmaları gerekir (diğer bir deyişle, yalnızca "sahip" olmalıdır "Okuma", "yazma" ve "Yürütme izinleri"). | Merhaba komut dosyası "sahibi" hello "Kök" kullanıcı ve yalnızca "sahip" "Okuma", "yazma" ve "yürütme" izinleri olduğundan emin olun. |
| InsufficientPermissionforPost-komut dosyası | Komut dosyaları çalıştırmak için kök kullanıcının hello dosyanın hello sahibi olması gerekir ve hello dosya "700" izinlere sahip olmaları gerekir (diğer bir deyişle, yalnızca "sahip" olmalıdır "Okuma", "yazma" ve "Yürütme izinleri"). | Merhaba komut dosyası "sahibi" hello "Kök" kullanıcı ve yalnızca "sahip" "Okuma", "yazma" ve "yürütme" izinleri olduğundan emin olun. |
| Öncesi ScriptTimeout | Merhaba hello uygulama tutarlı yedekleme öncesi betik yürütme işlemi zaman aşımına uğradı. | Merhaba komut dosyasını denetleyin ve hello hello zaman aşımı artırmak **VMSnapshotScriptPluginConfig.json** konumunda bulunan dosya **/etc/azure**. |
| POST ScriptTimeout | Merhaba uygulama tutarlı yedekleme sonrası betik Hello yürütülmesi zaman aşımına uğradı. | Merhaba komut dosyasını denetleyin ve hello hello zaman aşımı artırmak **VMSnapshotScriptPluginConfig.json** konumunda bulunan dosya **/etc/azure**. |

## <a name="next-steps"></a>Sonraki adımlar
[VM yedekleme tooa kurtarma Hizmetleri kasası yapılandırma](https://docs.microsoft.com/azure/backup/backup-azure-arm-vms)
