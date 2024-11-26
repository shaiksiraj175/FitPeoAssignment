# FitPeoAssignment
## 1. Source code of My Automation Script:

      package com.naukriassignment;
      
      import java.time.Duration;      
      import org.openqa.selenium.By;
      import org.openqa.selenium.JavascriptExecutor;
      import org.openqa.selenium.Keys;
      import org.openqa.selenium.WebDriver;
      import org.openqa.selenium.WebElement;
      import org.openqa.selenium.chrome.ChromeDriver;
      import org.openqa.selenium.interactions.Actions;
      import org.openqa.selenium.support.ui.ExpectedConditions;
      import org.openqa.selenium.support.ui.WebDriverWait;
      import org.testng.Assert;
      import org.testng.annotations.AfterClass;
      import org.testng.annotations.Test;
      
      public class FitPeoAssignment {      
      	WebDriver driver;
      	WebElement value, totalPurse;      
      	@Test(priority = 1)
      	public void navigatetToFitPeoHomepage() {
      		driver = new ChromeDriver();
      		driver.manage().window().maximize();
      		driver.get("https://www.fitpeo.com/");
      	}
      
      	@Test(priority = 2)
      	public void navigateToRevenueCalculatorPage() throws InterruptedException {
      		Thread.sleep(5000);
      		driver.navigate().to("https://fitpeo.com/revenue-calculator");
      	}
      
      	@Test(priority = 3)
      	public void scrollDownTheSliderSection() {
      		WebElement visibleEl = driver.findElement(By.xpath("//h4[contains(text(),'Medicare Eligible Patients')]"));
      		WebDriverWait wait = new WebDriverWait(driver, Duration.ofSeconds(10));
      		wait.until(ExpectedConditions
      				.visibilityOfElementLocated(By.xpath("//h4[contains(text(),'Medicare Eligible Patients')]")));
      		JavascriptExecutor js = (JavascriptExecutor) driver;
      		js.executeScript("arguments[0].scrollIntoView(true);", visibleEl);
      	}
      
      	@Test(priority = 4)
      	public void adjustTheSlider() throws InterruptedException {
      		Thread.sleep(5000);
      		WebElement patientsTextField = driver.findElement(By.id(":R57alklff9da:"));
      		patientsTextField.sendKeys(Keys.CONTROL + "a", Keys.DELETE);
      		WebElement slider = driver.findElement(By.cssSelector(
      				"body > div.MuiBox-root.css-3f59le > div.MuiBox-root.css-rfiegf > div.MuiGrid-root.MuiGrid-container.MuiGrid-spacing-xs-6.css-l0ykmo > div:nth-child(2) > div > div > span.MuiSlider-root.MuiSlider-colorPrimary.MuiSlider-sizeMedium.css-16i48op"));
      		WebDriverWait wait = new WebDriverWait(driver, Duration.ofSeconds(10));
      		wait.until(ExpectedConditions.visibilityOfElementLocated((By.cssSelector(
      				"body > div.MuiBox-root.css-3f59le > div.MuiBox-root.css-rfiegf > div.MuiGrid-root.MuiGrid-container.MuiGrid-spacing-xs-6.css-l0ykmo > div:nth-child(2) > div > div > span.MuiSlider-root.MuiSlider-colorPrimary.MuiSlider-sizeMedium.css-16i48op"))));
      		Actions actions = new Actions(driver);
      		actions.clickAndHold(slider).moveByOffset(-26, 0).release().perform();
      		for (int i = 0; i < 3; i++) {
      			actions.sendKeys(Keys.ARROW_LEFT).perform();
      		}
      	}
      
      	@Test(priority = 5)
      	public void updateTheTextField() {
      		value = driver.findElement(By.xpath("(//input[@value= '820'])[2]"));
      		value.sendKeys(Keys.CONTROL + "a", Keys.DELETE);
      		value.sendKeys("560", Keys.TAB);
      	}
      
      	@Test(priority = 6)
      	public void validateSliderValue() {
      		WebElement slider2 = driver.findElement(By.xpath("//input[@data-index='0']"));
      		if (Integer.parseInt(slider2.getAttribute("value")) == 560) {
      			System.out.println(
      					"The value 560 is entered in the text field, the slider's position is updated to reflect the value 560.");
      		}
      	}
      
      	@Test(priority = 7)
      	public void selectCPTCodes() {
      		value.sendKeys(Keys.CONTROL + "a", Keys.DELETE);
      		value.sendKeys("820");
      		driver.findElement(By.xpath("(//input[@type='checkbox'])[1]")).click();
      		driver.findElement(By.xpath("(//input[@type='checkbox'])[2]")).click();
      		driver.findElement(By.xpath("(//input[@type='checkbox'])[3]")).click();
      		driver.findElement(By.xpath("(//input[@type='checkbox'])[8]")).click(); 
      	}
       
      	@Test(priority = 8)
      	public void validateTotalRecurringReimbursement() {
      		totalPurse = driver
      				.findElement(By.xpath("(//p[@class='MuiTypography-root MuiTypography-body2 inter css-1xroguk'])[4]"));
      		System.out.println(totalPurse.getText()); 
      	}
      
      	@Test(priority = 9)
      	public void verifyTotalRecurringReimbursement() throws InterruptedException {   
      		String exp = "Total Recurring Reimbursement for all Patients Per Month:\r\n$110700";
      		String actual = totalPurse.getText().replace("\r\n", "\n").replace("\r", "\n");
      		String expected = exp.replace("\r\n", "\n").replace("\r", "\n");
      		Assert.assertEquals(actual, expected);      
      	}
      
      	// tearDown() method is used to close the browser window.
      	@AfterClass
      	public void tearDown() {
      		// driver.quit();
      	}
      }
      
      

