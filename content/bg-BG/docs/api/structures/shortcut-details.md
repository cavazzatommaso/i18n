# Обект ShortcutDetails

* `target` String - Целта, която трябва да се стартира от този пряк път.
* `cwd` String (по избор) - Работещата директория. Стойността на тази променлива по подразбиране е празна.
* `args` String (по избор) - Аргументите, които трябва да бъдат приложени към `target`, когато се стартира от този пряк път. Стойността на тази променлива по подразбиране е празна.
* `description` String (по избор) - Описанието на този пряк път. Стойността на тази променлива по подразбиране е празна.
* `icon` String (по избор) - Пътят до иконата. Може да е DLL или EXE. `icon` и `iconIndex` трябва да бъдат зададени заедно. Стойността на тази променлива по подразбиране е празна, което кара системата да използва иконата на целта/target.
* `iconIndex` Number (по избор) - Уникалният идентификатор на ресурса на иконата, когато `icon` е DLL или EXE. Стойността на тази променлива по подразбиране е 0.
* `appUserModelId` String (по избор) - Уникалният идентификатор над потребителския модел на приложението (Application User Model ID). Стойността на тази променлива по подразбиране е празна.