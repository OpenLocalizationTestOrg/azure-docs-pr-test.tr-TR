---
title: Azure sanal makineleri Sunucu Gezgini'nden aaaAccessing | Microsoft Docs
description: "Tooview oluşturma ve Azure sanal makineleri (VM'ler) Visual Studio Sunucu Gezgininde yönetmek bir genel bakış alın."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: eb3afde6-ba90-4308-9ac1-3cc29da4ede0
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: f8326aed105a64ca558f766d712cc68701f82c15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-azure-virtual-machines-from-server-explorer"></a>Server Explorer'dan Azure sanal makineleri erişme
Visual Studio'da Sunucu Gezgini kullanarak, Azure tarafından barındırılan sanal makinelerinizi hakkındaki bilgileri görüntüleyebilirsiniz.

## <a name="accessing-virtual-machines-in-server-explorer"></a>Sanal makineler Sunucu Gezgininde erişme
Azure tarafından barındırılan sanal makineler varsa, sunucu Gezgini'nde erişebilir. Mobil hizmetler tooyour Azure aboneliği tooview ilk kez oturum gerekir. toosign, sunucu Gezgini'nde hello Azure düğümü için hello kısayol menüsünü açın ve seçin **tooMicrosoft Azure Connect**.

### <a name="tooget-information-about-your-virtual-machines"></a>sanal makinelerinizi hakkında tooget bilgi
1. Sunucu Gezgini'nde, bir sanal makine seçin ve kendi özellikleri penceresinde hello F4 anahtar tooshow'i seçin.
   
    Aşağıdaki tablonun hello hangi özelliklerin kullanılabilir olduğunu gösterir, ancak tüm salt okunurdur. toochange bunları kullanan hello [Klasik Azure portalı](http://go.microsoft.com/fwlink/?LinkID=213885).
   
   | Özellik | Açıklama |
   | --- | --- |
   | DNS Adı |Merhaba hello sanal makinenin Internet adresi ile Merhaba URL'si. |
   | Ortam |Bir sanal makine için hello bu özellik her zaman üretim değeridir. |
   | Ad |Merhaba sanal makinenin adını Hello. |
   | Boyut |kullanılabilir bellek ve disk alanı miktarını hello yansıtır hello sanal makine Hello boyutu. Daha fazla bilgi için bkz: nasıl yapılır: sanal makine boyutlarını yapılandırın. |
   | Durum |Değerleri başlatma, başlatıldı, durdurma, durduruldu ve alma durumunu içerir. Durum alınıyor görünürse, hello geçerli durumu bilinmiyor. Bu özellik için Hello değerler farklı hello üzerinde kullanılan hello değerlerinden [Klasik Azure portalı](http://go.microsoft.com/fwlink/?LinkID=213885). |
   | Subscriptionıd |Azure hesabınız için Hello abonelik kimliği. Bu bilgileri üzerinde hello gösterebilir [Klasik Azure portalı](http://go.microsoft.com/fwlink/?LinkID=213885) bir abonelik hello özelliklerini görüntüleyerek. |
2. Bir uç nokta düğümü seçin ve ardından hello görüntüleyin **özellikleri** penceresi.
3. Merhaba aşağıdaki tabloda açıklanmaktadır hello kullanılabilir özellikler uç noktaları, ancak salt okunurdur. tooadd veya düzenleme hello uç noktaları bir sanal makine için kullanmak hello [Klasik Azure portalı](http://go.microsoft.com/fwlink/?LinkID=213885). 
   
   | Özellik | Açıklama |
   | --- | --- |
   | Ad |Merhaba uç noktası için bir tanımlayıcı. |
   | Özel bağlantı noktası |ağ erişim iç tooyour uygulaması için başlangıç bağlantı noktası. |
   | Protokol |Bu uç noktası için Aktarım katmanı hello hello protokolü, TCP veya UDP'i kullanır. |
   | Genel Bağlantı Noktası |Genel erişim tooyour uygulama için kullanılacak başlangıç bağlantı noktası. |

## <a name="next-steps"></a>Sonraki adımlar
Visual Studio'da Azure rolleri kullanma hakkında daha fazla toolearn bkz [Azure rolleri ile Uzak Masaüstü kullanarak](vs-azure-tools-remote-desktop-roles.md).

