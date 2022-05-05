package com.dezlearn.tests;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.testng.annotations.AfterClass;
import org.testng.annotations.AfterMethod;
import org.testng.annotations.BeforeClass;
import org.testng.annotations.BeforeMethod;
import org.testng.annotations.Test;
import org.testng.asserts.SoftAssert;
import org.testng.Assert;

public class Ebay_Home_Sanity {
	
	WebDriver driver;
	
   /*
      *** Assertions ***
      Assert.assertEquals(actual, expected, message);
	  Assert.assertNotEquals(actual1, actual2, message);
	  Assert.assertTrue(condition, message);
	  Assert.assertFalse(condition, message);
	  Assert.assertNull(object, message);
	  Assert.assertNotNull(object, message);
   */
	
  @BeforeClass
  public void beforeClassSetup() {
	  System.out.println("Before Class Settings Done");
	  System.out.println("Execution Starts: EBayHome_Sanity");
  }
  
  @AfterClass
  public void afterClassSetup() {
	  System.out.println("After Class Settings Done");
	  System.out.println("Execution Ends: EBayHome_Sanity");
  }
  
  @BeforeMethod
  public void setUp() throws Exception {
	  System.setProperty("webdriver.chrome.driver", "/Users/mayurdeshmukh/Documents/Drivers/chromedriver");
	  driver = new ChromeDriver();
	  driver.get("https://www.ebay.com/");
	  Thread.sleep(2000);
  }
  
  @AfterMethod
  public void tearDown() {
	  driver.close();
  }
		
  @Test
  public void empty_search_test() throws Exception {
	 
	  String expectedURL = "https://www.ebay.com/v/allcategories";
	  String expectedTitle = "All Categories - Browse and Discover more | eBay";
	  
	  Assert.assertTrue(driver.findElement(By.cssSelector("input#gh-btn")).isEnabled(), "Verify Search Button Enabled");
	  
	  driver.findElement(By.cssSelector("input#gh-btn")).click();
	  Thread.sleep(2000);
	  String newUrl = driver.getCurrentUrl();
	  String newTitle = driver.getTitle();
	  System.out.println(newUrl);
	  System.out.println(newTitle);
	
	  Assert.assertEquals(newUrl, expectedURL,"Verify URL of the new page");
	  Assert.assertEquals(newTitle, expectedTitle,"Verify Title of the new page");
	
  }	
  
  @Test
  public void empty_search_test_softassert() throws Exception {
	  
	  SoftAssert sa = new SoftAssert();
	  
	  String expectedURL = "https://www.ebay.com/v/allcategories";
	  String expectedTitle = "All Categories - Browse and Discover more | eBay";
	  
	  sa.assertTrue(driver.findElement(By.cssSelector("input#gh-btn")).isEnabled(), "Verify Search Button Enabled");
	  
	  driver.findElement(By.cssSelector("input#gh-btn")).click();
	  Thread.sleep(2000);
	  String newUrl = driver.getCurrentUrl();
	  String newTitle = driver.getTitle();
	  System.out.println(newUrl);
	  System.out.println(newTitle);
	
	  sa.assertEquals(newUrl, expectedURL,"Verify URL of the new page");
	  sa.assertEquals(newTitle, expectedTitle,"Verify Title of the new page");
	
	  sa.assertAll();
  }
}