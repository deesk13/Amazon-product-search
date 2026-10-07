# Amazon Selenium Automation

## Project Overview

This project automates the Amazon product search and Add to Cart workflow using Python and Selenium WebDriver.

The automation opens Amazon India, searches for a laptop, retrieves product details, opens the first product, adds it to the shopping cart, and verifies the cart count.

## Aim

To automate and validate the product search and Add to Cart functionality of an e-commerce website using Selenium WebDriver.

## Technologies Used

- Python
- Selenium WebDriver
- Google Chrome
- ChromeDriver

## Automation Flow

Launch Browser
→ Open Amazon India
→ Search for Laptop
→ Wait for Search Results
→ Extract Product List
→ Display First 5 Products
→ Open First Product
→ Click Add to Cart
→ Verify Cart Count
→ Display PASS/FAIL
→ Close Browser

## Algorithm

1. Launch the Chrome browser.
2. Open Amazon India.
3. Locate the search box.
4. Enter "laptop" and press Enter.
5. Wait until the search results are displayed.
6. Retrieve the available products.
7. Display the first five product names.
8. Select the first product.
9. Open the product details page.
10. Wait for the Add to Cart button.
11. Click Add to Cart.
12. Retrieve the cart count.
13. If the cart count is greater than zero, display "ADD TO CART: PASS".
14. Otherwise, display "ADD TO CART: FAIL".
15. Close the browser.

## Key Selenium Concepts

- WebDriver initialization
- Browser navigation
- Element identification
- ID locator
- CSS Selector
- Explicit Wait
- `find_element()`
- `find_elements()`
- Keyboard actions
- Text extraction
- Element clicking
- Exception handling
- Test validation

## Main Selenium Logic

```python
driver = webdriver.Chrome()
driver.maximize_window()

wait = WebDriverWait(driver, 20)

driver.get("https://www.amazon.in/")

search_box = wait.until(
    EC.element_to_be_clickable(
        (By.ID, "twotabsearchtextbox")
    )
)

search_box.send_keys("laptop")
search_box.send_keys(Keys.ENTER)

The script opens Amazon and searches for the required product.

wait.until(
    EC.presence_of_element_located(
        (By.CSS_SELECTOR,
         "div[data-component-type='s-search-result']")
    )
)

products = driver.find_elements(
    By.CSS_SELECTOR,
    "div[data-component-type='s-search-result']"
)

The script waits for the search results and retrieves the product elements.

for i, product in enumerate(products[:5], start=1):
    try:
        name = product.find_element(
            By.CSS_SELECTOR,
            "h2"
        ).text

        print(i, name)

    except Exception:
        continue

The first five product names are extracted and displayed.

first_product = products[0]

product_link = first_product.find_element(
    By.CSS_SELECTOR,
    "h2 a"
)

driver.execute_script(
    "arguments[0].click();",
    product_link
)

The first product is selected and opened.

wait.until(
    EC.presence_of_element_located(
        (By.ID, "productTitle")
    )
)

add_to_cart = wait.until(
    EC.element_to_be_clickable(
        (By.ID, "add-to-cart-button")
    )
)

add_to_cart.click()

The product page is loaded and the Add to Cart button is clicked.

cart_count = wait.until(
    EC.presence_of_element_located(
        (By.ID, "nav-cart-count")
    )
)

if cart_count.text.isdigit() and int(cart_count.text) > 0:
    print("ADD TO CART: PASS")
else:
    print("ADD TO CART: FAIL")
```
<img width="1912" height="992" alt="Screenshot 2026-10-07 101107" src="https://github.com/user-attachments/assets/7fa734e1-dd58-437a-89b2-b7551ed7c6f9" />

<img width="1917" height="982" alt="Screenshot 2026-10-07 101111" src="https://github.com/user-attachments/assets/c5fd592c-f9d6-4152-9f46-4556a5511cbe" />

<img width="1880" height="492" alt="Screenshot 2026-10-07 101123" src="https://github.com/user-attachments/assets/e2fa9d7a-cd32-4531-920e-9f6eae3354f0" />


The cart count is checked to validate whether the product was successfully added.
