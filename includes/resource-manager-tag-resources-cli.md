tooadd bir etiket tooa kaynak grubu kullanmak **azure Grup kümesini**. Merhaba kaynak grubu varolan etiketleri yoksa hello etiketinde geçirin.

```azurecli
azure group set -n tag-demo-group -t Dept=Finance
```

Etiketler, bir bütün olarak güncelleştirilir. Tooadd varolan etiketleri olan bir etiketi tooa kaynak grubu istiyorsanız, tüm hello etiketleri geçirin. 

```azurecli
azure group set -n tag-demo-group -t Dept=Finance;Environment=Production;Project=Upgrade
```

Etiketler, bir kaynak grubunda kaynaklar tarafından devralınmaz. tooadd etiketi tooa kaynak kullanmak **azure kaynak kümesi**. Merhaba hello etiket ekleme hello kaynak türü için API sürüm numarası geçirin. Tooretrieve hello API sürümü gerekiyorsa, hello kaynak sağlayıcısı hello türü için ayarladığınız komutuyla aşağıdaki hello kullan:

```azurecli
azure provider show -n Microsoft.Storage --json
```

Merhaba sonuçlarında hello kaynak türü için istediğiniz arayın.

```azurecli
"resourceTypes": [
{
  "resourceType": "storageAccounts",
  ...
  "apiVersions": [
    "2016-01-01",
    "2015-06-15",
    "2015-05-01-preview"
  ]
}
...
```

Şimdi, bu API sürümü sağlayın kaynak grubu adı, kaynak adı, kaynak türü ve parametreler olarak etiket değeri.

```azurecli
azure resource set -g tag-demo-group -n storagetagdemo -r Microsoft.Storage/storageAccounts -t Dept=Finance -o 2016-01-01
```

Etiketler, doğrudan kaynakları ve kaynak gruplarını yok. bir kaynak grubu ve kaynaklarını ile toosee hello varolan etiketleri, Al **azure Grup Göster**.

```azurecli
azure group show -n tag-demo-group --json
```

Hangi hello kaynak grubu, tüm uygulanan etiketleri tooit dahil olmak üzere ilgili meta verileri döndürür.

```azurecli
{
  "id": "/subscriptions/4705409c-9372-42f0-914c-64a504530837/resourceGroups/tag-demo-group",
  "name": "tag-demo-group",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "location": "southcentralus",
  "tags": {
    "Dept": "Finance",
    "Environment": "Production",
    "Project": "Upgrade"
  },
  ...
}
```

Belirli bir kaynak için hello etiketleri kullanarak görüntüleme **azure kaynak Göster**.

```azurecli
azure resource show -g tag-demo-group -n storagetagdemo -r Microsoft.Storage/storageAccounts -o 2016-01-01 --json
```

tooretrieve bir etiket değeri ile tüm hello kaynakları kullanın:

```azurecli
azure resource list -t Dept=Finance --json
```

tooretrieve bir etiket değeri tüm hello kaynak gruplarıyla kullanın:

```azurecli
azure group list -t Dept=Finance
```

Komutu aşağıdaki hello ile aboneliğinizde hello varolan etiketleri görüntüleyebilirsiniz:

```azurecli
azure tag list
```
