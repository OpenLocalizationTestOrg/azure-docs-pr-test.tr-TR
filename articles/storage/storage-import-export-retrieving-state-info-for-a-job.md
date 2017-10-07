---
title: "bir Azure içeri/dışarı aktarma işi için aaaRetrieving durum bilgilerini | Microsoft Docs"
description: "Nasıl tooobtain için durum bilgisi Microsoft Azure içeri/dışarı aktarma hizmeti işleri öğrenin."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 22d7e5f0-94da-49b4-a1ac-dd4c14a423c2
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/16/2016
ms.author: muralikk
ms.openlocfilehash: cbc35660519573d92f641924ac0025c9e577d69b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="retrieving-state-information-for-an-importexport-job"></a>İçeri/dışarı aktarma işi için durum bilgilerini alma
Merhaba çağırabilirsiniz [alma işi](/rest/api/storageimportexport/jobs#Jobs_Get) işlemi tooretrieve bilgilerini hem de almak ve işleri dışarı aktarma. döndürülen hello bilgileri içerir:

-   Merhaba hello işin geçerli durumu.

-   Merhaba yaklaşık yüzde her işi tamamlandı.

-   Merhaba her sürücünün geçerli durumu.

-   Hata günlüklerini ve ayrıntılı günlük kaydı bilgileri (etkinse) içeren BLOB'ları URI.

Merhaba aşağıdaki bölümlerde açıklanmıştır hello tarafından döndürülen hello bilgileri `Get Job` işlemi.

## <a name="job-states"></a>İş durumları
Merhaba tablo ve hello durumu diyagramı aşağıdaki yaşam döngüsü sırasında aracılığıyla bir iş geçişleri hello durumlar açıklanmaktadır. Merhaba işin geçerli durumu Hello arama hello tarafından belirlenebilir `Get Job` işlemi.

![JobStates](./media/storage-import-export-retrieving-state-info-for-a-job/JobStates.png "JobStates")

Merhaba aşağıdaki tabloda bir işi geçirir her durum açıklanmaktadır.

|İş durumu|Açıklama|
|---------------|-----------------|
|`Creating`|Merhaba iş Put işlemini çağırın, bir iş oluşturulur ve durumu çok ayarladıktan sonra`Creating`. Merhaba iş hello olsa `Creating` durumunda, hello içeri/dışarı aktarma hizmeti varsayar hello sürücüleri sevk edilen toohello veri merkezi olmayan olmuştur. Bir işi hello kalabilir `Creating` tootwo hafta sonra otomatik olarak silinir hello hizmeti tarafından yedeklemek için durum.<br /><br /> Hello iş hello durumdayken hello güncelleştirme işi özellikleri işlem çağrısı yaparsanız `Creating` durumunda, hello iş kalır hello `Creating` durum ve zaman aşımı hello sıfırlama tootwo hafta aralığıdır.|
|`Shipping`|Paketinizi sevk sonra hello güncelleştirme işi özellikleri işlemi güncelleştirme hello durumunu hello iş çok çağırmalıdır`Shipping`. yalnızca hello varsa durumu sevkiyat hello ayarlanabilir `DeliveryPackage` (posta taşıyıcı ve izleme numarası) ve hello `ReturnAddress` özellikleri hello işi için ayarlanmış.<br /><br /> Merhaba iş tootwo hafta yedeklemek için hello sevkiyat durumunda kalır. İki hafta geçtiğini ve hello sürücüleri alınmamış hello içeri/dışarı aktarma hizmeti işleçleri bildirilir.|
|`Received`|Tüm sürücüler hello veri merkezinde alınmış olan sonra hello iş durumu toohello alınan durumu ayarlanır.|
|`Transferring`|Merhaba sürücüleri almış hello veri merkezinde ve en az bir sürücü işleme başladı sonra hello iş durumu toohello ayarlanacak `Transferring` durumu. Merhaba bkz `Drive States` ayrıntılı bilgi için bölüm aşağıda.|
|`Packaging`|Tüm sürücüler işlemeyi tamamladıktan sonra hello iş hello yerleştirilecek `Packaging` sevk edilen geri toohello müşteri hello sürücülerdir kadar belirtin.|
|`Completed`|Hello iş hatasız tamamladıysa tüm sürücüler sevk edilen geri toohello müşteri eklendikten sonra ardından hello iş toohello ayarlanacak `Completed` durumu. Merhaba iş otomatik olarak hello 90 gün sonra silinir `Completed` durumu.|
|`Closed`|Olduysa hataları hello iş hello işlenmesi sırasında tüm sürücüler sevk edilen geri toohello müşteri eklendikten sonra ardından hello iş toohello ayarlanacak `Closed` durumu. Merhaba iş otomatik olarak hello 90 gün sonra silinir `Closed` durumu.|

Bir işi yalnızca belirli durumlar iptal edebilirsiniz. İşi iptal edildi hello veri kopyalama adımı atlar ancak Aksi durumda iptal bir iş olarak aynı durum geçişleri hello izler.

Merhaba aşağıdaki tabloda bir hata oluştuğunda, her iş durumu yanı sıra hello hello iş etkisi için oluşabilecek hatalar açıklanmaktadır.

|İş durumu|Olay|Çözümleme / sonraki adımlar|
|---------------|-----------|------------------------------|
|`Creating or Undefined`|Bir iş için bir veya daha fazla sürücüler ulaşmadığını ancak hello iş hello değil `Shipping` durumu veya hello hizmetindeki hello işin kaydı yok.|Merhaba içeri/dışarı aktarma hizmeti işlemler ekibinin toocontact hello müşteri toocreate denemek veya hello iş gerekli bilgileri toomove hello işlemiyle İleri güncelleştirin.<br /><br /> Merhaba işletim ekibi oluşturulamıyor toocontact hello müşteri iki hafta içinde ise hello işletim ekibi tooreturn hello sürücüleri deneyecek.<br /><br /> Merhaba sürücüleri döndürülemiyor ve hello müşteri ulaşılamıyor hello olayda hello sürücüleri Güvenli bir şekilde 90 gün içinde yok olacaktır.<br /><br /> Bir iş durumu çok güncelleştirilene kadar işlenemiyor Not`Shipping`.|
|`Shipping`|bir iş için başlangıç paketi iki hafta boyunca gelen değil.|Merhaba işletim ekibi hello müşteri hello eksik paketinin size bildirir. Hello Müşteri'nin yanıtta bağlı olarak, hello işletim ekibi hello aralığı toowait hello paket tooarrive için genişletme, veya hello işini iptal et.<br /><br /> Merhaba olay o hello müşteri temas kurulamıyor veya yanıt vermiyor 30 gün içinde hello işletim ekibi eylem toomove hello hello işten başlatmak `Shipping` doğrudan toohello durum `Closed` durumu.|
|`Completed/Closed`|hiçbir zaman Hello sürücüler hello dönüş adresi sınırına ya da (yalnızca tooan dışarı aktarma işini geçerlidir) sevkiyat zarar görmüş.|Merhaba sürücüleri hello dönüş adresi değil ulaştıysanız, onay hello iş durumu hello portal tooensure sürücüleri gönderilen bu hello veya hello müşteri ilk çağrı hello alma işi işlemi gerekir. Merhaba sürücüleri sevk durumunda hello müşteri hello sevkiyat sağlayıcısı tootry başvurun ve hello sürücüleri bulun.<br /><br /> Merhaba sürücüleri sevkiyat sırasında bozuksa, başka bir dışarı aktarma işini ya da indirme hello eksik BLOB'ları hello müşteri toorequest isteyebilirsiniz.|
|`Transferring/Packaging`|İş, yanlış bir ya da dönüş adresi eksik sahiptir.|Merhaba işlemler ekibinin toohello kişinin hello iş tooobtain hello doğru adres için kullanıma tamamlayacaktır.<br /><br /> Merhaba olayda hello müşteriye ulaşılamıyor, hello sürücüleri 90 gün içinde güvenli bir şekilde yok.|
|`Creating / Shipping/ Transferring`|İçe aktarılan sürücü toobe hello listesinde görünmeyen bir sürücü paketi sevkiyat hello dahil edilir.|Merhaba ek sürücüler işlenmeyecek ve hello iş tamamlandığında toohello müşteri döndürülür.|

## <a name="drive-states"></a>Sürücü durumları
bir içe veya dışa aktarma işi ile geçiş yapıldığı gibi hello tablo ve hello diyagrama ayrı ayrı bir sürücü hello yaşam döngüsünü açıklanmaktadır. Merhaba geçerli sürücü durumu tarafından arama hello alabilir `Get Job` işlemi ve İnceleme hello `State` hello öğesinin `DriveList` özelliği.

![DriveStates](./media/storage-import-export-retrieving-state-info-for-a-job/DriveStates.png "DriveStates")

Merhaba aşağıdaki tabloda bir sürücü üzerinden iletebilir her durum açıklanmaktadır.

|Sürücü durumu|Açıklama|
|-----------------|-----------------|
|`Specified`|Merhaba iş hello Put iş işlemi ile oluşturulduğunda bir içeri aktarma işi için hello ilk için bir sürücü hello durumdur `Specified` durumu. Hiçbir sürücü Hello iş oluşturulduğunda, belirtilen bir dışa aktarma işi için hello ilk sürücü durumu hello olduğu `Received` durumu.|
|`Received`|Merhaba sürücü geçişleri toohello `Received` durum hello zaman içeri/dışarı aktarma hizmeti işleci şirket içe aktarma işi için sevkiyat hello öğesinden alınan hello sürücüleri işledi. Bir verme için hello ilk sürücü durumu hello iş `Received` durumu.|
|`NeverReceived`|Merhaba sürücü toohello taşınır `NeverReceived` durum hello olduğunda bir iş için paket ulaşır ancak hello paket hello sürücü içermiyor. İki hafta hello hizmeti hello Sevkiyat bilgileri aldı, ancak hello paket henüz hello veri merkezinde geldi değil bu yana olması durumunda bir sürücü de bu duruma taşıyabilirsiniz.|
|`Transferring`|Bir sürücü toohello taşınır `Transferring` durum hello zaman hizmeti hello sürücü tooWindows Azure Storage tootransfer verilerden başlar.|
|`Completed`|Bir sürücü toohello taşınır `Completed` durum hello hizmeti başarıyla aktarılan tüm hello veri hatasız zaman.|
|`CompletedMoreInfo`|Bir sürücü toohello taşınır `CompletedMoreInfo` zaman hello hizmet bazı sorunlar veri kopyalanırken herhangi birinden karşılaştı veya toohello sürücüyü belirtin. Merhaba bilgi hataları, uyarıları veya BLOB üzerine hakkında bilgilendirici iletileri ekleyebilirsiniz.|
|`ShippedBack`|Merhaba sürücü toohello taşınır `ShippedBack` hello veri merkezi geri toohello dönüş adresinden gönderilen zaman durumu.|

Merhaba aşağıdaki tabloda hello sürücü hata durumları ve her durum için yapılan hello eylemler açıklanmaktadır.

|Sürücü durumu|Olay|Çözümleme / sonraki adım|
|-----------------|-----------|-----------------------------|
|`NeverReceived`|Olarak işaretlenmiş bir sürücü `NeverReceived` (Merhaba işin sevkiyat bir parçası olarak alınmadı çünkü) başka bir sevkiyat ulaşır.|Merhaba işletim ekibi hello sürücü toohello taşınır `Received` durumu.|
|`N/A`|Başka bir iş parçası olarak hello veri merkezindeki herhangi bir işi parçası olmayan bir sürücü ulaşır.|Merhaba sürücü fazladan bir sürücü olarak işaretlenir ve hello özgün paket ile ilişkili hello iş tamamlandığında toohello müşteri döndürülür.|

## <a name="faulted-states"></a>Hatalı durumları
Bir iş ya da sürücü tooprogress normalde beklenen yaşam döngüsü boyunca başarısız olduğunda, hello iş ya da sürücü içine taşınır bir `Faulted` durumu. Bu noktada, hello işletim ekibi hello müşteri e-posta veya telefon tarafından sizinle iletişim kuracaktır. Merhaba sorun çözüldükten sonra hello iş ya da hatalı sürücü dışında hello alınır `Faulted` durum ve hello içine taşınan durumu uygun.

## <a name="next-steps"></a>Sonraki adımlar

* [Merhaba içeri/dışarı aktarma hizmeti REST API'si kullanma](storage-import-export-using-the-rest-api.md)
