> [!div class="op_single_selector"]
> * [Node.js](../articles/iot-hub/iot-hub-node-node-direct-methods.md)
> * [C#/node.js](../articles/iot-hub/iot-hub-csharp-node-direct-methods.md)
> * [C#](../articles/iot-hub/iot-hub-csharp-csharp-direct-methods.md)
> * [Java](../articles/iot-hub/iot-hub-java-java-direct-methods.md)

Azure IOT Hub güvenilir sağlayan tam olarak yönetilen bir hizmettir ve arka uç milyonlarca cihaza ve çözüm arasında güvenli çift yönlü iletişim. Önceki öğreticileri ([IOT Hub ile çalışmaya başlama] ve [IOT Hub ile bulut cihaza ileti gönderme]) hello temel cihaz Bulut ve bulut-cihaz Mesajlaşma işlevlerini IOT Hub'ının gösterilmektedir. IOT hub'ı da size hello hello bulut aygıtlardan özelliği tooinvoke dayanıklı olmayan yöntemleri. Yöntemleri gösteren bir istek-yanıt etkileşimi doğrudan toolet hello kullanıcı HTTP çağrı başarılı veya başarısız hemen (bir kullanıcı tarafından belirtilen zaman aşımından sonra), bir cihaz benzer tooan ile Merhaba çağrısı hello durumunu bildirin. [Bir cihazda doğrudan bir yöntem çağırma] [ lnk-devguide-methods] doğrudan yöntemler daha ayrıntılı açıklanır ve ne zaman toouse doğrudan yöntemleri yerine bulut-cihaz iletilerini ya da istenen özellikleri hakkında yönergeler sunar.

Bu öğretici şunların nasıl yapıldığını gösterir:

* IOT hub'ınızda bir cihaz kimliği oluşturma ve Hello Azure portal toocreate IOT hub'ı kullanın.
* Merhaba bulut tarafından çağrılan doğrudan bir yönteme sahip bir sanal cihaz uygulaması oluşturursunuz.
* Merhaba sanal cihaz uygulamasında IOT hub'ınız aracılığıyla doğrudan bir yöntem çağırır bir konsol uygulaması oluşturun.

> [!NOTE]
> Şu anda doğrudan MQTT Protokolü tooIoT hub'ı kullanarak bağlanan üzerinde desteklenen aygıtlar hello yöntemleridir. Lütfen toohello bakın [MQTT Destek] [ lnk-devguide-mqtt] hakkında yönergeler için makalenin tooconvert mevcut aygıt uygulama toouse MQTT.


[lnk-devguide-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: ../articles/iot-hub/iot-hub-mqtt-support.md

[IOT Hub ile bulut cihaza ileti gönderme]: ../articles/iot-hub/iot-hub-csharp-csharp-c2d.md
[IOT Hub ile çalışmaya başlama]: ../articles/iot-hub/iot-hub-node-node-getstarted.md