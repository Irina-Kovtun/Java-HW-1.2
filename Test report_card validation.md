# Краткое описание

## Тестирование  функциональности программы валидации банковских карт

**Дата начала:** *17.08.2020*
**Дата окончания:** *17.08.2020*
На тестирование затрачено: 2 часа

### Что нужно проверить:
Проверить функциональность кода по проверке валидности банковских карт

### В результате тестирования выявлены следующие дефекты:
В коде не заложена проверка карт с менее или более 16 знаков в номере карты

## Описание процесса тестирования:
1. Запустить IntelliJ IDEA Community
2. Загрузить код:

```java
public class Main {
  public static void main(String[] args) {
    // TODO: подставлять номер карты нужно сюда между двойными кавычками, без пробелов
    String number = "5351719427810741";
    System.out.println(String.format("Result is %s", isValidCardNumber(number) ? "OK" : "FAIL"));
  }

  public static boolean isValidCardNumber(String number) {
    if (number == null) {
      return false;
    }

    if (number.length() != 16) {
      return false;
    }

    long result = 0;
    for (int i = 0; i < number.length(); i++) {
      int digit;
      try {
        digit = Integer.parseInt(number.charAt(i) + "");
      } catch (NumberFormatException e) {
        return false;
      }

      if (i % 2 == 0) {
        digit *= 2;
        if (digit > 9) {
          digit -= 9;
        }
      }
      result += digit;
    }

    return (result != 0) && (result % 10 == 0);
  }
}
```

3. Запустить код на исполнение с разными тестовыми данными в строке 4. 

#### В процессе тестирования составлены 2 багрепорта.

### В качестве тестовых данных использовались  номера банковских карт, сгенерированные сайтом [freeformatter.com](https://www.freeformatter.com/credit-card-number-generator-validator.html):
1. 16 значный номер
2. 14 значный номер
3. 19 значный номер

### Тестирование производилось в следующем окружении:

-  Ноутбук Aspire А515-52
- Windows 10 Home, x64
-  версия Java 11.0.8
- браузер Google Chrome 84.0.4147.125, x64

