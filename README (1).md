# Проект по автоматизации тестирования для компании [<img width="35%" title="Trello" src="media/logo/ttrello-log.png"/>](https://trello.com/)
> Trello — облачная программа для управления проектами небольших групп, разработанная Fog Creek Software. 
---

## Содержание:
+ [Описание проекта и используемый стек](#описание-проекта-и-используемый-стек)
+ [Реализованные проверки](#реализованные-проверки)
+ [Сборка в Jenkins](#-сборка-в-jenkins)
+ [Интеграция с Allure Report](#-интеграция-с-allure-report)
+ [Интеграция с Allure TestOps](#-интеграция-с-allure-testops)
+ [Видео примера запуска тестов в Selenoid](#-видео-примера-запуска-тестов-в-selenoid)
---

## Описание проекта и используемый стек
<p align="center">
<a href="https://www.jetbrains.com/idea/"><img title="IntelliJ IDEA" src="media/logo/Intelij_IDEA.svg" height="50" width="50"/></a> 
<a href="https://www.java.com/"><img title="Java" src="media/logo/Java.svg" height="50" width="50"/></a>
<a href="https://gradle.org/"><img title="Gradle" src="media/logo/Gradle.svg" height="50" width="50"/></a> 
<a href="https://selenide.org/"><img title="Selenide" src="media/logo/Selenide.svg" height="50" width="50"/></a> 
<a href="https://aerokube.com/selenoid/"><img title="Selenoid" src="media/logo/Selenoid.svg" height="50" width="50"/></a>
<a href="https://rest-assured.io"><img title="REST-Assured" src="media/logo/RestAssured.svg" height="50" width="50"/></a>
<a href="https://github.com/allure-framework/allure2"><img title="Allure Report" src="media/logo/Allure_Report.svg" height="50" width="50"/></a>
<a href="https://qameta.io"><img" title="Allure TestOps" src="media/logo/Allure_TO.svg" height="50" width="50"/></a>
<a href="https://junit.org/junit5/"><img title="JUnit5" src="media/logo/JUnit5.svg" height="50" width="50"/></a> 
<a href="https://github.com/"><img title="GitHub" src="media/logo/GitHub.svg" height="50" width="50"/></a> 
<a href="https://www.jenkins.io/"><img title="Jenkins" src="media/logo/Jenkins.svg" height="50" width="50"/></a>  
</p>   

- Проект состоит из UI-тестов и API тестов
- В данном проекте автотесты написаны на языке `Java`
- В качестве сборщика используется `Gradle`
- Используются фреймворки `JUnit 5` и `Selenide`
- Используется технология `Owner` для придания тестам гибкости и легкости конфигурации
- Используется `Lombok` для моделей в API тестах
- При прогоне UI тестов браузер запускается в `Selenoid`
- Реализована возможность запуска проектов с помощью `Jenkins`
- Реализована интеграция с `Allure TestOps`
- По завершению прохождения автотестов генерируется `Allure` отчет
---

## Реализованные проверки:

### Web
- [x] Проверка создания доски c типом видимости: рабочее пространство
- [x] Проверка редактирования названия доски c типом видимости: рабочее пространство
- [x] Проверка удаления доски c типом видимости: рабочее пространство
- [x] Проверка создания карточки на доске
- [x] Проверка редактирования карточки на доске
- [x] Проверка удаления карточки на доске
- [x] Проверка создания колонки на доске

### Api
- [x] Проверка редактирования доски через API
- [x] Проверка создания колонки через API
- [x] Проверка удаления колонки через API
- [x] Проверка создания карточки через API
- [x] Проверка удаления карточки через API

---

## <img height="35" width="35" style="vertical-align:middle" title="Jenkins" src="media/logo/Jenkins.svg"> Сборка в Jenkins

* <code>TASK</code> – название запускаемой задачи. По умолчанию - <code>main_web</code>.
* <code>BROWSER</code> – браузер, в котором будут выполняться тесты. По умолчанию - <code>chrome</code>.
* <code>BROWSER_VERSION</code> – версия браузера, в которой будут выполняться тесты. По умолчанию - <code>-</code>.
* <code>BROWSER_SIZE</code> – размер окна браузера, в котором будут выполняться тесты. По умолчанию - <code>1920x1080</code>.
* <code>Wdhost</code> – адрес Selenoid для удаленного запуска тестов.
* <code>apiKey</code> – ключ для доступа к Api.
* <code>token</code> – токен для доступа к Api.
* <code>login</code> – логин от учетной записи Trello.
* <code>password</code> – пароль от учетной записи Trello.
* <code>wdLogin</code> – логин от учетной записи Selenoid.
* <code>wdPassword</code> – пароль от учетной записи Selenoid.
  
***Параметры запуска для UI и Api:***
```
clean ${TEST_TASK}
-DBrowser=${BROWSER}
-DChromeVersion=${CHROME_VERSION}
-DFirefoxVersion=${FIREFOX_VERSION}
-DBrowserSize=${BROWSER_SIZE}
-DWdhost=${WDHOST}
-DapiKey=${apiKey}
-Dtoken=${token}
-Dlogin=${login}
-Dpassword=${password}
-DwdLogin=${wdLogin}
-DwdPassword=${wdPassword}
```

***Важно!***
```
Для запуска тестов данного проекта необходимо установить в настройках сборки apiKey и token от API Trello, login и password от существующего аккаунта Trello, а также wdLogin и wdPassword от учетной записи на сервере Selenoid.
```

Для запуска сборки необходимо перейти в раздел <code>Собрать с параметрами</code>, задать параметры и нажать кнопку <code>Собрать</code>.

<p align="center">
<img title="Jenkins" src="media/screenshots/JParameters.png">
</p>

***Важно!***
```
Для запуска тестов данного проекта необходимо установить в настройках сборки apiKey и token от API Trello, login и password от существующего аккаунта Trello, а также browserstackUsername и browserstackPassword от аккаунта BrowserStack.
```

После выполнения сборки, в блоке <code>История сборок</code> напротив номера сборки появится значок <code>Allure Report</code>, при клике на который открывается страница со сформированным html-отчетом,
а так же значок <code>Allure TestOps</code> при клике на который открывается страница проекта в <code>Allure TestOps</code>.

---
## <img height="35" width="35" style="vertical-align:middle" title="Allure_Report" src="media/logo/Allure_Report.svg"> Интеграция с Allure Report
`Allure Report` - инструмент для генерации и визуализации отчетов о выполнении тестов, который позволяет представлять результаты тестирования в наглядной и удобной форме.

### Диаграмма прохождения тестов

<p align="center">  
<img title="Allure Overview Dashboard" src="media/screenshots/AMain.png">  
</p>  

### Развернутый результат прохождения тестов

<p align="center">  
<img title="Allure Tests" src="media/screenshots/ATestCases.png">  
</p>

---
## <img height="35" width="35" style="vertical-align:middle" title="Allure_TestOps" src="media/logo/Allure_TO.svg"> Интеграция с Allure TestOps
`Allure TestOps` - платформа для управления тестированием, которая предоставляет обширный набор для организации, выполнения и анализа тестов в проектах.

<p align="center">  
<img title="Allure TestOps Dashboard" src="media/screenshots/TOTestCases.png">  
</p>

---
## <img height="35" width="35" style="vertical-align:middle" title="Selenoid" src="media/logo/Selenoid.svg"> Видео примера запуска тестов в Selenoid

В отчетах Allure для каждого теста прикреплен не только скриншот, но и видео прохождения теста.
<p align="center">
  <img title="Selenoid Video" src="media/screenshots/AVideo.gif">
</p>
