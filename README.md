Задание 1 
1. Эквивалентное деление
Эта техника подразумевает разделение всех возможных входных данных на эквивалентные классы. В нашем случае это может быть стаж вождения и количество страховых случаев:
  Стаж вождения:
  0-3 года
  3-5 лет
  5-10 лет
  Более 10 лет
  Количество страховых случаев:
  0 страховок
  1-2 страховки
  3-5 страховок
  Более 5 страховок
Каждый класс будет тестировать свою логику начисления скидок и наценок.
2. Граничные значения
Здесь мы проверяем условия на границах классов:
  Стаж вождения:
  0, 3, 5, 10 лет
  Количество страховых случаев:
  0, 2, 3, 5, 6
Граничные условия помогают выявить возможные ошибки при проверке.
3. Состояния и переходы
Тестирование различных состояний пользователя и их переходов в зависимости от изменений входящих параметров. Например:
  Переход от 3 лет стажа в 5 лет, при этом вывод информации о скидке.
  Переход от 5 страховок к 6 и проверка наценки.
4. Тестирование условий
Здесь мы проверяем различные условия награждения скидками и наценками, комбинируя их:
  Например, тестирование стажа вождения 5-10 лет и 3-5 страховок.
Примеры тестов
  Стаж 2 года, 0 страховок — ожидаемая скидка: 0%.
  Стаж 4 года, 0 страховок — ожидаемая скидка: 5%.
  Стаж 6 лет, 0 страховок — ожидаемая скидка: 10%.
  Стаж 12 лет, 0 страховок — ожидаемая скидка: 15%.
  Стаж 5 лет, 3 страховки — ожидаемая скидка/наценка: 0%.
  Стаж 2 года, 6 страховок — ожидаемая результат: отказ в страховке.


  Задание 2: Автотест на языке Java
Код:
import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;

public class TextBoxTest {
    public static void main(String[] args) {
        // Укажите путь к драйверу Chrome
        System.setProperty("webdriver.chrome.driver", "path/to/chromedriver");

        WebDriver driver = new ChromeDriver();
        driver.get("https://demoqa.com/");

        // Нажать на блок «Elements»
        driver.findElement(By.xpath("//div[@class='category-previews']//h5[text()='Elements']")).click();
        
        // Выбрать поле «Text Box»
        driver.findElement(By.xpath("//span[text()='Text Box']")).click();

        // Заполнить все поля
        driver.findElement(By.id("userName")).sendKeys("Имя Фамилия");
        driver.findElement(By.id("userEmail")).sendKeys("example@mail.com");
        driver.findElement(By.id("currentAddress")).sendKeys("Текущий адрес");
        driver.findElement(By.id("permanentAddress")).sendKeys("Постоянный адрес");

        // Нажать кнопку «Submit»
        driver.findElement(By.id("submit")).click();

        // Проверка правильности данных
        WebElement output = driver.findElement(By.id("output"));
        String expectedResult = "Имя Фамилияexample@mail.comТекущий адресПостоянный адрес";
        if (output.getText().equals(expectedResult)) {
            System.out.println("Тест пройден успешно!");
        } else {
            System.out.println("Тест не пройден.");
        }

        // Закрыть браузер
        driver.quit();
    }
}