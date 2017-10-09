Azure Storage’daki her blob bir kapsayıcıda yer almalıdır. Merhaba kapsayıcı forms bölümü hello blob adı. Örneğin, `mycontainer` Bu örnek blob Urı'lerinde hello kapsayıcısında hello adıdır:

    https://storagesample.blob.core.windows.net/mycontainer/blob1.txt
    https://storagesample.blob.core.windows.net/mycontainer/photos/myphoto.jpg

Bir kapsayıcı adı geçerli bir DNS adı olan adlandırma kuralları aşağıdaki uyumlu toohello olması gerekir:

1. Kapsayıcı adları bir harf veya sayı ile başlamalı ve yalnızca harf, rakam ve tire (-) karakterinden hello içerebilir.
2. Her tire (-) karakterinin hemen önünde ve arkasında bir harf veya rakam bulunmalıdır; kapsayıcı adlarında art arda tirelere izin verilmez.
3. Kapsayıcı adındaki tüm harfler küçük harf olmalıdır.
4. Kapsayıcı adları 3-63 karakter arası uzunlukta olmalıdır.

> [!IMPORTANT]
> Bu hello Not kapsayıcı adının her zaman küçük olmalıdır. Kapsayıcı adına bir büyük harf eklemek ya da aksi takdirde hello kapsayıcı adlandırma kurallarını ihlal 400 hatası (Hatalı istek) alabilirsiniz. 
> 
> 

