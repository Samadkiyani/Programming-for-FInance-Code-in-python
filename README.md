# Programming-for-FInance-Code-in-python
Programming for finance in Python
Smart Financial Management System**
Done By Abdul Samad Saleem Fast University Islamabad Campus
![th (7)](https://github.com/user-attachments/assets/bbbf6ba6-b110-4972-a308-35084a3afd7e)


🎯 Course Learning Outcomes (CLOs)
Python programs to solve basic financial problems.
Perform data manipulation and analysis using Python libraries.


 Scenario: Smart Financial Management System [20 marks]
SecureBank wants to develop an automated financial management system using Python. Your task is to implement different financial operations step by step.

This system will:
✅ Assess customer eligibility for loans.
✅ Classify investment portfolios based on risk.
✅ Automate loan repayment tracking.
✅ Monitor stock market trends and trigger alerts.
✅ Track currency exchange rates and suggest conversions.

Task is to break down the requirements, write a structured plan, and implement the logic step by step using ipywidgets for interactive user inputs.

![1step](https://github.com/user-attachments/assets/38eb4985-a8a2-402b-9f01-db37caf6dd43)


🟢 Part 1: Loan Eligibility & Interest Rate Calculation [4 marks]
📌 Requirement:
SecureBank only approves loans if the customer meets all eligibility criteria. The system should:
✔ Check if the customer is employed.
✔ Verify if the income is at least PKR 50,000.
✔ Check credit score:

750+ → 5% Interest Rate
650 - 749 → 8% Interest Rate
Below 650 → Loan Rejected
✔ If the applicant is unemployed, the loan is rejected immediately.

Implementation of code
import ipywidgets as widgets
from IPython.display import display

    def check_loan_eligibility(employment_status, income, credit_score):
    if employment_status == 'Unemployed':
        return "Loan Rejected: Applicant is unemployed."

    if income < 50000:
        return "Loan Rejected: Minimum income requirement not met."

    if credit_score >= 750:
        return "Loan Approved: Interest Rate = 5%"
    elif 650 <= credit_score < 750:
        return "Loan Approved: Interest Rate = 8%"
    else:
        return "Loan Rejected: Credit score too low."


    employment_status_widget = widgets.Dropdown(
    options=['Employed', 'Unemployed'],
    value='Employed',
    description='Employment:',
    )

    income_widget = widgets.IntText(
    value=50000,
    description='Income:',
    )

    credit_score_widget = widgets.IntSlider(
    value=700,
    min=300,
    max=850,
    step=10,
    description='Credit Score:',
    )

    output = widgets.Output()

    def on_button_click(b):
    with output:
        output.clear_output()
        result = check_loan_eligibility(
            employment_status_widget.value,
            income_widget.value,
            credit_score_widget.value
        )
        print(result)

    button = widgets.Button(description="Check Loan Eligibility")
    button.on_click(on_button_click)

    display(employment_status_widget, income_widget, credit_score_widget, button, output)

![2 step](https://github.com/user-attachments/assets/4383384d-c4ba-4d8c-90f8-a1beca59e091)

🟢 Part 2: Investment Risk Assessment:

📌 Requirement:
SecureBank offers investment analysis services. The system should evaluate a portfolio of stocks and classify the risk level based on stock returns:
✔ If any stock has a negative return, the portfolio is High Risk.
✔ If all stocks have positive returns, but at least one return is below 5%, classify as Medium Risk.
✔ If all stock returns are 5% or above, classify as Low Risk.

Implementation Steps:
🔹 Step 1:  loops to iterate through the list of stock returns.
🔹 Step 2:  if-elif conditions to classify the risk.
🔹 Step 3:  Python program using ipywidgets to allow users to input stock returns interactively and receive a risk assessment.

Implementation:

    import ipywidgets as widgets
    from IPython.display import display

    def assess_risk(returns):
    try:
        returns = [float(r) for r in returns.split(',')]
        if any(r < 0 for r in returns):
            risk = "High Risk"
        elif all(r >= 5 for r in returns):
            risk = "Low Risk"
        else:
            risk = "Medium Risk"

        result_label.value = f"Portfolio Risk Level: {risk}"
    except ValueError:
        result_label.value = "Invalid input! Please enter numeric values separated by commas."


    returns_input = widgets.Text(placeholder="Enter stock returns")
    assess_button = widgets.Button(description="Assess Risk")
    result_label = widgets.Label(value="")

    def on_button_click(b):
    assess_risk(returns_input.value)

    assess_button.on_click(on_button_click)

    display(returns_input, assess_button, result_label)

![s3](https://github.com/user-attachments/assets/a3c334c6-6d0a-4f7b-91ec-3f5472a77be2)

		
Part 3: Loan Repayment Tracker
📌 Requirement:
Customers who receive a loan should be able to track their loan balance as they make monthly payments. The system should:
✔ Start with an initial loan balance (e.g., PKR 500,000).
✔ Deduct a fixed monthly payment (e.g., PKR 25,000).
✔ Continue tracking until loan balance reaches zero.
✔ Display the remaining balance after each payment.

Implementation Steps:
🔹 Step 1:  appropriate loop (for or while).
🔹 Step 2:  loop stops once the loan is fully paid.
🔹 Step 3: Python program using ipywidgets to simulate loan repayment interactively.	

Implementation:

		import ipywidgets as widgets
from IPython.display import display

    def track_loan(initial_balance, monthly_payment):
    balance = initial_balance
    output.clear_output()

    with output:
        print("Loan Repayment Tracker")
        print("----------------------")
        while balance > 0:
            print(f"Remaining Balance: PKR {balance}")
            balance -= monthly_payment
            if balance < 0:
                balance = 0
        print(f"Final Balance: PKR {balance} (Loan Fully Paid)")


    initial_balance_widget = widgets.IntText(value=500000, description="Loan Amount:")
    monthly_payment_widget = widgets.IntText(value=25000, description="Monthly Payment:")
    track_button = widgets.Button(description="Track Loan")
    output = widgets.Output()

    def on_button_click(b):
    track_loan(initial_balance_widget.value, monthly_payment_widget.value)

    track_button.on_click(on_button_click)

    display(initial_balance_widget, monthly_payment_widget, track_button, output)

![step4](https://github.com/user-attachments/assets/b3b29dc6-caa3-4d9e-9490-3a89cac18915)

🟢 Part 4: Stock Price Monitoring and Trading Strategy 
📌 Requirement:
A stock trader wants to track stock prices daily and sell when the price reaches PKR 200. The system should:
✔ Iterate through a list of stock prices.
✔ Skip missing stock data (None values).
✔ Stop tracking once the price reaches PKR 200.

Implementation Steps:
🔹 Step 1: Handle missing stock data using continue.
🔹 Step 2: Stop tracking once the stock hits the target price (break).
🔹 Step 3: Python program using ipywidgets to process stock prices interactively and trigger alerts when conditions are met.

Implementation:

    import ipywidgets as widgets
    from IPython.display import display

    def track_stock_prices(prices):
    output.clear_output()
    for price in prices:
        if price is None:
            continue

        with output:
            print(f"Tracking stock price: PKR {price}")

        if price >= 200:
            with output:
                print("Target price reached! Consider selling.")
            break


    prices_input = widgets.Text(
    placeholder="Enter stock prices separated by commas"
    )

    track_button = widgets.Button(description="Track Prices")
    output = widgets.Output()

    def on_button_click(b):
    try:
        prices = [int(x.strip()) if x.strip() else None for x in prices_input.value.split(',')]
        track_stock_prices(prices)
    except ValueError:
        with output:
            print("⚠ Please enter valid numbers separated by commas!")

    track_button.on_click(on_button_click)

    display(prices_input, track_button, output)

![th (8)](https://github.com/user-attachments/assets/e3c5c5a0-5b60-46b3-a46c-6544946e5bc5)

Part 5: Currency Exchange Rate Tracker 
📌 Requirement:
SecureBank provides real-time currency exchange tracking. The system should:
✔ Start at PKR 290/USD.
✔ Increase by 1 PKR per day until it reaches PKR 300/USD.
✔ Print exchange rates daily and stop when the target rate is reached.

Implementation Steps:
🔹 Step 1: Suitable loop (for or while).
🔹 Step 2: Stop the loop when the exchange rate reaches the target.
🔹 Step 3: Python program using ipywidgets to track the currency exchange rate interactively.

Implementation:

    import ipywidgets as widgets
    from IPython.display import display
    import time

    def track_exchange_rate():

    exchange_rate = 290
    target_rate = 300


    label = widgets.Label(value=f"Current Exchange Rate: PKR {exchange_rate}/USD")
    display(label)

    while exchange_rate <= target_rate:
        label.value = f"Current Exchange Rate: PKR {exchange_rate}/USD"
        time.sleep(0.5)
        exchange_rate += 1
        if exchange_rate > target_rate:
            label.value = "Exchange rate tracking stopped. Target reached!"
            break


    track_exchange_rate()




