## <a name="typical-output"></a>Normal çıktı

Merhaba aşağıdaki örnekte toohello günlük dosyası hello Hello World örnek tarafından yazılmış hello çıktısı gösterilmektedir. Merhaba çıktı için okunabilirliği biçimlendirilmiş:

```json
[{
    "time": "Mon Apr 11 13:48:07 2016",
    "content": "Log started"
}, {
    "time": "Mon Apr 11 13:48:48 2016",
    "properties": {
        "helloWorld": "from Azure IoT Gateway SDK simple sample!"
    },
    "content": "aGVsbG8gd29ybGQ="
}, {
    "time": "Mon Apr 11 13:48:55 2016",
    "properties": {
        "helloWorld": "from Azure IoT Gateway SDK simple sample!"
    },
    "content": "aGVsbG8gd29ybGQ="
}, {
    "time": "Mon Apr 11 13:49:01 2016",
    "properties": {
        "helloWorld": "from Azure IoT Gateway SDK simple sample!"
    },
    "content": "aGVsbG8gd29ybGQ="
}, {
    "time": "Mon Apr 11 13:49:04 2016",
    "content": "Log stopped"
}]
```

## <a name="code-snippets"></a>Kod parçacıkları

Bu bölümde bazı anahtar bölümler hello hello hello kod ele alınmaktadır\_world örneği.

### <a name="iot-edge-gateway-creation"></a>IOT sınır ağ geçidi oluşturma

Uygulamanız gereken bir *ağ geçidi işlem*. Bu program hello iç altyapı (Merhaba Aracısı) oluşturur, hello IOT kenar modüllerini yükler ve hello ağ geçidi işlem yapılandırır. IOT kenar sağlar hello **ağ geçidi\_oluşturma\_gelen\_JSON** tooenable işlev bir JSON dosyası bir ağ geçidi toobootstrap. toouse hello **ağ geçidi\_oluşturma\_gelen\_JSON** işlev, hello IOT kenar modülleri tooload belirtir hello yol tooa JSON dosyası geçirin.

Merhaba ağ geçidi hello işleminde hello kod bulabilirsiniz *Hello World* hello örnek [main.c] [ lnk-main-c] dosya. Okunabilirliği için hello aşağıdaki kod parçacığında hello ağ geçidi işlem kodu kısaltılmış bir sürümünü gösterir. Bu örnek program bir ağ geçidi oluşturur ve hello kullanıcı toopress Merhaba bekler **ENTER** hello ağ geçidi çıkarır önce anahtar.

```c
int main(int argc, char** argv)
{
    GATEWAY_HANDLE gateway;
    if ((gateway = Gateway_Create_From_JSON(argv[1])) == NULL)
    {
        printf("failed toocreate hello gateway from JSON\n");
    }
    else
    {
        printf("gateway successfully created from JSON\n");
        printf("gateway shall run until ENTER is pressed\n");
        (void)getchar();
        Gateway_LL_Destroy(gateway);
    }
    return 0;
}
```

Merhaba JSON ayarları dosyası IOT kenar modülleri tooload ve hello modülleri arasında hello bağlantılar listesini içerir. Her IOT kenar modülü a: belirtmeniz gerekir

