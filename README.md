# Node Silme
**<span style="color:red">Bu satır kırmızı renkte.</span>**

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
    <img src="https://github.com/yasir723/node-ekle/assets/111686779/11d4aac8-b0d4-4762-b028-17d29fada8d1" width="600">
</div>

Yukarıdaki binary ağaçtan düğümler silme işlemi yapacağız
### `Soru 1: 4 değeri olan düğümü silme işlemi gerçekleştirin`
#### İşleyiş
- ilk olarak 4 değer 9 ile karışlaştırdı ve daha küçük oladuğu için sola gidilir.
- 4 değer bulana kadar arama işlemi devam etmiştir.
- 4 değer düğümü bulduğunda demek `node.value = value` şartını sağlamış ve silme işlemi gerçekleştirilir.
- silenecek düğümün yerine hangi düğüm geçeceği karar vermek için alt ağaçlarını kontrol etme işlemi yapılır.
- Silinecek düğümün yerine geçecek düğümü belirlemek için, alt ağaçlar kontrol edilir.
- sol alt ağaç boş olduğunu ve sağ alt ağaç boş olmadığını tespit edilir (yukarıdaki anlatıldığı işleyişin 4. maddesindeki ilk durumdur).
- bu durumda sağ alt düğümün silenecek düğümün yerine geçilir.
- sağ alt düğümün silenecek düğümün yerine geçtiğinde onun altındaki düğümleri koruyarak bağlı kalacak ve böylece ağaç yapısında herhangi bir kesilme olmayacaktır.

<div align="center">
    <h3>Binary Ağaç 4 değeri olan düğüm silindikten sonra</h3>
    <img src="https://github.com/yasir723/node-ekle/assets/111686779/a7b5d8d3-7fde-4d4d-818a-3689df53d17f" width="600">
</div>




