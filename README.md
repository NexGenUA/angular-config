### Установить необходимые пакеты

```javascript
$ npm i stylelint stylelint-config-airbnb stylelint-scss stylelint-order -D
$ npm i husky lint-staged -D
$ npm i prettier tslint-config-prettier tslint-plugin-prettier stylelint-config-prettier stylelint-prettier -D
```

### Создать файл

`.stylelintrc`

- Поместить в него следующий код

```javascript
{
  "plugins": [
    "stylelint-scss"
  ],
  "extends": ["stylelint-config-airbnb", "stylelint-prettier/recommended"],
  "rules": {}
}
```

Добавить в `package.json` 2 команды в поле `scripts`


```javascript
{
  "scripts": {
  ...
  "lint-css": "stylelint src/**/*.scss",
  "prettier": "prettier --write **/src/**/*.{js,ts,scss}"
}
```

Отредактировать файл `tslint.json`, изменить содержимое поля `"extends"` и в поле `"rules"` добавить строку `"prettier": true`


```javascript
{
  "extends": [
   "tslint-config-prettier",
   "tslint-plugin-prettier",
   "codelyzer"
  ],
  "rules": {
   "prettier": true
    ...
  }
}
```

**Для проверки конфликтов prettier и tslint запустить следующую команду**

```javascript
$ npx tslint-config-prettier-check ./tslint.json
```

- Удалить конфликтующие правила из файла `tslint.json` теперь их будет контроллировать `prettier`

**Проверяем правильность подключения правил `stylelint`**

```javascript
$ npx stylelint-config-prettier-check
```

### Создаем файл

`.huskyrc`

- Поместить в него следующий код

```javascript
{
  "hooks": {
     "pre-commit": "lint-staged && npm run lint"
  }
}
```

### Создаем файл

`.lintstagedrc`

- Поместить в него следующий код

```javascript
{
  "*.{ts,js,scss}": [
    "npm run prettier"
  ],
  "*.scss": [
    "npm run lint-css"
  ]
}
```

Запустить один раз команду, что бы привести к одному кодстайлу все файлы, которые еще не изменялись

```javascript
$ npm run prettier
```

Попробовать сделать коммит, должна запуститься проверка, если проверка пройдена - коммит добавляется

```javascript
$ git add .
$ git commit -m "feat: add prettier and bringing to a single style"
```

Так же можно настроить свой IDE, что бы он подсвечивал ошибки во время написания кода, тем самым экономя время на исправление ошибок

Готовые файлы `.stylelintrc` `.huskyrc` `.lintstagedrc` и отредактированный `tslint.json` можно скачать из дирректории [files](https://github.com/NexGenUA/angular-config/tree/master/files)
