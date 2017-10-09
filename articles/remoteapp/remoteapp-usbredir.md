---
title: "aaaHow USB aygıtları Azure remoteapp'te yeniden yönlendirme musunuz? | Microsoft Belgeleri"
description: "Bilgi nasıl Azure RemoteApp USB aygıtları için toouse yeniden yönlendirme."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 191d98af-2f5a-4307-9042-aae0e4049f9f
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 661b90c0910167d76ac3886b5af7a32d00b3943f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-do-you-redirect-usb-devices-in-azure-remoteapp"></a>Azure RemoteApp USB aygıtları nasıl yönlendirmek?
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.
> 
> 

Aygıt yeniden yönlendirme hello USB aygıtları ekli tootheir bilgisayar veya tablet hello uygulamalarında Azure RemoteApp ile kullanıcıların olanak sağlar. Örneğin, Skype Azure RemoteApp aracılığıyla paylaşılan, kullanıcılarınızın kendi cihaz kameralar toobe mümkün toouse gerekir.

Daha fazla geçmeden önce hello USB yeniden yönlendirme bilgileri okuma olduğundan emin olun [Azure Remoteapp'te yeniden yönlendirme kullanarak](remoteapp-redirection.md). Merhaba nusbdevicestoredirect:s ancak önerilen: * USB web kameraları için çalışmaz ve bazı USB yazıcıları ya da USB multifunctional aygıtlar için çalışmayabilir. Kullanıcılarınız bu cihazların kullanabilmek için tasarım ve güvenlik nedenleriyle, hello Azure RemoteApp Yöneticisi tooenable yeniden yönlendirme aygıt sınıfı GUID veya aygıt örnek kimliği var.

Bu makalede, web kamera yönlendirmesi hakkında ettiği rağmen benzer bir yaklaşım tooredirect USB Yazıcılar ve hello tarafından yönlendirilmez diğer USB multifunctional aygıtları kullanabilirsiniz **nusbdevicestoredirect:s:*** komutu.

## <a name="redirection-options-for-usb-devices"></a>USB cihazlar için yeniden yönlendirme seçenekleri
Azure RemoteApp, USB aygıtlarını kullanılabilir olanları için Uzak Masaüstü Hizmetleri hello olarak yönlendirmek için çok benzer mekanizmaları kullanır. Merhaba temel alınan teknoloji tooget hello her ikisi de üst düzey en iyi belirli bir aygıt için hello doğru yeniden yönlendirme yöntemini seçmenize olanak sağlar ve RemoteFX USB aygıtı yeniden yönlendirme hello kullanarak **usbdevicestoredirect:s:** komutu. Toothis komutu dört öğe vardır:

| İşleme sırası | Parametre | Açıklama |
| --- | --- | --- |
| 1 |* |Üst düzey yeniden yönlendirme toplanma olmayan tüm cihazlar seçer. Not: tasarıma göre * USB web kameraları için çalışmıyor. |
| {Aygıt sınıfı GUID} |Belirtilen hello eşleşen tüm aygıtları seçer aygıt kurulum sınıfı. | |
| USB\InstanceID |Örnek kimliği verilir hello için belirtilen bir USB aygıtı seçer | |
| 2 |-USB\Instance kimliği |Merhaba belirtilen cihaz için Hello yeniden yönlendirme ayarlarını kaldırır. |

## <a name="redirecting-a-usb-device-by-using-hello-device-class-guid"></a>Merhaba aygıt sınıfı GUID kullanarak bir USB aygıtı yeniden yönlendirme
Toofind hello aygıt sınıfı için yeniden yönlendirme kullanılabilir GUID'i iki yolu vardır. 

Merhaba ilk seçenektir toouse hello [tanımlı cihaz Kurulumu kullanılabilir sınıfları tooVendors](https://msdn.microsoft.com/library/windows/hardware/ff553426.aspx). Merhaba aygıt ekli toohello yerel bilgisayar en yakından eşleşen hello sınıfı seçin. Dijital kameraları için bu Imaging aygıt sınıfı veya Video yakalama aygıtı sınıfı olabilir. Bazı deneme hello aygıt sınıfları toofind hello sınıfı yerel olarak hello ile çalışır GUID USB aygıtın (bizim örnek hello web kamerası) bağlı doğru ile toodo gerekir.

Daha iyi şekilde ya da hello ikinci seçeneği toofollow olduğundan bu adımları toofind hello belirli cihaz GUID sınıfı:

1. Merhaba Aygıt Yöneticisi'ni açın, yönlendirilir ve sağ hello aygıtı bulun ve hello Özellikleri'ni açın.
   ![Merhaba Aygıt Yöneticisi'ni açın](./media/remoteapp-usbredir/ra-devicemanager.png)
2. Merhaba üzerinde **ayrıntıları** sekmesinde, hello özelliği seçin **sınıfı GUID**. Görüntülenen hello hello cihaz türü için sınıf GUID değeridir.
   ![Kamera özellikleri](./media/remoteapp-usbredir/ra-classguid.png)
3. Eşleşen hello sınıfı GUID değeri tooredirect aygıtları'nı kullanın.

Örneğin:

        Set-AzureRemoteAppCollection -CollectionName <collection name> -CustomRdpProperty "nusbdevicestoredirect:s:<Class Guid value>"

Merhaba birden çok aygıt yönlendirmeler birleştirebilirsiniz aynı cmdlet'i. Örneğin: tooredirect yerel depolama ve bir USB web kamera, cmdlet şu şekilde görünür:

        Set-AzureRemoteAppCollection -CollectionName <collection name> -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:<Class Guid value>"

Aygıt yeniden yönlendirme GUID sınıfı tarafından ayarladığınızda hello GUID sınıfında koleksiyon belirtilen eşleşen tüm aygıtları yönlendirilir. Vardır, örneğin, sahip birden çok bilgisayar hello yerel ağ üzerinde aynı hello USB web kameralar çalıştırabilirsiniz tek cmdlet tooredirect tüm hello web kameraları.

## <a name="redirecting-a-usb-device-by-using-hello-device-instance-id"></a>Merhaba aygıt örnek kimliği kullanarak bir USB aygıtı yeniden yönlendirme
Daha ayrıntılı denetim istediğiniz ve cihaz başına toocontrol yeniden yönlendirme istiyorsanız hello kullanabilirsiniz **USB\InstanceID** yeniden yönlendirme parametresi.

Bu yöntem en zor parçası Hello hello USB aygıtı örneği kimlik bulma Toohello bilgisayar ve hello belirli USB aygıtı erişim. Ardından aşağıdaki adımları izleyin:

1. Merhaba cihaz Uzak Masaüstü oturumunda açıklandığı gibi yönlendirmesini [nasıl kullanabilir miyim Aygıtlarımı ve kaynakları bir Uzak Masaüstü oturumunda?](http://windows.microsoft.com/en-us/windows7/How-can-I-use-my-devices-and-resources-in-a-Remote-Desktop-session)
2. Uzak Masaüstü Bağlantısı açın ve tıklatın **Seçenekleri Göster**.
3. Tıklatın **Farklı Kaydet** toosave hello geçerli bağlantı ayarlarını tooan RDP dosyası.  
    ![Hello ayarlarını bir RDP dosyası olarak Kaydet](./media/remoteapp-usbredir/ra-saveasrdp.png)
4. Bir dosya adı ve örneğin MyConnection.rdp ve bu PC\Documents bir konum seçin ve hello dosyasını kaydedin.
5. Açık hello MyConnection.rdp bir metin düzenleyicisi kullanarak dosya ve hello örnek kimliği Bul hello aygıtı tooredirect istiyor.

Şimdi, hello örnek kimliği hello aşağıdaki cmdlet'i kullanın:

    Set-AzureRemoteAppCollection -CollectionName <collection name> -CustomRdpProperty "nusbdevicestoredirect:s: USB\<Device InstanceID value>"



### <a name="help-us-help-you"></a>Yardımımıza katkıda bulunun
Toplama toorating bu makalede, aşağıda yorum yapmamanın, değişiklikleri toohello makalesi kendisini yapıp olduğunu biliyor muydunuz? Eksik bir şeyler mi var? Yanlış bir şeyler mi var? Kafa karıştırıcı bir şeyler mi yazdım? Yukarı doğru ilerleyin ve tıklatın **GitHub üzerinde Düzenle** toomake değişiklikleri - olanlar gelen gözden geçirilmek üzere toous ve biz üzerlerinde edildikten sonra değişiklikleriniz ve iyileştirmeleriniz burada göreceğiniz.

