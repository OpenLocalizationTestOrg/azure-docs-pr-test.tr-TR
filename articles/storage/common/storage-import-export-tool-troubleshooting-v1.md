---
title: "aaaTroubleshooting hello Azure içeri/dışarı aktarma aracı | Microsoft Docs"
description: "Toohandle hello Azure içeri/dışarı aktarma aracı kullanarak ne zaman ve nasıl görülen hello ortak sorunlardan bazıları hakkında bilgi edinin bunları."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: b91ca5eb-c557-460a-9afc-0590b38471f9
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 254439c15797862dded5d80028b8780ad163b2b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hello-azure-importexport-tool"></a>Sorun giderme hello Azure içeri/dışarı aktarma aracı
sorunla çalıştırıyorsa hello Microsoft Azure içeri/dışarı aktarma aracı hata iletilerini döndürür. Bu konuda, kullanıcıların içine çalışabilir bazı yaygın sorunlar listelenmiştir.  
  
## <a name="a-copy-session-fails-what-i-should-do"></a>Kopya oturumu başarısız oluyor, ne yapmalıyım?  
 Kopya oturumu başarısız olduğunda, iki seçenek vardır:  
  
 Merhaba hata kısa dönem ve şimdi tekrar çevrimiçi için hello ağ paylaşımı çevrimdışıysa örneğin yeniden denenebilir ise, hello kopya oturumu devam edebilirsiniz. Merhaba hata yeniden denenebilir, örneğin hello yanlış kaynak dosyası dizini hello komut satırı parametrelerinde belirtilen değilse tooabort hello kopya oturumu gerekir. Bkz: [bir içeri aktarma işi için sabit sürücüler hazırlama](../storage-import-export-tool-preparing-hard-drives-import-v1.md) sürdürme ve kopyalama oturumları iptal etme hakkında daha fazla bilgi.  
  
## <a name="i-cant-resume-or-abort-a-copy-session"></a>I sürdürün veya bir kopya oturum iptal olamaz.  
 Merhaba kopyalama oturumdur hello bir sürücü için ilk kopyalama oturumu sonra hello hata iletisi belirtin: "Merhaba ilk kopya oturumu durduruldu veya sürdürülemez." Bu durumda, hello eski günlük dosyasını silin ve hello komutu yeniden çalıştırın.  
  
 Birinci bir sürücü için bir kopya oturumu değil hello varsa, her zaman iptal edildi veya sürdürülebilir.  
  
## <a name="i-lost-hello-journal-file-can-i-still-create-hello-job"></a>Merhaba günlük dosyası kayıp, hello iş oluşturabilirsiniz?  
 bir sürücü için Hello günlük dosyası veri toothis sürücüsü kopyalama hello tüm bilgileri içerir ve gerekli tooadd daha fazla dosyaları toohello sürücüsü ve kullanılan toocreate bir alma işi olacaktır. Merhaba günlük dosyası kaybolursa, tüm hello kopyalama oturumları hello sürücü için tooredo gerekir.  
  
## <a name="next-steps"></a>Sonraki adımlar
 
* [Hello azure içeri/dışarı aktarma aracı ayarlama](../storage-import-export-tool-setup-v1.md)   
* [Sabit sürücüleri içeri aktarma işine hazırlama](../storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [Kopyalama günlük dosyalarıyla iş durumunu gözden geçirme](../storage-import-export-tool-reviewing-job-status-v1.md)   
* [Bir içeri aktarma işini onarma](../storage-import-export-tool-repairing-an-import-job-v1.md)   
* [Bir dışarı aktarma işini onarma](../storage-import-export-tool-repairing-an-export-job-v1.md)
