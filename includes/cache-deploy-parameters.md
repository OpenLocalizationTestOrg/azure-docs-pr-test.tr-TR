
### <a name="cacheskuname"></a>cacheSKUName
Fiyatlandırma katmanı hello Hello yeni Azure Redis önbelleği.

    "cacheSKUName": {
      "type": "string",
      "allowedValues": [
        "Basic",
        "Standard"
      ],
      "defaultValue": "Basic",
      "metadata": {
        "description": "hello pricing tier of hello new Azure Redis Cache."
      }
    },

Merhaba şablonu (temel veya standart) Bu parametre için izin verilen ve herhangi bir değer belirtilmezse varsayılan değer (Temel) atayan hello değerleri tanımlar. Basic too53 GB kullanılabilir birden çok boyutu ile tek bir düğüm sağlar.
Standart, iki düğümlü birincil/çoğaltma too53 GB ve % 99,9 SLA kullanılabilir birden çok boyutu, sağlar.

### <a name="cacheskufamily"></a>cacheSKUFamily
Merhaba sku ailesi Hello.

    "cacheSKUFamily": {
      "type": "string",
      "allowedValues": [
        "C"
      ],
      "defaultValue": "C",
      "metadata": {
        "description": "hello family for hello sku."
      }
    },


### <a name="cacheskucapacity"></a>cacheSKUCapacity
Merhaba yeni Azure Redis önbelleği örneği Hello boyutu. 

    "cacheSKUCapacity": {
      "type": "int",
      "allowedValues": [
        0,
        1,
        2,
        3,
        4,
        5,
        6
      ],
      "defaultValue": 0,
      "metadata": {
        "description": "hello size of hello new Azure Redis Cache instance. "
      }
    }


Merhaba şablonu (0, 1, 2, 3, 4, 5 veya 6) Bu parametre için izin verilen hello değerleri tanımlar ve herhangi bir değer belirtilmişse, varsayılan değer (1) atar. Bu sayılar toofollowing önbellek boyutlarını karşılık gelir: 0 = 250 MB, 1 = 1 GB, 2 = 2,5 GB, 3 = 6 GB, 4 = 13 GB, 5 = 26 GB, 6 = 53 GB'a

