---
title: "aaaHow toouse SendGrid Azure işlevlerinde | Microsoft Docs"
description: "Gösterir nasıl toouse Azure işlevlerinde SendGrid"
services: functions
documentationcenter: na
author: rachelappel
manager: erikre
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 01/31/2017
ms.author: rachelap
ms.openlocfilehash: a0ffdae04e5924c773d2d26427626fc1f570f7ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-sendgrid-in-azure-functions"></a>Nasıl toouse Azure işlevlerinde SendGrid

## <a name="sendgrid-overview"></a>SendGrid genel bakış

Azure işlevleri destekler SendGrid bağlamaları tooenable birkaç satır kod ve SendGrid hesabı, işlevleri toosend e-posta iletileriyle çıktı.

toouse hello SendGrid API bir Azure işlevi'olmalıdır bir [SendGrid hesap](http://SendGrid.com). Ayrıca, bir SendGrid API anahtarı olması gerekir. Tooyour SendGrid hesap açın ve tıklayın **ayarları** sonra **API anahtarı** toogenerate bir API anahtarı. Yaklaşan bir adımda kullanırken kullanılabilir bu anahtarı tutun.

Hazır toocreate bir Azure işlevi uygulama sunulmuştur.

## <a name="create-an-azure-function-app"></a>Azure İşlev uygulaması oluşturma 

Azure işlevi uygulamaları bir veya daha fazla Azure işlevleri için kapsayıcı görevi görür. Azure işlevleri yalnızca - bir işlevi olan. Merhaba işlevi toorun neden olan bir olay bağlı tooone tetikleyici her Azure işlevdir.
Her işlevi, giriş herhangi bir sayıda içermiyor ya da bağlamaları çıktı. Bağlamaları bir işlevde kullanabileceğiniz hizmetleridir. SendGrid, bağlama çıktı toosend e-postanızı kullanabileceğiniz ' dir. 

1. Toohello Azure portalında oturum ve [Azure işlev uygulaması oluşturma](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function) veya varolan bir işlev uygulaması açın. 
2. Azure bir işlev oluşturun. tookeep basit, onu seçin bir el ile tetikleyici ve C#. 

 ![Bir Azure işlevi oluşturma](./media/functions-how-to-use-sendgrid/functions-new-function-manual-trigger-page.png)

## <a name="configure-sendgrid-for-use-in-an-azure-function-app"></a>SendGrid bir Azure işlevi uygulamada kullanmak için yapılandırma

Bir uygulama ayarı toouse SendGrid API anahtarınıza depolamanız gerekir, bir işlev. Merhaba apikey ile yapılan alan gerçek SendGrid API anahtarınıza değildir, ancak bir uygulama ayarı gerçek API anahtarınıza temsil eden tanımlayın. Herhangi bir kod veya kaynak kod denetimine iade dosyalarını ayrı olduğundan bu şekilde anahtarınızın depolanması güvenlik için kalır.

- Oluşturma bir **AppSettings** işlevi uygulamanızın anahtar **uygulama ayarları**.

 ![Bir Azure işlevi oluşturma](./media/functions-how-to-use-sendgrid/functions-configure-sendgrid-api-key-app-settings.png)

## <a name="configure-sendgrid-output-bindings"></a>SendGrid çıkış bağlamaları yapılandırma

SendGrid Azure kullanılabilir işlevi çıktı bağlama. toocreate bir SendGrid bağlama çıktı:

1. Toohello Git **tümleştir** hello Azure portal hello işlevinde sekmesinde.
2. Tıklatın **yeni çıktı** toocreate bir SendGrid çıkış bağlama.
3. Hello dolgu **API anahtarı** ve **ileti parametre adı** özellikleri. İsterseniz, girebilirsiniz diğer özellikleri artık hello veya bunun yerine kod. Bu ayarlar varsayılan olarak kullanılabilir.

 ![SendGrid çıkış bağlamaları yapılandırma](./media/functions-how-to-use-sendgrid/functions-configure-sendgrid-output-bindings.png)

