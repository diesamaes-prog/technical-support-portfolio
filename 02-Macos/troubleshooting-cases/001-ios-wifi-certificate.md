# macOS Incident 001 — Wi-Fi Connection Fails Due to Certificate Issue

## Incident

A user contacted the Service Desk because their Mac could no longer connect to the company's secure Wi-Fi network.

The user reported that the Mac could see the corporate Wi-Fi network, but the connection would fail after entering their credentials. The same credentials were working on other company systems.

The issue started after the Mac had been restarted.

The user was able to connect to a guest Wi-Fi network, which confirmed that the wireless hardware was working and that the Mac could connect to a wireless network.

The problem was specific to the corporate network.

## Troubleshooting

I first confirmed that the corporate Wi-Fi network was visible from the Mac.

The network appeared in the available Wi-Fi networks, but the connection failed during authentication.

I connected the Mac to the guest network temporarily to confirm that general Wi-Fi connectivity was working.

The Mac successfully connected to the guest network and was able to access the Internet.

This ruled out a general Wi-Fi adapter or hardware problem.

I then attempted to connect to the corporate network again and observed the authentication process.

The Mac prompted for authentication but was unable to complete the connection.

Because the corporate network uses certificate-based authentication, I checked the certificates available on the Mac through **Keychain Access**.

The certificate used for authentication was present, but it was expired.

The expiration date matched the approximate time when the user first noticed the problem.

## Root Cause

The Mac was attempting to authenticate to the corporate Wi-Fi network using an expired client certificate.

The wireless hardware and network connection were functioning correctly. The failure was occurring during the authentication stage because the certificate required by the corporate 802.1X configuration was no longer valid.

## Resolution

Following the organization's certificate deployment procedure, the expired certificate was removed from the affected user configuration and the current certificate was deployed to the Mac.

The corporate Wi-Fi profile was then refreshed.

The user attempted to connect to the corporate network again.

The Mac successfully completed the authentication process and connected to the network.

## Verification

After reconnecting, I verified that:

* The Mac was connected to the corporate SSID.
* The device received a valid IP address.
* The default gateway was reachable.
* DNS resolution was working.
* Internal resources were accessible.
* Internet access was restored.

The user confirmed that they could access the resources required for their work.

## Ticket Notes

**Issue:** Mac unable to connect to corporate Wi-Fi.

**Affected network:** Corporate 802.1X Wi-Fi

**Initial observation:** Corporate SSID visible, authentication unsuccessful.

**Additional test:** Guest Wi-Fi connection successful.

**Cause:** Expired client certificate used for wireless authentication.

**Resolution:** Replaced the expired certificate and refreshed the corporate Wi-Fi configuration.

**Verification:** Successful 802.1X authentication and network connectivity restored.

**Status:** Resolved.

## Technical Details

The important distinction in this incident was between **Wi-Fi connectivity** and **network authentication**.

The Mac's wireless adapter was functioning because it could detect the corporate network and successfully connect to the guest network.

The failure occurred during the authentication process used by the corporate network.

The corporate environment used **802.1X certificate-based authentication**, so the certificate stored on the Mac had to be valid before the device could complete the connection.

Keychain Access was used to inspect the certificate and confirm that it was expired.

The troubleshooting path was:

```text
Corporate Wi-Fi visible
        ↓
Authentication fails
        ↓
Test guest Wi-Fi
        ↓
Guest Wi-Fi works
        ↓
Wireless hardware/network adapter OK
        ↓
Check corporate authentication
        ↓
Inspect certificates in Keychain Access
        ↓
Expired client certificate identified
        ↓
Deploy current certificate
        ↓
Refresh Wi-Fi configuration
        ↓
Corporate Wi-Fi connects successfully
```

## macOS Tools Used

**Keychain Access**

Used to inspect certificates stored on the Mac and verify their validity and expiration.

**Wi-Fi Settings**

Used to review available networks and reconnect to the corporate SSID.

**Terminal**

Network connectivity can be verified after authentication with commands such as:

```bash
ifconfig
```

```bash
ping -c 4 <gateway>
```

```bash
nslookup <internal-domain>
```

These checks help confirm that the issue has moved beyond authentication and that the Mac has normal network connectivity.

## Final Resolution

The expired wireless authentication certificate was replaced with a valid certificate issued through the organization's approved certificate deployment process.

After refreshing the Wi-Fi configuration, the Mac successfully authenticated to the corporate network and normal connectivity was restored.

No hardware replacement was required.

