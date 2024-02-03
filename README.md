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

4. Eğer aranan değer, kök düğümün değerine eşitse, bu durumda silme işlemi gerçekleştirilir:
a. Eğer sol alt ağaç boşsa, sağ alt ağacı geri döner.
b. Eğer sağ alt ağaç boşsa, sol alt ağacı geri döner.
c. Eğer her iki alt ağaç da doluysa, sağ alt ağacın en küçük düğümü bulunur ve kök düğümün değeri bu düğümle değiştirilir. Ardından, sağ alt ağaç üzerinde tekrar nodeSil metodu çağrılır.

5. Her adımda güncellenmiş ağaç yapısı, son olarak kök düğümü geri döndürülür.


