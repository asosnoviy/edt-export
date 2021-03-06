# edt-export
Экспорт диагностик 1С: EDT для SonarQube 1C (BSL) Community Plugin.

Покажет проверки от 1С: EDT в Сонаре.

## Что это?

Это приложение, которое возьмет результаты валидации проекта от 1С: EDT и сконвертирует их в файл json, который умеет читать Sonar.

## Вам потребуется

1. [1С: EDT](https://releases.1c.ru/project/DevelopmentTools10)
2. [Oscript](http://oscript.io/)
3. [Sonar](https://www.sonarqube.org/downloads/)
4. BSL Language Server https://github.com/1c-syntax/bsl-language-server
5. Плагин для SonarQube https://github.com/1c-syntax/sonar-bsl-plugin-community
6. Sonar Scanner https://docs.sonarqube.org/display/SCAN/Analyzing+with+SonarQube+Scanner

## Установка

1. Скачайте *.ospx файл из релизов
2. Выполните команду `opm install -f путь/к/ospx/файлу`

## Получение отчета о проверке от EDT

[Пример батника](test/export-edt.bat)

## Получение джсон файла для сонара по отчету о проверке EDT

`edt-export-bugs c ./edt-result.out ./edt-json.json ./src`

`c` или `convert` - команда конвертации  
`EDT_VALIDATION_RESULT` - Путь к файлу с результатом проверки edt. Например ./edt-result.out  
`EDT_VALIDATION_JSON` - Путь к файлу результату. Например ./edt-json.json. Его нужно указать в `sonar-project.properties`.  
`SRC` - Путь к каталогу с исходниками. Например ./src. Лучше указывать относительный путь. Абсолютный путь сонар может и не воспринять.  

Аргументы можно так же задать через одноименные параметры окружения.

## Пример настроек проекта Сонара

```
sonar.host.url=http://localhost:9000
sonar.projectKey=UNF
sonar.projectVersion=1.16
sonar.sources=src
sonar.sourceEncoding=UTF-8
sonar.inclusions=**/*.bsl
sonar.bsl.languageserver.reportPaths=bsl-json.json
sonar.externalIssuesReportPaths=edt-json.json
```
