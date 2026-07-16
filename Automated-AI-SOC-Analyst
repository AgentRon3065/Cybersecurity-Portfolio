from google import genai
import os
import sys

# 1. Read local logs
try:
    with open("server_logs.txt", "r") as file:
        log_data = file.readlines()
except FileNotFoundError:
    print("❌ Error: server_logs.txt not found.")
    sys.exit(1)

print("🔍 Reading local server logs...")

# 2. Local Python rule matching (Runs offline)
failed_attempts = 0
suspicious_ips = set()

for line in log_data:
    if "Login Failed" in line or "failed" in line.lower():
        failed_attempts += 1
        parts = line.split("IP:")
        if len(parts) > 1:
            ip = parts[1].split("-")[0].strip()
            suspicious_ips.add(ip)

if failed_attempts >= 3:
    print(f"\n🚨 [LOCAL ALERT] Brute Force Signature Detected!")
    print(f"⚠️ Total Failed Attempts: {failed_attempts}")
    print(f"🛑 Flagged Attacker IPs: {list(suspicious_ips)}")
else:
    print("\n✅ [LOCAL CHECK] System logs appear safe. No brute force signatures found.")

# 3. Try AI analysis as a premium feature
if os.environ.get("GEMINI_API_KEY"):
    print("\n🤖 Connecting to Gemini for Advanced AI Threat Intelligence...")
    client = genai.Client()
    
    prompt = f"Analyze these logs for security risks and give remediation advice:\n" + "".join(log_data)
    
    try:
        response = client.models.generate_content(
            model='gemini-3.5-flash',
            contents=prompt,
        )
        print("\n🎉 AI Threat Intelligence Report:")
        print(response.text)
    except Exception as e:
        print(f"\nℹ️ AI Server Busy ({e}). Relying on Local Rule Engine.")
else:
    print("\nℹ️ Skipping AI Analysis (API Key not set).")
