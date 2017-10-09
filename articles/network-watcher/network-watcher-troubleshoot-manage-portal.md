---
title: "aaaTroubleshoot Azure sanal ağ geçidi ve bağlantıları - PowerShell | Microsoft Docs"
description: "Bu sayfayı toouse hello Azure Ağ İzleyicisi PowerShell cmdlet'ini nasıl sorun giderme açıklar"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: f6f0a813-38b6-4a1f-8cfc-1dfdf979f595
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: bd568d34091209390c57d22475559bdb99ad2c59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-powershell"></a>Sanal ağ geçidi ve Azure Ağ İzleyicisi PowerShell kullanarak bağlantı sorunlarını giderme

> [!div class="op_single_selector"]
> - [Portal](network-watcher-troubleshoot-manage-portal.md)
> - [PowerShell](network-watcher-troubleshoot-manage-powershell.md)
> - [CLI 1.0](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [CLI 2.0](network-watcher-troubleshoot-manage-cli.md)
> - [REST API](network-watcher-troubleshoot-manage-rest.md)

Ağ kaynaklarınızı Azure toounderstanding ilgili olarak Ağ İzleyicisi çok sayıda özellik sağlar. Bu özelliklerin biri kaynak sorun giderme. Kaynak sorun giderme hello portal, PowerShell'i, CLI veya REST API çağrılabilir. Çağrıldığında, Ağ İzleyicisi Merhaba bir sanal ağ geçidi veya bağlantı durumunu inceler ve bulduklarını döndürür.

## <a name="before-you-begin"></a>Başlamadan önce

Bu senaryo zaten izlediğiniz hello adımlarda varsayar [bir Ağ İzleyicisi oluşturma](network-watcher-create.md) toocreate bir Ağ İzleyicisi.

Desteklenen ağ geçidi türleri ziyaret listesi [desteklenen ağ geçidi türleri](network-watcher-troubleshoot-overview.md#supported-gateway-types).

## <a name="overview"></a>Genel Bakış

Kaynak sorun giderme hello yeteneği sağlar sanal ağ geçitleri ve bağlantılarla ortaya çıkan sorunları giderme. Bir istek tooresource sorun giderme yapıldığında günlükleri yükleniyor sorgulanan ve sahip denetlenir. İnceleme tamamlandığında hello sonuçlar döndürülür. Hangi birden çok dakika tooreturn bir sonuç ele geçirebilir sorun giderme istekleri uzun süredir çalışıp kaynak ister. sorun giderme gelen hello günlükleri, belirtilen bir depolama hesabı üzerinde bir kapsayıcıda depolanır.

## <a name="troubleshoot-a-gateway-or-connection"></a>Bir ağ geçidi veya bağlantı sorunlarını giderme

1. Toohello gidin [Azure portal](https://portal.azure.com) tıklatıp **ağ** > **Ağ İzleyicisi** > **VPN tanılama**
2. Seçin bir **abonelik**, **kaynak grubu**, ve **konumu**.
3. Kaynak sorun giderme hello kaynak hello durumunu ilgili verileri döndürür. Ayrıca, ilgili günlükleri tooa depolama hesabı toobe gözden kaydeder. Tıklatın **depolama hesabı** tooselect bir depolama hesabı.
4. Merhaba üzerinde **depolama hesapları** dikey penceresinde, mevcut bir depolama hesabını seçin veya **+ depolama hesabı** toocreate yeni bir tane.
5. Merhaba üzerinde **kapsayıcıları** dikey penceresinde, var olan bir kapsayıcı seçin veya tıklatın **+ kapsayıcı** toocreate yeni bir kapsayıcı. Tıklatın tamamlandığında **seçin**
6. Hello geçidi ve bağlantıyla kaynakları tootroubleshoot tıklatıp **sorun gidermeyi Başlat**

Birden fazla kaynak seçtiyseniz, sorun giderme ağ geçidi kaynaklarını aynı anda çalıştırılır. Bir bağlantıda çalıştırılamaz ve hello konumundaki ağ geçidine ilişkilendirilmiş aynı anda. Tootroubleshoot ağ geçitleri önerilen ilk gibi bağlantı sorunlarını giderme daha uzun bir işlemdir. VPN tanılama kaynak hello üzerinde çalışırken **sorun giderme durum** sütununu durumunu göster **çalışan**

Tamamlandığında, durum sütun değişiklikleri çok hello**sağlıklı** veya **sağlıksız**.

![eksiksiz sorun giderme][2]

## <a name="understanding-hello-results"></a>Merhaba sonuçlarını anlama

Merhaba, **ayrıntıları** bölüm hello pencerenin hello **durum** sekmesi gösterir hello son sorun giderme hello durumu çalışma seçili hello kaynakta. Merhaba son Tanılama sonuçları gösterilen xx dakika sonra son çalıştırma hello olur.

|Özellik  |Açıklama  |
|---------|---------|
|Kaynak     | Bir bağlantı toohello kaynağıdır.        |
|Depolama alanı yolu     |  Yol toohello depolama hesabı ve kapsayıcı hello günlükleri (herhangi bir çalıştırma hello sırasında oluşturulamadığı varsa) içeren. Bu ayar hello portal çıktıktan sonra devam etmez.        |
|Özet     | Merhaba kaynak durumu özeti.        |
|Ayrıntısı     | Merhaba kaynak durumu hakkında ayrıntılı bilgiler.        |
|Son çalıştırma     | Son zaman hello hello olduğu zaman sorun giderme çalıştı.        |


Merhaba **eylem** sekmesi nasıl tooresolve hello üzerinde sorunu genel rehberlik sağlar. Bir eylemin hello sorunu gerçekleştirilebiliyorsa bir bağlantı ile ek yönergeler sağlanır. Merhaba durumda hiçbir ek yönergeler olduğu hello yanıt hello url tooopen bir destek servis talebi sağlar..  Merhaba yanıt ve dahil edilen nedir hello özellikleri hakkında daha fazla bilgi için ziyaret [Ağ İzleyicisi sorun giderme genel bakış](network-watcher-troubleshoot-overview.md)


## <a name="next-steps"></a>Sonraki adımlar

Bu Dur VPN bağlantısı ayarları değiştirilmiş olup [ağ güvenlik grupları yönet](../virtual-network/virtual-network-manage-nsg-arm-portal.md) söz konusu olabilecek hello ağ güvenlik grubu ve güvenlik kuralları aşağı tootrack.


[2]: ./media/network-watcher-troubleshoot-manage-portal/2.png
