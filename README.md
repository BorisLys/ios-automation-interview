# Интервью на позицию AQA iOS

> :warning: **Attention**: В текущем документе нет вопрос по Swift, их вы можете легко найти на других ресурсах. Здесь вопросы и кейсы по XCUITest 


## Вопросы

<details>
  <summary>Когда впервые анонсировали XCTest?</summary>
  XCTest был впервые анонсирован на WWDC 2016 одновременно с выпуском iOS 10
</details>

<details>
  <summary>Какие типы тестов можно написать используя XCTest?</summary>
  XCTest позволяет написать: unit, ui и perfomance тесты
</details>

<details>
  <summary>Как "под капотом" работает XCUITest?</summary>
  Когда мы добавляем ui-тесты в проект Xcode, они находят в отдельном таргете с препиской UITest. Это связано с тем, что ui-тесты компилируются и развертываются в отдельном приложении. Код ui-тестов, который мы пишем, выполняется в приложении для запуска тестов, а не в целевом приложении. Приложение для выполнения тестов действует как прокси, оно берет написанную тестовую логику и транслирует её в iOS Accessibility actions, которые выполняет с вашим целевым приложением. Это делается для имитации использования вашего приложения так же, как это делает человек. С точки зрения разработчика это означает, что мы не взаимодействуем напрямую с элементами UIKit в нашем приложении, такими как UILabel или UIButton, а скорее через прокси-элементы, называемые XCUIElement.
</details>

<details>
  <summary>Как задать предусловие и постусловие для автотеста?</summary>
  
  С помощью `setUp()` и `tearDown()` методов. Также мы можем задавать эти условия для всего сьюта тестов либо отдельно для каждого теста.  
</details>

<details>
  <summary>Какие бывают ожидания и как реализовать их в XCTest?</summary>
  Ожидания бывают двух видов явные и не явные.
  
  Явные ожидания можно реализовать несколькими способами:
  - 
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
  <summary>Какие ты знаешь нативные и не нативные способы реализации автотестов? И какие у них плюсы/минусы</summary>
  заглушка
</details>

<details>
  <summary>Какие знаешь фреймворки iOS автоматизации?</summary>
  заглушка
</details>

## Кейсы

<details>
  <summary>Как можно ускорить прогон автотестов?</summary>
  заглушка
</details>

<details>
  <summary>Нужно реализовать свайп до нижнего элемента в таблице с скролом, как будешь это реализовывать?</summary>
  заглушка
</details>

<details>
  <summary>Нужно улучшить текущий отчет об автотестах, что можно туда добавить и как будешь это реализовывать?</summary>
  заглушка
</details>

---

### Примечание

Данный документ будет пополняться. Если у вас есть интересные вопросы/кейсы, которыми можно дополнить этот документ, закидывайте их в Pull request
