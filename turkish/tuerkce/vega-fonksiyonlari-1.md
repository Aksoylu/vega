---
description: Vega Fonksiyonları
---

# Vega Fonksiyonları

**1- vega.Katman \(Ağ oluşturmak\)**

neuralNetwork = vega.Katman\(\[4,4\], \[36,36\]\)

neuralNetwork isminde ve 2 gizli katmana, toplam 4 katmana sahip, her bir katmanda 4 nöronun ve her nöronun da 36 weight\(bağlantı\) sayısına sahip olduğu bir ağ oluşturur.

İlk parametre olan \[4,4\] 4 nöronlu birinci ve 4 nöronlu ikinci katmanı oluşturur.

İkinci parametre olan \[36,36\] ise birinci katmanda 36, ikinci katmanda da 36 bağlantı \(weight\) oluşturulmasını sağlar.

Örneğin vega.Katman\(\[3,2\], \[12,2\]\) çağrısı, ilk katmanın 3, ikinci katmanın 2 nörona sahip olduğu ve ilk katmandaki nöronların 12 weight sayısı, ikinci katmandaki nöronların ise 2 weight sayısına sahip olduğu bir ağ yapısını inşa eder.

**2- &lt;Ağ&gt;.Name \(Ağ’a isim vermek\)**

neuralNetwork.name = "test\_network"

neuralNetwork adı ile oluşturulan nesne bir yapay sinir ağıdır. Bu ağa .name metodu ile isim verilebilir. Bu verilen isim kullanılarak eğitilmiş ağ Vega tarafından “.neurons” dosyası olarak kaydedilir.

**3- &lt;Ağ&gt;.loadModel \(.neurons dosyasından ağ’ı yüklemek\)**

neuralNetwork.loadModel\("gozs.neurons"\)

**gozs.neurons** dosyasında kayıt edilmiş ağı tekrar belleğe yükler ve kullanıma \(prediction’a\) hazır hale getirir. Eğer katman fonksiyonunu kullanarak bir yapı oluşturmuş iseniz, yüklenilen model ile oluşturduğunuz modelin katman, nöron ve weight sayılarının eşleşmesine özen gösterin. Bu işlemden sonra train fonksiyonunun tekrar çalıştırılmasına ihtiyaç yoktur. Doğrudan feedForward metodu kullanılarak ağ’a tahmin yaptırılabilir.

Not: Eğer ağınızın öğrenmesi yarım kalmış ise ağı yükledikten sonra train fonksiyonunu çalıştırırsanız, ağ kaldığı yerden öğrenmeye devam edecektir.

**4- &lt;Ağ&gt;.train \(Ağı eğitmek\)**

learning\_rate = 0.001

epoch = 1000

\#Now Learning Time

SinirAgi.train\(dataset, targets,learning\_rate, epoch\)

Dataset ve targets nesneleri, aynı sayıda eleman içeren Numpy array nesneleridir. Aynı sayıda nesne içermeleri önemlidir zira dataset’de tahmin edilecek veri ve targets’de de o veri ile eşleşen sonuç içerilmektedir. Yani ağ, dataset verisi ile targets verisi arasında ilişki kuracak biçimde eğitilecektir.

**Learning Rate :** Öğrenme adımıdır. Küçük olması durumunda ağ daha yavaş eğitilebilir. Ancak büyütülürse backPropagation fonksiyonunun yürürlüğe girmeme ihtimali oluşabileceğinden hiç eğitilmeye de bilir. Çoğunlukla deneme yanılma yöntemi ile en iyi learning rate değeri bulunabilir.

**Epoch :** \(aynı\) dataset verisinin ağı eğitmek için kaç defa ağ’dan ileri besleme yolu ile geçirilmesi gerektiği sayısıdır. Yüksek olması öğrenme ihtimalini arttırır ancak aşırı fazla Epoch \(devir\) sayısı, yapay sinir ağının ezberci davranmasını ve dataset-target arası mantıksal ilişki kurmak yerine bu ikişkiyi ezberlemesine sebebiyet verebilir.

**5- &lt;Ağ&gt;.feedforward\(Ağ’da ileri besleme\)**

prediction = neuralNetwork.feedforward\(testData\)

print\(prediction\)

testData nesnesi, ağın eğitilmesi için kullanılan dataset arrayList’inin elemanlarından biri ile aynı yapıda ve eleman sayısında olmalıdır. Ağ, bu veriyi işleyerek buna uygun target layer’ından bir benzetme yapacaktır.

Örneğin ağ eğitilirken sonuçların 1 veya 0 olması ağ’a target verisinde belirtilmişse, eğitilmiş ağ verinizi feedforward metodu ile işledikten size bir değer döndürecektir. Bu değerin 1’e veya 0’a yakın olması \(veya belirlediğiniz aralıkta olması\), işleminiz için anlamlı bir sonuç olacaktır. Böylece eğitilmiş ağ, size istediğiniz biçimde dönüş yapabilir.

**6-&lt;Ağ&gt;.saveLock**

neuralNetwork.saveLock\(True\) \#save model if program closes

True veya False değer alabilir. SaveLock, eğer öğrenme aşamasında program herhangi bir sebepten kapanırsa öğrenmekte olan modelin otomatik olarak kayıt edilmesini sağlar.

**7-&lt;Ağ&gt;.setEpochLock**

neuralNetwork.setEpochLock\(200\) \#save model per 200 epoch

Öğrenme \(Train\) fonksiyonu çalıştırılmadan önce çalıştırılmalıdır. Yukarıdaki örnekte her 200 epoch’da bir yapay sinir ağı modelinin kayıt edilmesini sağlar

