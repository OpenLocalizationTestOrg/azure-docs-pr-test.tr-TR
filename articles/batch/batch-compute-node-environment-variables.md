---
title: "aaa \"Azure toplu işlem düğüm ortam değişkenleri | Microsoft Docs\""
description: "Düğüm ortam değişkeni başvurusu Azure toplu analizi için işlem."
services: batch
author: tamram
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 05/05/2017
ms.author: tamram
ms.openlocfilehash: 860f34b530579a81fbd5cf8ffa31df79d917c080
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-batch-compute-node-environment-variables"></a>Azure toplu işlem düğüm ortam değişkenleri
Merhaba [Azure Batch hizmeti](https://azure.microsoft.com/services/batch/) işlem düğümlerinde ortam değişkenleri aşağıdaki hello ayarlar. Bu ortam değişkenleri görev komut satırları ve hello programlar başvurusu yapabilir ve komut dosyaları tarafından hello komut satırları çalıştırmak.

Ortam değişkenleri Batch ile kullanma hakkında ek bilgi için bkz: [görevler için ortam ayarları](https://docs.microsoft.com/azure/batch/batch-api-basics#environment-settings-for-tasks).

## <a name="environment-variable-visibility"></a>Ortam değişkeni görünürlüğü

Bu ortam değişkenleri yalnızca hello bağlamında hello görünür **görev kullanıcı**, kullanıcı hesabı altında bir görev yürütüldüğünde hello düğümde hello. Şunları yapacaksınız *değil* bunlar olup, [uzaktan bağlanmak](https://azure.microsoft.com/documentation/articles/batch-api-basics/#connecting-to-compute-nodes) tooa işlem Uzak Masaüstü Protokolü (RDP) veya güvenli Kabuk (SSH) ve liste hello ortam değişkenleri aracılığıyla düğümü. Uzak bağlantı için kullanılan hello kullanıcı hesabı değil hello hello görev tarafından kullanılan hello hesabıyla aynı olmasıdır.

## <a name="command-line-expansion-of-environment-variables"></a>Ortam değişkenleri komut satırı genişletme

bir kabuk altında düğümleri çalıştırmayın Hello komut satırları üzerinde görevler tarafından yürütülen işlem. Bu nedenle, bu komut satırlarından ortam değişkeni genişletmesi gibi Kabuk özelliklerinden yerel alamıyor (Bu hello içerir `PATH`). tootake avantajı özelliklerden yapmanız gerekir **hello Kabuk çağırma** hello komut satırında. Örneğin, başlatma `cmd.exe` Windows işlem düğümleri veya `/bin/sh` Linux düğümleri üzerinde:

`cmd /c MyTaskApplication.exe %MY_ENV_VAR%`

`/bin/sh -c MyTaskApplication $MY_ENV_VAR`

## <a name="environment-variables"></a>Ortam değişkenleri

| Değişken adı                     | Açıklama                                                              | Kullanılabilirlik | Örnek |
|-----------------------------------|--------------------------------------------------------------------------|--------------|---------|
| AZ_BATCH_ACCOUNT_NAME           | Görev hello hello toplu işlem hesabının adını Hello ait.                  | Tüm görevler.   | mybatchaccount |
| AZ_BATCH_CERTIFICATES_DIR       | Bir dizin hello içinde [görev çalışma dizini] [ files_dirs] işlem düğümleri hangi sertifikaların Linux için depolanır. Bu ortam değişkenini tooWindows işlem düğümleri uygulanmaz unutmayın.                                                  | Tüm görevler.   |  /mnt/batch/Tasks/workitems/batchjob001/Job-1/task001/certs |
| AZ_BATCH_JOB_ID                 | Görev hello hello işin Hello kimliği ait. | Başlangıç görevi dışında tüm görevler. | batchjob001 |
| AZ_BATCH_JOB_PREP_DIR           | Merhaba iş hazırlama Hello tam yolunu [görev dizini] [ files_dirs] hello düğümde. | Başlangıç görevi ve iş hazırlama görevi dışında tüm görevler. Yalnızca hello işi bir iş hazırlama görevi ile yapılandırılmışsa, kullanılabilir. | C:\user\tasks\workitems\jobprepreleasesamplejob\job-1\jobpreparation |
| AZ_BATCH_JOB_PREP_WORKING_DIR   | Merhaba iş hazırlama Hello tam yolunu [görev çalışma dizini] [ files_dirs] hello düğümde. | Başlangıç görevi ve iş hazırlama görevi dışında tüm görevler. Yalnızca hello işi bir iş hazırlama görevi ile yapılandırılmışsa, kullanılabilir. | C:\user\tasks\workitems\jobprepreleasesamplejob\job-1\jobpreparation\wd |
| AZ_BATCH_NODE_ID                | Görev hello hello düğümün Hello kimliği atanır. | Tüm görevler. | Tvm 1219235766_3 20160919t172711z |
| AZ_BATCH_NODE_ROOT_DIR          | Tüm hello kök Hello tam yolunu [toplu dizinleri] [ files_dirs] hello düğümde. | Tüm görevler. | C:\user\tasks |
| AZ_BATCH_NODE_SHARED_DIR        | Merhaba Hello tam yolunu [paylaşılan dizine] [ files_dirs] hello düğümde. Bir düğümde yürütülen tüm görevler okuma/yazma erişimi toothis dizinine sahip. Diğer düğümlerinde yürütülen görevler (bunu bir "paylaşılan" ağ dizin değil) uzaktan erişim toothis dizin yok. | Tüm görevler. | C:\user\tasks\shared |
| AZ_BATCH_NODE_STARTUP_DIR       | Merhaba Hello tam yolunu [görev dizini Başlat] [ files_dirs] hello düğümde. | Tüm görevler. | C:\user\tasks\startup |
| AZ_BATCH_POOL_ID                | Görev hello hello havuzun Hello kimliği çalışıyor. | Tüm görevler. | batchpool001 |
| AZ_BATCH_TASK_DIR               | Merhaba Hello tam yolunu [görev dizini] [ files_dirs] hello düğümde. Bu dizin hello içeren `stdout.txt` ve `stderr.txt` hello görev ve hello AZ_BATCH_TASK_WORKING_DIR. | Tüm görevler. | C:\user\tasks\workitems\batchjob001\job-1\task001 |
| AZ_BATCH_TASK_ID                | Merhaba geçerli görevin kimliği Hello. | Başlangıç görevi dışında tüm görevler. | task001 |
| AZ_BATCH_TASK_WORKING_DIR       | Merhaba Hello tam yolunu [görev çalışma dizini] [ files_dirs] hello düğümde. Görev şu anda çalışan hello okuma/yazma erişimi toothis dizini vardır. | Tüm görevler. | C:\user\tasks\workitems\batchjob001\job-1\task001\wd |
| CCP_NODES                       | düğümler ve tooa ayrılan çekirdek düğüm sayısı Hello listesi [çok örnekli görev][multi_instance]. Düğümler ve çekirdek hello biçiminde listelenir`numNodes<space>node1IP<space>node1Cores<space>`<br/>`node2IP<space>node2Cores<space> ...`, burada hello düğüm sayısını ardından bir veya daha fazla düğüm IP adresleri ile Merhaba çekirdek sayısı her biri için. |  Çok örnekli birincil ve alt görevler. |`2 10.0.0.4 1 10.0.0.5 1` |
| AZ_BATCH_NODE_LIST              | Merhaba tooa ayrılan düğümler listesi [çok örnekli görev] [ multi_instance] hello biçiminde `nodeIP;nodeIP`. | Çok örnekli birincil ve alt görevler. | `10.0.0.4;10.0.0.5` |
| AZ_BATCH_HOST_LIST              | Merhaba tooa ayrılan düğümler listesi [çok örnekli görev] [ multi_instance] hello biçiminde `nodeIP,nodeIP`. | Çok örnekli birincil ve alt görevler. | `10.0.0.4,10.0.0.5` |
| AZ_BATCH_MASTER_NODE            | Merhaba IP adresi ve bağlantı noktası hello hangi hello birincil görevi, üzerinde işlem düğümü bir [çok örnekli görev] [ multi_instance] çalıştırır. | Çok örnekli birincil ve alt görevler. | `10.0.0.4:6000`|
| AZ_BATCH_TASK_SHARED_DIR | Merhaba birincil görev ve her görevinin için aynı olan bir dizin yolu bir [çok örnekli görev][multi_instance]. Merhaba yolu hello çok örnekli görev çalıştığı her düğümde üzerinde var ve okuma/yazma bu düğümde çalışan erişilebilir toohello görev komutları (her iki hello [koordinasyon komutu] [ coord_cmd] ve hello [uygulama komutu][app_cmd]). Alt görevler veya diğer düğümlerde yürütmek birincil bir görev, uzaktan erişim toothis dizin ("paylaşılan" ağ dizinine olmadığı) gerekmez. | Çok örnekli birincil ve alt görevler. | C:\user\tasks\workitems\multiinstancesamplejob\job-1\multiinstancesampletask |
| AZ_BATCH_IS_CURRENT_NODE_MASTER | Merhaba geçerli düğüm için hello ana düğüm olup olmadığını belirtir bir [çok örnekli görev][multi_instance]. Olası değerler şunlardır: `true` ve `false`.| Çok örnekli birincil ve alt görevler. | `true` |
| AZ_BATCH_NODE_IS_DEDICATED | Varsa `true`, hello geçerli düğümdür adanmış bir düğüm. Varsa `false`, bu bir [düşük öncelikli düğüm](batch-low-pri-vms.md). | Tüm görevler. | `true` |

[files_dirs]: https://azure.microsoft.com/documentation/articles/batch-api-basics/#files-and-directories
[multi_instance]: https://azure.microsoft.com/documentation/articles/batch-mpi/
[coord_cmd]: https://azure.microsoft.com/documentation/articles/batch-mpi/#coordination-command
[app_cmd]: https://azure.microsoft.com/documentation/articles/batch-mpi/#application-command
