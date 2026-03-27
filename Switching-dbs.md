# Switching the Sage 300 People Public API to a New Database

## Config File Locations

| File | Folder |
|------|--------|
| `VIP.SchedulerConfig.exe.config` | `c:\Sage\People\SchedulerService\` |
| `SagePeoplePublicAPIService.exe.config` | `c:\Sage\People\SagePublicAPI\` |

---

## Step 1 — Update the Sage Hosting Connection

1. Open the Sage 300 People hosting configuration tool (e.g., Sage Config Manager).
2. Change the target database to the desired one (e.g., `devtest`).
3. Save and apply — this regenerates the encrypted connection string.

---

## Step 2 — Copy the Connection String from the Scheduler Config

1. Open `c:\Sage\People\SchedulerService\VIP.SchedulerConfig.exe.config`.
2. Copy the entire `<connectionStrings>` block:

```xml
<connectionStrings>
  <add name="VIPDB" connectionString="<encrypted_string_here>" providerName="System.Data.SqlClient" />
</connectionStrings>
```

---

## Step 3 — Replace the Connection String in the Public API Config

1. Open `c:\Sage\People\SagePublicAPI\SagePeoplePublicAPIService.exe.config`.
2. Find and replace lines 12–14 (the existing `<connectionStrings>` block):

```xml
<connectionStrings>
  <add name="VIPDB" connectionString="<old_encrypted_string>" providerName="System.Data.SqlClient" />
</connectionStrings>
```

3. Paste in the block copied from Step 2.
4. Save the file.

---

## Step 4 — Restart the Public API Service

