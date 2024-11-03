# AWZ: Заполнение данных по УНП (awz.autounp)

### [Установка модуля](https://github.com/zahalski/awz.autounp/tree/main/docs/install.md)

<!-- desc-start -->

## Описание
Модуль для заполнения названия компании и юридического адреса по данным из МНС Республики Беларусь.

**Поддерживаемые редакции CMS Битрикс:**<br>
«Старт», «Стандарт», «Малый бизнес», «Бизнес», «Корпоративный портал», «Энтерпрайз», «Интернет-магазин + CRM»

<!-- desc-end -->

## Документация
<!-- dev-start -->

**\Awz\AutoUnp\Helper::getInfo**    
Получение информации о компании по УНП

| Параметр    | Описание |
|-------------|----------|
| `unp` `int` | УНП организации     

возвращает объект `\Bitrix\Main\Result` с результатом запроса

```php
use Bitrix\Main\Loader;
if(Loader::includeModule('awz.autounp')){
    $dataOb = \Awz\AutoUnp\Helper::getInfo(192042385);
    if($dataOb->isSuccess()){
        print_r($dataOb->getData());
        /*
         *[
         *  [row] => [
         *    [vunp] => 192042385
         *    [vnaimp] => Иностранное информационно-технологическое унитарное предприятие "1С-Битрикс"
         *    [vnaimk] => Иностранное унитарное предприятие "1С-Битрикс"
         *    [vpadres] => Беларусь, г. Минск, ПР. ПОБЕДИТЕЛЕЙ, дом 110, пом. 110-5, офис 5-1
         *    [dreg] => 2013-09-06
         *    [nmns] => 111
         *    [vmns] => Инспекция МНС по Центральному району г. Минска
         *    [ckodsost] => 1
         *    [vkods] => Действующий
         *    [dlikv] => 
         *    [vlikv] => 
         *  ]
         *]
         * */
    }
}
```

### Динамическое обновление контента (мимо BX.ajax)

** подстановка события onkeyup

```js
if(typeof(AwzAutoUnp_ob)!='undefined'){
    AwzAutoUnp_ob.findDom();
}
```

** пример изменения логики и обработки ошибок

```js
const controller_url = '/bitrix/services/main/ajax.php?action=awz%3Aautounp.api.mnsrb.find';
BX.addCustomEvent('onAjaxSuccess',function(data, param){
    let error = false;
    try{
        if(param.url === controller_url){
            if(data.status != 'success') {
                error = true
            }else{
                if(!data.data.mns) error = true
            }
        }
    }catch (e) {
        error = true;
    }
    if(error){
        alert('Ошибка получения данных по УНП');
    }
});

```

<!-- dev-end -->


<!-- cl-start -->
## История версий

https://github.com/zahalski/awz.autounp/blob/master/CHANGELOG.md

<!-- cl-end -->
