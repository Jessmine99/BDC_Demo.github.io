# Analytic Modeling

### Create Sales Order Analytic Model

1️⃣ Go to `Data Builder` → `New Analytic Model` and drag `Sales Order Fact` onto the canvas.

2️⃣ In the pop-up window, keep all measures, attributes, and associated dimensions selected and click `Add`.

3️⃣ In the `Properties Panel`, enter `Sales Order Analytic Model` as the Analytic Model name.

### Add Projection

4️⃣ Click the `Sales Order Fact` node and in the `Properties Panel` **unselect**:
   - `DOCUMENT_ID`
   - `DOCUMENT_ID_POSITION`
   - `SHIP_TO_CUSTOMER`
   - `TRADE_DESCRIPTION`

5️⃣ Click the `Material DIM` node and **unselect**:
   - `BASE_UOM_CODE`
   - `MAXIMUM_PACKAGE_SIZE`

6️⃣ Click the `Customer DIM` node and **unselect**:
   - `LATITUDE`
   - `LONGITUDE`
   - `CUSTOMER_EFFECTIVE_DATE`
   - `CUSTOMER_CREATED_DATE`

### Create Calculated Measures

7️⃣ Click the `Fact Sources` node → `Measures` → `+` → `Calculated Measure`.

8️⃣ Create:
   - Business Name: `Avg Order Price`
   - Expression: `ORDER_AMOUNT_EURO / QUANTITY`
   - Click `Validate`.

9️⃣ Repeat to create:
   - Business Name: `% Discount`
   - Expression: `DISCOUNT_AMOUNT_DOCUMENT_CURRENCY` / `ORDER_AMOUNT_DOCUMENT_CURRENCY`
   - Click `Validate`.

### Add Restricted Measures

🔟 In Measures → `+` → `Restricted Measure`, create:

   - Business Name: `France revenue`
   - Source Measure: `NET_VALUE_AMOUNT_DOCUMENT_CURRENCY`
   - Expression: `COUNTRY_NAME_SOLD_ `= `'France'`
   - Click `Validate`.

1️⃣1️⃣ Create another `Restricted Measure`:

   - Business Name: `Invoice_gross_revenue`
   - Source Measure: `ORDER_AMOUNT_EURO`
   - Expression: `STATUS` = `'7'`
   - Click `Validate`.

### Define Count Distinct Measure

1️⃣2️⃣ In Measures → `+` → `Count Distinct Measure`:
   - Business Name: `Customer Count`
   - Dimension: `SOLD_TO_CUSTOMER`
   - Enable `Is Auxiliary`.

1️⃣3️⃣ Add a `Calculated Measure`:
   - Business Name: `Avg Spend per customer (EUR)`
   - Expression:
     `NET_VALUE_AMOUNT_DOCUMENT_CURRENCY * (ORDER_AMOUNT_EURO / ORDER_AMOUNT_DOCUMENT_CURRENCY) / Customer_Count`
   - Click `Validate`.

*Note: `ORDER_AMOUNT_EURO / ORDER_AMOUNT_DOCUMENT_CURRENCY` represents the exchange rate from document currency to Euro.*

### Define Exception Aggregation Measure

1️⃣4️⃣ Add a `Calculated Measure`:
   - Business Name: `High value products`
   - Expression: `ORDER_AMOUNT_EURO > 900`
   - Click `Validate`.

1️⃣5️⃣ Scroll to `Exception Aggregation` and set:
   - Type: `SUM`
   - Dimension: `MATERIAL (Sales Order Fact)`

### Add Filter Variable

1️⃣6️⃣ In the `Variables` section, add a `Filter Variable`:
   - Dimension: `Year (ORDER_DATE_KEY)`
   - Filter Type: `Interval`
   - From: `2024` To: `2025`

### Save & Preview

1️⃣7️⃣ Click Save and Deploy.

1️⃣8️⃣ Click `Preview` (top right) to validate the analytic model.
