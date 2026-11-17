---
{"dg-publish":true,"permalink":"/api/otvetstvennye-licza-api/","dg-note-properties":{}}
---

# GET `/employees`

**Описание:** список сотрудников склада — операторов или менеджеров (справочник `Сотрудники`).

**Запрос:**  
`GET /trade/hs/stock/employees?...`

**Авторизация:** заголовок `X-Api-Key`.

## Параметры

| параметр | описание | обязательный |
|----------|----------|--------------|
| `position` | роль: `operator` или `manager` (без учёта регистра) | да |
| `warehouseCode` | код склада | для `operator`: да, если нет `warehouse` |
| `warehouse` | наименование склада | для `operator`: да, если нет `warehouseCode` |
| `search` | отбор операторов по вхождению в наименование или по коду | нет, только для `operator` |

Для `position=manager` склад и `search` **не используются**.

Некорректный или отсутствующий `position` → **400**. Склад не найден / нет доступа (`operator`) → **404**.

---

## `position=operator`

Операторы выбранного склада: сотрудники из ТЧ «Склады» справочника `Сотрудники`, склад которых разрешён учётной записи. Не помечены на удаление; дата увольнения пустая или не раньше текущей даты.

```
GET /employees?position=operator&warehouseCode=2
GET /employees?position=operator&warehouse=Склад резерва&search=Полуэктов
```

**Ответ 200**

```json
{
    "warehouse": "Склад резерва",
    "warehouseCode": "2",
    "employees": [
        {
            "employee": "Полуэктов В.",
            "employeeCode": "11",
            "pin": "1234"
        },
        {
            "employee": "James Johnes",
            "employeeCode": "32",
            "pin": "5678"
        }
    ]
}
```

---

## `position=manager`

Сотрудники с `Менеджер = Истина`, без пометки удаления, с **пустой** датой увольнения. Отбор по складу не применяется.

```
GET /employees?position=manager
```

**Ответ 200** — без `warehouse` / `warehouseCode`:

```json
{
    "employees": [
        {
            "employee": "Продавайкин И.И.",
            "employeeCode": "5",
            "pin": ""
        }
    ]
}
```

Элемент `employees[]` тот же, что у операторов: `employee`, `employeeCode`, `pin`.
