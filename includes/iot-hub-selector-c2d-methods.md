> [!div class="op_single_selector"]
> * [Node.js](../articles/iot-hub/iot-hub-node-node-direct-methods.md)
> * [C#/node.js](../articles/iot-hub/iot-hub-csharp-node-direct-methods.md)
> * [C#](../articles/iot-hub/iot-hub-csharp-csharp-direct-methods.md)
> * [Java](../articles/iot-hub/iot-hub-java-java-direct-methods.md)

Azure IOT Hub güvenilir sağlayan tam olarak yönetilen bir hizmettir ve arka uç milyonlarca cihaza ve çözüm arasında güvenli çift yönlü iletişim. Önceki öğreticileri ([IOT Hub ile çalışmaya başlama] ve [IOT Hub ile bulut cihaza ileti gönderme]) IOT Hub'ın temel cihaz Bulut ve bulut-cihaz Mesajlaşma işlevlerini gösterilmektedir. IOT Hub ayrıca bulutta cihazlarda dayanıklı olmayan yöntemlerini çağırmasına olanak sağlar. Başarılı veya çağrı durumunu bilmeniz kullanıcı izin vermek hemen (bir kullanıcı tarafından belirtilen zaman aşımından sonra) başarısız bir istek-yanıt etkileşim için bir HTTP çağrısıyla benzer bir cihaz ile doğrudan yöntemleri temsil eder. [Bir cihazda doğrudan bir yöntem çağırma] [ lnk-devguide-methods] doğrudan yöntemler daha ayrıntılı açıklanır ve ne zaman doğrudan yöntemleri yerine bulut-cihaz iletilerini ya da istenen özellikleri kullanılacağı hakkında yönergeler sunar.

Bu öğretici şunların nasıl yapıldığını gösterir:

* IOT hub'ı oluşturun ve IOT hub'ınızda bir cihaz kimliği oluşturma için Azure Portalı'nı kullanın.
* Bulut tarafından çağrılan doğrudan bir yönteme sahip bir sanal cihaz uygulaması oluşturursunuz.
* Sanal cihaz uygulama IOT hub'ınız aracılığıyla doğrudan bir yöntem çağırır bir konsol uygulaması oluşturun.

> [!NOTE]
> Şu anda doğrudan yöntemleri yalnızca MQTT protokolünü kullanarak IOT hub'a bağlanan cihazlarda desteklenir. Lütfen [MQTT Destek] [ lnk-devguide-mqtt] MQTT kullanmak mevcut cihaz uygulaması dönüştürme hakkında yönergeler için makalenin.


[lnk-devguide-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: ../articles/iot-hub/iot-hub-mqtt-support.md

[IOT Hub ile bulut cihaza ileti gönderme]: ../articles/iot-hub/iot-hub-csharp-csharp-c2d.md
[IOT Hub ile çalışmaya başlama]: ../articles/iot-hub/iot-hub-node-node-getstarted.md