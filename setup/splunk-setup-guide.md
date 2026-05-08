# Splunk Setup Guide (macOS)

## Step 1 — Download Splunk Enterprise

1. Go to: https://www.splunk.com/en_us/download/splunk-enterprise.html
2. Create a free Splunk account
3. Download the macOS `.dmg` file
4. Open the `.dmg` and drag Splunk to your Applications folder
5. Open Terminal and start Splunk:

```bash
cd /Applications/Splunk/bin
./splunk start --accept-license
```

6. Open your browser and go to: `http://localhost:8000`
7. Log in with the admin credentials you set during install

---

## Step 2 — Download Splunk Universal Forwarder

1. Go to: https://www.splunk.com/en_us/download/universal-forwarder.html
2. Download macOS version
3. Install it — it runs silently in the background
4. Configure it to forward `/var/log/` to your local Splunk instance:

```bash
cd /Applications/SplunkUniversalForwarder/bin

./splunk add forward-server localhost:9997

./splunk add monitor /var/log/
```

---

## Step 3 — Add Data Inputs in Splunk

1. In Splunk web UI → **Settings → Data Inputs**
2. Add **Files & Directories**
3. Point to `/var/log/`
4. Set sourcetype to `syslog`
5. Save

---

## Step 4 — Verify Logs Are Coming In

In the Splunk search bar, run:

```splunk
index=main | head 20
```

If you see log events — your setup is working. ✅

---

## Step 5 — Create Your Index (Optional but Recommended)

1. Settings → Indexes → New Index
2. Name it: `soc_lab`
3. Use `index=soc_lab` in your searches for cleaner results
