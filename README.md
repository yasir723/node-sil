# Node Silme
Bu C# sınıfı, binary ağaç veri yapısını oluşturmak için kullanılır. `tree` adlı bir sınıf içerir ve `nodeSil` metodunu kullanarak ağaçtan bir düğüm silmeyi sağlar.

## `tree` Sınıfı

```csharp
class tree
{
    public int value;
    public tree right;
    public tree left;
}
```

### Özellikler

- `value`: Düğümün değerini temsil eder.
- `right`: Düğüme bağlı olan sağ alt düğümü belirtir.
- `left`: Düğüme bağlı olan sol alt düğümü belirtir.


## `nodeSil` Metodu
Bu C# metodunun amacı, verilen bir değeri ağaçtan silmektir. Ağaç içinde gezinerek belirli bir değeri bulur ve bu değeri ağaçtan kaldırır. Metot, ağacın kök düğümü ve silinecek değeri parametre olarak alır.
```csharp
static tree nodeSil(tree root, int value)
{
    if (root == null) return null;

    else if (root.value < value) // aranan value daha büyük
    {
        root.right = nodeSil(root.right, value);
    }
    else if (root.value > value) // aranan value daha küçük
    {
        root.left = nodeSil(root.left, value);
    }
    else // aranan value eşit, node u bulduk yani
    {
        if (root.left == null)
        {
            return root.right;
        }
        else if (root.right == null)
        {
            return root.left;
        }
        else
        {
            tree tmp = root.right;
            while (tmp.left != null)
            {
                tmp = tmp.left;
            }

            root.value = tmp.value;
            root.right = nodeSil(root.right, tmp.value);
        }
    }

    return root;
}
```

## Parametreler

- `node`: Ağaçtaki mevcut düğüm.
- `value`: Silenecek düğümün değeri.

## Dönüş Değeri

Metot, güncellenmiş ağaç yapısını temsil eden kök düğümü döndürür.

### İşleyiş:

1. Eğer ağacın kökü null ise, ağaç zaten boş demektir, dolayısıyla herhangi bir işlem yapmadan null döner.

2. Eğer aranan değer, kök düğümün değerinden küçükse, sağ ağaç üzerinde devam eder ve `nodeSil` metodu rekürsif olarak çağrılır.

3. Eğer aranan değer, kök düğümün değerinden büyükse, sol ağaç üzerinde devam eder ve yine `nodeSil` metodu rekürsif olarak çağrılır.

4. Eğer aranan değer, kök düğümün değerine eşitse, bu durumda silme işlemi gerçekleştirilir, bu işlemde 3 tane durum olacak:
   1. Eğer sol alt ağaç boşsa, sağ alt ağacı geri döner.
   2. Eğer sağ alt ağaç boşsa, sol alt ağacı geri döner.
   3. Eğer her iki alt ağaç da doluysa, sağ alt ağacın en küçük düğümü bulunur ve kök düğümün değeri bu düğümle değiştirilir. Ardından, sağ alt ağaç üzerinde tekrar `nodeSil` metodu çağrılır ki taşıdığımız düğüm kaldırılsın.

5. Her adımda güncellenmiş ağaç yapısı, son olarak kök düğümü geri döndürülür.

## Örnekler

<div align="center">
    <h3>Binary Ağaç</h3>
    <img src="https://github.com/yasir723/node-ekle/assets/111686779/7b94ef8d-22f2-45f7-906c-6a584c7ae6c5.png" width="600">
</div>

Yukarıdaki binary ağaçtan düğümler silme işlemi yapacağız
## $\color{aqua}{Örnek : 4 \space değeri \space olan \space düğümü \space silme \space işlemi \space gerçekleştirme}$

