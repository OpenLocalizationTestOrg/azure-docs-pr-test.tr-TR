
bir ana bilgisayar yapılandırma dosyası ve her biri aşağıdaki örneğine hello olduğu gibi ayrı bir işleve hello kodunu içeren bir veya daha fazla klasörleri içeren bir kök klasöründeki tüm verilen işlev uygulaması hello işlevlerin Hello kodunu yaşadığı:

```
wwwroot
 | - host.json
 | - mynodefunction
 | | - function.json
 | | - index.js
 | | - node_modules
 | | | - ... packages ...
 | | - package.json
 | - mycsharpfunction
 | | - function.json
 | | - run.csx
```

Merhaba *host.json* dosyası bazı çalışma zamanı özel yapılandırma içeriyor ve hello kök klasöründe hello işlev uygulaması bulunur. Kullanılabilir ayarlar hakkında daha fazla bilgi için bkz: [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) hello WebJobs.Script depo Wiki'deki.

Her işlevi bir veya daha fazla kod dosyaları, hello function.json yapılandırma ve başka bir bağımlılık içeren bir klasörü vardır.

