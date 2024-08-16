
This example serves a csv file.

```php
// Located inside a controller
    public function export() {

// The file serving functionality is defined by the header `Content-Type` and `Content-Disposition`
        $headers = [
            "Content-Type" => "text/csv",
            "Content-Disposition" => "attatchment; filename=orders.csv",
            "Cache-Control" => "must-revalidate, post-check=8, pre-check=0",
            "Expires" => "0",
        ];

// This callback retrieves all data from the database and formats it into csv
        $callback = function () {
            $orders = Order::all();
            $file = fopen("php://output", "a");

            fputcsv($file, ["ID", "Name", "Email", "Product Title", "Price", "Quantity"]);

            foreach ($orders as $order) {
                fputcsv($file, [
                    $order->id,
                    $order->name,
                    $order->email,
                    "", "", ""
                ]);

                foreach ($order->orderItems as $orderItem) {
                    fputcsv($file, [
                        "", "", "",
                        $orderItem->product_title,
                        $orderItem->price,
                        $orderItem->quantity,
                    ]);
                }
            }

            fclose($file);
        };

// Lastly, it will be returned as a Response::stream taking in the arguments (callback|file, status, headers)
        return \Response::stream($callback, 200, $headers);
    }
```


it can be accessed by assigning a route in `routes/api.php`
```php
     Route::post("orders/export", [OrderController::class, "export"]);
```