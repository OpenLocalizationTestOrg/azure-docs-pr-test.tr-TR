---
title: "aaaLearn nasıl toouse hello logic apps FTP Bağlayıcısı | Microsoft Docs"
description: "Logic apps ile Azure uygulama hizmeti oluşturun. TooFTP sunucu toomanage dosyalarınızı bağlayın. Karşıya yükleme gibi çeşitli eylemleri, güncelleştirme, almak ve FTP sunucusu dosyaları silin."
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: erikre
editor: 
tags: connectors
ms.assetid: d83c55fe-eb59-4b7b-a5ec-afac5c772616
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/22/2016
ms.author: mandia; ladocs
ms.openlocfilehash: a7020df2005ebb34fc569627ae0516b8528cc7a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-ftp-connector"></a>Merhaba FTP Bağlayıcısı ile çalışmaya başlama
Merhaba FTP Bağlayıcısı toomonitor kullanmak için yönetmek ve bir FTP sunucusu üzerinde dosya oluşturun. 

toouse [tüm bağlayıcıların](apis-list.md), toocreate bir mantıksal uygulama ilk gerekir. Tarafından başlayabiliriz [şimdi mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-tooftp"></a>TooFTP Bağlan
Mantıksal uygulamanızı herhangi bir hizmet erişebilmeniz için önce toocreate ilk gerekiyor bir *bağlantı* toohello hizmet. A [bağlantı](connectors-overview.md) bir mantıksal uygulama ile başka bir hizmet arasında bağlantı sağlar.  

### <a name="create-a-connection-tooftp"></a>Bir bağlantı tooFTP oluşturma
> [!INCLUDE [Steps toocreate a connection tooFTP](../../includes/connectors-create-api-ftp.md)]
> 
> 

## <a name="use-a-ftp-trigger"></a>FTP tetikleyici kullanın
Bir tetikleyici bir mantıksal uygulama tanımlı kullanılan toostart hello iş akışı olabilecek bir olaydır. [Tetikleyiciler hakkında daha fazla bilgi](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).  

> [!IMPORTANT]
> Merhaba FTP Bağlayıcısı Internet hello erişilebilir olduğundan ve FTP sunucusuna toooperate Pasif modu ile yapılandırılmış gerektirir. Ayrıca, hello FTP Bağlayıcıdır **örtük FTPS (FTP SSL üzerinden) ile uyumlu değil**. Merhaba FTP Bağlayıcısı, yalnızca açık FTPS (FTP SSL üzerinden) destekler.  
> 
> 

Bu örnekte, ı bunu nasıl yapacağınızı gösterir toouse hello **bir dosya eklendiğinde veya FTP -** bir dosya için eklendiğinde veya, bir FTP sunucusuna değiştirildiğinde tooinitiate mantığı uygulama iş akışı tetikler. Bir kurumsal örnekte müşterilerden siparişleri temsil eden yeni dosyalar için Bu tetikleyici toomonitor FTP klasörü kullanabilirsiniz.  Bir FTP Bağlayıcısı eylem gibi sonra kullanabilir **dosya içeriğini almak** tooget hello içeriği başka bir işleme ve depolama siparişleri veritabanınızdaki hello düzeni.

1. Girin *ftp* hello arama kutusuna hello logic apps tasarımcısında hello seçip **bir dosya eklendiğinde veya FTP -** tetikleyici   
   ![FTP tetikleyici görüntü 1](./media/connectors-create-api-ftp/ftp-trigger-1.png)  
   Merhaba **ne zaman bir dosya eklenen veya değiştirilen** denetim açılır  
   ![FTP tetikleyici görüntü 2](./media/connectors-create-api-ftp/ftp-trigger-2.png)  
2. Select hello **...**  hello sağ tarafında hello denetim bulunur. Bu hello Klasör Seçici denetim açar  
   ![FTP tetikleyici görüntü 3](./media/connectors-create-api-ftp/ftp-trigger-3.png)  
3. Select hello  **>**  (sağ ok) ve yeni veya değiştirilmiş dosyaları için toomonitor istediğiniz toofind hello klasöre göz atın. Merhaba klasörü seçin ve başlangıç klasörü hello şimdi görüntülenen fark **klasörü** denetim.  
   ![FTP tetikleyici görüntü 4](./media/connectors-create-api-ftp/ftp-trigger-4.png)   

Bu noktada, mantıksal uygulamanızı bir dosya değiştiren veya hello belirli FTP klasörde oluşturulan yükleyen hello yürütülmesi diğer tetikleyiciler ve Eylemler hello iş akışında başlayacak bir tetikleyici ile yapılandırıldı. 

> [!NOTE]
> Bir mantıksal uygulama toobe için işlev, en az bir tetikleyici ve bir eylem içermelidir. Merhaba sonraki bölümde tooadd eylemin Hello adımları izleyin.  
> 
> 

## <a name="use-a-ftp-action"></a>Bir FTP eylemi kullanın
Bir eylem, bir mantıksal uygulama tanımlı hello iş akışı tarafından gerçekleştirilen bir işlemdir. [Eylemler hakkında daha fazla bilgi](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).  

Bir tetikleyici eklediğiniz, bu adımları tooadd hello tetik tarafından bulunan hello yeni veya değiştirilmiş dosya hello içeriğini alacak bir eylem izleyin.    

1. Seçin **+ yeni adım** tooadd hello hello eylem tooget hello hello dosyasının içeriğini hello FTP sunucusunda  
2. Select hello **Eylem Ekle** bağlantı.  
   ![FTP eylem görüntü 1](./media/connectors-create-api-ftp/ftp-action-1.png)  
3. Girin *FTP* toosearch tüm eylemler için ilgili tooFTP.
4. Seçin **FTP - Al dosya içeriğini** hello FTP klasöründe yeni veya değiştirilmiş bir dosya bulunduğunda eylem tootake hello gibi.      
   ![FTP eylem görüntü 2](./media/connectors-create-api-ftp/ftp-action-2.png)  
   Merhaba **alma dosya içeriği** kontrol açar. **Not**:, istendiğinde tooauthorize FTP sunucunuza hesabını, daha önce yapmadıysanız, logic app tooaccess olacaktır.  
   ![FTP eylem görüntüsü 3](./media/connectors-create-api-ftp/ftp-action-3.png)   
5. Select hello **dosya** denetimi (Merhaba boşluk bulunan aşağıda **dosya***). Burada, herhangi bir hello çeşitli özellikleri dosyasından hello FTP sunucusunda bulunan hello yeni veya değiştirilmiş kullanabilirsiniz.  
6. Select hello **dosya içeriği** seçeneği.  
   ![FTP eylem görüntüsü 4](./media/connectors-create-api-ftp/ftp-action-4.png)   
7. Merhaba denetim güncelleştirilir, o hello belirten **FTP - Al dosya içeriğini** eylemin hello alırsınız *dosya içeriği* hello yeni veya değiştirilmiş dosyasının hello FTP sunucusundaki.      
   ![FTP eylem görüntüsü 5](./media/connectors-create-api-ftp/ftp-action-5.png)     
8. Çalışmanızı kaydedin, sonra iş akışınızı bir dosya toohello FTP klasörü tootest ekleyin.    

Bu noktada, hello mantıksal uygulama boyunca yeni bir dosya veya değiştirilmiş bir dosya hello FTP sunucusunda bulduğunda bir tetikleyici toomonitor ile bir klasör bir FTP sunucusu ve başlatma hello iş akışı yapılandırılmış. 

Merhaba mantıksal uygulama aynı zamanda bir eylem tooget hello hello yeni veya değiştirilmiş dosyasının içeriğiyle yapılandırıldı.

Hello gibi başka bir eylem artık ekleyebilirsiniz [SQL Server - Satır Ekle](connectors-create-api-sqlazure.md) eylem tooinsert hello hello yeni veya değiştirilmiş dosyasına SQL veritabanı tablosunda içeriğini.  

## <a name="connector-specific-details"></a>Bağlayıcı özgü ayrıntıları

Tüm tetikleyiciler ve Eylemler hello swagger içinde tanımlanan görüntüleyebilir ve ayrıca hello herhangi bir sınır bkz. [Bağlayıcısı ayrıntıları](/connectors/ftpconnector/). 

## <a name="next-steps"></a>Sonraki Adımlar
[Mantıksal uygulama oluşturun.](../logic-apps/logic-apps-create-a-logic-app.md)

