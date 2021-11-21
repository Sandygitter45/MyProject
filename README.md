# package com.Test;

import java.io.IOException;

import org.apache.poi.EncryptedDocumentException;
import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.testng.annotations.*;
import org.testng.asserts.SoftAssert;

import com.POM.HrmLogin;

import utility.BrowserSetup;
import utility.ExcelMethod;

public class TestCases {

	WebDriver driver;
	ExcelMethod e = new ExcelMethod();

	@BeforeMethod
	public void browser() {
		//Website: https://opensource-demo.orangehrmlive.com/

		BrowserSetup set = new BrowserSetup();
		driver = set.browserInit();
	}

	// To check login functionality
	//Verify that user should Enter valid Username and valid password and click on login button

	@Test
	public void tc01() throws EncryptedDocumentException, IOException {
		HrmLogin h = new HrmLogin(driver);
		h.enterUserName(e.excelRead(0, 0));
		h.enterPassword(e.excelRead(0, 1));
		h.clickButton();
		// Title assertion
		String actualTitle = driver.getTitle();
		String expectedTitle = "OrangeHRM";
		SoftAssert soft = new SoftAssert();
		soft.assertEquals(actualTitle, expectedTitle, "Title is mismatched");

		// Url Assertion
		String actualUrl = driver.getCurrentUrl();
		String expectedUrl = "https://opensource-demo.orangehrmlive.com/index.php/dashboard";
		soft.assertEquals(actualUrl, expectedUrl, "Url is mismatched");

		
		driver.close();
		soft.assertAll();

	}
	//Verify that if user Enter valid Username and invalid password and click on login button
	@Test
	public void tc02() throws EncryptedDocumentException, IOException {
		HrmLogin h = new HrmLogin(driver);
		h.enterUserName(e.excelRead(1, 0));
		h.enterPassword(e.excelRead(1, 1));
		h.clickButton();
		SoftAssert soft = new SoftAssert();

		String actualUrl = driver.getCurrentUrl();
		String expectedUrl = "https://opensource-demo.orangehrmlive.com/index.php/auth/validateCredentials";
		soft.assertEquals(actualUrl, expectedUrl, "Url is mismatched");

		String actualError = driver.findElement(By.id("spanMessage")).getText();
		String expectedError = "Invalid credentials";
		soft.assertEquals(actualError, expectedError, "Error Message is Wrong");

		// text Assertion
		String actualText = driver.findElement(By.name("txtUsername")).getAttribute("value");
		String expectedText = "";
		soft.assertEquals(actualText, expectedText, "TextBox text is mismatched");
		driver.quit();
		soft.assertAll();

	}
	//Verify that if user Enter invalid Username and invalid password and click on login button
	@Test
	public void tc03() throws EncryptedDocumentException, IOException {

		HrmLogin h = new HrmLogin(driver);
		h.enterUserName(e.excelRead(2, 0));
		h.enterPassword(e.excelRead(2, 1));
		h.clickButton();

		// Url assertion
		SoftAssert soft = new SoftAssert();
		String actualUrl = driver.getCurrentUrl();
		String expectedUrl = "https://opensource-demo.orangehrmlive.com/index.php/auth/validateCredentials";
		soft.assertEquals(actualUrl, expectedUrl, "Url is mismatched");

		// error msg Assertion
		String actualError = driver.findElement(By.id("spanMessage")).getText();
		String expectedError = "Invalid credentials";
		soft.assertEquals(actualError, expectedError, "Error Message is Wrong");

		// text Assertion
		String actualText = driver.findElement(By.name("txtUsername")).getAttribute("value");
		String expectedText = "";
		soft.assertEquals(actualText, expectedText, "TextBox text is mismatched");

		String actualValue = driver.findElement(By.name("txtPassword")).getAttribute("value");
		String expectedValue = "";
		soft.assertEquals(actualValue, expectedValue, "password text is mismatched");

		driver.quit();
		soft.assertAll();

	}
	//Verify that if user Enter invalid Username and valid password and click on login button
	@Test
	public void tc04() throws EncryptedDocumentException, IOException {

		HrmLogin h = new HrmLogin(driver);
		h.enterUserName(e.excelRead(3, 0));
		h.enterPassword(e.excelRead(3, 1));
		h.clickButton();

		// Url assertion
		SoftAssert soft = new SoftAssert();
		String actualUrl = driver.getCurrentUrl();
		String expectedUrl = "https://opensource-demo.orangehrmlive.com/index.php/auth/validateCredentials";
		soft.assertEquals(actualUrl, expectedUrl, "Url is mismatched");

		// error msg Assertion
		String actualError = driver.findElement(By.id("spanMessage")).getText();
		String expectedError = "Invalid credentials";
		soft.assertEquals(actualError, expectedError, "Error Message is Wrong");

		// text Assertion
		String actualText = driver.findElement(By.name("txtUsername")).getAttribute("value");
		String expectedText = "";
		soft.assertEquals(actualText, expectedText, "TextBox text is mismatched");

		String actualValue = driver.findElement(By.name("txtPassword")).getAttribute("value");
		String expectedValue = "";
		soft.assertEquals(actualValue, expectedValue, "password text is mismatched");

		driver.quit();
		soft.assertAll();

	}
	//Verify that if user Enter valid Username and password field is blank and click on login button 
	@Test
	public void tc05() throws EncryptedDocumentException, IOException {

		HrmLogin h = new HrmLogin(driver);
		h.enterUserName(e.excelRead(4, 0));
		h.clickButton();

		// Url assertion
		SoftAssert soft = new SoftAssert();
		String actualUrl = driver.getCurrentUrl();
		String expectedUrl = "https://opensource-demo.orangehrmlive.com/";
		soft.assertEquals(actualUrl, expectedUrl, "Url is mismatched");

		// error msg Assertion
		String actualError = driver.findElement(By.id("spanMessage")).getText();
		String expectedError = "Password cannot be empty";
		soft.assertEquals(actualError, expectedError, "Error Message is Wrong");

		driver.quit();
		soft.assertAll();

	}
	//Verify that if user Enter invalid Username and password field is blank and click on login button
	@Test
	public void tc06() throws EncryptedDocumentException, IOException {

		HrmLogin h = new HrmLogin(driver);
		h.enterUserName(e.excelRead(5, 0));
		h.clickButton();

		// Url assertion
		SoftAssert soft = new SoftAssert();
		String actualUrl = driver.getCurrentUrl();
		String expectedUrl = "https://opensource-demo.orangehrmlive.com/";
		soft.assertEquals(actualUrl, expectedUrl, "Url is mismatched");

		// error msg Assertion
		String actualError = driver.findElement(By.id("spanMessage")).getText();
		String expectedError = "Password cannot be empty";
		soft.assertEquals(actualError, expectedError, "Error Message is Wrong");

		driver.quit();
		soft.assertAll();
	}
	//Verify that if user Enter blank Username and valid password field and click on login button
	@Test
	public void tc07() throws EncryptedDocumentException, IOException {

		HrmLogin h = new HrmLogin(driver);
		h.enterPassword(e.excelRead(6, 1));
		h.clickButton();

		// Url assertion
		SoftAssert soft = new SoftAssert();
		String actualUrl = driver.getCurrentUrl();
		String expectedUrl = "https://opensource-demo.orangehrmlive.com/";
		soft.assertEquals(actualUrl, expectedUrl, "Url is mismatched");

		// error msg Assertion
		String actualError = driver.findElement(By.id("spanMessage")).getText();
		String expectedError = "Username cannot be empty";
		soft.assertEquals(actualError, expectedError, "Error Message is Wrong");

		driver.quit();
		soft.assertAll();
	}
	//Verify that if user Enter blank Username and invalid password and click on login button
	@Test
	public void tc08() throws EncryptedDocumentException, IOException {

		HrmLogin h = new HrmLogin(driver);
		h.enterPassword(e.excelRead(7, 1));
		h.clickButton();

		// Url assertion
		SoftAssert soft = new SoftAssert();
		String actualUrl = driver.getCurrentUrl();
		String expectedUrl = "https://opensource-demo.orangehrmlive.com/";
		soft.assertEquals(actualUrl, expectedUrl, "Url is mismatched");

		// error msg Assertion
		String actualError = driver.findElement(By.id("spanMessage")).getText();
		String expectedError = "Username cannot be empty";
		soft.assertEquals(actualError, expectedError, "Error Message is Wrong");

		driver.quit();
		soft.assertAll();
	}
	//Verify that if user Enter blank Username and password field is blank and click on login button
	@Test
	public void tc09() throws EncryptedDocumentException, IOException {

		HrmLogin h = new HrmLogin(driver);
		h.clickButton();

		// Url assertion
		SoftAssert soft = new SoftAssert();
		String actualUrl = driver.getCurrentUrl();
		String expectedUrl = "https://opensource-demo.orangehrmlive.com/";
		soft.assertEquals(actualUrl, expectedUrl, "Url is mismatched");

		// error msg Assertion
		String actualError = driver.findElement(By.id("spanMessage")).getText();
		String expectedError = "Username cannot be empty";
		soft.assertEquals(actualError, expectedError, "Error Message is Wrong");
		driver.quit();
		soft.assertAll();
	}
}
