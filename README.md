# Termius-cracked

##Данное руководство демонстрирует способ модификации файлов приложения Termius для активации премиум-функций. Только для образовательных целей.
⚠️ Важное предупреждение

Это руководство предназначено исключительно для обучения и исследования.

    Изменение ПО может нарушать условия использования

    Рекомендуется поддерживать разработчиков, приобретая лицензии

    Используйте на свой страх и риск

    Никаких гарантий или поддержки не предоставляется

##🛠️ Требования

Установите Node.js, затем установите утилиту asar:
bash

npm install -g asar

##🖥️ Для пользователей Windows

Процесс аналогичен macOS. Следуйте инструкциям ниже, подставляя пути для вашей системы (обычно Program Files).
##🍎 Для пользователей macOS
1. Распаковка файлов приложения

```shell
cd /Applications/Termius.app/Contents/Resources/
asar extract app.asar ./app
mv app.asar app.asar.bak   # рекомендуется сделать бэкап
rm app-update.yml          # отключить автообновления

```
2. Изменение фонового процесса

Отредактируйте файл:
```
app/js/background-process.js
```
Найдите строку:
`await this.api.bulkAccount`

`const e=await this.api.bulkAccount();` -> `var e=await this.api.bulkAccount();`

```js
var e=await this.api.bulkAccount();
e.account.pro_mode=true;
e.account.need_to_update_subscription=false;
e.account.current_period={
    "from": "2022-01-01T00:00:00",
    "until": "2099-01-01T00:00:00"
};
e.account.plan_type="Premium";
e.account.user_type="Premium";
e.student=null;
e.trial=null;
e.account.authorized_features.show_trial_section=false;
e.account.authorized_features.show_subscription_section=true;
e.account.authorized_features.show_github_account_section=false;
e.account.expired_screen_type=null;
e.personal_subscription={
    "now": new Date().toISOString().slice(0, -5),
    "status": "SUCCESS",
    "platform": "stripe",
    "current_period": {
        "from": "2022-01-01T00:00:00",
        "until": "2099-01-01T00:00:00"
    },
    "revokable": true,
    "refunded": false,
    "cancelable": true,
    "reactivatable": false,
    "currency": "usd",
    "created_at": "2022-01-01T00:00:00",
    "updated_at": new Date().toISOString().slice(0, -5),
    "valid_until": "2099-01-01T00:00:00",
    "auto_renew": true,
    "price": 12.0,
    "verbose_plan_name": "Termius Pro Monthly",
    "plan_type": "SINGLE",
    "is_expired": false
};
e.access_objects=[{
    "period": {
        "start": "2022-01-01T00:00:00",
        "end": "2099-01-01T00:00:00"
    },
    "title": "Pro"
}]
return .......
```

Важно: сохраните структуру кода и return-выражение.
##3. Завершение настройки

    Запустите Termius

    Войдите в аккаунт

    Полностью перезапустите приложение

    Проверьте наличие премиум-функций

##🔧 Устранение неполадок
Проблема	Решение
Permission denied	Используйте sudo или проверьте права
asar not found	Проверьте установку: npm list -g asar
Изменения не применились	Перезагрузите компьютер и приложение
Синтаксические ошибки	Проверьте код на опечатки
📝 Примечания

    Обновления приложения перезапишут изменения

    Метод может перестать работать в будущих версиях

    Для стабильной работы рекомендуется официальная подписка

    Делайте бэкапы важных данных

##📜 Лицензия и отказ от ответственности

Данный материал предназначен только для образовательных целей. Автор не поддерживает пиратство. Пользователи несут ответственность за соблюдение законов и лицензий. Если Termius полезен для вас — поддержите разработчиков покупкой подписки.
🤝 Участие

Руководство предоставляется «как есть». Вопросы, связанные с процессом модификации, могут обсуждаться, но никаких гарантий работоспособности не даётся.
