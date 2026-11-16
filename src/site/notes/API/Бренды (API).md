---
{"dg-publish":true,"permalink":"/api/brendy-api/","dg-note-properties":{}}
---

# GET `/api/v1/brands`

**Описание:** метод возвращает брэнды товаров (группы верхнего уровня справочника 1С [[Справочники (НСИ)/Номенклатура\|Номенклатура]]).
![Pasted image 20261116114104.png](/img/user/Assets/Pasted%20image%2020261116114104.png)

**Запрос**
    GET /trade/hs/stock/brands
    
**Параметры:** нет

**Ответ 200**
```json
[
    {
        "code": "15497",
        "brand": "Acer"
    },
    {
        "code": "13318",
        "brand": "AGM"
    },
    {
        "code": "22839",
        "brand": "AIBI"
    }
]
```