Azure Resource Manager ile tanımladığınız parametreler için değerler hello şablon dağıtıldığında toospecify istediğiniz. Merhaba şablonu tüm hello parametre değerlerini içeren parametreleri adlı bir bölüm içerir.
Dağıttığınız hello projesini temel alan veya dağıttığınız hello ortamı dayanarak değişir bu değerleri için bir parametre tanımlamanız gerekir. Her zaman kalacak değerleri aynı hello için parametreleri tanımlamayın. Her parametre değeri olan kaynaklar dağıtmak hello şablonu toodefine hello kullanılır. 

Parametreleri tanımlarken hello kullanın **allowedValues** kullanıcı değerleri alan toospecify dağıtımı sırasında sağlayabilir. Kullanım hello **defaultValue** alan tooassign dağıtımı sırasında herhangi bir değer sağlanmazsa bir değer toohello parametresi.

Biz hello şablonundaki her bir parametreyi anlatmaktadır.

### <a name="logicappname"></a>logicAppName
Merhaba mantığı uygulama toocreate Hello adı.

    "logicAppName": {
        "type": "string"
    }