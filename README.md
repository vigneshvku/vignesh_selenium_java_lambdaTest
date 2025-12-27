# vignesh_selenium_java_lambdaTest


SELENIUM AUTOMATION FRAMEWORK – FOLDER STRUCTURE

LambdaTestAutomationFramework

│

├── pom.xml

├── testng.xml

│

└── src

    ├── main

    │   ├── java

    │   │   ├── base

    │   │   │   └── BaseTest.java

    │   │   │

    │   │   ├── pages

    │   │   │   ├── HomePage.java

    │   │   │   ├── SimpleFormPage.java

    │   │   │   ├── DragDropSliderPage.java

    │   │   │   └── InputFormPage.java

    │   │   │

    │   │   └── utils

    │   │       ├── ConfigReader.java

    │   │       └── WaitUtils.java

    │   │

    │   └── resources

    │       └── config.properties

    │

    └── test

        └── java

            └── tests

                ├── TestScenario1.java

                ├── TestScenario2.java

                └── TestScenario3.java

BASE CLASS

BaseTest.java
package base;

import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.testng.annotations.AfterMethod;
import org.testng.annotations.BeforeMethod;

public class BaseTest {

    protected WebDriver driver;

    @BeforeMethod
    public void setUp() {
        driver = new ChromeDriver();
        driver.manage().window().maximize();
        driver.get("https://www.lambdatest.com/selenium-playground");
    }

    @AfterMethod
    public void tearDown() {
        driver.quit();
    }
}

Home Page
HomePage.java

package pages;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;

public class HomePage {

    WebDriver driver;

    By simpleFormDemo = By.linkText("Simple Form Demo");
    By dragDropSliders = By.linkText("Drag & Drop Sliders");
    By inputFormSubmit = By.linkText("Input Form Submit");

    public HomePage(WebDriver driver) {
        this.driver = driver;
    }

    public void clickSimpleFormDemo() {
        driver.findElement(simpleFormDemo).click();
    }

    public void clickDragDropSliders() {
        driver.findElement(dragDropSliders).click();
    }

    public void clickInputFormSubmit() {
        driver.findElement(inputFormSubmit).click();
    }
}

SCENARIO 1 – SIMPLE FORM PAGE
SimpleFormPage.java
package pages;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;

public class SimpleFormPage {

    WebDriver driver;

    By messageInput = By.id("user-message");
    By getCheckedValueBtn = By.id("showInput");
    By messageText = By.id("message");

    public SimpleFormPage(WebDriver driver) {
        this.driver = driver;
    }

    public void enterMessage(String message) {
        driver.findElement(messageInput).sendKeys(message);
    }

    public void clickGetCheckedValue() {
        driver.findElement(getCheckedValueBtn).click();
    }

    public String getMessage() {
        return driver.findElement(messageText).getText();
    }
}


SCENARIO 2 – DRAG & DROP SLIDER PAGE
DragDropSliderPage.java

package pages;

import org.openqa.selenium.*;
import org.openqa.selenium.interactions.Actions;

public class DragDropSliderPage {

    WebDriver driver;

    By slider = By.xpath("//input[@value='15']");
    By output = By.id("rangeSuccess");

    public DragDropSliderPage(WebDriver driver) {
        this.driver = driver;
    }

    public void moveSliderTo95() {
        Actions actions = new Actions(driver);
        WebElement sliderElement = driver.findElement(slider);
        WebElement outputElement = driver.findElement(output);

        while (!outputElement.getText().equals("95")) {
            actions.dragAndDropBy(sliderElement, 5, 0).perform();
        }
    }

    public String getSliderValue() {
        return driver.findElement(output).getText();
    }
}
package pages;

import org.openqa.selenium.*;
import org.openqa.selenium.interactions.Actions;

public class DragDropSliderPage {

    WebDriver driver;

    By slider = By.xpath("//input[@value='15']");
    By output = By.id("rangeSuccess");

    public DragDropSliderPage(WebDriver driver) {
        this.driver = driver;
    }

    public void moveSliderTo95() {
        Actions actions = new Actions(driver);
        WebElement sliderElement = driver.findElement(slider);
        WebElement outputElement = driver.findElement(output);

        while (!outputElement.getText().equals("95")) {
            actions.dragAndDropBy(sliderElement, 5, 0).perform();
        }
    }

    public String getSliderValue() {
        return driver.findElement(output).getText();
    }
}
package pages;

