package com.dezlearn.tests;

import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.testng.Assert;
import org.testng.annotations.AfterMethod;
import org.testng.annotations.BeforeMethod;
import org.testng.annotations.Test;

public class Ebay_Advanced_Search_Sanity {
	
	WebDriver driver;

	@BeforeMethod
    public void setUp() throws Exception {
		System.setProperty("webdriver.chrome.driver", "/Users/mayurdeshmukh/Documents/Drivers/chromedriver");
		driver = new ChromeDriver();
		driver.get("https://www.ebay.com/sch/ebayadvsearch");
		Thread.sleep(2000);
   }
	  
	@AfterMethod
	public void tearDown() {
		driver.close();
	}
	
	@Test
	public void empty_advanced_search_test() throws Exception {
		String expectedURL = "https://www.ebay.com/v/allcategories";
		String expectedTitle = "All Categories - Browse and Discover more | eBay";
		WebElement searchBtn = driver.findElement(By.cssSelector("button.btn-prim"));
		
		Assert.assertTrue(searchBtn.isEnabled(), "Verify Search Button Enabled");
		
		searchBtn.click();
		Thread.sleep(2000);
		
		String newUrl = driver.getCurrentUrl();
		String newTitle = driver.getTitle();
		System.out.println(newUrl);
		System.out.println(newTitle);
	
		Assert.assertEquals(newUrl, expectedURL,"Verify URL of the new page");
		Assert.assertEquals(newTitle, expectedTitle,"Verify Title of the new page");
	}
	
	@Test
	public void category_options_in_ascending_order_test() {
		
		List<WebElement> category_options = driver.findElements(By.cssSelector("select#e1-1>option"));
		List<String> arr1 = new ArrayList<String>();
		
		for(WebElement option : category_options) {
			arr1.add(option.getText());
		}
		List<String> arr2 = new ArrayList<String>(arr1);
		Collections.sort(arr2);
		System.out.println("Actual List:" + arr1);
		System.out.println("Sorted List:" + arr2);
		Assert.assertTrue(arr1.equals(arr2), "Verify Category Items Sorted");
	}
}
