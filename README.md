# Razorpay Go Client

Golang bindings for interacting with the Razorpay API

This is primarily meant for merchants who wish to perform interactions with the Razorpay API programatically

## Usage
You need to setup your key and secret using the following:
You can find your API keys at <https://dashboard.razorpay.com/#/app/keys>.

```
import (
razorpay "github.com/razorpay/razorpay-go"
)

client := razorpay.Client("<YOUR_API_KEY>", "<YOUR_API_SECRET>")

```

Note: All calls below return a `map[string]interface{} and error(`error`) object in response
### Payments

- Fetch all payments
    ```
    body, err := client.Payment.All()
    ```
- Fetch a particular payment
    ```
    body, err := client.Payment.Fetch(<payment_id>)
    ```
- Capture a payment
    ```
    body, err := client.Payment.Capture(<payment_id>, <amount>)
    ```
    Note: amount is in paisa
- Refund a payment
    ```
    body, err := client.Payment.Refund(<payment_id>, <amount_to_be_refunded>)
    ```

### Refunds
- Fetch all refunds
    ```
    body, err := client.Refund.All()
    ```
- Fetch a particular refund
    ```
    body, err := client.Refund.Fetch(<refund_id>)
    ```

### Orders
- Create a new order

    ```
    data := map[string]interface{}{
        "amount":          1234,
        "currency":        "INR",
        "receipt_id":      "some_receipt_id",
        "payment_capture": 1,
    }
    body, err := client.Order.Create(data)
    ```
    Note: data is a map and should contain these keys
        amount           : amount of order(in paisa)
        currency         : currency of order
        receipt          : receipt id of order
        payment_capture  : 1 if capture should be done automatically or else 0
        notes(optional)  : optional notes for order

- Fetch a particular order
    ```
    body, err := client.Order.Fetch(<order_id>)
    ```
- Fetch all orders
    ```
    body, err := client.Order.All()
    ```
- Fetch all payments for order
    ```
    body, err := client.Order.Payments(<order_id>)
    ```
