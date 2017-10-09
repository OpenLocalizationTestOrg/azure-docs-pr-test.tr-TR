Azure Resource Manager ile tanımladığınız parametreler için değerler hello şablon dağıtıldığında toospecify istediğiniz. Merhaba şablonu tüm hello parametre değerlerini içeren parametreleri adlı bir bölüm içerir.
Dağıttığınız hello projesini temel alan veya dağıttığınız hello ortamı dayanarak değişir bu değerleri için bir parametre tanımlamanız gerekir. Her zaman kalacak değerleri aynı hello için parametreleri tanımlamayın. Her parametre değeri dağıtılan hello şablonu toodefine hello kaynaklarında kullanılır. 

Parametreleri tanımlarken hello kullanın **allowedValues** kullanıcı değerleri alan toospecify dağıtımı sırasında sağlayabilir. Kullanım hello **defaultValue** alan tooassign dağıtımı sırasında herhangi bir değer sağlanmazsa bir değer toohello parametresi.

Biz hello şablonundaki her bir parametreyi anlatmaktadır.

### <a name="sitename"></a>SiteName
Merhaba web uygulamasının toocreate istediğiniz Hello adı.

    "siteName":{
      "type":"string"
    }

### <a name="hostingplanname"></a>hostingPlanName
Merhaba hello uygulama hizmeti adını hello web uygulamasını barındırmak için toouse planlayın.

    "hostingPlanName":{
      "type":"string"
    }

### <a name="sku"></a>SKU
Fiyatlandırma katmanı hello barındırma planı için hello.

    "sku": {
      "type": "string",
      "allowedValues": [
        "F1",
        "D1",
        "B1",
        "B2",
        "B3",
        "S1",
        "S2",
        "S3",
        "P1",
        "P2",
        "P3",
        "P4"
      ],
      "defaultValue": "S1",
      "metadata": {
        "description": "hello pricing tier for hello hosting plan."
      }
    }

Hello şablonu, bu parametre için izin verilen hello değerleri tanımlar ve herhangi bir değer belirtilmişse, varsayılan değer (S1) atar.

### <a name="workersize"></a>workerSize
barındırma planı (küçük, Orta veya büyük) hello Hello örnek boyutu.

    "workerSize":{
      "type":"string",
      "allowedValues":[
        "0",
        "1",
        "2"
      ],
      "defaultValue":"0"
    }

Merhaba şablonu (0, 1 veya 2) Bu parametre için izin verilen hello değerleri tanımlar ve herhangi bir değer belirtilmezse varsayılan değer (0) atar. Merhaba değerler toosmall, Orta ve büyük karşılık gelir.

