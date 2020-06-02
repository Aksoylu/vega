---
description: Öğrenme Metodolojisi
---

# Öğrenme Metodolojisi

Epoch ve Learning Rate sayısı en iyi olarak deneme-yanılma yöntemi ile bulunabilir.

* Bir süre sonra Epoch arttıkça düşmesi gereken loss değeri artışa geçebilir. Bu, öğrenmenin tersine \(zararına\) gerçekleştiğini gösterebilir ve olabilecek bir durumdur. Ağ optimum duruma geldiğinde genellikle dropout veya benzeri işlemlerin ağ üzerinde yapılması faydalı olabilir. Vega henüz bu teknikleri içermediğinden el ile yapılması tavsiye edilir.
* Eğer ağ öğreniminin tıkanması durumunda ağırlık değerlerinde rastsal bir filtre uygulanması, geçici bir süre için ağın öğrenimini geri plana atsa da daha ileri gidebilmesi için olanak oluşturabilir.
* Loss değerinin optimum değere geldiğinde öğrenimin kesilmesi gerekir. Öğrenim kesildiğinde ağın kaydedilmesi için saveLock değerinin true olarak ayarlanması önemlidir. Aynı şekilde, kestirebiliyorsanız EpochLock’da sizin için yeterli olacaktır.
* Vega, multithreading desteklemez bu sebeple çok yavaştır. Ancak bu, bilgisayar kaynaklarının çok fazla işgal edilmediği anlamına da gelir. Vega ile öğrenim süreci yavaş olacaktır ancak bilgisayarınızı kullanmanızda bir sorun da hissettirmeyecektir. Vega’nın ileri sürümlerinde bu kullanıcının tercihine sunulmak üzere opsiyonel bir seçenek haline getirilecektir.
* Bir TCP/Soket yordamı ile ağırlıkların birden fazla cihaza gönderilmesi ile paralel öğrenme gerçekleştirilebilir. Bu da dağıtık bir sistem oluşturulması ve bu sistemin bir ağ eğitiminde kullanılmasında işlevsel olabilir. Vega’nın ilerleyen sürümlerinde TCP/Soket yordamı ile dağıtık ağ öğreninin gerçeklenmesi hedeflenmektedir.

\*\*\*\*