* **ad**: hello modülü için benzersiz bir ad.
* **Yükleyici**: tooload hello modülü nasıl istenen bildiği bir yükleyicisi. Yükleyiciler, farklı türlerdeki modüllerin yüklenmesi için bir uzantı noktasıdır. IOT kenar yükleyicilerini kullanım için yerel C, Node.js, Java ve .NET içinde yazılmış modüller sağlar. Bu örnekteki tüm hello modülleri dinamik kitaplıkları c dilinde yazılmış olduğundan hello Hello World örnek hello yerel C yükleyicisi yalnızca kullanır. Hakkında daha fazla bilgi için bkz: hello farklı dillerde yazılmış toouse IOT kenar modülleri [Node.js](https://github.com/Azure/iot-edge/blob/master/samples/nodejs_simple_sample/), [Java](https://github.com/Azure/iot-edge/tree/master/samples/java_sample), veya [.NET](https://github.com/Azure/iot-edge/tree/master/samples/dotnet_binding_sample) örnekleri.
    * **ad**: kullanılan tooload hello modülü hello yükleyicisi hello adı.
    * **EntryPoint**: hello modülü içeren hello yolu toohello kitaplığı. Linux için bu kitaplık bir .so dosyası, Windows'ta ise bir .dll dosyasıdır. Merhaba giriş noktası belirli toohello kullanılan yükleyicisi türüdür. Merhaba Node.js yükleyicisi giriş noktası bir .js dosya yok. Merhaba Java yükleyicisi giriş noktası bir sınıf ve sınıf adı ' dir. Merhaba .NET yükleyicisi giriş noktası bir derleme adı ve bir sınıf adıdır.

* **bağımsız değişken**: herhangi bir yapılandırma bilgileri hello modülü gerekiyor.

Aşağıdaki kodu gösterir hello kullanılan JSON toodeclare tüm hello IOT kenar modülleri hello Hello World Örnek Linux için hello. Bir modül herhangi bir bağımsız değişken gerektirip gerektirmediğini hello modülü hello tasarımına bağlıdır. Bu örnekte, hello Günlükçü modülü hello yolu toohello çıkış dosyasını ve hello hello olmayan bir bağımsız değişken alan\_world modülü bir bağımsız değişken içeriyor.

```json
"modules" :
[
    {
        "name" : "logger",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "./modules/logger/liblogger.so"
        }
        },
        "args" : {"filename":"log.txt"}
    },
    {
        "name" : "hello_world",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "./modules/hello_world/libhello_world.so"
        }
        },
        "args" : null
    }
]
```

Merhaba JSON dosyası ayrıca toohello Aracısı geçirilen hello modülleri arasında hello bağlantılar içerir. Bir bağlantı iki özelliğe sahiptir:

* **Kaynak**: hello modülü adından `modules` bölümünde veya `\*`.
* **Havuz**: hello modülü adından `modules` bölümü.

Her bağlantı bir ileti yolu ve yönü tanımlar. Merhaba iletilerden **kaynak** toohello modülü teslim edilen **havuz** modülü. Merhaba ayarlayabilirsiniz **kaynak** modülü çok`\*`, o hello gösterir **havuz** modülü herhangi bir modül iletileri alır.

Merhaba aşağıdaki kod hello JSON tooconfigure bağlantılar hello hello kullanılan hello modülleri arasında kullanılan gösterir\_Linux'ta world örneği. Her ileti hello tarafından üretilen `hello_world` modülü hello tarafından tüketilen `logger` modülü.

```json
"links":
[
    {
        "source": "hello_world",
        "sink": "logger"
    }
]
```

### <a name="helloworld-module-message-publishing"></a>Merhaba\_dünya modülü ileti yayımlama

Merhaba hello tarafından kullanılan hello kodu bulabilirsiniz\_hello world modülü toopublish iletileri ['hello_world.c'] [ lnk-helloworld-c] dosya. Merhaba aşağıdaki kod parçacığında hello kodu değiştirilmiş bir sürümünü eklenen açıklamalar ve bazı hata işleme için okunabilirliği kaldırılan kodunu gösterir:

```c
int helloWorldThread(void *param)
{
    // create data structures used in function.
    HELLOWORLD_HANDLE_DATA* handleData = param;
    MESSAGE_CONFIG msgConfig;
    MAP_HANDLE propertiesMap = Map_Create(NULL);

    // add a property named "helloWorld" with a value of "from Azure IoT
    // Gateway SDK simple sample!" tooa set of message properties that
    // will be appended toohello message before publishing it. 
    Map_AddOrUpdate(propertiesMap, "helloWorld", "from Azure IoT Gateway SDK simple sample!")

    // set hello content for hello message
    msgConfig.size = strlen(HELLOWORLD_MESSAGE);
    msgConfig.source = HELLOWORLD_MESSAGE;

    // set hello properties for hello message
    msgConfig.sourceProperties = propertiesMap;

    // create a message based on hello msgConfig structure
    MESSAGE_HANDLE helloWorldMessage = Message_Create(&msgConfig);

    while (1)
    {
        if (handleData->stopThread)
        {
            (void)Unlock(handleData->lockHandle);
            break; /*gets out of hello thread*/
        }
        else
        {
            // publish hello message toohello broker
            (void)Broker_Publish(handleData->brokerHandle, helloWorldMessage);
            (void)Unlock(handleData->lockHandle);
        }

        (void)ThreadAPI_Sleep(5000); /*every 5 seconds*/
    }

    Message_Destroy(helloWorldMessage);

    return 0;
}
```

### <a name="helloworld-module-message-processing"></a>Merhaba\_dünya modülü ileti işleme

Merhaba hello\_world modülü iletileri diğer IOT kenar modüller toohello Aracısı yayımlama hiçbir zaman işler. Bu nedenle, hello hello hello ileti geri uyarlamasını hello\_world modülüdür yok işlevi.

```c
static void HelloWorld_Receive(MODULE_HANDLE moduleHandle, MESSAGE_HANDLE messageHandle)
{
    /* No action, HelloWorld is not interested in any messages. */
}
```

### <a name="logger-module-message-publishing-and-processing"></a>Günlükçü modülü ileti yayımlama ve işleme

Merhaba Günlükçü modülü hello Aracısı'ndan iletilerini alır ve bunları tooa dosyasına yazar. Hiçbir zaman bir ileti yayımlamaz. Bu nedenle, hello kod hello Günlükçü modülü hello hiçbir zaman çağırır **Broker_Publish** işlevi.

Merhaba **Logger_Receive** hello işlevinde [logger.c] [ lnk-logger-c] dosyasıdır hello geri çağırma hello Aracısı toodeliver iletileri toohello Günlükçü modülü çağırır. Merhaba aşağıdaki kod parçacığında değiştirilmiş bir sürümünü eklenen açıklamalar ve bazı hata işleme için okunabilirliği kaldırılan kodunu gösterir:

```c
static void Logger_Receive(MODULE_HANDLE moduleHandle, MESSAGE_HANDLE messageHandle)
{

    time_t temp = time(NULL);
    struct tm* t = localtime(&temp);
    char timetemp[80] = { 0 };

    // Get hello message properties from hello message
    CONSTMAP_HANDLE originalProperties = Message_GetProperties(messageHandle); 
    MAP_HANDLE propertiesAsMap = ConstMap_CloneWriteable(originalProperties);

    // Convert hello collection of properties into a JSON string
    STRING_HANDLE jsonProperties = Map_ToJSON(propertiesAsMap);

    //  base64 encode hello message content
    const CONSTBUFFER * content = Message_GetContent(messageHandle);
    STRING_HANDLE contentAsJSON = Base64_Encode_Bytes(content->buffer, content->size);

    // Start hello construction of hello final string toobe logged by adding
    // hello timestamp
    STRING_HANDLE jsonToBeAppended = STRING_construct(",{\"time\":\"");
    STRING_concat(jsonToBeAppended, timetemp);

    // Add hello message properties
    STRING_concat(jsonToBeAppended, "\",\"properties\":"); 
    STRING_concat_with_STRING(jsonToBeAppended, jsonProperties);

    // Add hello content
    STRING_concat(jsonToBeAppended, ",\"content\":\"");
    STRING_concat_with_STRING(jsonToBeAppended, contentAsJSON);
    STRING_concat(jsonToBeAppended, "\"}]");

    // Write hello formatted string
    LOGGER_HANDLE_DATA *handleData = (LOGGER_HANDLE_DATA *)moduleHandle;
    addJSONString(handleData->fout, STRING_c_str(jsonToBeAppended);
}
```

## <a name="next-steps"></a>Sonraki adımlar

Bu makalede, iletileri tooa günlük dosyasına yazar basit bir IOT sınır ağ geçidi verdi. toorun iletileri tooIoT Hub, gönderdiği bir örnek görmek [IOT kenar – Linux kullanmak için sanal bir cihaz cihaz bulut iletilerini göndermek] [ lnk-gateway-simulated-linux] veya [IOT kenar – sahip cihaz bulut iletilerini göndermek bir Windows kullanarak sanal cihaz][lnk-gateway-simulated-windows].


<!-- Links -->
[lnk-main-c]: https://github.com/Azure/iot-edge/blob/master/samples/hello_world/src/main.c
[lnk-helloworld-c]: https://github.com/Azure/iot-edge/blob/master/modules/hello_world/src/hello_world.c
[lnk-logger-c]: https://github.com/Azure/iot-edge/blob/master/modules/logger/src/logger.c
[lnk-iot-edge]: https://github.com/Azure/iot-edge/
[lnk-gateway-simulated-linux]: ../articles/iot-hub/iot-hub-linux-iot-edge-simulated-device.md
[lnk-gateway-simulated-windows]: ../articles/iot-hub/iot-hub-windows-iot-edge-simulated-device.md