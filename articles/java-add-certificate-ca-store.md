---
title: bir sertifika toohello Java CA deposu aaaAdd | Microsoft Docs
description: "Nasıl tooadd bir sertifika yetkilisi (CA) sertifika toohello Java CA sertifikasını (cacerts) depolamak Twilio hizmet veya Azure Service Bus için öğrenin."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: d3699b0a-835c-43fb-844d-9c25344e5cda
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 030e43129580023942dee662e72d2f443167f308
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="adding-a-certificate-toohello-java-ca-certificates-store"></a>Sertifika toohello Java CA sertifikaları deposu ekleme
Aşağıdaki adımları hello nasıl tooadd bir sertifika yetkilisi (CA) sertifika toohello Java CA sertifikasını (cacerts) depolamak gösterir. kullanılan hello örnek hello Twilio hizmeti tarafından hello CA sertifikası gereklidir. Daha sonra hello konuda sağlanan bilgiler nasıl tooinstall hello CA sertifika hello Azure Service Bus açıklar. 

JDK ve tooyour Azure projesi 's ekleyerek keytool tooadd hello CA sertifikası önceki toozipping kullanabileceğiniz **approot** klasör veya keytool tooadd hello sertifika kullanan bir Azure başlangıç görevi çalıştırabilir. Bu örnek, bir CA sertifikası önceki toohello daraltılmış JDK ekleyeceksiniz varsayar. Ayrıca, belirli bir CA sertifikası hello örnek, ancak farklı bir CA sertifikasını alma adımları hello kullanılacak ve hello cacerts alma deposu benzer olacaktır.

## <a name="tooadd-a-certificate-toohello-cacerts-store"></a>bir sertifika toohello cacerts tooadd depolama
1. Bir komut isteminde tooyour JDK'ın ayarlamak **jdk\jre\lib\security** klasörü, hangi sertifikaların yüklü toosee aşağıdaki hello çalıştırın:
   
    `keytool -list -keystore cacerts`
   
    Merhaba deposu parolasını istenir. Merhaba varsayılan parola **değiştirme**. (Toochange hello parola istiyorsanız hello keytool belgelerine bakın <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.) Bu örnek, MD5 parmak izi 67:CB:9 D hello sertifikayla varsayar: C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 listede ve tooimport istediğiniz BT (Merhaba Twilio API hizmeti tarafından bu belirli sertifika gereklidir).
2. Konumunda listelenen sertifikaları hello listesinden Hello sertifika elde [GeoTrust kök sertifikalarını](http://www.geotrust.com/resources/root-certificates/). Merhaba sertifikanın seri numarası 35:DE:F4:CF ile Merhaba bağlantıyı sağ tıklatın ve toohello kaydetmek **jdk\jre\lib\security** klasör. Bu örneğin amaçları doğrultusunda adlı tooa dosya kaydedildi **Equifax\_güvenli\_sertifika\_Authority.cer**.
3. Komutu aşağıdaki hello aracılığıyla Hello sertifikasını içeri aktarın:
   
    `keytool -keystore cacerts -importcert -alias equifaxsecureca -file Equifax_Secure_Certificate_Authority.cer`
   
    Zaman MD5 parmak izi 67:CB:9 D hello sertifika varsa, bu sertifika tootrust istenir: C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4, yazarak yanıtlayın **y**.
4. Komut tooensure hello CA sertifika aşağıdaki çalışma hello başarıyla alındı:
   
    `keytool -list -keystore cacerts`
5. Merhaba JDK zip ve tooyour Azure projesi 's ekleyin **approot** klasör.

Keytool hakkında daha fazla bilgi için bkz: <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.

## <a name="azure-root-certificates"></a>Azure kök sertifikaları
Azure Hizmetleri (örneğin, Azure Service Bus) kullanan, uygulamaları tootrust hello Baltimore CyberTrust kök sertifikası gerekir. (15 Nisan 2013 başlayan Azure hello GTE CyberTrust genel kök toohello Baltimore CyberTrust Root ' geçiş başlamıştır. Bu geçiş birkaç ay toocomplete sürdü.)

Merhaba sertifika önceden yüklenmiş olmalıdır cacerts deponuzda Baltimore şekilde unutmayın toorun hello **keytool-liste** zaten varsa, ilk toosee komutu.

Tooadd gerekiyorsa Baltimore CyberTrust Root Merhaba, seri numarası 02:00:00:b9 ve SHA1 parmak izi d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2 c vardır: 78:db:28:52:ca:e4:74. Adresten yüklenebilir <https://cacert.omniroot.com/bc2025.crt>, tooa yerel dosya uzantısı ile kaydedilen **.cer**ve kullanılarak içe **keytool** yukarıda gösterildiği gibi.

## <a name="next-steps"></a>Sonraki adımlar
Azure tarafından kullanılan hello kök sertifikaları hakkında daha fazla bilgi için bkz: [Azure kök sertifika geçiş](http://blogs.msdn.com/b/windowsazure/archive/2013/03/15/windows-azure-root-certificate-migration.aspx).

Java hakkında daha fazla bilgi için bkz: [Java geliştiriciler için Azure](/java/azure).

