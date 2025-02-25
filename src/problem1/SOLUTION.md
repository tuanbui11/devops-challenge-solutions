Provide your CLI command here:

# Solution to Validate and Verify the CLI Command

## 1. Verify Data Extraction (`grep` + `awk`)

Before sending HTTP GET requests, ensure that the correct `order_id` values are extracted from the file:

```bash
grep '"symbol": "TSLA", "quantity":' ./transaction-log.txt | grep '"side": "sell"' | awk -F'"' '{print $4}'
```

✅ Expected output: A list of order IDs (e.g., `12346`, `12362`), ensuring the filtering works correctly.

---

## 2. Test a Single HTTP GET Request with `curl`

Once an order ID is obtained, test the API call manually:

```bash
curl -s "https://example.com/api/12346"
```

✅ Expected output: A valid JSON response from the API.

---

## 3. Validate Full Pipeline Before Execution

Instead of immediately running `curl`, print the URLs to verify correctness:

```bash
grep '"symbol": "TSLA", "quantity":' ./transaction-log.txt | grep '"side": "sell"' | awk -F'"' '{print $4}' | xargs -I {} echo "https://example.com/api/{}"
```

✅ Expected output:

```
https://example.com/api/12346  
https://example.com/api/12362  
```

---

## 4. Run a Single Test Request and Save Output

Test a single API request and store the response:

```bash
curl -s "https://example.com/api/12346" -o test_output.txt
cat test_output.txt
```

✅ Expected output: JSON data confirming that API responses are correctly received.

---

## 5. Execute the Full Command and Verify Results

Once all checks are validated, run the complete command:

```bash
grep '"symbol": "TSLA", "quantity":' ./transaction-log.txt | grep '"side": "sell"' | awk -F'"' '{print $4}' | xargs -I {} curl -s "https://example.com/api/{}" >> ./output.txt
```

Then, verify the output:

```bash
cat output.txt
```

✅ Expected output: Contains API responses confirming that requests were executed correctly.

## Summary of Verification Steps

✅ **Step 1:** Ensure `order_id` extraction works (`grep` + `awk`).\
✅ **Step 2:** Test `curl` on a single `order_id`.\
✅ **Step 3:** Print URLs to verify correctness before execution.\
✅ **Step 4:** Run a test request and save the response.\
✅ **Step 5:** Execute the full command and check `output.txt`.
