# Интервью на позицию AQA iOS

> :warning: **Attention**: В текущем документе нет вопросов по Swift, их вы можете легко найти на других ресурсах. Здесь вопросы и кейсы по XCUITest 


## Вопросы

<details>
  <summary>Какие версии iOS поддерживают XCTest?</summary>
  XCTest поддерживает iOS 10 и выше и XCode версии 7.2 и выше
</details>

<details>
  <summary>Какие типы тестов можно написать используя XCTest?</summary>
  XCTest позволяет написать: unit, ui и perfomance тесты
</details>

<details>
  <summary>Как "под капотом" работает XCUITest?</summary>
  Когда мы добавляем ui-тесты в проект Xcode, они находят в отдельном таргете с препиской UITest. Это связано с тем, что ui-тесты компилируются и развертываются в отдельном приложении. Код ui-тестов, который мы пишем, выполняется в приложении для запуска тестов, а не в целевом приложении. Приложение для выполнения тестов действует как прокси, оно берет написанную тестовую логику и транслирует её в iOS Accessibility actions, которые выполняет с целевым приложением. Это делается для имитации использования приложения так же, как это делает человек. С точки зрения разработчика это означает, что мы не взаимодействуем напрямую с элементами UIKit в нашем приложении, такими как UILabel или UIButton, а скорее через прокси-элементы, называемые XCUIElement.
</details>

<details>
  <summary>По каким признакам xcode автоматически добавляет автотесты в таргет?</summary>
  
  Класс в котором находится тест должен наследоваться от XCTestCase
  
  Тестовый метод должен быть: без параметров, без возвращаемого значения и с именем, начинающимся со слова test в нижнем регистре
</details>

<details>
  <summary>В чем различие между accessibilityidentifier и accessibilitylabel</summary>
  
  accessibilityidentifier - Это строка идентифицирующая ui-элемент, используется в ui-тестах 
  
  accessibilityLabel - Это краткое описание содержимого в элементе, например текст на кнопке, используется в Voice over 
  
</details>

<details>
  <summary>Как задать предусловие и постусловие для автотеста?</summary>
  
  С помощью `setUp()` и `tearDown()` методов. Также мы можем задавать эти условия для всего сьюта тестов либо отдельно для каждого теста.  
</details>

<details>
  <summary>Какие бывают ожидания и как реализовать их в XCTest?</summary>
  
  Ожидания бывают двух видов явные и неявные.
  
  Неявные ожидания можно реализовать несколькими способами:
  - `wait(for expectations: [XCTestExpectation], timeout seconds: TimeInterval)`;
  - `waitForExistence(timeout:)`.
  
  Явное ожидание можно реализовать - `Thread.sleep(forTimeInterval: 1)`
</details>

<details>
  <summary>Какой класс отвечает за поиск элемента в приложении и по каким признакам можно искать элемент?</summary>
  
  За поиск UI-элементов отвечает класс XCUIElementQuery. Элемент можно искать по:
  1. по индефикатору, самый надежный вариант поиска.
  2. по индексу типа элемента(например вторая кнопка на экране).
  3. по вложенности(children и descedants).
  4. по предикату.
</details>

<details>
  <summary>Для чего нужны тест планы в XCTest?</summary>
  Тест план предоставляет возможность запускать наборы тестов с различными конфигурациями. Тест план — это JSON файл с расширением .xctestplan, которым можно управлять через пользовательский интерфейс или из исходного кода. Его удобно использовать, когда у вас есть несколько наборов тестов: Smoke, Rregression или группы тестов которые должны гонять на разных локализациях или с разной геолокацией
</details>

<details>
  <summary>Как сбросить permissions при запуске тестов?</summary>
  Чтобы сбросить permissions, нужно вызвать метод resetAuthorizationStatus и передать в него значение из enum XCUIProtectedResource
</details>


<details>
  <summary> Можно ли запустить сторонее приложение из теста? Например Safari </summary>
  
  Да можно. Для этого нужно знать bundle id приложения и передать его в качестве аргумента в XCUIApplication.
  
  Пример `XCUIApplication(bundleIdentifier: "com.apple.mobilesafari").launch()` 
</details>

<details>
  <summary>Какие ты знаешь нативные и не нативные фреймворки реализации автотестов? И какие у них плюсы/минусы</summary>
  Основная нативная библиотека для iOS - это XCTest, также можно воспользоваться фреймворками Earlgrey, Kif, Calabash.
  
  Не нативный фреймворк - Appium.
  
  | Критерий      | XCTest | Appium|
| ----------- | ----------- |----------|
| Язык      | Swift/Objective-C | Любой |
| Стабильность тестов   | Более стабильные | Менее стабильные |
| Кросплатформенность | Нет | Да |
| Скорость | Быстрее | Медленее |
| Доступ к коду приложения | Нужен | Не нужен |
  
</details>

<details>
  <summary>Можно ли взаимодействовать с симулятором из командной строки?</summary>
  Да для взаимодействия есть утилита от apple - simctl
</details>

<details>
  <summary>Как можно ускорить прогон автотестов?</summary>
  
  Для ускорения тестов можно воспользоваться:
  - параллелизацией ui-тестов;
  - стартовать флоу с нужного экрана;
  - убрать дублирущие проверки в сценариях, если они есть;
  - перевести тесты на моки;
  - запускать тесты без сборки приложения, а на основании derived data
</details>

<details>
  <summary>Нужно улучшить текущий отчет об автотестах, что можно туда добавить и как будешь это реализовывать?</summary>
  
  В отчет можно добавить:
  - запись видео прогона теста;
  - логи сетевых запросов;
  - сделать более информативные вывод в ассертах;
  - разбить сценарий на шаги, используя XCTContext
</details>

<details>
  <summary>Как работает snapshot тестирование,как его можно реализовать?</summary>
  Snapshot тесты - это тесты которые делают скриншот экрана (эталонный скриншот) и сравнивают с актуальным скриншотом, который делается во время прогона тестов.
  
  Для реализации этого вида тестирование в iOS, есть две библиотеки: iOSSnapshotTestCase (previously FBSnapshotTestCase), SnapshotTesting.
  
  При реализации нужно будет обрезать status bar дабы он не аффектил результаты прогона теста 
</details>

## Кейсы

<details>
  <summary>Нужно реализовать свайп до нижнего элемента в таблице с скролом, как будешь это реализовывать?</summary>
  
  При реализации метода учесть ограничение на кол-во свайпов и видимость элемента на экране
</details>


<details>
  <summary>Дать кандидату плохо написанный автотест и спросить что можно исправить.</summary>
</details>

---

### Примечание

Данный документ будет пополняться. Если у вас есть интересные вопросы/кейсы, которыми можно дополнить этот документ, закидывайте их в Pull request