Adlı bir dosya oluşturur bağlama tooa işlevi ekleme **function.json** , işlevin klasöründeki. Tüm bu dosyayı içeren hello Azure işlevin hello bkz aynı bilgileri **tümleştir** sekmesinde ancak Json biçiminde. Ayar hello **apikey ile yapılan**, **ileti**, ve **gelen** alanları oluşturmak hello girdiler aşağıdaki hello **function.json** dosyası: 

```json
{
  "bindings": [    
    {
      "type": "sendGrid",
      "name": "message",
      "apiKey": "SendGridKey",
      "direction": "out",
      "from": "azure@contoso.com"
    }
  ],
  "disabled": false
}
```

Tercih ederseniz, bu değiştirebilen kendiniz dosyasını doğrudan.

Oluşturulan ve hello işlev uygulaması ve işlevi yapılandırılmış göre bir e-posta hello kod toosend yazabilirsiniz.

## <a name="write-code-that-creates-and-sends-email"></a>Oluşturur ve e-posta gönderir. kod yazma

Merhaba SendGrid API içeren tüm hello komutları toocreate gerekir ve bir e-posta gönderin.  

- Merhaba işlevi Hello kodda koddan hello ile değiştirin:

```cs
#r "SendGrid"
using System;
using SendGrid.Helpers.Mail;

public static void Run(TraceWriter log, string input, out Mail message)
{
    message = new Mail
    {        
        Subject = "Azure news"          
    };

    var personalization = new Personalization();
    // change tooemail of recipient
    personalization.AddTo(new Email("MoreEmailPlease@contoso.com"));   

    Content content = new Content
    {
        Type = "text/plain",
        Value = input
    };
    message.AddContent(content);
    message.AddPersonalization(personalization);
}
```

Bildirim hello ilk satırında hello ```#r``` hello SendGrid derlemeye başvuran yönergesi. Bundan sonra kullanabileceğiniz bir ```using``` deyimi toomore hello nesneleri bu ad alanındaki kolayca erişebilirsiniz. Merhaba kodda örneklerini oluşturmak ```Mail```, ```Personalization```, ve ```Content``` hello e-posta oluştur hello SendGrid API nesnelerden. SendGrid selamlama iletisine döndüğünüzde sağlar. 

Merhaba işlevin imza ayrıca fazladan çıkış parametresi türü içeren ```Mail``` adlı ```message```. Her ikisi de giriş ve bağlamaları express kendilerini kod işlevi parametre olarak çıkış. 

2. Kodunuzu tıklayarak test **Test** ve bir ileti hello girerek **istek gövdesinde** alan sonra hello tıklatarak **çalıştırmak** düğmesi.

 ![Kodunuzu test](./media/functions-how-to-use-sendgrid/functions-develop-test-sendgrid.png)

3. SendGrid hello e-posta gönderilen e-posta tooverify denetleyin. Adım 1'den toohello adresi hello kodda gidin ve hello hello iletiden içeren **istek gövdesinde**.

## <a name="next-steps"></a>Sonraki adımlar
Bu makalede, nasıl toouse SendGrid hizmet toocreate hello ve e-posta Gönder gösterilmiştir. Uygulamalarınızda, Azure işlevlerini kullanma hakkında daha fazla toolearn aşağıdaki konularda hello bakın: 

- [En iyi uygulamalar için Azure işlevleri](functions-best-practices.md) Azure işlevleri oluşturulurken bazı en iyi yöntemler toouse listeler.

- [Azure işlevleri Geliştirici Başvurusu](functions-reference.md) işlevleri kodlamak ve tetikleyicileri ve bağlamaları tanımlamak için Programcı Başvurusu.

- [Azure işlevlerini test etme](functions-test-a-function.md) çeşitli araçları ve teknikleri işlevlerinizi test etmek için açıklar.