This project automates the Revenue Calculator functionality on the FitPeo website using Selenium WebDriver with Java and TestNG. It performs the following tasks:

    1. Navigates to the FitPeo Homepage and the Revenue Calculator page.
    2. Interacts with the slider and text field to validate their functionality.
    3. Selects specific CPT codes and validates the Total Recurring Reimbursement.

## 2. Prerequisites or System requirements :
    Java Development Kit .
    Maven for managing dependencies.
    Eclipse (or) Intellij IDE.
    Chrome Browser and ChromeDriver.
   
## 3. Project Setup:
    a) Creating a Maven Project
       Providing a Group ID (e.g., com.fitpeo.tests) and Artifact ID (e.g., FitPeoAutomation).
    b) Adding Selenium and TestNG Dependencies
   
## 4. Features:
        Automates end-to-end test scenarios for the FitPeo Revenue Calculator.
        Validates dynamic UI interactions such as sliders and text fields.
   
## 5.Test Scenarios Covered:

     Test Scenario 1: Navigate to the FitPeo Homepage
     Description: Open the web browser and navigate to the FitPeo homepage.  
        
     Test Scenario 2: Navigate to the Revenue Calculator Page
     Description: From the FitPeo homepage, navigate to the Revenue Calculator Page.
        
     Test Scenario 3: Scroll Down to the Slider Section
     Description: Scroll down the page until the revenue calculator slider is visible.
      
      Test Scenario 4: Adjust the Slider to Set Value to 820
      Description: Adjust the slider to set its value to 820.
      
      Test Scenario 5: Update the Text Field to 560
      Description: Click on the text field associated with the slider and enter the value 560.
     
      Test Scenario 6: Validate Slider Value after Entering 560 in Text Field
      Description: Ensure that when the value 560 is entered in the text field, the slider's position is updated to reflect the value 560.

      Test Scenario 7: Select CPT Codes
      Description: Scroll down and select the checkboxes for CPT-99091, CPT-99453, CPT-99454, and CPT-99474.
      
      Test Scenario 8: Test Scenario Title: Validate the Total Recurring Reimbursement value for all patients per month.
      Description: This test scenario ensures that the Total Recurring Reimbursement for all patients per month is correctly calculated and displayed on the Revenue Calculator page 
       after selecting the required CPT codes and adjusting the slider.
    
      Test Scenario 9: Verify that the header displaying "Total Recurring Reimbursement for all Patients Per Month" shows the value $110,700.
      Description: This test scenario verifies that the correct value of $110,700 is displayed in the header labeled "Total Recurring Reimbursement for all Patients Per Month" on the 
      Revenue Calculator page.

      
      
### *Note: I have Attached FitPeoTest.java (test script) along with pom.xml file which consists of maven dependencies to make the task of running my script easier*.
    