#### İşleyiş
- ilk olarak 4 değeri 9 ile karışlaştırılır ve daha küçük oladuğu için sola gidilir.
- 4 değeri bulana kadar arama işlemi devam edilir.
- 4 değeri düğümü bulduğunda demek `node.value == value` şartını sağlamış ve silme işlemi gerçekleştirilir.
- silenecek düğümün yerine hangi düğüm geçeceği karar vermek için alt ağaçlarını kontrol etme işlemi yapılır.
- sol alt ağaç boş olduğunu ve sağ alt ağaç boş olmadığını tespit edilir `yukarıdaki anlatıldığı işleyişin 4. maddesindeki ilk durumdur`.
- bu durumda sağ alt düğüm silenecek düğümün yerine geçilir.
- sağ alt düğüm, silenecek düğümün yerine geçtiğinde onun altındaki düğümleri koruyarak bağlı kalacak ve böylece ağaç yapısında herhangi bir kesilme olmayacaktır.

<div align="center">
    <h3>Binary Ağaç 4 değeri olan düğüm silindikten sonra</h3>
    <img src="https://github.com/yasir723/node-ekle/assets/111686779/484a305c-f1d8-411b-b271-bc4373f6a644.png" width="600">
</div>

## $\color{aqua}{Örnek : 11 \space değeri \space olan \space düğümü \space silme \space işlemi \space gerçekleştirme}$

#### İşleyiş
- ilk olarak 11 değeri 9 ile karışlaştırılır ve daha büyük oladuğu için sağ gidilir.
- 11 değeri bulana kadar arama işlemi devam edilir.
- 11 değeri düğümü bulduğunda demek `node.value == value` şartını sağlamış ve silme işlemi gerçekleştirilir.
- silenecek düğümün yerine hangi düğüm geçeceği karar vermek için alt ağaçlarını kontrol etme işlemi yapılır.
- sağ alt ağaç boş olduğunu ve sol alt ağaç boş olmadığını tespit edilir `yukarıdaki anlatıldığı işleyişin 4. maddesindeki 2. durumdur`.
- bu durumda sol alt düğüm, silenecek düğümün yerine geçilir.
- sağ alt düğüm, silenecek düğümün yerine geçtiğinde onun altındaki düğümleri koruyarak bağlı kalacak ve böylece ağaç yapısında herhangi bir kesilme olmayacaktır.

<div align="center">
    <h3>Binary Ağaç 11 değeri olan düğüm silindikten sonra</h3>
    <img src="https://github.com/yasir723/node-ekle/assets/111686779/11541aee-99d9-4449-8ee2-eb1d0eaea3b5.png" width="600">
</div>

## $\color{aqua}{Örnek : 12 \space değeri \space olan \space düğümü \space silme \space işlemi \space gerçekleştirme}$

#### İşleyiş
- ilk olarak 12 değeri 9 ile karışlaştırılır ve daha büyük oladuğu için sağ gidilir.
- 12 değeri bulana kadar arama işlemi devam edilir.
- 12 değeri düğümü bulduğunda demek `node.value == value` şartını sağlamış ve silme işlemi gerçekleştirilir.
- silenecek düğümün yerine hangi düğüm geçeceği karar vermek için alt ağaçlarını kontrol etme işlemi yapılır.
- sağ alt ağaç ve sol alt ağaç boş olmadığını tespit edilir `yukarıdaki anlatıldığı işleyişin 4. maddesindeki 3. durumdur`.
- Bu durumda, sağ alt ağacın en küçük düğümü bulunur ve kök düğümün değeri bu düğümle değiştirilir. İşlemin ayrıntıları şu adımlarla gerçekleşir:
   * Silinecek düğüm bulunduktan sonra, bir sağ düğüme gidilir.
   * Ardından, en küçük düğüme ulaşana kadar sola gidilir.
   * En küçük düğüme ulaşıldığında, bu düğümün değeri, silinecek olan düğümün yerine geçecek şekilde değiştirilir. Örneğin, 13 değeri olan düğüm, 12 yerine geçecek şekilde atanır.
   * Değeri değiştirildikten sonra, artık 13 değeri olan düğüm, silme işlemine tabi tutulur ve ağaçtan çıkarılır.

    <div align="center">
    <h3>Binary Ağaç 12 değeri olan düğüm silme adımları</h3>
    </div>

    [![3. durumun adlımları](https://github.com/yasir723/node-ekle/assets/111686779/f0ac87bb-4281-4498-ac71-f5f635d491cc)](https://github.com/yasir723/node-ekle/assets/111686779/c83e59ba-f7a1-405f-ae03-dd16f93a748c
)