import org.openqa.selenium.*;
import org.openqa.selenium.interactions.Actions;

public class DragDropSliderPage {

    WebDriver driver;

    By slider = By.xpath("//input[@value='15']");
    By output = By.id("rangeSuccess");

    public DragDropSliderPage(WebDriver driver) {
        this.driver = driver;
    }

    public void moveSliderTo95() {
        Actions actions = new Actions(driver);
        WebElement sliderElement = driver.findElement(slider);
        WebElement outputElement = driver.findElement(output);

        while (!outputElement.getText().equals("95")) {
            actions.dragAndDropBy(sliderElement, 5, 0).perform();
        }
    }

    public String getSliderValue() {
        return driver.findElement(output).getText();
    }
}
Scenario 3 - INPUT FORM PAGE
InputFormPage.java
package pages;

import org.openqa.selenium.*;
import org.openqa.selenium.support.ui.Select;

public class InputFormPage {

    WebDriver driver;

    By submitBtn = By.xpath("//button[text()='Submit']");
    By nameField = By.id("name");
    By successMsg = By.className("success-msg");

    public InputFormPage(WebDriver driver) {
        this.driver = driver;
    }

    public void clickSubmitWithoutData() {
        driver.findElement(submitBtn).click();
    }

    public String getNameFieldValidationMessage() {
        return driver.findElement(nameField)
                .getAttribute("validationMessage");
    }

    public void fillAllFields() {

        driver.findElement(nameField).sendKeys("Vignesh");
        driver.findElement(By.id("inputEmail4")).sendKeys("vignesh@test.com");
        driver.findElement(By.id("inputPassword4")).sendKeys("Test@123");
        driver.findElement(By.id("company")).sendKeys("LambdaTest");
        driver.findElement(By.id("websitename")).sendKeys("https://example.com");

        new Select(driver.findElement(By.name("country")))
                .selectByVisibleText("United States");

        driver.findElement(By.id("inputCity")).sendKeys("New York");
        driver.findElement(By.id("inputAddress1")).sendKeys("Street 1");
        driver.findElement(By.id("inputAddress2")).sendKeys("Street 2");
        driver.findElement(By.id("inputState")).sendKeys("NY");
        driver.findElement(By.id("inputZip")).sendKeys("10001");
    }

    public void clickSubmit() {
        driver.findElement(submitBtn).click();
    }

    public String getSuccessMessage() {
        return driver.findElement(successMsg).getText();
    }
}

TEST CLASSES

TestScenario1.java

package tests;

import base.BaseTest;
import pages.*;
import org.testng.Assert;
import org.testng.annotations.Test;

public class TestScenario1 extends BaseTest {

    @Test
    public void verifySimpleForm() {

        HomePage home = new HomePage(driver);
        home.clickSimpleFormDemo();

        SimpleFormPage page = new SimpleFormPage(driver);
        page.enterMessage("Welcome to LambdaTest");
        page.clickGetCheckedValue();

        Assert.assertEquals(page.getMessage(), "Welcome to LambdaTest");
    }
}

TestScenario2.java

package tests;

import base.BaseTest;
import pages.*;
import org.testng.Assert;
import org.testng.annotations.Test;

public class TestScenario2 extends BaseTest {

    @Test
    public void verifyDragAndDropSlider() {

        HomePage home = new HomePage(driver);
        home.clickDragDropSliders();

        DragDropSliderPage sliderPage = new DragDropSliderPage(driver);
        sliderPage.moveSliderTo95();

        Assert.assertEquals(sliderPage.getSliderValue(), "95");
    }
}

TestScenario3.java
package tests;

import base.BaseTest;
import pages.*;
import org.testng.Assert;
import org.testng.annotations.Test;

public class TestScenario3 extends BaseTest {

    @Test
    public void verifyInputFormSubmit() {

        HomePage home = new HomePage(driver);
        home.clickInputFormSubmit();

        InputFormPage formPage = new InputFormPage(driver);

        formPage.clickSubmitWithoutData();

        Assert.assertEquals(
                formPage.getNameFieldValidationMessage(),
                "Please fill out this field."
        );

        formPage.fillAllFields();
        formPage.clickSubmit();

        Assert.assertTrue(
                formPage.getSuccessMessage()
                        .contains("Thanks for contacting us, we will get back to you shortly.")
        );
    }
}
