---
title: Sınıflar, Yapılar ve Birleşimleri Hazırlama
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- data marshaling, classes
- marshaling, unions
- marshaling, structures
- marshaling, samples
- data marshaling, structures
- platform invoke, marshaling data
- marshaling, classes
- data marshaling, unions
- data marshaling, samples
- data marshaling, platform invoke
- marshaling, platform invoke
ms.assetid: 027832a2-9b43-4fd9-9b45-7f4196261a4e
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: a53c8b7b88bd25a6611c33218c7a386de55889e9
ms.sourcegitcommit: 3ac05b2c386c8cc5e73f4c7665f6c0a7ed3da1bd
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/20/2019
ms.locfileid: "71151760"
---
# <a name="marshaling-classes-structures-and-unions"></a>Sınıflar, Yapılar ve Birleşimleri Hazırlama
Sınıflar ve yapılar .NET Framework benzerdir. Her ikisinde de alanlar, Özellikler ve olaylar olabilir. Statik ve statik olmayan yöntemlere de sahip olabilirler. Bir önemli farkı, yapıların değer türleri ve sınıfların başvuru türleridir.  
  
 Aşağıdaki tablo sınıflar, yapılar ve birleşimler için sıralama seçeneklerini listeler; kullanımlarını açıklar; ve buna karşılık gelen platform çağırma örneğine bir bağlantı sağlar.  
  
|Tür|Açıklama|Örnek|  
|----------|-----------------|------------|  
|Değere göre sınıf.|Tamsayı üyeleri olan bir sınıfı, yönetilen durum gibi bir ın/out parametresi olarak geçirir.|SysTime örneği|  
|Değere göre yapı.|Yapıları parametrelerde olduğu gibi geçirir.|Yapılar örneği|  
|Başvuruya göre yapı.|Yapıları ın/out parametreleri olarak geçirir.|OSInfo örneği|  
|İç içe yapılar (düzleştirilmiş) ile yapı.|Yönetilmeyen işlevde iç içe yapılar içeren bir yapıyı temsil eden bir sınıf geçirir. Yapı, yönetilen prototipde bir büyük yapıya düzleştirilir.|FindFile örneği|  
|Başka bir yapıya işaretçi içeren yapı.|İkinci bir yapıya bir işaretçi içeren bir yapıyı üye olarak geçirir.|Yapılar Örneği|  
|Değere göre tamsayılar içeren yapıların dizisi.|Yalnızca tamsayı içeren bir yapı dizisini bir ın/out parametresi olarak geçirir. Dizi üyeleri değiştirilebilir.|Diziler Örneği|  
|Başvuruya göre tamsayılar ve dizeler içeren yapıların dizisi.|Out parametresi olarak tamsayılar ve dizeler içeren bir yapı dizisini geçirir. Çağrılan işlev dizi için bellek ayırır.|OutArrayOfStructs Örneği|  
|Değer türleri olan birleşimler.|Birleşimleri değer türleriyle geçirir (tamsayı ve çift).|Birleşimler örneği|  
|Karışık Türler içeren birleşimler.|Birleşimleri karışık türler (tamsayı ve dize) ile geçirir.|Birleşimler örneği|  
|Yapıda null değerler.|Değer türüne başvuru yerine bir null başvurusu (Visual Basic**hiçbir şey** ) geçirir.|HandleRef örneği|  
  
## <a name="structures-sample"></a>Yapılar örneği  
 Bu örnek, ikinci yapıya işaret eden bir yapının nasıl geçirileceğini, gömülü bir yapıya sahip bir yapının nasıl geçirileceğini ve bir yapının gömülü dizi ile nasıl geçirileceğini gösterir.  
  
 Yapılar örneği, özgün işlev bildirimiyle gösterilen aşağıdaki yönetilmeyen işlevleri kullanır:  
  
- **Teststructsöylemek** , PInvokeLib. dll dosyasından verildi.  
  
    ```cpp  
    int TestStructInStruct(MYPERSON2* pPerson2);  
    ```  
  
- **TestStructInStruct3** , PInvokeLib. dll dosyasından verildi.  
  
    ```cpp  
    void TestStructInStruct3(MYPERSON3 person3);  
    ```  
  
- **Testarraybildirmek** , PInvokeLib. dll dosyasından verildi.  
  
    ```cpp  
    void TestArrayInStruct( MYARRAYSTRUCT* pStruct );  
    ```  
  
 [PInvokeLib. dll](marshaling-data-with-platform-invoke.md#pinvokelibdll) , önceden listelenmiş işlevlere ve dört yapıya yönelik uygulamalar içeren özel bir yönetilmeyen kitaplıktır: **MyPerson**, **MyPerson2**, **MyPerson3**ve **MyArrayStruct**. Bu yapılar aşağıdaki öğeleri içerir:  
  
```cpp  
typedef struct _MYPERSON  
{  
   char* first;   
   char* last;   
} MYPERSON, *LP_MYPERSON;  
  
typedef struct _MYPERSON2  
{  
   MYPERSON* person;  
   int age;   
} MYPERSON2, *LP_MYPERSON2;  
  
typedef struct _MYPERSON3  
{  
   MYPERSON person;  
   int age;   
} MYPERSON3;  
  
typedef struct _MYARRAYSTRUCT  
{  
   bool flag;  
   int vals[ 3 ];   
} MYARRAYSTRUCT;  
```  
  
 Yönetilen `MyPerson`, `MyPerson2`, `MyPerson3`ve yapılarıaşağıdakiözellikleresahiptir:`MyArrayStruct`  
  
- `MyPerson`yalnızca dize üyelerini içerir. [Karakter kümesi](specifying-a-character-set.md) alanı yönetilmeyen işleve GEÇIRILDIĞINDE dizeleri ANSI biçimine ayarlar.  
  
- `MyPerson2``MyPerson` yapıya bir **IntPtr** içerir. .NET Framework uygulamalar, kod **güvensiz**olarak işaretlenmedikçe işaretçileri kullanmadığı Için, **IntPtr** türü özgün işaretçinin yönetilmeyen yapıya göre yerini alır.  
  
- `MyPerson3`gömülü `MyPerson` yapı olarak içerir. Başka bir yapıda gömülü bir yapı, gömülü yapının öğeleri doğrudan ana yapıya girilerek düzleştirilir veya bu örnekte yapıldığı gibi gömülü bir yapı olarak bırakılabilir.  
  
- `MyArrayStruct`bir tamsayılar dizisi içerir. Özniteliği, <xref:System.Runtime.InteropServices.UnmanagedType> numaralandırma değerini dizideki öğelerin sayısını göstermek için kullanılan ByValArray olarak ayarlar. <xref:System.Runtime.InteropServices.MarshalAsAttribute>  
  
 Bu örnekteki tüm yapılar için, <xref:System.Runtime.InteropServices.StructLayoutAttribute> üyelerin bellekte sırayla, göründükleri sırada düzenlendiğinden emin olmak için özniteliği uygulanır.  
  
 Sınıfı,`TestStructInStruct` ,ve`App`sınıfıtarafından çağrılan yöntemler için yönetilen prototürler içerir. `TestArrayInStruct` `TestStructInStruct3` `NativeMethods` Her prototip, aşağıdaki gibi tek bir parametre bildirir:  
  
- `TestStructInStruct`parametresi olarak yazmak `MyPerson2` için bir başvuru bildirir.  
  
- `TestStructInStruct3`türü `MyPerson3` parametresi olarak bildirir ve parametreyi değere göre geçirir.  
  
- `TestArrayInStruct`parametresi olarak yazmak `MyArrayStruct` için bir başvuru bildirir.  
  
 Parametreler **ref** (Visual Basic içinde**ByRef** ) anahtar sözcüğü içermiyorsa, yöntemlere bağımsız değişken olarak geçirilen yapılar değere göre geçirilir. Örneğin, `TestStructInStruct` yöntemi bir başvurusu (bir adresin değeri) türünde `MyPerson2` bir nesneye, yönetilmeyen koda geçirir. ' A işaret eden `MyPerson2` yapıyı değiştirmek için örnek, belirtilen boyutun bir arabelleğini oluşturur ve <xref:System.Runtime.InteropServices.Marshal.AllocCoTaskMem%2A?displayProperty=nameWithType> ve <xref:System.Runtime.InteropServices.Marshal.SizeOf%2A?displayProperty=nameWithType> yöntemlerini birleştirerek adresini döndürür. Ardından örnek, yönetilen yapının içeriğini yönetilmeyen arabelleğe kopyalar. Son olarak, örnek, yönetilmeyen <xref:System.Runtime.InteropServices.Marshal.PtrToStructure%2A?displayProperty=nameWithType> arabellekteki verileri yönetilen bir nesneye <xref:System.Runtime.InteropServices.Marshal.FreeCoTaskMem%2A?displayProperty=nameWithType> ve yönetilmeyen bellek bloğunu serbest bırakma yöntemine göre sıralamak için yöntemini kullanır.  
  
### <a name="declaring-prototypes"></a>Prototipleri Bildirme  
 [!code-cpp[Conceptual.Interop.Marshaling#23](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.interop.marshaling/cpp/structures.cpp#23)]
 [!code-csharp[Conceptual.Interop.Marshaling#23](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.interop.marshaling/cs/structures.cs#23)]
 [!code-vb[Conceptual.Interop.Marshaling#23](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.interop.marshaling/vb/structures.vb#23)]  
  
### <a name="calling-functions"></a>İşlevleri Çağırma  
 [!code-cpp[Conceptual.Interop.Marshaling#24](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.interop.marshaling/cpp/structures.cpp#24)]
 [!code-csharp[Conceptual.Interop.Marshaling#24](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.interop.marshaling/cs/structures.cs#24)]
 [!code-vb[Conceptual.Interop.Marshaling#24](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.interop.marshaling/vb/structures.vb#24)]  
  
## <a name="findfile-sample"></a>FindFile örneği  
 Bu örnek, yönetilmeyen bir işleve ikinci, gömülü bir yapı içeren bir yapının nasıl geçirileceğini gösterir. Ayrıca, yapı içinde sabit uzunluklu bir <xref:System.Runtime.InteropServices.MarshalAsAttribute> dizi bildirmek için özniteliği nasıl kullanacağınızı gösterir. Bu örnekte, katıştırılmış yapı öğeleri üst yapıya eklenir. Düzleştirilmemiş gömülü bir yapının örneği için bkz. [yapılar örneği](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/eadtsekz(v=vs.100)).  
  
 FindFile örneği, özgün işlev bildirimiyle gösterilen aşağıdaki yönetilmeyen işlevi kullanır:  
  
- Kernel32. dll dosyasından bir **FindFirstFile** verildi.  
  
    ```cpp
    HANDLE FindFirstFile(LPCTSTR lpFileName, LPWIN32_FIND_DATA lpFindFileData);  
    ```  
  
 İşleve geçirilen özgün yapı aşağıdaki öğeleri içerir:  
  
```cpp
typedef struct _WIN32_FIND_DATA   
{  
  DWORD    dwFileAttributes;   
  FILETIME ftCreationTime;   
  FILETIME ftLastAccessTime;   
  FILETIME ftLastWriteTime;   
  DWORD    nFileSizeHigh;   
  DWORD    nFileSizeLow;   
  DWORD    dwReserved0;   
  DWORD    dwReserved1;   
  TCHAR    cFileName[ MAX_PATH ];   
  TCHAR    cAlternateFileName[ 14 ];   
} WIN32_FIND_DATA, *PWIN32_FIND_DATA;  
```  
  
 Bu örnekte, `FindData` sınıfı özgün yapıdaki her öğe için karşılık gelen bir veri üyesini ve katıştırılmış yapıyı içerir. İki orijinal karakter arabelleği yerine, sınıf yerine dizeler koyar. **MarshalAsAttribute** <xref:System.Runtime.InteropServices.UnmanagedType> numaralandırmayı, yönetilmeyen yapılar içinde görünen satır içi, sabit uzunlukta karakter dizilerini belirlemek için kullanılan **ByValTStr**olarak ayarlar.  
  
 Sınıfı, `FindData` sınıfının bir parametre olarak geçişini sağlayan `FindFirstFile` , yönetilen bir prototipi içerir. `NativeMethods` Parametre, <xref:System.Runtime.InteropServices.InAttribute> ve <xref:System.Runtime.InteropServices.OutAttribute> öznitelikleri ile bildirilmelidir çünkü başvuru türleri olan sınıflar varsayılan olarak parametrelerde olarak geçirilir.  
  
### <a name="declaring-prototypes"></a>Prototipleri Bildirme  
 [!code-cpp[Conceptual.Interop.Marshaling#17](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.interop.marshaling/cpp/findfile.cpp#17)]
 [!code-csharp[Conceptual.Interop.Marshaling#17](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.interop.marshaling/cs/findfile.cs#17)]
 [!code-vb[Conceptual.Interop.Marshaling#17](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.interop.marshaling/vb/findfile.vb#17)]  
  
### <a name="calling-functions"></a>İşlevleri Çağırma  
 [!code-cpp[Conceptual.Interop.Marshaling#18](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.interop.marshaling/cpp/findfile.cpp#18)]
 [!code-csharp[Conceptual.Interop.Marshaling#18](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.interop.marshaling/cs/findfile.cs#18)]
 [!code-vb[Conceptual.Interop.Marshaling#18](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.interop.marshaling/vb/findfile.vb#18)]  
  
## <a name="unions-sample"></a>Birleşimler örneği  
 Bu örnek, yalnızca değer türlerini içeren yapıların ve bir değer türü içeren yapıların ve bir birleşim bekleyen yönetilmeyen bir işleve parametre olarak dize olarak nasıl geçirileceğini gösterir. Birleşim, iki veya daha fazla değişken tarafından paylaşılabilen bir bellek konumunu temsil eder.  
  
 Birleşimler örneği, özgün işlev bildirimiyle gösterilen aşağıdaki yönetilmeyen işlevi kullanır:  
  
- **TestUnion** , PInvokeLib. dll dosyasından verildi.  
  
    ```cpp
    void TestUnion(MYUNION u, int type);  
    ```  
  
 [PInvokeLib. dll](marshaling-data-with-platform-invoke.md#pinvokelibdll) , önceden listelenmiş işlev için bir uygulama ve **MyUnion** ve **MYUNION2**olmak üzere iki birleşim içeren özel bir yönetilmeyen kitaplıktır. Birleşimler aşağıdaki öğeleri içerir:  
  
```cpp
union MYUNION  
{  
    int number;  
    double d;  
}  
  
union MYUNION2  
{  
    int i;  
    char str[128];  
};  
```  
  
 Yönetilen kodda birleşimler yapılar olarak tanımlanır. Yapı `MyUnion` , üyeleri olarak iki değer türü içerir: tamsayı ve çift. <xref:System.Runtime.InteropServices.StructLayoutAttribute> Özniteliği her bir veri üyesinin kesin konumunu denetlemek üzere ayarlanır. <xref:System.Runtime.InteropServices.FieldOffsetAttribute> Özniteliği, bir birleşimin yönetilmeyen gösterimi içindeki alanların fiziksel konumunu sağlar. Her iki üyenin de aynı fark değerlerine sahip olduğuna dikkat edin, bu nedenle Üyeler aynı bellek parçasını tanımlayabilirler.  
  
 `MyUnion2_1`ve `MyUnion2_2` sırasıyla bir değer türü (tamsayı) ve bir dize içerir. Yönetilen kodda, değer türleri ve başvuru türlerinin örtüşmesine izin verilmez. Bu örnek, çağıranın aynı yönetilmeyen işlevi çağırırken her iki türü de kullanmasını sağlamak için yöntem aşırı yüklemesini kullanır. Düzeni `MyUnion2_1` açıktır ve kesin bir fark değeri içerir. Buna karşılık, `MyUnion2_2` başvuru türlerinde açık mizanpajlara izin verilmediğinden sıralı bir düzene sahiptir. Özniteliği, UNION 'nin <xref:System.Runtime.InteropServices.UnmanagedType> yönetilmeyen gösterimi içinde görünen satır içi, sabit uzunlukta karakter dizilerini belirlemek için kullanılan ByValTStr olarak ayarlanır. <xref:System.Runtime.InteropServices.MarshalAsAttribute>  
  
 `NativeMethods` `TestUnion` Sınıfı ve`TestUnion2` yöntemlerinin prototiplerini içerir. `TestUnion2`, parametreleri bildirmek `MyUnion2_1` `MyUnion2_2` için aşırı yüklendi.  
  
### <a name="declaring-prototypes"></a>Prototipleri Bildirme  
 [!code-cpp[Conceptual.Interop.Marshaling#28](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.interop.marshaling/cpp/unions.cpp#28)]
 [!code-csharp[Conceptual.Interop.Marshaling#28](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.interop.marshaling/cs/unions.cs#28)]
 [!code-vb[Conceptual.Interop.Marshaling#28](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.interop.marshaling/vb/unions.vb#28)]  
  
### <a name="calling-functions"></a>İşlevleri Çağırma  
 [!code-cpp[Conceptual.Interop.Marshaling#29](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.interop.marshaling/cpp/unions.cpp#29)]
 [!code-csharp[Conceptual.Interop.Marshaling#29](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.interop.marshaling/cs/unions.cs#29)]
 [!code-vb[Conceptual.Interop.Marshaling#29](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.interop.marshaling/vb/unions.vb#29)]  
  
## <a name="systime-sample"></a>SysTime örneği  
 Bu örnek, bir sınıfa işaretçi bekleyen yönetilmeyen bir işleve bir işaretçinin nasıl geçirileceğini gösterir.  
  
 SysTime örneği, özgün işlev bildirimiyle gösterilen aşağıdaki yönetilmeyen işlevi kullanır:  
  
- Kernel32. dll ' den bir **GetSystemTime** verildi.  
  
    ```cpp
    VOID GetSystemTime(LPSYSTEMTIME lpSystemTime);  
    ```  
  
 İşleve geçirilen özgün yapı aşağıdaki öğeleri içerir:  
  
```cpp
typedef struct _SYSTEMTIME {   
    WORD wYear;   
    WORD wMonth;   
    WORD wDayOfWeek;   
    WORD wDay;   
    WORD wHour;   
    WORD wMinute;   
    WORD wSecond;   
    WORD wMilliseconds;   
} SYSTEMTIME, *PSYSTEMTIME;  
```  
  
 Bu örnekte, `SystemTime` sınıfı sınıf üyeleri olarak temsil edilen orijinal yapının öğelerini içerir. <xref:System.Runtime.InteropServices.StructLayoutAttribute> Özniteliği, üyelerin bellekte sırayla, göründükleri sırada düzenlendiğinden emin olmak üzere ayarlanır.  
  
 Sınıfı, varsayılan olarak `SystemTime` sınıfı bir ın/ `GetSystemTime` out parametresi olarak ileten yönteminin yönetilen bir prototipini içerir. `NativeMethods` Parametre, <xref:System.Runtime.InteropServices.InAttribute> ve <xref:System.Runtime.InteropServices.OutAttribute> öznitelikleri ile bildirilmelidir çünkü başvuru türleri olan sınıflar varsayılan olarak parametrelerde olarak geçirilir. Çağıranın sonuçları alması için, bu [yönlü özniteliklerin](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/77e6taeh(v=vs.100)) açıkça uygulanması gerekir. Sınıfı, `SystemTime` sınıfının yeni bir örneğini oluşturur ve veri alanlarına erişir. `App`  
  
### <a name="code-samples"></a>Kod Örnekleri  
 [!code-cpp[Conceptual.Interop.Marshaling#25](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.interop.marshaling/cpp/systime.cpp#25)]
 [!code-csharp[Conceptual.Interop.Marshaling#25](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.interop.marshaling/cs/systime.cs#25)]
 [!code-vb[Conceptual.Interop.Marshaling#25](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.interop.marshaling/vb/systime.vb#25)]  
  
## <a name="outarrayofstructs-sample"></a>OutArrayOfStructs örneği  
 Bu örnek, yönetilmeyen bir işleve tamsayı ve dizeler içeren bir yapı dizisinin nasıl geçirileceğini gösterir.  
  
 Bu örnek, <xref:System.Runtime.InteropServices.Marshal> sınıfını kullanarak ve güvenli olmayan kod kullanarak yerel bir işlevin nasıl çağrılacağını gösterir.  
  
 Bu örnek, bir sarmalayıcı işlevleri ve kaynak dosyalarında da sağlanmış olan [PInvokeLib. dll](marshaling-data-with-platform-invoke.md#pinvokelibdll)içinde tanımlanan platform çağırır kullanır. `TestOutArrayOfStructs` İşlevi`MYSTRSTRUCT2` ve yapısını kullanır. Yapı aşağıdaki öğeleri içerir:  
  
```cpp
typedef struct _MYSTRSTRUCT2  
{  
   char* buffer;  
   UINT size;   
} MYSTRSTRUCT2;  
```  
  
 Sınıf `MyStruct` , ANSI karakterlerinden oluşan bir dize nesnesi içerir. <xref:System.Runtime.InteropServices.DllImportAttribute.CharSet> Alan ANSI biçimini belirtir. `MyUnsafeStruct`, bir dize yerine <xref:System.IntPtr> tür içeren bir yapıdır.  
  
 Sınıfı, aşırı yüklenmiş `TestOutArrayOfStructs` prototip metodunu içerir. `NativeMethods` Bir yöntem parametre olarak bir işaretçi bildirirse, sınıf `unsafe` anahtar sözcüğüyle işaretlenmelidir. Visual Basic güvenli olmayan kod kullanamadığından, aşırı yüklenmiş yöntem, güvensiz değiştirici ve `MyUnsafeStruct` yapı gereksizdir.  
  
 Sınıfı, diziyi iletmek `UsingMarshaling` için gereken tüm görevleri gerçekleştiren yöntemini uygular. `App` Dizi `out` (`ByRef` Visual Basic) anahtar sözcüğüyle işaretlenir ve bu, verilerin çağrıdan çağırana 'e geçtiği anlamına gelir. Uygulama aşağıdaki <xref:System.Runtime.InteropServices.Marshal> sınıf yöntemlerini kullanır:  
  
- <xref:System.Runtime.InteropServices.Marshal.PtrToStructure%2A>yönetilmeyen arabellekteki verileri yönetilen bir nesneye sıralama.  
  
- <xref:System.Runtime.InteropServices.Marshal.DestroyStructure%2A>yapıdaki dizeler için ayrılan belleği serbest bırakmak için.  
  
- <xref:System.Runtime.InteropServices.Marshal.FreeCoTaskMem%2A>dizi için ayrılan belleği serbest bırakmak için.  
  
 Daha önce belirtildiği gibi C# , güvenli olmayan koda izin verir ve Visual Basic. C# Örnekte, `UsingUnsafePointer` `MyUnsafeStruct` yapıyı içeren diziyi geri geçirmek için <xref:System.Runtime.InteropServices.Marshal> sınıfı yerine işaretçiler kullanan alternatif bir yöntem uygulamasıdır.  
  
### <a name="declaring-prototypes"></a>Prototipleri Bildirme  
 [!code-cpp[Conceptual.Interop.Marshaling#20](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.interop.marshaling/cpp/outarrayofstructs.cpp#20)]
 [!code-csharp[Conceptual.Interop.Marshaling#20](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.interop.marshaling/cs/outarrayofstructs.cs#20)]
 [!code-vb[Conceptual.Interop.Marshaling#20](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.interop.marshaling/vb/outarrayofstructs.vb#20)]  
  
### <a name="calling-functions"></a>İşlevleri Çağırma  
 [!code-cpp[Conceptual.Interop.Marshaling#21](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.interop.marshaling/cpp/outarrayofstructs.cpp#21)]
 [!code-csharp[Conceptual.Interop.Marshaling#21](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.interop.marshaling/cs/outarrayofstructs.cs#21)]
 [!code-vb[Conceptual.Interop.Marshaling#21](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.interop.marshaling/vb/outarrayofstructs.vb#21)]  
  
## <a name="see-also"></a>Ayrıca bkz.

- [Platform Çağırma ile Veri Hazırlama](marshaling-data-with-platform-invoke.md)
- [Dizeleri Hazırlama](marshaling-strings.md)
- [Farklı Dizi Türlerini Hazırlama](marshaling-different-types-of-arrays.md)
